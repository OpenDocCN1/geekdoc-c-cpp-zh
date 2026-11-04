+   - **Data Sets and Data Tables:** ADO.NET Core supports DataSet and DataTable objects for working with in-memory data. These objects can be used to store and manipulate data retrieved from the database server.

```
```csharp
using System.Data;
using System.Data.SqlClient;

// Establishing a connection to a SQL Server database
string connectionString = "Server=localhost;Database=SampleDatabase;Integrated Security=true;";
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();

    // Creating a command to retrieve data from a table
    string sql = "SELECT * FROM Employees";
    using (SqlCommand command = new SqlCommand(sql, connection))
    {
        // Executing the command and retrieving data
        using (SqlDataReader reader = command.ExecuteReader())
        {
            while (reader.Read())
            {
                // Processing each row of data
                int employeeId = reader.GetInt32(0);
                string employeeName = reader.GetString(1);
                Console.WriteLine($"Employee ID: {employeeId}, Employee Name: {employeeName}");
            }
        }
    }
}
```
```

# ADO.NET Core Architecture