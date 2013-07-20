>J'ai un Mac et je veux travailler avec Python, comment puis-je faire ? Et je me fous que ce soit meilleur sur Linux ou Windows puisque je ne les utilise pas.
Un petit synthèse s'impose. Je précise que je ne suis pas un développeur mais un scientifique qui utilise Python dans un environnement Mac OS X. Il n'y a rien de neuf ici car on peut tout trouver sur Internet quand on veut s'en donner la peine (les développeurs et les utilisateurs anglophones ou hispanophones de Python sur Mac sont de plus en plus nombreux). Je constate aussi que de plus en plus de modules scientifiques sont développés sur Mac OS X.

Une première chose fondamentale est pourtant:

> Hormis si on le désire, il n'y a pas besoin d'installer Python sur Mac OS X puisqu'il est déjà présent


Le problème va néanmoins se poser si je désire installer une autre version, d'où cette petite présentation.

1) Rappels
----------

Rappelons tout d'abord que Mac OS X, sous son interface « grand public », est un système Unix, tout comme Linux, mais basé sur un Unix BSD. En conséquence, il y a beaucoup de fichiers/dossiers Unix dans le système, mais ceux-ci sont masqués par défaut dans l'interface (Finder), par sécurité selon Apple. Si l'on ne fait rien, des dossiers comme */usr/* ne seront jamais visibles. 
Pourtant, sous Unix, l’installation des librairies tierces se fait généralement dans les dossiers comme */usr* et */usr/local*. Il est donc important d'avoir accès à ces dossiers ou de les rendre visibles. Pour cela, il y a plusieurs solutions:

Choisissez « Aller/Aller au dossier » dans le Finder et tapez */usr*, par exemple;  

  - Dans le Terminal (terminal.app, dans */Utilitaires/*):  

        defaults write com.apple.Finder AppleShowAllFiles TRUE
        killal Finder

    et pour revenir à la normale
    
        defaults write com.apple.Finder AppleShowAllFiles FALSE
        killal Finder

  - ou par le choix d'afficher tous les fichiers/dossiers à l'aide d'utilitaires comme [Onyx](http://www.titanium.free.fr/) ou [Avosmacs2Visibility](http://www.magazine-avosmac.com/avosmacV4/telecharger/Avosmac2.php). L'option est réversible .

2) Python, 64 bits et 32 bits
-----------------------------

Comme c'est un Unix, plusieurs versions de Python sont préinstallées. Pour s'en rendre compte il suffit d'ouvrir le Terminal (dans /Utilitaires/) et de taper Python. Elles sont en 64 bits mais il y a moyen de le faire tourner en 32 bits si l'envie vous en prend, de même qu'il est possible de choisir la version que l'on désire utiliser, voir https://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/python.1.html pour montrer qu'il y a bien de la documentation sur le site d'Apple quand on cherche...

3) Vous n'êtes pas satisfaits des versions proposées et vous voudriez en installer une autre ?
----------------------------------------

Plusieurs solutions s'offrent alors à vous:

**a) la manière préconisée par Apple: les Frameworks**

La plus simple est de télécharger une des versions officielles de Python.org et de l'installer Ces versions sont livrées sous forme de Frameworks mais, c'est quoi un Framework ?

Pour faciliter le développement sous Mac OS X, ses concepteurs ont introduit la notion de Frameworks. Un Framework est un dossier contenant du code, des headers, de la documentation et d’éventuelles ressources supplémentaires. Il est ainsi possible d’installer des librairies dynamiques en ne manipulant qu’un seul objet, le Framework. Ils permettent de gérer plusieurs versions d'une librairie (mises à jour,etc.) avec des liens symboliques.
    
Les emplacements de ces Frameworks sont les dossiers Bibliothèque/Library (même si vous voyez Bibliothèque dans le Finder, ce sera Library dans le Terminal). Il y en a au moins trois:  

  - */Système/Bibliothèque/*, réservé à Mac OS X et auquel il ne faut pas toucher;
  - */Bibliothèque/*, utilisable par les administrateurs et dont le contenu est destiné à être partagé par tous les utilisateurs;
  - un dossier *̃/Bibliothèque/* par utilisateur qui peut y mettre ce qu'il veut.
 
La plupart des distributions de logiciels ou de librairies libres utilisent de plus en plus le système de Frameworks pour s'installer sur Mac OS X. Citons, entre autres, QT, GTK+, R, le Python de Python.org

Il est aussi utiliser ce qu'il y a dans un Framework comme dépendances pour compiler d'autres librairies ou applications(tout comme s'il était dans */usr/local/...*).

