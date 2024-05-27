# Default Configuration SMB

Comme on peut l'imaginer, Samba offre une large gamme de paramètres que nous pouvons configurer. Encore une fois, nous définissons les paramètres via un fichier texte où nous pouvons obtenir un aperçu de certains des paramètres. Voici à quoi ressemblent ces paramètres une fois filtrés :

```bash 
cat /etc/samba/smb.conf | grep -v "#\|\;" 
```

Jetons un coup d'œil à certains des paramètres pour comprendre comment les partages sont configurés dans Samba.

| Paramètre                  | Description                                                                                                     |
|----------------------------|-----------------------------------------------------------------------------------------------------------------|
| `[sharename]`              | Nom du partage réseau.                                                                                          |
| `workgroup = WORKGROUP`   | Groupe de travail visible lors des requêtes clients.                                                             |
| `path = /path/here/`      | Répertoire auquel l'utilisateur doit avoir accès.                                                                |
| `server string = STRING`  | Chaîne qui s'affichera lorsqu'une connexion sera initiée.                                                       |
| `unix password sync = yes`| Synchroniser le mot de passe UNIX avec le mot de passe SMB ?                                                    |
| `usershare allow guests = yes` | Autoriser les utilisateurs non authentifiés à accéder au partage défini ?                                   |
| `map to guest = bad user` | Que faire lorsqu'une demande de connexion utilisateur ne correspond pas à un utilisateur UNIX valide ?         |
| `browseable = yes`         | Ce partage doit-il être affiché dans la liste des partages disponibles ?                                        |
| `guest ok = yes`           | Autoriser la connexion au service sans utiliser de mot de passe ?                                                |
| `read only = yes`          | Autoriser les utilisateurs à lire uniquement les fichiers ?                                                      |
| `create mask = 0700`      | Quels droits doivent être définis pour les fichiers nouvellement créés ?                                         |

**Dangerous Settings**

Certains des paramètres ci-dessus offrent déjà des options sensibles. Cependant, si nous remettons en question les paramètres listés ci-dessous et nous nous demandons ce que les employés et les attaquants pourraient en retirer, nous verrons les avantages et les inconvénients qu'ils apportent. Prenons le paramètre `browseable = yes` par exemple. Si nous, en tant qu'administrateurs, adoptons ce paramètre, les employés de l'entreprise auront le confort de pouvoir consulter les dossiers individuels avec leur contenu. Si l'employé peut parcourir les partages, l'attaquant pourra également le faire après avoir réussi à accéder.

| Paramètre                  | Description                                                                                                     |
|----------------------------|-----------------------------------------------------------------------------------------------------------------|
| `browseable = yes`         | Autoriser la liste des partages disponibles dans le partage actuel ?                                             |
| `read only = no`           | Interdire la création et la modification de fichiers ?                                                           |
| `writable = yes`           | Autoriser les utilisateurs à créer et modifier des fichiers ?                                                    |
| `guest ok = yes`           | Autoriser la connexion au service sans utiliser de mot de passe ?                                                |
| `enable privileges = yes`  | Respecter les privilèges attribués à un SID spécifique ?                                                         |
| `create mask = 0777`       | Quels droits doivent être attribués aux fichiers nouvellement créés ?                                            |
| `directory mask = 0777`    | Quels droits doivent être attribués aux répertoires nouvellement créés ?                                         |
| `logon script = script.sh` | Quel script doit être exécuté à la connexion de l'utilisateur ?                                                  |
| `magic script = script.sh` | Quel script doit être exécuté lorsque le script se ferme ?                                                       |
| `magic output = script.out`| Où doit être stockée la sortie du script magique ?                                                               |

