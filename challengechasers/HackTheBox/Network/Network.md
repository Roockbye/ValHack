# Modèle OSI 

Le modèle OSI a été défini dans le cadre de la norme ISO/OSI dans le but de créer un modèle de référence permettant la communication entre différents systèmes techniques via divers dispositifs et technologies, tout en assurant la compatibilité. Le modèle OSI utilise sept couches différentes, organisées de manière hiérarchique, pour atteindre cet objectif. Ces couches représentent les phases dans l'établissement de chaque connexion à travers laquelle les paquets envoyés passent. Ainsi, la norme a été créée pour tracer visuellement comment une connexion est structurée et établie.

![osi.png]

|Couche|Fonction|
|---|---|
|7. Application|Cette couche contrôle, entre autres, l'entrée et la sortie des données et fournit les fonctions d'application.|
|6. Présentation|La tâche de la couche de présentation est de convertir la présentation des données dépendante du système en une forme indépendante de l'application.|
|5. Session|La couche de session contrôle la connexion logique entre deux systèmes et empêche, par exemple, les interruptions de connexion ou d'autres problèmes.|
|4. Transport|La couche 4 est utilisée pour le contrôle de bout en bout des données transférées. La couche de transport peut détecter et éviter les situations de congestion et segmenter les flux de données.|
|3. Réseau|À la couche de réseau, des connexions sont établies dans les réseaux à commutation de circuit, et les paquets de données sont acheminés dans les réseaux à commutation de paquets. Les données sont transmises sur l'ensemble du réseau, de l'émetteur au récepteur.|
|2. Liaison de données|La tâche centrale de la couche 2 est de permettre des transmissions fiables et sans erreur sur le support respectif. À cette fin, les flux de bits de la couche 1 sont divisés en blocs ou trames.|
|1. Physique|Les techniques de transmission utilisées sont, par exemple, les signaux électriques, les signaux optiques ou les ondes électromagnétiques. À travers la couche 1, la transmission s'effectue sur des lignes de transmission câblées ou sans fil.|

Les couches 2 à 4 sont orientées vers le transport, et les couches 5 à 7 sont orientées vers l'application. Dans chaque couche, des tâches précisément définies sont effectuées, et les interfaces avec les couches voisines sont soigneusement décrites. Chaque couche offre des services destinés à être utilisés par la couche directement au-dessus d'elle. Pour rendre ces services disponibles, la couche utilise les services de la couche située en dessous d'elle et effectue les tâches de sa propre couche.

Lorsque deux systèmes communiquent, les sept couches du modèle OSI sont traversées au moins deux fois, car tant l'émetteur que le récepteur doivent tenir compte du modèle en couches. Par conséquent, un grand nombre de tâches différentes doivent être effectuées dans les couches individuelles pour assurer la sécurité, la fiabilité et les performances de la communication.

# Modèle TCP/IP 


Le modèle TCP/IP est également un modèle de référence en couches, souvent appelé la Suite de Protocoles Internet. Le terme TCP/IP représente les deux protocoles Transmission Control Protocol (TCP) et Internet Protocol (IP). 

![Pasted image 20240307105516.png]


Les tâches les plus importantes de TCP/IP sont :

- **Adressage Logique (IP):** En raison de nombreux hôtes dans différents réseaux, il est nécessaire de structurer la topologie du réseau et l'adressage logique. Dans TCP/IP, IP prend en charge l'adressage logique des réseaux et des nœuds. Les paquets de données atteignent uniquement le réseau où ils sont censés être, grâce à des méthodes telles que les classes de réseau, le sous-réseau et CIDR.
    
- **Routage (IP):** Pour chaque paquet de données, le prochain nœud est déterminé à chaque nœud sur le chemin de l'émetteur au récepteur. Ainsi, un paquet de données est routé vers son récepteur, même si sa localisation est inconnue de l'émetteur.
    
- **Contrôle des Erreurs et du Flux (TCP):** L'émetteur et le récepteur sont fréquemment en contact l'un avec l'autre via une connexion virtuelle. Par conséquent, des messages de contrôle sont envoyés en continu pour vérifier si la connexion est toujours établie.
    
- **Support de l'Application (TCP):** Les ports TCP et UDP forment une abstraction logicielle pour distinguer des applications spécifiques et leurs liens de communication.
    
- **Résolution des Noms (DNS):** Le DNS fournit une résolution des noms via des noms de domaine complets (FQDN) en adresses IP, nous permettant d'atteindre l'hôte souhaité avec le nom spécifié sur Internet.


# Adresses IPv4 / IPv6 et Sous réseaux 

Chaque hôte dans un réseau est identifiable par une adresse MAC (Media Access Control) pour les échanges de données internes. Cependant, pour les connexions extérieures, les adresses IPv4 ou IPv6 sont essentielles, composées du network address et du host address.

Peu importe la taille du réseau, l'adresse IP garantit la transmission des données au bon destinataire. Les adresses MAC et IPv4/IPv6 peuvent être comparées à une adresse postale et à un appartement dans un immeuble, respectivement.

## Structure IPv4

IPv4 utilise un format de 32 bits, regroupés en 4 octets (bytes) de 8 bits chacun. Ces octets sont convertis en une notation décimale à quatre parties, par exemple, 192.168.10.39. Chaque interface réseau a une adresse IP unique.

Les adresses IPv4 autorisent 4 294 967 296 adresses uniques et sont divisées en classes A, B, C, D et E. Cependant, avec la méthode CIDR, la division se fait de manière plus flexible.

#### Masque de sous-réseau

Le subnetting permet une séparation plus fine des classes via le netmask. Les classes A, B, C, D et E sont subdivisées en sous-réseaux définis par le masque de sous-réseau, précisant les positions des bits pour la partie réseau et hôte.

#### Adresses réseau et passerelle

Les adresses réseau incluent deux IPs réservées pour le network address et le broadcast address. Le default gateway, souvent la première ou dernière adresse attribuable dans un sous-réseau, gère les connexions entre réseaux et systèmes.

#### Adresse de diffusion

Le broadcast, envoyé à toutes les adresses, permet la communication sans réponse. La dernière adresse IPv4 dans un sous-réseau est utilisée à cette fin.

#### Système binaire

Une adresse IPv4 est divisée en 4 octets, chacun consistant en 8 bits. Chaque bit a une valeur décimale, permettant la conversion de binaire à décimal.

#### CIDR

CIDR remplace les classes fixes en utilisant un suffixe indiquant le nombre de bits réseau. Par exemple, CIDR pour 192.168.10.39 avec un masque de sous-réseau 255.255.255.0 est /24.

La table des matières complète l'introduction au réseautage, couvrant la structure du réseau, le flux de travail réseau, l'adressage, les protocoles, l'établissement de la connexion, le poste de travail, et les informations hors ligne.

## Introduction aux adresses IPv6

#### Généralités

IPv6 est le successeur d'IPv4. Contrairement à IPv4, l'adresse IPv6 est composée de 128 bits. Le préfixe identifie les parties hôte et réseau. L'Autorité des numéros assignés sur Internet (IANA) est responsable de l'attribution des adresses IPv4 et IPv6 ainsi que de leurs parties réseau associées. À long terme, IPv6 est censé remplacer complètement IPv4, qui est encore largement utilisé sur Internet. Cependant, IPv4 et IPv6 peuvent coexister simultanément (Dual Stack).

