# Méthodologie d'Énumération en Cybersécurité


Les tests d'intrusion, et donc l'énumération, sont des processus dynamiques. Cette méthodologie est structurée en 6 couches et représente, métaphoriquement parlant, des frontières que nous essayons de franchir avec le processus d'énumération. Le processus d'énumération entier est divisé en trois niveaux différents :

1. Énumération basée sur l'infrastructure
2. Énumération basée sur l'hôte
3. Énumération basée sur le système d'exploitation

![Image](./image/enum-method3.png)

**Note :** Les composants de chaque couche représentés ici sont les catégories principales et non une liste complète de tous les composants à rechercher. De plus, il convient de mentionner que les première et deuxième couches (Présence sur Internet, Passerelle) ne s'appliquent pas tout à fait à l'intranet, comme une infrastructure Active Directory. Les couches pour l'infrastructure interne seront couvertes dans d'autres modules.

Imaginez ces lignes comme un obstacle, comme un mur par exemple. Ce que nous faisons ici, c'est chercher où se trouve l'entrée, ou la faille par laquelle nous pouvons passer, ou grimper pour nous rapprocher de notre objectif. Théoriquement, il est également possible de passer à travers le mur tête baissée, mais très souvent, il arrive que l'endroit où nous avons créé une brèche avec beaucoup d'efforts et de temps ne nous apporte pas grand-chose car il n'y a pas d'entrée à cet endroit pour passer au mur suivant.

Ces couches sont conçues comme suit :

| Couche                 | Description                                                        | Catégories d'information                                 |
|------------------------|--------------------------------------------------------------------|---------------------------------------------------------|
| 1. Présence sur Internet | Identification de la présence sur Internet et de l'infrastructure accessible de l'extérieur. | Domaines, Sous-domaines, vHosts, ASN, Netblocks, Adresses IP, Instances Cloud, Mesures de sécurité |
| 2. Passerelle          | Identification des mesures de sécurité possibles pour protéger l'infrastructure externe et interne de l'entreprise. | Pare-feux, DMZ, IPS/IDS, EDR, Proxys, NAC, Segmentation du réseau, VPN, Cloudflare |
| 3. Services Accessibles | Identification des interfaces et services accessibles hébergés en externe ou en interne. | Type de service, Fonctionnalité, Configuration, Port, Version, Interface |
| 4. Processus           | Identification des processus internes, des sources et des destinations associés aux services. | PID, Données traitées, Tâches, Source, Destination |
| 5. Privilèges          | Identification des permissions et privilèges internes pour les services accessibles. | Groupes, Utilisateurs, Permissions, Restrictions, Environnement |
| 6. Configuration OS    | Identification des composants internes et de la configuration du système d'exploitation. | Type de système d'exploitation, Niveau de correctif, Configuration du réseau, Environnement OS, Fichiers de configuration, fichiers privés sensibles |

**Remarque importante :** L'aspect humain et les informations pouvant être obtenues par les employés à l'aide de l'OSINT ont été retirés de la couche "Présence sur Internet" pour simplifier.



 Même après un test d'intrusion de quatre semaines, nous ne pouvons pas dire à 100 % qu'il n'y a plus de vulnérabilités. Quelqu'un qui a étudié l'entreprise pendant des mois et les a analysées aura probablement une compréhension beaucoup plus grande des applications et de la structure que nous avons pu acquérir au cours des quelques semaines passées sur l'évaluation. Un excellent exemple récent est l'attaque cybernétique sur SolarWinds. C'est une autre excellente raison pour une méthodologie qui doit exclure de tels cas.

Supposons que nous avons été chargés de réaliser un test d'intrusion "boîte noire" externe. Une fois tous les éléments contractuels nécessaires complètement remplis, notre test d'intrusion commencera à l'heure spécifiée.

### Couche No.1 : Présence sur Internet

La première couche que nous devons franchir est la couche "Présence sur Internet", où nous nous concentrons sur la recherche des cibles que nous pouvons investiguer. Si le périmètre du contrat nous permet de rechercher des hôtes supplémentaires, cette couche est encore plus critique que pour les cibles fixes uniquement. Dans cette couche, nous utilisons différentes techniques pour trouver des domaines, des sous-domaines, des netblocks, et de nombreux autres composants et informations qui présentent la présence de l'entreprise et de son infrastructure sur Internet.

L'objectif de cette couche est d'identifier tous les systèmes cibles et interfaces possibles qui peuvent être testés.

### Couche No.2 : Passerelle

Ici, nous essayons de comprendre l'interface de la cible atteignable, comment elle est protégée et où elle est située dans le réseau. En raison de la diversité, des fonctionnalités différentes et de certaines procédures particulières, nous aborderons cette couche plus en détail dans d'autres modules.

L'objectif est de comprendre avec quoi nous traitons et ce que nous devons surveiller.

### Couche No.3 : Services Accessibles

Dans le cas des services accessibles, nous examinons chaque destination pour tous les services qu'elle offre. Chacun de ces services a un objectif spécifique qui a été installé pour une raison particulière par l'administrateur. Chaque service a certaines fonctions, qui conduisent donc à des résultats spécifiques. Pour travailler efficacement avec eux, nous devons savoir comment ils fonctionnent. Sinon, nous devons apprendre à les comprendre.

Cette couche vise à comprendre la raison et la fonctionnalité du système cible et à acquérir les connaissances nécessaires pour communiquer avec lui et l'exploiter à nos fins de manière efficace.

C'est la partie de l'énumération que nous traiterons principalement dans ce module.

### Couche No.4 : Processus

Chaque fois qu'une commande ou une fonction est exécutée, des données sont traitées, qu'elles soient saisies par l'utilisateur ou générées par le système. Cela démarre un processus qui doit accomplir des tâches spécifiques, et de telles tâches ont au moins une source et une cible.

L'objectif ici est de comprendre ces facteurs et d'identifier les dépendances entre eux.

### Couche No.5 : Privilèges

Chaque service fonctionne par l'intermédiaire d'un utilisateur spécifique dans un groupe particulier avec des permissions et des privilèges définis par l'administrateur ou le système. Ces privilèges nous offrent souvent des fonctions que les administrateurs négligent. Cela se produit souvent dans les infrastructures Active Directory et de nombreux autres environnements et serveurs d'administration spécifiques où les utilisateurs sont responsables de plusieurs domaines d'administration.

Il est crucial de les identifier et de comprendre ce qui est et n'est pas possible avec ces privilèges.

### Couche No.6 : Configuration OS

Ici, nous collectons des informations sur le système d'exploitation réel et sa configuration en utilisant un accès interne. Cela nous donne une bonne vue d'ensemble de la sécurité interne des systèmes et reflète les compétences et les capacités des équipes administratives de l'entreprise.
