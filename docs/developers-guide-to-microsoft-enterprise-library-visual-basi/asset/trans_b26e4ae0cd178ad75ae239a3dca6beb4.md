

- 接受 **CommandType** 值和表示命令的字符串的重载在您的应用程序执行内联 SQL 语句或不需要参数的存储过程时非常方便。
- 接受事务的重载允许您在现有事务中执行该方法。
- 如果使用 **SqlDatabase** 类型，可以使用方法的 **Begin** 和 **End** 版本异步执行多个常用方法。
- 可以使用 **Database** 类创建 **Accessor** 实例，以同步和异步方式执行数据访问操作，并将结果作为一系列适合使用 LINQ 等技术进行客户端查询的对象返回。

## 如何使用数据访问块？

在开始使用数据访问块之前，必须将其添加到您的应用程序中。配置该块以指定要使用的数据库，并将相关程序集添加到项目中。然后可以在代码中创建这些数据库的实例，并使用它们读取和写入数据。

## 配置块并引用所需程序集

使用数据访问块的第一步是配置要访问的数据库。该块使用 App.config、Web.config 或其他配置文件的标准 **<connectionStrings>** 节来存储各个数据库连接字符串，并添加一个小型 Enterprise Library 特定节，用于定义配置的数据库中哪个是默认数据库。可以使用 Enterprise Library 配置控制台配置所有这些设置，如图 1 所示。

![](img/d7009d38323c3b86f2dfbc5155fbf141_48_0.png)

图 1 为数据访问应用程序块创建新配置

配置所需数据库后，必须在应用程序代码中实例化它们。添加所需程序集的引用，并为代码中将使用的对象所在的命名空间添加 Imports 语句。除了每个 Enterprise Library 项目所需的 Enterprise Library 程序集（第 1 章“简介”中列出）之外，还必须引用或将程序集 Microsoft.Practices.EnterpriseLibrary.Data.dll 添加到 bin 文件夹。该程序集包含用于处理 SQL Server 数据库的类。

如果使用 SQL Server Compact Edition 数据库，还必须引用或添加程序集 Microsoft.Practices.EnterpriseLibrary.Data.SqlCe.dll。如果使用 Oracle 数据库，可以使用 Enterprise Library 包含的 Oracle 提供程序和 ADO.NET Oracle 提供程序，这要求引用或添加程序集 System.Data.OracleClient.dll。但是，请注意，OracleClient 提供程序在 .NET Framework 4.0 版中已弃用，尽管 Enterprise Library 仍支持它。对于未来的开发，请考虑选择其他 Oracle 驱动程序，例如 Enterprise Library Contrib 站点 http://codeplex.com/entlibcontrib 上提供的驱动程序。

为了更轻松地使用数据访问块中的对象，可以将相关命名空间（例如 Microsoft.Practices.EnterpriseLibrary.Data 和 Microsoft.Practices.EnterpriseLibrary.Data.Sql）的引用添加到项目中。

## 创建数据库实例

可以使用多种技术获取要访问的数据库的 Database 实例。第 1 章“简介”中的“实例化 Enterprise Library 对象”部分描述了可以使用的不同方法。本章可下载的示例使用最简单的方法：调用 EnterpriseLibraryContainer.Current 属性中可用的服务定位器的 GetInstance 方法（如下所示），并将这些实例存储在应用程序范围的变量中，以便从代码中的任何位置访问它们。

```
' Resolve the default Database object from the container.
' The actual concrete type is determined by the configuration settings.
Dim defaultDB As Database _
    = EnterpriseLibraryContainer.Current.GetInstance(Of Database)()

' Resolve a Database object from the container using the connection string name.
Dim namedDB As Database _
    = EnterpriseLibraryContainer.Current.GetInstance(Of Database)("ExampleDatabase")
```

上述代码演示了如何获取默认数据库和命名实例（使用连接字符串节中的名称）的实例。使用默认数据库是一种有用的方法，因为可以通过编辑配置文件更改配置中哪个数据库是默认数据库，而无需重新编译或重新部署应用程序。

请注意，上述代码将数据库实例引用为 Database 基类的实例。如果希望以后能够更改数据库类型，这是兼容性所必需的。但是，这意味着只能使用所有可能数据库类型中可用的功能（**Database** 类中定义的方法和属性）。

