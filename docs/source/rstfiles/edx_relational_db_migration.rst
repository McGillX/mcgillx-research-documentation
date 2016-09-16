Migration to MySql
==================================
Documentation for moving the McGillx reserach data to a relational db.
We used mysql (since its free) but the mechanism for any other db should be similar.

All code for migrating JSON to mysql is in C# and will be made available on our github at a later date.


Constructing the db
-------------------------------
Here is a list of the tables present in our database in alphabetical order.

- all_logs
- auth_user
- auth_userprofile
- certificates_generatedcertificates
- courses
- courseware_studentmodule
- forum_searched
- forum_text_created
- forum_text_voted
- problem_definition
- problem_submission
- question_definition
- question_submission
- student_anonymoususerid
- student_courseenrollment
- student_languageproficiency
- teams
- teams_membership
- user_id_map
- video_events

Note that McGill offers several courses every year, and often re-offers the same course over the years. As such, we manually created  the courses table to hold the course ids for each course.
This has been very helpful in ensuring that each uploaded log has a valid course id with it (much of the data from edx is incomplete or otherwise garbled).
Our courses table has the following format:

=========   ================== 
Field           Type   
=========   ==================
id            vachar(255)
offering      tinyint(4)
code          varchar(20)
title         varchar(255)
term          varchar(200
startDate     date
endDate       date
=========   ==================

A sample entry might look like:

course-v1:McGillX+ATOC185x+1T2016  3 ATOC185x Natural Disasters  1T2016 2016-01-13 2016-04-08

This entry describes the third offering of the course titled Natural Disasters. The id for this course is course-v1:McGillX+ATOC185x+1T2016.
The course code is ATOC185x, and it was offered in the winter term of 2016. It started on January 13, and ended on April 8. 

Uploading sql files
-----------------------


Once you have downloaded and decrypted the datapackage with the sql files, you are ready to create the tables and upload the files to your database.
The precise syntax for table creation and file uploads will likely depend on which database management system you are using. 
If you are using MySql, you can upload each file by using the *load data local infile* command. An example is shown below for the auth_user table.

.. code:: mysql

  load data local infile 'pathTofile/auth_user.sql' into table auth_user 
  FIELDS TERMINATED BY '\\t' LINES TERMINATED BY '\\n'  
  IGNORE 1 LINES (id,username,first_name,last_name,email,
  password,is_staff,is_active,is_superuser,last_login,date_joined,
  status,email_key,avatar_typ,country,show_country,date_of_birth,
  interesting_tags,ignored_tags,email_tag_filter_strategy,
  display_tag_filter_strategy,consecutive_days_visit_count,course_id) 
  SET course_id='McGillX/CHEM181x_2/3T2014';

Since not all of the files provided by edx have a courses column, we added that ourselves. Be sure to first add the column in the table. Then, when you upload the file, you can set the value for each course using the SET command.


Uploading JSON files
--------------------------------
The section will detail how we parsed speficic event types in the JSON files from the tracking logs.



Video events
--------------------------
In video events, we dealt with the following event types:

- edx.video.closed_captions.hidden
- edx.video.closed_captions.shown 
- hide_transcript 
- load_video
- pause_video             
- play_video                
- seek_video             
- show_transcript         
- speed_change_video      
- stop_video            
- video_hide_cc_menu      
- video_show_cc_menu  

Forum events
------------------
In discussion forum events, we dealt with the following event types:

- edx.forum.response.created
- edx.forum.comment.created
- edx.forum.thread.created 
- edx.forum.response.voted
- edx.forum.thread.voted  
- edx.forum.searched

Problem events
-----------------------------
In problem events, we have only dealt with the following event type:

- problem_check

Below is a detailed sketch of the four tables involved in storing the problem_check details. 
Note that we define a *problem* as a non-empty set of questions which has a single 'submit' or 'check' button.
Every question belongs to a problem. A problem might have many questions.

.. figure:: ../../../images/problem_check_sketch.png
