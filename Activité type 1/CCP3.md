# Exploiter des serveurs Linux
## 📌 La gestion du stockage
### L'abstraction
- **Chemin absolu** : Définit un chemin complet à partir de la racine (`/`), comme `/home/wilder/` ou `/var/log/auth.log`.
- **Chemin relatif** : Définit un chemin par rapport au répertoire courant, comme `./wilder` ou `./auth.log`.
- **Variable d'environnement PATH** : Définit les répertoires dans lesquels le système recherche les exécutables. Exemple : `$PATH`.

### Les systèmes de fichier
#### EXT4 (Fourth Extended File System)
EXT4 est le système de fichiers principal sous Linux, basé sur la famille EXT (EXT2, EXT3). Il offre de meilleures performances et fonctionnalités que ses prédécesseurs.  
**Avantages du EXT4** :
- **Limite la fragmentation (extent)** : Utilise des extents pour améliorer la gestion des fichiers et réduire la fragmentation.
- **Défragmentation en ligne** : Permet de réorganiser les fichiers fragmentés sans redémarrage du système.
- **Journalisation** : Permet de récupérer les données après un plantage, comme NTFS.
- **Compression** : Bien que non native, des outils tiers permettent de compresser les données.
- **Chiffrement** : Supporte le chiffrement des données via des outils externes pour renforcer la sécurité.

### L'arborescence classique
Sous Linux, les répertoires sont organisés selon la hiérarchie des fichiers UNIX (FHS).
- **/bin** : Exécutables essentiels pour l'utilisateur.
- **/boot** : Fichiers nécessaires au démarrage du système, y compris le noyau.
- **/dev** : Fichiers représentant les périphériques matériels (disques, ports série…).
- **/etc** : Fichiers de configuration du système.
- **/home** : Répertoires personnels des utilisateurs.
- **/lib** : Bibliothèques partagées.
- **/mnt**, **/media**, **/cdrom** : Points de montage temporaires (disques externes, CD/DVD…).
- **/opt** : Logiciels non standards installés manuellement.
- **/proc** : Informations sur les processus et le noyau.
- **/root** : Répertoire personnel de l'utilisateur root.
- **/sbin** : Exécutables pour l'administration du système.
- **/sys** : Informations sur l'état actuel du système.
- **/tmp** : Données temporaires.
- **/usr** : Programmes et ressources standards.
- **/var** : Données variables, comme les logs et caches.

### Fichiers dans /dev et Outils de gestion de systèmes de fichiers
#### Fichiers dans /dev
Les fichiers dans /dev sont utilisés pour accéder aux périphériques matériels.
- **Disques IDE** : 
  - Format : `/dev/hdX` avec X = a, b, c…
  - **Partitions** : `/dev/hdXP` avec P = 1, 2, 3…
- **Disques SATA** : 
  - Format : `/dev/sdX` avec X = a, b, c…
  - **Partitions** : `/dev/sdXP` avec P = 1, 2, 3…
- **Disques NVMe** :
  - Format : `/dev/nvmeYnZ` avec Y = 0, 1, 2… et Z = 1, 2, 3…
  - **Partitions** : `/dev/nvmeYnZpP` avec P = 1, 2, 3…

#### Règles de numérotation
- La numérotation des disques et partitions suit l'ordre de leur détection.
- Un disque peut changer de nom, notamment après un redémarrage.

#### Outils pour la création de systèmes de fichiers
- **Commande principale** : `mkfs` (exemple pour formater en ext4) :
```bash
mkfs.ext4 /dev/sdX
```

#### À la création d'un système de fichier
1. **UUID** : Un identifiant unique pour chaque système de fichiers.
2. **Étiquette (Label)** : Possibilité d'attribuer un label au système de fichiers.
3. **Paramètres** : Choix des options (taille des blocs, journalisation…).

#### Outils complémentaires
- **fsck** : Vérifie et répare les systèmes de fichiers.
- **resize2fs** : Redimensionne un système de fichiers ext2/3/4.
- **e2label** : Change l'étiquette d'un système de fichiers ext2/3/4.
- **badblocks** : Recherche les blocs défectueux.
- **tune2fs** : Paramètre un système de fichiers ext2/3/4 (ex : fréquence des vérifications).

### Commandes utiles pour la gestion du stockage

#### Gestion des périphériques et UUID
- **lsblk** : Affiche les périphériques de stockage et leurs UUID.
- **blkid** : Affiche des informations similaires mais à un niveau plus bas.
- **Liens symboliques dans /dev/disk/by-uuid** : Utilisés pour accéder aux périphériques via leur UUID.

#### Monter et démonter des systèmes de fichiers
- **mount** : Monte un système de fichiers dans l'arborescence :
    - Syntaxe : `mount /dev/sdX /chemin/de/montage`
- **umount** : Démonte un système de fichiers :
    - Syntaxe : `umount /chemin/de/montage`
- **/etc/fstab** : Fichier de configuration pour les montages automatiques au démarrage.

