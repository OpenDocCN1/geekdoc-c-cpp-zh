
```
Using conn As New SqlCeConnection(My.Settings.productsConnectionString)
    conn.Open()
    Using cmd As _
        New SqlCeCommand("SELECT ProductName, UnitPrice FROM Products", conn)
        Using reader As SqlCeDataReader = cmd.ExecuteReader
            While reader.Read
                Console.WriteLine("{0}: {1:c}",
                    reader.GetString(0),
                    reader.GetDecimal(1))
            End While
        End Using
    End Using
End Using
```

If you use the provider-agnostic classes, then the code becomes even more like the SQL Server equivalent:

```
Dim fact As DbProviderFactory
Dim prov As String = My.Settings.productsProvider
fact = DbProviderFactories.GetFactory(prov)
Using conn As DbConnection = fact.CreateConnection()
    conn.ConnectionString = My.Settings.productsConnectionString
    conn.Open()
    Using cmd As DbCommand = fact.CreateCommand
        With cmd
            .CommandText = "SELECT ProductName, UnitPrice FROM Products"
            .CommandType = CommandType.Text
            .Connection = conn
            Using reader As DbDataReader = cmd.ExecuteReader
                While reader.Read
                    Console.WriteLine("{0}: {1:c}", _
                        reader.GetString(0), _
                        reader.GetDecimal(1))
                End While
            End Using
        End With
    End Using
End Using
```

The simplest possible way to use a SQL Server Compact database in your application is to use it as a standalone database. While you get none of the benefits of synchronization, you do get the benefit of the simpler (and smaller) deployment for SQL Server Compact. However, the true power of SQL Server Compact comes into play when you use it along with synchronization with a full SQL Server database. This enables you to more easily create applications that work both offline and online.

## Connecting to a SQL Server Compact Database

As with other editions of SQL Server, the key to connecting to a SQL Server Compact database is in the connection string. However, because SQL Server Compact does not have the same features in terms of server and integrated security, different options are used to connect to the database, the most important of which are described in Table 12-1. Only the data source and password values can be set within the IDE.

### TABLE 12-1: SQL Server Compact Connection Options

| OPTION | DESCRIPTION |
|---|---|
| Provider name | System.Data.SqlServerCe |
| Data source | Points to the SDF file. As this file is normally included in the project, the value can be written using the DataDirectory shortcut: DataSource=|DataDirectory|\DatabaseName.sdf; |
| Password | The password used to encrypt the database. |
| Max buffer size | The maximum amount of memory that is used before SQL Server Compact flushes the changes to disk, measured in kilobytes. The default value is 640, which should be enough for everyone. |
| Max database size | The maximum size for the database, measured in megabytes. The default value is 256MB (128MB when SQL Server Compact is running on devices), and the maximum value is 4096MB (4GB). |
| Mode | How the database file will be opened. This value can be Read Only, Read Write, Exclusive, or Shared Read. The default, Read Write, should be used, unless you have particular needs for your database. |
| Autoshrink threshold | As SQL Server Compact databases will grow on demand, there may be situations when you need them to shrink on demand as well, such as when a large amount of data is deleted or a complex operation needing temporary tables completes. When this occurs, this setting identifies when, and by how much, the database should shrink. By default, SQL Server Compact will shrink a database when 60 percent of the available space is empty. Normally, you will not need to change this setting unless space is at a premium. |

Using SQL Server Compact as a local standalone database can be useful when creating small, easily deployed applications. You can see this by creating a simple application to store contact data in a SQL Server Compact database:

- 1. Create a new Windows Forms Application project named LocalDatabase and add a new local database to your application by right-clicking the project and selecting Add Item (see Figure 12-1).

![](img/d99870e80390742f93963da7be0b2e61_472_0.png)

### FIGURE 12-1

- 2. Once you have added the new database, Visual Studio will also add a new data set to the project and start the Data Source Configuration Wizard. As you are not using the database to retrieve server data, the DataSet will initially be blank (see Figure 12-2). Click Finish to add the new DataSet. You will add the tables later.

![](img/d99870e80390742f93963da7be0b2e61_473_0.png)

### FIGURE 12-2

