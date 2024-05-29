# Default Configuration FTP

Le serveur FTP vsFTPd est couramment utilisé sur les distributions Linux. Sa configuration par défaut se trouve dans /etc/vsftpd.conf. 


## Install vsFTPd

L'installation se fait via la commande :
```bash 
sudo apt install vsftpd
```

## vsFTPd Config File

Le fichier /etc/vsftpd.conf contient des paramètres tels que `listen`, `anonymous_enable`, etc. 
```bash 
cat /etc/vsftpd.conf | grep -v "#"
```

Certains paramètres pertinents sont résumés ci-dessous :

| Paramètre                      | Description                                                         |
|--------------------------------|---------------------------------------------------------------------|
| listen=NO                      | Exécution via inetd ou en tant que démon autonome ?               |
| listen_ipv6=YES                | Écouter sur IPv6 ?                                                 |
| anonymous_enable=NO            | Activer l'accès anonyme ?                                          |
| local_enable=YES               | Autoriser les utilisateurs locaux à se connecter ?                |
| dirmessage_enable=YES          | Afficher des messages de répertoire actif lors de l'accès ?       |
| use_localtime=YES              | Utiliser l'heure locale ?                                          |
| xferlog_enable=YES             | Activer la journalisation des téléchargements/envois ?            |
| connect_from_port_20=YES       | Se connecter à partir du port 20 ?                                 |
| secure_chroot_dir=/var/run/vsftpd/empty | Nom d'un répertoire vide sécurisé ?                         |
| pam_service_name=vsftpd        | Nom du service PAM utilisé par vsftpd.                            |
| rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem | Emplacement du certificat RSA pour les connexions SSL.  |
| rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key | Emplacement de la clé privée RSA.                     |
| ssl_enable=NO                  | Activer les connexions SSL ?                                      |


## FTPUSERS

Le fichier /etc/ftpusers permet de restreindre l'accès.

```bash 
cat /etc/ftpusers
```

# Dangerous Settings

| Setting                      | Description                                                         |
|------------------------------|---------------------------------------------------------------------|
| anonymous_enable=YES         | Autoriser la connexion anonyme ?                                   |
| anon_upload_enable=YES       | Autoriser les utilisateurs anonymes à téléverser des fichiers ?    |
| anon_mkdir_write_enable=YES | Autoriser les utilisateurs anonymes à créer de nouveaux répertoires ? |
| no_anon_password=YES         | Ne pas demander de mot de passe aux utilisateurs anonymes ?        |
| anon_root=/home/username/ftp | Répertoire pour les utilisateurs anonymes.                          |
| write_enable=YES             | Autoriser l'utilisation des commandes FTP : STOR, DELE, RNFR, RNTO, MKD, RMD, APPE et SITE ? |



