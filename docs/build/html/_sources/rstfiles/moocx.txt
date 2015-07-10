MOOCX
======

We are currently working towards an installable package. 
Users will be able to execute the input and output of data from the commandline.

.. warning::
    At the moment MOOCX can only generate a few csv reports, all database setup needs to be executed using individual python scripts and import commands outlined in this documentation.

Installation
------------

Download the repo and run :code: python setup.py install

Requirements
------------

McGillX uses [Python 2.7](https://www.python.org/download/releases/2.7/) scripts to populate and analyze a [Mongo Database](https://www.mongodb.org/). In order to execute the following setup you will need to have python 2.7, mongodb and [PyMongo](https://api.mongodb.org/python/current/) installed on your machine. Note some scripts require the installation of specific python libraries in order to run.


MOOCX Package Contents
----------------------

+---------------------------------+---------------------------------------------------------------------------------------------------------------+
| Directory                       | Description                                                                                                   |
+=================================+===============================================================================================================+
| edx\_data\_research/parsing     | Contains the scripts and procedures used to load the raw data (json, sql, csv, mongodb) from edx to MongoDB   |
+---------------------------------+---------------------------------------------------------------------------------------------------------------+
| edx\_data\_research/reporting   | Contains scripts that were used for extracting and aggregating data for analysis                              |
+---------------------------------+---------------------------------------------------------------------------------------------------------------+
| edx\_data\_research/cli         | Command line interface                                                                                        |
+---------------------------------+---------------------------------------------------------------------------------------------------------------+




