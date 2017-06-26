git -a -m "initial commit"
##########################

:date: 2011-08-20 16:20
:tags: talks, open source, oggcamp, blog, python, nginx, gunicorn, django
:author: Simon

I’ve decided to set this blog up after hearing a talk given at
`OggCamp`_ by `LornaJane Mitchell`_ entitled: careers in Open Source.

It was refreshing to hear her enthusiasm for open source but also her
frankness about what got her started and what has lead on from her doing
more in open source and how we and others can benefit from giving back
to the **open source community**.

The sunday morning (*hangover*) slot for a talk is never the best time,
but gave what I thought and it seems `others`_ an inspiring talk to get
more involved with open source and so enhance not only your career
prospects but also to enhance you as a person.

One of these goals is to do something like starting a blog to which this
is my attempt. Like all new things I hope it doesn’t become like a new
gym membership that sees frantic use for the first few weeks/months,
then tails off to a slow decline. I hope not, but we’ll see, with
`twitter`_ / `identi.ca`_ / `google+`_ these things can all sap time, but a
point she made which I think rings true is don’t try and write the
perfect blog entry, if something worked for you blog about it, post it
and get on with your life. It may contain typos and it may not be
grammatically correct but if someone searches on google and finds your
solution can also help them with their problem, then its all good. An
*agile* approach to blogging, release early and often.

This is true for me as I often have one line solutions to problems that
I’ve found or written that I might stash away to my `~/UbuntuOne`_
account for later reference, maybe that also needs to be added to my
blog from now on.

As well as wanting to set up a blog I wanted to use `python`_,
`gunicorn`_ & `nginx`_, the following is a list of technologies I used:

-  `django`_
-  `nginx`_
-  `gunicorn`_
-  `supervisord`_
-  `virtualenv`_
-  `fabric`_

I wanted to get this blog up and running ASAP, so taken mostly from
`James Bennetts`_ great book `Practical Django Projects`_, I purchased a
domain name, set up a `github`_ repo, set up a `linode VPS`_ and so now
have a functioning blog.

It’s been fun setting this up and that’s one of the main reasons I’ve
chosen `django`_ (not only because I’ve been listening to and trying to
learn gypsy jazz guitar like the **real** `Django Reinhardt`_) but because it
encourages reuse, simplicity and application decoupling. I love the line
taken from the `Practical Django Projects`_ book:

    *“At the end, you’ll come to a wonderful realization - that web
    development is fun again”*

So all of these feels a bit like starting a new project (hence git -a -m
“initial commit”), with many more commits to come..

.. _OggCamp: http://oggcamp.org/
.. _LornaJane Mitchell: http://www.lornajane.net/
.. _others: https://twitter.com/#!/search/oggcamp
.. _twitter: http://twitter.com/simhay
.. _identi.ca: http://identi.ca/simhay
.. _google+: https://plus.google.com/
.. _~/UbuntuOne: https://one.ubuntu.com/
.. _python: http://www.python.org/
.. _gunicorn: http://gunicorn.org/
.. _nginx: http://nginx.net/
.. _django: https://www.djangoproject.com/
.. _supervisord: http://supervisord.org/
.. _virtualenv: http://pypi.python.org/pypi/virtualenv
.. _fabric: http://docs.fabfile.org/
.. _James Bennetts: http://www.b-list.org/
.. _Practical Django Projects: http://www.amazon.co.uk/Practical-Django-Projects-Experts-Development/dp/1430219386
.. _github: https://github.com/simonhayward/simonsblog_django
.. _linode VPS: http://www.linode.com/
.. _Django Reinhardt: http://en.wikipedia.org/wiki/Django_Reinhardt

