# Commandes Nmap pour la Découverte d'Hôte

## Analyser une Plage d'Adresses IP

```shell
📝 sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```

- **Description:**
    - Analyse la plage d'adresses IP spécifiée.
    - Désactive l'analyse des ports.
    - Stocke les résultats dans tous les formats commençant par le nom 'tnet'.

## Analyser une Liste d'Adresses IP à partir d'un Fichier

```shell
📝 sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
```
- **Description:**
    - Analyse les adresses IP spécifiées dans le fichier `hosts.lst`.
    - Désactive l'analyse des ports.
    - Stocke les résultats dans tous les formats commençant par le nom 'tnet'.

## Analyser Plusieurs Adresses IP spécifique

```shell
📝 sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20 | grep for | cut -d" " -f5
```

- **Description:**
    - Analyse les adresses IP spécifiées individuellement.
    - Désactive l'analyse des ports.
    - Stocke les résultats dans tous les formats commençant par le nom 'tnet'.

## Analyser une Plage d'Adresses IP Spécifiques

```shell
📝 sudo nmap -sn -oA tnet 10.129.2.18-20 | grep for | cut -d" " -f5
```
- **Description:**
    - Analyse la plage d'adresses IP spécifiée.
    - Désactive l'analyse des ports.
    - Stocke les résultats dans tous les formats commençant par le nom 'tnet'.

## Analyser une seule Adresse IP
```shell
📝 sudo nmap 10.129.2.18 -sn -oA host
```
- **Description:**
    - Analyse une seule adresse IP pour déterminer si elle est active.
    - Désactive l'analyse des ports.
    - Stocke les résultats dans tous les formats commençant par le nom 'host'.

## Analyser une Seule Adresse IP avec Trace de Paquets

```shell
📝 sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace
```
- **Description:**
    - Analyse une seule adresse IP avec suivi des paquets.
    - Désactive l'analyse des ports.
    - Effectue l'analyse ping en utilisant les requêtes d'écho ICMP sur la cible.
    - Affiche tous les paquets envoyés et reçus.

## Analyser une Seule Adresse IP avec Désactivation des ping ARP

