# Travail Pratique 1

## Énoncé

Le but de ce TP va être dans une première partie de découvrir l'interface de GitHub (le site de gestion de projet open source le plus populaire), afin de récupérer le TP. Dans une seconde partie nous effectuerons plusieurs commandes afin de se familiariser avec Git.

## Première Partie
Tout d'abord, il faut se rendre à l'adresse [github.com/etiennebatise/Git-Training](http://github.com/etiennebatise/Git-Training). Si vous n'avez pas de compte sur GitHub, créez votre compte utilisateur puis revenez sur la page indiquée et cliquez sur le bouton **Fork**. Cela va copier entièrement ce dépot et le mettre dans votre liste de dépôt, ainsi vous pourrez effectuer toutes les modifications voulues sans que le propriétaire initiale ne soit embêté. L'opération va prendre quelques secondes.

Une fois le _fork_ terminée, retournez sur votre page personnelle et cliquez sur le dépot et copiez l'URL. 

Enfin, sur votre machine, ouvrez un terminal et lancer la commande :

```
git clone <l'url copiée>
```

Attendez que le téléchargement soit terminé. Voilà vous avez cloné votre premier dépôt. 


## Deuxième Partie
Vous allez devoir effectuez quelques actions très simples :

1. Créez un fichier _1.file_
2. Observez le résultat de la commande `git status`
3. Indiquez à Git de suivre les modification du fichier.  
4. Observez de nouveau le résultat de la commande `git status`
5. Commitez l'ajout du fichier avec le message :
    _Ajout du fichier 1.file_
6. Constater que le fichier n'est pas présent depuis l'interface de Github
7. Mettre la modification en ligne.


## Solution
1. `touch 1.file`
2. `git status`
3. `git add 1.file`
4. `git status`
5. `git commit -m "Ajout du fichier 1.file"`
6. Constatez que le fichier n'est pas présent depuis l'interface de Github
7. `git push`


# Travail Pratique 2
Le but de ce TP va être dans une première partie de découvrir l'interface de GitHub (le site de gestion de projet open source le plus populaire), afin de récupérer le TP. Dans une seconde partie nous effectuerons plusieurs commandes afin de se familiariser avec Git.

## Énoncé
Le but de ce TP va être de manipuler les branches sur le dépôt local puis dans une seconde partie de découvrir l'interface de _pull request_ qui est l'un des fonctionnalité les plus importantes de GitHub.

## Première Partie
Vous allez devoir reprendre le dépôt précédent. 

1. Créez une nouvelle branche nommée _ma-premiere-branche_
2. Dans cette nouvelle branche 
3. Modifiez le fichier _1.file_ (rajouter un lorem-ipsum)
4. Créer un fichier _2.file_
5. Validez ces modifications
6. Basculez sur la branche _master_. Effectuez une modification dans le fichier _1.file_. 
7. Faites en sorte de récupérer les modifications des _master_ sur _ma-premiere-branche_, réglez les eventuels conflits.
8. Enfin, faites en sorte que la branche _ma-premiere-branche_ soit visible depuis GitHub.

## Deuxième Partie
Si vous avez correctement fini la première partie, vous devez vous rendre sur Github. Allez dans votre compte, puis dans vos dépôt et enfin dans le dépôt Travail-Pratique-Avec-Git.

Vous devriez voir un bouton vert à gauche, en dessous des statistiques du dépôts. Cliquez sur ce bouton. Cliquez sur le bouton _Compare_ et choisissez _ma-premiere-branche_, puis validez en cliquant sur le bouton _Compare pull request_. Observez les différente options proposées par l'interface. Expérimentez.

Une fois que vous avez fini de découvrir cette nouvelle interface, validez votre pull request. Enfin sur votre dépôt local, mettez à jou le dépôt et constatez les changements.

## Solution
1. `git branch ma-premiere-branche`
2. `git checkout ma-premiere-branche`
3. `echo "Random stuff" >> 1.file`
4. `touch 2.file`
5. `git commit -a -m "un commit pas très intelligent"`
6. `git checkout master && echo "une modification" >> 1.file`
7. `git checkout ma-premiere-branche && git merge master`
8. `git branch -u origin/ma-premiere-branche`
9. `git push`

