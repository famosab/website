.. post:: Apr 28, 2022
   :tags: blog
   :author: Famke Bäuerle

.. role:: bash(code)
   :language: bash

Building a blog with ablog, github-pages and github-actions
===========================================================

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
