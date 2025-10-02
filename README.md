# Exercices - Débutant
## Exercice 1



-   `ls` — j'ai listé le contenu du répertoire courant.
    
-   `mkdir files` — j'ai créé un dossier nommé `files`.
    
-   `cd files` — j'entre dans le dossier `files`.
    
-   `touch fichier1.txt` — j'ai créé un premier fichier : `fichier1.txt`.
    
-   `touch fichier2.txt` — deuxième fichier : `fichier2.txt`.
    
-   `touch .fichier3.txt` — troisième fichier **caché** `.fichier3.txt`.
    
-   `ls` — vérifier les fichiers visibles dans `files` (les fichiers cachés ne s’affichent donc pas).
    
-   `cd ../` — afin revenir au répertoire parent.
    
-   `ls` — pour lister le contenu de `~` pour voir les dossiers dont `files`.
    
-   `cp files/fichier1.txt fichier1bis.txt` 
- — copier `fichier1.txt` de `files/` vers `~` sous le nom `fichier1bis.txt`.
    
-   `ls` — vérifier que `fichier1bis.txt` est bien présent dans `~`.

<img src="/assets/exercice1(débutant).png" height="100%" width="100%"> 



## Exercice 2


### Étape 1 :

`ls /etc > log.txt` 

-  cette commande permet de créer  un fichier  log.txt  qui  contient  la  liste  des  fichiers  de  /etc.

----------

### Étape 2 :

`ls` 

-   j'affiche juste  le contenu du dossier courant (`~/Documents`) pour vérifier que `log.txt` a bien été créé.    

----------

### Étape 3 :

`sudo tail -n 10 /var/log/syslog >> log.txt` 

- Affiche les 10 dernières lignes de `/var/log/syslog` avec `sudo` et les ajoute à la fin de `log.txt` sans l’écraser.

----------

### Étape 4 :

`cat log.txt` 

-   Affiche le contenu du fichier `log.txt`.
    
<img src="/assets/Exercice2(part1).png" height="100%" width="100%"> 

-   On observe bien (au dessus de la ligne rouge) que les 10 dernières lignes s'affichent

### Étape 5 :

`grep "error" log.txt`

- permet d'afficher les lignes de `log.txt` qui contiennent le mot "error"

<img src="/assets/Exercice2(part2).png" height="100%" width="100%"> 