Si l'on veut une distribution scientifique de Python, il suffit d'installer la version OpenSource de [Enthought](https://www.enthought.com/products/epd/free/) (EPD avec tous les modules nécessaires) en 32 ou 64 bits livrée aussi sous forme de Framework.
  

**b) les gestionnaires de paquets**

Vous pouvez utiliser un Gestionnaires de paquets comme Synaptic sur Ubuntu, ou autres.
Vous leur indiquez ce que vous voulez installer et ils s'occupent de tout (installation des dépendances préalables, configuration et compilation). Au final, vous obtiendrez des exécutables semblables à ceux obtenus dans la première solution, mais dans d'autres dossiers. Ceux-ci sont:

  - [Fink](fink.sf.net/) qui est le système de gestion de paquets de la distribution Linux Debian porté sur Mac OS X. Il installe les programmes dans un dossier à la racine du disque: */sw/*

    fink install Python27
    

 soit à partir d'interfaces graphiques comme [FinkCommander](http://finkcommander.sourceforge.net/)
  
  - [MacPorts](http://www.macports.org/) est un autre système qui installe aussi les programmes dans un dossier à la racine du disque: */opt/*

    sudo port -v install python27

 soit à partir d'interfaces graphiques comme [Porticus](http://porticus.alittledrop.com/)
 
  - [Homebrew](http://mxcl.github.io/homebrew/) , le dernier venu et le plus prometteur d'après moi. Il installe les programmes dans */usr/local/Cellar* avec des liens symboliques dans *usr/local/bin*.

    brew install python

  ou comme Framework
  
    brew install python --framework 
   


Il faut alors rajouter dans le PATH, */sw/bin*, */sw/lib*, */sw/include* ou la même chose pour */opt*

- Le principal problème de Fink et de MacPorts, c'est que ce sont des usines à gaz: ils ne tiennent pas compte de ce qui est préalablement installé, installent tout dans leurs dossiers respectifs ce qui peut créer de réels problèmes dans la gestion des PATHs.
- Homebrew est plus « propre » (dans */usr/*) et se base sur les librairies existantes, si elles sont à jour.

**c) Compiler les sources**


Si le cœur vous en dit, vous pouvez compiler les sources. Pour cela, il vaut mieux installer les « Developper tools » disponible gratuitement. Ils offrent un IDE, XTools et une multitude d'éléments supplémentaires. En pratique, c'est long mais relativement facile. Il est possible de le faire sous une forme classique (résultats dans le dossier */usr/*) ou sous forme de Framework.

**d) une version autonome: [Anaconda](https://store.continuum.io/)**

C'est une version complète de Python autonome (qui n'interfère pas avec les autres versions de Python) et qui s'installe dans un simple dossier (à votre choix).

La version de base est la 2.7.x, mais elle permet d'installer tous les autres versions (de la 2.6 à la 3.3).
Il suffit, pour la lancer d'adapter le chemin (par exemple */Users/vous/anaconda/bin/python*).

