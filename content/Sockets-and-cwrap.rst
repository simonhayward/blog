Sockets and cwrap
#################

:date: 2014-05-01 11:41
:tags: linux, testing, sockets, cwrap
:category: linux
:author: Simon


Have you ever wanted to run a software stack locally, testing client/server
interactions, all on the same machine, under a normal user account?

Maybe `cwrap`_ could help.

What is `cwrap`_?

    cwrap is a set of tools to create a fully isolated network environment to
    test client/server components on a single host.
    It provides synthetic account information, hostname resolution and
    support for privilege separation. The heart of cwrap consists of three
    libraries you can preload to any executable.


`cwrap`_ consists of three libraries:

* `socket_wrapper`_
* `nss_wrapper`_
* `uid_wrapper`_

These libraries allow you to preload to a binary and so replacing library function calls,
by using **LD_PRELOAD**.

From the `ld.so`_ man pages:

    LD_PRELOAD
              A list of additional, user-specified, ELF shared libraries to
              be loaded before all others.  The items of the list can be
              separated by spaces or colons.  This can be used to
              selectively override functions in other shared libraries.

I'm going to look at `socket_wrapper`_ and some examples of how to redirect
tcp sockets to use unix sockets.

Installation
============


**I'm installing socket_wrapper-1.0.1 on Ubuntu 13.04.**

The author of this software is `Andreas Schneider`_, so before installing this I'm going to
import his `pgp key`_.

PGP keys
--------

.. code-block:: bash

    simon@X220:~$ wget --quiet http://www.cryptomilk.org/0xCC014E3D-asn@cryptomilk.org-gpg_key.asc
    simon@X220:~$ gpg --import 0xCC014E3D-asn@cryptomilk.org-gpg_key.asc
    gpg: key CC014E3D: public key "Andreas Schneider <asn@cryptomilk.org>" imported
    gpg: Total number processed: 1
    gpg:               imported: 1  (RSA: 1)
    gpg: no ultimately trusted keys found

The project is part of the samba suite of software, so it's available for download
via the `samba`_ site.

Download
--------

The latest version of `socket_wrapper`_ is `socket_wrapper-1.0.1.tar.gz`_ (04-Feb-2014 09:04, 36K)

.. code-block:: bash

    simon@X220:~$ mkdir sockets
    simon@X220:~$ cd sockets
    simon@X220:~/sockets$ wget --quiet https://ftp.samba.org/pub/cwrap/socket_wrapper-1.0.1.tar.gz
    simon@X220:~/sockets$ wget --quiet https://ftp.samba.org/pub/cwrap/socket_wrapper-1.0.1.tar.asc
    simon@X220:~/sockets$ gzip -d socket_wrapper-1.0.1.tar.gz
    simon@X220:~/sockets$ gpg --verify socket_wrapper-1.0.1.tar.asc
    gpg: Signature made Tue 04 Feb 2014 16:04:36 GMT using RSA key ID CC014E3D
    gpg: Good signature from "Andreas Schneider <asn@cryptomilk.org>"
    gpg:                 aka "Andreas Schneider <asn@samba.org>"
    gpg: WARNING: This key is not certified with a trusted signature!
    gpg:          There is no indication that the signature belongs to the owner.
    Primary key fingerprint: 8DFF 53E1 8F2A BC8D 8F3C  9223 7EE0 FC4D CC01 4E3D
    simon@X220:~/sockets$ tar -xf socket_wrapper-1.0.1.tar
    simon@X220:~/sockets$ cd socket_wrapper-1.0.1/
    simon@X220:~/sockets/socket_wrapper-1.0.1$ mkdir builddir
    simon@X220:~/sockets/socket_wrapper-1.0.1$ cd builddir/

Requirements
------------

`cmake`_ is a requirement to build.

.. code-block:: bash

    simon@X220:~/sockets/socket_wrapper-1.0.1/builddir$ sudo aptitude install cmake

Compile and Install
-------------------

