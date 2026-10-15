

如果将它通过 SqlCommand（或任何执行方法）的 ExecuteReader 传递给 SQL Server，SQL Server 在运行之前必须先编译代码，就像 VB .NET 应用程序在执行前必须先编译一样。这种编译会占用 SQL Server 的时间，因此很容易推断，如果能减少 SQL Server 需要进行的编译量，数据库性能应该会提高。（比较编译应用程序与解释代码的执行速度。）

这就是存储过程的全部意义：你创建一个过程，将其存储在数据库中，并且由于该过程事先被识别和理解，因此可以提前编译并准备好在应用程序中使用。

使用存储过程在代码中还有一个好处，那就是通常更安全。在不使用存储过程的情况下使用 SQL 时，总会有构建 SQL 语句时拼接字符串的诱惑。这样做存在危险——特别是如果其中一些字符串由用户生成——生成的 SQL 可能是无效的或恶意的；例如，如果你有一个文本框，用户可以在其中输入搜索条件，然后你将其拼接进查询，使用如下代码：

```
Dim sql As String = "SELECT * FROM myTable WHERE field LIKE '" & query & "%'"
```

这看起来无害，但如果你让用户输入类似以下内容，很快就会出问题：

```
Bob;delete * from systables;
```

使用存储过程可以防止此类攻击的发生。

存储过程非常容易使用，但访问它们的代码有时有点冗长。下一节演示了一些可以使访问存储过程更简便的代码，但为了更清晰，让我们先通过构建一个简单的应用程序来演示如何创建和调用存储过程。

## 创建存储过程

要创建存储过程，你可以使用 Visual Studio .NET 中的工具，也可以使用 SQL Server 2000 中的 SQL Server 企业管理器中的工具，或者如果你使用的是 SQL Server 2005/2008，则使用 SQL Server Management Studio 中的工具。（从技术上讲，你可以使用第三方工具或只是在一个好旧的 SQL 脚本中创建存储过程。）

此示例构建一个存储过程，返回给定作者 ID 的所有列。执行此操作的 SQL 如下所示：

```
SELECT
    au_id, au_lname, au_fname, phone,
    address, city, state, zip, contract
FROM
    authors
WHERE
    au_id = whatever author ID you want
```

“whatever author ID you want” 部分很重要。在使用存储过程时，你通常必须能够向存储过程提供参数并在代码中使用它们。这不是一本关于 SQL Server 的书，因此本示例仅关注所涉及的原理。你可以在网上找到许多关于构建存储过程的资源（它们已经存在很长时间了，而且绝对不是 .NET 特定的功能）。

SQL Server 中的变量以 @ 符号为前缀，因此如果你的变量名为 au_id，则你的 SQL 将如下所示：

```
SELECT
    au_id, au_lname, au_fname, phone,
    address, city, state, zip, contract
FROM
    authors
WHERE
    au_id = @au_id
```

在创建 Command 对象实例后，通过调用 Command 对象的 ExecuteReader 方法创建 DataReader。以下是创建 DataReader 并遍历它以将值打印到屏幕的示例：

```
Private Sub TraverseDataReader()
    ' Build the SQL and Connection strings.
    Dim sql As String = "SELECT * FROM authors"
    Dim connectionString As String = "database=pubs;" & "server=(local)\sqlexpress;trusted_connection=true;"
    ' Initialize the SqlCommand with the SQL query and connection strings.
    Dim command As SqlCommand = New SqlCommand(sql, _
        New SqlConnection(connectionString))
    ' Open the connection.
    command.Connection.Open()
    ' Execute the query, return a SqlDataReader object.
    ' CommandBehavior.CloseConnection flags the
    ' DataReader to automatically close the DB connection
    ' when it is closed.
    Dim reader As SqlDataReader = _
        command.ExecuteReader(CommandBehavior.CloseConnection)
    ' Loop through the records and print the values.
    Do While reader.Read
        Console.WriteLine(reader.GetString(1) & " " & reader.GetString(2))
    Loop
    ' Close the DataReader (and its connection).
    reader.Close()
End Sub
```

代码片段来自 AdoNetFeaturesTest 项目

此代码片段使用 SqlCommand 对象通过 ExecuteReader 方法执行查询。此方法返回一个填充的 SqlDataReader 对象，你可以遍历它然后打印出作者姓名。此代码与遍历 DataTable 的行之间的主要区别在于，你在遍历 DataReader 对象中的数据时必须保持连接；这是因为 DataReader 每次只读取少量数据流以节省内存空间。

