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

.. list-table:: Title
   :widths: 25 25 25 25
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
+--------+-----------+----------------------+---------------------+
|   | model | medium    | numerical value  |                     |
+========+===========+======================+=====================+
| 0      | pear  | taste                   | 57.823951783569846  |
| 1      | tomato  | taste                   | 59.67999088948053   |
| 2      | peach  | taste                   | 50.33647865242004   |
| 3      | orange  | taste                   | 50.62443366153196   |
| 4      | apple  | taste                   | 27.682989245440137  |
| 5      | pear  | color                   | 75.80515258921106   |
| 6      | tomato  | color                   | 75.18930666754245   |
| 7      | peach  | color                   | 74.42379457475845   |
| 8      | orange  | color                   | inf                 |
| 9      | apple  | color                   | 46.81581083984173   |
| 10     | pear  | SNM3                 | 63.47756297402682   |
| 11     | tomato  | SNM3                 | 63.26914442036741   |
| 12     | peach  | SNM3                 | 56.20027628042825   |
| 13     | orange  | SNM3                 | 53.88541260594831   |
| 14     | apple  | SNM3                 | 28.51221018471888   |
| 15     | pear  | shape                 | 60.018016799064014  |
| 16     | tomato  | shape                 | 61.91412975986793   |
| 17     | peach  | shape                 | 55.771298747719904  |
| 18     | orange  | shape                 | 52.63825837197864   |
| 19     | apple  | shape                 | inf                 |
| 20     | pear  | cooking time               | 75.81617006462481   |
| 21     | tomato  | cooking time               | 75.20032414295646   |
| 22     | peach  | cooking time               | 74.4348120501725    |
| 23     | orange  | cooking time               | inf                 |
| 24     | apple  | cooking time               | 46.83827301353397   |
+--------+-----------+----------------------+---------------------+

.. list-table:: Title
   :widths: 25 25 25 25 25
   :header-rows: 1
+-----------+--------------------+---------------------+--------------------+---------------------+
|           | cooking time       | taste               | color              | shape                | 
+===========+====================+=====================+====================+=====================+
| apple     | 46.83827301353397  | 27.682989245440137  | 46.81581083984173  | inf                 | 
| pear      | 75.81617006462481  | 57.823951783569846  | 75.80515258921106  | 60.018016799064014  | 
| peach     | 74.4348120501725   | 50.33647865242004   | 74.42379457475845  | 55.771298747719904  | 
| orange    | inf                | 50.62443366153196   | inf                | 52.63825837197864   | 
| tomato    | 75.20032414295646  | 59.67999088948053   | 75.18930666754245  | 61.91412975986793   | 
+-----------+--------------------+---------------------+--------------------+---------------------+
