# Documentation
## subgXX
Le script subgXX (XX=16 actuellement) permet de lancer des calculs avec gaussian sur notre cluster.
Il utilise :
 - le fichier com
 - le fichier .fchk.gz s'il existe

À la fin du calcul, on obtient dans le répertoire de travail :
 - le fichier .log
 - le fichier .fchk.gz mis à jour

### Pourquoi pas le fichier .chk?
Les fichiers .chk générés par gaussian sont très gros. Les fichiers formaté (.fchk) et compressés (.gz) prennent moins de place sur le disque.

### Comment ça marche ?
1. Au départ du job, le fichier .com et le fichier .fchk.gz sont copiés sur le disque scratch.
```
cp ${repertoire de travail}/molecule.com ${repertoire de travail}/molecule.fchk.gz ${repertoire scratch}/
```
2. Le fichier .fchk.gz est transformé en .chk
```
cd ${repertoire scratch}
gunzip molecule.fchk.gz #crée le fichier molecule.fchk
unfchk ${fchknam} #crée le fichier molecule.chk
```
3. Le calcul est lancé avec comme fichier de sortie le fichier .log __dans le repertoire de travail__
```
g16 < molecule.com > ${repertoire de travail}/molecule.log
```
4. Une fois le calcul terminé on rapatrie le fichier .fchk.gz issu du calcul:
```
formchk molecule.chk
gzip molecule.fchk
cp molecule.fchk.gz ${repertoire de travail}
```

### OK et alors?
Vous aurez noté que seul le fichier .fchk.gz est rapatrié vers votre répertoire de travail: si votre calcul gaussian génère d'autres fichiers il faudra s'occuper de les récupérer par vous même.
