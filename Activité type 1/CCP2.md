# Exploiter des serveurs Windows et un domaine Active Directory

## 📦 La gestion du stockage sous Windows

### **Disques de base et disques dynamiques :**
- **Disques de base** : Ce sont des disques standard utilisés par Windows pour gérer les partitions (primaires, étendues, ou logiques). C'est le type de disque utilisé par défaut sur la plupart des systèmes.
- **Disques dynamiques** : Un disque dynamique permet une gestion plus flexible du stockage. Il permet de créer des volumes (partitions) au-delà des limites d'un seul disque de base, avec des options comme la redondance ou la parité (RAID).

### **Volumes Dynamiques et RAID sous Windows**

#### **Qu'est-ce qu'un volume dynamique ?**
- Un **volume dynamique** permet de créer des configurations de stockage plus complexes que les volumes simples des disques de base. Les volumes dynamiques permettent une plus grande flexibilité en matière de gestion des disques et de la redondance des données. Les disques dynamiques sont gérés par un **gestionnaire de disques dynamique** intégré dans Windows.

#### **Types de volumes dynamiques :**
1. **Volume Simple :**
   - Un **volume simple** est un seul volume de disque dur, utilisant une seule partition.
   - Il fonctionne de manière similaire à une partition sur un disque de base.
   - Par exemple, un disque de 500 Go formaté en NTFS représente un volume simple.

2. **Volume Étendu :**
   - Un **volume étendu** peut s'étendre sur plusieurs disques physiques, permettant de combiner l'espace de plusieurs disques en un seul volume.
   - Cela permet d'augmenter la capacité du volume, mais sans redondance. Si un disque échoue, toutes les données sont perdues.

3. **Volume Mirroir (RAID 1) :**
   - Un **volume miroir** crée une copie exacte des données sur deux disques (RAID 1).
   - Ce type de volume est utilisé pour assurer la redondance des données. Si un disque échoue, les données sont toujours disponibles sur l'autre disque.
   - Les performances de lecture peuvent être améliorées, mais les écritures sont parfois un peu plus lentes, car les données doivent être écrites sur les deux disques.

4. **Volume Strié (RAID 0) :**
   - Un **volume strié** (RAID 0) divise les données en blocs qui sont écrits simultanément sur plusieurs disques. Cela améliore les performances de lecture et d’écriture.
   - Cependant, ce type de volume n'offre **pas de redondance**. Si un disque échoue, toutes les données sont perdues.

5. **Volume Parité (RAID 5) :**
   - Un **volume parité** (RAID 5) offre un compromis entre la performance, la capacité et la redondance.
   - Les données sont réparties sur plusieurs disques, et un disque supplémentaire contient des informations de parité. En cas de défaillance d'un disque, les données peuvent être reconstruites à partir des informations de parité.
   - Le RAID 5 nécessite au moins **trois disques** et permet de conserver une bonne capacité de stockage tout en offrant une protection contre la perte de données.

6. **Volume RAID 10 (RAID 1+0) :**
   - Un **volume RAID 10** combine les avantages des volumes RAID 1 et RAID 0.
   - Il offre à la fois **redondance et performance**. Les données sont d'abord miroirées (RAID 1), puis les disques sont groupés en une configuration striée (RAID 0).
   - Ce type de volume nécessite **au moins quatre disques** et offre une bonne protection contre les pannes de disques tout en maintenant de bonnes performances.

#### **Comment gérer les volumes dynamiques sous Windows ?**
- **Création d’un volume dynamique** :
  1. Ouvrir le **Gestionnaire de disques** (`diskmgmt.msc`).
  2. Clic droit sur un disque non initialisé et sélectionner **Convertir en disque dynamique**.
  3. Une fois le disque converti, vous pouvez créer un volume dynamique (simple, miroir, étendu, etc.) en choisissant le type de volume.

- **Redimensionner un volume dynamique** :
  - Vous pouvez agrandir ou réduire un volume dynamique directement depuis le gestionnaire de disques, à condition que l’espace disque soit disponible.
  - Les volumes étendus peuvent être redimensionnés en ajoutant ou retirant de l’espace depuis d'autres disques dynamiques.

- **Suppression et conversion d'un volume dynamique** :
  - Pour supprimer un volume dynamique, vous devez d'abord **démonter les volumes** ou les **supprimer**. Une fois les volumes supprimés, le disque peut être reconverti en disque de base.

#### **RAID sous Windows** :
Sous Windows, vous pouvez configurer des volumes RAID via le gestionnaire de disques dynamique pour implémenter des niveaux RAID comme le RAID 0, RAID 1, RAID 5 et RAID 10. Toutefois, pour des performances optimales et un contrôle avancé du RAID, les **cartes RAID matérielles** ou des solutions tierces peuvent offrir de meilleures performances et une gestion plus simple.

