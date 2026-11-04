ADO.NET Core has a lightweight and modular architecture optimized for performance and flexibility. It comprises several layers, including the data provider layer, the command layer, and the data reader layer. Each layer has a specific responsibility in data access, such as establishing a connection, executing SQL commands, and reading data.

+   - **Data Provider Layer**: This layer provides a connection to the database server and executes SQL commands. It includes classes like DbConnection, DbCommand, and DbDataReader.
+   - **Command Layer**: This layer executes SQL commands and retrieves data from the database server. It includes classes like SqlCommand, MySqlCommand, and NpgsqlCommand.
+   - **Data Reader Layer**: This layer reads data from the database server. It includes classes like SqlDataReader, MySqlDataReader, and NpgsqlDataReader.

```
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

```