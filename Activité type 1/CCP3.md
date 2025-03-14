# Exploiter des serveurs Linux
## La gestion du stockage
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


---

## Gestion des processeurs et mémoire

---

## Gestion des utilisateurs

---

## Cryptographie

---

## SSH

---

## HTTP et serveurs web