Ce n'est pas un framework mais le même genre de version qui serait installée dans */usr/* mais elle a le même avantage qu'un framework, si l'on veut s'en débarrasser, il suffit de placer le dossier anaconda dans la corbeille et c'est tout. Elle peut donc être installée sur un support externe comme une clé USB.

  - elle est installée avec la plupart des modules scientifiques et autres (voir la liste à [Packages](http://docs.continuum.io/anaconda/pkgs.html));
  - elle dispose de toutes les fonctionnalités d'une installation classique comme easy_install ou pip (il suffit d'ajuster le chemin lors de l'appel : */Users/vous/anaconda/bin/pip install* ...).

Mais elle dispose surtout de son propre installeur, nommé [conda](http://www.continuum.io/blog/conda):

  - il permet d'installer et de gérer des modules optimisés à partir du site d'anaconda (optimisés car il est toujours possible de les installer de manière classique)
  - il permet surtout d'installer d'autres versions de Python (2.6.x, à 3.x.x) dans des environnements autonomes, indépendants de la version 2.7.x (une espèce de super "virtual environment", voir [Creating Python 3.3 or Python 2.6 environments](http://docs.continuum.io/conda/intro.html#creating-python-3-3-or-python-2-6-environments))
  - il permet aussi d'installer un nombre infini de versions de Python avec des versions de modules différentes (une avec numpy 1.5, une autre avec numpy 1.7, etc., voir [conda-overview](http://docs.continuum.io/conda/intro.html#conda-overview-).
  - il permet aussi de mettre à jour la version d'anaconda
  - même solution, si vous voulez vous en débarrasser -> dossiers dans la corbeille

4) Les modules
----------------

  - Avec les versions de Python préinstallées ou la version officielle (Framework), cela se fait classiquement avec Pip, easy_install ou python setup.py install. Il existe de plus en plus des distributions propres à Mac OS X comme numpy, scipy, PyQt4, PySide, etc., ce qui fait qu'il n'y a pas besoin de les compiler soi même. Le seul qui posait problème était WxPython avec la version 64 bits de Python;
  - Hormis rares exceptions, je n'ai jamais eu le moindre problème pour installer simplement un module, même les plus complexes comme ceux qui utilisent Fortran;
  - il y a, bien entendu, des modules spécifiques à Mac OS X comme le module py2app qui permet de créer des applications (comme Pyexe sur Windows ou cxfreeze). Et donc ceux qui voudraient utiliser cxfreeze sur Mac OS X en seront pour leur frais et ils pourront dire qu'il n'y a rien sur Mac. Le problème est simplement que les utilisateurs Mac n'en ont pas besoin...

5) Désinstallation d'une version de Python
-------------------------------------------

Comment désinstaller quelque chose sur Mac ? Ça a l'air éminemment complexe pour certains et pourtant...

>Il suffit de mettre l'objet dans la corbeille

- Si on a suivi les directives d'Apple (Frameworks etc., d'où leur intérêt) et si je veux supprimer l'entièreté d'une version de Python, je déplace le dossier Python 2.x dans la corbeille, et c'est tout. Il y aura peut être des chemins à supprimer dans votre fichier .bash_profile et peut être des liens symboliques dans /usr/bin/.
- Si je veux supprimer une version de Python installées par un gestionnaire de paquet, il offre généralement les moyens de le faire.
- le problème se posera éventuellement si l'on a choisi de le compiler soi-même sous une forme classique (multiples fichiers dans le dossier /usr/).
 
Le problème se posera éventuellement si l'on a choisi de le compiler soi-même sous une forme classique (multiples fichiers dans le dossier /usr/).

Compliqué, n'est ce pas ?
Attention, la seule chose à ne pas faire est de supprimer une des versions préinstallées.


6) Désinstallation ou mise à jour d'un module
----------------------------------------------

- si vous avez choisi de le faire de la manière préconisée avec pip ou easy_install, c'est la même chose qu'avec Linux ou Windows
- si elles ont été installées par un gestionnaire de paquets, c'est le problème du gestionnaire, pas d'Apple

7) Conclusions
---------------
Et voila, j'espère avoir été clair.
Pour ma part, j'utilise exclusivement les versions préinstallées et maintenant Anaconda pour les autres versions
Et ne faites surtout pas comme certains débutants qui installent tout n'importe comment et se retrouvent « Gros-Jean comme devant »: [Python + Leopard + Fink + Mac Ports + Python.org + Idiot = broken Python - fresh start?](http://stackoverflow.com/questions/242065/python-leopard-fink-mac-ports-python-org-idiot-broken-python-fresh).

Bien entendu Python sur Mac OS X a de vrais défauts spécifiques, tout comme les versions pour Windows ou Linux et il serait peut être intéressant de les aborder réellement.

Et bien entendu aussi, les utilisateurs de Mac OS X sont souvent les grands oubliés, surtout dans le monde francophone: Linux pour les développeurs et Windows pour les utilisateurs, Mac OS X c'est beau et pas sérieux. Quand je vois dans le monde scientifique le nombre de plus en plus grand de personnes qui utilisent les macs, je me pose des questions. 

