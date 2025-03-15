# 📡 Exploiter un réseau IP

## 🌐 Ethernet
Ethernet est une technologie réseau filaire qui définit des normes pour la communication des données sur un réseau local (LAN). 
- Protocoles : IEEE 802.3
- Modes de transmission : Half-duplex, Full-duplex
- Débits courants : 100 Mbps (Fast Ethernet), 1 Gbps, 10 Gbps et plus
- Adressage : Utilisation des adresses MAC (Media Access Control)

---

## 🏠 Adresse IP (IPv4 & IPv6) & Encapsulation
### 📌 IPv4
- **Adresse sur 32 bits**, exprimée en 4 octets (ex: `192.168.1.1`)
- Catégories d’adresses :
  - **Privées** (non routables sur Internet) : `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
  - **Publiques** (routables sur Internet)
  - **Loopback** (test local) : `127.0.0.1`
  - **Lien-local** (APIPA) : `169.254.0.0/16`
  - **Multicast** : `224.0.0.0/4`
  - **Broadcast** : `255.255.255.255`

### 🌍 IPv6
- **Adresse sur 128 bits** (ex: `2001:db8::1`)
- Types d’adresses :
  - **Unicast global** : routable sur Internet (ex: `2000::/3`)
  - **Link-local** : attribuée automatiquement (`fe80::/10`)
  - **Multicast** : `ff00::/8`
  - **Loopback** : `::1`
  - **Aucune adresse** : `::`

### 🔄 Encapsulation
L’encapsulation suit le modèle OSI :
1. **Application** (HTTP, SSH, DNS…)
2. **Transport** (TCP, UDP)
3. **Réseau** (IPv4, IPv6)
4. **Liaison** (Ethernet, Wi-Fi)
5. **Physique** (Câble, fibre…)

Chaque couche ajoute un en-tête contenant des informations spécifiques. Exemple d’encapsulation HTTP sur IPv4 :
```
Ethernet | IPv4 | TCP | HTTP | Données
```

---

## 🚦 Le routage IP, NAT et les ACL
### 🛣️ Routage IP
Le routage permet à un paquet d’atteindre une destination via plusieurs réseaux.
- **Routage statique** : Configuration manuelle des routes
  ```bash
  ip route add 192.168.2.0/24 via 192.168.1.1
  ```
- **Routage dynamique** : Utilisation de protocoles (RIP, OSPF, BGP)

### 🔄 NAT (Network Address Translation)
Permet la traduction d’adresses privées en adresses publiques.
- **NAT statique** : Une IP privée vers une IP publique fixe
- **NAT dynamique** : Plusieurs IP privées vers plusieurs IP publiques
- **PAT (Port Address Translation)** : Multiples IP privées vers une seule IP publique
  ```bash
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
  ```

### 🔒 ACL (Access Control List)
Une ACL permet de filtrer le trafic réseau en définissant des règles spécifiques.

#### Exemple sur un routeur Cisco
  ```bash
  access-list 100 deny tcp any host 192.168.1.10 eq 22
  access-list 100 permit ip any any
  ```
**Explication** :
- `access-list 100 deny tcp any host 192.168.1.10 eq 22` : Bloque toute tentative de connexion TCP vers l’hôte `192.168.1.10` sur le port 22 (SSH).
- `access-list 100 permit ip any any` : Autorise tout le reste du trafic IP.

#### Exemple avec `iptables` sur Linux
  ```bash
  iptables -A INPUT -p tcp --dport 22 -s 192.168.1.100 -j DROP
  ```
**Explication** :
- `-A INPUT` : Applique la règle aux paquets entrants.
- `-p tcp --dport 22` : Cible les paquets destinés au port 22 (SSH).
- `-s 192.168.1.100` : S’applique uniquement aux connexions provenant de l’IP `192.168.1.100`.
- `-j DROP` : Bloque la connexion.

---

## 📏 Le découpage réseau et les méthodes de calcul IP
### 📌 Méthodes de calcul
Pour découper un réseau, on ajuste le masque de sous-réseau.

#### 🔹 Exemple : Découper `192.168.100.0/16` en 4 sous-réseaux
1. Réseau initial : `192.168.100.0/16` (65534 hôtes)
2. Nous devons créer **4 sous-réseaux** → **Augmenter les bits du masque**
3. `2^n >= 4`, donc **n = 2** bits supplémentaires
4. Nouveau masque : **`/18`** (16 + 2 = 18)
5. Découpage en 4 sous-réseaux :
   - **192.168.0.0/18** (192.168.0.1 → 192.168.63.254)
   - **192.168.64.0/18** (192.168.64.1 → 192.168.127.254)
   - **192.168.128.0/18** (192.168.128.1 → 192.168.191.254)
   - **192.168.192.0/18** (192.168.192.1 → 192.168.255.254)

### 🔹 Calcul du nombre d'hôtes
Formule : `2^(32 - masque) - 2`
- Exemple pour `/24` : `2^(32-24) - 2 = 254 hôtes`
- Exemple pour `/18` : `2^(32-18) - 2 = 16382 hôtes`
