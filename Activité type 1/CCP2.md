# Exploiter des serveurs Windows et un domaine ActiveDirectory
## La gestion du stockage  
### L'abstraction  
- **Chemin absolu** :  
  - `C:\Users\wilder`  
  - `C:\Windows\system32\notepad.exe`  
- **Chemin relatif** :  
  - `.\wilder`  
  - `.\notepad.exe`  
- **Variable d'environnement `PATH`** :  
  - `$env:path`  

### Les systèmes de fichiers  
#### NTFS (New Technology File System)  
Le NTFS est un système de fichiers développé par Microsoft pour les systèmes Windows modernes. Il remplace FAT et offre de meilleures performances et sécurité.  

#### ✅ Avantages du NTFS  
✔ **Support des ACL (Listes de Contrôle d’Accès)** : gestion avancée des permissions  
✔ **Journalisation** : suivi des modifications et récupération après incident  
✔ **Compression** : réduction de la taille des fichiers sans perte  
✔ **Chiffrement** : protection des fichiers contre les accès non autorisés  
✔ **Meilleure capacité** : prise en charge de grands volumes et optimisation des performances  

### L'arborescence classique  
📁 **Répertoires système importants** :  
- `C:\$Recycle.Bin` → Corbeille du système de fichiers C:  
- `C:\PerfLogs` → Journaux de performance  
- `C:\Program Files` → Installation des programmes tiers  
- `C:\Program Files (x86)` → Installation des programmes tiers (32 bits)  
- `C:\ProgramData` → Données globales des programmes  
- `C:\Recovery` → Récupération après incident  
- `C:\System Volume Information` → Métadonnées NTFS et points de restauration  
- `C:\Users` → Répertoires personnels des utilisateurs  
- `C:\Windows` → Installation du système  

### Les outils  
#### 🖥️ CLI (Command Line Interface)  
- `Diskpart` → Gestion des disques et partitions  
- `Format` → Création d’un système de fichiers sur une partition  

#### 🖱️ GUI (Graphical User Interface)  
- `diskmgmt.msc` → Gestion des disques  

💡 **Les disques sont automatiquement disponibles à chaque démarrage.**  

### Quelques commandes utiles  

#### 📂 Navigation et affichage  
- `Get-Location` (alias `pwd`) → Affiche le répertoire courant  
- `Get-ChildItem` (alias `ls`) → Liste le contenu d’un répertoire  
- `Get-Content` (alias `cat`) → Affiche le contenu d’un fichier  
- `more` → Affichage paginé  

#### 📄 Gestion des fichiers/dossiers  
- `Copy-Item` (alias `cp`) → Copie un fichier/dossier  
- `Move-Item` (alias `mv`) → Déplace ou renomme un fichier/dossier  
- `Remove-Item` (alias `rm` ou `rmdir`) → Supprime un fichier/dossier  
- `mkdir` → Crée un dossier  

#### 🔍 Comparaison et filtrage  
- `Compare-Object` (alias `diff`) → Compare des objets (fichiers, textes, etc.)  
- `Where-Object` → Filtre des objets selon une condition  

---

## 📌 Gestion des processeurs et mémoire
### Les métadonnées  
Chaque processus possède des informations spécifiques :  
- **Id** → Identifiant du processus (**équivalent PID**)  
- **ParentId** → Identifiant du processus parent (**équivalent PPID**)  
- **UserName** → Nom de l’utilisateur associé (**équivalent UID**)  
- **Group** → Groupe associé (**équivalent GID**)  
- **Handles** → Nombre de handles ouverts par le processus (**assimilable aux fichiers ouverts**)  
- **State** → État actuel du processus (**en cours d’exécution, suspendu, etc.**)  
- **Path** → Chemin d’accès du répertoire de travail du processus  

### Quelques Cmdlets PowerShell  
#### 📋 Gestion des processus  
- `Get-Process` → Récupération d’informations sur les processus  
- `Stop-Process` → Arrêter un processus  
- `Wait-Process` → Attendre la fin d’un processus  
- `Start-Process` → Lancement d’un processus local  
- `Invoke-Command` → Lancement d’une commande locale ou distante  

#### 💻 Informations système  
- `Get-ComputerInfo` → Récupération d’informations matérielles et système  
- `Get-CimInstance` → Récupération d’objets WMI (Windows Management Instrumentation)  

#### ⚙️ Gestion des services  
- `Get-Service` → Liste et état des services  
- `Stop-Service` → Arrêter un service  
- `Start-Service` → Démarrer un service  
- `Suspend-Service` → Mettre un service en pause  
- `Restart-Service` → Redémarrer un service  
- `Set-Service` → Modifier un service  

---

## Gestion des utilisateurs

---

## Active Directory

---

## GPO

---

## Cryptographie

---

## SSH
