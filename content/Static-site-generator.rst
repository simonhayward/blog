Static site generator - Pelican
###############################

:date: 2013-02-03 21:50
:tags: blog, pelican
:category: python
:author: Simon

I `initially <|filename|Git-initial-commit.rst>`_ set up this blog using `django`_,
but recently I've wanted to try out a static site generator & decided to try
out `pelican`_.

It was **extremely** easy to set this up and deploy an updated blog to my site.
It took a few hours to set up pelican and import previous posts
(converting markdown to `reStructuredText`_) and so had a new blogging platform
up and running very quickly.

Installing
----------

.. code-block:: bash

    simon@x220:~$ mkproject simonsblog
    (simonsblog)simon@x220:~/Devel/simonsblog$ pip install pelican

Then set up pelican by answering these basic questions. Note the option to
deploy via ftp/SSH or dropbox.

Set up
------

.. code-block:: bash

    (simonsblog)simon@x220:~/Devel/simonsblog$ pelican-quickstart
    > What will be the title of this web site? Simonblog
    > Who will be the author of this web site? Simon
    > What will be the default language of this web site? [en]
    > Do you want to specify a URL prefix? e.g., http://example.com   (Y/n)
    > What is your URL prefix? (see above example; no trailing slash) http://simonsblog.co.uk
    > Do you want to enable article pagination? (Y/n)
    > How many articles per page do you want? [10]
    > Do you want to generate a Makefile to easily manage your website? (Y/n)
    > Do you want an auto-reload & simpleHTTP script to assist with theme and site development? (Y/n)
    > Do you want to upload your website using FTP? (y/N)
    > Do you want to upload your website using SSH? (y/N) y
    > What is the hostname of your SSH server? [localhost] simonsblog
    > What is the port of your SSH server? [22]
    > What is your username on that server? [root] simon
    > Where do you want to put your web site on that server? [/var/www]
    > Do you want to upload your website using Dropbox? (y/N)


Your virtualenv project should now look something like this:

.. code-block:: bash

    (simonsblog)simon@x220:~/Devel/simonsblog$ ls
    content  develop_server.sh  Makefile  output  pelicanconf.py  publishconf.py

Update pelicanconf.py with your specific details:

.. code-block:: python

    AUTHOR = "Simon"
    SITENAME = ("Simonsblog")
    SITEURL = 'http://simonsblog.local'

    TIMEZONE = 'Europe/London'

    DEFAULT_LANG = 'en'

    # Blogroll
    LINKS =  (('Python.org', 'http://python.org'),)

    # Social widget
    SOCIAL = (('delicious', 'http://delicious.com/djangos'),
              ('github', 'https://github.com/simonhayward'),
              ('google+', 'https://plus.google.com/u/0/105199393791103843210/posts'),
              ('rss', '/feeds/all.atom.xml'),
              ('twitter', 'https://twitter.com/simhay'),)

    FILES_TO_COPY = (('extra/robots.txt', 'robots.txt'),
                     ('extra/favicon.ico', 'favicon.ico'),)

    DEFAULT_PAGINATION = 10
    THEME = "subtle"
    STATIC_PATHS = ['images']
    GOOGLE_ANALYTICS = 'UA-2417620-7'
    TWITTER_USERNAME = 'simhay'
    DISQUS_SITENAME = 'siblog'


I've created an *extra* folder within the content folder to hold favicon.ico
and robots.txt file.

Styling
-------

Pelican comes with *pelican-themes* to manage various themes for pelican.

.. code-block:: bash

    (simonsblog)simon@x220:~/Devel/simonsblog$ cd
    (simonsblog)simon@x220:~$ git clone git://github.com/getpelican/pelican-themes.git
    (simonsblog)simon@x220:~$ pelican-themes -i pelican-themes/subtle


Create a post
-------------

.. code-block:: bash

    (simonsblog)simon@x220:~$ cdproject && cd content
    (simonsblog)simon@x220:~/Devel/simonsblog/content$ vi Static-site-generator.rst

Each file contains some metadata, for this post this is the first 7 lines:

.. code-block:: bash

    Static site generator
    #####################

    :date: 2013-02-03 21:50
    :tags: blog, pelican
    :category: python
    :author: Simon

The rest of the post is standard `reStructuredText`_.
It's a simpler set up now, as all I need is to use is vim. Once I have
created a new file under the content directory, I'm using `reStructuredText`_,
but you can use markdown, I can view these changes locally and simply rsync
the generated content direct to my server. It couldn't be easier or simpler &
means I can host this blog anywhere.

Viewing changes
---------------

.. code-block:: bash

    (simonsblog)simon@x220:~$ cdproject
    (simonsblog)simon@x220:~/Devel/simonsblog$ ./develop_server.sh start
    (simonsblog)simon@x220:~/Devel/simonsblog$ firefox localhost:8000

When you make any further changes, these should be picked up automatically and the site
is generated again so you can view these changes locally.

Deploy
------

Assuming you already have a host and web server set up (apache/nginx etc),
you simply need to push the generated content out to your host - in my case
via SSH.

.. code-block:: bash

    (simonsblog)simon@x220:~$ cdproject
    (simonsblog)simon@x220:~/Devel/simonsblog$ make rsync_upload


When you happy just close down the local http server:

.. code-block:: bash

    (simonsblog)simon@x220:~/Devel/simonsblog$ ./develop_server.sh stop


For me the benefits are:

- Using vim (reStructuredText)
- Code syntax highlighting
- Rsync deployment
- Ease of use
- Host content anywhere

Having a complete `django`_ installation was maybe too much for a simple blog,
so switching to `pelican`_ makes perfect sense for me. If you have a blog and
want to simplify the creation and hosting process, try `pelican`_ it really
stands out as a simple, easy to use static site generator.


.. _django: https://www.djangoproject.com/
.. _pelican: http://getpelican.com/
.. _reStructuredText: http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html
