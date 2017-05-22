Cette cheat sheet est basée sur la version disponible sur [https://www.git-tower.com/blog/git-cheat-sheet/]

### CREATE

**Cloner un dépot existant**

`git clone ssh://user@domain.com/repo.git`

**Initialiser un nouveau dépot en local**

`git init` (dans le dossier du dépot)

### Changements locals

**Suivre les changement dans l'espace de travail**
`git status`

**Suivre les changements dans les fichiers**
`git diff`

**Ajouter tous les changement dans le prochain commit**
`git add .`

**N'ajouter que certaines modifications dans un fichier dans le prochain commit**
`git add -p <file>`

**Commit toutes les modification** (sans avoir besoin de faire `git add .`)
`git commit -a`

**Commit les changement**
`git commit`

**Changer le dernier commit**
`git commit --amend`

### Historique des commits
**Voir tous les commits en partant du plus récent**
`git log`

**Voir les logs pour un fichier spécifique**
`git log -p <file>`

**Voir qui a changer quoi et quand dans un fichier**
`git blame <file>`

### Branches & Tags
**Lister toutes les branches existantes**
`git branch -av`

**Changer de branche**
`git checkout <branche>`

**Créer une nouvelle branche basée sur le HEAD actuel**
`git branch <new-branch>`

**Créer une branche de tracking basée sur une autre branche**
git checkout --track <remote/branch>`

**Supprimer une branche locale**
`git branch -d <branch>`

**Marquer le commit courant avec un tag**
`git tag <tag-name>`

### Update & Publish
**Lister tous les dépots trackés par votre workspace**
`git remote -v`

**Voir les informations sur un remote (dépot distant)**
`git remote show <remote>`

**Ajouter un nouveau répertoire distant (ex. origin)**
`git remote add <shortname> <url>`

**Télécharger tous les changement depuis un répertoire distant, mais ne pas les intégrer dans HEAD**
`git fetch <remote>`

**Télécharger une branche distante et directement merge dans HEAD**
`git fetch <remote> <branch>`

**Télécharger une branche distante et directement merge dans HEAD**
`git pull <remote> <branch>`

**Publier des changements sur une branche distante**
`git push <remote> <branch>`

**Supprimer une branche distante**
`git branch -dr <remote> <branch>`

**Publier des tags**
`git push --tags`

### Merge & Rebase
Merge : Fusionner des branches
Rebase : Mettre à jour une branche à partir d'une autre

**Merge une branche dans le HEAD courant**
`git merge <branch>`

**Rebase la HEAD courante à partir d'une branche**
`git rebase <branch>`
-!- L'option -i (pour interactive) est très intéressante, elle permet d'effectuer un rebase commit par commit pour fusionner ces derniers entre eux ou encore en réécrire pour qu'il soit plus explicite. On obtient ainsi un historique plus propre.

**Anuler un rebase en cours**
Lorsque vous n'êtes pas sûr d'être en mesure de résoudre un conflit.
`git rebase --abort`

**Poursuivre un rebase après la résolution d'un conflit**
`git rebase --continue`

### Revenir en arrière (en maitrisant)

**Supprimer tous les changements en local dans l'espace de travail**
`git reset --hard HEAD`

**Supprimer tous les changements en local dans un fichier spécifique**
`git reset --hard HEAD <file>`

**Inverser un commit (en produisant un nouveau commit avec les changements inverses)**
`git revert <commit>`

**Reset votre pointeur HEAD sur un commit antérieur**
**.. et supprimer tous les changements depuis lors**
`git reset --hard <commit>`

**.. et conserver tous les changements en non commités mais en perdant le travail local**
`git reset <commit>`

**.. et conserver tout**
`git revert --keep <commit>`












