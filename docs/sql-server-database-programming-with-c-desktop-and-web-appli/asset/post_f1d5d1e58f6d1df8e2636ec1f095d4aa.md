
# Accessing Data in ASP.NET

505

![](img/d59a47501d0a20fc0460a49c469c6fb7_533_0.png)

Another way to test this student record updating action is to open the Student table via the Server Explorer window to verify whether or not that new student record has been updated.

Next let's take care of data deleting action by building our codes in the Delete button's Click method in the project current.

## 8.9.3.3 The Coding for the Data Deleting Query

Open our WebSP_Student Project, double-click on the Delete button from the Design View of the Student page to open its click method, and enter the codes in Figure 8.99 into that method.

```sharp
protected void cmdDelete_Click(object sender, EventArgs e)
{
    cse_dept.deleteStudentSP(txtStudentName.Text);
    Photobox.ImageURL = null;
    CurrentStudent();
    ClearStudent();
}
```

**FIGURE 8.99** The detailed codes for the delete button's click method.

# SQL Server Database Programming with C#

The function of this piece of code is straightforward and easily understood.

- A. The first stored procedure deleteStudentSP we built in Server 8.9.3.1 is executed to delete the selected student record from the student's name.
- B. The selected student's image is also deleted from the PhotoBox by assigning a null to the property ImageUrl.
- C. All current students' names in our sample database are retrieved and added into the Student Name combobox. Also, all selected textboxes are cleaned up to indicate that the selected student's record has been deleted from our database.

Now run project, finish the login process and open the Student page. To test our data deleting action, select a student's name, such as Jennifer Bai, from the Student Name combobox, and click on the Delete button to delete that record.

To confirm that data deletion action, go to the Student Name combobox, and one can find that the selected student has been deleted and cannot be found from there. Another way to verify this student deleting action is to open the Student table via the Server Explorer to verify whether new student record has been deleted.

Click on the Back button to return our application to the Selection page, and then click on the Exit button to terminate our Web application.

A complete Web application project WebSP_Student Project contains the data updating and deleting actions can be performed by a class DB Projects> Chapter 8:WebSP_Student Solution is under the Students folder on the CRC Press flip site (refer to 1.2 in Chapter 2).

## 8.10 CHAPTER SUMMARY

A detailed and commented introduction to the ASP.NET and the .NET Framework, including ASP.NET 4.8, is provided at the beginning of this chapter. This is especially useful and important to readers or students who have no knowledge or background in the Web application developments and implementations.

Following the introduction section, a detailed discussion on how to install and configure the environment to develop ASP.NET Web applications is provided. Some essential tools, such as the Web server, IIS and FrontPage Extension 2000, as well as the installation process of these tools, are introduced and discussed in detail.

Starting from Section 8.3, detailed developments and building processes of ASP.NET Web applications to access SQL Server database are discussed with seven real Web application projects. The seven ASP.NET Web applications are as follows:

- 1) ASP.NET Web application to select and display data from the Faculty table in the Microsoft SQL Server database.
- 2) ASP.NET Web application to insert data into the Faculty table in the Microsoft SQL Server database.
- 3) ASP.NET Web application to update and delete data from the Faculty table in the Microsoft SQL Server database.
- 4) ASP.NET Web application to perform actions with LINQ to SQL query.
- 5) ASP.NET Web application to select and display data for the Course table.
- 6) ASP.NET Web application to insert data into the Course table.
- 7) ASP.NET Web application to update and delete data from the Student table in the SQL Server database with the stored procedures.

The stored procedures with the entity class and object of the DataContext are utilized in the last project to help readers or students to perform different actions against our sample Server database more efficiently and conveniently. The detailed discussion on the data action order is provided to help readers understand the integrity constraint built in the relational database. It is a tough topic to update or delete data from related tables in a relational database, and a clear and deep discussion on this topic will significantly benefit readers and improve their knowledge and hands-on experience of these issues.

# HOMEWORK

## I. TRUE/FALSE SELECTIONS

- 1. The actual language used in the communications between the client and the server is HTML.
- 2. ASP.NET and .NET Framework are two different models that provide the development environments to the Web programming.
- 3. The .NET Framework is composed of the Common Language Runtime (called runtime) and a collection of class libraries.
- 4. You can access the .NET Framework by using the class libraries provided by the .NET Framework, and implement the .NET Framework using the tools such as Visual Studio.NET provided by the .NET Framework, too.
- 5. ASP.NET 4.8 is a programming framework built on the .NET Framework 4.8 and it is used to build Web applications.
- 6. The fundamental component of ASP.NET is the Web Form. A Web Form is the Web page users view one or more Web Forms.
- 7. A Web Form is a dynamic page that runs on the server side. It can access server resources when it is viewed by users via the client browser.
- 8. Similar to traditional Web pages, an ASP.NET 4.x Web page can only run scripts on the client side.
- 9. The controls you added to the Web form will run on the server when this Web page is requested by the user through a client browser.
- 10. To allow a List Box to respond to a user click as the Web page runs, the AutoPostBack property of List Box must be set to False.

## II. MULTIPLE CHOICES

- 1. When the user sends a request from the client's browser to request a Web page, the server needs to build that form and sends it back to the user's browser in the language format.
  a. ASP.NET
  b. .NET Framework
  c. XML
  d. HTML

- 2. Once a requested Web page is received by the client's browser, the connection between the client and the server is
  a. Still active
  b. Terminated
  c. Not active
  d. Either active or inactive

- 3. As a Web application runs, the programs developed in any .NET-based language are converted into the ______ codes that can be recognized by the CLR, and the CLR can compile and execute the MSIL codes using the Just-In-Time compiler.
  a. Visual Studio
  b. Basic.NET
  c. Microsoft Intermediate Language (MSIL)
  d. C#

- 4. The terminal file of an ASP.NET Web application is a ______ file.
  a. Dynamic Linked Library (dll)
  b. MSIL
  c. XML
  d. HTML

- 5. Because Web pages are frequently refreshed by the server, one must use the ______ to store the global variable.
  a. Global.asax file
  b. Default.aspx file
  c. Config file
  d. Application state function

- 6. One needs to use the ______ method to display a message box in Web applications.
  a. MessageBox.Show()
  b. MessageBox.Display()
  c. Javascript alert()
  d. Response.Write()

- 7. Unlike the Windows-based applications that use the Form_Load as the first event method, a Web-based application uses the ______ as the first event method.
  a. Start_Page
  b. Page_Load
  c. First_Page
  d. Web_Start

- 8. To delete data from a relational database, one must first delete the data from the ______ tables, and then one can delete the data from the ______ table.
  a. Major, minor
  b. Parent, child
  c. Parent, parent
  d. Child, parent

- 9. To allow the SQL Server database engine to delete all related records from the child tables, the Delete Rule item in the INSERT AND UPDATE Specifications box of the Foreign Key Relationship dialog box must be set to ______.
  a. No action
  b. Cascade
  c. Set default
  d. Set Null

- 10. To display any message on a running Web page, one must use the ______ method.
  a. MessageBox.Show()
  b. Response()
  c. Response.Redirect()
  d. Response.Write()
