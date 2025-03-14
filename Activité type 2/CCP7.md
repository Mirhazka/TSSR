# Maintenir et sécuriser les accès à Internet et les interconnexions des réseaux

## Le modèle TCP/IP vs Le modèle OSI
![image](https://github.com/Mirhazka/TSSR/blob/dde4df851017de6a5a842c4858e33c5d897eb56c/Ressources/tcpip-comparatif.webp)

### Couche 1 : Physique
- Encodage du signal, câblage et connecteurs, spécifications physiques.
- Câbles, Hub, ...

### Couche 2 : Liaison
- Adresse localement les interfaces, livre les informations localement, méthode MAC
- Switch, Carte réseau, ...

### Couche 3 : Réseau
- Adresse les interfaces globalement et détermine les meilleurs chemins à travers un inter-réseau
- Routeur, Pare-feu, ...

### Couche 4 : Transport
- Etablit, maintient et termine des sessions entre des périphériques terminaux
- Load balancer, Firewall avec inspection de paquet

### Couche 5 : Application
- Etablit des sessions entre des applications; Encode, chiffre et compresse les données utiles; Services applicatifs au plus proche des utilisateurs
- Serveur RDP, Proxy applicatif; Chiffrement SSL/TLS, Convertisseur de format (encodeur/décodeurs); Serveur Web (Apache, Nginx), Client FTP (File Zilla)

## Cybersécurité
### Vulnérabilité & Menace
L'analyse de risques évalue les vulnérabilités du système, les menaces potentielles et les attaques qui peuvent exploiter ces faiblesses pour causer des dommages.
- Prévenir : éviter les vulnérabilités
- Détecter : savoir si et quand une attaque à lieu
- Réagir : décider de la réponse appropriée à l'attaque
- Réparer : remettre le SI en état opérationnel
- Type de menace
	- Les attaques par déni de service : DDoS
	- Le ransomware
	- Les attaques virales
	- Fishing

## Filtrage réseau
### Définition
Un pare-feu est un dispositif de sécurité réseau qui filtre et contrôle le trafic entre des réseaux de différents niveaux de confiance, en s'appuyant sur les protocoles de transport (TCP, UDP) et des règles de routage.
- Liste de blocage
- Liste d'autorisation puis finir sur un deny all

### DMZ
Les machines clientes ont un accès restreint, tandis que les serveurs accessibles depuis l'extérieur sont placés en DMZ, une zone contrôlée avec un filtrage spécifique pour limiter les risques d'intrusion.

## VPN
### Les types
- Sites à sites
- Host to network
- Host to host

### Les solutions
- IPsec
- OpenVPN

**Attention**, la mise en place de VPN ouvre une brèche entre des réseaux.

## Journalisation
### GNU / Linux
- Syslog (date, hôte du message, service/processus, ID, priorité, le message)
  - 24 catégories de messages (0 à 23)
  - Les 8 derniers (16 à 23) sont réservées
  - Stocké dans */var/log/*
    - /var/log/auth.log
    - /var/log/kern.log
- Systemd 
  - au format binaire dans /run/systemd/journal
  - outil : `journalctl`
  - peut transmettre à syslog
- Analyse des logs
  - logwatch
  - graylog
  - loganalyzer

### Windows
- L'observateur d'évènements (event viewer) est le journal dans lequel toute l'activité est enregistrée
  - Information simple
  - Enregistrement d'erreurs de fonctionnalités
- Les fichiers de logs sont dans `C:\Windows\System32\winevt\Logs`
- 3 niveaux de criticité :
  - High
  - Medium
  - Low
- Quelques event ID intéressant
  - 4624 : logon normal avec succès
  - 4625 : logon avec erreur de connexion
  - 4740 : compte verrouillé
  - 4728 : ajout d’un utilisateur à un groupe de sécurité global
  - 4732 : ajout d’un utilisateur à un groupe de sécurité local
  - 4756 : ajout d’un utilisateur à un groupe de sécurité universel
  - 4663 : tentative d’accès à des objets
  - 1102 : suppression des journaux

## Supervision
C'est la **surveillance** du bon fonctionnement d'un système, cela permet d'**observer à distance ce qui se passe sur un réseau**. La supervision est une aide à :
- La détection (pannes/incidents systèmes, services, historique)
- La modifications (configuration, révision de documentation)
- La disponibilité (consommation de ressources, débit)
- L'amélioration des performances (suivi statistique)
- La prévention des activités suspectes

En suivant, nous avons l'**hypervision** qui centralise les outils de supervision d'infrastructure, d'applications et de référentiels. La supervision utilise le protocole **SNMP** (Simple Network Management Protocol) et la base de donnée **MIB**(Management Information Base).  
  
Exemple de logiciel de supervision :
- Solarwinds
- PRTG
- NextThink
- Nagios
- Zabbix

## IDS & IPS

IDS | IPS
--- | ---
Intrusion Detection System | Intrusion Prevention System
Network IDS & Host IDS | Nework IPS, Host-Based IPS, Kernel IPS
Analyse seulement l'activité pour détecter toute intrusion | Analyse l'activité pour détecter toute intrusion et sécurise



