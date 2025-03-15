# Exploiter un réseau IP

## 📌 Ethernet  

### Ethernet = Internet ?  
Ethernet est un ensemble de protocoles permettant la mise en place de réseaux locaux (LAN) filaires. Il est défini par la norme **IEEE 802.3** et propose des débits de **10 Mbps à 400 Gbps**.  

### 🏛️ La norme Ethernet  

#### 📜 Définition  
Ethernet est le protocole filaire le plus couramment utilisé pour les réseaux locaux.  

#### 🏗️ Architecture en couches IEEE  
- **Couche PHY** (Physique - 1)  
- **Couche Liaison (2)** séparée en :  
  - **MAC (Medium Access Control)** → spécifique à chaque protocole  
  - **LLC (Logical Link Control)** → commune à tous les protocoles IEEE  

#### 📌 Principales normes IEEE  
- **802.3** : Ethernet  
- **802.11** : Wi-Fi  
- **802.15** : Bluetooth  
- **802.16** : WiMAX  

### 🔌 Le câblage et les équipements  

#### 🏗️ Types de câbles  
- **Coaxial** (ancien) → utilisé avec 10Base2  
- **Paire torsadée** (actuel) → 4 paires torsadées, 8 fils  
- **RJ45** → Connecteur standard des réseaux filaires  

#### 🔁 Câblage droit ou croisé ?  
- **Droit (MDI)** → PC vers switch  
- **Croisé (MDI-X)** → Switch vers switch  
- **Auto MDI/MDIX** → Automatisation du type de connexion  

#### 🛡️ Type de blindage RJ45  
- **U/UTP** : Non blindé  
- **F/UTP** : Blindage global  
- **U/FTP** : Blindage par paire  
- **S/FTP** : Blindage maximal  

#### 🔥 Fibre optique  
- **Monomode (SMF)** → Longue distance, plus coûteux  
- **Multimode (MMF)** → Moins cher, distances plus courtes  

### 🏭 Les équipements réseau  

#### 🖧 Carte réseau (NIC)  
- Permet la connexion au réseau  
- Associée à une **adresse MAC**  

#### 🔌 Modules SFP  
- Utilisés pour les connexions fibre optique  
- Types : **GBIC, SFP, QSFP, CFP, XFP**  

#### 🖥️ Hub vs Switch  
- **Hub** → Diffuse à tous, obsolète  
- **Switch** → Envoie uniquement au destinataire (utilise une table MAC)  

#### 💡 Ports Ethernet  
- **Link** → Vérifie la connexion physique  
- **Activity** → Indique le trafic réseau  

### 🏷️ Les adresses MAC  

#### 📍 Définition  
Chaque interface réseau dispose d'une adresse **MAC** unique.  

#### 🏢 Attribution des MAC  
- **IEEE assigne un préfixe unique aux constructeurs**  
- **Les constructeurs garantissent l’unicité du suffixe**  

#### ⚠️ Problèmes  
- **Les MAC peuvent être modifiées** (ex: VM, spoofing)  
- **Ne pas se fier aux MAC pour la cybersécurité**  

#### 🔍 Format d'une adresse MAC  
- **48 bits (6 octets)** → Ex: `00:1A:2B:3C:4D:5E`  
- **Bit U/L** : 0 = Universelle, 1 = Locale  
- **Bit I/G** : 0 = Individuelle, 1 = Groupe  
- **Adresse de broadcast** : `FF:FF:FF:FF:FF:FF`  

#### 🔎 Commandes pour voir sa MAC  
- **Linux** : `ip l`  
- **Windows (PowerShell)** : `Get-NetAdapter`  

### 📦 La trame Ethernet  

#### 📋 Structure d’une trame  
1. **Préambule** (Synchronisation)  
2. **En-tête MAC**  
   - Adresse MAC Destination  
   - Adresse MAC Source  
   - EtherType (Protocole de niveau supérieur)  
