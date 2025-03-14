# Maintenir des serveurs dans une infrastructure virtualisée

## Glossaire

- **L'émulation**
  - C'est le processus de création d'un système qui reproduit la manière dont fonctionne un système (exemple : émulateur d'une console de jeu).
- **La simulation**
  - C'est une représentation numérique d'un système réel ou fictif basée sur un modèle abstrait (simple ou complexe). Exemples : simulation météorologique, de vol, boursière...
- **La virtualisation**
  - C'est le processus de création d'une version virtuelle des ressources informatiques, qu'elles soient matérielles ou logicielles.
  - Elle reprend le concept de l'émulation MAIS en utilisant l'architecture du système hôte.
- **Relation avec l'outil GNS3**
  - Simulation du comportement d’interfaces réseaux connectées.
  - Émulation de routeurs, switchs, ordinateurs.
  - Virtualisation de routeurs, switchs, ordinateurs (en incorporant des VM et des conteneurs).
- **Format de partitionnement**
  - **MBR (Master Boot Record)** : Partitionnement Intel historique.
  - **GPT (GUID Partition Table)** : Nouveau format de partitionnement.

---

## Les hyperviseurs

### Les hyperviseurs de type 1
- La virtualisation *bare-metal* s'exécute directement sur le matériel, offrant de meilleures performances et un noyau léger. Cependant, elle impose un seul hyperviseur possible et engendre des coûts matériels et logiciels plus élevés.
- Les hyperviseurs de type 1, utilisés dans les centres de données et les applications à forte puissance de calcul, offrent des performances supérieures en interagissant directement avec le matériel (exemple : AWS, Azure, GCP).
- **Exemples** :
  - Proxmox
  - VMware ESXi

### Les hyperviseurs de type 2
- L'hyperviseur de type 2 s'exécute à l'intérieur d'un autre OS, offrant une utilisation plus simple et la possibilité d'exécuter plusieurs hyperviseurs, mais avec moins de ressources matérielles que les hyperviseurs de type 1.
- **Exemples** :
  - VirtualBox
  - VMware Workstation

---

## La conteneurisation
- La conteneurisation exécute des applications isolées sur un même OS, offrant de bonnes performances et une faible consommation de ressources, mais avec une isolation moins forte qu'en virtualisation.
- Les conteneurs sont idéaux pour le déploiement d'applications, l'architecture de microservices et les pipelines CI/CD, garantissant une exécution cohérente et efficace des services.
- **Exemples** :
  - Docker
  - Kubernetes

---

## La haute disponibilité
- Désigne la capacité d'un système à fonctionner en continu sans interruption, même en cas de défaillance d'un composant.
- Assurée par des mécanismes comme la redondance, le basculement automatique et la récupération rapide.
- **Éléments indispensables** :
  - Redondance matérielle (serveurs, stockage).
  - Système de répartition de charge (*Load Balancing*).
  - Basculement automatique (*Failover*).
  - Réplication des données en temps réel.
  - Supervision du système.
  - Plan de reprise d'activité (*PRA*) et plan de continuité (*PCA*).

---

## Le cloud computing
- Utilisation de ressources informatiques via Internet, offrant divers services.
- **Modèles de service** :
  - **IaaS** (*Infrastructure as a Service*) : Fourniture de ressources virtuelles (serveurs, stockage, réseaux).
  - **PaaS** (*Platform as a Service*) : Plateforme pour développer, déployer et gérer des applications.
  - **SaaS** (*Software as a Service*) : Applications accessibles via un navigateur (*Google Workspace, Microsoft 365*).
- **Types de cloud** :
  - **Public** : Accès partagé entre plusieurs clients.
  - **Privé** : Infrastructure dédiée à une organisation.
  - **Hybride** : Combinaison de cloud public et privé.
- **Types d'hébergement** :
  - **Mutualisé** : Ressources partagées entre plusieurs utilisateurs.
  - **VPS** : Serveurs virtuels isolés dans un environnement partagé.
  - **Dédié** : Serveur physique réservé à un seul utilisateur.
  - **Conteneurisation** : Applications exécutées dans des conteneurs légers.
- **Interfaces d'accès** :
  - Shell (CLI)
  - Web (interface graphique)
  - API (programmation)

---

## Avantages de la virtualisation
- **Optimisation des ressources** : Exécution de plusieurs systèmes sur un même serveur.
- **Installation et déploiement facilites** : Templates permettant une création rapide d'environnements.
- **Économie de matériel** : Plusieurs serveurs hébergés sur une même machine physique.
- **Isolation** : Protection des VM contre les pannes des autres machines.

---

## Inconvénients de la virtualisation
- **Points de défaillance unique** : Une panne impacte toutes les VM.
- **Besoins en matériel puissant** : Gestion de l'overhead (*ressources supplémentaires*).
- **Dégradation des performances** : Inférieures à un OS natif.
- **Complexité du diagnostic** : Erreurs possibles à plusieurs niveaux (*guest OS, host OS, hyperviseur, matériel*).
- **Inadaptation possible** : Certaines applications exigeant un accès direct aux I/O matérielles peuvent être affectées.
