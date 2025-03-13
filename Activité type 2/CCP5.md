# Maintenir des serveurs dans une infrastructure virtualisée
## Glossaire
- L'émulation
	- C'est le processus de création d'un système qui reproduit la manière dont fonctionne un système (émulateur d'une console de jeu)
- La simulation
	- C'est une représentation numérique d'un système réel ou fictif basée sur un modèle abstrait (simple ou complexe). Une simulation météorologiques, de vol, boursières...
- La virtualisation
	- C'est le processus de création d'une version virtuelle des ressources informatiques, qu'elles soient matérielles ou logicielles
	- Reprise du concept de l'émulation MAIS avec une utilisation de l'architecture du système hôte
- Relation avec l'outil GNS3
	- Simulation du comportement d’interfaces réseaux connectées
	- Emulation de routeurs, switch, ordinateurs
	- Virtualisation de routeurs, switch, ordinateurs (en incorporant des VM et des conteneurs)
- Format de partitionnement
	- MBR (Master Boot Record) = Partitionnement intel historique
	- GPT (GUID Partition Table) = Nouveau format de partitionnement

## Les hyperviseurs
### Les hyperviseurs de type 1
- La virtualisation *bare-metal* s'exécute directement sur le matériel, offrant de meilleures performances et un noyau léger, mais avec un seul hyperviseur possible et des coûts matériels et logiciels plus élevés.
- Les hyperviseurs de type 1, utilisés dans les centres de données et pour des applications nécessitant une grande puissance de calcul, offrent des performances supérieures en interagissant directement avec le matériel, comme ceux utilisés par AWS, Azure et GCP.
- Exemple :
	- Proxmox
	- VMware ESXi

### Les hyperviseurs de type 2
- L'hyperviseur de type 2 s'exécute à l'intérieur d'un autre OS, offrant une utilisation facile et la possibilité d'exécuter plusieurs hyperviseurs, mais avec moins de ressources matérielles que les hyperviseurs de type 1.
- Exemple :
	- VirtualBox
	- VMware Workstation

## La conteneurisation
- La conteneurisation exécute des applications isolées sur un même OS, offrant de bonnes performances et une faible consommation de ressources, mais avec une isolation moins forte qu'en virtualisation.
- Les conteneurs sont idéaux pour le déploiement d'applications, l'architecture de microservices et les pipelines CI/CD, garantissant une exécution cohérente et efficace des services.
- Exemple :
	- Docker
	- Kubernetes

## La haute disponibilité
- Cela désigne la capacité d'un système ou d'une infrastructure à fonctionner de manière continue et sans interruption, même en cas de défaillance d'un de ses composants. Cela est généralement assuré par la mise en place de redondances, de basculements automatiques et de mécanismes de récupération rapides pour minimiser les temps d'arrêt et garantir un service quasi permanent.
- Les éléments indispensables sont :
	- La redondance matérielle (serveur, stockage)
	- Un système de répartition de charge (Load Balancing)
	- Un système de basculement automatique en cas d’erreur ou de panne (Failover)
	- Une copie (réplication) des données en temps réel
	- Un système de supervision
	- Un PRA et PCA

## Le cloud computing
Le **Cloud Computing** désigne l'utilisation de ressources informatiques (serveurs, stockage, réseaux, etc.) via internet, offrant des services variés selon les besoins des utilisateurs.
- **IaaS (Infrastructure as a Service)** : Fourniture de ressources matérielles virtuelles (serveurs, stockage, réseaux) via le cloud, permettant à l'utilisateur de gérer les systèmes d'exploitation et les applications.
- **PaaS (Platform as a Service)** : Offre une plateforme complète permettant de développer, déployer et gérer des applications sans gérer l'infrastructure sous-jacente.
- **SaaS (Software as a Service)** : Applications hébergées dans le cloud et accessibles via un navigateur, sans nécessiter d'installation ou de gestion par l'utilisateur (par exemple, Google Workspace, Microsoft 365).
- **Cloud public** : Services cloud fournis par un fournisseur tiers accessibles à tous, avec des ressources partagées entre plusieurs clients.
- **Cloud privé** : Cloud réservé à une organisation spécifique, offrant un contrôle total sur l'infrastructure et une meilleure sécurité.
- **Cloud hybride** : Combinaison de clouds publics et privés, permettant à une organisation de déplacer des données et des applications entre eux selon les besoins.
- **Hébergement Web mutualisé** : Plusieurs utilisateurs partagent les ressources d'un même serveur pour héberger leurs sites, généralement moins coûteux mais avec des performances limitées.
- **Serveurs privés virtuels (VPS)** : Des serveurs virtuels isolés dans un environnement partagé, offrant plus de ressources et de contrôle qu'un hébergement mutualisé.
- **Serveurs dédiés (bare metal)** : Serveurs physiques réservés à un seul utilisateur, offrant des ressources dédiées et un contrôle total sur la configuration matérielle.
- **Conteneurisation** : Technologie permettant d'exécuter des applications dans des conteneurs légers et isolés, garantissant portabilité et efficacité, souvent utilisée avec Docker ou Kubernetes.
- **Interface d'accès Shell** : Accès en ligne de commande via un terminal pour gérer et administrer des systèmes ou des applications dans le cloud.
- **Interface d'accès Web** : Accès aux ressources cloud via un navigateur web, offrant une interface graphique pour gérer les services et applications.
- **Interface d'accès API** : Interface de programmation permettant aux applications de communiquer avec les services cloud via des appels API, offrant une automatisation et une intégration plus poussée.

## Avantages de la virtualisation
- Etat des lieux sur l'utilisation des serveurs
	- Optimise l'utilisation des ressources matérielles en permettant d'exécuter plusieurs systèmes et applications sur un même serveur, contrairement à l'ancienne pratique d'un serveur physique par service pour la sécurité.
- Installation et déploiement facilité
	- Facilite l'installation, le déploiement et la migration des systèmes grâce aux *templates*, permettant de créer et reproduire des environnements rapidement.
- Economie de matériel
	- Permet d'héberger plusieurs serveurs sur une même machine physique, réduisant ainsi les coûts tout en optimisant les ressources.
- Isolation
	- Isole chaque système ou application dans une machine virtuelle, les protégeant des pannes et des failles des autres VM.

## Inconvénients de la virtualisation
- Points de défaillance unique
	- Une panne du serveur physique impacte toutes les VM hébergées, d'où l'importance de la redondance avec des serveurs de secours prêts à prendre le relais.
- Besoin de machine puissantes
	- Nécessite des serveurs puissants pour gérer l'overhead, c'est-à-dire les ressources supplémentaires utilisées par l'hyperviseur en plus des VM.
- Dégradation des performances
	- Peut réduire les performances par rapport à un OS natif, mais avec le matériel et les logiciels modernes, cet impact reste généralement faible.
- Complexité d'analyse d'erreurs
	- Le dépannage en virtualisation est plus complexe, car les erreurs peuvent venir du guest OS, du host OS, de l'hyperviseur ou du matériel, nécessitant des compétences variées.
- Inadaptation possible (I/O spécifique)
	- La virtualisation n'est pas toujours idéale, surtout pour les applications nécessitant de hautes performances ou un accès direct aux I/O matérielles, ce qui nécessite une analyse préalable des besoins.
