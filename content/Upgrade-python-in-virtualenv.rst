Upgrade Python in Virtualenv
############################

:date: 2014-09-20 17:15
:tags: open source, python, django, virtualenv
:category: python
:author: Simon

You can simply create a new `virtualenv`_ from scratch with the new version
of `Python`_ installed, but you can also upgrade your Python binary in place
of the old.

Upgrade
~~~~~~~~~~~~~~

I keep my python virtual environments in a hidden folder *.virtualenvs*
in my home directory.

Inside my project I can see the current python 3.3 version

.. code-block:: bash

    simon@X220:~$ cd .virtualenvs/
    simon@X220:~/.virtualenvs$ ls -l project/bin/python*
    lrwxrwxrwx 1 simon simon       9 Apr  4 16:03 project/bin/python -> python3.3
    lrwxrwxrwx 1 simon simon       9 Apr  4 16:03 project/bin/python3 -> python3.3
    -rwxrwxr-x 1 simon simon 3928976 Apr  4 16:03 project/bin/python3.3


If you want to go from `Python 3.3.2`_ to `Python 3.4.1`_ you can `download`_ and
compile each release individually or if you are using `Ubuntu`_ and you want
to get a range of `Python`_ versions, you can add the `Dead snakes`_
PPA to get versions from 2.3 right through to 3.4

.. code-block:: bash

    simon@X220:~/.virtualenvs$ sudo add-apt-repository ppa:fkrull/deadsnakes
    simon@X220:~/.virtualenvs$ sudo apt-get update
    simon@X220:~/.virtualenvs$ sudo aptitude install python3.4 python3.4-dev

You can now install this python version, by re-running the virtualenv
initialisation over the top of your current one.

.. code-block:: bash

    simon@X220:~/.virtualenvs$ virtualenv -p python3.4 project
    simon@X220:~/.virtualenvs$ ls -l project/bin/python*
    lrwxrwxrwx 1 simon simon       9 Sep 20 17:59 project/bin/python -> python3.4
    lrwxrwxrwx 1 simon simon       9 Sep 20 17:59 project/bin/python3 -> python3.4
    -rwxrwxr-x 1 simon simon 3928976 Apr  4 16:03 project/bin/python3.3
    -rwxrwxr-x 1 simon simon 3508112 Sep 20 17:59 project/bin/python3.4

Your previous version is still there, as well as your new version, but the
default symbolic link now points to your latest version.

.. code-block:: bash

    simon@X220:~/.virtualenvs$ source project/bin/activate && python -V
    Python 3.4.1

One thing you will have to do is to **re-install all your module requirements**
after the upgrade.

.. code-block:: bash

    (project)simon@dev-wishiwashi:~/Devel/project$ pip install -r requirements.txt


.. _Python: https://www.python.org
.. _virtualenv: http://www.virtualenv.org
.. _Python 3.3.2: https://www.python.org/download/releases/3.3.2/
.. _Python 3.4.1: https://www.python.org/download/releases/3.4.1/
.. _Dead snakes: https://launchpad.net/~fkrull/+archive/ubuntu/deadsnakes
.. _Ubuntu: http://www.ubuntu.com
.. _download: https://www.python.org/download
