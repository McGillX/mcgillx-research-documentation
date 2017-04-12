C# Code documentation
==================================
This documents, file by file, the purpose and function of the C# code on Github. 
Note that the main method is in the **Program.cs** file. If you would like to simply try to make thing 'go' and skip the full documentation, you can just read that part. 

Program.cs
-------------------------------
This is the file that contains the Main method. It has several static attributes:

See the AppSettings.txt file included with the C# code for details on all of the private attributes. These are set in that file. 

The two below are not obtained from the AppSettings file, but are populated in the code when someone selects the problem_definition event type. 
*  HashSet<ProblemDefinition> allProblems. This keeps a set of all seen problem definitions. It then adds them to the table in bulk.
*  HashSet<QuestionDefinition> allQuestion. This has the same function as above, except for quesitons.

The main method of this program reads its settings from file, and the executes a command based on the value of the choice attribute. 

* test connection. This option just calls the connect() method to verify that the program can connect to the database.
* discussion dump. This option reads the mongo discussion files provided by edx and populates the discussion tables in the database
* course structure. This option reads the json course structure files provided by edx and populates the course_structure table.
* logs. This option calls the etUpTrackingLogs() method. Inside the logs methods, we open all of the subdirectories and *sort*. Sorting is highly advisable - without this step, there is no way to know where you need to start from if your connection dies - it is *not* guaranteed that all files in a directory will be opened in the same order between runs of a program. This will then call the ReadFile method. This method reads all of the lines in a trackng log file, and calls a different method depending on the value of EVENT_TYPE. For example, if EVENT_TYPE has the value "Discussion", it will call the DiscussionLogs method. There, it will check if the log in question represents a discussion event and, if it does, what kind of discussion event. It then calls the appropriate method from the BuildingObjects class to obtain the object representation of the log, and then send it to the appropriate method in the AddToTable class. 

 The methods for the various event types function in roughly the same way, except for ProblemLogs(). If the EVENT_TYPE is "Problem_Definitions", it will not immediately call an AddToTable method. Instead, it will call Create*Definitions and add to the Problem and Quesiton hashsets. At the end of the SetUpTrackingLogs() method, we can see that in the case of "Problem_Definitions", the last thing that happens is a call to both AddValues* methods in the AddToTable class. There, the contents of both hashsets will be inserted into their respective tables. 

Error Handling and Dead Connections
++++++++++++++++++++++++++++++++++++
If the connection dies, the active line and file numbers are written to a log file (you can change the location/file name). This allows up to pick up where we left off. This is especially useful when populating the larger tables, as sometimes things can die overnight. 

AddToTable.cs
-------------------------------
Almost all methods in this file follow the same formot, and have the same purpose: they add a particular log to the table indicated in the method name. The method names have the format AddRowTo*Table or AddValueTo*Table. 

The AddRowTo*Table methods all take as input the MySqlConnection, as well as an object containing all of the data for one row/log. They values contained in the input object are then extracted into a mysql query, and the query is executed. The query has the field names, and table names hard coded. If you would like to use different names in your database, you will have to go in and change the string literal values. 

The AddValuesTo*Table methods are for the problem and question definition tables. Because of the way in which to code extracts the problem/quesiton definitions, these two methods only take the connection as input. The HashSets containing the problem/question definitions are internal global static variables in the **Program.cs** file. 

This file also contains the createTrackingLogTableForCourse method that takes as input a connection and the name of the course. This method creates an all_logs table for a specific course. It it designed to be used in conjunction with the populateTrackingLogTableForCourse which takes the same input and copies rows from the all_logs table to the course specific table. This is useful if someone has access to view the data for only one specific course. 

The code that reads in the .mongo discussion files can be found in the void *ReadDiscussionDump* method. This method takes as input the location of the .mongo files, reads them all in, and then adds them to the db. In our logs, the data was stored in reverse chronological order. In order to meet foreign key constraints, it was important to insert the data in chronological order, so each file was parsed in reverse. 

Due to the edx students being from around the world, each line is force parsed in UTF-8 encoding. As an alternative, this could be omitted, but then non utf-8 logs would have to be discarded, or the settings in mysql could be updated to utf-16 encoding. Since we had very few logs in non-utf-8 encoding, it didn't make sense to double the size of the db to store just a few characters, so the decision was made to brute force convert them to utf-8. The Comment and CommentThread types are constructed separately, and then inserted into the db. 

This file also contains some private helper methods. 

AllLogEvents.cs
-------------------------------
This file contains the classes used to create the 'generic' tracking log objects that are used to populate data in the all_logs table. Since the exact fields included in the logs vary across event types, there are a few different options that are tried.


BuildingObjects.cs
-------------------------------

This file contains all of the methods used to normalize each JSON log into an object of the appropriate type. All of the methods take as input a single line from the tracking logs and return an object of the appropriate type. Most of these methods are fairly short; however, the BuildTrackingObjectProblem method is quite lengthy, as many of the fields in the problem_check event have ill defined types, and so there are additional type-checking steps included. It is also used for the Comment and CommentThread objects from the Mongodb. 

Course.cs
-------------------------------
This file contains a class that describes an edx course. This is no longer really used, and might be removed in later updates. 

ProblemEvents.cs
-------------------------------
This file contains all of the class definitions related to the problem_check event. There are three main 'parent' types: **ProblemDefinition**, **QuestionDefinition**, and **ProblemCheck**. 

DiscussionEvents.cs
-------------------------------
This file contains all of the class definitions related to the discussion forum tracking log events. The main 'parent' types are: **DiscussionSearch**, **DiscussionVote**, and **DiscussionTest**. 

MongoDiscussionData.cs
-------------------------------
This file contains all of the class definitions related to the mongo discussion events. The main 'parent' types are: **CommentEntry**, **ThreadEntry**.

VideoEvents.cs
-------------------------------

This file contains all of the class definitions related to the supported video events. The main 'parent' types are: **VideoSeek**, **VideoSpeed**, **VideoLoad**, and **VideoOther**. 

