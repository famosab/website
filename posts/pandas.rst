.. post:: Jan 24, 2023
   :tags: python
   :author: Famke Bäuerle

.. role:: bash(code)
   :language: bash

Collection of pandas 'hacks'
============================

I regularly stumble upon the same issues when using pandas. There is a wonderful documentation but I sometimes lack the time to read through all of it. This page is intended to help me remember stuff that I already did.

How to transform a Multi-Index DataFrame with one column into a table with columns and rows
-------------------------------------------------------------------------------------------

If you end up with a table that has two three columns from which you want one as rows, one as columns and the entries, do the following:

* set the index to a Multi-Index with the columns which should turn into the columns and rows
* sort this index to remove duplicate entries
* transform it to allow turning into a table
* stack it to obtain a table
* if you want you can remove column and index names and keep only level 1 of the Multi-Index to obtain a cleaner table

.. code-block:: python
   :caption: pandas

    df.set_index(['colum1','colum2']).sort_index().T.stack()
    df.columns.name = None
    df.index.names = (None, None)
    df.index.name = None
    df.index = df.index.get_level_values(1)

Graphical representation of what this does:

.. flat-table:: Title
   :header-rows: 1

   * -
     - food
     - property
     - numerical value
   * - 0
     - pear 
     - taste
     - 57
   * - 1
     - tomato
     - taste
     - 60
    * - 2
     - peach
     - taste
     - 55
    * - 3
     - pear 
     - color
     - green
   * - 4
     - tomato
     - color
     - red
   * - 5
     - peach
     - color
     - pink

.. flat-table:: Title
   :header-rows: 1
   * -
     - taste
     - color
   * - peach
     - 55
     - pink
   * - pear
     - 57
     - green
   * - tomato
     - 60
     - red  
