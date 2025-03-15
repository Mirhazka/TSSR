
# Automatiser des tâches à l'aide de scripts 🛠️

## Les Shells 💻

Le **Shell** est un interpréteur de commandes qui permet de communiquer avec le système d'exploitation. Il peut être utilisé pour automatiser des tâches, manipuler des fichiers et exécuter des commandes système.

### Types de Shells :
- **Bash** : Le Bourne Again Shell, utilisé principalement sur Linux.
- **Zsh** : Un autre Shell populaire sur Linux, offrant plus de fonctionnalités avancées.
- **PowerShell** : Le Shell de Microsoft pour Windows, avec une syntaxe orientée objets.

Les Shells permettent de créer des scripts pour automatiser des tâches, effectuer des recherches dans des fichiers, et gérer des processus.

---

## Git & GitHub 🌍

**Git** est un système de contrôle de version, et **GitHub** est une plateforme basée sur Git pour la gestion de projets et la collaboration.

### Commandes Git de base :
- `git init` : Initialiser un dépôt Git.
- `git clone <url>` : Cloner un dépôt distant.
- `git add <fichier>` : Ajouter un fichier à l'index pour le prochain commit.
- `git commit -m "message"` : Sauvegarder les modifications avec un message.
- `git push origin main` : Envoyer les modifications vers un dépôt distant.

### Exemple de Workflow Git :
1. Initialiser un dépôt :
   ```bash
   git init
   ```

2. Ajouter un fichier et effectuer un commit :
   ```bash
   git add script.sh
   git commit -m "Ajout du script d'automatisation"
   ```

3. Pousser vers GitHub :
   ```bash
   git push origin main
   ```

**GitHub** permet de collaborer facilement avec des équipes, de gérer des versions de scripts et de suivre l'évolution des projets.

---

## Scripting Bash 🐚

Le **Bash** est utilisé pour automatiser des tâches sur des systèmes Unix-like. Voici quelques commandes utiles en Bash :

### Commandes de base :
- `ls` : Liste les fichiers et répertoires.
- `cd` : Change de répertoire.
- `echo` : Affiche une ligne de texte.
- `cp` : Copie un fichier.
- `rm` : Supprime un fichier.
- `chmod` : Change les permissions d'un fichier.

### Exemple de script Bash :
```bash
#!/bin/bash

# Script de sauvegarde
echo "Début de la sauvegarde..." 
tar -czf /backup/sauvegarde_$(date +'%Y%m%d').tar.gz /home/user/documents
echo "Sauvegarde terminée."
```

**Explication** :
- `tar -czf` : Crée une archive compressée.
- `$(date +'%Y%m%d')` : Ajoute la date actuelle à l'archive.
- Le script réalise une sauvegarde des documents et affiche des messages avant et après l'exécution.

---

## Scripting PowerShell ⚡

Le **PowerShell** est principalement utilisé sur Windows. Il combine des commandes classiques et des objets .NET pour une gestion avancée du système.

### Commandes PowerShell de base :
- `Get-Process` : Affiche les processus en cours.
- `Set-ExecutionPolicy` : Modifie la politique d'exécution des scripts.
- `Get-Content` : Lit le contenu d'un fichier.
- `New-Item` : Crée un nouvel élément (fichier, répertoire).

### Exemple de script PowerShell :
```powershell
# Script PowerShell de sauvegarde
$source = "C:\Users\Utilisateur\Documents"
$destination = "D:\Backup\Documents_$((Get-Date).ToString('yyyyMMdd')).zip"
Write-Host "Début de la sauvegarde..."
Compress-Archive -Path $source -DestinationPath $destination
Write-Host "Sauvegarde terminée."
```

**Explication** :
- `Compress-Archive` : Comprime un dossier ou fichier en archive ZIP.
- `Get-Date` : Obtient la date actuelle pour l'inclure dans le nom du fichier de sauvegarde.

---

## Conclusion 🚀

L'automatisation des tâches avec des scripts permet de gagner du temps, d'éviter les erreurs humaines et de rendre les processus plus efficaces. Que ce soit en utilisant des Shells comme Bash ou PowerShell, ou des outils de gestion de version comme Git et GitHub, il est essentiel de comprendre leur utilisation pour gérer les systèmes et les infrastructures de manière optimale.

---

🔗 **Références** :
- [Documentation Git](https://git-scm.com/doc)
- [Documentation Bash](https://www.gnu.org/software/bash/manual/)
- [Documentation PowerShell](https://docs.microsoft.com/en-us/powershell/)
