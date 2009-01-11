## Configurer un dépôt privé ##

Si vous devez configurer un dépôt privé et que vous désirez faire ça
localement, plutôt que d’utiliser un hébergeur, vous avez plusieurs
solutions.

### Accéder au dépôt par SSH ###

En général, la solution la plus facile est d’utiliser simplement Git à travers ssh.
Si les utilisateurs ont déjà des comptes ssh sur le serveur, vous pouvez
placer le dépôt git n’importe où dans le système auquel ils ont accès
et les laisser accéder à ce dépôt grâce à une simple connexion ssh.
Par exemple, disons que vous avez un dépôt que vous voulez héberger.
Vous pouvez l’exporter comme un dépôt « nu » puis le copier sur votre
serveur avec `scp` comme ceci :
	
	$ git clone --bare /home/user/mondepot/.git /tmp/mondepot.git
	$ scp -r /tmp/mondepot.git monserveur.com:/opt/git/mondepot.git
	
Puis, quelqu’un d’autre avec un compte ssh sur `monserveur.com` peut cloner votre
dépôt via :

	$ git clone myserver.com:/opt/git/myrepo.git

Cette commande leur demandera seulement leur mot de passe ssh ou
leur clé publique, suivant la configuration de l’authentification ssh.

### Accès multi-utilisateurs en utilisant Gitosis ###

Si vous ne voulez pas configurer des comptes différents pour chaque
utilisateur, vous pouvez utiliser un outils nommé Gitosis. Dans
gitosis, il y a un fichier `authorized_keys` qui contient les clés
publiques de toutes les personnes autorisées à accéder au dépôt.
Ensuite tout le monde peut utiliser l’utilisateur `git` pour
publier et récupérer les modifications sur le dépôt.

Pour plus d'informations sur Gitosis :
[Installing and Setting up Gitosis](http://www.urbanpuddle.com/articles/2008/07/11/installing-git-on-a-server-ubuntu-or-debian)
