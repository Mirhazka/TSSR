# Maintenir des serveurs dans une infrastructure virtualisée

## 1. Architecture des ordinateurs 🖥️
### C'est quoi ?
L'architecture d'un ordinateur désigne l'organisation des composants matériels et leur interaction. Elle détermine la manière dont le processeur, la mémoire, les périphériques et les autres éléments sont agencés et interagissent.

### Utilité
L'architecture permet de déterminer les capacités de performance, de gestion de la mémoire, et de connectivité du système. Elle influence directement la stabilité et l'efficacité des serveurs.

### Exemples
- **Architecture x86** : Utilisée dans la majorité des PC et serveurs.
- **ARM** : Architecture plus courante dans les appareils mobiles et les serveurs dédiés à l'efficacité énergétique.
- **RISC (Reduced Instruction Set Computing)** : Utilisée dans des systèmes nécessitant des calculs rapides.

---

## 2. Virtualisation 🌀
### Hyperviseur Type 1 (Bare-metal) 🖥️
Un **hyperviseur Type 1** fonctionne directement sur le matériel physique sans système d'exploitation hôte. Il est plus performant et plus sécurisé que le Type 2.

**Exemples** : VMware ESXi, Microsoft Hyper-V, Xen

### Hyperviseur Type 2 (Hosted) 🖱️
Un **hyperviseur Type 2** fonctionne sur un système d'exploitation hôte. Il est plus simple à mettre en place mais moins performant.

**Exemples** : VMware Workstation, VirtualBox

### Cluster d'hyperviseur 🌐
Un **cluster d'hyperviseurs** est un groupe de serveurs physiques hébergeant des hyperviseurs, permettant la gestion centralisée de la virtualisation et d'assurer la haute disponibilité des machines virtuelles.

### Avantages
- **Optimisation des ressources** : Maximisation de l'utilisation des serveurs physiques.
- **Gestion simplifiée** : Création et gestion rapide des VM.
- **Isolation** : Chaque machine virtuelle fonctionne indépendamment.

### Inconvénients
- **Consommation des ressources** : Les hyperviseurs ajoutent une couche qui peut entraîner une surconsommation de ressources.
- **Complexité** : La gestion des hyperviseurs et des VM peut devenir complexe dans un grand environnement.

---

## 3. Conteneurisation 🐳
### C'est quoi ?
La **conteneurisation** est une méthode qui permet de déployer des applications dans des environnements isolés appelés conteneurs, permettant une portabilité entre les environnements.

### Utilité
Elle permet de garantir la cohérence entre les environnements de développement, de test et de production. Elle est idéale pour les applications légères et évolutives.

### Exemple : Docker
**Docker** est un outil populaire de conteneurisation qui permet de créer, déployer et exécuter des applications dans des conteneurs. Chaque conteneur peut contenir tout le nécessaire pour faire tourner une application (dépendances, configurations, etc.).

### Avantages
- **Portabilité** : Un conteneur peut être exécuté sur n'importe quel système supportant Docker.
- **Isolation** : Les applications fonctionnent indépendamment les unes des autres.
- **Consommation faible** : Moins lourd qu'une machine virtuelle.

### Inconvénients
- **Sécurité** : Moins isolé que les hyperviseurs.
- **Complexité de gestion** : L'orchestration de conteneurs (avec Kubernetes, par exemple) peut être complexe.

### Différence entre conteneurisation et hyperviseur 🤔
Bien que les conteneurs et les hyperviseurs permettent tous deux d'exécuter des applications de manière isolée, il existe des différences fondamentales entre les deux approches :

- **Isolation** :
  - **Hyperviseur** : Chaque machine virtuelle (VM) contient son propre système d'exploitation complet, ce qui les rend plus isolées les unes des autres. Chaque VM emploie une partie du système hôte et du matériel physique.
  - **Conteneurisation** : Les conteneurs partagent le noyau du système hôte. Ils sont donc plus légers que les VMs, mais moins isolés.

- **Performance** :
  - **Hyperviseur** : Les VMs étant plus isolées et indépendantes, elles consomment plus de ressources, car chaque machine virtuelle a son propre système d'exploitation et ses propres applications.
  - **Conteneurisation** : Les conteneurs étant plus légers (ils n'ont pas de système d'exploitation complet), ils utilisent moins de ressources et démarrent plus rapidement.

