The Object Relational Designer (O/R Designer) then launches so that you can visually edit the databases and tables you want to use. Open the Server Explorer window, and connect to the pubs sample database. Drag and drop the publisher and title tables onto the design surface of DataClasses.dbml (see Figure 17-5).

![](bbox=[0.15, 0.23, 0.85, 0.53])

Figure 17-5

Save the DataClasses.dbml file by pressing Ctrl+S. When you save the file, Visual Studio 2008 persists out .NET classes that represent the entities and database relationships that you have just added. For each LINQ to SQL designer file you add to your solution, a custom DataContext class is generated. It is the main object that you use to manipulate the table. In this example, the DataContext class is named DataClassesDataContext.

Be sure to save DataClasses.dbml before proceeding.

# Data Binding Using the GridView Control

To display the records from a table, you can use the GridView control, which displays the values of a data source in a table where each column represents a field and each row represents a record. Drag the GridView control from the Toolbox and drop it onto the design surface of Default.aspx. In the SmartTag of the GridView control, select <New data source ...> in the Choose Data Source dropdown list (see Figure 17-6).

![](bbox=[0.15, 0.91, 0.85, 0.98])

Figure 17-6