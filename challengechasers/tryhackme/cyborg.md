# Cyborg

## I- Scanning

On utilise nmap `nmap -sC -sV <target ip>` ou tu peux faire un nmap agressif `nmap -A <target ip>` ou encore `nmap -sV <target ip>`

On regarde les ports ouvert et en fonction on peut essayer de se connecter aux services disponible (ex: HTTP, SSH, SMB etc…)

Sur cette machine, nous avons SSH et un serveur web qui sont accessible.

## II- Enumération

On peut aller sur le serveur web voir si l’ont trouve quelque chose d’intéressant.

On utilise **gobuster** lors de cette étape pour découvrir les dossier présent sous la page web:

`gobuster dir -u http://<ip-cible> -w <wordlist>`

chemin de wordlists:

* /usr/share/wordlists/dirb/common.txt
* /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
* /usr/share/wordlists/rockyou.txt

Nous avons trouvé deux dossiers intéressant: /admin et /etc

Dans /etc nous avons trouvé un autre dossier /squid contenant le mot de passe haché de Apache. On utilise John the Ripper pour crack le mot de passe.

```powershell
john —wordlist=/usr/share/wordlists/rockyou.txt <fichier.txt>
```

Nous avons également un username: music\_archive.

Sur la page /admin, dans “Archive”, nous avons la possibilité de télécharger un “archive.tar”

Pour extract:

```powershell
tar -xvf archive.tar
```

Il semble que Borg crypte les fichiers et les sauvegarde. Nous nous souvenons que notre utilisateur (éventuellement administrateur) Alex était un amateur de musique, qui sauvegardait ses fichiers sous "music\_archive". Prenons un moment pour rechercher comment Borg est utilisé. Tout d'abord, nous devons l'installer.

Installation des dépendances selon la documentation :

[https://borgbackup.readthedocs.io/en/stable/installation.html](https://borgbackup.readthedocs.io/en/stable/installation.html)

Dans /home/alex, on peut essayer de chercher des fichiers intéressant

```powershell
find . -type f
```

Nous obtenons un fichier note.txt qui contient des identifiants, si ont les utilisent pour se connecter en SSH cela fonctionne. Nous avons notre premier flag !

## IV- Escalation de privilège

Comme toujours, on vérifie les droits de notre user:

```powershell
sudo -l 
```

Dans notre cas on peut exécuter “/backup.sh” en tant que root. On peut jeter un œil à ce script:

```powershell
cat /etc/mp3backups/backup.sh
```

On donne les permissions de modifier ce fichier

```powershell
chmod +w backup.sh
```

Nous pouvons maintenant exécuter le script

```powershell
sudo -r root /etc/mp3backups/backup.sh -c bash
```

Nous sommes en root sur la machine ! Si jamais vous n’avez aucun retour des commandes lorsque vous êtes sur le shell root, vous pouvez en root faire:

```powershell
chmod 4577 /bin/bash
```

Quitter puis faire bash -p

Alternative: faire un reverse shell, lancer netcat puis exécuter le script)

Ensuite naviguez dans root et trouver votre dernier flag.
