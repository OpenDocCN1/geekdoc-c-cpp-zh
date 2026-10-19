Figure 12-1: Relationship between database tables, data table and controls on a form

![](bbox=[0.08, 0.09, 0.33, 0.35])

We will use the wizard to create the necessary objects and to help you work with the data.

# 12.2 Creating Database Objects

To create the database object, first, you specify the data source—that is, the source of data, its type and location. The data source could be a database on the local computer or on a server, or a web service or other object.

Next, you drag the data table to the form to create the controls that display the data and objects that bind the controls to the data table.

# Specifying the Data Source

You specify the data source using the Data Source Configuration Wizard, which in turn generates the data tables and other objects, like the binding source.

# Tutorial 1: Display Employee Records Using the Wizard

Let’s create an application that lets you work with a human resource database that includes an Employee table.

Step 1-1: Create a new project named Ch12_Databases. Rename the form to EmployeeTabularView.

Step 1-2: Copy the SQL Server database file HR.mdf from Tutorial_Starts/DataFiles folder to a local directory outside the project directory, Ch12_Database. Appendix B provides instructions on how to create a new database in Visual Studio.

Step 1-3: To start the Data Source Configuration Wizard, click Project from the menu, and click Add New Data Source. You will see the Configuration Wizard window, as shown in Figure 12-2.