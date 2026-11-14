

上面的代码还展示了一种从 **ExecuteXmlReader** 方法返回的 **XmlReader** 中提取 XML 数据的简单方法。需要注意的是，默认情况下，结果是一个 XML 片段，而不是有效的 XML 文档。它实际上是一组表示结果集中每一行的 XML 元素。因此，至少必须使用单个根元素包装输出，以使其格式正确。有关使用 **XmlReader** 的更多信息，请参阅在线 MSDN 文档中的“使用 XmlReader 读取 XML”，网址为 http://msdn.microsoft.com/en-us/library/9d8k26z1.aspx。

示例 **使用 SQL Server XML 查询将数据作为 XML 片段返回** 使用上面的代码查询 SQL Server 数据库。它以 FOR XML AUTO 查询的默认格式返回两个 XML 元素，数据集中每个列的值都表示为属性，如下所示。

```
<OrderList Id="1" Status="DRAFT" CreatedOn="2009-02-01T11:12:06" Name="Adjustable Race" LastName="Abbas" FirstName="Syed" ShipStreet="123 Elm Street" ShipCity="Denver" ShipZipCode="12345" ShippingOption="Two-day shipping" State="Colorado" /> <OrderList Id="2" Status="DRAFT" CreatedOn="2009-02-03T11:12:06" Name="All-Purpose Bike Stand" LastName="Abel" FirstName="Catherine" ShipStreet="321 Cedar Court" ShipCity="Denver" ShipZipCode="12345" ShippingOption="One-day shipping" State="Colorado" />
```

当您想要填充 XML 文档、转换数据以供显示或以其他形式持久化数据时，可以使用此方法。您可以使用 XSLT 样式表将数据转换为所需格式。有关 XSLT 的更多信息，请参阅“XSLT 转换”，网址为 http://msdn.microsoft.com/en-us/library/14689742.aspx。

## 检索单个标量值

使用数据库时，一个常见的要求是根据选择单行或单个值的查询提取单个标量值。这通常发生在使用查找表或检查数据库中特定实体是否存在时。数据访问块提供了 **ExecuteScalar** 方法来处理此要求。它执行您指定的查询，然后将结果集中第一行第一列的值作为 **Object** 类型返回。这意味着它比 **ExecuteReader** 方法提供更好的性能，因为不需要创建 **DataReader** 并将结果作为行集流式传输到客户端。为了最大限度地提高这种效率，您应该努力使用返回单个值或单行的查询。

**ExecuteScalar** 方法具有一组与本章前面使用的 **ExecuteReader** 方法类似的重载。您可以指定 **CommandType**（默认值为 **StoredProcedure**）以及 SQL 语句或存储过程名称。您还可以传入表示查询参数的 **Object** 实例数组。或者，您可以向该方法传递包含所需参数的 **Command** 对象。

以下代码演示了将 **Command** 对象传递给该方法以执行内联 SQL 语句和存储过程。它使用 GetSqlStringCommand 和 GetStoredProcCommand 方法从当前 Database 实例获取合适的 Command 实例。如果需要，可以在调用 ExecuteScalar 方法之前向命令添加参数。但是，为了演示该方法的工作方式，此处的代码只是提取完整的行集。结果是一个单个 Object，您必须在显示或在代码中使用它之前将其强制转换为适当的类型。

```
' Create a suitable command type for a SQL statement.
Using sqlCmd As DbCommand _
    = defaultDB.GetSqlStringCommand("SELECT [Name] FROM States")
' Call the ExecuteScalar method of the command.
Console.WriteLine("Result using a SQL statement: {0}", _
    defaultDB.ExecuteScalar(sqlCmd).ToString())
End Using
```

```
' Create a suitable command type for a stored procedure.
' NB: For efficiency, aim to return only a single value or a single row.
Using sprocCmd As DbCommand = defaultDB.GetStoredProcCommand("GetStatesList")
' Call the ExecuteScalar method of the command.
Console.WriteLine("Result using a stored procedure: {0}", _
    defaultDB.ExecuteScalar(sprocCmd).ToString())
End Using
```

您可以在示例“从 SQL 语句或存储过程返回单个标量值”中查看上面列出的代码运行情况。它产生的有些平淡无奇的结果如下所示。

```
Result using a SQL statement: Alabama
Result using a stored procedure: Alabama
```

## 异步检索数据

在了解了使用数据访问块提取数据的所有主要方法后，我们将继续探讨一些更有趣的场景（尽管许多人可能不愿将任何与数据访问相关的事情视为有趣……）。数据库通常不以成为应用程序中最快的组件而闻名——事实上，许多人会告诉您，它们是任何企业应用程序中的主要瓶颈。问题不在于它们效率低下，通常只是因为它们包含数百万行数据，而您需要执行的查询相对复杂。当然，也可能只是查询编写不佳导致性能不佳，但那是另一个故事了。

应用程序可以通过异步执行数据访问来最大限度地减少性能损耗。这意味着应用程序代码可以继续执行，并且用户界面在整个过程中可以保持交互。异步数据访问可能不适合每种情况，但它可能非常有用。

例如，您可能能够并发执行多个查询并合并结果以创建所需的数据集。或者查询多个数据库，仅使用最先返回结果的那个数据库的数据（这也是一种故障转移功能）。但是，请记住，异步数据访问会影响网络上的连接和数据流式传输性能。不要指望返回十行的查询使用异步方法会有任何改进——它更可能花费更长时间来返回结果！

数据访问块为许多标准数据访问方法提供了异步 Begin 和 End 版本，包括 ExecuteReader、ExecuteScalar、ExecuteXmlReader 和 ExecuteNonQuery。它还为以对象序列形式返回数据的访问器提供了 Execute 方法的异步 Begin 和 End 版本。您将在此处看到这两种技术。

## 为异步数据访问做准备

在异步执行查询之前，必须在要使用的数据库的连接字符串中指定适当的设置。默认情况下，连接的异步数据访问处于禁用状态，这可以防止它们承受与异步数据检索相关的性能损耗。要在连接上使用异步方法，连接字符串必须包含 Asynchronous Processing=true（或仅 async=true），如配置文件中 <connectionStrings> 部分的此示例所示。

```
<connectionStrings>
  <add name="AsyncExampleDatabase"
       connectionString="Asynchronous Processing=true; Data Source=.\SQLEXPRESS;
       Initial Catalog=MyDatabase; Integrated Security=True;"
       providerName="System.Data.SqlClient" />
  ...
</connectionStrings>
```

此外，数据访问块中的异步处理仅适用于 SQL Server 数据库。Database 类包含一个名为 SupportsAsync 的属性，您可以查询该属性以查看当前 Database 实例是否确实支持异步操作。本章的示例包含对此的简单检查。

还需要注意的是，异步数据访问通常涉及使用在与调用代码不同的线程上运行的回调。在现代应用程序中编写回调代码的常见方法是使用 Lambda 表达式，而不是单独的回调处理程序例程。但是，Visual Basic 第 9 版（在 Visual Studio® 2008 和 .NET Framework 3.5 版中）不完全支持用于回调的 Lambda 表达式，因此在此场景下您可能需要使用单独的回调例程。此回调通常无法直接访问 Windows® 窗体或 Windows Presentation Foundation (WPF) 应用程序中的用户界面。在大多数情况下，您需要使用委托调用原始 UI 类中的方法以更新回调返回的数据。

