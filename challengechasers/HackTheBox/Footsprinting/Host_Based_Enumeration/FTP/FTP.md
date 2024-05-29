# Le Protocole de Transfert de Fichiers (FTP)

Le **File Transfer Protocol (FTP)** est l'un des plus anciens protocoles Internet, fonctionnant dans la couche application de la pile TCP/IP. Il utilise des programmes spécifiques ou des navigateurs pour transférer des fichiers.

## Fonctionnement

### Connexion FTP

1. **Canal de contrôle** : Établi via le port TCP 21, où le client envoie des commandes et le serveur renvoie des codes d'état.
2. **Canal de données** : Utilisé pour la transmission de données via le port TCP 20, surveillant les erreurs et permettant la reprise en cas d'interruption.

### Modes de FTP

- **FTP Actif** : Le client se connecte au port 21 et spécifie un port client pour les réponses. Problème avec les pare-feu.
- **FTP Passif** : Le serveur spécifie un port pour le client, permettant de contourner les pare-feu.

## Commandes et Codes d'État

Le FTP utilise des commandes pour gérer les fichiers et répertoires, avec des réponses sous forme de codes d'état. Toutes les commandes ne sont pas uniformément implémentées sur tous les serveurs.

## Sécurité

- **Credentials** : Nécessaires pour la connexion FTP, avec le risque que les données soient en texte clair et interceptées.
- **FTP Anonyme** : Permet aux utilisateurs de se connecter sans mot de passe, avec des restrictions pour des raisons de sécurité.

# Le Protocole de Transfert de Fichiers Trivial (TFTP)

Le **Trivial File Transfer Protocol (TFTP)** est plus simple que le FTP et permet les transferts de fichiers entre les processus client et serveur. Contrairement au FTP, il n'offre pas d'authentification utilisateur ni d'autres fonctionnalités avancées.

## Différences avec FTP

- **Protocole** : TFTP utilise UDP, rendant le protocole moins fiable, tandis que FTP utilise TCP.
- **Authentification** : TFTP ne nécessite pas d'authentification utilisateur et ne prend pas en charge les connexions protégées par mot de passe.
- **Permissions** : L'accès est limité aux permissions de lecture et d'écriture des fichiers dans le système d'exploitation, ce qui restreint TFTP à des fichiers et répertoires accessibles globalement.

## Utilisation

En raison de son manque de sécurité, TFTP est recommandé uniquement pour les réseaux locaux et protégés.

## Commandes TFTP

| Commande | Description |
|----------|-------------|
| `connect` | Définit l'hôte distant, et éventuellement le port, pour les transferts de fichiers. |
| `get` | Transfère un fichier ou un ensemble de fichiers de l'hôte distant à l'hôte local. |
| `put` | Transfère un fichier ou un ensemble de fichiers de l'hôte local à l'hôte distant. |
| `quit` | Quitte TFTP. |
| `status` | Affiche l'état actuel de TFTP, y compris le mode de transfert (ASCII ou binaire), le statut de connexion, la valeur de temporisation, etc. |
| `verbose` | Active ou désactive le mode verbeux, qui affiche des informations supplémentaires lors du transfert de fichiers. |

Contrairement au client FTP, TFTP ne dispose pas de fonctionnalité de listing de répertoires.
