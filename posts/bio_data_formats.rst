.. post:: Feb 17, 2023
   :tags: data, biology
   :author: Famke Bäuerle

.. role:: bash(code)
   :language: bash

An overview on biological data formats and databases
====================================================

Since starting my degree in Bioinformatics I stumbled across so many data formats. Some of them I use regularly, but some are still a little bit misterious to me. So this post is thought as a collection of formats, their use and possible structure mainly for myself. But maybe it is of interest for someone else who might just be as confused as I was.

First of all: There is a difference between file format and file extension. 

File formats
------------

**FASTA files**

The FASTA format is a text-based format for representing either nucleotide sequences (GATCU) or amino acid (protein) sequences. The FASTA format means that each sequence begins with `>` which is followed by the sequence description in the same line and the sequence itself in the lines below.

* `.fas` and `.fa` are common shortenings of `.fasta`. files
* `.fna` is short for  **F**ASTA **N**ucleic **A**cids
* `.faa` is used by the NCBI for **F**ASTA **A**mino **A**cids (protein FASTA file)

**General Feature format**

The `GFF` format can be used to describe genes and other features of DNA, RNA and protein sequences.

**SBML**

The Systems Biology Markup Language is an XML based format to store computational models of biological processes.


Databases
---------

* GenBank: Open access sequence database hosted by the NCBI. Contains sequences for any organism submitted.
* RefSeq: Open access, annotated and curated sequence database hosted by the NCBI. Limited to major organisms for which sufficient data is available.