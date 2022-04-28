.. post:: Apr 28, 2022
   :tags: blog
   :author: Famke Bäuerle

.. role:: bash(code)
   :language: bash

First Thoughts
==============

This blog will serve as a personal archive where I can (publicly) not stuff that I want to remember or that I might find helpful another day. I must admit that this was heavily inspired by `Sam Nicholls Blog <https://samnicholls.net/>`_. This post today will teach me how to setup a blog from scratch. This might prove useful for converting some (or all) of the plain html websites that I am currently responsible for:

* `Faktor 14 Magazin <https://www.faktor14magazin.de/>`_
* `StudSciCom Initiative <https://www.stud-scicom.de/>`_
*  `Pantoffeln im Regen Podcast <https://www.pantoffelnimregen.de/>`_

At first glance I thought that using simple HTML / CSS / Js templates that I only need to adapt and maintain would be enough to host those websites permanently. This is not true. Especially for the now very "blog stlyed" website of Faktor 14 where we need to keep track of all cross-links within the site and also update them by hand. This is a really tideous task that I want to automate. 

However all of these websites are up and running with designs that I quite like. So the first taks after publishing this first post will be to customize this blog and see how the :file:`_templates` directory works in doing so. All of this must also be teachable to others since I plan to collaborate (more) on the stuff that is published to the above mentioned websites.

Some Takeaways:
---------------
* I had to configure an SSH key to make :bash:`ablog deploy` work, with the setup described below this will no longer be needed. 
* I can edit the blog and have a preview with :bash:`ablog build` and :bash:`ablog serve`. If i am satisfied with result, I can add, commit and push the changes.
* I separated the source of the website (the files written in rst) and the repository which hosts the website (html files) and connected those with a github actions script called :file:`deploy.yml`.
* I added my API-TOKEN to the secrets of the :file:`website` repository (the repo where I push from) as described `here <https://github.com/cpina/github-action-push-to-another-repository>`_. This is needed for the github actions script called :file:`deploy.yml`
* The :file:`.nojekyll` is necessary to have the blog rendered correctly.

.. code-block:: yaml
   :caption: github actions script to deploy the website automatically

   name: deploy-website

   on:
   workflow_dispatch:
   push:

   jobs:
   deploy-website:
      runs-on: ubuntu-latest
      steps:
      - uses: actions/checkout@v2

      - name: Set up Python 3.8
         uses: actions/setup-python@v2
         with:
         python-version: 3.8.6

      - name: Install dependencies
         run: pip install ablog

      - name: Build the site
         run: ablog build
         
      - name: Create .nojekyll file
         uses: 1arp/create-a-file-action@0.2
         with:
            path: '_website'
            file: '.nojekyll'

      - name: Push to .github.io repository
         uses: cpina/github-action-push-to-another-repository@main
         env:
         API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}
         with:
         source-directory: '_website'
         destination-github-username: 'famosab'
         destination-repository-name: 'famosab.github.io'
         user-email: famke.baeuerle@gmail.com
         target-branch: master