IPv6 suit systématiquement le principe de bout en bout et offre des adresses IP publiquement accessibles pour tous les dispositifs finaux sans nécessiter de NAT. Par conséquent, une interface peut avoir plusieurs adresses IPv6, et il existe des adresses IPv6 spéciales auxquelles plusieurs interfaces peuvent être assignées.

IPv6 présente de nombreuses nouvelles fonctionnalités et offre plusieurs avantages par rapport à IPv4, notamment un espace d'adressage plus important, la configuration automatique des adresses (SLAAC), plusieurs adresses IPv6 par interface, un routage plus rapide, le chiffrement de bout en bout (IPsec), et la possibilité de gérer des paquets de données jusqu'à 4 Go.

#### Caractéristiques Comparées IPv4 / IPv6

|Fonctionnalités|IPv4|IPv6|
|---|---|---|
|Longueur en bits|32 bits|128 bits|
|Couche OSI|Couche réseau|Couche réseau|
|Plage d'adressage|~ 4.3 milliards|~ 340 undécillions|
|Représentation|Binaire|Hexadécimal|
|Adressage dynamique|DHCP|SLAAC / DHCPv6|
|IPsec|Optionnel|Obligatoire|

Il existe quatre types d'adresses IPv6:

1. **Unicast:** Adresses pour une seule interface.
2. **Anycast:** Adresses pour plusieurs interfaces, où seule l'une d'entre elles reçoit le paquet.
3. **Multicast:** Adresses pour plusieurs interfaces, où toutes reçoivent le même paquet.
4. **Broadcast:** N'existent pas et sont réalisées avec des adresses multicast.

#### Système Hexadécimal

Le système hexadécimal (hex) est utilisé pour rendre la représentation binaire plus lisible. Contrairement au système binaire et décimal, le système hexadécimal permet de représenter 16 états avec un seul caractère. Voici une table de conversion :

|Décimal|Hexadécimal|Binaire|
|---|---|---|
|1|1|0001|
|2|2|0010|
|3|3|0011|
|4|4|0100|
|5|5|0101|
|6|6|0110|
|7|7|0111|
|8|8|1000|
|9|9|1001|
|10|A|1010|
|11|B|1011|
|12|C|1100|
|13|D|1101|
|14|E|1110|
|15|F|1111|

Un exemple avec une adresse IPv4 : la représentation hexadécimale de l'adresse IPv4 (192.168.12.160) serait :

|Représentation|1er octet|2ème octet|3ème octet|4ème octet|
|---|---|---|---|---|
|Binaire|11000000|10101000|00001100|10100000|
|Hexadécimal|C0|A8|0C|A0|
|Décimal|192|168|12|160|

En tout, l'adresse IPv6 est composée de 16 octets. En raison de sa longueur, une adresse IPv6 est représentée en notation hexadécimale. Ainsi, les 128 bits sont divisés en 8 blocs, chacun représenté par 16 bits (ou 4 chiffres hexadécimaux). Les quatre chiffres hexadécimaux sont regroupés et séparés par deux-points (:) au lieu d'un simple point (.) comme dans IPv4. Pour simplifier la notation, nous omettons au moins 4 zéros initiaux dans les blocs, que nous pouvons remplacer par deux double-points (::).

Une adresse IPv6 peut ressembler à ceci :

IPv6 complet : fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64 IPv6 abrégé : fe80::dd80:b1a9:6687:2d3b/64

Une adresse IPv6 est composée de deux parties :

1. Préfixe réseau (partie réseau)
2. Identifiant d'interface, également appelé suffixe (partie hôte)

Le préfixe réseau identifie le réseau, le sous-réseau ou la plage d'adresses. L'identifiant d'interface est formé à partir de l'adresse MAC 48 bits (que nous discuterons plus tard) de l'interface et est converti en une adresse de 64 bits dans le processus. La longueur de préfixe par défaut est /64, mais d'autres préfixes typiques sont /32, /48 et /56. Si nous voulons utiliser nos réseaux, notre fournisseur nous attribue un préfixe plus court (par exemple /56) que /64.

RFC 5952 définit la notation d'adresse IPv6 susmentionnée :

1. Tous les caractères alphabétiques sont toujours écrits en minuscules.
2. Tous les zéros initiaux d'un bloc sont toujours omis.
3. Un ou plusieurs blocs consécutifs de 4 zéros (hex) sont raccourcis par deux double-points (::).
4. Le raccourcissement en deux double-points (::) ne peut être effectué qu'une seule fois en partant de la gauche.
## Sous-réseaux

#### Définition

Le subnetting, ou la division d'une plage d'adresses IPv4 en plusieurs plages plus petites, permet de créer des sous-réseaux.

#### Caractéristiques d'un Sous-réseau

Un sous-réseau représente un segment logique d'un réseau, utilisant des adresses IP partageant la même adresse réseau. On peut l'assimiler à une porte numérotée dans un vaste couloir d'un bâtiment, symbolisant la séparation entre différents départements d'une entreprise. En utilisant le sous-réseau, il est possible de créer une structure spécifique ou de comprendre le schéma réseau.

#### Éléments clés d'un Sous-réseau

1. Network address
2. Broadcast address
3. First host
4. Last host
5. Number of hosts

#### Exemple Pratique

Considérons une adresse IPv4 et un masque de sous-réseau :

- Adresse IPv4 : 192.168.12.160
- Masque de sous-réseau : 255.255.255.192
- CIDR : 192.168.12.160/26

L'adresse IP se divise déjà en deux parties : network part et host part.

### Partie Réseau

#### Détails

|1er octet|2ème octet|3ème octet|4ème octet|Décimal|
|---|---|---|---|---|
|11000000|10101000|00001100|10100000|192.168.12.160/26|

En utilisant le masque de sous-réseau comme modèle, les 1-bits indiquent les bits fixes de l'adresse IPv4, définissant ainsi le "réseau principal" du sous-réseau.

### Partie Hôte

#### Détails

|1er octet|2ème octet|3ème octet|4ème octet|Décimal|
|---|---|---|---|---|
|11000000|10101000|00001100|10100000|192.168.12.160/26|

Les bits dans la partie hôte peuvent être modifiés pour obtenir la première et la dernière adresse utilisable dans le sous-réseau.

#### Importance de l'Adresse Réseau

L'adresse réseau est cruciale pour le routage des paquets de données. Si l'adresse source et l'adresse de destination partagent la même network address, le paquet est livré dans le même sous-réseau. Dans le cas contraire, le paquet doit être acheminé vers un autre sous-réseau via la passerelle par défaut.

#### Rôle du Subnet Mask

Le subnet mask détermine la séparation entre les parties réseau et hôte, guidant ainsi le routage des données.

### Séparation des Parties Réseau et Hôte

#### Détails

|1er octet|2ème octet|3ème octet|4ème octet|Décimal|
|---|---|---|---|---|
|11000000|101010...|||



# Lexique à connaitre 