#### **Réduire un volume dynamique ou migrer un RAID** :
- Lors de la gestion des volumes RAID sous Windows, il est essentiel de comprendre que la **migration d'un RAID** ou la **réduction d’un volume dynamique** nécessite de libérer de l’espace, parfois en supprimant des volumes existants, ce qui peut entraîner une perte de données si les sauvegardes ne sont pas correctement effectuées.

#### **Avantages et inconvénients des volumes dynamiques et RAID sous Windows** :
- **Avantages** :
  - **RAID 1 (Mirroir)** : Haute redondance, protection des données.
  - **RAID 0 (Strié)** : Haute performance.
  - **RAID 5 (Parité)** : Bon compromis entre performance et sécurité.
  
- **Inconvénients** :
  - Les volumes dynamiques peuvent être plus complexes à gérer que les disques de base.
  - Le RAID logiciel sous Windows n'offre pas les mêmes performances et fonctionnalités avancées que le RAID matériel.
  - La gestion des volumes RAID peut entraîner une perte de données si mal configurée ou si les disques ne sont pas correctement synchronisés.

---

## 👥 La gestion des utilisateurs sous Windows

- **Création et gestion des comptes utilisateurs** :
  - Utilisation de `Active Directory Users and Computers (ADUC)` pour créer, modifier, désactiver ou supprimer des comptes utilisateurs.
  - Gestion des propriétés des utilisateurs (groupes, mots de passe, informations personnelles).

- **Groupes locaux et globaux** :
  - Différence entre groupes locaux, globaux et universels.
  - Affectation des utilisateurs aux groupes appropriés.

## 🏢 L'Active Directory (AD-DS, OU, Groupe, User, Domaine, Arbre, Forêt)

- **Active Directory Domain Services (AD-DS)** :
  - Fonctionnement de l'AD-DS pour la gestion centralisée des utilisateurs, groupes, et ressources.
  - Utilisation de `dcpromo` pour promouvoir un serveur en contrôleur de domaine.

- **Unités d'Organisation (OU)** :
  - Structure des OUs pour organiser les objets dans AD (utilisateurs, groupes, ordinateurs).
  - Application des GPOs au niveau des OUs.

- **Domaines, Arbres, et Forêts** :
  - Définition d’un domaine Active Directory, d’un arbre et d’une forêt.
  - Relation entre les domaines : domaine parent, domaine enfant.
  - Confiance entre les domaines et forêts.

## 🌐 DHCP & DNS

- **DHCP (Dynamic Host Configuration Protocol)** :
  - Configuration de l'IP dynamique via le rôle DHCP.
  - Plage d'adresses, réservations d'adresses, étendues DHCP.
  - Relais DHCP et options DHCP.

- **DNS (Domain Name System)** :
  - Rôle de DNS dans AD : résolutions de noms pour les domaines.
  - Configuration de zones DNS : zone primaire, secondaire et inverse.
  - Enregistrement des ressources DNS (A, CNAME, PTR).

## ⚙️ Les GPO (Group Policy Objects)

- **Création et gestion des GPOs** :
  - Utilisation de `Group Policy Management Console (GPMC)` pour créer et appliquer des GPOs.
  - Différents types de GPOs : Local, Domaine, OU.
  - Application des GPOs : héritage, bloquer l'héritage, forcer l'application.

- **Paramètres des GPOs** :
  - Configuration de la sécurité des utilisateurs et des ordinateurs.
  - Réglages des scripts, des redirections de dossiers, des restrictions d'application.

## 🔒 SSH sous Windows

- **Configuration du serveur SSH sous Windows** :
  - Installation de la fonctionnalité `OpenSSH Server` via PowerShell ou les fonctionnalités facultatives de Windows.
  - Configuration des clés SSH et autorisation des connexions.

- **Utilisation de SSH pour l’administration à distance** :
  - Connexion via `ssh username@hostname`.
  - Transfert de fichiers avec `scp` ou `sftp`.

## 🖥️ WSUS (Windows Server Update Services)

- **Rôle WSUS** :
  - Utilisation de WSUS pour gérer les mises à jour sur les machines Windows dans un environnement d'entreprise.
  - Configuration de WSUS : approbation des mises à jour, programmation des installations.

- **Gestion des clients WSUS** :
  - Configuration des clients WSUS via les GPOs pour définir le serveur WSUS.
  - Surveillance et rapport sur l'état des mises à jour.

## 📀 WDS (Windows Deployment Services)

- **Installation et configuration de WDS** :
  - Rôle WDS pour déployer des images Windows sur les ordinateurs clients.
  - Configuration des serveurs WDS et des partages de distribution.

- **Création d’images de déploiement** :
  - Capture d’images de systèmes existants avec l’outil `ImageX`.
  - Déploiement de systèmes via PXE.

---

> **Référence** :
> Ce fichier est destiné à une révision détaillée sur les tâches liées à l'exploitation de serveurs Windows et d'un domaine Active Directory pour un technicien supérieur Système & Réseaux.
