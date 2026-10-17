
`string name = (string)reader[1];`

`DateTime from = (DateTime)reader[2];`

`DateTime? to = (DateTime?)reader[3];`

```csharp
int id = (int)reader["ProductID"];

string name = (string)reader["Name"];

DateTime from = (DateTime)reader["StartDate"];

DateTime? to = (DateTime?)reader["EndDate"];
```

`SqlDataReader`的索引器还允许使用字符串而不是整数，传递列名。在这些不同的选项中，这是最慢的方法，但它可能满足你的需求。与进行服务调用所需的时间相比，访问索引器所需的额外时间可以忽略不计：

```csharp
int id = (int)reader["ProductID"];

string name = (string)reader["Name"];

DateTime from = (DateTime)reader["StartDate"];

DateTime? to = (DateTime?)reader["EndDate"];
```

### 调用存储过程

使用命令对象调用存储过程，只需定义存储过程的名称，为存储过程的每个参数添加定义，然后使用上一节介绍的方法之一执行命令即可。

以下示例调用存储过程`uspGetEmployeeManagers`获取某位员工的所有经理。该存储过程接收一个参数，通过递归查询返回所有经理的记录：

```sql
CREATE PROCEDURE [dbo].[uspGetEmployeeManagers]

    @BusinessEntityID [int]

AS

--...
```

要查看该存储过程的实现，请查阅AdventureWorks2014数据库。

要调用存储过程，需要将`SqlCommand`对象的`CommandText`设置为存储过程的名称，并将`CommandType`设置为`CommandType.StoredProcedure`。除此之外，命令的调用方式与之前看到的类似。该参数使用`SqlCommand`对象的`CreateParameter`方法创建，但是你也可以使用前面使用的其他方法来创建参数。对于该参数，需要设置`SqlDbType`、`ParameterName`和`Value`属性。由于存储过程返回记录，因此通过调用`ExecuteReader`方法来调用它（代码文件`CommandSamples/Program.cs`）：

```csharp
private static void StoredProcedure(int entityId)

{

    using (var connection = new SqlConnection(GetConnectionString()))

    {

        SqlCommand command = connection.CreateCommand();

        command.CommandText = "[dbo].[uspGetEmployeeManagers]";

        command.CommandType = CommandType.StoredProcedure;

        SqlParameter p1 = command.CreateParameter();

        p1.SqlDbType = SqlDbType.Int;

        p1.ParameterName = "@BusinessEntityID";

        p1.Value = entityId;

        command.Parameters.Add(p1);

        connection.Open();

        using (SqlDataReader reader = command.ExecuteReader())

        {

            while (reader.Read())

            {

                int recursionLevel = (int)reader["RecursionLevel"];

                int businessEntityId = (int)reader["BusinessEntityID"];

                string firstName = (string)reader["FirstName"];

                string lastName = (string)reader["LastName"];

                WriteLine($"{recursionLevel} {businessEntityId}" +

                    $" {firstName} {lastName}");

            }

        }

    }

}
```

当你运行应用程序并传递实体ID 251时，会得到该员工的经理，如下所示：

```

0 251 Mikael Sandberg

1 250 Sheela Word

2 249 Wendy Kahn

```

根据存储过程的返回类型，你需要使用`ExecuteReader`、`ExecuteScalar`或`ExecuteNonQuery`来调用存储过程。

对于包含输出参数的存储过程，你需要指定`SqlParameter`的`Direction`属性。默认情况下，该方向为`ParameterDirection.Input`：

```csharp
var pOut = new SqlParameter();

pOut.Direction = ParameterDirection.Output;
```

### 异步数据访问

