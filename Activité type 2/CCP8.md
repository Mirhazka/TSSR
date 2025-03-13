# Mettre en place, assurer et tester les sauvegardes et les restaurations des éléments de l'infrastructure
## La sauvegarde
### Les types de sauvegarde
- Complète
	- Dupliquer toutes les données
	- Long et consommateur de stockage
	- Restauration facile
- Incrémentale
	- Uniquement les modifications depuis la sauvegarde précédente
	- Rapide et peu consommateur de stockage
	- Restauration plus délicate
- Différentielle
	- Uniquement les modifications depuis dernière sauvegarde complète
	- Compromis

### Règle du 3-2-1 
- 3 copies
- 2 types de support différents
- 1 copie hors site

### Fréquence des sauvegardes
- Régulièrement
	- Avoir toujours des données fraîches
	- Minimiser la quantité de données perdues (temps de sauvegarde <-> panne
- Fréquence = Compromis
	- Consommation en espace de stockage
	- Temps nécessaire à faire les sauvegardes
	- Impact sur la production
- Classique :
	- 1 complète par semaine
	- 1 incrémentale par jour

### Péremption
- Durée de conservation d'une sauvegarde
	- Minimum : jusqu'à la prochaine complète
- En générale, *longtemps* pour pouvoir revenir plus loin dans le temps
	- Compromission invisible
	- Données supprimées par erreur
	- Maladresse
- Exemple
	- Hebdomadaire pendant 1 à 2 mois
	- Mensuelles pendant 1 à 2 ans

### PRA & PCA
- PRA = Plan de Reprise d'Activité, remettre en fonctionnement après une panne
- PCA = Plan de Continuité d'Activité, maintenir l'activité malgré les pannes

### Les supports 
- Sur disques
	- Autre disque du même serveur
	- Autre serveur
	- Autre site
- Sur périphériques amovibles
	- Bandes magnétiques
	- Disques durs externes
	- Disques optiques

### Divers
- Planification des sauvegardes dans les creux d'utilisation (*exemple la nuit*)
	- Snapshot
	- Sauvegardes en lignes
	- Réseau dédié de sauvegardes
- Restauration des sauvegardes 
	- Complètes 
	- Partielle
- Clonage
	- Installation & Restauration
	- Image complète d'une machine
		- Redémmarage de la prod plus rapide
		- Taille et temps des sauvegardes plus long
		- Nécessite souvent des outils particuliers
	- Machine virtuelle
		- Clonage beaucoup plus simple

## L'archivage
### Considérations 
Certaines données doivent légalement être conservées
- Durée en fonction de leur nature
	- Donnée comptables : 10 ans
	- Contrats et factures : 5 ans
	- Journaux de connexion : 6 mois à 1 an

### Contraintes particulières
- Support physique adaptés à la longue conservation
- Obsolescence des formats de fichiers
- Garantie et vérification de l'intégrité
- Indexation et recherche

## La sécurité des systèmes
### Mise à jours
**La mise à jour de tous les logiciels au plus vite est essentiel mais** : 
- L'application de la mise à jour change le logiciel = *Risque pour la  production*
- Gestion des mises à jours avec des tests et des environnements dédiés = *Nécessité méthodologique*

### Minimisation physique
Disposer uniquement du nécessaire 
- Périphériques d'entrée (port USB, lecteur optique, ...)
- Périphériques réseaux (ethernet, wifi, bluetooth)
	- Possibilité de désactiver et activer le matériel au besoin
- Composant d'administration à distance

### Sécurité physique
- Machine d'autorité de certification
- Restriction d'accès
- Mot de passe de démarrage (BIOS et/ou BOOT)
- Démarrage via périphériques amovibles désactivé
- Chiffrement des disques


## L'outils Bareos
### Les composants
- Bareos Director = *bareos-dir*
	- Chef d'orchestre
- Bareos Console
	- CLI
- Bareos File Daemon = *bareos-fd*
	- Collecte les informations pour BSD
	- Doit être installé sur les clients
- Bareos Storage Daemon = *bareos-sd*
	- Effectue les sauvegardes
- Catalogue
	- L'ensemble des tâches de sauvegarde

### A savoir
- BAREOS peut sauvegarder des clients GNU/Linux et Windows
- BAREOS est l'acronyme de Backup Archiving Recovery Open Sourced
- *bconsole* permet de lancer la console BAREOS
- *Bareos WebUI* est un composant facultatif
- *status dir* permet de lister les jobs planifiées, en cours et terminés

### Les jobs
- FileSet
	- Ensemble de chemins de fichiers que le *Job* doit sauvegarder
- Client 
	- Là où se trouve les fichiers
- Schedule
	- Planification automatiser du *Job*
- Pool
	- Ensemble des supports de stockage présents sur un *Storage Daemon* à utiliser pour le *Job*

## Les différences
### La sauvegarde
C'est une copie de données en production actuellement utilisées. Nous pouvons restaurer ces données en cas de perte ou de corruption.

### L'archivage
C'est un stockage à long terme de données qui ne serve plus à la production, mais qui doivent être conservées pour des raisons légales ou historiques. Les données sont supprimées de la production.

### Le clonage
C'est la réplique exacte d'un système ou d'un disque dur, souvent utilisé pour déployer des configurations identiques sur plusieurs machines.
