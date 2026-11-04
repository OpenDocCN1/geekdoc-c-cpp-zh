```
```csharp
// Example of a parameterized query
string sql = "SELECT * FROM Employees WHERE EmployeeID = @EmployeeID";
using (SqlCommand command = new SqlCommand(sql, connection))
{
    command.Parameters.AddWithValue("@EmployeeID", employeeID);
    // Execute the query
}
```
```

# ## 2. Connection Pooling

Connection pooling is a technique that helps improve the performance and scalability of your data access solutions. When you create a connection to a database, ADO.NET will automatically pool the connection so that it can be reused by other requests. This reduces the overhead of creating and destroying connections, improving the performance of your application.

```
```csharp
// Example of using connection pooling
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    // Use the connection
}
```
```

# ## 3. Transactions

Transactions are another important best practice for data access. Transactions allow you to group multiple database operations into a single unit of work. This ensures that either all the operations succeed or none of them do. This helps maintain data integrity and consistency.

```
```csharp
// Example of using a transaction
using (SqlConnection connection = new SqlConnection(connectionString))
```
```