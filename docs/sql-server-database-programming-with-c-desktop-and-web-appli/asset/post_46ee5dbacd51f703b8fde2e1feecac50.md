
# 574 SQL Server Database Programming with C#

M. The ExecuteNonQuery() method is called to perform this data insertion query to insert a new course record into the Course table in our sample database. This method will return an integer to indicate the number of rows that have been successfully inserted into the database.

N. If this returned integer is zero, which means that no rows have been inserted into the database and this insertion is failed, a warning message is assigned to the member SQLInsertError and our method ReportError() is called to report this error.

O. The third query, which is used to retrieve all courses, including the newly inserted course, from the database based on the input faculty_id, is assigned to the SqlCommand property of the Command object.

P. The dynamic parameter facultyID is initialized with the faculty_id obtained from the first query as we did above.

Q. The initialized Command object is assigned to the SelectCommand property of the DataAdapter.

R. The Fill() method of the DataAdapter is used to retrieve all courses, including the inserted courses, from the database and add them into the DataSet dsCourse.

S. Finally the DataSet that contains the updated course information is returned to the calling procedure.

Compared with the first method, it appears that more codes are involved in this method. Yes, it is true. however, this method has two functions: inserting data into the database and validating the inserted data from the database. In order to validate the data insertion for the first method, the second Web method must be executed. Therefore, from the point of data insertion and validation process, the third Web method has less code than the first one.

Now let's run our service project to test this Web method using the built-in Web interface. Click on the Insert button to run the project and click on our third Web method InsertDataSet from the built-in Web interface to start it. The parameters wizard is displayed, which is shown later in Figure 9.62. After entering the following parameters into each associated Value box of a new course:

| FacultyName | Ying Bai |
| :--- | :--- |
| CourseID | CSE-665 |
| Course | Advanced Robotics |
| Schedule | T-H: 1:30-2:45 PM |
| Classroom | MTC-309 |
| Credit | 3 |
| Enroll | 32 |

Your finished parameter wizard should match one that is shown in Figure 9.62.
Click on the Invoke button to run this Web method to perform this new insertion. The running result is shown in Figure 9.63.

All six courses, including the sixth CSE-665 that is the newly inserted course, are displayed in the XML format or tags in this running result.

A point to be noted is that you can only insert this course record into the database one time, which means that you cannot continue to click on the Invoke button to perform another insertion with the same course information since the data to be inserted into the database must be unique.

Click on the Close button that is located at the upper-right of this Web interface to terminate our service. Next let's develop our fourth method.

# ASP.NET Web Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_603_0.png)

FIGURE 9.62 The finished input parameter wizard.

![](img/d59a47501d0a20fc0460a49c469c6fb7_603_1.png)

FIGURE 9.63 The running result of the third web method.

# 9.4.2.5 Develop the Fourth Web Method GetInsertCourse()

The function of this method is to retrieve the detailed course information from the database based on the input course_id. This method can be consumed by a client procedure when users want to get the detailed course information such as the course name, schedule, classroom, credit, enrollment and faculty_id when a course_id is selected from a ListBox.

Because this is a single query, you can use either a normal query or a stored procedure if you want to reduce the coding load for this method. Relatively speaking, a stored procedure is more efficient with a normal query, so we prefer to use a stored procedure to perform this query.

Now let's create our stored procedure WebSelectCourseSP.

# 9.4.2.1 Create the Stored Procedure WebSelectCourseSP()

Open Visual Studio 2022 and the Server explorer window, click on the arrow in front of our sample database folder CSE_DEPT and then expand the Stored Procedures folder. To create a new stored procedure, right-click on this folder and select the item Add New Stored Procedure to Open the New Stored Procedure wizard.

Enter the codes that are shown later in Figure 9.64 as shown in Figure 9.64, and click on the Update button on the Open Database button then click on the Review Database Updates to save this new stored procedure. A successful update message will be displayed in the Data Operations box at the bottom if everything is fine.

To test this procedure, right-click on this newly created stored procedure (you may need to refresh the Stored Procedures folder to see this added one). Then select the item Execute from the popup menu to run the Stored Procedure wizard.

Enter CSE-438 into the Value box in this as the input course_id and click on the OK button in Figure 9.65. The result is displayed in the Results window, which shown that 6 queries are retrieved from our database, from the Course table, and displayed in this. Our stored procedure works. Right-click on our database CSE_DEPT in the Server Explorer and select the item Close Connection from the popup menu to close this connection.

# 9.4.2.2 Develop the codes for our fourth Web method GetInsertCourse() to call this stored procedure to perform the information query.

Open the main service page WebServiceInsert.asmx and add the codes that are shown in Figure 9.66 into this page to create this method.

Let's take a look at this method to see how they might use.

