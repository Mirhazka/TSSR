# Exploiter des serveurs Windows et un domaine ActiveDirectory
## La gestion du stockage
### 📌 L'abstraction
- Chemin absolu : `C:\Users\wilder` ou `C:\Windows\system32\notepad.exe`
- Chemin relatif : `.\wilder` ou `.\notepad.exe`
- La variable d'environnement **path** : `$env:path`

### 📌 Les systèmes de fichier
#### NTFS (New Technology File System)

Le NTFS (New Technology File System) est un système de fichiers développé par Microsoft, conçu pour être utilisé sur les systèmes d'exploitation Windows, à partir de Windows NT. Il remplace le système de fichiers FAT (File Allocation Table) utilisé dans les versions antérieures de Windows. NTFS offre des performances et une sécurité accrues par rapport à FAT, et il est devenu le standard pour les systèmes Windows modernes.

#### Avantages du NTFS

- **Support des ACL (Listes de Contrôle d'Accès) avancées** : Permet une gestion fine des permissions et des droits d'accès pour chaque fichier et dossier.
- **Journalisation** : Enregistre les modifications sur les fichiers et les volumes, ce qui permet de récupérer les données en cas de panne du système.
- **Compression** : Permet de réduire la taille des fichiers sans perdre de données, ce qui permet d’économiser de l’espace disque.
- **Chiffrement** : Protéger les données en chiffrant les fichiers et les dossiers pour assurer leur sécurité en cas de vol ou d'accès non autorisé.
- **Meilleures capacités** : Prend en charge des volumes de plus grande taille, un nombre de fichiers supérieur, et permet une gestion plus efficace des systèmes de fichiers avec des disques durs modernes.

### 📌 L'arborescence classique
- `C:\$Recycle.Bin` : corbeille du système de fichiers C:
- `C:\PerfLogs` : journaux de performance
- `C:\Program Files` : installation des programmes tiers
- `C:\Program Files (x86)` : installation des programmes tiers (32 bits)
- `C:\ProgramData` : données globales des programmes
- `C:\Recovery` : récupération après incident
- `C:\System Volume Information` : métadonnées NTFS et points de restauration
- `C:\Users` : répertoire personnel des utilisateurs
- `C:\Windows` : installation du système

### 📌 Les outils  

#### CLI :  
- `Diskpart` : gestion des disques et partitions  
- `Format` : création d'un système de fichiers sur une partition  

#### GUI :  
- `diskmgmt.msc` : gestion de disques  

💡 **Les disques sont automatiquement disponibles à chaque démarrage.**  

### 📌 Quelques commandes utiles  

- `Get-Location` (alias `pwd`) : affiche le répertoire courant  
- `Get-ChildItem` (alias `ls`) : affiche (et cherche) le contenu d'un répertoire  
- `Get-Content` (alias `cat`) : affiche un fichier  
- `more` : affichage paginé  
- `Copy-Item` (alias `cp`) : copie un fichier/dossier  
- `Move-Item` (alias `mv`) : déplace/renomme un fichier/dossier  
- `Remove-Item` (alias `rm` et `rmdir`) : supprime un fichier/dossier  
- `mkdir` : crée un dossier  
- `Compare-Object` (alias `diff`) : affiche les différences  
- `Where-Object` : filtre  

---

## Stockage avancé

---

## Gestion processeurs et mémoire

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
