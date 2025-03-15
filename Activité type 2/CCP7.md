# Maintenir et sécuriser les accès à Internet et les interconnexions des réseaux

## 📡 Principe des réseaux
Les réseaux informatiques sont un ensemble d'équipements interconnectés permettant d'échanger des informations. Leur but est de permettre la communication entre différents systèmes (ordinateurs, serveurs, périphériques) au sein d'une organisation ou à travers Internet.

**Utilité** : Faciliter le partage de données et de ressources entre les utilisateurs et les systèmes informatiques.

**Exemples** :
- Réseau local (LAN)
- Réseau étendu (WAN)
- Internet

### Modèle OSI et modèle TCP/IP

#### Modèle OSI (Open Systems Interconnection)
Le modèle OSI est un cadre conceptuel divisé en 7 couches qui permet d'expliquer comment les données circulent dans un réseau.

**Utilité** : Standardisation des protocoles réseau pour assurer l’interopérabilité entre différents systèmes.

**Exemples de couches** :
1. Couche physique (câbles, interfaces réseau)
2. Couche liaison de données (Ethernet, PPP)
3. Couche réseau (IP)
4. Couche transport (TCP, UDP)
5. Couche session (gestion des sessions)
6. Couche présentation (encodage, compression)
7. Couche application (HTTP, FTP, DNS)

#### Modèle TCP/IP
Le modèle TCP/IP est plus simple et plus utilisé dans la pratique. Il se divise en 4 couches :  
- Couche réseau
- Couche Internet (IP)
- Couche transport (TCP, UDP)
- Couche application

**Utilité** : Définir les protocoles utilisés pour la communication réseau dans un environnement Internet.

**Exemples** :
- HTTP, FTP, DNS (Application)
- TCP, UDP (Transport)
- IP (Internet)

---

## 🔐 Introduction à la cybersécurité

La cybersécurité désigne l’ensemble des pratiques, technologies et processus qui protègent les systèmes informatiques et les réseaux contre les menaces telles que les attaques, les intrusions et les vols de données.

**Utilité** : Assurer la confidentialité, l’intégrité et la disponibilité des informations et des systèmes.

**Exemples** :
- Protection contre les malwares (virus, ransomwares)
- Authentification forte (2FA)
- Sécurisation des communications via chiffrement (SSL/TLS)

---

## 🔥Firewalls

Un firewall (pare-feu) est un dispositif de sécurité qui contrôle les connexions entrantes et sortantes d'un réseau en fonction de règles de sécurité définies.

**Utilité** : Protéger les réseaux internes contre les accès non autorisés et les attaques externes.

**Exemples** :
- Firewall matériel (pare-feu physique)
- Firewall logiciel (pare-feu sur un serveur ou une machine)
- Pare-feu intégré dans les routeurs domestiques

---

## 🌐 VPN (Virtual Private Network)

Un VPN est un réseau privé virtuel permettant de sécuriser les communications sur un réseau public (comme Internet). Il crée un tunnel crypté entre l'utilisateur et le réseau privé.

**Utilité** : Garantir la confidentialité et l'intégrité des données échangées en ligne.

**Exemples** :
- **IPsec** : Protocole de sécurité pour la transmission de données sur un réseau IP.
- **OpenVPN** : Une solution VPN open-source, flexible et sécurisée.

---

## 🔒 Sécuriser les systèmes

Sécuriser un système informatique consiste à mettre en place des mesures techniques et organisationnelles pour protéger les données et les ressources contre les menaces.

**Utilité** : Prévenir les attaques, les intrusions et les fuites de données.

**Exemples** :
- Utilisation de mots de passe forts
- Mise à jour régulière des logiciels et systèmes
- Désactivation des services inutiles

---

## 📑 Journalisation sous Linux puis sous Windows

La journalisation consiste à enregistrer les événements survenus sur un système (logs) afin d’en assurer le suivi et la sécurité.

**Utilité** : Identifier rapidement les anomalies et assurer une traçabilité des actions.

**Exemples** :
- Sous **Linux** : `/var/log/syslog`, `/var/log/auth.log`
- Sous **Windows** : Event Viewer, journaux d'événements

---

## 📊 Supervision sous Linux puis sous Windows

La supervision permet de surveiller les performances et l'état des systèmes et réseaux pour anticiper les pannes.

**Utilité** : Garantir la disponibilité des services et anticiper les incidents.

**Exemples** :
- Sous **Linux** : Outils comme `Nagios`, `Zabbix`, `Prometheus`
- Sous **Windows** : System Center Operations Manager, Performance Monitor

---

## 🌐 Radius (Remote Authentication Dial-In User Service)

RADIUS est un protocole d'authentification et d'autorisation pour gérer les accès à des réseaux.

**Utilité** : Permet d’assurer un contrôle d’accès centralisé pour les utilisateurs.

**Exemples** :
- Utilisation dans les réseaux Wi-Fi pour authentifier les utilisateurs.
- RADIUS avec un serveur VPN pour sécuriser les connexions à distance.

---

## 🛡️ IPS & IDS (Intrusion Prevention System & Intrusion Detection System)

- **IDS** : Système qui détecte les intrusions dans un réseau en analysant le trafic.
- **IPS** : Système qui détecte et empêche les intrusions en agissant activement.

**Utilité** : Protéger contre les attaques en temps réel.

**Exemples** :
- IDS : Surveiller le trafic réseau et alerter en cas d'anomalie.
- IPS : Bloquer des attaques comme les tentatives de déni de service (DoS).

---

## 🧠 Snort

Snort est un logiciel open-source de détection d'intrusion et de prévention qui analyse le trafic réseau en temps réel.

**Utilité** : Surveiller et prévenir les menaces de sécurité sur un réseau.

**Exemples** :
- Détecter des tentatives d’intrusion par signature de vulnérabilité.
- Utilisé dans des systèmes IDS/IPS pour analyser le trafic réseau.