![](img/d59a47501d0a20fc0460a49c469c6fb7_604_0.png)

Figure 9.64 The codes for the stored procedure WebSelectCourseSP().

# ASP.NET Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_605_0.png)

FIGURE 9.65 The result of running the stored procedure SelectCourseSP().

![](img/d59a47501d0a20fc0460a49c469c6fb7_605_1.png)

FIGURE 9.66 The code for the web method GetInsertCourse().

# 578 SQL Server Database Programming with C#

The function of this method is to retrieve the detailed course information from the database based on the input course_id. This method can be consumed by a client procedure when users want to get the detailed course information such as the course name, schedule, classroom, credit, enrollment and faculty_id when a course_id is selected from a ListBox.

Because this is a single query, you can use either a normal query or a stored procedure if you want to reduce the coding load for this method. Relatively speaking, a stored procedure is more efficient with a normal query, so we prefer to use a stored procedure to perform this query.

Now let's create our stored procedure WebSelectCourseSP.

# 9.4.2.1 Create the Stored Procedure WebSelectCourseSP()

Open Visual Studio 2022 and the Server explorer window, click on the arrow in front of our sample database folder CSE_DEPT and then expand the Stored Procedures folder. To create a new stored procedure, right-click on this folder and select the item Add New Stored Procedure to Open the New Stored Procedure wizard.

Enter the codes that are shown later in Figure 9.64 as shown in Figure 9.64, and click on the Update button on the Open Database button then click on the Review Database Updates to save this new stored procedure. A successful update message will be displayed in the Data Operations box at the bottom if everything is fine.

To test this procedure, right-click on this newly created stored procedure (you may need to refresh the Stored Procedures folder to see this added one). Then select the item Execute from the popup menu to run the Stored Procedure wizard.

Enter CSE-438 into the Value box in this as the input course_id and click on the OK button in Figure 9.65. The result is displayed in the Results window, which shown that 6 queries are retrieved from our database, from the Course table, and displayed in this. Our stored procedure works. Right-click on our database CSE_DEPT in the Server Explorer and select the item Close Connection from the popup menu to close this connection.

# 9.4.2.2 Develop the codes for our fourth Web method GetInsertCourse() to call this stored procedure to perform the information query.

Open the main service page WebServiceInsert.asmx and add the codes that are shown in Figure 9.66 into this page to create this method.

Let's take a look at this method to see how they might use.

![](img/d59a47501d0a20fc0460a49c469c6fb7_604_0.png)

Figure 9.64 The codes for the stored procedure WebSelectCourseSP().

# ASP.NET Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_605_0.png)

FIGURE 9.65 The result of running the stored procedure SelectCourseSP().

![](img/d59a47501d0a20fc0460a49c469c6fb7_605_1.png)

FIGURE 9.66 The code for the web method GetInsertCourse().

The function of this method is to retrieve the detailed course information from the database based on the input course_id. This method can be consumed by a client procedure when users want to get the detailed course information such as the course name, schedule, classroom, credit, enrollment and faculty_id when a course_id is selected from a ListBox.

Because this is a single query, you can use either a normal query or a stored procedure if you want to reduce the coding load for this method. Relatively speaking, a stored procedure is more efficient with a normal query, so we prefer to use a stored procedure to perform this query.

Now let's create our stored procedure WebSelectCourseSP.

# 9.4.2.1 Create the Stored Procedure WebSelectCourseSP()

Open Visual Studio 2022 and the Server explorer window, click on the arrow in front of our sample database folder CSE_DEPT and then expand the Stored Procedures folder. To create a new stored procedure, right-click on this folder and select the item Add New Stored Procedure to Open the New Stored Procedure wizard.

Enter the codes that are shown later in Figure 9.64 as shown in Figure 9.64, and click on the Update button on the Open Database button then click on the Review Database Updates to save this new stored procedure. A successful update message will be displayed in the Data Operations box at the bottom if everything is fine.

To test this procedure, right-click on this newly created stored procedure (you may need to refresh the Stored Procedures folder to see this added one). Then select the item Execute from the popup menu to run the Stored Procedure wizard.

Enter CSE-438 into the Value box in this as the input course_id and click on the OK button in Figure 9.65. The result is displayed in the Results window, which shown that 6 queries are retrieved from our database, from the Course table, and displayed in this. Our stored procedure works. Right-click on our database CSE_DEPT in the Server Explorer and select the item Close Connection from the popup menu to close this connection.

# 9.4.2.2 Develop the codes for our fourth Web method GetInsertCourse() to call this stored procedure to perform the information query.

Open the main service page WebServiceInsert.asmx and add the codes that are shown in Figure 9.66 into this page to create this method.

Let's take a look at this method to see how they might use.