| Protocole                                         | Abréviation | Description                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Wired Equivalent Privacy                          | WEP         | Le WEP est un type de protocole de sécurité couramment utilisé pour sécuriser les réseaux sans fil.                                                                                                                                                                                                                                     |
| Secure Shell                                      | SSH         | Protocole réseau sécurisé utilisé pour se connecter et exécuter des commandes sur un système distant.                                                                                                                                                                                                                                   |
| File Transfer Protocol                            | FTP         | Protocole réseau utilisé pour transférer des fichiers d'un système à un autre.                                                                                                                                                                                                                                                          |
| Simple Mail Transfer Protocol                     | SMTP        | Protocole utilisé pour envoyer et recevoir des emails.                                                                                                                                                                                                                                                                                  |
| Hypertext Transfer Protocol                       | HTTP        | Protocole client-serveur utilisé pour envoyer et recevoir des données sur Internet.                                                                                                                                                                                                                                                     |
| Server Message Block                              | SMB         | Protocole utilisé pour partager des fichiers, des imprimantes et d'autres ressources dans un réseau.                                                                                                                                                                                                                                    |
| Network File System                               | NFS         | Protocole utilisé pour accéder aux fichiers via un réseau.                                                                                                                                                                                                                                                                              |
| Simple Network Management Protocol                | SNMP        | Protocole utilisé pour gérer les dispositifs réseau.                                                                                                                                                                                                                                                                                    |
| Wi-Fi Protected Access                            | WPA         | Le WPA est un protocole de sécurité sans fil qui utilise un mot de passe pour protéger les réseaux sans fil contre les accès non autorisés.                                                                                                                                                                                             |
| Temporal Key Integrity Protocol                   | TKIP        | Le TKIP est également un protocole de sécurité utilisé dans les réseaux sans fil, mais moins sécurisé.                                                                                                                                                                                                                                  |
| Network Time Protocol                             | NTP         | Il est utilisé pour synchroniser l'horloge des ordinateurs sur un réseau.                                                                                                                                                                                                                                                               |
| Virtual Local Area Network                        | VLAN        | C'est une méthode de segmentation d'un réseau en plusieurs réseaux logiques.                                                                                                                                                                                                                                                            |
| VLAN Trunking Protocol                            | VTP         | Le VTP est un protocole de couche 2 utilisé pour établir et maintenir un réseau local virtuel (VLAN) sur plusieurs commutateurs.                                                                                                                                                                                                        |
| Routing Information Protocol                      | RIP         | RIP est un protocole de routage à vecteur de distance utilisé dans les réseaux locaux (LAN) et les réseaux étendus (WAN).                                                                                                                                                                                                               |
| Open Shortest Path First                          | OSPF        | Il s'agit d'un protocole de passerelle intérieure (IGP) pour le routage du trafic à l'intérieur d'un système autonome (AS) dans un réseau IP.                                                                                                                                                                                           |
| Interior Gateway Routing Protocol                 | IGRP        | L'IGRP est un protocole de passerelle intérieure exclusif à Cisco, conçu pour le routage à l'intérieur des systèmes autonomes.                                                                                                                                                                                                          |
| Enhanced Interior Gateway Routing Protocol        | EIGRP       | C'est un protocole de routage avancé utilisé pour router le trafic IP à l'intérieur d'un réseau.                                                                                                                                                                                                                                        |
| Pretty Good Privacy                               | PGP         | PGP est un programme de cryptage utilisé pour sécuriser les emails, les fichiers et d'autres types de données.                                                                                                                                                                                                                          |
| Network News Transfer Protocol                    | NNTP        | NNTP est un protocole utilisé pour distribuer et récupérer des messages dans les groupes de discussion sur Internet.                                                                                                                                                                                                                    |
| Cisco Discovery Protocol                          | CDP         | Il s'agit d'un protocole propriétaire développé par Cisco Systems qui permet aux administrateurs réseau de découvrir et de gérer les dispositifs Cisco connectés au réseau.                                                                                                                                                             |
| Hot Standby Router Protocol                       | HSRP        | HSRP est un protocole utilisé dans les routeurs Cisco pour fournir une redondance en cas de défaillance d'un routeur ou d'un autre dispositif réseau.                                                                                                                                                                                   |
| Virtual Router Redundancy Protocol                | VRRP        | Il s'agit d'un protocole utilisé pour fournir l'attribution automatique de routeurs IP disponibles aux hôtes participants.                                                                                                                                                                                                              |
| Spanning Tree Protocol                            | STP         | Le STP est un protocole réseau utilisé pour assurer une topologie sans boucle dans les réseaux Ethernet de couche 2.                                                                                                                                                                                                                    |
| Terminal Access Controller Access-Control System  | TACACS      | Le TACACS est un protocole fournissant une authentification, une autorisation et une comptabilité centralisées pour l'accès au réseau.                                                                                                                                                                                                  |
| Session Initiation Protocol                       | SIP         | Il s'agit d'un protocole de signalisation utilisé pour établir et terminer des sessions vocales, vidéo et multimédias en temps réel sur un réseau IP.                                                                                                                                                                                   |
| Voice Over IP                                     | VOIP        | La VOIP est une technologie qui permet de passer des appels téléphoniques via Internet.                                                                                                                                                                                                                                                 |
| Extensible Authentication Protocol                | EAP         | L'EAP est un cadre d'authentification prenant en charge plusieurs méthodes d'authentification, telles que les mots de passe, les certificats numériques, les mots de passe à usage unique et l'authentification par clé publique.                                                                                                       |
| Lightweight Extensible Authentication Protocol    | LEAP        | LEAP est un protocole de sécurité sans fil propriétaire développé par Cisco Systems, basé sur le Protocole d'authentification extensible (EAP) utilisé dans le Protocole de point à point (PPP).                                                                                                                                        |
| Protected Extensible Authentication Protocol      | PEAP        | Le PEAP est un protocole de sécurité assurant un tunnel crypté pour les réseaux sans fil et d'autres types de réseaux.                                                                                                                                                                                                                  |
| Systems Management Server                         | SMS         | Le SMS est une solution de gestion de systèmes qui aide les organisations à gérer leurs réseaux, systèmes et appareils mobiles.                                                                                                                                                                                                         |
| Microsoft Baseline Security Analyzer              | MBSA        | C'est un outil de sécurité gratuit de Microsoft utilisé pour détecter d'éventuelles vulnérabilités de sécurité dans les ordinateurs, réseaux et systèmes Windows.                                                                                                                                                                       |
| Supervisory Control and Data Acquisition          | SCADA       | Il s'agit d'un type de système de contrôle industriel utilisé pour surveiller et contrôler les processus industriels, tels que la fabrication, la production d'énergie et le traitement de l'eau et des déchets.                                                                                                                        |
| Virtual Private Network                           | VPN         | La VPN est une technologie qui permet aux utilisateurs de créer une connexion sécurisée et chiffrée vers un autre réseau via Internet.                                                                                                                                                                                                  |
| Internet Protocol Security                        | IPsec       | L'IPsec est un protocole utilisé pour assurer une communication sécurisée et chiffrée sur un réseau, couramment utilisé dans les VPN pour créer un tunnel sécurisé entre deux dispositifs.                                                                                                                                              |
| Point-to-Point Tunneling Protocol                 | PPTP        | Protocole utilisé pour créer un tunnel sécurisé et chiffré pour l'accès à distance.                                                                                                                                                                                                                                                     |
| Network Address Translation                       | NAT         | La NAT est une technologie qui permet à plusieurs dispositifs sur un réseau privé de se connecter à Internet en utilisant une seule adresse IP publique. La NAT fonctionne en traduisant les adresses IP privées des dispositifs sur le réseau en une seule adresse IP publique, qui est ensuite utilisée pour se connecter à Internet. |
| Carriage Return Line Feed                         | CRLF        | Combinaison de deux caractères de contrôle pour indiquer la fin d'une ligne et le début d'une nouvelle, utilisée dans certains formats de fichiers texte.                                                                                                                                                                               |
| Asynchronous JavaScript and XML                   | AJAX        | Technique de développement web permettant de créer des pages web dynamiques en utilisant JavaScript et XML/JSON.                                                                                                                                                                                                                        |
| Internet Server Application Programming Interface | ISAPI       | Permet de créer des extensions web orientées performances pour les serveurs web en utilisant un ensemble d'API.                                                                                                                                                                                                                         |
| Uniform Resource Identifier                       | URI         | Syntaxe utilisée pour identifier une ressource sur Internet.                                                                                                                                                                                                                                                                            |
| Uniform Resource Locator                          | URL         | Sous-ensemble de l'URI qui identifie une page web ou une autre ressource sur Internet, y compris le protocole et le nom de domaine.                                                                                                                                                                                                     |
| Internet Key Exchange                             | IKE         | IKE est un protocole utilisé pour établir une connexion sécurisée entre deux ordinateurs. Il est utilisé dans les réseaux privés virtuels (VPN) pour fournir une authentification et un chiffrement des données, protégeant ainsi les données contre l'écoute et la manipulation extérieures.                                           |
| Generic Routing Encapsulation                     | GRE         | Ce protocole est utilisé pour encapsuler les données transmises dans le tunnel VPN.                                                                                                                                                                                                                                                     |
| Remote Shell                                      | RSH         | Il s'agit d'un programme sous Unix qui permet d'exécuter des commandes et des programmes sur un ordinateur distant.                                                                                                                                                                                                                     |

