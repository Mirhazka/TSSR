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
- Établit, maintient et termine des sessions entre des périphériques terminaux
- Load balancer, Firewall avec inspection de paquet

### Couche 5 : Application
- Établit des sessions entre des applications; Encode, chiffre et compresse les données utiles; Services applicatifs au plus proche des utilisateurs
- Serveur RDP, Proxy applicatif; Chiffrement SSL/TLS, Convertisseur de format (encodeur/décodeurs); Serveur Web (Apache, Nginx), Client FTP (FileZilla)

---

## Cybersécurité
### Vulnérabilité & Menace
L'analyse de risques évalue les vulnérabilités du système, les menaces potentielles et les attaques qui peuvent exploiter ces faiblesses pour causer des dommages.

#### Principales actions de cybersécurité :
- **Prévenir** : éviter les vulnérabilités
- **Détecter** : savoir si et quand une attaque a lieu
- **Réagir** : décider de la réponse appropriée à l'attaque
- **Réparer** : remettre le SI en état opérationnel

#### Types de menaces :
- Attaques par déni de service : DDoS
- Ransomware
- Attaques virales
- Phishing

---

## Filtrage réseau
### Définition
Un pare-feu est un dispositif de sécurité réseau qui filtre et contrôle le trafic entre des réseaux de différents niveaux de confiance, en s'appuyant sur les protocoles de transport (TCP, UDP) et des règles de routage.

#### Principes de filtrage :
- Liste de blocage
- Liste d'autorisation suivie d'un *deny all*

### DMZ
Les machines clientes ont un accès restreint, tandis que les serveurs accessibles depuis l'extérieur sont placés en **DMZ**, une zone contrôlée avec un filtrage spécifique pour limiter les risques d'intrusion.

---

## VPN
### Types de VPN
- **Site-à-site**
- **Host-to-network**
- **Host-to-host**

### Solutions de VPN
- **IPsec**
- **OpenVPN**

⚠️ **Attention** : La mise en place de VPN ouvre une brèche entre des réseaux.

---

## Journalisation
### GNU / Linux
- **Syslog** (date, hôte, service, ID, priorité, message)
  - 24 catégories de messages (0 à 23)
  - Stocké dans `/var/log/`
    - `/var/log/auth.log`
    - `/var/log/kern.log`
- **Systemd**
  - Format binaire dans `/run/systemd/journal`
  - Outil : `journalctl`
  - Peut transmettre à syslog

#### Outils d'analyse des logs :
- Logwatch
- Graylog
- Loganalyzer

### Windows
- **Observateur d'événements** (`event viewer`)
  - Informations système
  - Enregistrements d'erreurs
- Fichiers de logs : `C:\Windows\System32\winevt\Logs`

#### Niveaux de criticité :
- High
- Medium
- Low

#### Event ID intéressants :
- `4624` : Logon normal avec succès
- `4625` : Logon avec erreur
- `4740` : Compte verrouillé
- `4728` : Ajout d’un utilisateur à un groupe global
- `4732` : Ajout d’un utilisateur à un groupe local
- `4756` : Ajout d’un utilisateur à un groupe universel
- `4663` : Tentative d’accès à des objets
- `1102` : Suppression des journaux

---

## Supervision
La **supervision** permet d'**observer à distance ce qui se passe sur un réseau**. Elle est essentielle pour :
- **Détection** : pannes, incidents
- **Modifications** : configuration, documentation
- **Disponibilité** : consommation de ressources
- **Amélioration des performances** : statistiques
- **Prévention** : activités suspectes

L'**hypervision** centralise les outils de supervision. Utilisation du protocole **SNMP** et de la base **MIB**.

#### Outils de supervision :
- Solarwinds
- PRTG
- NextThink
- Nagios
- Zabbix

---

## IDS & IPS

| IDS | IPS |
|---|---|
| Intrusion Detection System | Intrusion Prevention System |
| Network IDS & Host IDS | Network IPS, Host-Based IPS, Kernel IPS |
| Peut détecter et alerter, mais ne bloque pas | Peut détecter, alerter et interrompre une attaque |
| Snort, Splunk | Snort, Fail2ban |

---

## Les ACL

### **Objectifs des ACL sur un routeur**
✅ Bloquer les accès non autorisés (*ex. restreindre l’accès à Internet pour certains utilisateurs*).  
✅ Sécuriser les interconnexions entre VLANs ou sous-réseaux.  
✅ Filtrer le trafic selon IP, protocoles et ports.  

### **Types d’ACL**
- **ACL standard** : filtre uniquement sur l’adresse IP source.
- **ACL étendue** : filtre selon plusieurs critères (IP source/destination, protocole, ports, etc.).

### **Exemples d’ACL pour sécuriser l'accès Internet**

#### **Autoriser HTTP/HTTPS, bloquer tout le reste**
```bash
access-list 101 permit tcp any any eq 80
access-list 101 permit tcp any any eq 443
access-list 101 deny ip any any
```

#### **Bloquer un sous-réseau interne (192.168.1.0/24) d’accéder à Internet**
```bash
access-list 102 deny ip 192.168.1.0 0.0.0.255 any
access-list 102 permit ip any any
```

#### **Autoriser un serveur (192.168.1.100) à accéder en SSH à un autre réseau (192.168.2.0/24)**
```bash
access-list 103 permit tcp host 192.168.1.100 192.168.2.0 0.0.0.255 eq 22
access-list 103 deny ip any any
```

### **Application des ACL sur une interface**
```bash
interface GigabitEthernet0/1
  ip access-group 101 in
```
📌 **"in"** pour filtrer le trafic entrant, **"out"** pour le trafic sortant.  

Les ACL sont essentielles pour la **sécurisation des réseaux** et doivent être configurées avec précaution. 🚀

