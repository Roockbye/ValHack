# Crack the hash

### **Outils**

Tout d’abord voici quelques sites intéressant pour cracker des hash

[https://hashes.com/en/decrypt/hash](https://hashes.com/en/decrypt/hash)

[https://crackstation.net/](https://crackstation.net/)

[https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)

[https://dencode.com/](https://dencode.com/)

[https://www.tunnelsup.com/hash-analyzer/](https://www.tunnelsup.com/hash-analyzer/)

Il existe également des outils sur Kali comme: **Hash-Identifier** et **Hashcat**

On peut également utiliser **John The Ripper**

```powershell
john <format> <wordlist> <hash>
```

### **Hash**

Les fonctions de hachage transforment les données en une représentation numérique unique et caractéristique, appelée hash. L'une des propriétés fondamentales des fonctions de hachage est que deux ensembles de données différents ne devraient pas produire le même hash. De plus, il doit être difficile de retrouver les données d'origine à partir du hash, ce qui rend le hash unidirectionnel. Même une petite modification dans les données d'entrée devrait produire un hash complètement différent.

Exemples et aides sur les hash:

[https://hashcat.net/wiki/doku.php?id=example\_hashes](https://hashcat.net/wiki/doku.php?id=example\_hashes)

[https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats](https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats)