#### Commandes de gestion de fichiers
- **pwd** : Affiche le répertoire courant.
- **ls** : Affiche le contenu d'un répertoire.
- **cat** : Affiche le contenu d'un fichier.
- **more/less** : Affichage paginé du contenu d'un fichier.
- **head/tail** : Affiche le début ou la fin d'un fichier.
- **cp** : Copie un fichier ou un dossier.
- **mv** : Déplace ou renomme un fichier ou un dossier.
- **rm** : Supprime un fichier ou un dossier.
- **mkdir** : Crée un dossier.
- **rmdir** : Supprime un dossier (vide).
- **touch** : Crée un fichier ou met à jour la date d'accès.
- **which/whereis/locate** : Trouve un fichier.
- **diff** : Affiche les différences entre deux fichiers.
- **wc** : Compte les lignes, mots ou caractères d'un fichier.
- **grep** : Filtre les lignes d'un fichier en fonction d'un motif.
- **find** : Recherche des fichiers.
- **sed** : Édition de fichier texte en ligne.
- **awk** : Traitement de fichier par champs.

---

## 📌 Gestion des processeurs et mémoire  

### Les métadonnées  
Chaque processus possède des informations spécifiques :  
- **PID** → Identifiant du processus  
- **PPID** → Identifiant du processus parent  
- **CMD** → Commande de lancement  
- **UID** → Identifiant utilisateur associé  
- **GID** → Identifiant groupe associé  
- **TTY** → Terminal d’entrée/sortie  

### Messages standards  
💡 **Un processus peut envoyer un signal à un autre processus :**  
- `SIGINT` → Interruption (CTRL + C dans un terminal)  
- `SIGTERM` → Demande d’arrêt propre  
- `SIGKILL` → Destruction forcée du processus par le noyau  
- `SIGTSTP` → Mise en pause (`CTRL + Z`), reprise avec `fg`  
- `SIGQUIT` → Arrêt avec **core dump** (`CTRL + \`)  
- `SIGSEGV` → Erreur de segmentation (accès mémoire interdit)  

👉 **La commande `kill` permet d'envoyer des signaux aux processus.**  

### Quelques commandes utiles  

#### 📋 Gestion des processus  
- `ps` → Liste les processus  
- `pstree` → Affiche l’arborescence des processus  
- `top` → Liste les processus en temps réel selon leur consommation CPU  
- `htop` → Version interactive de `top`  

#### ❌ Gestion des signaux  
- `kill` / `killall` → Envoi de signaux aux processus (ex: arrêt d’un programme)  
- `fg` → Passe un processus en **premier plan**  
- `bg` → Relance un processus en pause en **arrière-plan**  
- `<commande> &` → Lance une commande directement en arrière-plan  
- `nohup <commande>` → Lance un processus **détaché** de la session utilisateur  
  - Ex: `nohup my_script.sh &` (continue même après fermeture du terminal)  

#### ⏳ Planification des tâches  
- `cron` → Exécute des tâches récurrentes  
- `crontab` → Configure les tâches automatiques de `cron`  
- `at` / `atq` / `atrm` / `batch` → Planifie des tâches uniques  

---

## 📌 Gestion des utilisateurs  

### Les types de droits d’accès  
Tout fichier ou dossier possède des droits attribués à 3 catégories :  
- **UID (User ID)** → Propriétaire du fichier (**s’applique à l’utilisateur ayant le même UID**)  
- **GID (Group ID)** → Groupe propriétaire du fichier (**s’applique aux membres de ce groupe**)  
- **Other** → Tous les autres utilisateurs (**ne rentrant pas dans les deux premières catégories**)  

###  L’affichage des droits d’accès  
Les droits apparaissent sous la forme d’une chaîne de **10 caractères** :  
- **1er caractère** → Type de fichier (**répertoire, fichier, lien symbolique, etc.**)  
- **3x3 caractères suivants** → Définissent les droits pour les **User, Group, Other**  
- **Un `-` signifie l’absence de droit**  

### **Commande pour afficher les droits d’un fichier/dossier** :  
```bash
ls -l
```
### **Les droits avancés ACL**
Les ACL (Access Control Lists) permettent de définir des droits plus précis que le modèle classique.

✅ Exemple : Ajouter un accès en lecture pour l’utilisateur `wilder` sur le fichier `text.txt`

```bash
setfacl -m u:wilder:r text.txt
```
### **Afficher les droits ACL :**

``` bash
getfacl text.txt
```
### Quelques commandes utiles
- `ls -l` → Affiche les droits des fichiers d’un répertoire
- `chown utilisateur:fichier` → Change le propriétaire d’un fichier
- `chmod 755 fichier` → Modifie les droits d’accès
- `setfacl -m u:utilisateur:permission fichier` → Ajoute/Supprime des droits ACL
- `getfacl fichier` → Affiche les droits ACL

---

## Cryptographie

---

## SSH

---

## HTTP et serveurs web
