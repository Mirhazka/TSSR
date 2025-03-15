# Exploiter des serveurs Linux - Fiche de révision détaillée

## 🖥️ Les Shells

### Qu'est-ce qu'un Shell ?
Le shell est une interface entre l'utilisateur et le noyau Linux. Il interprète les commandes de l'utilisateur et leur transmet au noyau pour exécution. Les deux shells les plus courants sous Linux sont **Bash** et **Zsh**.

- **Bash** : Bourne Again Shell, très utilisé pour les scripts et l'interaction en ligne de commande.
- **Zsh** : Z Shell, offrant des fonctionnalités avancées et une meilleure gestion des commandes.
  
### Commandes utiles :
- `echo` : Affiche un texte ou une variable.
- `cd` : Change de répertoire.
- `ls` : Liste les fichiers et répertoires.
- `man` : Affiche le manuel d'une commande.

---

## 💾 La gestion du stockage sous Linux

### Systèmes de fichiers :
Les systèmes de fichiers sous Linux sont essentiels pour l'organisation des données.

- **ext4** : Le système de fichiers le plus couramment utilisé.
- **XFS** : Utilisé pour les grandes capacités de stockage.
- **Btrfs** : Système de fichiers plus avancé avec des fonctions comme la gestion des snapshots.

### Commandes utiles :
- `df` : Affiche l'utilisation de l'espace disque.
- `fdisk` : Gère les partitions de disque.
- `mount` et `umount` : Monter et démonter un système de fichiers.

---

## 🛠️ Gestion avancée avec LVM (Logical Volume Manager)

LVM permet de créer des volumes logiques qui peuvent être redimensionnés facilement. Il est très utile pour gérer dynamiquement l'espace disque. Voici des exemples détaillés avec les commandes.

### Concepts clés :
- **Volume Group (VG)** : Groupe de volumes physiques.
- **Logical Volume (LV)** : Unité logique à utiliser comme partition.
- **Physical Volume (PV)** : Disques physiques ou partitions sous-jacentes.

### Étapes pour créer un volume logique avec LVM :

#### 1. Créer un volume physique (PV)
Pour créer un volume physique à partir d'un disque ou d'une partition, utilisez la commande `pvcreate`.