3. **Données** (Payload)  
4. **Checksum CRC** (Contrôle d'erreur)  

#### 🎯 EtherType  
- **< 1500** → Indique la longueur des données  
- **≥ 1536** → Indique le protocole (ex: IPv4, ARP)  

#### 🔎 Vérification des erreurs  
- **CRC (Cyclic Redundancy Check)** → Détruit la trame en cas d’erreur  

### 🔄 Protocole CSMA/CD  

#### 📌 Problème  
Ethernet en topologie **bus** entraîne des **collisions** lors des transmissions simultanées.  

#### 🛠️ Fonctionnement CSMA/CD  
1. **CS (Carrier Sense)** → Écoute du réseau  
2. **MA (Multiple Access)** → Accès partagé  
3. **CD (Collision Detection)** → Détection des collisions  
4. **Backoff** → Attente aléatoire avant nouvelle tentative  

#### ❌ Best Effort  
Ethernet n’assure **pas** la retransmission → confiée aux **couches supérieures (ex: TCP)**  

#### ⚡ CSMA/CD aujourd’hui  
- **Obsolète** avec les switchs Full-Duplex  
- **Disparu à partir de 10 Gbps**  

### 🔀 La commutation  

#### 🎛️ Le switch  
- Fonctionne en **couche 2**  
- **Apprend** les adresses MAC  
- **Filtrage** → Envoie la trame uniquement au bon port  

#### 🔍 Transparent Bridging  
- **Apprentissage** → Ajout d’une entrée MAC ↔ Port  
- **Inondation** → Envoi à tous si destination inconnue  
- **Réexpédition** → Envoi sur le port correct  

#### 🔧 Fonctionnalités avancées  
- **Empilable (stack)**  
- **Agrégation de liens (LACP 802.3ad)**  
- **Supervision (SNMP, SMON)**  
- **Port Mirroring** (Duplication du trafic)  
- **QoS (802.1p)**  
- **Authentification (802.1x)**  

### 🏠 Les VLAN  

#### 🏢 VLAN (Virtual LAN)  
- **Sépare les domaines de broadcast**  
- **Hôtes sur VLAN différents ne communiquent pas directement**  

#### 📜 IEEE 802.1Q  
- **Ajoute un tag VLAN (4 octets) dans la trame Ethernet**  
- **VLAN ID** (12 bits) → Permet jusqu’à **4096 VLANs**  

#### 🔗 VLAN inter-switch  
- **Le tag VLAN n’est transporté que sur les liens entre switches**  
- **Les switches ajoutent/enlèvent les tags automatiquement**  

### 🔮 Évolutions d’Ethernet  

#### 🚀 Extensions notables  
- **Auto-négociation** (débit, duplex)  
- **PoE (Power over Ethernet)** → Alimentation via Ethernet  
- **Jumbo Frames** → MTU augmenté jusqu’à 9000 octets  

--- 

## 📌 IP Version 4 – Adresse et Paquet  

### Rappel : Ethernet  
- **Norme IEEE 802.3** : permet la communication entre machines sur un réseau local filaire (LAN).  
- **Adresses MAC** : identifiants "uniques" des interfaces réseau.  
- **MTU : 1500 octets** → Taille max d'une trame Ethernet.  
### 🏛️ Définition de l'IP  

#### 📜 Internet Protocol (IP)  
- **Protocole d’interconnexion de réseaux** (Couche 3 – Modèle OSI).  
- Standardisé par l'**IETF** (Internet Engineering Task Force).  
- 2 versions actives : **IPv4 & IPv6**.  
- Permet **Internet**, un réseau mondial accessible à tous.  

#### 📖 Standards de l’Internet  
- **RFC** (Request for Comments) → Définition des protocoles Internet.  
- **RFC 791** (1980) → Définition de l’IPv4.  
- **RFC 2460** (1998) → Définition de l’IPv6.  

### 🖧 La notion de réseau  

#### 📌 Définition  
- **Lien** : Ensemble d'interfaces connectées sur un même réseau physique.  
- **Réseau logique** : Ensemble d’interfaces partageant un même préfixe IP.  
- **Routeur** : Interconnecte plusieurs réseaux logiques.  

#### 🔧 Architecture réseau  
- Un administrateur doit concevoir ses **réseaux IP** en fonction des **réseaux physiques**.  
- L’interconnexion se fait via **passerelles (routeurs)**.  

### 📍 Les adresses IPv4  

#### 🔢 Format des adresses  
- **Adresse sur 32 bits** (4 octets).  
- Notation **décimale pointée** (ex : `192.168.1.1`).  
- **2 parties** :  
  - **Préfixe réseau** : identifie le réseau.  
  - **Identifiant hôte** : identifie la machine dans le réseau.  

#### 📦 Classes d’adresses (Historiques)  
- **Classe A** : 8 bits réseau / 24 bits hôte (ex : `10.0.0.0`).  
- **Classe B** : 16 bits réseau / 16 bits hôte (ex : `172.16.0.0`).  
- **Classe C** : 24 bits réseau / 8 bits hôte (ex : `192.168.0.0`).  
⚠️ **Limites** → Classes trop rigides, menant à une pénurie d’adresses.  

#### 🚀 CIDR (Classless Inter-Domain Routing)  
- Définition : Notation `a.b.c.d/s` (ex : `192.168.1.0/24`).  
- Permet un découpage flexible des adresses.  
- **Masque de réseau** : définit la partie réseau d’une adresse.  

#### 🔎 Adresses réservées  
- **Réseaux privés (RFC 1918)** :  
  - `10.0.0.0/8`  
  - `172.16.0.0/12`  
  - `192.168.0.0/16`  
- **Adresse de loopback (localhost)** : `127.0.0.1/8`.  
- **Adresse de diffusion** : `255.255.255.255/32`.  
- **Multicast** : `224.0.0.0/4`.  

### 🏗️ Configuration du réseau  

#### Sur Linux  
- Configuration **temporaire** avec `ip` :  
```bash
  ip address add 192.168.1.100/24 dev eth0
```

- Configuration **persistante** :
    - `/etc/network/interfaces`
    - `/etc/netplan/` (Ubuntu moderne)

#### Sur Windows (PowerShell)

- **Afficher la config** :
```powershell
Get-NetIPConfiguration
```

- **Ajouter une adresse IP** :
```powershell
New-NetIPAddress -InterfaceIndex 2 -IPAddress 192.168.1.100 -PrefixLength 24 -DefaultGateway 192.168.1.1
```

### 📦 Le paquet IPv4

#### 🏛️ Structure du paquet

1. **Version** (4 bits) → 4 pour IPv4.
2. **IHL (Internet Header Length)** (4 bits) → Taille de l’en-tête.
3. **Type of Service (ToS)** (8 bits) → QoS.
4. **Total Length** (16 bits) → Taille du paquet.
5. **Identification** (16 bits) → ID du paquet.
6. **Flags & Fragment Offset** → Gestion de la fragmentation.
7. **TTL (Time To Live)** (8 bits) → Nombre de sauts max.
8. **Protocol** (8 bits) → Type de protocole transporté (ex: TCP, UDP).
9. **Header Checksum** (16 bits) → Vérification de l'en-tête.
10. **Source IP** (32 bits) → Adresse IP source.
11. **Destination IP** (32 bits) → Adresse IP destination.

### 🔄 Protocoles connexes

#### 🔎 **ICMP (Internet Control Message Protocol)**

- Utilisé pour les messages d'erreur et diagnostic réseau.
- **Exemples de types ICMP** :
    - `0` → Echo Reply (réponse à `ping`).
    - `8` → Echo Request (`ping`).
    - `11` → Time Exceeded (TTL dépassé).

#### 🏷️ **ARP (Address Resolution Protocol)**

- Permet de trouver l’adresse MAC associée à une IP.
- **Fonctionnement** :
    - Envoi d’une requête ARP en **broadcast**.
    - La machine détentrice de l’IP répond avec son **adresse MAC**.
- **Commande pour afficher la table ARP** :
```bash
arp -a
```

### 🏠 DHCP (Dynamic Host Configuration Protocol)

#### 📜 Objectif

- Permet l’attribution **automatique** d’adresses IP.
- Gestion dynamique des baux (attribution temporaire).
- Réduit la **configuration manuelle** des machines.

#### 🔧 Fonctionnement

1. **DHCP Discover** (client → broadcast) → Demande d’une adresse.
2. **DHCP Offer** (serveur → client) → Proposition d’une adresse.
3. **DHCP Request** (client → serveur) → Acceptation de l’offre.
4. **DHCP Ack** (serveur → client) → Confirmation & envoi de la config.

#### 📌 Paramètres fournis par DHCP

- Adresse IP & masque.
- Passerelle par défaut.
- Serveurs DNS.
- Serveur de temps (NTP).

#### 🔎 Commandes

- **Linux** :
```bash
dhclient eth0
```
    
- **Windows (PowerShell)** :
```powershell
ipconfig /renew
```

---

## 📌 IP Version 6 – Adresse et Paquet  
### 🚀 Objectifs d’IPv6  
- **Étendre les capacités d’adressage** (128 bits).  
- **Simplifier les en-têtes** (meilleure efficacité).  
- **Automatiser la configuration** (SLAAC).  
- **Améliorer la sécurité** (IPsec natif).  
- **Réduire la fragmentation** (éviter fragmentation en route).  

### 📍 Les adresses IPv6  

#### 🔢 Format des adresses  
- **128 bits** (≈ `3,4 × 10³⁸` adresses possibles).  
- **Notation hexadécimale** en **8 groupes de 16 bits** séparés par `:`.  
- **Simplifications** :  
  - **Suppression des zéros en tête** (ex: `0012` → `12`).  
  - **Remplacement d’une suite de groupes `0000` par `::`** (une seule fois).  
- **Exemples** :  
```plaintext
  2001:0db8:0000:85a3:0000:0000:ac1f:8001  
  ↓
  2001:db8:0:85a3::ac1f:8001  
```

- **Notation CIDR** pour le découpage (ex: `2001:db8::/64`).

#### Catégories d’adresses
- **Unicast** : Une seule interface.
- **Multicast** : Transmission à plusieurs destinataires.
- **Anycast** : Transmission à une seule interface parmi plusieurs.  
❌ **Suppression du broadcast** (remplacé par multicast).

#### 🔍 Adresses particulières
- `::1` → **Boucle locale** (`127.0.0.1` en IPv4).
- `::` → **Adresse indéfinie** (`0.0.0.0` en IPv4).
- `ff00::/8` → **Multicast**.
- `fe80::/10` → **Lien-local** (utilisé pour la découverte de voisins, non routable).
- `fc00::/7` → **Adresses locales uniques (ULA)**, privées et non routables sur Internet.

#### 🏢 Adresses publiques et routage

- **Préfixe global** (ex: `2a00::/12` pour RIPE NCC).
- **Attribution hiérarchique** (IANA → RIR → LIR → FAI → Clients).
- **Politique d’attribution** : Un site peut avoir **plusieurs réseaux** (`/64` minimum, `/48` pour les grandes structures).

### 🔄 Auto-configuration IPv6 (SLAAC)

#### 🛠️ Objectif
- **Configuration automatique** sans DHCP obligatoire.
- **Facilité de re-numérotation** (utile pour les changements de FAI).
- **Durée de vie des adresses** pour éviter des conflits.

#### 🎯 Identifiant d’interface
- **64 bits** (ex: dérivé de l’adresse MAC via EUI-64).
- **Méthodes** :
    - **Génération aléatoire** (RFC 8981).
    - **Basé sur la MAC** (RFC 4291).
    - **Basé sur cryptographie** (RFC 3972).

#### 📌 Préfixe réseau
- **Lien-local (`fe80::/64`)** → Toujours configuré automatiquement.
- **Autres adresses** → Annoncées par **Router Advertisement (RA)** via **ICMPv6**.
### 📦 Le paquet IPv6

#### 🏛️ Structure de l'en-tête
1. **Version** (4 bits) → Toujours `6`.
2. **Traffic Class** (8 bits) → Priorité et QoS.
3. **Flow Label** (20 bits) → Gestion des flux.
4. **Payload Length** (16 bits) → Taille des données transportées.
5. **Next Header** (8 bits) → Indique le protocole encapsulé (ex: TCP = 6, UDP = 17).
6. **Hop Limit** (8 bits) → Nombre max de sauts (**équivalent TTL IPv4**).
7. **Source Address** (128 bits) → IP source.
8. **Destination Address** (128 bits) → IP destination.

#### ❌ Pas de fragmentation en route
- **IPv6 ne fragmente pas en route** → Requiert **Path MTU Discovery (PMTUd)** (RFC 8201).
- **Si un paquet est trop grand** :
    - Le routeur le **rejette**.
    - Il envoie un message ICMPv6 pour informer l’expéditeur.

### 🔄 Protocoles associés

#### 🔎 **ICMPv6 (RFC 4443)**
- **Messages d'erreur et de contrôle** (ex: `ping`, découverte des voisins).
- **Utilisé pour SLAAC et NDP** (équivalent de ARP en IPv4).
- **Transporté avec Next Header = `58` (0x3A)**.

#### 🔄 **NDP (Neighbor Discovery Protocol, RFC 4861)**
- Remplace **ARP et IGMP**.
- **Router Advertisement (RA)** : Annonce les préfixes et paramètres réseaux.
- **Router Solicitation (RS)** : Demande de configuration.
- **Neighbor Solicitation (NS)** : Vérifie la présence d’un hôte.
- **Neighbor Advertisement (NA)** : Réponse à NS.
- **Redirect** : Optimisation du routage.

#### 🏠 **DHCPv6 (RFC 3315)**
- **Optionnel** (SLAAC peut suffire).
- Utilisé pour **les DNS dynamiques** et autres paramètres spécifiques.
- Utilise **Multicast** (`FF02::1:2`) sur **UDP ports 546 et 547**.

#### 🔒 **IPsec (RFC 4301)**
- **Sécurisation des communications IP**.
- Inclus **nativement** dans IPv6 (mais optionnel en pratique).
- Protocoles associés :
    - **AH (Authentication Header)** → Intégrité et authentification.
    - **ESP (Encapsulating Security Payload)** → Chiffrement.
    - **IKE (Internet Key Exchange)** → Gestion des clés.

#### 📡 **Mobilité IPv6 (RFC 6275)**
- Permet à un hôte de conserver son adresse IP en **changeant de réseau**.
- **Home Address** : Adresse fixe de l’utilisateur.
- **Care-of Address** : Adresse temporaire obtenue dans le réseau visité.
- **Home Agent** : Réachemine les paquets vers la bonne adresse.

---

## Le routage IP

---

## DNS

---

## WiFi
