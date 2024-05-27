# SMB

**Protocole SMB**

Le Server Message Block (SMB) est un protocole client-serveur régulant l'accès aux fichiers et autres ressources réseau. Principalement utilisé dans les systèmes Windows, il permet la communication entre différentes versions du système d'exploitation. Le projet Samba offre une solution similaire pour les distributions Linux et Unix, permettant ainsi la communication interplateforme via SMB.

Un serveur SMB peut fournir des parties arbitraires de son système de fichiers local sous forme de partages. Ainsi, la hiérarchie visible pour un client est partiellement indépendante de la structure sur le serveur. Les droits d'accès sont définis par des Listes de Contrôle d'Accès (ACL) permettant un contrôle fin basé sur des attributs tels que l'exécution, la lecture et l'accès complet pour des utilisateurs ou groupes d'utilisateurs individuels. Les ACL sont définies en fonction des partages et ne correspondent donc pas aux droits attribués localement sur le serveur.

**Samba **

Samba fonctionne sur Linux et Windows, permettant à chaque hôte de partager des ressources dans un groupe de travail. IBM a créé NetBIOS pour la connexion et le partage de données entre ordinateurs. Chaque machine a besoin d'un nom pour se connecter en ligne, soit en réservant son nom d'hôte, soit via NBNS ou WINS.
