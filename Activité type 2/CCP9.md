# Exploiter et maintenir les services de déploiement des postes de travail

## Suivi de parc

---

## Déploiement automatisé de Windows

### Les outils de déploiement

- **WDS (Windows Deployment Service)**  
  Permet d'installer un système d'exploitation Windows via le réseau.
  - Déploiement d'images **WIM** (Windows Imaging Format)
  - **PXE (Preboot Execution Environment)** :  
    Permet de démarrer un poste sans système d'exploitation local via le réseau.
  - Fourniture d'images de démarrage par **TFTP** (Trivial File Transfer Protocol) :  
    Protocole léger permettant le transfert d'images au démarrage via le réseau.
  - Utilisation de fichiers de réponse **XML** pour automatiser le déploiement.
  - **Rôle serveur à ajouter sur Windows Server** :  
    Il est nécessaire d’ajouter le rôle WDS sur un serveur Windows. **ADDS (Active Directory Domain Services)** n'est pas obligatoire, mais **DHCP (Dynamic Host Configuration Protocol)** est requis pour fournir les adresses IP.

- **MDT (Microsoft Deployment Toolkit)**  
  Outil permettant de simplifier et d'automatiser le déploiement de Windows. Il peut être utilisé pour créer des images et déployer des systèmes d'exploitation de manière centralisée.  
  **Utilité** : MDT permet d'automatiser des tâches comme l'installation des systèmes d'exploitation, des applications, et la configuration des paramètres système via des scripts et des modèles.

- **WADK (Windows Assessment and Deployment Kit)**  
  **C'est quoi ?** Un kit de déploiement de Windows qui contient les outils nécessaires pour créer des images de déploiement et personnaliser l'installation des systèmes d'exploitation.  
  **Utilité** : WADK est utilisé pour créer des images personnalisées et faciliter l'évaluation des performances des systèmes.

- **SCCM (System Center Configuration Manager)**  
  **C'est quoi ?** Un outil de gestion d'infrastructure permettant de déployer des systèmes d'exploitation et de gérer les configurations des machines.  
  **Utilité** : SCCM permet une gestion centralisée des installations, mises à jour et configurations des postes de travail à grande échelle, tout en offrant des fonctionnalités de gestion des applications et des correctifs.

### Le déploiement Windows

- **Le master** est une image disque de référence, utilisée pour créer des installations standardisées.
  - **Thin image** : Ne contient que l'OS, sans logiciels supplémentaires.
  - **Thick image** : Contient l'OS et l'ensemble des logiciels nécessaires à l'utilisateur final.
  - **Hybrid image** : Contient l'OS avec les logiciels de base (antivirus, navigateur, bureautique, etc.).

- **Sysprep** (System Preparation Tool) :  
  Permet de préparer une image Windows pour un déploiement sur différents matériels.
  - **Synonyme** : "Reseal" (mise en scellé) d'une image Windows.
  - Ligne de commande à exécuter :  
    ```shell
    C:\Windows\System32\sysprep\sysprep.exe /oobe /generalize /shutdown
    ```
    - `oobe` : **Out Of Box Experience**. Lance la séquence de personnalisation lors du premier démarrage.
    - `generalize` : Permet de rendre l'image générique, compatible avec différents matériels.
    - `shutdown` : Éteint l'ordinateur après avoir exécuté Sysprep.
  
  **Attention** : Après un sysprep, il ne faut pas allumer le PC immédiatement. Cela permet d'éviter des problèmes liés à la réinitialisation des SID (Security Identifiers) et à la réactivation de Windows.

### Autres concepts clés

- **WinPE (Windows Preinstallation Environment)**  
  Un environnement de préinstallation minimal permettant de déployer des systèmes d'exploitation, de réparer des installations, ou de récupérer des données.  
  **Utilité** : WinPE est utilisé comme environnement de démarrage pour lancer des tâches de déploiement ou de réparation.

- **PXE (Preboot Execution Environment)**  
  Un protocole qui permet de démarrer un poste de travail via le réseau, sans système d'exploitation installé localement.  
  **Utilité** : PXE est essentiel pour les déploiements sans intervention physique sur le matériel.

- **WIM (Windows Imaging Format)**  
  Format de fichier utilisé pour capturer des images de systèmes d'exploitation Windows.  
  **Utilité** : Les fichiers WIM sont utilisés pour stocker des images Windows et peuvent être déployés via WDS ou d'autres outils de déploiement comme MDT ou SCCM.

---

## Gestion des mises à jour

---

## WSUS

---

## APT
