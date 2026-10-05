# Code that creates and executes a command
returns an aggregate value

```
string selectStatement = "SELECT SUM(InvoiceTotal) FROM Invoices";nSqlCommand selectCommand = new SqlCommand(selectStatement, connection);
connection.Open();
decimal invoiceTotal = (decimal)selectCommand.ExecuteScalar();
connection.Close();
```

# Code that creates and executes a command that inserts a row

```
string insertStatement = "INSERT Products "
+ "(ProductCode, Description, UnitPrice) "
+ "VALUES (@ProductCode, @Description, @UnitPrice)";
SqlCommand insertCommand = new SqlCommand(insertStatement, connection);
insertCommand.Parameters.AddWithValue("@ProductCode", product.Code);
insertCommand.Parameters.AddWithValue("@Description", product.Description);
insertCommand.Parameters.AddWithValue("@UnitPrice", product.Price);
try
{
    connection.Open();
    int productCount = insertCommand.ExecuteNonQuery();
} catch (SqlException ex)
{
    MessageBox.Show(ex.Message);
} finally
{
    connection.Close();
}
```

# How to execute queriesScalar to return a single value

+   You use the ExecuteScalar method of a command object to retrieve a single value, called a scalar value.

+   The value that's returned can be the value of a single column and row in the database, a calculated value, an aggregate value that summarizes data in the database, or any other value that can be retrieved from the database.

+   If the Select statement returns more than one column or row, only the value in the first column and row is retrieved by the ExecuteScalar method.

# How to execute action queries

+   You use the ExecuteNonQuery method of a command object to execute an Insert, Update, or Delete statement, called an action query.

+   The ExecuteNonQuery method returns an integer that indicates the number of rows that were affected by the query.

+   You can also use the ExecuteNonQuery method to execute statements that affect the structure of a database object. For more information, see the documentation for your database management system.

![](bbox=[0.066, 0.913, 0.881, 0.936])