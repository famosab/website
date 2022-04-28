.. post:: Apr 28, 2022
   :tags: blog
   :author: Famke Bäuerle

First Thoughts
==============

This blog will serve as a personal archive where I can (publicly) not stuff that I want to remember or that I might find helpful another day. I must admit that this was heavily inspired by `Sam Nicholls Blog <https://samnicholls.net/>`_. This post today will teach me how to setup a blog from scratch. This might prove useful for converting some (or all) of the plain html websites that I am currently responsible for:

* `Faktor 14 Magazin <https://www.faktor14magazin.de/>`_
* `StudSciCom Initiative <https://www.stud-scicom.de/>`_
*  `Pantoffeln im Regen Podcast <https://www.pantoffelnimregen.de/>`_

At first glance I thought that using simple HTML / CSS / Js templates that I only need to adapt and maintain would be enough to host those websites permanently. This is not true. Especially for the now very "blog stlyed" website of Faktor 14 where we need to keep track of all cross-links within the site and also update them by hand. This is a really tideous task that I want to automate. 

However all of these websites are up and running with designs that I quite like. So the first taks after publishing this first post will be to customize this blog and see how the ``_templates`` directory works in doing so. All of this must also be teachable to others since I plan to collaborate (more) on the stuff that is published to the above mentioned websites.

Some Takeaways:
+ I had to configure an SSH key to make ``ablog deploy`` work
+ Storing everything on github proves to be more complicated than expected