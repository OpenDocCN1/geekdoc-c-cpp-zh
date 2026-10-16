```
int businessEntityId = (int)reader["BusinessEntityID"];
string firstName = (string)reader["FirstName"];
string lastName = (string)reader["LastName"];
WriteLine($"{recursionLevel} {businessEntityId}" +
    $"{firstName} {lastName}");
}
}
}
}
```

When you run the application and pass the entity ID 251, you get the managers of this employee as shown:

```
0 251 Mikael Sandberg
1 250 Sheela Word
2 249 Wendy Kahn
```

Depending on the return of the stored procedure, you need to invoke the stored procedure with ExecuteReader, ExecuteScalar, or ExecuteNonQuery.

With a stored procedure that contains Output parameters, you need to specify the Direction property of the SqlParameter. By default, the direction is ParameterDirection.Input:

```
var pOut = new SqlParameter();
pOut.Direction = ParameterDirection.Output;
```

# Asynchronous Data Access

Accessing the database can take some time. Here you shouldn’t block the user interface. The ADO.NET classes offer task-based asynchronous programming by offering asynchronous methods in addition to the synchronous ones. The following code snippet is similar to the previous one using the SqlDataReader, but it makes use of Async method calls. The connection is opened with SqlConnection.OpenAsync, the reader is returned from the method SqlCommand.ExecuteReaderAsync, and the records are retrieved using SqlDataReader.ReadAsync. With all these methods, the calling thread is not blocked but can do other work before getting the result (code file AsyncSamples/Program.cs):

```
public static void Main()
{
    ReadAsync(714).Wait();
}

public static async Task ReadAsync(int productId)
{
    var connection = new SqlConnection(GetConnectionString());

    string sql =
        "SELECT Prod.ProductID, Prod.Name, Prod.StandardCost,
Prod.ListPrice," +
        "CostHistory.StartDate, CostHistory.EndDate,
CostHistory.StandardCost" +
        "FROM Production.ProductCostHistory AS CostHistory " +
        "INNER JOIN Production.Product AS Prod ON" +
        "CostHistory.ProductId = Prod.ProductId" +
```