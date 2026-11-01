A resource reader has to implement the interface IResourceReader. This interface defines the methods Close() and GetEnumerator() to return an IDictionaryEnumerator that returns keys and values for the resources. In the implementation of GetEnumerator(), create a Hashtable where all keys and values for a specific language are stored. Next, you can use the SqlConnection class in the namespace System.Data.SqlClient to access the database in SQL Server. Connection.CreateCommand() creates a SqlCommand() object that you use to specify the SQL SELECT statement to access the data in the database. If the language is set to de, the SELECT statement is SELECT [key], [de] FROM Messages. Then you use a SqlDataReader to read all values from the database and put them into a Hashtable. Finally, the enumerator of the Hashtable is returned.

> For more information about accessing data with ADO.NET, see Chapter 30, “Core ADO.NET.”

```
public System.Collections.IDictionaryEnumerator GetEnumerator()
{
    Dictionary<string, string> dict = new Dictionary<string, string>();

    SqlConnection connection = new SqlConnection(connectionString);
    SqlCommand command = connection.CreateCommand();
    if (String.IsNullOrEmpty(language))
        language = "Default";

    command.CommandText = "SELECT [key], [" + language + "] " +
                          "FROM Messages";

    try
    {
        connection.Open();

        SqlDataReader reader = command.ExecuteReader();
        while (reader.Read())
        {
            if (reader.GetValue(1) != System.DBNull.Value)
            {
                dict.Add(reader.GetString(0).Trim(), reader.GetString(1));
            }
        }

        reader.Close();
    }
    catch (SqlException ex)
    {
        if (ex.Number != 207)  // ignore missing columns in the database
            throw;             // rethrow all other exceptions
    }
    finally
    {
        connection.Close();
    }
    return dict.GetEnumerator();
}

public void Close()
{
}
```