# Protocoles

## TCP


|**Protocole**|**Acronyme**|**port**|**Description**|
|---|---|---|---|
|Telnet|`Telnet`|`23`|Service de connexion à distance|
|Enveloppe de protection|`SSH`|`22`|Service de connexion à distance sécurisé|
|Protocole de gestion de réseau simple|`SNMP`|`161-162`|Gérer les périphériques réseau|
|Protocole de transfert hypertexte|`HTTP`|`80`|Utilisé pour transférer des pages Web|
|Protocole de transfert hypertexte sécurisé de|`HTTPS`|`443`|Utilisé pour transférer des pages Web sécurisées|
|Système de noms de domaines|`DNS`|`53`|Rechercher des noms de domaine|
|Protocole de transfert de fichier|`FTP`|`20-21`|Utilisé pour transférer des fichiers|
|Protocole de transfert de fichiers trivial|`TFTP`|`69`|Utilisé pour transférer des fichiers|
|Protocole de temps réseau|`NTP`|`123`|Synchroniser les horloges des ordinateurs|
|Protocole de transfert de courrier simple|`SMTP`|`25`|Utilisé pour le transfert d'e-mails|
|Protocole du bureau de poste|`POP3`|`110`|Utilisé pour récupérer des emails|
|Protocole d'accès aux messages Internet|`IMAP`|`143`|Utilisé pour accéder aux e-mails|
|Bloc de messages du serveur|`SMB`|`445`|Utilisé pour transférer des fichiers|
|Système de fichiers réseau|`NFS`|`111`, `2049`|Utilisé pour monter des systèmes distants|
|Protocole d'amorçage|`BOOTP`|`67`, `68`|Utilisé pour amorcer les ordinateurs|
|Kerberos|`Kerberos`|`88`|Utilisé pour l'authentification et l'autorisation|
|Protocole d'accès à l'annuaire léger|`LDAP`|`389`|Utilisé pour les services d'annuaire|
|Service utilisateur d'authentification à distance|`RADIUS`|`1812`, `1813`|Utilisé pour l'authentification et l'autorisation|
|Protocole de configuration d'hôte dynamique|`DHCP`|`67`, `68`|Utilisé pour configurer les adresses IP|
|Protocole de bureau à distance|`RDP`|`3389`|Utilisé pour l'accès au bureau à distance|
|Protocole de transfert de nouvelles en réseau|`NNTP`|`119`|Utilisé pour accéder aux groupes de discussion|
|Appel de procédure à distance|`RPC`|`135`, `137-139`|Utilisé pour appeler des procédures distantes|
|Protocole d'identification|`Ident`|`113`|Utilisé pour identifier les processus utilisateur|
|Protocole de message de contrôle Internet|`ICMP`|`0-255`|Utilisé pour résoudre les problèmes de réseau|
|Protocole de gestion de groupe Internet|`IGMP`|`0-255`|Utilisé pour la multidiffusion|
|Écouteur Oracle DB (par défaut/alternatif)|`oracle-tns`|`1521`/`1526`|L'écouteur par défaut/alternatif de la base de données Oracle est un service qui s'exécute sur l'hôte de la base de données et reçoit les requêtes des clients Oracle..|
|Verrouillage Ingres|`ingreslock`|`1524`|La base de données Ingres est couramment utilisée pour les grandes applications commerciales et comme porte dérobée pouvant exécuter des commandes à distance via RPC..|
|Proxy Web Squid|`http-proxy`|`3128`|Le proxy Web Squid est un proxy Web HTTP de mise en cache et de transfert utilisé pour accélérer un serveur Web en mettant en cache les requêtes répétées..|
|Protocole de copie sécurisée|`SCP`|`22`|Copiez en toute sécurité des fichiers entre les systèmes|
|séance d'initiation au protocoles|`SIP`|`5060`|Utilisé pour les sessions VoIP|
|Protocole d'accès aux objets simple|`SOAP`|`80`, `443`|Utilisé pour les services Web|
|Couche de socket sécurisée|`SSL`|`443`|Transférer des fichiers en toute sécurité|
|Encapsuleur TCP|`TCPW`|`113`|Utilisé pour le contrôle d'accès|
|Association de sécurité Internet et protocole de gestion des clés|`ISAKMP`|`500`|Utilisé pour les connexions VPN|
|Microsoft SQL Server|`ms-sql-s`|`1433`|Utilisé pour les connexions client à Microsoft SQL Server.|
|Négociation Internet Kerberisée des clés|`KINK`|`892`|Utilisé pour l'authentification et l'autorisation|
|Ouvrez le chemin le plus court en premier|`OSPF`|`520`|Utilisé pour le routage|
|Protocole de tunneling point à point|`PPTP`|`1723`|Est utilisé pour créer des VPN|
|Exécution à distance|`REXEC`|`512`|Ce protocole est utilisé pour exécuter des commandes sur des ordinateurs distants et renvoyer le résultat des commandes à l'ordinateur local..|
|Connexion à distance|`RLOGIN`|`513`|Ce protocole démarre une session shell interactive sur un ordinateur distant.|
|Système X Window|`X11`|`6000`|Il s'agit d'un système logiciel informatique et d'un protocole réseau qui fournit une interface utilisateur graphique (GUI) pour les ordinateurs en réseau..|
|Système de gestion de base de données relationnelle|`DB2`|`50000`|Le SGBDR est conçu pour stocker, récupérer et gérer des données dans un format structuré pour les applications d'entreprise telles que les systèmes financiers et les systèmes de gestion de la relation client (CRM)..|
## UDP

