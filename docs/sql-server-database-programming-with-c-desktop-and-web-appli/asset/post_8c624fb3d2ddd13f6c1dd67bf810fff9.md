
# SQL Server Database Programming with C#

| Record Name | Record Value |
| --- | --- |
| student id | T77896 |
| student name | Toney Black |
| gpa | 3.28 |
| credits | 52 |
| major | Information System Engineering |
| schoolYear | Sophomore |
| email | tblack@college.edu |
| sblimage | David.jpg |

**Figure 9.114** The updated record for the student Tom Erica.

![](img/d59a47501d0a20fc0460a49c469c6fb7_650_0.png)

**Figure 9.115** The running status of the student updating process.

Now let's select some other student's name for the *Student Name* **Select** to get related information for that student. Then select the updated student's name **Toney Black** from the same combobox and click the **Select** button again to get the updated information for that student. You can find that all information related to that student, as shown in Figure 9.115. Our data updating action is successful!

To test the deleting function, keep the current student **Toney Black** selected and click on the **Delete** button to delete this record from the *Student Form*. Click on the popup MessageBox to confirm this deletion. If this deletion action is successful, all pieces of information related to this student would be deleted from our sample database and Student Form window.

To confirm this data deleting action, click on the **Select** button to retrieve all pieces of information for the deleted student. Immediately a warning message is displayed to indicate that no matched student found.

# ASP.NET Web Services 623

Click on the Back and Exit buttons to terminate your client project. The client project is very successful. However, the story is not finished. It is highly recommended that you recover that deleted student record for your Student since we want to keep our database neat and complete. You can recover this record by using one of the following methods:

- 1) Using the Server Explorer window in Visual Studio.NET to open our database CSE_DEPT and our Student data table, and add the original record.
- 2) Using the Microsoft SQL Server Management Studio to open our sample database CSE_DEPT and our Student data table and add the original record.

Refer to Figures 9.108, 9.109, and 9.110 in Section 9.5.5.2 to complete this recovery job since all records for the deleted student in all tables, using the Login, Student and StudentCourse, also deleted. The recovery order is: First recover the deleted record in the Student table since it is a part table and the student_id is a primary key in that table, then do recovery jobs for other tables.

To recover the image in the Student table, you can just enter a NULL to column and perform another updating action by running this project. Alternatively, one can use RTOInsertProject or RTOInsertProject, which are Exercises 4 and 5 in the homework on Chapter 6, to insert that original record if you completed any of them. However, you must first delete the updated student record before you insert the original record since they used the student_id.
A Windows-based client project can be found from the folder ClassDB\Chapter 9\SPUpdateDelete is located on the CRC Press ftp site (refer to Figure 1.2 in Chapter 1).

# 9.7 WEB-BASED CLIENT PROJECT TO CONSUME THE WEB SERVICES

There is no significant difference between building a Windows-based and a Web-based client project to consume a Web service. To save the time and space, we can create a new ASP.NET Web Application (.NET Framework) project, and then add and modify a Student page to consume our Web service project.
This section can be developed in the following sequences:

- 1) Create a new-brand ASP.NET Web Application (.NET Framework) project WebClientSQLUpDt and add an existing Web page Student.aspx from the folder Web Forms that are the Students folder on the CRC Press ftp site (refer to Figure 1.2 in Chapter 1) into our new project.
- 2) Add a Web service reference to our Web project.
- 3) Add and build codes in the related methods to the Student.aspx file to call the Web method to perform our data updating and deleting. The code additions and modifications include the following sections:

- A. Build the codes inside Back click method.
- B. Develop the codes for the Update button click method.
- C. Develop the codes for the Delete button click method.

Now let's start with the first step listed above.

# 9.7.1 CREATE A NEW ASP.NET WEB APPLICATION PROJECT AND ADD AN EXISTING WEB PAGE

Open Visual Studio.NET and go to the File | New Project item to create a new ASP.NET Web Application (.NET Framework) project. Enter WebClientSQLUpDtProject into the Name box and C:\Location box, click on the Create button, select the Web Forms and click on the Create button on the next page to create this project.

# SQL Server Database Programming with C#

On the opened project Solution Explorer window, right-click on our new project WebClientSQLUpdProject, and select the Add | Existing Item from the popup menu to open the Add Existing Item window. Browse to the folder Web Forms which is under the Students of the CRC ftp site (refer to Figure 1.2 in Chapter 1). Select the items Student.aspx, Student.aspx.designer.cs and Student.aspx.cs by checking them one by one, and click the Add button to add these items.

Perform the following operations:

- 1) Right-click on Student.aspx in the Solution Explorer, select the Properties window, and set the Action property to Content File.
- 2) Double-click Student.aspx to open the design view.
- 3) Rebuild the project to generate the designer code.

# 9.7.2 ADD A WEB SERVICE REFERENCE AND MODIFY THE WEB FORM

Right-click on the project in the Solution Explorer, select Add | Service Reference. In the dialog box, enter the URL of the web service and click Go. Set the namespace name and click OK. Now, open the Student.aspx code view and add the following code to handle the back button:

(Code omitted for back button)

# 9.7.3 BUILD THE CODES INSIDE BACK CLICK METHOD

Double-click the Back button in the designer view to generate the Back_Click event handler. Add the following code:

```csharp
protected void btnBack_Click(object sender, EventArgs e)
{
    Response.Redirect("Default.aspx");
}
```

# 9.7.4 ADD THE CODES TO UPDATE BUTTON METHOD

Double-click the Update button in the designer view to generate the Update_Click event handler. Add the following code to handle the data updating:

```csharp
protected void btnUpdate_Click(object sender, EventArgs e)
{
    // Code to update student information
}
```

# 9.7.5 DEVELOPMENT CODES FOR THE DELETE BUTTON CLICK

Double-click the Delete button in the designer view to generate the Delete_Click event handler. Add the following code to handle the data deleting process:

```csharp
protected void btnDelete_Click(object sender, EventArgs e)
{
    // Code to delete student record
}
```