.. code-block:: bash

    simon@X220:~/sockets/socket_wrapper-1.0.1/builddir$ cmake .. -DCMAKE_INSTALL_PREFIX:PATH=~/sockets/bin
    -- The C compiler identification is GNU 4.7.3
    -- Check for working C compiler: /usr/bin/cc
    -- Check for working C compiler: /usr/bin/cc -- works
    ......
    -- Configuring done
    -- Generating done
    -- Build files have been written to: /home/simon/sockets/socket_wrapper-1.0.1/builddir
    simon@X220:~/sockets/socket_wrapper-1.0.1/builddir$ make && make install
    Scanning dependencies of target socket_wrapper
    [100%] Building C object src/CMakeFiles/socket_wrapper.dir/socket_wrapper.c.o
    Linking C shared library libsocket_wrapper.so
    [100%] Built target socket_wrapper
    [100%] Built target socket_wrapper
    Install the project...
    -- Install configuration: ""
    -- Installing: /home/simon/sockets/bin/lib/pkgconfig/socket_wrapper.pc
    -- Installing: /home/simon/sockets/bin/lib/cmake/socket_wrapper-config-version.cmake
    -- Installing: /home/simon/sockets/bin/lib/cmake/socket_wrapper-config.cmake
    -- Installing: /home/simon/sockets/bin/lib/libsocket_wrapper.so.0.0.1
    -- Installing: /home/simon/sockets/bin/lib/libsocket_wrapper.so.0
    -- Installing: /home/simon/sockets/bin/lib/libsocket_wrapper.so

Running netcat
==============

In one terminal run netcat binding to IP: 127.0.0.10 on port 7

.. code-block:: bash

    simon@X220:~/sockets/socket_wrapper-1.0.1/builddir$ cd ~/sockets/bin/
    simon@X220:~/sockets/bin$ mktemp -d
    /tmp/tmp.hxyAQf3Pda
    simon@X220:~/sockets/bin$ LD_PRELOAD=lib/libsocket_wrapper.so \
    > SOCKET_WRAPPER_DIR=/tmp/tmp.hxyAQf3Pda \
    > SOCKET_WRAPPER_DEFAULT_IFACE=10 nc -v -l 127.0.0.10 7
    Listening on [127.0.0.10] (family 0, port 7)


In a seperate terminal send a message to that IP and port.

.. code-block:: bash

    simon@X220:~/sockets/bin$ LD_PRELOAD=lib/libsocket_wrapper.so \
    > SOCKET_WRAPPER_DIR=/tmp/tmp.hxyAQf3Pda \
    > SOCKET_WRAPPER_DEFAULT_IFACE=10 nc -v 127.0.0.10 7
    Connection to 127.0.0.10 7 port [tcp/echo] succeeded!
    Hello!

'Hello!' is then received by the listening netcat

.. code-block:: bash

    simon@X220:~/sockets/bin$ LD_PRELOAD=lib/libsocket_wrapper.so \
    > SOCKET_WRAPPER_DIR=/tmp/tmp.hxyAQf3Pda \
    > SOCKET_WRAPPER_DEFAULT_IFACE=10 nc -v -l 127.0.0.10 7
    Listening on [127.0.0.10] (family 0, port 7)
    Connection from [127.0.0.10] port 7 [tcp/echo] accepted (family 2, sport 41505)
    Hello!

Instead of netcat using tcp sockets, SOCKET_WRAPPER_DIR contains the unix sockets created in place of those tcp sockets.