```bash
sudo pvcreate /dev/sdb
````

Cela initialise le disque `/dev/sdb` comme un volume physique pour LVM.

#### 2. Créer un groupe de volumes (VG)

Ensuite, on crée un groupe de volumes en utilisant le volume physique créé.

```bash
sudo vgcreate vg_data /dev/sdb
```

Cela crée un groupe de volumes nommé `vg_data` à partir de `/dev/sdb`.

#### 3. Créer un volume logique (LV)

Maintenant, nous allons créer un volume logique à partir du groupe de volumes `vg_data`.

```bash
sudo lvcreate -L 10G -n lv_data vg_data
```

Cela crée un volume logique de 10 Go nommé `lv_data` dans le groupe de volumes `vg_data`.

#### 4. Formater le volume logique

Avant de pouvoir utiliser le volume logique, il doit être formaté avec un système de fichiers, par exemple ext4.

```bash
sudo mkfs.ext4 /dev/vg_data/lv_data
```

#### 5. Monter le volume logique

Une fois formaté, vous pouvez monter le volume logique sur un répertoire.

```bash
sudo mount /dev/vg_data/lv_data /mnt/data
```

Cela monte le volume logique sur le répertoire `/mnt/data`.

#### 6. Agrandir un volume logique

Pour agrandir un volume logique existant, on peut utiliser la commande `lvextend`. Voici comment augmenter un volume de 10 Go :

```bash
sudo lvextend -L +10G /dev/vg_data/lv_data
sudo resize2fs /dev/vg_data/lv_data
```

Le premier commande augmente la taille du volume logique, et la deuxième ajuste le système de fichiers.

#### 7. Réduire un volume logique

Pour réduire un volume logique, commencez par démonter le volume, puis utilisez `lvreduce` :

```bash
sudo umount /mnt/data
sudo lvreduce -L -5G /dev/vg_data/lv_data
sudo resize2fs /dev/vg_data/lv_data
```

---

## 👥 La gestion des utilisateurs sous Linux

La gestion des utilisateurs permet de contrôler l'accès aux systèmes Linux. Voici des exemples détaillés avec les commandes pour gérer les utilisateurs.

### Commandes essentielles pour gérer les utilisateurs :

#### 1. Créer un utilisateur

Pour créer un utilisateur, utilisez `useradd`. Par exemple, pour ajouter un utilisateur `john` :

```bash
sudo useradd john
sudo passwd john
```

Cela crée un utilisateur `john` et lui attribue un mot de passe.

#### 2. Modifier un utilisateur

Pour modifier un utilisateur existant, on peut utiliser `usermod`. Par exemple, pour changer le groupe principal de `john` à `admin` :

```bash
sudo usermod -g admin john
```

#### 3. Supprimer un utilisateur

Pour supprimer un utilisateur et son répertoire personnel, utilisez `userdel` avec l'option `-r` :

```bash
sudo userdel -r john
```

#### 4. Ajouter un utilisateur à un groupe

Pour ajouter un utilisateur à un groupe, utilisez `usermod -aG`. Par exemple, pour ajouter `john` au groupe `sudo` :

```bash
sudo usermod -aG sudo john
```

#### 5. Vérifier les utilisateurs et groupes

Pour lister tous les utilisateurs :

```bash
cat /etc/passwd
```

Pour lister tous les groupes :

```bash
cat /etc/group
```

#### 6. Modifier les mots de passe

Pour changer le mot de passe d’un utilisateur, utilisez la commande `passwd` :

```bash
sudo passwd john
```

#### 7. Gérer les permissions d'un fichier

Les permissions sur un fichier ou un répertoire sont gérées avec `chmod`, `chown` et `chgrp`.

- **chmod** : Change les permissions d’un fichier.
- **chown** : Change le propriétaire d’un fichier.
- **chgrp** : Change le groupe associé à un fichier.

##### Exemple : Changer le propriétaire et les permissions d’un fichier

```bash
sudo chown john:admin /home/john/file.txt
sudo chmod 755 /home/john/file.txt
```

Cela change le propriétaire du fichier `file.txt` à `john` et son groupe à `admin`, et définit les permissions en lecture-exécution pour tous les utilisateurs.

---

## 🌐 DHCP & DNS

### DHCP (Dynamic Host Configuration Protocol)

Le DHCP attribue automatiquement des adresses IP aux clients du réseau.

- **Serveur DHCP** : Utilise `isc-dhcp-server` sur Debian/Ubuntu.
- **Client DHCP** : Utilise `dhclient` pour obtenir une adresse IP.

### DNS (Domain Name System)

Le DNS permet de traduire les noms de domaine en adresses IP.

- **Serveur DNS** : `BIND9` est le plus utilisé sous Linux.
- **Client DNS** : Fichier `/etc/resolv.conf` pour la configuration du serveur DNS.

### Commandes utiles :

- `systemctl restart isc-dhcp-server` : Redémarre le serveur DHCP.
- `dig` : Interroge le DNS pour obtenir des informations sur un domaine.

---

## 🔒 SSH sous Linux

SSH (Secure Shell) permet de se connecter à un serveur à distance de manière sécurisée.

### Configurer un serveur SSH :

- Installer `openssh-server` sur le serveur.
- Modifier le fichier `/etc/ssh/sshd_config` pour personnaliser la configuration.

### Commandes utiles :

- `ssh user@hostname` : Se connecter à un serveur distant.
- `scp file user@hostname:/path` : Copier des fichiers entre hôtes.

---

## 🌐 HTTP et Serveur Web (Apache et Nginx)

### Apache

Apache est l'un des serveurs web les plus utilisés.

- **Installation** : `sudo apt install apache2`
- **Configuration** : Fichiers de configuration dans `/etc/apache2/sites-available/`.

### Nginx

Nginx est un serveur web léger et performant.

- **Installation** : `sudo apt install nginx`
- **Configuration** : Fichiers de configuration dans `/etc/nginx/sites-available/`.

### Commandes utiles :

- `systemctl restart apache2` : Redémarre Apache.
- `systemctl restart nginx` : Redémarre Nginx.
