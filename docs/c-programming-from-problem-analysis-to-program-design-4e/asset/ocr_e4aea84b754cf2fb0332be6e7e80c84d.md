# EXAMPLE 14.14

```
```csharp
private OleDbConnection    dbConn;
private OleDbCommand        dbCmd;
private string              sConnection;
private string              sql;
                         ;  // Colon indicates items missing
// Construct an object of the OleDbConnection
// class to store the connection string
// representing the type of data provider
// (database) and the source (actual db).
sConnection =
        "Provider=Microsoft.ACE.OLEDB.12.0;" +
        "Data Source=member.accdb";
dbConn = new OleDbConnection(sConnection);

// Construct an object of the OleDbCommand
// class to hold the SQL query. Tie the
// OleDbCommand object to the OleDbConnection
// object.
sql = "SELECT * FROM memberTable Order " +
       "BY LastName ASC, FirstName ASC;";
dbCmd = new OleDbCommand();
dbCmd.CommandText = sql;
dbCmd.Connection = dbConn;
```
```

# DATASET OBJECT

The data reader object held one record of the query result at a time. The dataset object stores an entire relational tablelike structure. More than one table, plus relationships and constraints on the database, can be stored with the dataset object. The dataset is considered a memory-resident representation of the data. An object of the DataSet class can be instantiated, as shown in Example 14–15.

# EXAMPLE 14.15

```
```csharp
DataSet memberDS = new DataSet();
```
```

# DATAADAPTER OBJECT

An easy way to use a DataSet object is to instantiate an object of the DataAdapter class. Adapters are used to exchange data between a database source and a dataset object. The adapter also makes it easier to update the database if changes are made. An object of the DataAdapter class for an OleDb provider can be instantiated, as shown in Example 14–16.