某些功能仅在特定数据库的具体类型中可用。例如，**ExecuteXmlReader** 方法仅在 **SqlDatabase** 类中可用。如果要使用此类功能，必须将实例化的数据库类型转换为相应的具体类型。以下代码创建 **SqlDatabase** 类的实例。

```
' Resolve a SqlDatabase object from the container using the default database.
Dim SqlServerDB As Database _
    = TryCast(EnterpriseLibraryContainer.Current.GetInstance(Of Database)()), _
    SqlDatabase)
```

除了使用配置来定义将使用的数据库之外，数据访问块还允许直接在代码中创建继承自 **Database** 类的具体类型的实例（如下所示）。只需提供指定相应 ADO.NET 数据提供程序类型（例如 **SqlClient**）的连接字符串即可。

```
' Assume the method GetConnectionString exists in your application and
' returns a valid connection string.
Dim myConnectionString As String = GetConnectionString()
Dim db As SqlDatabase = New SqlDatabase(myConnectionString)
```

## 示例应用程序

现在您已准备好新的 **Database** 对象，我们将向您展示如何使用它来执行各种任务。可以下载一个示例应用程序（一个简单的控制台应用程序），它演示了本章余下部分中将看到的所有场景。可以直接从 bin\debug 文件夹运行此应用程序，或在 Microsoft Visual Studio® 中打开名为 **DataAccess** 的解决方案，以在运行示例时查看所有代码。

本示例提供的数据库的两个连接字符串如下：

```
Data Source=.\SQLEXPRESS;
AttachDbFilename=|DataDirectory|\DataAccessExamples.mdf;
Integrated Security=True;User Instance=True
Data Source=.\SQLEXPRESS;Asynchronous Processing=true;AttachDbFilename=
|DataDirectory|\DataAccessExamples.mdf;
Integrated Security=True;User Instance=True
```

如果使用示例提供的脚本配置了其他数据库，运行此示例时可能会遇到不同的错误。很可能是 App.config 文件中数据库的连接字符串无效。此外，使用“管理工具”文件夹中的“服务” MMC 管理单元检查 SQL Server (SQLEXPRESS) 数据库服务（服务名为 **MSSQL$SQLEXPRESS**）是否正在运行。

此外，此块的最后一个示例使用分布式事务协调器 (DTC) 服务。此服务在您的计算机上可能未设置为自动启动。如果收到 DTC 服务不可用的错误，请从“管理工具”菜单打开“服务” MMC 管理单元并手动启动该服务；然后再次运行示例。

## 读取多个数据行

使用数据库时最常见的操作之一是读取多行数据。在 .NET 应用程序中，通常将这些行作为 DataReader 实例访问，或将其存储在 DataTable 中（通常位于创建的 DataSet 中）。本节将介绍返回 DataReader 的 ExecuteReader 方法的用法。本章后面将介绍如何将 DataSet 与数据访问块方法配合使用。

### 使用无参数查询读取行

由不带参数的内联 SQL 语句或存储过程组成的简单查询，可以使用接受 CommandType 值以及作为字符串的 SQL 语句或存储过程名称的 ExecuteReader 方法重载来执行。

以下代码演示了存储过程的最简单方法，其中也可以省略 CommandType 参数。默认值为 CommandType.StoredProcedure（与 ADO.NET 不同，ADO.NET 的默认值为 CommandType.Text）。

```
' Call the ExecuteReader method by specifying just the stored procedure name.
Using reader As IDataReader = namedDB.ExecuteReader("MyStoredProcName")
    ' Use the values in the rows as required.
End Using
```

若要使用内联 SQL 语句，必须指定相应的 CommandType 值，如下所示。

```
' Call the ExecuteReader method by specifying the command type
' as a SQL statement, and passing in the SQL statement
Using reader As IDataReader = namedDB.ExecuteReader(CommandType.Text, _
    "SELECT TOP 1 * FROM OrderList")
    ' Use the values in the rows as required - here we are just displaying them.
    DisplayRowValues(reader)
End Using
```

名为“使用无参数 SQL 语句返回行”的示例使用此代码检索包含示例数据库中第一个订单的 DataReader，然后显示此单行中的值。它使用一个简单的辅助例程，遍历所有行和列，并将值写入控制台屏幕。

