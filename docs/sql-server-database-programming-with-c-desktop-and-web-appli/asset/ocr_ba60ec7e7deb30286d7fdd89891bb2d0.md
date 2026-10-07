# SQL Server Database Programming with C#

```
string cmdString = "SELECT name, office, title, color FROM Faculty";
SqlCommand command = new SqlCommand();
SqlDataAdapter adapter = new SqlDataAdapter();
DataSet dataset = new DataSet();

command.Connection = connection;
command.CommandType = CommandType.Text;
command.CommandText = cmdString;

sqlDataAdapter adapter = new SqlDataAdapter(cmdString, connection);
adapter.SelectCommand = command;
dataset = new DataSet();
dataset.Clear();
int value = adapter.Fill(dataset);
if (value == 0)
{
    MessageBox.Show("No valid faculty found!");
```

FIGURE 3.23 An example of using the SqlDataAdapter to fill the DataSet.

An integer Index is used to hold the return value of calling this Fill() method. This value is equal to the number of rows filled into the Faculty table in the DataSet. If this value is 0, which means that no row has been found from the Faculty table in the database and 0 row has been filled into the Faculty table in the DataSet, an error message is displayed. Otherwise, this value is successful.

In step F, all components used for this piece of code are released by the Dispose() method.

# 3.4.5 The DataReader Class

The DataReader is a read-only class and can only be used to retrieve and hold the data rows returned from a database executing ExecuteReader() method. This provides a way of reading a forward-only stream of rows from a database. Depending on the Data Provider you are using, four DataReaders are provided by four Providers. These are ODataReader, OleDbDataReader, SqlDataReader and OracleDataReader.

To create a DataReader instance, you must call the ExecuteReader() method of the Command object, instead of using a constructor that the DataReader class does not have any public constructor. The following code to create an instance of the SqlDataReader is incorrect:

```
SqlDataReader sqlDataReader = new SqlDataReader();
```

While the DataReader object is being used, the Connection is busy serving the DataReader, and no other operations can be performed on the Connection other than closing it. This is the case when the Close() method of the Command is called. For instance, you cannot retrieve output parameters until you call the Close() method to close the connected Data.

The Closed property of the DataReader class can be used to check if the DataReader has been closed or not, and it returns a Boolean value. A true means that the DataReader has been closed. It is a good habit to call the Close() method each time you finish that query using DataReader to avoid the troubles caused by the multiple connections to the database.

Figure 3.24 lists most public properties of the SqlDataReader class. All other DataReader classes have the similar properties.