The changes in LINQ to SQL in the .NET Framework 4.0 include enhancements in terms of query compilation and performance improvements. In addition to this, now you do not need to worry about encountering exceptions or facing system crashes when unexpected data types are encountered. With .NET Framework 4.0, the LinqDataSource control introduces support for inherited entities and types.

> A LinqDataSource control is a Web server control that can be used on an ASP.NET Web page. Using a LinqDataSource control helps you to connect to data on a database or in an in-memory collection of data, such as an array.

Now, let’s create a Windows application, LINQtoSQL, to learn the implementation of LINQ to SQL. For this, perform the following steps:

+   1. Repeat steps 1 to 3 shown earlier while creating the LINQQuery application in the Explaining LINQ Queries and their Execution section of this chapter.
+   2. Enter LINQtoSQL in the Name text box to specify the name of the application, and enter an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The LINQtoSQL application is created.
+   4. Set the Size property of Form1 in the Properties window to 680, 450, as shown in Fig.C#10.12:

![](bbox=[0.35, 0.38, 0.61, 0.52])

+   5. Add a ListView control to Form1.
+   6. Click the smart tag and select the Tile option from the View drop-down list in the ListView Tasks menu (Fig.C#10.13).
+   7. Select the Dock in Parent Container option from the ListView Tasks pane, as shown in Fig.C#10.13:

![](bbox=[0.26, 0.62, 0.75, 0.8])

After setting the properties of the listView1 control, the next step in creating the LINQtoSQL application is to add a LINQ to SQL class. For this, let’s proceed to the next step.