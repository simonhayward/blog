Add munin monitoring in 5 minutes
#################################

:date: 2011-08-31 14:49
:tags: munin, debian, monitoring
:category: linux
:author: Simon

This site is set up on a `Linode VPS`_, the OS is `debian`_ squeeze 32
bit, and I wanted some basic monitoring in place, so knowing how quick
`Munin`_ is to set up, I did indeed have monitoring up and running on
this VM in no time at all.

.. code-block:: bash

    $ sudo aptitude install munin
    $ sudo aptitude install munin-plugins-extra

It’s then just a case of creating symbolic links to those plugins you
want to use. I’m using `nginx`_ and used these `perl scripts`_ to add
monitoring and added a server config for these plugins to query on the
nginx status.

.. code-block:: bash

    $ git clone https://github.com/perusio/nginx-munin
    $ mv nginx-munin/nginx_* /usr/share/munin/plugins/
    $ cd /etc/munin/plugins
    $ ln -s /usr/share/munin/plugins/nginx_connection_request nginx_connection_request
    $ ln -s /usr/share/munin/plugins/nginx_memory nginx_memory
    $ ln -s /usr/share/munin/plugins/nginx_request nginx_request
    $ ln -s /usr/share/munin/plugins/nginx_status nginx_status
    $ sudo aptitude install libio-all-lwp-perl # nginx plugins have dependencies

I’ve compiled nginx from source, so had to recompile with the
*http\_stub\_status\_module*

.. code-block:: bash

    $ wget http://nginx.org/download/nginx-1.0.5.tar.gz
    $ tar -zxvf nginx-1.0.5.tar.gz && mv nginx-1.0.5 nginx-src && cd nginx-src
    $ ./configure --prefix=/opt/nginx-1.0.5 --user=nginx --group=nginx \
    --with-http_ssl_module --with-ipv6 --with-http_stub_status_module
    $ make
    $ make install

Then add an server config for nginx monitoring:

.. code-block:: bash

    server {
       server_name munin.simonsblog.co.uk;
       root /var/cache/munin/www/;
       location / {
       index index.html;
       access_log off;
    }
    server {
        server_name nginx.local;
        allow 127.0.0.1;
        deny all;
        location /nginx_status {
        stub_status on;
        access_log off;
        }
    }

    $ chmod -R 755 /usr/share/munin/plugins/
    $ /etc/init.d/nginx stop
    $ ln -sfn /opt/nginx-1.0.5 /opt/nginx # point to newly compiled nginx
    $ /etc/init.d/nginx start
    $ /etc/init.d/munin-node start

You should then have a working munin monitoring installation. For the
curious you can view this via the subdomain (munin) on this domain.

.. _Linode VPS: http://linode.com
.. _debian: http://www.debian.org
.. _Munin: http://munin-monitoring.org
.. _nginx: http://nginx.org
.. _perl scripts: https://github.com/perusio/nginx-munin
