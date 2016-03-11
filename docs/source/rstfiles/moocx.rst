MOOCX
======

Installation
------------

Download the repo and run :code: python setup.py install

Requirements
------------

McGillX uses `Python 2.7`_ scripts to populate and analyze a `Mongo Database`_. In order to execute the following setup you will need to have python 2.7, mongodb and `PyMongo`_ installed on your machine. Note some scripts require the installation of specific python libraries in order to run.

.. _Python 2.7: https://www.python.org/download/releases/2.7/
.. _Mongo Database: https://www.mongodb.org/
.. _PyMongo: https://api.mongodb.org/python/current/


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




