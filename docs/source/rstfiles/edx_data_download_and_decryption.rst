edX Data Download and Decryption
================================

We use the file transfer client Cyberduck to access the amazon s3 server which stores edX data

1. Start Cyberduck
2. Click Open Connection
3. In the new window that opens:
 1. Select S3 (Amazon Simple Storage Service) from the dropdown
 2. Enter the Access Key ID and Secret Access Key which has been provided to you by edX
.. note::
  edX will provide a gpg encrypted txt file containing both the Access Key ID and Secret Access Key
 3. Click connect
 
Download the Course Package
---------------------------

1. Open the "/course-data" directory 
2. Download the lastest folder, it contains user profile and course information for all your institutions courses
3. Decompress the folder
4. Decrypt the files using [Kleopatra Gpg4win](http://gpg4win.org/) 

.. note::

    At McGillX we perform analysis post course offering and therefore use course data package generated just **after** a course has closed and certificates have been generated.
    
.. warning::

    The folder contains both edge and edx.org files.

Download the Tracking Logs
--------------------------

1. To access the tracking logs click "Go" from the top menu bar 

   Do not try finding the tracking logs in the default course directory

2. Select "Go to Folder"
3. In the new window that opens enter the file path "/edx-course-data" to access the tracking logs 
4. Find the name of your institution in the directory

   A directory with the following file structure should display:
 
   \insituition  
   -\edge  
   --\events  
   ---\YEAR  
   ----\InstitutionName-ex-events-YYYY-MM-DD.log.gz.gpg  
   
   -\edx  
   --\events  
   ---\YEAR  
   ----\InstitutionName-ex-events-YYYY-MM-DD.log.gz.gpg  

   The trackings logs are contained in the encrypted .gpg files
5. Download your files of interest
6. Decrypt the files using [Kleopatra Gpg4win](http://gpg4win.org/) 

.. note::

You do not need to extract the decompress the log.gz files. Our import script works with both the compressed gz and extracted log files.
