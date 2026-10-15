The DataTable class is a member of the System.Data namespace within the .NET Framework Class Library. You can create and use a DataTable independently or as a member of a DataSet, and DataTable objects can be used by other .NET Framework objects, including the DataView. You access the collection of tables in a DataSet through the DataSet object’s Tables property.

The schema, or structure, of a table is represented by columns and constraints. You define the schema of a DataTable using DataColumn objects as well as ForeignKeyConstraint and UniqueConstraint objects. The columns in a table can map to columns in a data source, contain calculated values from expressions, automatically increment their values, or contain primary key values.

If you populate a DataTable from a database, it inherits the constraints from the database, so you don’t have to do all of that work manually. A DataTable must also have rows in which to contain and order the data. The DataRow class represents the actual data contained in the table. You use the DataRow and its properties and methods to retrieve, evaluate, and manipulate the data in a table. As you access and change the data within a row, the DataRow object maintains both its current and original state.

You can create parent-child relationships between tables within a database, such as SQL Server, using one or more related columns in the tables. You create a relationship between DataTable objects using a DataRelation, which can then be used to return a row’s related child or parent rows.

# Advanced ADO.NET Features of the DataSet and DataTable Objects

One of the main complaints developers had about ADO.NET 1.x was related to the performance of the DataSet and its DataTable children — in particular, when they contained a large amount of data. The performance hit comes in two different ways. The first way is the time it takes to actually load a DataSet with a lot of data. As the number of rows in a DataTable increases, the time to load a new row increases almost proportionally to the number of rows. The second way is when the large DataSet is serialized and remoted. A key feature of the DataSet is the fact that it automatically knows how to serialize itself, especially when you want to pass it between application tiers. Unfortunately, the serialization is quite verbose and takes up a lot of memory and network bandwidth. Both of these performance problems have been addressed since ADO.NET 2.0.

# Indexing

The first improvement made since ADO.NET 2.0 to the DataSet family was a complete rewrite of the indexing engine for the DataTable, which now scales much better for large DataSets. The addition of the new indexing engine results in faster basic inserts, updates, and deletes, which also means faster Fill and Merge operations. Just as in relational database design, if you are dealing with large DataSets, then it pays big dividends if you first add unique keys and foreign keys to your DataTable. Even better, you don’t have to change any of your code at all to take advantage of this new feature.

# Serialization

The second improvement made to the DataSet family was adding new options to the way the DataSet and DataTable are serialized. The main complaint about retrieving DataSet objects from Web services and remoting calls was that they were way too verbose and took up too much network bandwidth. In ADO.NET 1.x, the DataSet serializes as XML, even when using the binary formatter. Using ADO.NET, you can also specify true binary serialization by setting the newly added RemotingFormat property to SerializationFormat.Binary, rather than (the default) SerializationFormat.XML. In the AdoNetFeaturesTest project of the Examples solution, I have added a Button (serializationButton) to the form and its associated Click event handler that demonstrates how to serialize a DataTable in binary format:

```
Private Sub _serializationButton_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles _serializationButton.Click
' Get the authors reader.
Dim reader As SqlDataReader = GetAuthorsSqlReader()
```