.. code-block:: bash

    simon@X220:~/sockets/bin$ file /tmp/tmp.hxyAQf3Pda/* && lsof /tmp/tmp.hxyAQf3Pda/*
    /tmp/tmp.hxyAQf3Pda/T0A0007: socket
    /tmp/tmp.hxyAQf3Pda/T0AA221: socket
    COMMAND   PID  USER   FD   TYPE             DEVICE SIZE/OFF    NODE NAME
    nc      31334 simon    5u  unix 0x0000000000000000      0t0 2265223 /tmp/tmp.hxyAQf3Pda/T0A0007
    nc      31505 simon    3u  unix 0x0000000000000000      0t0 2267187 /tmp/tmp.hxyAQf3Pda/T0AA221

Running Nginx
=============

I created the most basic of nginx confs as a simple example:

.. code-block:: bash

    simon@X220:~$ mkdir -p nginx-local/www
    simon@X220:~$ touch nginx-local/www/test
    simon@X220:~$ cd nginx-local
    simon@X220:~/nginx-local$ vi nginx.conf
    error_log /home/simon/nginx-local/error.log;
    worker_processes 1;
    events {
        worker_connections 3;
    }
    http {
        server {
            listen 127.0.0.10:7;
            root /home/simon/nginx-local/www;
            location / {
                autoindex on;
                access_log off;
            }
        }
    }

    simon@X220:~/nginx-local$ LD_PRELOAD=/home/simon/sockets/bin/lib/libsocket_wrapper.so \
    > SOCKET_WRAPPER_DIR=/tmp/tmp.hxyAQf3Pda \
    > SOCKET_WRAPPER_DEFAULT_IFACE=10 \
    > /usr/sbin/nginx -c /home/simon/nginx-local/nginx.conf \
    > -g "pid /home/simon/nginx-local/nginx.pid;"


    Note: You may receive an [alert] warning from nginx, that is cannot read the default error_log.
    As of version 0.7.53, nginx will use the compiled-in default error log before, reading in
    the config file.

Next, check that Nginx is running

.. code-block:: bash

    simon@X220:~/nginx-local$ netstat -nlp | grep $(cat ~/nginx-local/nginx.pid)
    (Not all processes could be identified, non-owned process info
     will not be shown, you would have to be root to see it all.)
    unix  2      [ ACC ]     STREAM     LISTENING     2266669  919/nginx.pid;      /tmp/tmp.hxyAQf3Pda/T0A0007

Connect as a client to the server and capture conversation (SOCKET_WRAPPER_PCAP_FILE)

.. code-block:: bash

    simon@X220:~/nginx-local$ LD_PRELOAD=/home/simon/sockets/bin/lib/libsocket_wrapper.so \
    > SOCKET_WRAPPER_DIR=/tmp/tmp.hxyAQf3Pda \
    > SOCKET_WRAPPER_PCAP_FILE=/tmp/nginx.pcap \
    > SOCKET_WRAPPER_DEFAULT_IFACE=10 telnet 127.0.0.10 7
    Trying 127.0.0.10...
    Connected to 127.0.0.10.
    Escape character is '^]'.
    GET / HTTP/1.1
    Host: 127.0.0.10

    HTTP/1.1 200 OK
    Server: nginx/1.2.6 (Ubuntu)
    Date: Thu, 01 May 2014 15:26:31 GMT
    Content-Type: text/html
    Transfer-Encoding: chunked
    Connection: keep-alive

    104
    <html>
    <head><title>Index of /</title></head>
    <body bgcolor="white">
    <h1>Index of /</h1><hr><pre><a href="../">../</a>
    <a href="test">test</a>                                               01-May-2014 14:10                   0
    </pre><hr></body>
    </html>

    0

    simon@X220:~/nginx-local$ kill -QUIT $(cat /home/simon/nginx-local/nginx.pid)


All of this network conversation is caught in the pcap file and so can be loaded into
wireshark.

.. code-block:: bash

    simon@X220:~/nginx-local$ wireshark /tmp/nginx.pcap

Conclusion
==========

This throws up a whole host of possibilities to test client/server interactions
that are required for your application and all tested locally as a normal
(non root) user.

The ability to easily translate IPv4 and IPv6 addresses to a unix sockets,
and simulate binding to privileged ports (< 1024), allows for
easier local testing, if your application requires a lot of network interactions
as part of it's test suite.

You may also be interested in the other components of `cwrap`_

`nss_wrapper`_

* Provides information for user and group accounts
* Network name resolution using a hosts file

Name resolution could work well with `socket_wrapper`_ and works much the same
way.


.. code-block:: bash

    simon@X220:~/nss_wrapper$ echo "127.0.0.10  simonsblog.co.uk" > hosts
    simon@X220:~/nss_wrapper$ LD_PRELOAD="bin/lib/libnss_wrapper.so" \
    > NSS_WRAPPER_HOSTS=hosts \
    > python -c "import socket; print(socket.gethostbyname('simonsblog.co.uk'))"
    127.0.0.10


`uid_wrapper`_

* Allows uid switching as a normal user.
* Start any application making it believe it is running as root.
* Support for user/group changing in the local thread using the syscalls (like glibc).


Check out the article on `lwn.net`_ and `cwrap`_ for more info.

.. _cwrap: http://cwrap.org
.. _socket_wrapper: http://git.samba.org/?p=socket_wrapper.git
.. _nss_wrapper: http://git.samba.org/?p=nss_wrapper.git
.. _uid_wrapper: http://git.samba.org/?p=uid_wrapper.git
.. _Andreas Schneider: http://blog.cryptomilk.org
.. _pgp key: http://blog.cryptomilk.org/2013/10/07/new-pgp-key/
.. _samba: https://ftp.samba.org/pub/cwrap/
.. _cmake: http://www.cmake.org/
.. _ld.so: http://man7.org/linux/man-pages/man8/ld.so.8.html
.. _lwn.net: https://lwn.net/Articles/595320/
.. _socket_wrapper-1.0.1.tar.gz: https://ftp.samba.org/pub/cwrap/socket_wrapper-1.0.1.tar.gz
