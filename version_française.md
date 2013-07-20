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

a) la manière préconisée par Apple: les Frameworks
