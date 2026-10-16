
在事务完成之前，无法看到事务 B 的中间状态。

- **持久性**——事务完成后，必须以持久方式存储。这意味着如果断电或服务器崩溃，重启时必须恢复状态。

> **注意** *事务和有效状态可以很容易地用婚礼仪式来比喻。一对新人站在事务协调员面前。事务协调员先问新人中的第一位：“你愿意与身边的这个人结婚吗？”如果第一位同意，再问第二位：“你愿意与这个人结婚吗？”如果第二位拒绝，第一位会收到回滚。这个事务的有效状态只能是双方都结婚，或者双方都不结婚。如果双方都同意，事务提交，双方进入已婚状态。如果一方拒绝，事务中止，双方都保持未婚状态。无效状态是一方已婚而另一方未婚。事务保证结果永远不会处于无效状态。*

使用 ADO.NET，可以通过调用 `SqlConnection` 的 `BeginTransaction` 方法启动事务。事务始终与一个连接相关联；你不能在多个连接上创建事务。`BeginTransaction` 方法返回一个 `SqlTransaction`，该事务需要与在同一事务下运行的命令一起使用（代码文件 `TransactionSamples/Program.cs`）：

```
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

> **注意** *实际上，你可以创建跨多个连接的事务。在 Windows 操作系统上，这需要使用分布式事务协调器。你可以使用 `TransactionScope` 类创建分布式事务。然而，这个类仅属于完整的 .NET Framework，并未引入 .NET Core；因此本书不涉及。如果你需要了解更多关于 `TransactionScope` 的信息，请参阅本书的前一版本，例如《Professional C# 5 and .NET 4.5.1》。*

代码示例在 `Sales.CreditCard` 表中创建一条记录。使用 SQL 子句 `INSERT INTO` 添加记录。`CreditCard` 表定义了一个自增标识符，该标识符由第二条 SQL 语句 SELECT SCOPE_IDENTITY() 返回，该语句返回创建的标识符。实例化 `SqlCommand` 对象后，通过设置 `Connection` 属性分配连接，并通过设置 `Transaction` 属性分配事务。对于 ADO.NET 事务，你无法将事务分配给使用不同连接的命令。但是，你也可以使用同一连接创建与事务无关的命令：

```
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

定义参数并填充值后，通过调用 `ExecuteScalarAsync` 方法执行命令。这次 `ExecuteScalarAsync` 方法与 `INSERT INTO` 子句一起使用，因为完整的 SQL 语句以返回单个结果结束：创建的标识符从 `SELECT SCOPE_IDENTITY()` 返回。如果在 `WriteLine` 方法之后设置断点并检查数据库中的结果，你不会在数据库中看到新记录，尽管创建的标识符已经返回。原因是事务尚未提交：

```
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

现在可以在同一事务中创建另一条记录。使用示例代码，继续使用相同的命令，该命令仍然关联着连接和事务，只需在再次调用 `ExecuteScalarAsync` 之前更改值。你也可以创建一个新的 `SqlCommand` 对象，访问同一数据库中的不同表。通过调用 `SqlTransaction` 对象的 `Commit` 方法提交事务。提交之后，你可以在数据库中看到新记录：

```
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
// etc.
}
```

如果发生错误，`Rollback` 方法会撤销同一事务中的所有 SQL 命令。状态会重置为事务开始之前的状态。你可以通过取消注释提交之前的异常语句来轻松模拟回滚：

```
public static void TransactionSample()
{
    // etc.

    catch (Exception ex)
    {
        WriteLine($"error {ex.Message}, rolling back");
        tx.Rollback();
    }
}
}
```

如果你以调试模式运行程序，并且断点激活时间过长，事务将会中止，因为达到了事务超时时间。事务在激活期间不应有用户输入。为了用户输入而增加事务超时时间也没有用，因为活动事务会导致数据库中的锁。根据你读取和写入的记录，可能会发生行锁、页锁或表锁。你可以通过为创建的事务设置隔离级别来影响锁以及数据库的性能。然而，这也会影响事务的 ACID 属性——例如，并非所有内容都是隔离的。

应用于事务的默认隔离级别是 `ReadCommitted`。下表显示了可以设置的不同选项。

| 隔离级别 | 描述 |
|---|---|
| ReadUncommitted | 事务之间互不隔离。使用此级别时，无需等待其他事务锁定的记录。这样，可以从其他事务读取未提交的数据——脏读。此级别通常仅用于读取那些是否读到中间更改并不重要的记录，例如报表。 |
| ReadCommitted | 等待其他事务中带有写锁的记录。这样可以避免脏读。此级别对当前读取的记录设置读锁，并对正在写入的记录设置写锁，直到事务完成。在读取一系列记录的过程中，每读取一条新记录，前一条记录就会被解锁。这就是为什么可能发生不可重复读。 |
| RepeatableRead | 对已读取的记录持有锁，直到事务完成。这样就避免了不可重复读的问题。幻读仍可能发生。 |
| Serializable | 持有范围锁。在事务运行期间，无法添加与正在读取数据所在范围相同的新记录。 |
| Snapshot | 使用此级别会对实际数据进行快照。此级别通过复制修改行来减少锁。这样，其他事务仍然可以读取旧数据，而无需等待锁释放。 |
| Unspecified | 表示提供程序使用的隔离级别不同于 `IsolationLevel` 枚举定义的值。 |
| Chaos | 此级别类似于 ReadUncommitted，但除了执行 ReadUncommitted 值的操作外，Chaos 不锁定更新的记录。 |

下表总结了设置最常用事务隔离级别时可能出现的问题。