访问数据库可能会耗费一些时间。在这里，你不应该阻塞用户界面。ADO.NET类在提供同步方法的同时，还提供了异步方法，从而支持基于任务的异步编程。下面的代码片段与之前使用`SqlDataReader`的代码类似，只是使用了异步方法调用。连接通过`SqlConnection.OpenAsync`打开，读取器通过`SqlCommand.ExecuteReaderAsync`方法返回，记录通过`SqlDataReader.ReadAsync`检索。使用所有这些方法，调用线程不会被阻塞，而是在获得结果之前可以处理其他工作（代码文件`AsyncSamples/Program.cs`）：

```csharp
public static void Main()

{

    ReadAsync(714).Wait();

}

public static async Task ReadAsync(int productId)

{

    var connection = new SqlConnection(GetConnectionString());

    string sql =

        "SELECT Prod.ProductID, Prod.Name, Prod.StandardCost, Prod.ListPrice, " +

        "CostHistory.StartDate, CostHistory.EndDate, CostHistory.StandardCost " +

        "FROM Production.ProductCostHistory AS CostHistory " +

        "INNER JOIN Production.Product AS Prod ON " +

        "CostHistory.ProductId = Prod.ProductId " +

        "WHERE Prod.ProductId = @ProductId";

    var command = new SqlCommand(sql, connection);

    var productIdParameter = new SqlParameter("ProductId", SqlDbType.Int);

    productIdParameter.Value = productId;

    command.Parameters.Add(productIdParameter);

    await connection.OpenAsync();

    using (SqlDataReader reader = await command.ExecuteReaderAsync(

        CommandBehavior.CloseConnection))

    {

        while (await reader.ReadAsync())

        {

            int id = reader.GetInt32(0);

            string name = reader.GetString(1);

            DateTime from = reader.GetDateTime(4);

            DateTime? to = reader.IsDBNull(5) ? (DateTime?)null:

                reader.GetDateTime(5);

            decimal standardPrice = reader.GetDecimal(6);

            WriteLine($"{id} {name} from: {from:d} to: {to:d}; " +

                $"price: {standardPrice}");

        }

    }

}
```

使用异步方法调用不仅对Windows应用程序有利，而且在服务器端同时进行多个调用时也很有用。ADO.NET API的异步方法具有支持`CancellationToken`的重载，以便提前停止长时间运行的方法。

> 注意 有关异步方法调用和`CancellationToken`的更多信息，请阅读第15章“异步编程”。

### 事务

默认情况下，单个命令在事务中运行。如果你需要发出多个命令，并且这些命令要么全部执行，要么全部不执行，你可以显式启动和提交事务。

事务用术语ACID来描述。ACID是原子性、一致性、隔离性和持久性这四个词的首字母缩写：

- **原子性**——表示一个工作单元。对于事务，要么整个工作单元成功，要么什么都不会改变。
- **一致性**——事务开始之前和事务完成之后的状态必须是有效的。在事务期间，状态可能会有中间值。
- **隔离性**——并发发生的事务与在事务期间更改的状态相隔离。事务A在事务完成之前，无法看到事务 B 的中间状态。
- **持久性**——事务完成后，必须以持久方式存储。这意味着如果断电或服务器崩溃，重启时必须恢复状态。

> 注意 事务和有效状态可以很容易地用婚礼仪式来比喻。一对新人站在事务协调员面前。事务协调员先问新人中的第一位：“你愿意与身边的这个人结婚吗？”如果第一位同意，再问第二位：“你愿意与这个人结婚吗？”如果第二位拒绝，第一位会收到回滚。这个事务的有效状态只能是双方都结婚，或者双方都不结婚。如果双方都同意，事务提交，双方进入已婚状态。如果一方拒绝，事务中止，双方都保持未婚状态。无效状态是一方已婚而另一方未婚。事务保证结果永远不会处于无效状态。

使用 ADO.NET，可以通过调用`SqlConnection`的`BeginTransaction`方法启动事务。事务始终与一个连接相关联；你不能在多个连接上创建事务。`BeginTransaction` 方法返回一个`SqlTransaction`，该事务需要与在同一事务下运行的命令一起使用（代码文件`TransactionSamples/Program.cs`）：

