# Footprinting the Service

## Scripts Nmap FTP

```bash
sudo nmap --script-updatedb
```

Les scripts Nmap pour FTP se trouvent dans le répertoire /usr/share/nmap/scripts/ sur le Pwnbox, mais vous pouvez également les trouver sur vos systèmes en exécutant la commande suivante :

```bash
find / -type f -name ftp* 2>/dev/null | grep scripts
```

## Nmap

Vous pouvez analyser un serveur FTP avec Nmap en spécifiant le port 21, qui est le port par défaut pour FTP. Voici une commande d'analyse de base avec Nmap :

```bash
sudo nmap -sV -p21 -sC -A 10.129.14.136
```

### Exemple:

```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rwxrwxrwx    1 ftp      ftp       8138592 Sep 16 17:24 Calendar.pptx [NSE: writeable]
| drwxrwxrwx    4 ftp      ftp          4096 Sep 16 17:57 Clients [NSE: writeable]
| drwxrwxrwx    2 ftp      ftp          4096 Sep 16 18:05 Documents [NSE: writeable]
```

---

## Nmap Script Trace

Le suivi des scripts Nmap vous permet de voir les commandes envoyées et les réponses reçues du serveur scanné. Voici comment activer le suivi de script Nmap :

```bash
sudo nmap -sV -p21 -sC -A 10.129.14.136 --script-trace

Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 13:54 CEST                                                                                                                                                   
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 8 [10.129.14.136:21]                                   
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 16 [10.129.14.136:21]             
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 24 [10.129.14.136:21]
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 32 [10.129.14.136:21]
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #1 [10.129.14.136:21] (timeout: 7000ms) EID 42
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #2 [10.129.14.136:21] (timeout: 9000ms) EID 50
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #3 [10.129.14.136:21] (timeout: 7000ms) EID 58
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #4 [10.129.14.136:21] (timeout: 11000ms) EID 66
NSE: TCP 10.10.14.4:54226 > 10.129.14.136:21 | CONNECT
NSE: TCP 10.10.14.4:54228 > 10.129.14.136:21 | CONNECT
NSE: TCP 10.10.14.4:54230 > 10.129.14.136:21 | CONNECT
NSE: TCP 10.10.14.4:54232 > 10.129.14.136:21 | CONNECT
NSOCK INFO [11.4660s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 50 [10.129.14.136:21] (41 bytes): 220 Welcome to HTB-Academy FTP service...
NSOCK INFO [11.4660s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 58 [10.129.14.136:21] (41 bytes): 220 Welcome to HTB-Academy FTP service...
NSE: TCP 10.10.14.4:54228 < 10.129.14.136:21 | 220 Welcome to HTB-Academy FTP service.
```
---

## Service Interaction

Vous pouvez interagir avec le service FTP en utilisant des outils tels que netcat ou telnet. Voici comment se connecter au service FTP avec netcat :

```bash
nc -nv 10.129.14.136 21
```

Ou avec telnet :

```bash
telnet 10.129.14.136 21
```

Si le serveur FTP utilise le chiffrement TLS/SSL, vous pouvez utiliser openssl pour vous connecter. Voici comment vous pouvez le faire :

```bash
openssl s_client -connect 10.129.14.136:21 -starttls ftp
```