|**Protocole**|**Acronyme**|**port**|**Description**|
|---|---|---|---|
|Système de noms de domaines|`DNS`|`53`|C'est un protocole pour résoudre les noms de domaine en adresses IP.|
|Protocole de transfert de fichiers trivial|`TFTP`|`69`|Il est utilisé pour transférer des fichiers entre les systèmes.|
|Protocole de temps réseau|`NTP`|`123`|Il synchronise les horloges des ordinateurs dans un réseau.|
|Protocole de gestion de réseau simple|`SNMP`|`161`|Il surveille et gère les périphériques réseau à distance.|
|Protocole d'informations de routage|`RIP`|`520`|Il est utilisé pour échanger des informations de routage entre les routeurs.|
|Échange de clés Internet|`IKE`|`500`|Échange de clés Internet|
|Protocole d'amorçage|`BOOTP`|`68`|Il est utilisé pour amorcer les hôtes dans un réseau.|
|Protocole de configuration d'hôte dynamique|`DHCP`|`67`|Il est utilisé pour attribuer dynamiquement des adresses IP aux appareils d’un réseau..|
|Telnet|`TELNET`|`23`|Il s'agit d'un protocole de communication d'accès à distance basé sur du texte.|
|MySQL|`MySQL`|`3306`|Il s'agit d'un système de gestion de base de données open source.|
|Serveur Principal|`TS`|`3389`|Il s'agit d'un protocole d'accès à distance utilisé par défaut pour les services Terminal Server de Microsoft Windows..|
|Nom NetBIOS|`netbios-ns`|`137`|Il est utilisé dans les systèmes d'exploitation Windows pour résoudre les noms NetBIOS en adresses IP sur un réseau local..|
|Microsoft SQL Server|`ms-sql-m`|`1434`|Utilisé pour le service Microsoft SQL Server Browser.|
|Plug and Play universel|`UPnP`|`1900`|Il s'agit d'un protocole permettant aux appareils de se découvrir sur le réseau et de communiquer.|
|PostgreSQL|`PGSQL`|`5432`|Il s'agit d'un système de gestion de base de données objet-relationnel.|
|Informatique en réseau virtuel|`VNC`|`5900`|C'est un système de partage de bureau graphique.|
|Système X Window|`X11`|`6000-6063`|Il s'agit d'un système logiciel informatique et d'un protocole réseau qui fournit une interface graphique sur les systèmes de type Unix..|
|Journal système|`SYSLOG`|`514`|Il s'agit d'un protocole standard pour collecter et stocker les messages de journal sur un système informatique..|
|Chat de relais Internet|`IRC`|`194`|Il s'agit d'un protocole de messagerie texte Internet (chat) ou de communication synchrone en temps réel..|
|OpenPGP|`OpenPGP`|`11371`|C'est un protocole de cryptage et de signature des données et des communications.|
|Sécurité du protocole Internet|`IPsec`|`500`|IPsec est également un protocole qui permet une communication sécurisée et cryptée. Il est couramment utilisé dans les VPN pour créer un tunnel sécurisé entre deux appareils.|
|Échange de clés Internet|`IKE`|`11371`|C'est un protocole de cryptage et de signature des données et des communications.|
|Protocole de contrôle du gestionnaire d'affichage X|`XDMCP`|`177`|XDMCP est un protocole réseau qui permet à un utilisateur de se connecter à distance à un ordinateur exécutant X11.|

## ICMP et VoIP

## **Internet Control Message Protocol (ICMP)**

Le **Protocole de message de contrôle Internet (ICMP)** est un protocole essentiel utilisé par les appareils pour communiquer entre eux sur Internet, jouant un rôle crucial dans le rapport d'erreurs et la transmission d'informations d'état. Il opère en envoyant des requêtes et des messages entre les appareils, facilitant la détection d'erreurs et la vérification de la connectivité.

## **Requêtes ICMP**

Les requêtes ICMP sont des messages envoyés par un appareil à un autre pour demander des informations ou effectuer des actions spécifiques. Un exemple bien connu de requête ICMP est la requête "ping", qui teste la connectivité entre deux appareils. L'appareil émetteur attend une réponse, générant ainsi un message de type "ping reply" de la part du destinataire.

 ## **Messages ICMP**

Les messages ICMP peuvent être des requêtes ou des réponses, servant à signaler divers types d'informations et d'erreurs entre les appareils du réseau. En plus des requêtes "ping" et des réponses, ICMP prend en charge des messages tels que "destination unreachable" (destination inaccessible) et "time exceeded" (temps écoulé), fournissant des détails sur les problèmes rencontrés lors de la transmission des données.

ICMP existe en deux versions distinctes :

- **ICMPv4 :** Conçu pour IPv4, reste largement utilisé.
- **ICMPv6 :** Développé pour IPv6, offre des fonctionnalités supplémentaires et surmonte certaines limitations de l'ICMPv4.

**Exemples de types de requêtes et de messages ICMP :**

- _Type de requête :_
    
    - **Echo Request :** Teste la disponibilité d'un appareil sur le réseau.
    - **Timestamp Request :** Détermine l'heure sur un appareil distant.
    - **Address Mask Request :** Demande le masque de sous-réseau d'un appareil.
- _Type de message :_
    
    - **Echo Reply :** Réponse à une demande d'écho.
    - **Destination Unreachable :** Indique qu'un appareil ne peut pas livrer un paquet à sa destination.
    - **Redirect :** Informe qu'un appareil doit envoyer ses paquets à un autre routeur.
    - **Time Exceeded :** Indique qu'un paquet a mis trop de temps à atteindre sa destination.
    - **Parameter Problem :** Signale un problème avec l'en-tête d'un paquet.
    - **Source Quench :** Indique qu'un appareil reçoit des paquets trop rapidement et ne peut pas suivre, ralentissant le flux.

Un aspect crucial de l'ICMP est le champ "Time to Live (TTL)" dans l'en-tête du paquet, qui limite sa durée de vie lors de son déplacement sur le réseau, évitant ainsi les boucles de routage.

Le TTL décroît à chaque passage par un routeur, et lorsque la valeur atteint 0, un routeur rejette le paquet et envoie un message ICMP Time Exceeded à l'expéditeur.

L'utilisation du TTL permet également de déterminer le nombre de sauts effectués par un paquet, offrant une indication approximative de la distance jusqu'à la destination.

Il est possible de déduire le système d'exploitation d'un appareil en examinant la valeur TTL par défaut utilisée par celui-ci, bien que cela ne soit pas infaillible, car les utilisateurs peuvent modifier ces valeurs.

**Voix sur protocole Internet (VoIP)**

