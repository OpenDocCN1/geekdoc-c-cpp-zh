# Appendix B

# Creating a Database

SQL Server databases can be created in Visual Studio because the Express edition of SQL Server DBMS is automatically installed on your computer when you install Visual Studio.

# Tutorial: Creating HR Database

This tutorial creates a database called HR (for human resources) that includes a table named Employee (EmpId, LastName, FirstName, DateOfBirth, Phone, DeptNo, CountryId, Salary, FullTime).

Step B-1: Create a new project named Ch11_Databases and rename the form to EmpDirectory.

Step B-2: Create a new database as follows:

Select: Project, Add New Item, Service-based Database.

Change the name of the database to: HR.mdf, and Click: Add.

If the Data Source Configuration Wizard window opens, asking you information about the data source, click Cancel because currently there are no tables in the database.

Notice that the Solution Explorer now includes the HR database file. In addition, you will see the Server Explorer (or Database Explorer if you are using Visual Studio Express) on the left side of the form will show the name of the database, shown in Figure B-1. If the Server Explorer is not visible, select View, Server Explorer.

Figure B-1: Server Explorer

![](bbox=[0.078, 0.582, 0.31, 0.665])

Open the project directory, Ch12_Databases. You will see the database file, HR.mdf.

Step B-3: To add a table to the database, right click Tables and select Add New Table. You will see the Table Designer window, shown in Figure B-2.

Figure B-2: Table Designer window

![](bbox=[0.078, 0.804, 0.575, 0.933])