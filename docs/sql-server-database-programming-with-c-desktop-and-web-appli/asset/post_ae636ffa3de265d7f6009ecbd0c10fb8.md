
# SQL Server Database Programming with C#

# C# Window Form

![](img/d59a47501d0a20fc0460a49c469c6fb7_108_0.png)

FIGURE 3.28 A global representation of the DataSet and other data objects.

| Constructor | Functionality |
|--- |--- |
| DataSet() | Initializes a new instance of the DataSet class. |
| DataSet(String) | Initializes a new instance of a DataSet class with the given name. |

FIGURE 3.29 Popular constructors of the DataSet class.

A DataSet object provides you with an easier way to access the content of the data table fields through strongly typed programming. The so-called strongly typed programming uses information from the underlying schema, which means you can directly access and manipulate those data objects related to data tables. Another point is that a typed DataSet has a reference to an XML schema file and this file has an extension of .xsd. A complete description of the structure of all data tables included in the DataSet is provided in this schema file.

## 3.4.6.1 The DataSet Constructor

The first constructor is used to create a new instance of the DataSet class with a blank parameter. The second constructor is used to create a new instance of the DataSet with the specific name of the new instance.

## 3.4.6.2 The DataSet Properties

The DataSet class has more than 15 public properties. Figure 3.30 lists the most used properties.

| Property Name | Type | Functionality |
|--- |--- |--- |
| DataSetName | String | Gets or sets the name of the current DataSet. Gets a custom view of the data contained in the DataSet to allow filtering, searching, and navigating using a DataViewManager |
| DefaultViewManager | DataView | |
| HasErrors | Boolean | Gets a value indicating whether there are errors in any of the Data objects within the DataSet. |
| IsInitialized | Boolean | Gets a value that indicates whether the DataSet is initialized. |
| Namespace | String | Gets or sets the name of the DataSet. |
| Tables | DataTableCollection | Gets the collection of tables contained in the DataSet. |

FIGURE 3.30 Public properties of the DataSet class.

# Introduction to ADO.NET

| Method Name | Description |
| --- | --- |
| BeginInit | Begins the initialization of a DataSet that is used on a form or used by another component. The initialization occurs at run time. |
| Clear | Clears the DataSet of any data by removing all rows in it. |
| Copy | Copies the structure and data for this DataSet. Releases the resources used by the MarshalBy.Value.Component. |
| GetChanges | Gets a copy of the DataSet containing all changes since it was last changed. AcceptChanges was called. |
| HasChanges | Gets a value indicating whether the DataSet has changes, including new, deleted, or modified rows. |
| Load | Fills a DataSet with values from a source using the supplied DataReader. |
| Merge | Merges a specified DataSet, DataTable, or array of DataRow objects into the current DataSet or DataTable. |
| Reset | Resets the DataSet to its original state. Subclasses should override Reset to reset a DataSet to its original state. |
| ToString | Returns a string containing the name of the Component, if any. This method should not be overridden. |
| WriteXml | Writes data, and optionally the schema, from the DataSet. |
| WriteSchema | Writes the DataSet structure as an XML schema. |

**FIGURE 3.31** Public methods of the DataSet class.

| Event | Description |
| --- | --- |
| Disposed | Adds an event handler to listen to the Disposed event on the component. |
| Initialized | Occurs after the DataSet is initialized. |
| MergeFailed | Occurs when a target and source DataRow have the same key value, and EnforceConstraints is set to true. |

**FIGURE 3.32** Public events of the DataSet class.

Among these, the DataSetName, IsInitialized and Tables are the most often used in your data-driven applications.

## 3.4.6.3 The DataSet Methods

The DataSet has more than 30 public methods. Figure 3.31 lists the most frequently used methods.
Among those, the Clear(), Dispose() and Merge() method are often used. Before you can fill a DataSet, it is better to execute the Clear() method to clean up the DataSet to avoid any old data. Often in your applications, you may need to merge other DataSets or data arrays into the current DataSet by using the Merge() method. After you finished your query or action using the DataSet, you need to release it by executing the Dispose() method.

## 3.4.6.4 The DataSet Events

DataSet class has three public events and Figure 3.32 lists these events.
The Initialized event is used to make a indicate that the DataSet has been initialized to your applications. The MergeFailed event is triggered when a conflict occurs and the EnforceConstraints property is set to true as you want to merge a DataSet with an array of DataRow objects, another DataSet, or a DataTable.

Before we can this section, we need to show your guys how to create, initialize and implement a real DataSet object in a data-driven application. A piece of code shown in Figure 3.33 is used to illustrate these issues and a Sql Server Data Provider is utilized for this example. Assuming that a `SqlConnection`, `sqlConnection`, has been created and initialized for this example.

# SQL Server Database Programming with C#

- A A cmdString = "SELECT faculty_name, title, college FROM Faculty";
SqlCommand sqlCommand = new SqlCommand();
SqlDataAdapter sqlDataAdapter = new SqlDataAdapter();
DataSet sqlDataSet = new DataSet();
int intValue = 0;

- B sqlCommand.Connection = sqlConnection;
sqlCommand.CommandType = CommandType.Text;
sqlCommand.CommandText = cmdString;

- C sqlDataAdapter.SelectCommand = sqlCommand;
DataSet sqlDataSet = new DataSet();
sqlDataSet.Clear();

- D int intValue = sqlDataAdapter.Fill(sqlDataSet);
if (intValue == 0)
MessageBox.Show("No valid faculty found!");

- E sqlDataSet.Dispose();
sqlDataAdapter.Dispose();
sqlCommand.Dispose();

FIGURE 3.33 An example of using DataSet.

Starting from step A, some initialization joins are performed. An SQL SELECT statement is executed, an SqlCommand, an SqlDataAdapter object and a DataSet object are created. The integer variable intValue is used to return the value from calling the Fill() method.

In section B, the SqlCommand object is initialized by assigning the SqlConnection object to the Connection property, the CommandType.Text to the CommandType and cmdString to the CommandText property of the SqlCommand object.

The initialized SqlCommand is assigned to the SelectCommand property of the SqlDataAdapter object in step C: A new DataSet object sqlDataSet is initialized and the Clear() method is called to clear the DataSet object before it is filled.

In step D, the Fill() method of the SqlDataAdapter is executed to fill the SqlDataSet. If this fill is successful, it means that the SqlDataSet (exactly the DataDataSet) has been filled by some data, the return value should be greater than 0. Otherwise it means some error occurred and this error message will be displayed to the user.

Before the process can complete, all resources used in this piece of code are released and cleaned up. These cleaning jobs are performed in step E by executing some method such as Dispose().

You need to know that the Fill() method is executed to fill a DataSet. The Fill() method retrieves the data from a source using the SELECT statement specified by an adapter. The Connection object associated with the SELECT statement must be valid, but it does not need to be open. If the connection is closed before the Fill() method is called, it will open the connection and then close it later. If the connection is open before the Fill() is called, it remains open.

The fill operation adds rows to the DataSet, DataTable objects creates the DataTable objects if they are not exist. When creating DataTables, the fill operation normally creates one column name match. However, if the MissingSchemaAction property is set to AddWithKey, appropriate primary keys and constraints are applied.

If the Fill() returns the value of an OUTER JOIN, the DataAdapter does not set a PrimaryKey value for the resulting DataSet. You must explicitly define the primary key to ensure duplicate rows are resolved correctly.

You can use the Fill() method multiple times on the same DataTable. If a primary key exists, incoming rows are merged with matching rows already. If no primary key exists, incoming rows are appended to the DataTable.
