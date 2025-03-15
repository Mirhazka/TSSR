# Exploiter et maintenir les services de déploiements des postes de travail

## 1. Suivi de parc informatique 🖥️

### Définition
Le **suivi de parc informatique** consiste à assurer la gestion complète des équipements informatiques dans une organisation : ordinateurs, serveurs, appareils mobiles, imprimantes, etc. Cela inclut la planification, l'achat, la maintenance et la mise à jour des équipements.

### Entretien
L'entretien du parc informatique comprend :
- Vérification régulière des performances.
- Nettoyage des composants physiques (nettoyage des ventilateurs, disque dur, etc.).
- Mise à jour du matériel et des logiciels.
- Remplacement des équipements défectueux ou obsolètes.

### Développement et Optimisation
- **Développement** : Amélioration des performances des équipements existants.
- **Optimisation** : Ajustement des configurations système pour maximiser la performance des postes de travail, comme la gestion des ressources (mémoire, processeur).

### Méthodes de gestion
- **Gestion manuelle** : Recensement manuel des équipements et suivi via des outils tels qu'Excel.
- **Gestion automatisée** : Utilisation d'outils spécialisés comme GLPI, Lansweeper ou OCS Inventory.

### Gestion des appareils mobiles 📱
- Gestion des smartphones et tablettes via un **MDM (Mobile Device Management)** pour appliquer des politiques de sécurité et gérer les applications installées.

### Outils de gestion de parc
- **GLPI** : Outil open-source de gestion du parc informatique et des incidents.
- **Lansweeper** : Outil pour l'inventaire automatique du parc informatique.
- **OCS Inventory** : Outil open-source pour l'inventaire et la gestion des équipements.

---
## 2. Déploiement automatisé de Windows 💻

### Outils et Technologies :
- **WDS (Windows Deployment Services)** : Utilisé pour déployer Windows sur des machines via le réseau (PXE).
- **MDT (Microsoft Deployment Toolkit)** : Outil de déploiement automatisé pour les postes Windows, permettant une personnalisation poussée.
- **WADK (Windows Assessment and Deployment Kit)** : Kit d'outils pour automatiser l'installation et la configuration de Windows.
- **SCCM (System Center Configuration Manager)** : Permet de déployer Windows, gérer les mises à jour et les configurations des postes à l'échelle de l'entreprise.

### Master et les 3 images : Thin, Thick, Hybrid
- **Thin Image** : Une image Windows basique sans aucune application ou configuration spécifique.
- **Thick Image** : Une image pré-configurée avec des applications et des configurations définies.
- **Hybrid Image** : Une image qui combine les avantages des deux précédentes, offrant une flexibilité.

### Sysprep et Commande
Le **Sysprep** est utilisé pour préparer un système d'exploitation Windows à être déployé sur différentes machines :
```bash
C:\Windows\System32\sysprep\sysprep.exe /oobe /generalize /shutdown
````

- **/oobe** : Démarre l’interface de bienvenue pour l'utilisateur.
- **/generalize** : Prépare l’image pour un déploiement sur différents matériels.
- **/shutdown** : Éteint la machine après la préparation.

### Préventives lors d'un Sysprep

- Sauvegarder les données avant d’exécuter Sysprep.
- Vérifier que les pilotes génériques sont installés.
- Tester l'image dans un environnement de test avant le déploiement.

### Concepts clés

- **WinPE (Windows Preinstallation Environment)** : Environnement léger pour préparer le système avant l'installation.
- **PXE (Preboot Execution Environment)** : Protocole pour démarrer un ordinateur via le réseau.
- **WIM (Windows Imaging Format)** : Format utilisé pour créer des images Windows.

---
## 3. Gestion des mises à jour 🔄

### Qu'est-ce qu'une mise à jour ?

Une mise à jour consiste à corriger des erreurs, améliorer les fonctionnalités ou ajouter des nouvelles fonctionnalités à un système ou un logiciel.

### Exemples de failles majeures

- **WannaCry** : Exploitant une vulnérabilité dans Windows SMB.
- **Spectre et Meltdown** : Affectant les processeurs Intel et AMD.

### Types de mise à jour

- **Mise à jour de sécurité** : Corrige des failles de sécurité.
- **Mise à jour de fonctionnalité** : Ajoute de nouvelles fonctionnalités ou améliore les anciennes.
- **Mise à jour cumulative** : Contient toutes les mises à jour précédentes et des améliorations.

### Stratégies des mises à jour

- **Déploiement immédiat** : Applique les mises à jour dès leur disponibilité.
- **Déploiement testé** : Teste les mises à jour dans un environnement de pré-production avant de les déployer.

### Solutions dédiées à la gestion des mises à jour

- **WSUS (Windows Server Update Services)** : Permet de gérer les mises à jour de Microsoft dans l'entreprise.
- **SCCM** : Intègre des fonctionnalités avancées de gestion des mises à jour et des déploiements.

---
## 4. WSUS (Windows Server Update Services) 🔧

### Qu'est-ce que WSUS ?

WSUS est un service qui permet aux administrateurs de gérer les mises à jour de Windows sur un réseau. Il offre un contrôle complet sur le déploiement des mises à jour dans l'entreprise.

### Utilité de WSUS

- Permet de télécharger et de distribuer les mises à jour sans saturer la bande passante Internet.
- Permet de tester les mises à jour avant leur déploiement.

### Concepts importants

- **Patch Tuesday** : Le deuxième mardi de chaque mois, Microsoft publie ses mises à jour de sécurité.
- **Avantage de WSUS avec SCCM** : WSUS peut être intégré à SCCM pour une gestion centralisée et plus puissante des mises à jour dans un environnement large.

--- 
## 5. APT (Advanced Package Tool) 🛠️

### Qu'est-ce que APT ?

APT est un système de gestion de paquets utilisé sur les distributions Debian et dérivées (Ubuntu, par exemple). Il permet d'installer, de mettre à jour et de supprimer des paquets logiciels.

### Utilité d'APT

APT est utilisé pour simplifier la gestion des paquets et dépendances dans les systèmes Linux.

### Principaux gestionnaires de paquets

- **apt-get** : Interface en ligne de commande pour gérer les paquets.
- **apt-cache** : Permet de consulter la base de données des paquets.
- **dpkg** : Outil bas niveau pour installer des paquets Debian.

### Architecture et fonctionnement

APT fonctionne en accédant à des **dépôts** qui contiennent des paquets logiciels. Les paquets sont téléchargés et installés automatiquement.

### Commandes de base APT

- **`apt-get update`** : Met à jour la liste des paquets disponibles.
- **`apt-get install <package>`** : Installe un paquet.
- **`apt-get upgrade`** : Met à jour les paquets installés.

### Utilité d'un dépôt local de paquets

Un dépôt local permet de stocker et de gérer des paquets internes, ce qui est utile pour des mises à jour dans des environnements hors ligne ou pour contrôler les versions des logiciels déployés.
