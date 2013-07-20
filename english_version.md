
    The Apple Python is functional and the normal site-packages folder is /Library/Python/2.7/site-packages (and not /System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages). You can use it without problem.
    I never had any problem to install all modules (numpy, scipy, matplotlib, pandas, shapely, and others...) that I wanted as frameworks, or with pip or easy_install, including virtualenv (simply install them in the conventional way in Python) or creating virtual environments.
    when you install a framework module, It is placed in in the normal site-packages folder.
    the only problem is possibly the "old" Python version (not a problem for me, using 2.6.x, 2.7.x and 3.3.x versions)

But if you want, you can install others versions of Python (in 64-bits, not 32 !):

a) the way prescribed by Apple: as a framework

    the official versions of Python.org are installed in /Library/Frameworks/Python.framework with site-packages folder in /Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages
    same for the Enthought scientific version of Python (scientific distribution with many modules preinstalled, numpy, scipy, matplotlib,...),
    (you can also install the Homebrew Python version as a framework, see below)

You must change the PATH of the Python executable in /usr/bin (usually, this is done automatically by the distribution by symlinks or in the */Users/me/.bash_profile* file ).

The modules installed in /Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages do not interfere with those installed in /Library/Python/2.7/site-packages if you use the appropriate Python executable and viceversa.

b) the package management system way

    MacPorts install its own version of Python in the folder /opt/;

    sudo port -v install python27

    Fink install its own version of Python in the folder /sw/;

    fink install Python27

    Homebrew installs Python in /usr/local/Cellar with symlinks in /usr/local/bin.

    brew install python
    or
    brew install python --framework

    To use them, you must add /sw/bin, /sw/lib/ or /opt/bin, /opt/lib/ to the PATH and change the PATH of the Python executable
    For me, the main problem with Fink and MacPorts is that they do not take into account what is already installed and install all in their respective folders which can create real problems in the management of library paths.
    The Homebrew solution is "cleaner" (in /usr/local) and is based on existing libraries if they are up to date, otherwise it installs its own versions of the libraries

c) the "autonomous" way

    the perfect solution is Anaconda (another scientific distribution with many modules preinstalled, ),
        Installs cleanly into a single directory (where you want as /Users/me/anaconda)
        doesn’t require root privileges
        doesn’t affect other Python installs on your system, or interfere with OS X Frameworks
        switch to/from Anaconda just by setting $PATH or creating an alias in */Users/me/.bash_profile*
            alias anaconda='/Users/me/anaconda/bin/python'
            alias anaconda3='/Users/me/anaconda/envs/py33/bin/python3'
        you can install Python versions from 2.6.x to 3.3.x
        Innovative package and environment manager for Python, named conda, but you can use pip or easy_install without problem
        for me now, it is the best solution to install virtual environments (as /Users/me/anaconda/envs/py33 )

d) the "hard" way

    you can compile your own version of Python in a classical form (results in /usr/) or as a framework. It takes time but it is not difficult.

So your question:

    How can I get a Python installation in a virtual environment that includes a framework that I can include into Xcode?

Unless you are a Unix specialist (PATHs management) , you must use the Apple's recommended solution, a frameworks distribution (including the Apple Python)