- **Gestion des ressources** :
  - **Hyperviseur** : Les VMs disposent de ressources dédiées (mémoire, processeur, etc.), ce qui peut offrir des performances plus prévisibles.
  - **Conteneurisation** : Les conteneurs utilisent les ressources de manière plus flexible et partagée, ce qui peut être plus efficace mais moins prévisible en termes de performance sous charge.

- **Portabilité** :
  - **Hyperviseur** : Une VM peut être transférée entre différents hôtes mais nécessite souvent des ajustements si le matériel ou le système d'exploitation change.
  - **Conteneurisation** : Les conteneurs sont plus portables, car ils incluent tout le nécessaire pour l'exécution d'une application, ce qui permet de les faire fonctionner facilement sur n'importe quelle machine ou cloud qui supporte Docker, sans modification.

---

## 4. Haute disponibilité 🔧
### C'est quoi ?
La **haute disponibilité (HA)** fait référence à un système conçu pour garantir une disponibilité continue, même en cas de défaillance d'un composant du système.

### Utilité
Elle permet d'assurer une continuité de service pour des applications critiques en minimisant les temps d'arrêt.

### Exemples
- **Cluster de serveurs** : Plusieurs serveurs configurés pour se prendre en charge en cas de panne de l'un d'eux.
- **RAID (Redundant Array of Independent Disks)** : Une solution pour assurer la redondance des données au niveau du stockage.

### Exemples supplémentaires
- **Load balancing (Répartition de charge)** : Utilisation de serveurs supplémentaires pour répartir le trafic entre plusieurs instances. Exemple : **HAProxy**, **NGINX**.
- **Replication (Réplique de base de données)** : Mise en place de serveurs de bases de données redondants pour garantir la continuité des services. Exemple : **MySQL Cluster**, **PostgreSQL avec streaming replication**.
- **Disaster recovery (Plan de reprise après sinistre)** : Mise en place d'une infrastructure secondaire qui prend le relais en cas de défaillance majeure du système principal. Exemple : **Backup répliqué sur un autre site**, **Virtual Machine replication**.
- **UPS (Uninterruptible Power Supply)** : Des alimentations sans coupure sont installées pour assurer la continuité de l'alimentation électrique, même en cas de panne de courant.

---

## 5. Cloud computing ☁️
### IaaS (Infrastructure as a Service) 🌐
**IaaS** fournit une infrastructure complète sur laquelle vous pouvez exécuter des applications. Vous louez des serveurs, des espaces de stockage et des réseaux sans avoir à gérer les équipements.

**Exemples** : AWS EC2, Google Compute Engine

### PaaS (Platform as a Service) 🎛️
**PaaS** offre une plateforme complète pour le développement, le test et le déploiement d'applications. L'infrastructure sous-jacente est gérée par le fournisseur.

**Exemples** : Heroku, Google App Engine

### SaaS (Software as a Service) 💻
**SaaS** propose des applications en ligne que les utilisateurs peuvent utiliser sans avoir à se soucier de la gestion de l'infrastructure ou de la plateforme.

**Exemples** : Google Workspace, Office 365

### Différents types de cloud ☁️
- **Cloud public** : Les ressources sont gérées par un fournisseur externe (ex. : AWS, Microsoft Azure).
- **Cloud privé** : L'infrastructure est utilisée exclusivement par une organisation.
- **Cloud hybride** : Combinaison de clouds publics et privés, permettant une flexibilité maximale.

### Différents types d'hébergement 🌍
- **Hébergement mutualisé** : Plusieurs sites partagent le même serveur.
- **Hébergement dédié** : Un serveur entier est dédié à un seul client.
- **Hébergement cloud** : Utilisation de plusieurs serveurs pour l’hébergement d’applications ou de données.

### Différents types d'interface d'accès 🔑
- **Interface Web** : Accès via un navigateur web.
- **API (Application Programming Interface)** : Permet l’intégration avec des applications tierces.
- **Console CLI** : Accès via une ligne de commande pour une gestion plus avancée.
