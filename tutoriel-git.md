# Tutoriel Git

## Introduction

Git est un logiciel de versionnement de code source développé par Linux Torvalds et utilisé par de nombreuses entreprises du secteur informatique. C'est un outil très pratique et très puissant permettant d'avoir un projet propre et de collaborer sur un même projet avec de nombreux autres développeurs.


## La base
    
Le fonctionnement du git est le même que celui de nombreux autres gestionnaires de versions: le code source partagé se trouve sur une **dépôt** principal, généralement sur un serveur dédié et accessible en ligne et chaque collaborateur / développeur télécharge une copie de ce dépôt sur sa machine et travail ainsi indépendamment des autres. 

### Création d'un dépôt
Généralement, si l'on utilise un fournisseur de dépôt  (ou _repo_ en anglais) tel que _Github_, _BitBucket_ cette opération est facultative. Dans le cas contraire, il faut créer le dépôt :
```
git init
```
Pour vérifier que tout se passe bien, on peut vérifier qu'il y a bien un fichier **.git** dans le répertoire. 


### Clonage du dépôt
L'action de récupérer pour la première fois le code source disponible sur le dépôt principal s'appelle le **clonage**. Si le dépôt est accessible via une URL tel que _mondepot.monNomDeDomaine.tld_, il suffit de rentrer la commande :
```
git clone http://mondepot.monNomDeDomaine.tld
```
Suite à cette commande, on vous demandera généralement votre login et mot de passe en fonction de la façon dont le dépôt à été configuré. 


### État du dépôt 
Afin d'utiliser correctement git, il est nécessaire de voir régulièrement l'état du dépôt. Pour l'instant cette description est certainement abstraite mais cette commande est sans doute la plus utilisée par les utilisateurs de git :
```
git status
```
Bon nombre d'informations vont s'afficher, il est important de bien les lire car git est relativement intelligent et vous donnera des indications très utiles en cas de problème.


### Configuration personnelle
Avant de rentrer dans le vif du sujet, il est important de configurer un peu le dépot.
* Configuration du nom d'utilisateur :
```
git config (--global) user.name <le nom d'utilisateur>
```

* Configuration de l'email utilisateur :
```
git config (--global) user.email <email utilisateur>
```

* Activation de la couleur dans git :
```
git config (--global) color.ui true
```


### Suivi des fichiers
Lorsqu'on crée un fichier dans le code source, il n'est pas automatiquement suivi. Il faut dire à git de suivre ce fichier, cela signifie qu'on l'ajoute au dépôt :
```
git add mon_nouveau_fichier
```
Avec un petit coup de `git status`, on remarque que le fichier est désormais suivi.


### Validation d'une modification
Lorsqu'on travaille sur un fichier, on modifie l'état du dépôt. Ainsi, lorsqu'on termine une modification, il faut 2 étapes afin de **valider** la modification. 

Exemple :

1. On modifie le fichier *mon_fichier*
2. On voit grâce à `git status` que le fichier à été modifié. Cependant la modification n'est pas suivie.
3. On indique à git qu'il faut suivre la modification :
```
git add mon_fichier
```

4. On indique à git que ces modification sont valides. 
```
git commit -m "Corrections des erreurs sur le fichier mon_fichier"
```

L'option **-m** permet d'écrire le message de _commit_ directement dans la commande comme dans l'exemple précédent. Si l'option n'est pas présente, git va ouvrir l'éditeur de texte par défaut, il suffira d'écrire votre texte, de sauvegarder puis de fermer la fenêtre. 

À cette étape, la commande `git status` devrait vous dire que vous êtes en avance de 1 commit. Cela signifie que l'opération s'est bien passée.


### Mise à jour du dépôt local
Lorsqu'on travaille sur un dépôt en ligne, il est important de s'assurer que la version du dépôt sur laquelle on travaille est toujours à jours. 

Version en ligne :
---A---B---C---

Version locale
---A---B(+modifications)

Ici, il manque la mise à jour C à notre version locale, il faut donc la récupérer :
```
git pull
```

