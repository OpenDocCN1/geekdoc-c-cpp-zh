# Introduction to ADO.NET

| Methods | Descriptions |
|---|---|
| Dispose | Releases the resources used by the DataAdapter. |
| Fill | Add or refreshes rows in the DataSet to match those in the data source using the DataSet name, and creates a DataTable. Adds a DataTable to the specified DataSet. |
| GetParameters | Gets the parameters set by the user when executing a SQL statement. |
| ToString | Returns a String representing the Component, if any. This method should not be overridden. |
| Update | Calls the INSERT, UPDATE, or DELETE statement for each inserted, updated, or deleted row in the specified DataSet from a named DataTable. |

FIGURE 3.21 The public methods of the DataAdapter class.

# 3.4.4.3 The Methods of the DataAdapter Class

The DataAdapter has more than 10 methods to help users develop professional data-driven applications. Figure 3.21 lists some of the most frequently used methods.
Among these, the **Dispose**, **Fill**, **FillSchema** and **Update** are among the most often used methods. The **Dispose()** method should be used to release the DataAdapter after the DataAdapter completes its job. The **Fill()** method should be used to populate a DataSet after the Command is initialized and ready to be used. The **FillSchema()** method should be called if you want to add a new DataTable into the DataSet, and the **Update()** method should be used if you want to perform some data manipulations as Insert, Update and Delete with the database and the DataSet.

# 3.4.4.4 The Events of the DataAdapter Class

Two popular events are widely used in the DataAdapter class, and these events are listed in Figure 3.22.
Before we can complete this, an example coding is provided to show readers how to use the DataAdapter to perform some data and actions between your DataSet and your database. Figure 3.23 shows an example of using a SQL ServerDataAdapter (assuming that a Connection object **SqlConnection** has been created).
Starting from step A, an SQL SELECT statement is created with other object declarations, such as a new instance of SqlCommand and a new instance of the DataSet. The DataSet class will be discussed in the following section and the **Fill()` method of the DataAdapter can be used to populate the data tables embedded in the DataSet.
In step B, the SqlCommand object is initialized with the Connection object, **CommandType** and the command string.
The instance of the SqlDataAdapter, sqlDataAdapter, is initialized with the command string and the SqlConnection object in step C.
In step D, the SqlSqlCommand object, sqlCommand, is assigned to the SelectCommand property of the sqlDataAdapter is initialized and cleared to make it ready to be filled by executing the **Fill()` method of the sqlDataAdapter to populate the table in the DataSet.
The **Fill()** method is called to execute a population of data from the Faculty table into the mapping of that table in the DataSet step E.

| Events | Descriptions |
|---|---|
| Disposed | Occurs when the component is disposed by a call to the Dispose method. |
| FillError | Returned when an error occurs during a fill operation. |

FIGURE 3.22 The events of the DataAdapter class.