``` shell
📝 sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping`
```
- **Description:**
    - Analyse une seule adresse IP avec désactivation des pings ARP.
    - Désactive l'analyse des ports.
    - Effectue l'analyse ping en utilisant les requêtes d'écho ICMP sur la cible.
    - Affiche tous les paquets envoyés et reçus.

# Voici un tableau avec les options importantes 

`-sM` : Certains pare-feu laisseront passer ces paquets ACK, tandis que d'autres les bloqueront. Cela peut aider à identifier le type de pare-feu utilisé sur le réseau cible.

-sS : Silencieux (SYN > SYN,ACK > au lieu de renvoyer un ACK il bloque la connexion)

`-sI ZOMBIE_IP` : Cette option spécifie une liste d'hôtes zombies à utiliser lors d'un balayage Idle. Dans un balayage Idle, l'attaquant envoie des paquets de sondage au réseau cible, mais au lieu de recevoir des réponses, il utilise des hôtes tiers (les "zombies") pour recevoir ces réponses. Cela peut aider à cacher l'identité de l'attaquant.

|Commande|Description|
|---|---|
|sudo nmap -sN 10.10.41.57|TCP Null Scan - Envoie des paquets sans drapeau TCP|
|sudo nmap -sF 10.10.41.57|TCP FIN Scan - Envoie des paquets avec le drapeau FIN actif|
|sudo nmap -sX 10.10.41.57|TCP Xmas Scan - Envoie des paquets avec les drapeaux URG, PSH et FIN actifs|
|sudo nmap -sM 10.10.41.57|TCP Maimon Scan - Utilise des paquets ACK pour tester les pare-feu|
|sudo nmap -sA 10.10.41.57|TCP ACK Scan - Envoie des paquets ACK pour détecter les ports filtrés|
|sudo nmap -sW 10.10.41.57|TCP Window Scan - Utilise la taille de la fenêtre TCP pour détecter les ports ouverts|
|sudo nmap --scanflags URGACKPSHRSTSYNFIN 10.10.41.57|Balayage TCP personnalisé avec des drapeaux spécifiques|
|sudo nmap -S SPOOFED_IP 10.10.41.57|Spoofed Source IP - Utilise une adresse IP source falsifiée|
|sudo nmap -D DECOY_IP,ME 10.10.41.57|Decoy Scan - Utilise des leurres pour masquer l'origine du balayage|
|sudo nmap -sI ZOMBIE_IP 10.10.41.57|Idle (Zombie) Scan - Utilise des hôtes zombies pour cacher l'attaquant|

|Option|Description|
|---|---|
|-f|Fragmentation IP en 8 octets|
|-ff|Fragmentation IP en 16 octets|
|sudo nmap -sV 10.10.41.57|Version - Détecte les versions des services en cours d'exécution|
|sudo nmap -O 10.10.41.57|Exploitation - Détecte le système d'exploitation|

|Option|Description|
|---|---|
|--source-port PORT_NUM|Spécifie le numéro de port source|
|--data-length NUM|Ajoute des données aléatoires pour atteindre une longueur donnée|

|Option|Description|
|---|---|
|-oN output.txt|Enregistre la sortie au format normal|
|-oG output.txt|Enregistre la sortie au format grepable|
|-oX output.xml|Enregistre la sortie dans le format XML|
|-oA output|Enregistre la sortie dans les formats normal, XML et grepable|

|Option|Purpose|
|---|---|
|--reason|spécifier le numéro de port source|
|-v|verbose|
|-vv|very verbose|
|-d|debugging|
|-dd|more details for debugging|

Les Script se trouvent `/usr/share/nmap/scripts`,

| Catégorie de script | Description                                                                                      |
| ------------------- | ------------------------------------------------------------------------------------------------ |
| auth                | Scripts liés à l'authentification                                                                |
| broadcast           | Découvrez les hôtes en voyant des messages diffusés                                              |
| brute               | Effectuer un audit de mot de passe par force brute par rapport aux connexions                    |
| default             | Scripts par défaut, identiques à -sC                                                             |
| discovery           | Récupérer les informations accessibles, telles que les tables de base de données et les noms DNS |
| dos                 | Détecte les serveurs vulnérables au déni de service (DoS))                                       |
| exploit             | Tentatives d'exploitation de divers services vulnérables                                         |
| external            | Vérifications à l'aide d'un service tiers, tel que Geoplugin et Virustotal                       |
| fuzzer              | Lancez des attaques fuzzing                                                                      |
| intrusive           | Scripts intrusifs tels que les attaques par force brute et l'exploitation                        |
| malware             | Recherche de portes dérobées                                                                     |
| safe                | Des scripts sécurisés qui ne feront pas planter la cible                                         |
| version             | Récupérer les versions du service                                                                |
| vuln                | Vérifie les vulnérabilités ou exploite les services vulnérables                                  |
1. **Nmap - Spécification des scripts**
    
    - Utilisation de scripts avec Nmap pour analyser un port SMTP.
    
| Commande                                   | Description                         |
| ------------------------------------------ | ----------------------------------- |
| `-sC`                                      | Scripts par défaut avec Nmap.       |
| `--script <category>`                      | Scripts d'une catégorie spécifique. |
| `--script <script-name>,<script-name>,...` | Scripts spécifiques définis.        |
    
    - Exemple :

```shell 
📝 sudo nmap 10.129.2.28 -p 25 --script banner,smtp-commands
```

# Énumération du réseau avec Nmap - Performance

La performance d'analyse joue un rôle crucial dans l'exploration étendue de réseaux ou dans des situations de bande passante limitée. Différentes options permettent à Nmap de définir la vitesse (-T <0-5>), la fréquence (--min-parallelism **number**), les délais d'attente (--max-rtt-timeout time) des paquets de test, le nombre de paquets à envoyer simultanément (--min-rate **number**), et le nombre de tentatives (--max-retries **number**) pour les ports analysés.

---
## Délais d'attente

Lorsque Nmap envoie un paquet, le temps nécessaire pour recevoir une réponse (Round-Trip-Time - RTT) peut être crucial. Un délai d'attente initial trop court peut négliger des hôtes.

### **Analyse par défaut**

```bash
📝 sudo nmap 10.129.2.0/24 -F
```

### **RTT optimisé**

```bash
📝 sudo nmap 10.129.2.0/24 -F --initial-rtt-timeout 50ms --max-rtt-timeout 100ms
```

---
## **Nombre maximal de tentatives**

Spécifier le taux de nouvelles tentatives (--max-retries) peut accélérer les analyses, mais peut également entraîner la négligence d'informations importantes.

### **Analyse par défaut**

```bash
📝 sudo nmap 10.129.2.0/24 -F | grep "/tcp" | wc -l
```

### **Nouvelles tentatives réduites**

```bash
📝 sudo nmap 10.129.2.0/24 -F --max-retries 0 | grep "/tcp" | wc -l
```

---
## **Taux**

Le débit de paquets peut être ajusté en fonction de la bande passante du réseau, accélérant ainsi considérablement les analyses avec Nmap.

### **Analyse par défaut**

```bash
📝 sudo nmap 10.129.2.0/24 -F -oN tnet.default
```

### **Numérisation optimisée**

```bash
📝 sudo nmap 10.129.2.0/24 -F -oN tnet.minrate300 --min-rate 300
```

----
## **Timing**

Six modèles de timing différents (-T <0-5>) permettent d'ajuster l'agressivité des scans, avec des valeurs déterminées par les développeurs de Nmap.

### **Analyse par défaut**

```bash
📝 sudo nmap 10.129.2.0/24 -F -oN tnet.default
```

### **Analyse insensée**

```bash
📝 sudo nmap 10.129.2.0/24 -F -oN tnet.T5 -T 5
```


# Évasion de pare-feu et IDS/IPS

### **Introduction**

L'énumération d'un réseau à l'aide de Nmap implique la nécessité de contourner les règles des pare-feu et des systèmes IDS/IPS. Ces mesures de sécurité sont conçues pour protéger les systèmes contre des connexions non autorisées.

### Pare-feu

Les pare-feu sont des mesures de sécurité qui bloquent les connexions non autorisées depuis des réseaux externes. Ils fonctionnent en surveillant le trafic réseau et en appliquant des règles pour décider du traitement des connexions.

---
### IDS/IPS

Les systèmes de détection d'intrusion (IDS) analysent le réseau à la recherche d'attaques potentielles, tandis que les systèmes de prévention d'intrusion (IPS) prennent des mesures défensives en cas de détection d'une attaque.

### Détermination des pare-feux et de leurs règles

Lorsqu'un port est filtré, cela peut être dû à des règles spécifiques dans le pare-feu. Les paquets peuvent être "dropped" (ignorés) ou "rejected" (renvoyés avec un RST flag).

#### Analyse TCP ACK de Nmap (-sA)


```shell 
📝 sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```

Cette méthode est difficile à filtrer pour les pare-feux et IDS/IPS, car elle envoie uniquement un paquet TCP avec le flag ACK.

_Analysez les résultats spécifiques de cette commande pour déterminer l'état des ports._

### Détection des IDS/IPS

La détection des systèmes IDS/IPS est complexe car ils sont passifs. L'utilisation de plusieurs VPS avec des adresses IP différentes peut aider à déterminer leur présence.

---
### Leurres

L'utilisation de leurres, telle que la méthode de numérisation Decoy (-D), peut être efficace pour masquer l'origine des paquets envoyés.

#### Scanner à l'aide de leurres


```shell 
📝 sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```

Cette méthode génère diverses adresses IP aléatoires pour masquer l'origine du paquet envoyé.

_Analysez les résultats spécifiques de cette commande pour évaluer l'efficacité des leurres._

### Test de la règle de pare-feu

#### Analyse de ports avec OS detection


```shell 
📝 sudo nmap 10.129.2.28 -n -Pn -p 445 -O
```

Cette commande analyse le port 445 tout en tentant de détecter le système d'exploitation.

_Analysez les résultats spécifiques de cette commande pour obtenir des informations sur le port et le système d'exploitation._

#### Numérisation avec adresse IP source différente

```shell 
📝 sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```

Cette commande effectue une analyse avec une adresse IP source différente.

_Analysez les résultats spécifiques de cette commande pour évaluer l'impact de l'adresse IP source sur l'analyse._

---

### Proxy DNS

L'utilisation de serveurs DNS spécifiques peut être cruciale pour interagir avec des hôtes dans une zone démilitarisée (DMZ) ou pour contourner des restrictions.

### Scans particuliers

#### SYN-Scan d'un port filtré

bashCopy code

```shell 
📝 sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace
```

Ce scan utilise une analyse SYN sur un port filtré (port 50000).

_Analysez les résultats spécifiques de cette commande pour évaluer le comportement du pare-feu._

#### SYN-Scan depuis le port DNS


```shell 
📝 sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```

Ce scan utilise une analyse SYN avec un port source spécifié (port 53).

_Analysez les résultats spécifiques de cette commande pour déterminer si le pare-feu accepte le port source spécifié._

### Commande Nmap pour vérifier la version du serveur DNS :


```shell 
📝sudo nmap -sSU -p 53 --script dns-nsid 10.129.2.48
```

- **Description :** Cette commande utilise Nmap, un outil de découverte réseau, pour interroger le serveur DNS à l'adresse IP `10.129.2.48` sur le port UDP `53`. L'option `-sSU` indique à Nmap d'effectuer un balayage SYN/UDP, et l'option `--script dns-nsid` spécifie le script DNS-NSID pour récupérer des informations supplémentaires, telles que le nom du serveur.

---
### Commande Netcat pour établir une connexion sur un port  :

```shell 
📝sudo nc -nv -p 53 10.129.75.43 50000
```

- **Description :** Cette commande utilise Netcat (`nc`) pour établir une connexion vers l'adresse IP `10.129.75.43` sur le port UDP `53`, avec l'option `-p 53` spécifiant le port local comme `53`. L'option `-nv` active le mode verbeux pour afficher davantage d'informations. Cependant, l'utilisation du port `50000` en tant que port local peut nécessiter une compréhension spécifique du contexte ou des configurations particulières sur la machine cible.

### **Conclusion**

En conclusion, l'énumération de réseau avec Nmap nécessite une compréhension approfondie des pare-feu et des IDS/IPS, ainsi que des techniques spécifiques pour les contourner de manière efficace. Les tests et analyses détaillés permettent d'évaluer la robustesse des mesures de sécurité en place.



