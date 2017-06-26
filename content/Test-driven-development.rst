Test driven development with Django
###################################

:date: 2011-11-17 19:10
:tags: django, selenium, TDD, python
:category: python
:author: Simon

I went to a `workshop`_ last night on TDD (`Test Driven Development`_)
using `django`_ and `selenium`_, which was given by `Harry Percival`_.
It was hosted at `skills matter exchange`_ in London and there was free
beer and pizza…which was an unexpected bonus!

There must have been around 35 attendees with a mixture of skill sets
and backgrounds and it was an extremely good introduction not only to
TDD but also to django framework, and almost everyone kept pace and I
was impressed by Harry’s enthusiasm for TDD and why you should be
adopting it for development.

I also think it highlighted the accessibility of the `django framework`_
and how you can pick up on it very quickly, and half way through the
pace was picked up as everyone in the room was generally flying though
the work. The workshop was based on the django tutorial `writing my
first app`_ which leads you through from starting a project to creating
a polls application, which you can administer through the admin
interface and is a gentle introduction to the `models / templates /
view`_ paradigm adopted by django.

So you go from installing and setting up a basic django project and
application to firing up selenium to check each step of your progress
along the way.

The key thing that I took away from it was the *develop - test - develop
- test* loop that you need to cycle through, in order to be really TDD,
the tests direct **all** development, so the steps are small and
incremental. Even though you know creating a models.py file with an
model class that doesn’t even extend from django.db.models.Model, you do
*just* enough to pass the next step of the test. Which should end up
with you not developing unnecessary code, which can happen when you are
developing without tests and you try to cover all possibilities without
thinking about what the application will *actually* deliver upon. You
design your tests up front which you then write code to pass each
step/test along the way. Write a test that fails, write the code to make
it pass.

You can follow all this along simply by going to `Harry’s website`_, I
recommended you do if you are interested in trying TDD and preferably
with the django framework, this is really aimed at everyone and so no
experience is necessary.

Well done to harry for delivering such a good introduction on TDD with
django and selenium! There could be more workshops lined up, so if your
in London and fancy coming along, check the `python-uk mailing list`_ to
see when any future workshops are planned.

.. _workshop: http://skillsmatter.com/podcast/ajax-ria/tdd-django-selenium/js-2958
.. _Test Driven Development: http://en.wikipedia.org/wiki/Test-driven_development
.. _django: https://www.djangoproject.com/
.. _selenium: http://seleniumhq.org/
.. _Harry Percival: http://harry.pythonanywhere.com/
.. _skills matter exchange: http://skillsmatter.com/go/find-us/js-1520
.. _django framework: https://www.djangoproject.com/
.. _writing my first app: https://docs.djangoproject.com/en/dev/intro/tutorial01/
.. _models / templates / view: https://docs.djangoproject.com/en/dev/faq/general/#django-appears-to-be-a-mvc-framework-but-you-call-the-controller-the-view-and-the-view-the-template-how-come-you-don-t-use-the-standard-names
.. _Harry’s website: http://harry.pythonanywhere.com/
.. _python-uk mailing list: http://mail.python.org/mailman/listinfo/python-uk
