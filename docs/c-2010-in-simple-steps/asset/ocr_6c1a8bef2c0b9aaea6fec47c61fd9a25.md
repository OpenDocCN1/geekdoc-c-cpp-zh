8 Right-click the project name LINQtoSQL in Solution Explorer (Fig.C#-10.14).

9 Select Add→New Item from the context menu, as shown in Fig.C#-10.14:

![](bbox=[0.18, 0.17, 0.78, 0.32])

Fig.C#-10.14

The Add New Item dialog box opens.

10 Select LINQ to SQL Classes in the middle pane and enter the name MyClass.dbml in the Name text box in the Add New Item dialog box.

11 Click the Add button.

The MyClass.dbml class is added to the LINQtoSQL application. As you click the Add button, the Object Relational Designer window opens. You can drag tables from Server Explorer, drop them in the Object Relational Designer window, and retrieve data from the tables that you have added. In our case, we have added the Products table from the NORTHWND database.

12 Open the Server Explorer window (Fig.C#-10.15).

> **Tip**
> Alternatively, you can open the Server Explorer window by clicking the View menu on the menu bar of the Visual Studio 2010 IDE and then selecting Server Explorer from the drop-down menu that appears. You can also press the CTRL+W, L keys in combination to open the Server Explorer window.

13 Click the triangle glyph in front of the Data Connections node in the Server Explorer window to expand the Data Connections node (Fig.C#-10.15).

14 Select a database connection and click the triangle glyph in front of it to expand it. In our case, we have selected the temp-pc\sqlexpress.D:\SQL SAMPLE DATABASE\NORTHWND.MDF.dbo database connection (Fig.C#-10.15).

15 Click the triangle glyph in front of the Tables node to expand it and view the tables inside the NORTHWND database (Fig.C#-10.15).

16 Drag the Products table from the Tables node and drop it in the Object Relational Designer window, as shown in Fig.C#-10.15.