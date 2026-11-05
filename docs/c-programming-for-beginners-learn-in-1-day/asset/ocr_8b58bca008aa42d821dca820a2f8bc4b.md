+   a. SQLCommand – This data type is used to define objects which are used to perform SQL operations against a database. This object will hold the SQL command which will run against our SQL Server database.
+   b. The dataadapter object is used to perform specific SQL operations such as insert, delete and update commands.
+   c. We then define a string variable, which is SQL to hold our SQL command string.
+   2. The next step is to actually define the SQL statement which will be used against our database. In our case we are issuing an update statement, this will update the Tutorial name to “VB.Net Complete” while the TutorialID is unchanged and kept as 3.
+   3. Next, we will create the command object, which is used to execute the SQL statement against the database. In the SQL command, you have passed the connection object and the SQL string.
+   4. In our data adapter command, we now associate the insert SQL command to our adapter. We also then issue the ExecuteNonQuery method which is used to execute the Update statement against our database.
+   5. We finally close all the objects related to our database operation. Remember this is always a good practice.

When the above code is set, and the project is executed using Visual Studio, you will get the below output. Once the form is displayed, click the Connect button.

# **Output:-**