Il est important pour la suite de savoir que cette commande est en fait un raccourci pour :
```
git fetch
git merge
```

La première permet de télécharger les modifications, la seconde permet de fusionner ces modifications avec les nôtres .

Lorsqu'on travaille à plusieurs sur un dépôt en ligne, il est important de faire en sorte que nos modifications n'entre pas en **conflit** avec les modifications des autres. En effet, si 2 développeurs écrivent sur la même ligne du même fichier, il y aura un conflit et git n'est pas capable de régler ce problème tout seul. Généralement, les conflits apparaissent après un `git merge` (et donc après un `git pull`).

Lorsqu'il y a un conflit, il est d'usage de se référer à un `git status` pour savoir quels fichiers provoquent des conflits. Il faudra ensuite ouvrir ces fichiers et les corriger. 


### Mise à jour du dépôt en ligne
Enfin pour finir cette partie sur les bases de git, nous allons envoyer nos modifications locales sur le dépôt en ligne. Cette étape ne peut avoir lieu que lorsqu'on est bien sûr que le code source fonctionne correctement (tous les tests au vert), que l'on a validé nos modifications (commits) et que l'on a en local la dernière version possible (pull). Il est évident qu'il faut s'assurer que le code fonctionne toujours (tests) après un `git merge`. La commande permettant de mettre sont code en ligne est 
```
git push
```

Généralement, git vous demandera votre _login_ et votre _mot de passe_ pour s'assurer que vous avez le droit de modifier ce dépôt. 

### Travail pratique
À ce point, il est intéressant de suivre la première partie du tutoriel situé dans le fichier tutoriel.md.

## Les branches

L'une des fonctionnalités avancés de git est sa gestion des _branches_. Sans le savoir vous avez déjà utilisées les branches, si vous avez suivi le tp. En effet, sur le dépôt en ligne la branche principale s'appelle _origin_, et sur le dépôt local, la branche principale s'appelle _master_. Lorsqu'on fait un `git fetch`, on met à jour _origin_ en local. Lorsqu'on fait un `git merge`, on fusionne la branche _origin_ et la branche _master_. Cela fait partie de la partie de Git dont on s'occupe rarement. Cependant les branche offrent de nombreuses possibilités afin de travailler proprement à plusieurs sans déranger le travail des autres.

### Création d'une branche
Créer une branche est très simple. Il suffit de rentrer la commande :
```
git branch ma_nouvelle_branche
```

### Changer de branche
Lorsqu'on crée une branche, git ne bascule pas automatiquement dessus, il faut lui dire :
```
git checkout ma_nouvelle_branche
```

Ensuite, on peut effectuer les mêmes commandes que l'on a vue dans la première partie.

Exemple :
Imaginons que nous soyons sur la branche _master_. Nous avons fait deux _commits_ que l'on va appeler _A_ et _B_. Ensuite nous allons créer une branche _nouvelleBranche_ et nous allons faire deux nouveaux _commits_ que l'on va appeler _C_ et _D_. Enfin après cette étape nous allons faire un _commit_ E sur master. À la fin de cette opération, le dépôt devrait ressembler à cela :

```
(nouvelleBranche)      C---D
                      /
(master)      ---A---B---E
```

Les deux étapes précédentes peuvent être synthétisées en une seule :
```
git checkout -b nouvelleBranche
```

### Récupérer des modifications
Admettons que nous sommes dans le cas précédent, nous voulons mettre à jours _nouvelleBranche_ pour travailler avec la modification _E_. Il suffit de se placer sur la nouvelle branche et d'utiliser la commande `merge` :
```
git checkout nouvelleBranche
git merge master
```

Le dépôt devrait ressembler désormais à ceci :

```
(nouvelleBranche)      C---D---E
                      /      /
(master)      ---A---B------E
```

#### Les conflits
Vous vous souvenez de ce que je vous avais dit sur **git merge** ? C'est à cette étape que les conflits apparaissent. Si vous lisez correctement le message que vous renverra Git, vous verrez lorsqu'il y a un problème. Généralement, après chaque étape `git status` vous donnera des indications sur les fichiers où il y a des conflits. Dans ce fichiers vous verrez ce que Git n'auras pas su résoudre :

