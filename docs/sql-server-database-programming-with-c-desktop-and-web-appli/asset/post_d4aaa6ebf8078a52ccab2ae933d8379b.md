
# ASP.NET Services

| WebServiceInsertPoint | FillCourseDetail() |
|---|---|

```csharp
protected void FillCourseDetail(ref SQLInsertRecord sResult, SqlDataReader sReader)
{
    sReader.Read();
    sResult.FacultyID = System.Convert.ToString(sReader("facultyID"));
    sResult.Course = System.Convert.ToString(sReader("course"));
    sResult.Schedule = System.Convert.ToString(sReader("schedule"));
    sResult.Classroom = System.Convert.ToString(sReader("classroom"));
    sResult.Credit = System.Convert.ToInt32(sReader("credit"));
    sResult.Enrollment = System.Convert.ToInt32(sReader("enrollment"));
}
```

**FIGURE 9.6** The codes for FillCourseDetail() method.

C. Each column of queried course record is assigned to the associated member data in our child class. Two system methods, Convert.ToString() and Convert.ToInt32(), are used to convert all data to the appropriate types for assignment. For a point this one can use a System namespace on the top of the page by adding it using System; to directly use the Convert class without prefixing the System.

Now let's build and run our project to this web method. Click the IIS Express button to run the project. Select our method GetCourse() from the built-in Web interface, enter CSE-665 as the course id into the Value box, and then click on the Invoke to run this web method. The result of this method is displayed in Figure 9.68.

Six pieces of course information are displayed in XML tags. Recall that the course_id as array Course[] with a dimension of 10 in our child class. This member data is used to GetFirst() for our second web method. Since we did not use it in this method elements the CourseID[] array are to true and displayed in this resulting file.

![](img/d59a47501d0a20fc0460a49c469c6fb7_607_0.png)

**FIGURE 9.68** The running result of our web method GetInsertCourse().

# 580 SQL Database Programming with C#

Click on the Close button that is located at the upper-right corner of this Web interface to terminate our service. A complete Web service project WebServiceInsert can be found from a folder ClassDB Projects\Chapter 9\WebServiceInsert that is under the Students folder at the CRC Press filter (refer to Figure 1.2 in Chapter 1).

At this point, we have finished all code jobs in our Web project in the service side. Next we need to develop some professional Windows-based and Web-based application projects with beautiful graphic user interfaces to use or consume the Web service application developed in this Web service project WebInsertProject. Those Windows-based and Web-based applications can be developed as Web service clients.

## 9.4.3 Build Windows-Based Clients to Consume The Web Services

To use or consume a Web service, we first need to create a Web service proxy class in our Windows- or Web-based applications. Then we can create a new instance of the Web service proxy class and execute the desired Web service methods in that service class. The process of creating a Web service proxy class is equivalent to add a Web reference to our Windows-based or Web-based applications.

### 9.4.3.1 Create a Windows-Based Consumer and a Web Service Proxy Class

Basically, adding a Web reference to our Windows-based or Web-based applications is to execute a search. During this process, Visual Studio.NET 2022 will find to all Web services available to our applications.

Open Visual Studio.NET 2022 in the Administrator mode and create a new C# Windows Forms App (.NET Framework) and name it as WinClientInsertProject and save it to the folder C:\Chapter 9.3.11 to Let add a Web reference to our new project. Refer to Section 9.3.12 to start this Web reference. Perform the following operations to finish this:

- Open our Web service project WebInsert, and click on the IIS button to run it.
- Copy the URL from the Address bar in running Web service project.
- Then open our Windows-based client WinClientInsertProject from the Solution Explorer,
- Right click on the client Add | Service Reference from the popup menu to open Add Service Reference.
- Click on the Advanced button located at the lower-left corner on this window to open Service Settings.
- Click on the Add Reference button to open the Web Reference wizard, which is shown in Figure 9.6.
- Paste that URL we copied from step 2 into the URL box in Add Reference wizard and click on the button to begin Visual Studio.NET search for it.
- When the Web service is found, the name of our service is displayed in the right pane, which is shown in Figure 9.6.
- Alternatively you can change the name for this Web reference from localhost to any meaningful, such as WS_SQLInsert, in our class. Click on the Add Reference button to add Web service as new client project.
- Click on the Close button from Web service window to terminate our project.

Immediately, you can find that the Web service WS_SQLInsert, which is under the folder References, has been added to the Solution Explorer in our client project. This reference is the Web service proxy class.

![](img/d59a47501d0a20fc0460a49c469c6fb7_608_0.png)

# ASP.NET Web Services

581

![](img/d59a47501d0a20fc0460a49c469c6fb7_609_0.png)

**FIGURE 9.6** The finished web reference wizard.

Next let's develop the graphic interface by adding useful controls to interface to our service and to display course information.

### 9.4.3.2 Develop the Graphic User Interface for the Client

Perform the following modifications to new client project:

- Rename the Form Object from the default name Form1.cs to our desired name WinClient.cs.
- Rename the Window Form from the default name Form1 to our desired name CourseForm by modifying the Name property of the window.
- Rename the form from the default title Form1 to CSE_CourseForm by modifying the Text property of the form.
- Change StartPosition property of the form window to CenterScreen.

To save time and space, we can use the Course form located in the project RTOUpdateDelete we developed in Chapter 7 as our graphic interface. You can find this project from the folder ClassDB Projects\Chapter7\RTOUpdateDelete is under the Students folder on the CRC Press site to refer (Figure 1.2 in Chapter 1). Perform the following operations to add this Course into new client project:

- Open the project RTOUpdateDelete Project and the Course form window from the CRC Press site.
- Select all controls from that form by going to Edit | Select All and going to Edit | Copy menu item to copy all controls selected from this window.
- Return to our Windows-based client WinClientInsert Project, open our form window CourseForm and paste those controls we copied from step 2 into this form.

# 502 SQL Database Programming with C#

![](img/d59a47501d0a20fc0460a49c469c6fb7_610_0.png)

**FIGURE 9.7** The finished graphic user interface.

Your finished graphic user interface is shown in 9.7. The purpose of the Query Method combobox control is to select two different methods opened in our service project to get desired course information:

- Stored Procedure Method that uses a stored procedure to insert a new course record into the database.
- DataSet Method that uses queries to insert a new course record into the database and returns a DataSet that contains the detailed course information.

The Faculty Name combobox control is used to select desired faculty member as the input parameter to the Web methods to insert and pick the desired course record.

In this application, the Insert, Select and Back buttons are used. The Insert button is used to trigger a data insertion action, the Select button is used to trigger a data validation action to confirm data insertion and the Back button is used to terminate our project.

The detailed functions of this project include:

- Insert Data Using the Stored Procedure Method: when the project runs, this method and a faculty name as a new course record stored in six textboxes have been selected and entered. The Insert button is clicked by the user. Our client project built on our Web service via the Reference provided, and call the selected Web method SetInsertSP() to run the stored procedure to insert that new course record into our sample database.
- Insert Data Using the DataSet Method: if this method is selected, the Web method InsertDataSet() built in our Web service will be called to execute queries to perform this new course insertion. In addition, all courses, which include the newly inserted course, taught by the selected faculty that works as an input to this method, will be retrieved and stored into a DataSet, and that DataSet will be returned to our client project.
