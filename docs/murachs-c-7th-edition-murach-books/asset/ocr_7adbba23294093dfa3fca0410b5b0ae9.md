# Code that executes a command that returns a single value

```
string select = "SELECT SUM(InvoiceTotal) FROM Invoices";
using SqlConnection connection = new SqlConnection(connectionString);
using SqlCommand command = new SqlCommand(select, connection);
connection.Open();
decimal invoiceTotal = (decimal) command.ExecuteScalar;
```

# Code that executes a command that inserts a row

```
string insert = "INSERT Products (ProductCode, Description, UnitPrice) "
    + "VALUES (@ProductCode, @Description, @UnitPrice)";
using SqlConnection connection = new SqlConnection(connectionString));
using SqlCommand command = new SqlCommand(insert, connection);
command.Parameters.AddWithValue("@ProductCode", product.Code);
command.Parameters.AddWithValue("@Description", product.Description);
command.Parameters.AddWithValue("@UnitPrice", product.Price);
try
{
    connection.Open();
    int productCount = command.ExecuteNonQuery();
}
catch (SqlException ex)
{
    MessageBox.Show(ex.Message);
}
```

# How to execute queries that return a single value

+   - You use the ExecuteScalar() method of a command object to retrieve a single value, called a scalar value.

+   - If the SELECT statement returns more than one column or row, only the value in the first column and row is retrieved by the ExecuteScalar() method.

# How to execute action queries

+   - The INSERT, UPDATE, and DELETE statements are sometimes called action queries.

+   - You use the ExecuteNonQuery() method of a command object to execute an INSERT, UPDATE, or DELETE statement.

+   - The ExecuteNonQuery() method returns an integer that indicates the number of rows that were affected by the query.