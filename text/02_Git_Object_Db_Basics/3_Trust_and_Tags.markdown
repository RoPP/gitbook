
### L’objet tag ###

[fig:object-tag]

Un objet « tag » contient un nom d’objet (simplement nommé « object »), un type
d’objet, un nom de tag, le nom de la personne (« taggeur ») qui a créé le tag
et un message, qui peut contenir une signature comme on peut le voir en
utilisant linkgit:git-cat-file[1] :

    $ git cat-file tag v1.5.0
    object 437b1b20df4b356c9342dac8d38849f24ef44f27
    type commit
    tag v1.5.0
    tagger Junio C Hamano <junkio@cox.net> 1171411200 +0000

    GIT 1.5.0
    -----BEGIN PGP SIGNATURE-----
    Version: GnuPG v1.4.6 (GNU/Linux)

    iD8DBQBF0lGqwMbZpPMRm5oRAuRiAJ9ohBLd7s2kqjkKlq1qqC57SbnmzQCdG4ui
    nLE/L9aUXdWeTFPron96DLA=
    =2E+0
    -----END PGP SIGNATURE-----

Voyez la commande linkgit:git-tag[1] pour apprendre comment créer et
vérifier les objets « tags » (Notez que linkgit:git-tag[1] peut aussi être
utilisé pour créer des « tags légers », qui ne sont pas du tout des objets
« tags » mais juste de simples références dont le nom commence par
« refs/tags/ »).
