# Documentation
##subgXX
Le script subgXX (XX=16 actuellement) permet de lancer des calculs avec gaussian sur notre cluster.
Il utilise :
 - le fichier com
 - le fichier fchk.gz s'il existe
### Pourquoi pas le fichier chk?
 Les fichiers chk générés par gaussian sont très gros. Les fichiers formaté (fchk) et compressés (gz) prennent moins de place sur le disque.
### Comment ça marche ?
 Au départ du job, le fichier com et le fichier fchk.gz sont copiés sur le disque scratch.
