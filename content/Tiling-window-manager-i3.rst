Tiling window manager: i3
#########################

:date: 2012-11-09 17:28
:tags: window manager, i3, ubuntu, debian, linux
:category: linux
:author: Simon

After using the `awesome`_ window manager for the last few years, I’ve
switched over to a new tiling window manger `i3`_ - after trying it out,
I’ve now completely switched over and really like the ease of use and
increased functionality it provides.

`Tiling window managers`_ allow me to manage my screen space much more
efficiently and mean I can work within multiple windows easily. I like
the simplicity of `i3`_, it allows for `3 container layouts`_
splith/splitv, stacking, tabbed. I also find it **very** easy to modify
your keyboard mappings via a simple (plain text rather than a `lua`_
config file in the case of awesome wm) file in your home directory.
`~/.i3/config`_.This config file is created for you based on default
settings when you first use i3.

.. image:: /images/i3/i3-screen-thumb.png
   :alt: i3 example screenshot
   :align: center
   :height: 394px
   :width: 700px

`View a screenshot`_

I didn’t need to add much to mine, just some short cuts I would need,
suspend/lock (I’m using `i3lock`_ - which comes with the i3 suite) - the
defaults are sane and get’s you up and running quickly.

`i3`_ has good support for multi monitors and uses `xrandr`_ by default.

What is most impressive is not only the simplicity of the configuration
but the speed of it, and the minimal memory space it occupies. The
`docs`_ are extremely well laid out and answer almost all questions you
may have. There is a good `google tech talk video on i3`_ from `Michael
Stapelberg`_ outlining the design decisions they took and why they
decided to built yet another window tiling manager.

My main reasons for switching are:

-  Speed
-  Simplicity
-  Complete test suite
-  Clean design
-  Great documentation

If you are using or considering switching to a tiling manager, I
recommend trying `i3`_, if you are using ubuntu or debian it’s even
easier to install as you can use their `repositories`_.

.. _awesome: http://awesome.naquadah.org/
.. _i3: http://i3wm.org
.. _Tiling window managers: http://en.wikipedia.org/wiki/Tiling_window_manager
.. _3 container layouts: http://i3wm.org/docs/userguide.html#_changing_the_container_layout
.. _lua: http://www.lua.org/
.. _~/.i3/config: https://gist.github.com/simonhayward/11316105
.. _i3lock: http://i3wm.org/i3lock/
.. _xrandr: http://xorg.freedesktop.org/wiki/Projects/XRandR
.. _docs: http://i3wm.org/docs/
.. _google tech talk video on i3: http://www.youtube.com/watch?v=QnYN2CTb1hM
.. _Michael Stapelberg: http://michael.stapelberg.de/
.. _repositories: http://i3wm.org/docs/repositories.html
.. _View a screenshot: /images/i3/i3-screen.png