La **Voix sur protocole Internet (VoIP)** est une méthode de transmission de communications vocales et multimédias via Internet. Elle permet notamment de passer des appels téléphoniques en utilisant une connexion haut débit au lieu d'une ligne téléphonique traditionnelle.

Les ports les plus courants pour la VoIP sont TCP/5060 et TCP/5061, utilisés pour les protocoles de séance d'initiation (SIP). Le SIP, largement utilisé dans la VoIP, permet de lancer, maintenir, modifier et terminer des sessions en temps réel impliquant la vidéo, la voix, la messagerie, etc.

**Exemples de requêtes et méthodes SIP :**

- **Méthode :**
    - **INVITE :** Lance une session ou invite un autre point de terminaison à participer.
    - **ACK :** Confirme la réception d'une demande d'INVITE.
    - **BYE :** Termine une session.
    - **CANCEL :** Annule une demande INVITE en attente.
    - **REGISTER :** Enregistre un agent utilisateur (UA) SIP auprès d'un serveur SIP.
    - **OPTIONS :** Demande des informations sur les capacités d'un serveur SIP ou d'un agent utilisateur.

La VoIP présente toutefois des vulnérabilités potentielles, telles que la divulgation d'informations via des requêtes SIP OPTIONS, qui permet d'énumérer les utilisateurs existants. Cela peut être exploité à des fins d'attaque, comme la détermination de la disponibilité d'un utilisateur ou la préparation d'attaques par force brute sur les comptes d'utilisateurs.

L'utilisation de requêtes SIP OPTIONS peut également révéler des fichiers de configuration, tels que le fichier SEPxxxx.cnf, utilisé par Cisco Unified Communications Manager pour définir les paramètres des téléphones IP Cisco Unified. Ce fichier spécifie des détails tels que le modèle de téléphone, la version du micrologiciel et les paramètres réseau.

# Documentation sur les Réseaux sans Fil

## Introduction

Les réseaux sans fil sont des infrastructures informatiques qui permettent la communication entre des appareils tels que des ordinateurs portables, des smartphones et des tablettes sans nécessiter de connexions physiques telles que des câbles. Ces réseaux utilisent la technologie de radiofréquence (RF) pour transmettre des données entre les appareils, offrant ainsi une flexibilité de communication.

## Technologies sans Fil

### 1. **WiFi et Plages de Fréquences**

- Les réseaux locaux (LAN) utilisent souvent la technologie WiFi, qui opère dans les bandes de fréquences de 2,4 GHz ou 5 GHz.
- Les réseaux étendus sans fil (WWAN) utilisent des technologies de télécommunication mobile telles que les données cellulaires (3G, 4G LTE, 5G), couvrant des zones plus vastes.

### 2. **Connexion au Réseau sans Fil**

- Les appareils doivent être à portée du réseau et configurés avec les paramètres appropriés tels que le nom du réseau (SSID Service Set Identifier) et le mot de passe.
- Une fois connectés, les appareils peuvent échanger des données et accéder à Internet via un point d'accès sans fil (WAP), qui agit comme une passerelle vers le réseau filaire.

### 3. **Communication RF**

- La communication entre les appareils se fait via des signaux RF dans les bandes de 2,4 GHz ou 5 GHz.
- La puissance du signal et la portée dépendent de divers facteurs, dont la puissance de l'émetteur et la densité des interférences RF.

## Connexion WiFi

### 1. **Protocole IEEE 802.11**

- Lorsqu'un appareil souhaite se connecter à un réseau WiFi, il envoie une demande de connexion au WAP en utilisant le protocole IEEE 802.11.
- La demande de connexion comprend des informations telles que l'adresse MAC, le SSID, les débits de données pris en charge et les protocoles de sécurité.

### 2. **Sécurité de la Connexion WiFi**

- Les réseaux WiFi utilisent des protocoles de sécurité tels que WEP, WPA2, et WPA3 pour garantir la confidentialité et l'intégrité des données.
- Le filtrage MAC, la désactivation de la diffusion du SSID et d'autres mesures renforcent la sécurité du réseau.

## Prise de Contact Défi-Réponse WEP

### 1. **Processus de Défi-Réponse**

- Le processus de prise de contact défi-réponse établit une connexion sécurisée entre le WAP et le périphérique client dans un réseau utilisant WEP.
- Il implique l'échange de paquets pour l'authentification et l'établissement d'une connexion sécurisée.

### 2. **Contrôle de Redondance Cyclique (CRC)**

- Le CRC est utilisé dans WEP pour détecter les erreurs de transmission.
- La conception du CRC présente une faille permettant de déchiffrer un paquet sans connaître la clé de chiffrement.

## Fonctions de Sécurité dans les Réseaux WiFi

### 1. **Chiffrement**

- Les algorithmes tels que WEP, WPA2 et WPA3 sont utilisés pour le chiffrement des données.

### 2. **Contrôle d'Accès**

- Le filtrage MAC permet d'autoriser ou de rejeter les connexions en fonction des adresses MAC des appareils.

### 3. **Pare-feu**

- Les routeurs WiFi intègrent souvent des pare-feu pour contrôler le trafic entrant et sortant, renforçant la sécurité du réseau.

## Protocoles d'Authentification et Sécurité

### 1. **Protocoles d'Authentification**

- Protocoles tels que LEAP, PEAP, et TACACS+ sont utilisés pour sécuriser l'authentification des appareils sur le réseau sans fil.

### 2. **Attaque de Dissociation**

- L'attaque de dissociation vise à perturber la communication entre le WAP et ses clients en envoyant des trames de dissociation.

## Durcissement des Réseaux sans Fil

### 1. **Mesures de Sécurité**

- Désactivation de la diffusion du SSID, utilisation de WPA, filtrage MAC et déploiement d'EAP-TLS sont des mesures pour renforcer la sécurité.
- Ces mesures contribuent à protéger contre l'accès non autorisé, les attaques et l'interception de données sensibles.

En résumé, la mise en œuvre de bonnes pratiques de sécurité, le choix de protocoles robustes et la compréhension des vulnérabilités potentielles contribuent à garantir des réseaux sans fil fiables et sécurisés.

# VPN

## Introduction

Un Réseau Privé Virtuel (VPN) est une technologie qui permet une connexion sécurisée et cryptée entre un réseau privé et un appareil distant. Cette connexion établit un tunnel sécurisé, offrant un accès confidentiel aux ressources et services du réseau. Les VPN sont largement utilisés par les entreprises pour fournir un accès à distance sécurisé aux employés et connecter plusieurs sites distants à un réseau privé unique.

## Utilisation des VPN

1. **Accès à Distance :**
    
    - Les administrateurs peuvent se connecter à un serveur VPN via l'Internet pour gérer les serveurs internes depuis des emplacements distants.
    - Les employés peuvent accéder au réseau privé depuis leur domicile ou en déplacement, permettant l'utilisation des services internes.
2. **Sécurisation de la Connexion :**
    
    - Les VPN chiffrent les communications entre l'appareil distant et le réseau privé, renforçant la sécurité et empêchant l'interception d'informations sensibles.
3. **Flexibilité d'Accès :**
    
    - Les VPN permettent un accès distant depuis n'importe où avec une connexion Internet, offrant une flexibilité aux employés travaillant à distance.