```
Random line that is good

<<<<< your modification delimiter
random modification made be you
========== (SEPARATOR)
modification made be the others
>>>>>> others modification delimiter

Random line that is also good
```

#### Attention ! Gare à l'admin

Maintenant vous devez commencer à comprendre que `git merge` est une commande très importante. Le script suivant présente ce que vous ne devez jamais faire si vous n'êtes pas administrateur du dépôt.

```
git checkout master
git merge une-branche
```


Ici, on bascule sur la branche _master_ et on fusionne la branche actuelle avec les modifications effectuées sur _une-branche_. Ainsi, on fait ce qu'on appelle une mise en production puisque la branche **master** contient généralement le produit fini. Vous ne devez donc jamais faire cela sans l'autorisation de l'autorisation de l'administrateur.

La solution est de mettre votre branche en ligne, afin qu'un responsable puisse faire une revue de votre code et le valider :
```
git checkout une-branche

git branch -u origin/une-branche
```

Un façon de créer un branche qui va automatiquement se mettre à jour avec le dépôt (plus précisément la branche _origin_) est la suivante :
```
git branch --track origin/nouvelleBranche
```
La commande précédente est aussi valable pour l'administrateur qui doit récupérer une branche disponible sur le dépôt en ligne sur sa version locale.

### Travail Pratique
À ce point, il est intéressant de suivre la seconde partie du tutoriel situé dans le fichier tutoriel.md.

## Fonctionnalités avancées
### Git ++
À ce niveau, je vous demande de prendre le temps de regarder cette video : [https://www.youtube.com/watch?v=rt-9mPaYtKo](https://www.youtube.com/watch?v=rt-9mPaYtKo)

### Convention de message de commit
```
<type> (<scope>) : <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<FOOTER>
```

* **type** : Quoi ?
     + _feat_ (fonctionnalités) 
     + _fix_ (resolution bug) 
     + _test_ 
     + _docs_ 
     + _refactor_(changement) 
     + _style_ (changement de format de fichier ou de convention de texte)
     + _chore_ (externes au projet, config etc ..)

* **scope** : Où ?
* **subject** : Pourquoi ? Très important. Message orienté utilisateur. Terme non technique.
* **body** : Comment ? Contexte et détails.
* **footer** : Lien(s) vers un ticket par exemple.

_Note_ : Les informations suivantes sont tirées du manuel. Elles ont simplement pour but de vous familiariser avec, de vous montrer quelques commandes utiles.

### GIT REBASE
Si vous avez regardé la vidéo, alors, vous avez vu que la commande `git rebase` est très puissante et pratique pour manipuler son dépôt et avoir un bel historique. L'un des cas pratique est le suivant : Imaginons que nous travaillons sur un branche _ma-feature_ qui doit être implémentée sur la version de dev : _dev-branch_. Vous faites plusieurs commits qui implémente correctement votre fonctionnalité. Cependant, pendant que vous codiez, un autre développeur à terminé sont développement, et sa _pull-request_ a été accepté. Votre branche n'est donc plus à jour. Vous avez donc 2 choix : le `git merge` ou le `git rebase`.

Le git merge va créer un nouveau commit pour indiquez que le données ont été rapatriées.
```
git checkout ma-feature
git merge master

       A---B---C ma-feature                    A---B---C---M ma-feature   
      /                           ==>        /           /
 D---E---F---G dev-branch               D---E---F-------G dev-branch
```

On constate qu'on crée un commit de merge. Ce n'est pas très jolie et cela mène à avoir un historique chaotique lorsqu'on fait beaucoup de `git merge`.


À l'inverse, le `git rebase`, va changer le commit à partir duquel vous avez créé votre branche pour prendre le plus récent. Dans le cas précédent :
```
git checkout ma-feature
git merge master

       A---B---C ma-feature                            A---B---C ma-feature   
      /                           ==>                /           
 D---E---F---G dev-branch               D---E---F---G dev-branch
```

Cette solution est idéale pour avoir un historique de code propre. Cependant, il est important de savoir quand ne pas l'utiliser. Il ne faut pas utiliser de `git rebase` lorsque vous êtes plusieurs à développer sur la même branche. C'est donc idéal lorsque vous travailler seul sur votre feature. À l'inverse des branche comme _dev_ ou _master_ doivent être traités avec des merges. Sémantique cela est plus correcte car ont fusionne bien une branche dans une autre pour obtenir ses modifications et on rebase une branche par rapport à une autre pour partir de la dernière version.

Je vous laisse le soin de vous renseigner sur la commande `git rebase -i`. C'est une commande très pratique qui permet de réordonner les commits avant de faire une `git push`. Je vous conseil vraiment de regarder la partie de la vidéo qui concerne `git rebase -i`.

### GIT STASH
Cette commande est très pratique dans un cas très particulier. Imaginons que vous être en train de travailler sur votre feature dans votre branche _ma-feature_ et vous n'avez pas encore ajouté vos modifications au suivi du dépôt (vous n'avez pas fait de `git add`). À ce moment, votre boss ou votre chef dev vous demande de corriger un bug sur la branche en production ou sur la branche de dev. Vous ne voulez pas perdre votre travail, la solution est la commande `git stash`. 

