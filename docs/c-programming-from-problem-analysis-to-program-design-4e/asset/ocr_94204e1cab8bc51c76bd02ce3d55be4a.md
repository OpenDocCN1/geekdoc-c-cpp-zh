# EXAMPLE 14.18

```
memberDataAdap.Fill(memberDS, "memberTable");
```

The Fill() method can be used without writing additional SQL statements because you instantiated an object of the command builder class. The command builder automatically generates SQL statements for the InsertCommand, UpdateCommand, and DeleteCommand properties of the DataAdapter class. You could set the value for each of these properties in exactly the same manner you set the SelectCommand property—using a string containing a SQL statement.

**NOTE** If your application requires that the dataset contain values from two or more tables, you cannot have the command builder class automatically generate the SQL statements for you. In this case, you have to set the InsertCommand, UpdateCommand, and DeleteCommand properties of the DataAdapter class. You do this by setting the DataAdapter object’s InsertCommand property with a SQL INSERT statement, DeleteCommand property with a SQL DELETE statement, and UpdateCommand property with a SQL UPDATE statement.

That is all that is required to retrieve records from a database. To show the contents of the table and enable the user to make changes, a presentation user interface layer is needed. The table values could be displayed on the console screen or on a control in a Windows application. The grid control is especially well suited to dataset objects. The next section explains how to bind a dataset object to a data grid on a Windows application.

**Adding a DataGridView Control to Hold the Dataset** To see the data from the database, the records can be placed in a DataGridView object on a Windows form. The DataGridView control creates a structure that is divided into rows and columns much like the structure you associate with a relational database table. In addition to being able to navigate around in the data grid, you can make changes by editing current records as well as to insert and delete new records. To tie the DataGridView object to the dataset, use the DataSource and DataMember properties of the dataGridView object, as shown in Example 14-19.

# EXAMPLE 14.19

```
dataGridView1.DataSource = memberDS;
dataGridView1.DataMember = "memberTable";
```

**NOTE** There are over 50 different Windows.Forms controls that can be added to your application. Not all are shown in the dropdown list. Additional ones can be added to the ToolBox using the **Choose ToolBox Items** from the **TOOLS** menu.