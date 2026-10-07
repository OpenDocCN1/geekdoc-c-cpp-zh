# 272

# SQL Server Database Programming with C#

One can try to change the query method by the DataReader by selecting it from the Query Method combobox to perform some queries for other students.

Click on the Back and Exit buttons to terminate our operation. Our project used to call two stored procedures is very successful!

Some readers may find that these two stored procedures are relatively simple, and each contains only one SQL statement. Ok, let's dig a little deeper and develop some sophisticated stored procedures and to call them from our Visual C# project. Next we will develop a stored procedure that contains SQL statements.

# 5.16.5 Query Data Using More Complicated Stored Procedures

Now we want to get all courses (each course_id) taken by the selected student based only on the student name from the StudentTable. To do that, we must first go to the Student table based on the associated student_id based on the student name since there is no student name column available in the StudentTable. Then we can go to the StudentTable to pick all course_id based on the selected student_id. We need to perform two queries to simplify this data-retrieving operation. Now we combine these two queries into a single stored procedure to simplify our data-querying operation. First let's create our stored procedure.

Open Studio.NET and the Server Explorer window, and click on the arrow-symbol icon on the left of our database to connect to our database if this database was added to the Server Explorer. Otherwise you need to right click on the Data Connections folder to add and connect to our database.

Right-click on the Stored Procedures folder and select the Add New Stored Procedure item to open the Add Procedure wizard, and then enter the codes that are shown in Figure 5.102 into this new procedure.

Let's give a detailed discussion for this piece of codes.

+   A. The stored procedure is named dbo.StudentCourseInto.
B. The input parameter is the student name, @stdName, which is a varchar-char variable with a maximum character limit of 50. All parameters, no matter input or output, must be declared inside the braces.

![](bbox=[0.156, 0.631, 0.843, 0.903])

FIGURE 5.102 A new stored procedure – StudentCourseInto.