Cette commande va garder en tête toutes vos modification et remettre le dépôt dans l'état précédent vos modifications. Vous pouvez donc changer de branche, faire la modification importante demandée par votre boss, et commiter. Mais comment retrouver vos modification ? Il faut retourner sur la branche en question et exécuter : `git stash pop`. Cette commande va remettre le dépôt dans l'état juste avant le git stash.


### GIT RESET
Lorsque vous travaillez avec Git, vous travaillez sur une version du dépôt. Cette version est généralement pointé par le dernier commit que vous avez fait. Ce pointeur s'appelle **HEAD**, c'est le commit sur lequel vous vous basez pour travaillez. Il est donc possible de se balader sur l'arborescence des commits. 

Il existe une symbolique qui vient avec **HEAD** :

* _HEAD_ : Représente le commit sur lequel on se base.
* _HEAD~_ : Représente le niveau précédent dans l'arborescence. Dans un contexte simple, c'est le commit précédent.
* _HEAD^_ : Représente le premier parent dans  le niveau précédent (Un commit peut avoir plusieurs parents).
* _HEAD~2^3_ : Représente le 3eme parent du commit au niveau -2 (grand parent) de **HEAD**.

```
G   H   I   J
 \ /     \ /
  D   E   F
   \  |  / \
    \ | /   |
     \|/    |
      B     C
       \   /
        \ /
         A
         
A =      = A^0
B = A^   = A^1     = A~1
C = A^2  = A^2
D = A^^  = A^1^1   = A~2
E = B^2  = A^^2
F = B^3  = A^^3
G = A^^^ = A^1^1^1 = A~3
H = D^2  = B^^2    = A^^^2  = A~2^2
I = F^   = B^3^    = A^^3^
J = F^2  = B^3^2   = A^^3^2
```

Il existe des options intéressantes pour `git reset` :

* `--soft` : Ne touche pas aux fichiers mais change la valeur de **HEAD**.
* `--hard` : Annule toutes les modifications faites.

Exemple d'utilisation de `git reset` :

Vous venez de faire un commit, et vous vous apercevez que vous avez oublié un fichier :
```
git commit ...   (Le commit malheureux)
git reset --soft HEAD^ (On retourne au commit précédent sans annuler les modifications)
edit (Mes modifications)
git add . (On redit à Git de suivre les bon fichiers)
git commit -m "Un nouveau message"
```

### Conclusion
Je vous invite fortement à prendre le temps de lire les pages du manuel pour comprendre mieux le fonctionnement de chaque commande, de trouver les options qui pourront vous simplifier la vie. 

Enfin pour comprendre les différentes étapes que suivent les fichiers avec Git je vous invite également à lire cette page web : [http://stackoverflow.com/questions/3689838/difference-between-head-working-tree-index-in-git](http://stackoverflow.com/questions/3689838/difference-between-head-working-tree-index-in-git)