> 在这一点上，一个明显的设计问题是是否使用 DataReader 或 DataSet。答案取决于性能以及你将如何使用数据。如果你想要高性能并且只需要访问检索到的数据一次，那么 DataReader 是最佳选择。如果你需要多次访问相同的数据，或者需要在内存中建模复杂的关系，或者需要在不连接数据库时使用数据，那么 DataSet 是最佳选择。始终在决定哪一个最好之前彻底测试每个选项。

DataReader 对象的 Read 方法用于从查询结果中获取一行。返回行的每一列都可以通过传递列的名称或序数引用给 DataReader 来访问；或者，为了获得最佳性能，DataReader 提供了一系列方法，使你能够以其原生数据类型访问列值（GetDateTime、GetDouble、GetGuid、GetInt32 等）。当底层数据类型已知时使用类型化访问器方法可以减少检索列值时所需的类型转换量（从 Object 类型转换）。

DataReader 提供了一个非缓冲的数据流，使过程逻辑能够高效地顺序处理来自数据源的结果。DataReader 在检索大量数据时是一个不错的选择；一次只加载一行数据到内存中。你在使用完 DataReader 对象后应始终调用 Close 方法，以及关闭 DataReader 对象的数据库连接；否则，连接将保持打开状态，直到垃圾回收器收集该对象为止。或者，使用 Using 语句在 Using 子句结束时自动关闭数据库连接。

注意你在 `SqlDataReader.ExecuteReader` 方法上使用 `CommandBehavior.CloseConnection` 枚举值。这告诉 `SqlCommand` 对象在调用 `SqlDataReader.Close` 方法时自动关闭数据库连接。

> 如果你的命令包含输出参数或返回值，它们在 DataReader 关闭之前将不可用。

## 异步执行命令

在 ADO.NET 中，提供了额外的支持，使 Command 对象能够异步执行其命令，这在许多应用程序中，尤其是 Windows 窗体应用程序中，可以带来巨大的感知性能提升。这在你必须执行长时间运行的 SQL 语句时尤其方便。本节探讨此功能如何使你能够添加异步处理以增强应用程序的响应能力。

SqlCommand 对象提供三种不同的异步调用选项：BeginExecuteReader、BeginExecuteNonQuery 和 BeginExecuteXmlReader。每种方法都有对应的“结束”方法——即 EndExecuteReader、EndExecuteNonQuery 和 EndExecuteXmlReader。现在你熟悉了 DataReader 对象，让我们看一个使用 BeginExecuteReader 方法执行长时间运行查询的示例。

在 AdoNetFeaturesTest 项目中，我向窗体添加了一个按钮和一个关联的 Click 事件处理程序，该处理程序将启动异步调用以获取 DataReader 实例：

```
Private Sub _testAsyncCallButton_Click(ByVal sender As System.Object,
        ByVal e As System.EventArgs) Handles _testAsyncCallButton.Click

    ' Build a connection for the async call to the database
    Dim connection As SqlConnection = GetPubsConnection()
    connection.ConnectionString &= "Asynchronous Processing=true;"

    ' Build a command to call the stored procedure
    Dim command As New SqlCommand("usp_Long_Running_Procedure", connection)

    ' Set the command type to stored procedure
    command.CommandType = CommandType.StoredProcedure

    ' The reader requires an open connection
    connection.Open()

    ' Make the asynchronous call to the database
    command.BeginExecuteReader(AddressOf Me.AsyncCallback,
    command, CommandBehavior.CloseConnection)
End Sub
```

*代码片段来自 AdoNetFeaturesTest 项目*

首先，你重用你的辅助方法 GetPubsConnection 来获取到 pubs 数据库的连接。接下来，这一点非常重要，你将语句 "Asynchronous Processing=true" 附加到你的 Connection 对象的连接字符串中。必须设置此项才能使 ADO.NET 对 SQL Server 进行异步调用。

在连接设置好后，你然后构建一个 SqlCommand 对象并初始化它以能够执行 usp_Long_Running_Procedure 存储过程。此过程通过使用 SQL Server WAITFOR DELAY 语句在执行 usp_Authors_Get_All 存储过程之前创建 20 秒的延迟来模拟长时间运行的查询。正如你可能猜到的，usp_Authors_Get_All 存储过程只是从 authors 表中选择所有作者。延迟只是为了演示

