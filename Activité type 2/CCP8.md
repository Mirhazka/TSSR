# Mettre en place, assurer et tester les sauvegardes et les restaurations des éléments de l'infrastructure

## La sauvegarde

### Types de sauvegarde
- **Complète**  
  - Duplique toutes les données  
  - Long et consommateur de stockage  
  - Restauration facile  

- **Incrémentale**  
  - Sauvegarde uniquement les modifications depuis la dernière sauvegarde  
  - Rapide et peu consommateur de stockage  
  - Restauration plus délicate  

- **Différentielle**  
  - Sauvegarde uniquement les modifications depuis la dernière sauvegarde complète  
  - Compromis entre rapidité et stockage  

### Règle du 3-2-1
- 3 copies de données  
- 2 types de support différents  
- 1 copie hors site  

### Fréquence des sauvegardes
- **Régulièrement**  
  - Avoir toujours des données fraîches  
  - Minimiser la quantité de données perdues (compromis entre temps de sauvegarde et panne)  
- **Fréquence = compromis**  
  - Consommation en espace de stockage  
  - Temps nécessaire pour les sauvegardes  
  - Impact sur la production  
- **Exemple classique**  
  - 1 sauvegarde complète par semaine  
  - 1 sauvegarde incrémentale par jour  

### Péremption
- **Durée de conservation d'une sauvegarde**  
  - Minimum jusqu'à la prochaine sauvegarde complète  
- **En général**, conserver les sauvegardes *longtemps* pour pouvoir revenir plus loin dans le temps  
  - Compromission invisible  
  - Données supprimées par erreur  
  - Maladresse  
- **Exemples de péremption**  
  - Hebdomadaire pendant 1 à 2 mois  
  - Mensuelles pendant 1 à 2 ans  

### PRA & PCA
- **PRA** : Plan de Reprise d'Activité (remettre en fonctionnement après une panne)  
- **PCA** : Plan de Continuité d'Activité (maintenir l'activité malgré les pannes)  

### Supports de sauvegarde
- **Disques**  
  - Autre disque du même serveur  
  - Autre serveur  
  - Autre site  
- **Périphériques amovibles**  
  - Bandes magnétiques  
  - Disques durs externes  
  - Disques optiques  

### Divers
- **Planification des sauvegardes** dans les créneaux de faible utilisation (ex : la nuit)  
  - Snapshot  
  - Sauvegardes en ligne  
  - Réseau dédié de sauvegardes  
- **Restauration des sauvegardes**  
  - Complète  
  - Partielle  
- **Clonage**  
  - Installation & Restauration  
  - Image complète d'une machine  
    - Restauration plus rapide de la production  
    - Sauvegardes plus volumineuses et plus longues  
    - Nécessite souvent des outils particuliers  
  - Machine virtuelle  
    - Clonage beaucoup plus simple  

---

## L'archivage

### Considérations
Certaines données doivent être conservées légalement :
- **Durée en fonction de leur nature**  
  - Données comptables : 10 ans  
  - Contrats et factures : 5 ans  
  - Journaux de connexion : 6 mois à 1 an  

### Contraintes particulières
- Supports physiques adaptés à la longue conservation  
- Obsolescence des formats de fichiers  
- Garantie et vérification de l'intégrité  
- Indexation et recherche  

---

## La sécurité des systèmes

### Mise à jour
- **Mise à jour rapide** des logiciels essentielle, mais risque pour la production  
- Gestion des mises à jour avec tests et environnements dédiés : nécessité méthodologique  

### Minimisation physique
Disposer uniquement du nécessaire :
- **Périphériques d'entrée** (USB, lecteur optique, etc.)  
- **Périphériques réseaux** (Ethernet, Wi-Fi, Bluetooth)  
  - Possibilité de désactiver et réactiver le matériel selon besoin  
- **Composants d'administration à distance**  

### Sécurité physique
- Machine d'autorité de certification  
- Restriction d'accès  
- Mot de passe de démarrage (BIOS et/ou BOOT)  
- Démarrage via périphériques amovibles désactivé  
- Chiffrement des disques  

---

## L'outil Bareos

### Composants de Bareos
- **Bareos Director (bareos-dir)** : Chef d'orchestre  
- **Bareos Console** : CLI  
- **Bareos File Daemon (bareos-fd)** : Collecte les informations pour BSD, à installer sur les clients  
- **Bareos Storage Daemon (bareos-sd)** : Effectue les sauvegardes  
- **Catalogue** : L'ensemble des tâches de sauvegarde  

### À savoir
- Bareos peut sauvegarder des clients GNU/Linux et Windows  
- **BAREOS** : Backup Archiving Recovery Open Sourced  
- **bconsole** : Console Bareos  
- **Bareos WebUI** : Composant facultatif  
- **status dir** : Liste les jobs planifiés, en cours et terminés  

### Les jobs
- **FileSet** : Ensemble de chemins de fichiers à sauvegarder  
- **Client** : L'endroit où se trouvent les fichiers  
- **Schedule** : Planification automatisée des jobs  
- **Pool** : Ensemble des supports de stockage utilisés par un Storage Daemon pour un job  

---

## Différences clés

### Sauvegarde
- Copie de données en production utilisées, permettant la restauration en cas de perte ou de corruption.  

### Archivage
- Stockage à long terme de données non utilisées en production, conservées pour des raisons légales ou historiques. Les données sont supprimées de la production.  

### Clonage
- Réplique exacte d'un système ou disque dur, souvent utilisée pour déployer des configurations identiques sur plusieurs machines.
