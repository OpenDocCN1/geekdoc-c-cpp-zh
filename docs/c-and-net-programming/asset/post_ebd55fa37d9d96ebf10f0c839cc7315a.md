
## DataReader methods

| Method | Description |
|---|---|
| Close | Closes a DataReader object. |
| Read | Reads next record in the data reader. |
| NextResult | Advances the data reader to the next result during batch transactions. |
| Getxxx | There are dozens of Getxxx methods. These methods read a specific data type value from a column. For example, GetChar will return a column value as a character and GetString as a string. |

## Creating a SqlDataReader Object

Instantiating SqlDataReader is different from instantiating other ADO.NET objects.

First, call ExecuteReader on a command object:

```csharp
SqlDataReader sqldr = sqlcmd.ExecuteReader();
```

The ExecuteReader method of the SqlCommand object, sqlcmd, returns a SqlDataReader instance. Creating a SqlDataReader with the new operator is not sufficient to do anything as the SqlCommand object references the connection and the SQL statement is necessary for the SqlDataReader to obtain data.

## Reading Data

The SqlDataReader returns data via a sequential stream. To read this data, data is fetched from a table row-by-row. Once a row has been read, the previous row is no longer available. To read that row again, one would have to create a new instance of the SqlDataReader and read through the data stream again.

The typical method of reading from the data stream returned by the SqlDataReader is to iterate through each row with a while loop.

```csharp
while (sqldr.Read())
{
    // get the results of each column
    string contact = (string)sqldr["AuthorContactName"];
    string publication = (string)sqldr["AuthorPublicationName"];
    string city = (string)sqldr["AuthorCity"];

    // print results
    Console.Write("{0,35}", contact);
    Console.Write("{0,30}", city);
    Console.Write("{0,35}", publication);
}
```

The return value of *Read* is type bool and returns true as long as there are more records to read. After the last record in the data stream has been read, *Read* returns false.

Each column can be extracted from the row with a numeric indexer. Instead of a numeric indexer, a string indexer can be used, where the string is the column name from the SQL query (the table column name is used if an asterisk, \*, is used.) String indexers are much more readable, making the code easier to maintain.

Regardless of the type of the indexer parameter, a SqlDataReader indexer will return type object.

### Closing Connection

Once SqlDataReader has been used, close the SqlConnection.

```csharp
try
{
    // data access code
}
finally
{
    // 3. close the reader
    if (sqldr != null)
    {
        sqldr.Close();
    }

    // close the connection too
}
```

### Example

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ADONetDemos
{
    class ReadersDemo
    {
        static void Main()
        {
            ReadersDemo rsd = new ReadersDemo();
            rsd.DataRead();
        }

        public void DataRead()
        {
            // declare the SqlDataReader
            SqlDataReader sqldr = null;

            // create a connection object
            SqlConnection sqlconn = new SqlConnection(
                "Data Source=(local);Initial Catalog=Northwind;Integrated Security=SSPI");

            // create a command object
            SqlCommand sqlcmd = new SqlCommand(
                "select * from Books", sqlconn);

            try
            {
                // open the connection
                sqlconn.Open();

                // 1. get an instance of the SqlDataReader
                sqldr = sqlcmd.ExecuteReader();

                // print column headers
                Console.WriteLine("Author Contact Name  Author City  Publication Name");

                // 2. print necessary columns of each record
                while (sqldr.Read())
                {
                    // get the results of each column
                    string contact = (string)sqldr["AuthorContactName"];
                    string publication = (string)sqldr["Publication"];
                    string city = (string)sqldr["AuthorCity"];

                    // print results
                    Console.Write("{0,-35}", contact);
                    Console.Write("{0,-30}", city);
                    Console.Write("{0,-35}", publication);
                }
            }
            finally
            {
                // 3. close the reader
                if (sqldr != null)
                {
                    sqldr.Close();
                }

                // close the connection
                if (sqlconn != null)
                {
                    sqlconn.Close();
                }
            }
        }
    }
}
```

## 5. Using SqlDataAdapter

- A DataSet is an in-memory data store that can hold numerous tables. DataSets only hold data and do not interact with a data source. SqlDataAdapter manages connections with the data source and gives the disconnected behavior. The SqlDataAdapter opens a connection only when required and closes it as soon as it has performed its task.

- SqlDataAdapter performs the following tasks when filling a DataSet with data:
    1. Open connection
    2. Retrieve data into DataSet
    3. Close connection

  It performs the following actions when updating a data source when the DataSet changes:
    1. Open connection
    2. Write changes from DataSet to data source
    3. Close connection

In between the Fill and Update operations, data source connections are closed. Data can be read and written with the DataSet. As the applications holds on to connections only when necessary, the application becomes more scalable.

### Creating a DataSet Object

```csharp
DataSet dsBooks = new DataSet();
```

Now, the DataSet is empty and needs a SqlDataAdapter to load it.

### Creating a SqlDataAdapter

1. The SqlDataAdapter holds the SQL commands and connection object for reading and writing data. It is initialized with a SQL select statement and connection object:

    ```csharp
    SqlDataAdapter daBooks = new SqlDataAdapter("select BookID,Author from Books", sqlconn);
    ```

2. The code above creates a new SqlDataAdapter, daBooks. The SQL select statement specifies what data will be read into a DataSet. The connection object, sqlconn, should have already been instantiated, but not opened. SqlDataAdapter is responsible for opening and closing the connection during Fill and Update method calls.

3. The SqlDataAdapter contains all of the commands necessary to interact with the data source. There are two ways to add insert, update, and delete commands: via SqlDataAdapter properties or with a SqlCommandBuilder.

    ```csharp
    // Using SqlCommandBuilder
    SqlCommandBuilder cmdBldr = new SqlCommandBuilder(daBooks);
    ```

4. SqlCommandBuilder is instantiated with a single constructor parameter of the SqlDataAdapter, daBooks, instance. This tells the SqlCommandBuilder what SqlDataAdapter to add commands to. The SqlCommandBuilder will read the SQL select statement (specified when the SqlDataAdapter was instantiated), infer the insert, update, and delete commands, and assign the new commands to the Insert, Update, and Delete properties of the SqlDataAdapter, respectively.

Note that SqlCommandBuilder would work for a single table and not for multiple-table joins.

## Filling the DataSet

```csharp
daBooks.Fill(dsBooks, "Books");
```

The Fill method, in the code above, takes two parameters: a DataSet and a table name. The DataSet must be instantiated before trying to fill it with data. The second parameter is the name of the table that will be created in the DataSet.

The Fill method has an overload that accepts one parameter for the DataSet only. In that case, the table created has a default name of "table1" for the first table. The number will be incremented (table2, table3, ..., tableN) for each table added to the DataSet where the table name was not specified in the Fill method.

## Using the DataSet

A DataSet will bind with both ASP.NET and Windows Forms DataGrids.

```csharp
// Illustration of a DataSet assigned to a Windows Forms DataGrid
dgBooks.DataSource = dsBooks;
dgBooks.DataMember = "Books";
```

The DataSet is assigned to the DataSource property of the DataGrid.

To specify exactly which table to use, set the DataGrid's DataMember property to the name of the table.

## Updating Changes

After modifications are made to the data, if it is to be updated to the actual database, the Update method of the SqlDataAdapter is used to put modifications to the database.

```csharp
daBooks.Update(dsBooks, "Books");
```

The Update method above is called on the SqlDataAdapter instance that originally filled the dsBooks DataSet. The second parameter to the Update method specifies which table, from
