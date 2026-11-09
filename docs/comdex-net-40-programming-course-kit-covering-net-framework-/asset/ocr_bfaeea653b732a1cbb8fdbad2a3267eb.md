![](bbox=[0.255, 0.136, 0.768, 0.335])

Fig.C#-6.29

After learning about the LINQ to Dataset technology, let’s now learn about the LINQ to SQL component.

# LINQ to SQL

LINQ to SQL is a component of .NET Framework 4.0 and is specifically designed to work with a SQL Server database. It allows you to write queries to retrieve and manipulate data from SQL Server database. In other words, by using LINQ to SQL, you can perform various operations, such as retrieving, inserting, updating, and deleting information from a table in a database. Visual C# 2010 provides you the functionality to create LINQ to SQL classes from the existing database. It also provides a simple way to bind the controls in your forms to your database.

LINQ to SQL creates an **Object-Relational Mapping (ORM)** layer between the tables in the SQL Server database and the objects in a Visual C# program. The ORM layer helps to exchange data between incompatible languages. This layer is created using the **Object Relational Designer**, which enables you to map LINQ to SQL classes to the tables in a database, and it is called LINQ to SQL ORM mapping. With the help of LINQ to SQL ORM mapping, the classes that match the database tables are created automatically from the database itself and you can start using these classes immediately.

Perform the following steps to implement LINQ to SQL in a Windows Forms application:

+   1. *Start* **VisualStudio2010**.
+   2. *Select* **File→New→Project** from the menu bar. The New Project dialog box opens.
+   3. *Select* **Visual C#→Windows** from the Installed Templates section in the left pane of the New Project dialog box. The project templates available for developing Windows-based applications in C# are displayed in the right pane of the New Project dialog box.
+   4. *Select* the **Windows Forms Application** template in the right pane to create a Windows Forms application.
+   5. Enter the name of the application as **LINQtoSQL** (also available on the CD) in the Name text box and an appropriate location for the application in the Location combo box.
+   6. *Click* the **OK** button to close the New Project dialog box. The **LINQtoSQL** application is created (Fig.C#-6.30).
+   7. *Drag and drop* a **ListView** control on the form from the Toolbox.
+   8. *Select* the **ListView** control in the form and click the right arrow button at the top right corner of the ListView control, as shown in Fig.C#-6.30.