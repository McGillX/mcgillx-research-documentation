.. McGillX Research Documentation documentation master file, created by
   sphinx-quickstart on Fri Jul 10 09:49:11 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

McGillX Research Documentation
=================================================

This is a public repository documenting the tools developed and used by the
McGillX research team to package, analyse, and manipulate the data that
is collected through McGill’s online courses offered via the edX
platform.

Contents:

.. toctree::
   :numbered:
   
   rstfiles/getting_started
   rstfiles/edx_data_download_and_decryption
   rstfiles/setting_up_the_mongo_databases
   rstfiles/moocx
   rstfiles/moocx_data_parsing
   rstfiles/moocx_report_generation
   

Getting Started
===============

If you are hosting courses on edx.org, before starting the setup consult with edX to setup keys and credentials for data transfer.

The McGillX Research Platform (moocx) is underdevelopment. At present only report generation (data exports) can be run from the moocx command line interface; all setup and import is still perform using individual scripts. Following the workflow below will walk you through downloading and decrypting data from edX, uploading it to a mongo database and installing the moocx python package for creating csv extracts for analysis.

Workflow Overview
-----------------

.. figure:: ../../images/mcgillx-database-structure-and-workflow.png

Open Issues
-----------


Contact
-----------

Contact McGillX for questions or assistance with setup:

McGillX - <mcgillx.tls@mcgill.ca>

Contribute
----------

If you would like to add new scripts, improve existing scripts, or found an error in the script feel free to send a pull request or raise an issue.


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

