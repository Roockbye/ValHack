# Bounty Hacker

## I- Scanning

On utilise nmap `nmap -sC -sV <target ip>` ou tu peux faire un nmap agressif `nmap -A <target ip>` ou encore `nmap -sV <target ip>`

On regarde les ports ouvert et en fonction on peut essayer de se connecter aux services disponible (ex: HTTP, SSH, SMB etc…)

Nous avons FTP, SSH et un serveur web avec Apache qui tourne, d’ouvert sur cette machine.

## II- Enumération

On peut aller sur le serveur web voir si l’ont trouve quelque chose d’intéressant. On peut tenter gobuster mais nous n’aurons rien de spécial dans ce cas.

Nous allons donc partir sur la piste du FTP, comme préciser dans le nmap Anonymous login est activé, nous pouvons donc nous connecté sans connaitre les identifiants

```powershell
ftp <ip-cible>
```

On peut faire un dir pour voir s’il y a des fichiers intéressant ainsi qu’un mget \<fichier> ou mget \* pour télécharger les fichiers sur notre machine et ainsi pouvoir les consulter.

Un fichier est une wordlist qui pourra nous servir pour faire du bruteforce et obtenir le mot de passe et le deuxième fichier contient le username dont on a besoin. Nous pouvons maintenant bruteforce SSH !

## III- Exploitation

Nous allons cette fois utiliser hydra pour bruteforce.

```powershell
hydra -l username -P <fichier-list-pwd> ssh://<ip-cible>
```

Nous obtenons le mot de passe pour nous connecter en SSH

```powershell
ssh username@<ip-cible>
```

On peut maintenant se déplacer sur la machine cible, pour récupérer le premier flag.

## IV- Escalation de privilège

On vérifie en premier lieu nos permissions:

```powershell
sudo -l 
```

Notre utilisateur actuel peut exécuter les privilèges root

Ce dernier peut utiliser “tar” car l’output est “(root) /bin/tar on check sur le site :[https://gtfobins.github.io/](https://gtfobins.github.io/)

```powershell
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

On obtient un shell root, on peut donc se balader dans root et obtenir notre dernier flag !
