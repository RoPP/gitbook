### L’objet blob ###

Un « blob » stocke généralement le contenu d’un fichier.

[fig:object-blob]

Vous pouvez utiliser linkgit:git-show[1] pour examiner le contenu de
n’importe quel blob. Si nous avons le SHA1 d’un blob, nous pouvons l’examiner
comme ceci :

    $ git show 6ff87c4664

     Note that the only valid version of the GPL as far as this project
     is concerned is _this_ particular version of the license (ie v2, not
     v2.2 or v3.x or whatever), unless explicitly otherwise stated.
    ...

Un « blob » n’est rien de plus qu’un morceau de données binaires. Il ne fait
référence à rien et n’a aucun attribut, même pas un nom de fichier.

Puisque le « blob » est entièrement défini par ses données, si deux fichiers dans
un répertoire (ou dans différentes versions du dépôt) ont le même contenu,
ils partageront alors le même objet blob. Cet objet est totalement
indépendant de l’endroit où il se trouve dans la hiérarchie des dossiers
et renommer un fichier ne change pas l’objet auquel ce fichier est
associé.

### L’objet tree ###

Un « tree » est un simple objet qui contient une liste de pointeurs vers des
« blobs » et d’autres « trees » — il représente généralement le contenu d’un
répertoire ou d’un sous-répertoire.

[fig:object-tree]

La commande polyvalente linkgit:git-show[1] peut aussi être utilisée pour
examiner un objet « tree », mais linkgit:git-ls-tree[1] vous donnera plus de
détails. Si nous avons le SHA1 d’un « tree », nous pouvons le détailler comme ceci :

    $ git ls-tree fb3a8bdd0ce
    100644 blob 63c918c667fa005ff12ad89437f2fdc80926e21c    .gitignore
    100644 blob 5529b198e8d14decbe4ad99db3f7fb632de0439d    .mailmap
    100644 blob 6ff87c4664981e4397625791c8ea3bbb5f2279a3    COPYING
    040000 tree 2fb783e477100ce076f6bf57e4a6f026013dc745    Documentation
    100755 blob 3c0032cec592a765692234f1cba47dfdcc3a9200    GIT-VERSION-GEN
    100644 blob 289b046a443c0647624607d471289b2c7dcd470b    INSTALL
    100644 blob 4eb463797adc693dc168b926b6932ff53f17d0b1    Makefile
    100644 blob 548142c327a6790ff8821d67c2ee1eff7a656b52    README
    ...

Comme vous pouvez le voir, un objet « tree » contient une liste d’entrées,
chacune avec un mode, un type d’objet, un nom SHA1, un nom, le tout trié
à partir des noms. L’objet « tree » représente le contenu d’un unique dossier.

Un objet référencé par un « tree » peut être un « blob » représentant le contenu
d’un fichier ou un autre « tree » représentant le contenu d’un sous-répertoire.
Puisque les « trees » et les « blobs », comme les autres objets, sont nommés par le
hash SHA1 de leur contenu, deux « trees » ont le même nom SHA1 si, et seulement si,
leur contenu (en incluant récursivement le contenu de tous les 
sous-répertoires) est identique. Cela permet à git de déterminer rapidement
les différences entre deux objets « trees » associés puisqu'il peut ignorer les
entrées avec le même nom d’objet.

Note : en présence de sous-modules, les « trees » peuvent aussi contenir des
commits comme entrées. Voir la section **Sous-Modules**.

Notez que tous les fichiers ont le mode 644 ou 755 : git ne tient compte que
du bit exécutable.
