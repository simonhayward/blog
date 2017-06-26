Virtualenvwrapper
#################

:date: 2011-09-19 21:43
:tags: open source, python, django
:category: python
:author: Simon

If your using `virtualenv <http://www.virtualenv.org/>`_ then you should
be using
`virtualenvwrapper <http://www.doughellmann.com/docs/virtualenvwrapper/>`_,
it's a great tool to make it really easy to use multiple virtualenv's
and work with them painlessly.

Here's the why
~~~~~~~~~~~~~~

`Virtualenv <http://www.virtualenv.org/>`_ is a nice way to separate out
all your python libraries into their own individual environments,
`virtualenvwrapper <http://www.doughellmann.com/docs/virtualenvwrapper/>`_
makes it easy to put all these environments into one convenient
location, rather than install all your python libraries into a site
wide, global location.

By default when you *pip install* onto your machine, these will default
to your global site packages location, somewhere like:
/usr/local/lib/python2.6/dist-packages (on ubuntu)

Instead if we use virtualenv's +
`virtualenvwrapper <http://www.doughellmann.com/docs/virtualenvwrapper/>`_
we can contain multiple python modules/libraries installed to a selected
personal folder. I have all my virtualenv's installed in a hidden
directory in my home folder.

.. code-block:: bash

    /home/simon/.virtualenvs

This is defined via your shell initialisation file (in my case .bashrc)

.. code-block:: bash

    $ grep virtualenvs .bashrc
    export WORKON_HOME="$HOME/.virtualenvs"

Within this folder all my libs are installed (once I've activated that
virtual environment):

.. code-block:: bash

    simon@simon-development:/home/simon/.virtualenvs$ ls -d */
    geo/  metrics/  monitor/  simonsblog/

To actually use one of these virtual environments you only have to
*activate* the one you wish to work in, this is where
`virtualenvwrapper <http://www.doughellmann.com/docs/virtualenvwrapper/>`_
comes in really handy:

.. code-block:: bash

    simon@simon-development:/home/simon/.virtualenvs$ workon
    geo
    metrics
    monitor
    simonsblog

This list all my virtual environments, to select mine I simply:

.. code-block:: bash

    simon@simon-development:/home/simon/.virtualenvs$ workon simonsblog
    (simonsblog)simon@simon-development:/home/simon/Devel/simonsblog_django$

I'm then transferred into my virtual environment (simonsblog\_django)
and any libraries I want to install via pip or easy\_install will be
installed into my virtual environment and not globally, and using
virtualenvwrapper.projects (as of virtualenvwrapper 2.9 there is no need
to install this package separately) I also get dumped into my working
folder for that project (see
`setvirtualenvproject <http://www.doughellmann.com/docs/virtualenvwrapper/command_ref.html#setvirtualenvproject>`_).

.. code-block:: bash

    $ ls -d /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/*/

    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/akismet-0.2.0-py2.6.egg-info/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/debug_toolbar/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/django/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/Django-1.3-py2.6.egg-info/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/django_debug_toolbar-0.8.5-py2.6.egg-info/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/django_imagekit-0.3.6-py2.6.egg-info/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/django_tagging-0.3.1-py2.6.egg-info/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/docutils/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/gunicorn/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/imagekit/
    /home/simon/.virtualenvs/simonsblog/lib/python2.6/site-packages/markdown/
    ....

Whenever I do pip install *package* all those files are dumped into my
/home/simon/.virtualenvs/simonsblog\_django/lib/python2.6/site-packages/
directory.

The only rule is this: **you need to install *virtualenv* &
*virtualenvwrapper* as you would normally into the global site wide
packages**, then once these are installed globally for everything else
you can install to one of your virtual environments.

Here's the how
~~~~~~~~~~~~~~

.. code-block:: bash

    $ sudo aptitude install python-pip python-dev build-essential
    $ sudo pip install -U pip
    $ sudo pip install virtualenv
    $ sudo pip install virtualenvwrapper
    $ mkdir $HOME/.virtualenvs
    $ vi .bashrc
    export WORKON_HOME="$HOME/.virtualenvs"
    source /usr/local/bin/virtualenvwrapper.sh
    $ source bashrc
    $ mkvirtualenv myvirtualenvtest
    ....

This will then initiate your myvirtualenvtest environment and from then
on your installs (pip/easy\_installs) will relate to your activated
virtualenv.

My .bashrc looks something like this:

.. code-block:: bash

    export WORKON_HOME="$HOME/.virtualenvs"
    export VIRTUALENVWRAPPER_HOOK_DIR=$WORKON_HOME
    source /usr/local/bin/virtualenvwrapper.sh
    export PIP_VIRTUALENV_BASE=$WORKON_HOME
    export PIP_RESPECT_VIRTUALENV=true
    export PROJECT_HOME=$HOME/Devel

    # alias' from Holger Krekel http://paste.pocoo.org/show/164838/
    alias v=workon
    alias v.deactivate=deactivate
    alias v.mk='mkvirtualenv --no-site-packages'
    alias v.mk_withsitepackages='mkvirtualenv'
    alias v.rm=rmvirtualenv
    alias v.switch=workon
    alias v.add2virtualenv=add2virtualenv
    alias v.cdsitepackages=cdsitepackages
    alias v.cd=cdvirtualenv
    alias v.lssitepackages=lssitepackages

You'll also see in my .bashrc is a PROJECT\_HOME environment variable,
this is where I keep my project code, which again keeps my code in a
handy convenient place, check out
`projects <http://www.doughellmann.com/docs/virtualenvwrapper/projects.html>`_
in virtualenvwrapper for more on this, but you can do nice things like
use templates so you can start a new django project (this is an
extension details
`here <http://www.doughellmann.com/projects/virtualenvwrapper.django/>`_)
and this will build up the necessary libraries for django within this
new project.

There is loads more to `virtualenv <http://www.virtualenv.org/>`_ and
`virtualenvwrapper <http://www.doughellmann.com/docs/virtualenvwrapper/>`_,
you will find that are invaluable when dealing with multiple
projects/sites which each need their own specific python modules and
libraries.

Also check out this `Pycon video <http://www.pycon.tv/video/36/>`_ that
explains `virtualenv <http://www.virtualenv.org/>`_.

