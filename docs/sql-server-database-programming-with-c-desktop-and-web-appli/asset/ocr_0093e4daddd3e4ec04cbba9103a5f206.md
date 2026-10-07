to help users display queried information from the Web services. In most real applications, users
need to develop user interfaces to perform these data displaying or other operations.
Click on the Close button that is located at the upper-right corner of the page to close our Web
service project.

# 9.3.8 Develop a Stored Procedure to Perform the Data Query in Web Service

An optional and better way to perform the data query via Web service is to use the stored procedures.
The advantage of using this method is that the coding process can be greatly simplified and most
query jobs can be performed in the database side. Therefore, the query execution speed can be faster.
The query efficiency can also be improved and the query operations can be integrated into a single
group or block of code body to strengthen the integrity of the query.

# 9.3.8.1 Develop the Stored Procedure WebSelectFacultySP

Now let's first develop our stored procedure in the Server Explorer window in Visual.NET
environment.
Open the Studio.NET and open the Server Explorer window, then click on the small arrow
icon in front of our SQL Server to expand our database. Then right click on the
 Procedures folder and select the item Add Stored Procedure from the popup menu to make
a new stored procedure. Enter the codes that are shown in Figure 9.26 into this code body as
new stored procedure.
Click on the Update item shown in Figure 9.26 and the Update Database to save this new
stored procedure with a name of dbo.WebSelectFaculty.
Now one can expand the Stored Procedures folder in the Server Explorer to check and confirm this
created stored procedure. Right click on folder and select the Refresh item if you cannot find it.
We can run this stored procedure in the Visual.NET environment to confirm its function.
Right click on the newly created stored procedure from the popup menu to open the Run Stored Procedure
wizard. Select the faculty name Yi Bai in the Value box as the input parameter and click on the OK
to run it. The result is displayed in the Output window that is located at the bottom of
this wizard, which is shown in Figure 9.27.
All queried (7) columns, that include the faculty_id, title, office, phone, college, email and
im in the faculty table, are displayed in this Result window. You need to move the horizontal bar
at the bottom to see all of these columns.
Our stored procedure is successful.
Now let's handle the coding development in our Web service project to collect this stored procedure
to perform this data query.

![](bbox=[0.105, 0.725, 0.895, 0.913])

FIGURE 9.26 The stored procedure dbo.WebSelectFacultySP.