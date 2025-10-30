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

<img src="/assets/Exercice2(part1).png" height="100%" width="100%"> 

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
    
-   On observe bien (au dessus de la ligne rouge) que les 10 dernières lignes s'affichent


<img src="/assets/Exercice2(part2).png" height="100%" width="100%"> 


### Étape 5 :

`grep "error" log.txt`

- permet d'afficher les lignes de `log.txt` qui contiennent le mot "error"

## Exercice 3

<img src="/assets/Exercice3.png" height="100%" width="100%"> 

### Etape 1
`touch secret.txt`
- je créé un fichier secret.txt comme demandé
-`ls` permet simplement qu'il a bien été créé

### Etape 2

`chmod 600 secret.txt`
- permet de changer les permissions, le rendant accessible (lecture et écriture)

### Etape 3
`ls -l secret.txt`
- Cette commande permet de voir les permissions accordées par le fichier secret.txt
- On voit bien que le r de "read" et le w de "write" sont présents.


----------------------------------------------------------

# Exercices Intermédiaires 
## Exercice 1

### 1) Ouvrir **htop** et trier par mémoire
```bash
htop
```
- Dans *htop*, j’ai trié sur la colonne **MEM%** pour inverser l’ordre de tri.  
- En tri decroissant, le processus qui consomme le **plus** de RAM est **en haut** de la liste.  
- ici le PID du processus le plus haut est 2256 

---

### 2) Changer la priorité (*renice*) d’un processus
```bash
sudo renice -n 0 -p 4452
```
- J’ai ciblé le PID **4452**.  
- La sortie a affiché : *old priority 0, new priority 0* → cela signifie que la **priorité était déjà à 0**, donc **pas de changement**.

---

### 3) Terminer un processus par son PID
```bash
sudo kill 4452
```


------------------------------------------------------------------------

Screenshot : 
![test4](https://i.imgur.com/jdVCMiM.png) 

------------------------------------------------------------------------


# Exercice Intermédiaire 2



## 1) Créer le script
```bash
nano /home/pepitodelanoche/backups/backup_docs.sh
```
Contenu :
```bash
mkdir -p /home/pepitodelanoche/backups
cp -a /home/pepitodelanoche/Documents/ /home/pepitodelanoche/backups/
```
> `mkdir -p` crée le dossier s'il n'existe pas.  
> `Documents/` (slash) = copie **le contenu** de `Documents` *dans* `backups/`.

---

## 2) Planifier avec cron (tous les jours à 02:00)
```bash
crontab -e
```
Ajouter cette ligne :
```
0 2 * * * sh /home/pepitodelanoche/backups/backup_docs.sh
```

----------------------------------------------------------

Screenshot : 
![test5](https://i.imgur.com/SZtLcBg.png)

----------------------------------------------------------

## 3) # TP - Exercices Intermédiaire

### Objectif
Analyser les logs du service SSH pour identifier et sauvegarder les tentatives de connexion échouées.

### Instructions

#### 1. Afficher les logs du service SSH sur les 24 dernières heures

- Pour consulter les logs SSH des dernières 24 heures, utilisez la commande suivante :

```journalctl -u ssh --since "24 hours ago"```

Ou pour les systèmes utilisant `sshd` :

```journalctl -u sshd --since "24 hours ago"```


**Alternative avec les fichiers de logs :**

```grep "sshd" /var/log/auth.log | tail -n 100```


#### 2. Filtrer les logs pour avoir que les connexions ratées

- Pour afficher uniquement les tentatives de connexion échouées :

```journalctl -u ssh --since "24 hours ago" | grep "Failed"``` 


Ou :

```grep "Failed password" /var/log/auth.log``` 


#### 3. Sauvegarde tout dans un fichier sshd_failed_logins.txt

- Pour sauvegarder les résultats dans un fichier :

`journalctl -u ssh --since "24 hours ago" | grep "Failed" > sshd_failed_logins.txt`


Ou avec les fichiers de logs :

`grep "Failed password" /var/log/auth.log > sshd_failed_logins.txt`


**Comment faire :**

- Avec journalctl :
`journalctl -u sshd --since "24 hours ago" | grep -E "Failed password|Invalid user" > sshd_failed_logins.txt`

- Avec auth.log :
`grep -E "Failed password|Invalid user" /var/log/auth.log | grep "$(date -d '24 hours ago' '+%b %d')" > sshd_failed_logins.txt`