```csharp
public static void TransactionSample()

{

    using (var connection = new

SqlConnection(GetConnectionString()))

    {

        await connection.OpenAsync();

        SqlTransaction tx = connection.BeginTransaction();

        // etc.

    }

}
```

> 注意 实际上，你可以创建跨多个连接的事务。在 Windows 操作系统上，这需要使用分布式事务协调器。你可以使用`TransactionScope`类创建分布式事务。然而，这个类仅属于完整的 .NET Framework，并未引入 .NET Core；因此本书不涉及。如果你需要了解更多关于`TransactionScope`的信息，请参阅本书的前一版本，例如《Professional C# 5 and .NET 4.5.1》。

代码示例在`Sales.CreditCard`表中创建一条记录。使用 SQL 子句`INSERT INTO`添加记录。`CreditCard` 表定义了一个自增标识符，该标识符由第二条 SQL 语句`SELECT SCOPE_IDENTITY()`返回，该语句返回创建的标识符。实例化`SqlCommand`对象后，通过设置`Connection`属性分配连接，并通过设置`Transaction`属性分配事务。对于 ADO.NET 事务，你无法将事务分配给使用不同连接的命令。但是，你也可以使用同一连接创建与事务无关的命令：

```csharp
public static void TransactionSample()

{

    // etc.

    try

    {

        string sql ="INSERT INTO Sales.CreditCard" +

            "(CardType, CardNumber, ExpMonth, ExpYear)" +

            "VALUES (@CardType, @CardNumber, @ExpMonth, @ExpYear);" +

            "SELECT SCOPE_IDENTITY()";

        var command = new SqlCommand();

        command.CommandText = sql;

        command.Connection = connection;

        command.Transaction = tx;

    // etc.

}

```

定义参数并填充值后，通过调用`ExecuteScalarAsync`方法执行命令。这次`ExecuteScalarAsync`方法与`INSERT INTO`子句一起使用，因为完整的 SQL 语句以返回单个结果结束：创建的标识符从`SELECT SCOPE_IDENTITY()`返回。如果在`WriteLine`方法之后设置断点并检查数据库中的结果，你不会在数据库中看到新记录，尽管创建的标识符已经返回。原因是事务尚未提交：

```csharp
public static void TransactionSample()

{

    // etc.

        var p1 = new SqlParameter("CardType", SqlDbType.NVarChar, 50);

        var p2 = new SqlParameter("CardNumber", SqlDbType.NVarChar, 25);

        var p3 = new SqlParameter("ExpMonth", SqlDbType.TinyInt);

        var p4 = new SqlParameter("ExpYear", SqlDbType.SmallInt);

        command.Parameters.AddRange(new SqlParameter[] { p1, p2, p3, p4 });

        command.Parameters["CardType"].Value ="MegaWoosh";

        command.Parameters["CardNumber"].Value ="08154711123";

        command.Parameters["ExpMonth"].Value = 4;

        command.Parameters["ExpYear"].Value = 2019;

        object id = await command.ExecuteScalarAsync();

        WriteLine($"record added with id: {id}");

    // etc.

}

```

现在可以在同一事务中创建另一条记录。使用示例代码，继续使用相同的命令，该命令仍然关联着连接和事务，只需在再次调用`ExecuteScalarAsync`之前更改值。你也可以创建一个新的`SqlCommand`对象，访问同一数据库中的不同表。通过调用`SqlTransaction`对象的`Commit`方法提交事务。提交之后，你可以在数据库中看到新记录：

```csharp
public static void TransactionSample()

{

    // etc.

    command.Parameters["CardType"].Value ="NeverLimits";

    command.Parameters["CardNumber"].Value ="987654321011";

    command.Parameters["ExpMonth"].Value = 12;

    command.Parameters["ExpYear"].Value = 2025;

    id = await command.ExecuteScalarAsync();

    WriteLine($"record added with id: {id}");

    // throw new Exception("abort the transaction");

    tx.Commit();

}
```
