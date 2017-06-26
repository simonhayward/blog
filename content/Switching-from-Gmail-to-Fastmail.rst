Switching from Gmail to Fastmail
################################

:date: 2013-12-06 14:16
:tags: email
:author: Simon

.. image:: /images/fastmail/header-thumb.png
   :alt: Fastmail.fm page header
   :align: center
   :height: 143px
   :width: 400px

`Large image`_

Three months ago I decided to try out `fastmail.fm`_ after having used
google's `gmail`_ as my primary email for a number of years. I kept seeing
a number of people moving away from google after the `NSA revelations`_  and
the admission that `gmail users cannot expect privacy`_.

I have no complaints about using `gmail`_ all these years, for a free service
it is better than most other free options and their service has never been
down or caused me any issues.

However you do end up living in this **google product world**, an all
encompassing world in which they will end up knowing more about you than
even your family will know about you.

If something is free is it really right
to expect privacy? Which goes along with the saying:

    *"If you don't pay for the product, then you are the product*".


Maybe this is true, in which case you need to look at other options,
`fastmail.fm`_ was one of those options.
Their offer of *Providing a Reliable and Clutter-Free Email Experience* who
take privacy seriously, was attractive. While they also suggest that being an
Australian company, they `fall outside the (US) NSA's jurisdiction`_.

So I initially signed up for a free trial account on the Enhanced ($40 a year)
account, which includes:

* 15 GB email storage
*  5 GB file storage
*  Use your own domain
*  No included SMS
*  Advanced anti-spam
*  No ads

You can choose an email address from a substantial (~115)
list of *fastmail* like top level domains, a selection being:

* fastmail.fm
* fastmail.to
* fastmail.us
* fastmail.cn
* fastmail.com.au
* fastmail.jp
* fastmail.net
* fastmail.es
* fastmail.co.uk
* fastmail.in
* fastmail.im
* fastmail.nl
* fastmail.se
* fastmail.mx
* fastmail.tw
* fmail.co.uk
* sent.com
* myfastmail.com
* speedymail.org
* fast-email.com
* fastimap.com
* fast-mail.org
* fastemail.us
* operamail.com

After which I set up my fastmail account to use my own domain name, simonsblog.co.uk.
So I switched my DNS MX records via my `dnsimple`_ DNS hosting provider
to point to fastmails servers. Fastmail do offer to handle DNS
for you, but I'm already happily using the excellent service provided by
`dnsimple`_ for all my DNS hosting.

.. code-block:: bash

    simon@X220:~$ dig +short simonsblog.co.uk mx
    20 in2-smtp.messagingengine.com.
    10 in1-smtp.messagingengine.com.


Added an SPF record.

.. code-block:: bash

    simon@X220:~$ dig simonsblog.co.uk +short spf
    "v=spf1 include:spf.messagingengine.com -all"

I then added a TXT record for my DKIM key, retrieved via Fastmail.fm ->
Advanced settings -> Virtual Domains

I also set up an alias (CNAME) to access webmail via my domain.

.. code-block:: bash

    simon@X220:~$ dig +short mail.simonsblog.co.uk cname
    www.fastmail.fm.

While under this free trial, `fastmail.fm`_ announced that `staff had purchased the
business back from opera`_ which was getting noticed on `twitter`_.

This is a key issue for me, for staff to un-acquire itself just shows the belief
the team have in it.

So three months in and I'm happily switched to using `fastmail.fm`_ as my primary
email address. Some nice features are:

* Fast loading
* Infinite scrolling
* Extensive configuration
* Ad free

Some not nice features:

* No native mobile app (I'm using `MailDroid Pro`_)

I haven't totally unplugged myself from gmail, I still forward all gmail to
my fastmail account, but these are becoming less and less as I move more
accounts over to use my new address.

The process to switch has been relatively pain free and for $40
a year seems a small price to pay to have secure and private email.


.. _MailDroid Pro: https://play.google.com/store/apps/details?id=com.maildroid.pro&hl=en
.. _twitter: https://twitter.com/jacobian/status/383084245784076288
.. _staff had purchased the business back from opera: http://blog.fastmail.fm/2013/09/25/exciting-news-fastmail-staff-purchase-the-business-from-opera/
.. _fall outside the (US) NSA's jurisdiction: http://www.theguardian.com/technology/2013/oct/07/australias-fastmail-secure-email-nsa
.. _dnsimple: https://dnsimple.com/r/3d06c548b79445
.. _excellent dnsimple: https://dnsimple.com/r/3d06c548b79445
.. _gmail: https://gmail.google.com
.. _fastmail.fm: http://www.fastmail.to/?STKI=11487141
.. _Large image: /images/fastmail/header.png
.. _NSA revelations: http://www.theguardian.com/world/the-nsa-files
.. _gmail users cannot expect privacy: http://www.theguardian.com/technology/2013/aug/14/google-gmail-users-privacy-email-lawsuit
