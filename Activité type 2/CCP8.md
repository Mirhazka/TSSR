# Mettre en place, assurer et tester les sauvegardes et les restaurations des éléments de l'infrastructure

## Sauvegarde 🗂️

### Types de sauvegarde
Il existe plusieurs types de sauvegarde, chacun ayant ses propres avantages et inconvénients :

- **Sauvegarde complète** : Sauvegarde de l'ensemble des données sélectionnées. Elle prend beaucoup de temps mais permet une restauration rapide.
- **Sauvegarde incrémentielle** : Sauvegarde des données modifiées depuis la dernière sauvegarde, qu'elle soit complète ou incrémentielle. Elle est rapide mais nécessite toutes les sauvegardes précédentes pour une restauration.
- **Sauvegarde différentielle** : Sauvegarde des données modifiées depuis la dernière sauvegarde complète. Elle est plus rapide que la sauvegarde complète mais nécessite plus d'espace que l'incrémentielle.

### Règle du 3-2-1 🔒
La règle du 3-2-1 stipule que :
- **3 copies de données** : La donnée originale et deux sauvegardes.
- **2 types de supports différents** : Exemple : disques durs externes, cloud, bandes.
- **1 copie hors site** : Pour se protéger contre les catastrophes locales (incendie, vol, etc.).

### Fréquence des sauvegardes ⏰
La fréquence des sauvegardes dépend de l'importance des données et des exigences de l'entreprise :
- Sauvegardes complètes mensuelles.
- Sauvegardes incrémentielles quotidiennes ou hebdomadaires.

### Péremption des sauvegardes ⏳
Les sauvegardes doivent être conservées pendant une période définie, souvent en fonction de la politique interne :
- **Sauvegardes quotidiennes** : Conservez-les pendant 7 à 30 jours.
- **Sauvegardes mensuelles** : Conservez-les pendant 6 à 12 mois.
- **Sauvegardes annuelles** : Conservez-les pendant plusieurs années selon la législation.

### Supports de sauvegarde 💾
Les supports de sauvegarde peuvent être variés :
- Disques durs externes
- Bandes magnétiques
- Cloud (public ou privé)
- Serveurs de sauvegarde dédiés

## Archivage 📂

### C'est quoi ?
L'archivage est un processus de stockage des données inactives ou obsolètes, mais toujours nécessaires pour une consultation future.

### Utilité ?
L'archivage permet de libérer de l'espace sur les serveurs tout en garantissant que les données peuvent être récupérées en cas de besoin pour des raisons légales, réglementaires ou historiques.

### Exemple ?
- **Archivage des logs systèmes** : Les logs peuvent être archivés après 30 jours pour libérer de l'espace tout en restant accessibles pour des audits.
  
### Durée d'archivage en fonction de la nature des données 🕒
La durée de l'archivage dépend du type de données :
- **Données financières** : 5 à 10 ans.
- **Données personnelles** : En fonction des réglementations, souvent 5 ans maximum.
- **Logs systèmes** : Environ 1 à 3 ans.

## Le clonage 🖥️

### C'est quoi ?
Le clonage consiste à créer une réplique exacte d'un système, d'un disque dur, ou d'un volume.

### Utilité ?
- **Migration** : Déplacer un système d'un disque à un autre.
- **Tests** : Créer des copies pour tester des modifications sans risquer de détruire le système principal.
  
### Exemple ?
Cloner un serveur pour créer un environnement de test ou une réplication d'un serveur de production sur un autre.

## Sécuriser les systèmes 🔐

### Mise à jour
Assurer que tous les systèmes sont à jour est essentiel pour se protéger contre les vulnérabilités :
- **Mises à jour logicielles** : Systèmes d'exploitation, logiciels, firmwares.
- **Mises à jour de sécurité** : Correctifs spécifiques pour des failles découvertes.

### Minimisation physique 🏢
Réduire la surface d'attaque en désactivant les services non nécessaires et en verrouillant l'accès physique :
- **Désactivation des ports inutilisés**.
- **Protection des équipements par mot de passe BIOS/UEFI**.

### Sécurité physique 🚪
Protéger les installations contre les accès non autorisés :
- Contrôle d'accès physique avec des badges ou des clés.
- Caméras de surveillance dans les salles serveur.

## Le logiciel Bareos 🖥️

### Composants de Bareos
Bareos (Backup Archiving Recovery Open Sourced) est un logiciel de sauvegarde open-source composé de plusieurs composants :
- **Directeurs** : Coordonnent les tâches de sauvegarde et de restauration.
- **Clients** : Installés sur les serveurs à sauvegarder.
- **Stockage** : Gère l'endroit où les données sont stockées (disques, bandes).
- **Console** : Interface d'administration en ligne de commande.

### Interface web 🌐
Bareos propose une interface web pour faciliter la gestion des sauvegardes et des restaurations via un navigateur.

### Les jobs Bareos 🎯
Les jobs dans Bareos représentent des tâches spécifiques, telles que des sauvegardes ou des restaurations :
- **Job de sauvegarde** : Sauvegarde des données spécifiées.
- **Job de restauration** : Restauration des données à partir d'une sauvegarde.
- **Job de vérification** : Vérifie l'intégrité des sauvegardes.
  
### Exemple de job Bareos
Un job de sauvegarde pourrait être configuré pour sauvegarder un serveur toutes les nuits à 2h00 et vérifier l'intégrité des sauvegardes chaque dimanche.
