## Le modèle objet Git ##

### SHA ###

Toutes les informations nécessaires pour décrire l’historique d’un
projet sont stockées dans des fichiers référencés par un « nom d’objet »
de 40 caractères qui ressemble à quelque chose comme ça :
    
    6ff87c4664981e4397625791c8ea3bbb5f2279a3

Partout dans Git, vous trouverez ces chaînes de 40 caractères.
Dans chaque situation, le nom est calculé en prenant le hash SHA1
représentant le contenu de l’objet. Le hash SHA1 est une fonction de
hash cryptographique. Ce que cela signifie pour nous, c’est qu’il est
virtuellement impossible de trouver deux objets différents avec le même nom.
Cela à de nombreux avantages, parmi lesquels :

- Git peut rapidement savoir si 2 objets sont les mêmes ou non, juste
  en comparant les noms ;
- puisque le nom des objets sont calculés de la même façon dans chaque
  dépôt, le même contenu stocké dans des dépôts différent sera toujours
  stocké avec le même nom ;
- Git peut détecter les erreurs quand il lit un objet, en vérifiant que
  le nom de l’objet est toujours le hash SHA1 de son contenu.

### Les objets ###

Chaque objet se compose de 3 choses : un **type**, une **taille** et le
**contenu**. La _taille_ est simplement la taille du contenu, le contenu
dépend du type de l’objet et il y a 4 types d’objets différents :
« blob », « tree », « commit » et « tag ».

- Un **« blob »** est utilisé pour stocker les données d’un fichier — il
  s’agit en général d'un fichier.
- Un **« tree »** est comme un répertoire — il référence une liste d’autres
  « tree » et/ou d’autres « blobs » (i.e. fichiers et sous-répertoires).
- Un **« commit »** pointe vers un unique "tree" et le marque afin de 
  représenter le projet à un certain point dans le temps. Il contient des
  méta-informations à propos de ce point dans le temps, comme le timestamp,
  l’auteur du contenu depuis le dernier commit, un pointeur vers le (ou les)
  dernier(s) commit(s), etc.
- Un **« tag »** est une manière de représenter un commit spécifique un peu
  spécial. Il est normalement utilisé pour tagger certains commits en tant
  que version spécifique ou quelque chose comme ça.

La quasi-totalité de Git est construit autour de la manipulation de cette simple
structure de 4 types d’objets différents. C’est comme un mini-système de 
fichier qui se situe au-dessus du système de fichier de votre ordinateur.

### Différences avec SVN ###

Il est important de noter que ce système est très différent des autres
outils de contrôle de version (SCM) dont vous êtes familier. Subversion, CVS, 
Perforce, Mercurial et les autres utilisent tous un système de 
_stockage de Delta_ — ils stockent les différences entre un commit et le
suivant. Git ne fait pas ça — il stocke une vue instantanée de la 
représentation de tous les fichiers de votre projet dans une structure
hiérarchisée chaque fois que vous faites un commit. C’est un concept très 
important pour comprendre comment utiliser Git.
