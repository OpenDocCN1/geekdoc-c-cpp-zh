

# 使用 C# 进行 SQL Server 数据库编程

某些旧数据库系统仅支持 ODBC 作为访问技术，包括旧版本的 SQL Server 和 Oracle，以及如 Sybase 等第三方数据库。

## 3.4.1.2 OLEDB 数据提供程序

System.Data.OleDb 命名空间包含了 .NET Framework 2.0 为 OLE DB 数据提供程序所使用的所有类。.NET Framework OLE DB 数据提供程序描述了一组用于在托管空间中访问 OLE DB 数据库源的类。使用 `OleDbDataAdapter`，你可以填充一个内存驻的 `DataSet`，并使用它来查询和更新数据源。以下数据提供程序支持：

- Microsoft Access
- SQL Server (7.0 或更高版本)
- Oracle (9 或更高版本)

使用 OLEDB.NET 数据提供程序的一个优势是允许用户开发通用的数据应用程序。所谓的通用应用程序意味着你可以使用 OLEDB.NET 数据提供程序——你可以使用它来访问任何数据源，例如 Microsoft Access、SQL Server、Oracle 及其它任何支持 OLEDB 的其他数据源。

图 3.4 显示了 OLEDB 数据提供程序与 OLE DB.NET 提供程序之间的兼容性。

## 3.4.1.3 SQL Server 数据提供程序

此数据提供程序通过其内部协议访问 7.0 或更高版本的 SQL Server 数据库。该数据提供程序的功能设计类似于 .NET Framework 的 OLE DB、ODBC 和 Oracle 数据提供程序。与此提供程序相关的所有类都定义在一个 DLL 文件中并位于 `System.Data.SqlClient` 命名空间。虽然微软提供了不同的数据提供程序来访问 SQL Server 数据库中的数据（如 ODBC 和 OLE DB），但为了实现最优操作，强烈建议使用此提供程序访问 SQL Server 数据源中的数据。

如图 3.4 所示，此数据提供程序是一个新版本，它仅适用于 SQL Server 7.0 及更高版本。如果使用旧版本的 SQL，则需要使用 OLE DB.NET 或 SQLOLEDB 数据提供程序。

## 3.4.1.4 Oracle 数据提供程序

此数据提供程序是 .NET Framework 的扩展，提供了对 Oracle 数据库的访问。与此提供程序相关的所有类位于 `System.Data.Oracle` 命名空间。此提供程序依赖于 Oracle 客户端软件提供的 Oracle 客户端接口。你需要在计算机上安装 Oracle 客户端才能使用此数据提供程序。微软提供了多种访问存储在 Oracle 数据库中的数据的方法，例如 Microsoft ODBC for Oracle 和 OLE DB，你应该使用此 Oracle 数据提供程序访问 Oracle 数据源，因为这是访问 Oracle 数据库最高效的方法。

此数据提供程序仅适用于最新版本的 Oracle 数据库（如 8.1.7）。对于旧版本的 Oracle 数据库，你需要使用 MSDAORA 或 OLE DB.NET。

| 提供程序名称 | 描述 |
|---|---|
| SQLOLEDB | 用于 Microsoft SQL Server 6.5 或更早版本 |
| Microsoft.Jet.OLEDB.4.0 | 用于 Microsoft JET 数据库 (Microsoft Access) |
| MSDAORA | 用于 Oracle 7 或更高版本的数据库 |

图 3.4 OLEDB 与 OLEDB.NET 之间的兼容性。

# ADO.NET 简介

如前部分所述，所有不同的数据提供程序都使用相似的对象、属性和方法对不同的数据库执行数据操作。在接下来的章节中，我们将详细讨论这些用于不同数据提供程序的相似对象、属性和方法。

## 3.4.2 Connection 类

如图 3.1 和 3.2 所示，数据提供程序包含四个子类，`Connection` 组件是其中之一。该类在你的应用程序与你选择连接到项目的数据库之间提供了连接。要使用此类类建立应用程序与目标数据库之间的连接，你首先需要基于该类创建一个实例或对象。根据你的应用程序需求，你可以为整个项目创建一个全局实例，也可以为你的每个窗口创建本地连接对象。全局实例是一个较好的选择，因为你不需要对对象执行多次打开和关闭连接的操作。本书中的所有示例项目都使用了全局连接。

