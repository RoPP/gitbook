## Ignorer des fichiers ##

Un projet générera souvent des fichiers que vous ne voulez pas surveiller
avec git. En général, ce sont des fichiers qui ne servent qu’à la compilation
de programme ou des fichiers temporaires créés par votre éditeur de texte.
Ne pas surveiller ces fichiers revient à ne pas les inclure avec `git-add`.
Mais il devient très vite ennuyant d’avoir tous ces fichiers non-suivis, ils
rendent `git add .` et `git commit -a` pratiquement inutile et ils
se montrent dans chaque sortie de `git status`.

Vous pouvez demander à git d’ignorer certains fichiers en créant un fichier
nommé `.gitignore` dans la racine de votre répertoire de travail. Ce fichier
contiendra ce type d’information :

	# Les ligne commençant par '#' sont des commentaires.
    # Ignorer tous les fichiers nommés foo.txt
    foo.txt
    # Ignorer tous les fichiers html
    *.html
    # à l'exception de foo.html qui est maintenu à la main
    !foo.html
    # Ignorer les objets et les archives
    *.[oa]

Voir linkgit:gitignore[5] pour une explication plus détaillée de la syntaxe.
Vous pouvez aussi placer `.gitignore` dans un autre sous-répertoire de votre
répertoire de travail, ses règles s’appliqueront alors seulement au répertoire
et sous-répertoire de là où il se trouve. Le fichier `.gitignore` peut être
ajouté au dépôt comme n’importe quel autre fichier (lancez juste
`git add .gitignore` and `git commit`, comme d’habitude), cela est utile quand
les chaînes d’exclusion (comme celle pour exclure les fichiers de compilation)
peuvent aussi être utiles aux autres développeurs clonant votre dépôt.

Si vous voulez que la chaîne d’exclusion n’affecte que certains
sous-répertoires (plutôt que tout le dépôt pour un certain projet), vous
devrez alors peut-être mettre cette chaîne dans un fichier de votre dépôt
nommé `.git/info/exclude` ou dans un des fichiers spécifiés par la variable
de configuration `core.excludesfile`. Certaines commandes git peuvent
aussi prendre ces chaînes d’exclusion directement comme argument de la ligne de
commande. Voir linkgit:gitignore[5] pour plus de détails.
