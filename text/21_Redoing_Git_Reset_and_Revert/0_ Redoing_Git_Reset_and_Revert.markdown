## Réparation avec git — Reset, checkout et revert ##

Git fournit plusieurs méthodes pour réparer vos erreurs durant
votre développement. La bonne méthode dépend
si vous avez committé ou non votre erreur et si elle a été
committée, si cette erreur a déjà été récupérée par un autre
développeur.

### Réparer une erreur non-committée ###

Si vous vous êtes embrouillé dans votre répertoire de travail, mais
que vous n’avez pas encore committé vos erreurs, vous pouvez retrouver
l’état dans lequel était votre répertoire après le dernier
commit en utilisant :

    $ git reset --hard HEAD

Cela effacera toutes les modifications que vous avez ajouté à l’index git
ainsi que les changements qui sont présents dans votre répertoire de travail
mais qui n’ont pas été ajoutés à l’index. En d’autres termes, après cette
commande, le résultat de `git diff` et `git diff --cached` sera vide.

Si vous ne voulez restaurer qu’un seul fichier, par exemple `hello.rb`,
utiliser plutôt linkgit:git-checkout[1] :

    $ git checkout -- hello.rb
    $ git checkout HEAD hello.rb

La première commande restaure `hello.rb` à la version de l’index 
afin que `git diff hello.rb` ne retourne aucune différence. La seconde
commande restaurera `hello.rb` à la version de la révision HEAD afin que
`git diff hello.rb` et `git diff --cached hello.rb` ne retourne aucune
différence.

### Réparer une erreur committée ###

Si vous avez déjà committé ce que vous n’auriez pas du, il y a deux façons
fondamentalement différentes de régler le problème :

1. Vous pouvez créer un nouveau commit qui annule les changements
	du dernier commit. C’est la manière correcte de s’y prendre si
	votre erreur est déjà publique.

2. Vous pouvez revenir en arrière et modifier l’ancien commit. Vous ne
	devriez jamais faire ça si vous avez déjà rendu l’historique publique.
	Git n’est pas conçu pour que l’historique d’un projet change et ne
	peut pas effectuer correctement des merges répétés sur depuis une branche
	qui a vu son historique changer.

#### Réparer une erreur sur un nouveau commit ####

Il est facile de créer un nouveau commit qui annule les changements d’un
commit précédent. Utilisez la commande linkgit:git-revert[1] avec la référence
du mauvais commit, par exemple, pour revenir au commit le plus récent :

    $ git revert HEAD

Cela créera un nouveau commit qui annule les changements dans HEAD.
Vous pourrez éditer le message de ce nouveau commit.

Vous pouvez aussi revenir sur des changements plus anciens, par
exemple, sur l’avant-dernier changement :

    $ git revert HEAD^

Dans ce cas, git essayera d’annuler l’ancien changement en gardant
intactes les modifications faites depuis. Si plus d’un changement
se superpose sur les changements à annuler, vous aurez à régler les
conflits manuellement, de la même façon que quand vous réglez un merge.

#### Réparer une erreur en modifiant le commit ####

Si vous venez de committer quelque chose mais que vous vous rendez compte
que vous devez réparer ce commit, les versions récentes de
linkgit:git-commit[1] vous donnent accès à l’option **--amend** qui
demande à git de remplacer le commit de HEAD par un autre, basé sur
le contenu actuel de l’index. Cela vous donne l’opportunité d’ajouter
de fichiers que vous avez oubliés ou de corriger des erreurs de typo
dans le message du commit, avant de publier les changements pour les
autre développeurs.

Si vous trouvez une erreur dans un ancien commit, mais que vous ne l’avez
toujours pas publié, utilisez le mode interactif de linkgit:git-rebase[1],
avec `git rebase -i` en marquant les changements qui doivent être corrigés
avec **edit**. Cela vous permettra de modifier le commit pendant le
processus de recombinaison.