你想要使用的 `Connection` 对象取决于你所选择的数据源类型。数据提供程序提供了四种不同的 `Connection` 类，每个类都对应一个不同的数据源。基础 3.5 列出了用于不同数据源的这些 `Connection` 类：

`new` 关键字用于创建 `Connection` 类的新实例或对象。虽然不同的类提供了重载的构造函数，但 Visual C#.NET 2008 使用了两个常用的构造函数。其中一个不接受任何参数，而另一个接受连接字符串作为参数，且该构造函数在数据连接中使用得最频繁。

连接字符串是 `Connection` 类的一个属性，它提供了连接到数据源的所有必要信息。通常，此连接字符串包含几个定义连接的参数，但只有五个参数被广泛用于数据驱动应用程序：

1) Provider (提供程序)
2) Data Source (数据源)
3) Database (数据库)
4) User ID (用户名)
5) Password (密码)

连接字符串中包含参数可能略有不同。例如，OLE DB 和 ODBC 数据库都需要连接字符串中包含所有五个参数以连接 OleDb 或 ODBC 数据源。对于 SQL Server 连接，你可能需要使用 `Server` 来替换 `Provider` 参数，而对于 Oracle 数据库连接，你的连接字符串中完全不需要 `Provider` 和 `Database` 参数。你可以在第 5 章第 5.15 节找到这些差异。

连接字符串中的参数可能存在细小差异。例如，OLE DB 和 ODBC 数据库都需要连接字符串中包含所有五个参数以连接 OleDb 或 ODBC 数据源。对于 SQL Server 连接，你可能需要使用 `Server` 来替换 `Provider` 参数，而对于 Oracle 数据库连接，你的连接字符串中完全不需要 `Provider` 和 `Database` 参数。你可以在第 5 章第 5.15 节找到这些差异。

连接字符串中的参数名称通常不区分大小写，但某些参数（如 `Password`）可能是区分大小写的。

| 连接类 | 关联数据库 |
|---|---|
| OdbcConnection | ODBC 数据源 |
| OleDbConnection | OLE DB |
| SqlConnection | SQL Server 数据库 |
| OracleConnection | Oracle 数据库 |

图 3.5 连接类与数据库。

带有通用连接字符串的典型连接实例可以表示如下：

```csharp
xxxConnection Connection = new xxxConnection("Provider=MyProvider;" + +
"Data Source=MyServer;" + +
"Database=MyDatabase;" + +
"User ID=MyUserID;" + +
"Password=MyApp;
```

其中 `xxx` 应该替换为应用程序中所选的数据程序，如 `OleDb`、`Sql` 或 `Oracle`。你需要使用实际实现的值来替换这些示例值，如 `MyServer`、`MyDatabase`、`MyUserID` 和 `MyPassword`。`Provider` 指的是驱动程序。如果你在计算机上安装了本地 SQL Server 客户端（例如 SQL Server 2019 Express），`Provider` 可以是 `localhost`。如果你正在使用远程 SQL Server 实例，你需要使用服务器的网络名称。如果你使用的是默认实例名 `SQLX`，你需要将 `SQLEXPRESS` 作为 `Provider` 的值。对于 Oracle 数据库，你不需要使用此参数。`Data Source` 参数指定安装并运行 SQL Server 或 Oracle 的网络计算机。`Database` 参数指定你的数据库名称。`User ID` 和 `Password` 参数用于数据库的安全问题。通常使用默认的 Windows 身份验证。

下面列出了不同数据库的一些典型连接实例：

# 用于 Microsoft Access 的 OLE DB 提供程序

```csharp
OleDbConnection Connection = new OleDbConnection("Provider=Microsoft.Jet.OLEDB.4.0;")
```

```csharp
"Data Source=C:\database\CSE_DEPT.mdb;" + +
"User ID=MyUserID;" + +
"Password=MyApp;")
```

# 用于 SQL Server 数据库的 SQL Server 数据提供程序

```csharp
SqlConnection Connection = new SqlConnection("Server=localhost;" + +
"Data Source=YBAI\SQLEXPRESS;" + +
"Database=CSE_DEPT;" + +
"Integrated Security=SSPI;")
```

# 用于 Oracle 数据库的 Oracle 数据提供程序

```csharp
OracleConnection Connection = new OracleConnection("Data Source=XE;" + +
"User ID=system;" + +
"Password=come")
```