3. Double-click on the Contacts.sdf file in your project to open it in the Server Explorer window. You can now add a new table named Contacts to the database, as shown in Figure 12-3 and described in the following table.

| COLUMN | DATA TYPE | DESCRIPTION |
|---|---|---|
| id | Int | This should be set to not allow null values, and as the primary key for the table. Remember to set Identity to true. |
| FirstName | NVarChar (50) | Allow Nulls should be set to false. |
| LastName | NVarChar (50) | Allow Nulls should be set to false. |
| EMail | NVarChar (100) | Allow Nulls should be set to true. |

![](img/d99870e80390742f93963da7be0b2e61_473_1.png)

### FIGURE 12-3

4. In Solution Explorer, double-click the ContactsDataSet added earlier to open the designer and drag the newly created table onto the surface (see Figure 12-4).

5. Open the Data Sources window in Visual Studio by clicking the Data Sources tab. You should see the ContactsDataSet, with the Contacts table. Drag the Contacts table onto the form to create a DataGridView control and a navigator (see Figure 12-5). You should now be able to run the application and add some data.

6. If you look at the contents of the Contacts.sdf file, you may be dismayed, as no data is visible. This is because it is not the database actually being written to. If you look in the /bin/debug folder for the application, you will see the actual database, which contains the data added (see Figure 12-6).

![](img/d99870e80390742f93963da7be0b2e61_474_0.png)

![](img/d99870e80390742f93963da7be0b2e61_474_1.png)

![](img/d99870e80390742f93963da7be0b2e61_474_2.png)

## Synchronizing Data

As mentioned earlier, although you can use SQL Server Compact as a standalone database, it really shines when it is used in combination with a remote database and synchronization. Synchronization enables you to reduce the network traffic required when querying the database, while still keeping up-to-date data on the client. It may be one-way synchronization, pulling the most recent server changes down to the client, or it may be bidirectional, keeping both client and server synchronized. The best choice depends on the situation. You would want to use synchronization in your applications in a number of scenarios:

- Remote data mirror applications — These applications use the local database only as a local copy of the master database, likely as a subset of data. In this scenario, shown in Figure 12-7, data flows only one way: from the server database to the client. Most commonly, this would be product information, news, or customer data that the clients would read but not change.

![](img/d99870e80390742f93963da7be0b2e61_474_3.png)

- Remote data entry applications — These include Sales or Field Force Automation (SFA and FFA) applications, such as the classic “traveling sales agent” applications. In this scenario, a given data row goes only in a single direction: reference data down to the client, inserts up to the server, as shown in Figure 12-8. As with the remote data mirror applications, a subset of data is typically installed on the client workstation, generally the catalog information and any reference data required, before the application goes off the network. The sales agent then goes out, making sales. Occasionally, the application is reconnected to the network, when new customer and sales data are uploaded to the main database, and updated catalog data is sent to the client.

- Simple queuing applications — These applications are a special case of the preceding scenario. The applications write exclusively to the local database and use synchronization to push the changed data to the server database. The difference here is partly intent; here the local database on the client is used as a temporary holding space. A periodic synchronization moves data between server and client when the two are connected. This scenario, shown in Figure 12-9, improves the overall performance of the application, particularly when you have a slow connection between server and client. It also provides access to the application even when the network is not available.

- Remote database applications — These applications treat the remote database as though it were a “master” copy of the data. In this scenario, shown in Figure 12-10, data may be changed either at the client or at the server, and the changes flow in both directions. This is the most dangerous scenario for synchronization clients because the data may have been changed differently in two (or more) locations. Therefore, some form of conflict resolution is required, as well as policies that specify which changes take precedence (e.g., last change overrides the data, someone must manually process all conflicts to select the valid data, or the data change made by the highest person in the organization chart wins). It is best to avoid or limit this scenario if possible when building a synchronization solution.

![](img/d99870e80390742f93963da7be0b2e61_475_0.png)

图中标注：Clients inserts submitted on synchronization；Reference data from server；Application stores data locally while offline；Data from server；When network is available, data is pushed to server periodically；Application stores data locally。

Disconnected　　Connected

FIGURE 12-8　　　　　　　　　　　 FIGURE 12-9