4. **Connectivité Entre Sites Distants :**
    
    - Les VPN sont utilisés pour connecter plusieurs sites distants en un seul réseau privé, simplifiant la gestion et l'accès aux ressources.

## Composants et Exigences des VPN

1. **Client VPN :**
    
    - Installé sur l'appareil distant, le client VPN établit et maintient la connexion avec le serveur VPN, par exemple, OpenVPN.
2. **Serveur VPN :**
    
    - Un ordinateur ou périphérique réseau accepte les connexions VPN des clients et achemine le trafic entre ces clients et le réseau privé.
3. **Chiffrement :**
    
    - Les connexions VPN sont cryptées grâce à des algorithmes tels qu'AES et protocoles tels qu'IPsec, assurant la sécurité des données transmises.
4. **Authentification :**
    
    - Le serveur VPN et le client s'authentifient mutuellement par un secret partagé, un certificat ou d'autres méthodes pour établir une connexion sécurisée.

## Protocole IPsec

**IPsec (Internet Protocol Security) :**

- Protocole de sécurité réseau assurant le cryptage et l'authentification des communications Internet.
- Utilise l'Encapsulation de la charge utile de sécurité (ESP) et l'En-tête d'authentification (AH) pour assurer la sécurité des paquets IP.
- Modes d'utilisation : Transport Mode (communication de bout en bout) et Tunnel Mode (création d'un tunnel VPN entre réseaux).

**Ports utilisés par IPsec :**

- IP (Internet Protocol): UDP/50-51, utilisé pour acheminer les paquets entre le client VPN et le serveur VPN.
- IKE (Internet Key Exchange): UDP/500, utilisé pour établir et maintenir une communication sécurisée entre le client et le serveur VPN.
- ESP (Encapsulating Security Payload): UDP/4500, assure le cryptage du trafic VPN.

## Protocole PPTP (Point-to-Point Tunneling Protocol)

- Depuis 2012, considéré comme non sécurisé en raison de vulnérabilités, remplacé par d'autres protocoles VPN tels que L2TP/IPsec, IPsec/IKEv2 ou OpenVPN.
- Protocole réseau permettant la création de VPN en établissant un tunnel sécurisé et en encapsulant les données transmises.
- Utilisé pour tunneler des protocoles tels que IP, IPX ou NetBEUI via IP.

En résumé, les VPN offrent une solution sécurisée, flexible et rentable pour l'accès à distance aux réseaux privés, permettant aux entreprises de garantir la confidentialité des données et de connecter efficacement des sites distants.

# VLAN et VXLAN

## **Virtual LAN (VLAN) - Réseau Local Virtuel :**

Un réseau local virtuel, ou VLAN, est une méthode de segmentation logique d'un réseau physique, permettant de regrouper des périphériques au sein de domaines distincts, même s'ils partagent le même réseau physique. Cette segmentation offre plusieurs avantages, tels que l'amélioration de la sécurité, de la gestion du trafic et de la flexibilité au sein du réseau.

- **Avantages des VLAN :**
    
    - **Sécurité :** Les VLAN permettent de restreindre la communication entre différents groupes d'appareils, renforçant ainsi la sécurité en limitant l'accès à des ressources spécifiques.
    - **Performance :** La segmentation réduit le trafic de diffusion, améliorant les performances globales du réseau en évitant la congestion inutile.
    - **Gestion :** Les administrateurs réseau peuvent gérer plus efficacement les groupes d'appareils en les organisant logiquement, simplifiant ainsi l'administration du réseau.
- **Attribution des VLAN :**
    
    - Les ports des commutateurs peuvent être attribués à des VLAN de manière statique ou dynamique, permettant aux appareils de faire partie d'un VLAN spécifique en fonction de différents critères tels que l'adresse MAC.
- **Types de Ports VLAN :**
    
    - **Port d'Accès :** Connecte un seul VLAN et est utilisé pour les périphériques finaux.
    - **Port de Liaison :** Connecte plusieurs VLAN et est utilisé pour le trafic entre les commutateurs.

---

## **Virtual eXtensible LAN (VXLAN) - Réseau Local Virtuel eXtensible :**

VXLAN est un protocole de réseau virtuel qui étend les fonctionnalités des VLAN en permettant la création de réseaux locaux virtuels à grande échelle, notamment dans des environnements de centres de données virtualisés.

- **Principales Caractéristiques de VXLAN :**
    
    - **Extension sur le Réseau de couche 3 :** VXLAN permet l'extension d'un réseau de couche 2 sur un réseau de couche 3, facilitant la connectivité dans des environnements distribués.
    - **Identificateurs de segment (VNI) :** Chaque VXLAN est identifié par un numéro appelé VXLAN Network Identifier (VNI), qui permet de distinguer différents réseaux virtuels.
    - **Encapsulation UDP :** VXLAN encapsule les trames Ethernet dans des paquets UDP, facilitant le transport sur des réseaux IP.
- **Utilisations Courantes de VXLAN :**
    
    - **Virtualisation des Data Centers :** VXLAN est largement utilisé dans la virtualisation des centres de données, offrant une flexibilité accrue et une gestion simplifiée.
    - **Connectivité multi-sites :** VXLAN facilite la connectivité entre différents sites géographiques, créant un réseau virtuel global.
- **Interopérabilité :**
    
    - VXLAN est conçu pour être compatible avec divers équipements réseau, offrant une solution flexible pour les besoins évolutifs des infrastructures modernes.

Ces technologies, VLAN et VXLAN, jouent un rôle essentiel dans la conception et la gestion des réseaux informatiques, offrant des solutions puissantes pour répondre aux exigences de sécurité, de performances et de flexibilité.

# Mécanismes d'Échange de Clés 

Les méthodes d'échange de clés sont cruciales pour sécuriser les communications en établissant des clés cryptographiques partagées. Différentes méthodes existent, chacune avec ses avantages et ses limites.

- **Diffie-Hellman (DH) :**
    
    - Permet à deux parties de convenir d'une clé secrète partagée sans communication préalable.
    - Utilisé dans la Sécurité de la couche de transport (TLS) pour des canaux sécurisés.
    - Vulnérable aux attaques de l'homme du milieu (MITM) et exige une puissance CPU significative.
- **Rivest–Shamir–Adleman (RSA) :**
    
    - Repose sur des nombres premiers pour générer une clé secrète partagée.
    - Utilisé dans SSL/TLS pour la protection des données en transit.
    - Considéré comme sécurisé mais demande des calculs intensifs.
- **Courbe Elliptique Diffie-Hellman (ECDH) :**
    
    - Variante efficace et sécurisée de l'échange de clés Diffie-Hellman.
    - Utilisé dans le protocole TLS pour la confidentialité des communications.
- **Échange de Clés Internet (IKE) :**
    
    - Protocole pour établir des sessions de communication sécurisées, notamment dans les VPN.
    - Utilise Diffie-Hellman et d'autres techniques cryptographiques.
    - Opère en mode principal (sécurisé mais plus lent) ou mode agressif (plus rapide mais moins sécurisé).
