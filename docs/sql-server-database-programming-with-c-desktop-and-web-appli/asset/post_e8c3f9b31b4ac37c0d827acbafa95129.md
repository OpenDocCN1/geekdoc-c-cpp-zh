
# 536

# SQL Server Database Programming with C#

| WebServiceSelect Project | FillFacultyReader() |
| --- | --- |
| protected void FillFacultyReader(ref SQLSelectResult sreader, SQLDataReader sreader) {

if (sreader.Read() == true) {
  sResult.Id = Convert.ToString(sreader["faculty_id"]);
  sResult.Title = Convert.ToString(sreader["title"]);
  sResult.Office = Convert.ToString(sreader["office"]);
  sResult.Phone = Convert.ToString(sreader["phone"]);
  sResult.College = Convert.ToString(sreader["college"]);
  sResult.Email = Convert.ToString(sreader["email"]);
  sResult.Image = (byte[])sreader["Image"];
}
}

**FIGURE 2.21** The codes for the method FillFacultyReader().

| WebServiceSelect Project | ReportError(SQLSelectResult ErrSource) |
| --- | --- |
| protected void ReportError(SQLSelectResult ErrSource) {

  ErrSource.SQLRequestOK = false;
}

**FIGURE 9.22** The codes for the subroutine ReportError().

The key point for this method is the passing mode for the first argument. A passing-by-reference mode is used for our returning object and is equivalent to return an address of the passed object from a function.
The codes for another user-defined method ReportError() are shown in Figure 9.22.
The input parameter to this subroutine is our returning object. A *False* is assigned to the SQLRequestOK member data and the error message is assigned to the SQLError string variable in our class SQLSelectBase. Since our returning object is instantiated from our child class SQLSelectResult that is inherited from our base, our returning object can access and use those member data defined in the base class.
At this point, we finished all coding for our Web service project. Now let's run our project to test the data query functionality. Click on the IIS Express button to run the project and the built-in Web interface, which is shown in Figure 9.23.

![](img/d59a47501d0a20fc0460a49c469c6fb7_564_0.png)

**FIGURE 9.23** The running status of the web service.

![](img/d59a47501d0a20fc0460a49c469c6fb7_565_0.png)

**FIGURE 9.24** The status of our web method.

Click on our method GetSQLSelect to open the built-in Web interface for our Web method, which is shown in Figure 9.24. Enter the faculty name *Ying Bai* into the FacultyName box as an input Value, and then click on the Invoke button to execute the Web method to trigger the ASP.NET runtime to perform our data query.

The running result is returned and displayed in the XML format, which is shown in Figure 9.25. Each returned data is enclosed by a pair of XML tags to indicate its firstly. For example, **B78880**, which the queried *faculty_id* is enclosed by the tag `<FacultyId>...</FacultyId>`, and the name of this tag is defined in our class SQLSearchResult. Our first Web service method is very successful.

As mentioned before, a Web service did not provide any interface and one needs to develop some users to consume the service we want to display pieces of information from the Web Services, a built-in Web interface is provided by Microsoft

![](img/d59a47501d0a20fc0460a49c469c6fb7_565_1.png)

**FIGURE 9.25** The running result of our web service project.

to help users display queried information from the Web services. In most real applications, users
need to develop user interfaces to perform these data displaying or other operations.
Click on the Close button that is located at the upper-right corner of the page to close our Web
service project.

## 9.3.8 Develop a Stored Procedure to Perform the Data Query in Web Service

An optional and better way to perform the data query via Web service is to use the stored procedures.
The advantage of using this method is that the coding process can be greatly simplified and most
query jobs can be performed in the database side. Therefore, the query execution speed can be faster.
The query efficiency can also be improved and the query operations can be integrated into a single
group or block of code body to strengthen the integrity of the query.

### 9.3.8.1 Develop the Stored Procedure WebSelectFacultySP

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
Click on the Close button that is located at the upper-right corner of the page to close our Web
service project.

## 9.3.2 Add Method to Stored Procedure

To distinguish from the first method, we have added another method to perform this. To do that, we copy the coding body of our first method, including both the header and the code body. Perform the modifications shown in Figure 9.28 to this **GetSQLSelectSP**. The modified parts are highlighted in blue. Let's have a closer look at this code to show how this method works.

- A Change the method's name by adding two letters SP to the end of the original method's name, and the new method's name becomes GetSQLSelectSP.
- B Change the content of the query string `cmdString` to `dbo.WebSelectFacultySP`; to call a stored procedure from Web project, the content of the query string must be equal to the name of stored procedure. Otherwise a running error may be encountered during the project runs.
- C Change the `CommandType` property of the Command object from `CommandType.Text` to `CommandType.StoredProcedure`. This change is very important since we need to call a stored procedure to perform the data query. We must tell the ASP.NET runtime that a stored procedure should be called when the command is executed.

Now run the project to test this new method. Click on the second method **GetSQLSelectSP** as the project runs, enter a desired faculty member as Yang Bai in the FacultyName box and click on **Invoke** to run it. The same running result as we got from the last project can be obtained. You can see how easy it is to develop codes to perform the data query by calling the stored procedure in the Web service.

Next we discuss how to use a DataSet as the returning object to contain all pieces of information from running a Web service project.

### 9.3.9 Use DataSet as the Returning Object FOR THE WEB METHOD IN WEB SERVICE

The advantage of using DataSet as the returning object for the Web method is that we do not need to create any application class to instantiate an object. Another advantage is that DataSet can contain multiple records from the different tables, and we do not need to create multiple member data in our application class to hold those data items. Finally, the size of our coding body could be greatly reduced when a DataSet is used, especially for a large block of data that is queried via the Web service project.
