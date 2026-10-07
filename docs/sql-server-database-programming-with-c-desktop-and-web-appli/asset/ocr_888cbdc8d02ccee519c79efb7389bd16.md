# SQL Server Database Programming with C#

| Constructors | Descriptions |
| :--- | :--- |
| DataTable() | Initializes a new instance of the DataTable class with no arguments. |
| DataTable(String) | Initializes a new instance of the DataTable class with the specified table name. |
| DataTable(String, String) | Initializes a new instance of the DataTable class using the specified table name and namespace. |

**FIGURE 3.34** Three primary constructors of the DataTable class.

```
DataSet FacultyDataSet;
DataTable FacultyTable;
FacultyDataSet = new DataSet();
FacultyTable = new DataTable("Faculty");
FacultyDataSet.Tables.Add(FacultyTable);
```

**FIGURE 3.35** An example of adding a DataTable to a Dataset.

When you first create a DataTable, it does not have a schema (that is, a structure). To define the schema of the table, you must create and add Column objects to the Columns collection of the table. You can also define a primary key for the table and create Constraint objects of the table. After you have defined the schema for the DataTable, you can add rows of the table by adding DataRow to the Rows collection of the table.

You are not required to supply a value for the TableName property at any time, or when you create a DataTable; however when you add a table without a TableName value to a Dataset, it will be given an incremental default name of Table, starting with "Table" for "Table1".

Figure 3.35 shows an example of creating a new DataTable and a Dataset, and then adding the DataTable into the Dataset.

First, you need to create an instance for Dataset and DataTable classes. Then you can add your new DataTable into the new Dataset by using the Add() method.

# 3.4.7.2 The DataTable Properties

The DataTable class has more than 20 properties. Figure 3.36 lists some most used properties. Among these properties, the Columns and Rows properties are very important to us, and both properties contain a collection of DataColumn objects in the current DataTable and each column in the table can be considered as a DataColumn object, and can be added to this collection. A similar situation happens with the Rows property contains a collection of DataRow objects that are composed of all rows in the current DataTable object. You can get the total number of columns and rows from the current DataTable by calling these two properties.

# 3.4.7.3 The DataTable Methods

The DataTable class has about 50 different methods with 33 public methods, and Figure 3.37 lists some most used methods.

Among these methods, three are important to us: NewRow(), ImportRow() and LoadDataRow(). Calling the NewRow() adds a row to the table using the existing table, but with default values for the row, and sets the RowState to Added. Calling the ImportRow preserves the existing RowState along with other values in the row. Calling the LoadDataRow() is to find and update a row from the current data table. This method has two arguments, the Value (Object) and the Accept Condition (Boolean). The Value is used to update the row that is found and