- **Algorithme de Signature Numérique à Courbe Elliptique (ECDSA) :**
    
    - Utilise la cryptographie à courbe elliptique pour générer des signatures numériques.
    - Garantit sécurité et efficacité dans l'authentification des parties.
- **Comparaison des Algorithmes :**
    
|Algorithme|Acronyme|Sécurité|
    |---|---|---|
    |Diffie-Hellman|DH|Relativement sécurisé, CPU intense|
    |RSA|RSA|Largement utilisé, gourmand en calculs|
    |ECDH|ECDH|Sécurité améliorée, efficace|
    |ECDSA|ECDSA|Sécurité et efficacité accrues|



# Protocole d'authentification

|**Protocole**|**Description**|
|---|---|
|`Kerberos`|Protocole d'authentification basé sur le Key Distribution Center (KDC) qui utilise des tickets dans les environnements de domaine.|
|`SRP`|Il s'agit d'un protocole d'authentification par mot de passe sécurisé qui utilise la cryptographie pour se protéger contre les écoutes clandestines et les attaques de l'homme du milieu..|
|`SSL`|Un protocole cryptographique utilisé pour sécuriser la communication sur un réseau informatique.|
|`TLS`|TLS est un protocole cryptographique qui assure la sécurité des communications sur Internet. C'est le successeur de SSL.|
|`OAuth`|Un standard ouvert d'autorisation qui permet aux utilisateurs d'accorder à des tiers l'accès à leurs ressources Web sans partager leurs mots de passe.|
|`OpenID`|OpenID est un protocole d'authentification décentralisé qui permet aux utilisateurs d'utiliser une seule identité pour se connecter à plusieurs sites Web..|
|`SAML`|Security Assertion Markup Language est une norme basée sur XML pour l'échange sécurisé de données d'authentification et d'autorisation entre les parties..|
|`2FA`|Une méthode d'authentification qui utilise une combinaison de deux facteurs différents pour vérifier l'identité d'un utilisateur.|
|`FIDO`|La Fast IDentity Online Alliance est un consortium d'entreprises travaillant au développement de normes ouvertes pour l'authentification forte.|
|`PKI`|PKI est un système d'échange sécurisé d'informations basé sur l'utilisation de clés publiques et privées pour le cryptage et les signatures numériques..|
|`SSO`|Une méthode d'authentification qui permet à un utilisateur d'utiliser un seul ensemble d'informations d'identification pour accéder à plusieurs applications.|
|`MFA`|MFA est une méthode d'authentification qui utilise plusieurs facteurs, tels que quelque chose que l'utilisateur connaît (un mot de passe), quelque chose qu'il possède (un téléphone) ou quelque chose qu'il est (données biométriques), pour vérifier son identité..|
|`PAP`|Un protocole d'authentification simple qui envoie le mot de passe d'un utilisateur en texte clair sur le réseau.|
|`CHAP`|Un protocole d'authentification qui utilise une négociation à trois pour vérifier l'identité d'un utilisateur.|
|`EAP`|Un cadre pour prendre en charge plusieurs méthodes d'authentification, permettant l'utilisation de diverses technologies pour vérifier l'identité d'un utilisateur..|
|`SSH`|Il s'agit d'un protocole réseau pour une communication sécurisée entre un client et un serveur. Nous pouvons l'utiliser pour l'accès à distance en ligne de commande et à l'exécution de commandes à distance, ainsi que pour le transfert de fichiers sécurisé. SSH utilise le cryptage pour se protéger contre les écoutes clandestines et autres attaques et peut également être utilisé pour l'authentification..|
|`HTTPS`|Il s'agit d'une version sécurisée du protocole HTTP utilisé pour la communication sur Internet. HTTPS utilise SSL/TLS pour crypter les communications et fournir une authentification, garantissant ainsi que des tiers ne peuvent pas intercepter et lire les données transmises. Il est largement utilisé pour sécuriser les communications sur Internet, notamment pour la navigation sur le Web..|
|`LEAP`|LEAP est un protocole d'authentification sans fil développé par Cisco. Il utilise EAP pour fournir une authentification mutuelle entre un client sans fil et un serveur et utilise l'algorithme de cryptage RC4 pour crypter la communication entre les deux. Malheureusement, LEAP est vulnérable aux attaques par dictionnaire et à d'autres failles de sécurité et a été largement remplacé par des protocoles plus sécurisés tels que EAP-TLS et PEAP..|
|`PEAP`|PEAP, quant à lui, est un protocole de tunneling sécurisé utilisé pour les réseaux sans fil et filaires. Il est basé sur EAP et utilise TLS pour crypter la communication entre un client et un serveur. PEAP utilise un certificat côté serveur pour authentifier le serveur et peut également être utilisé pour authentifier le client à l'aide de diverses méthodes, telles que des mots de passe, des certificats ou des données biométriques. PEAP est largement utilisé dans les réseaux d'entreprise pour une authentification sécurisée.|
# Introduction à la Cryptographie

La cryptographie est l'art de sécuriser les informations par le biais de techniques de chiffrement. Dans le contexte des réseaux informatiques, elle est utilisée pour protéger la confidentialité et l'intégrité des données transmises sur Internet.

### Chiffrement Symétrique

Le chiffrement symétrique, également connu sous le nom de chiffrement par clé secrète, utilise une clé unique pour chiffrer et déchiffrer les données. Des algorithmes tels que l'Advanced Encryption Standard (AES) et le Data Encryption Standard (DES) sont des exemples de chiffrement symétrique couramment utilisés.

### Chiffrement Asymétrique

Le chiffrement asymétrique, ou chiffrement par clé publique, utilise une paire de clés : une clé publique pour chiffrer et une clé privée pour déchiffrer. Les algorithmes RSA, PGP et Elliptic Curve Cryptography (ECC) sont largement utilisés pour assurer la sécurité des communications.

### Avantages du Chiffrement Asymétrique

La cryptographie asymétrique offre une sécurité renforcée en éliminant le besoin d'échanger secrètement des clés. Elle est utilisée dans des applications telles que les signatures électroniques, SSL/TLS, et les VPN.

### Data Encryption Standard (DES)

Le DES est un chiffrement symétrique par bloc qui utilise une clé de 56 bits. Son extension, Triple DES (3DES), renforce la sécurité en utilisant trois cycles de chiffrement. Cependant, AES, successeur du DES, offre une sécurité supérieure.

### Advanced Encryption Standard (AES)

AES utilise des clés plus longues (128, 192, ou 256 bits) pour chiffrer et déchiffrer les données. Il est plus rapide et plus sécurisé que le DES, ce qui le rend largement utilisé dans diverses applications et protocoles, notamment WLAN IEEE 802.11i, IPsec, et VoIP.

### Modes de Chiffrement

Différents modes de chiffrement par bloc, tels que ECB, CBC, CFB, OFB, CTR, et GCM, sont utilisés pour traiter et combiner les blocs de données de manière à assurer la confidentialité et l'intégrité des messages.

## Conclusion

La cryptographie dans les réseaux informatiques est une composante essentielle de la sécurité des données. En comprenant les principes du chiffrement symétrique et asymétrique, ainsi que les différents modes de chiffrement, les professionnels de la sécurité peuvent mettre en œuvre des solutions robustes pour protéger les informations sensibles transmises sur les réseaux.