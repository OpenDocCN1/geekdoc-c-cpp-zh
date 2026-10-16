

## 第四部分
## Web 应用程序与服务

- **第37章：** ADO.NET
- **第38章：** Entity Framework Core
- **第39章：** Windows 服务
- **第40章：** ASP.NET Core
- **第41章：** ASP.NET MVC
- **第42章：** ASP.NET Web API
- **第43章：** WebHooks 和 SignalR
- **第44章：** Windows Communication Foundation
- **第45章：** 部署网站和服务

## 37 ADO.NET

### 本章内容

- 连接数据库
- 执行命令
- 调用存储过程
- ADO.NET 对象模型

### 本章的 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 www.wrox.com/go/professionalcsharp6 的 Download Code 标签页找到。本章代码分为以下几个主要示例：

- ConnectionSamples
- CommandSamples
- AsyncSamples
- TransactionSamples

### ADO.NET 概述

本章讨论如何使用 ADO.NET 从 C# 程序访问关系数据库（如 SQL Server）。你将了解如何连接和断开数据库、如何使用查询、以及如何添加和更新记录。你还将学习各种命令对象选项，了解如何针对 SQL Server 提供程序类提供的每个选项使用命令；如何使用命令对象调用存储过程；以及如何使用事务。

以前，ADO.NET 附带不同的数据库提供程序：一个用于 SQL Server，一个用于 Oracle，使用 OLE DB 和 ODBC。OLE DB 技术已停止使用，因此新应用程序不应使用该提供程序。对于访问 Oracle 数据库，Microsoft 的提供程序也已停止使用，因为 Oracle 提供的提供程序（http://www.oracle.com/technetwork/topics/dotnet/）更符合需求。对于其他数据源（也包括 Oracle），有许多第三方提供程序可用。在使用 ODBC 提供程序之前，你应该使用针对所访问数据源的特定提供程序。本章中的代码示例基于 SQL Server，但你可以轻松更改，使用不同的连接和命令对象，例如访问 Oracle 数据库时使用 OracleConnection 和 OracleCommand，而不是 SqlConnection 和 SqlCommand。

> **注意** *本章不涉及在内存中保存表的 `DataSet`。DataSet 使你可以从数据库中检索记录，并将内容存储到带有关系的内存数据表中。你应该改用 Entity Framework，这将在第38章“Entity Framework Core”中讨论。Entity Framework 使你可以使用对象关系，而不是基于表的关系。*

### 示例数据库

本章的示例使用 AdventureWorks2014 数据库。你可以从 https://msftdbprodsamples.codeplex.com/ 下载该数据库。通过此链接，你可以下载 AdventureWorks2014 数据库的备份 zip 文件。选择推荐的下载——Adventure Works 2014 Full Database Backup.zip。解压该文件后，可以使用 SQL Server Management Studio 还原数据库备份，如图 37.1 所示。如果你的系统没有 SQL Server Management Studio，可以从 http://www.microsoft.com/downloads 下载免费版本。

![](img/3d365b72b289213a91ade7eb366b8f35_1430_0.png)

**图 37.1**

本章使用的 SQL Server 是 SQL Server LocalDB。这是随 Visual Studio 安装的数据库服务器。你也可以使用任何其他 SQL Server 版本；只需相应地更改连接字符串。

### NuGet 包和命名空间

所有 ADO.NET 示例代码都使用以下依赖项和命名空间：

**依赖项**

- NETStandard.Library
- Microsoft.Extensions.Configuration
- Microsoft.Extensions.Configuration.Json
- System.Data.SqlClient

**命名空间**

- Microsoft.Extensions.Configuration
- System
- System.Data
- System.Data.SqlClient
- System.Threading.Tasks
- static System.Console

### 使用数据库连接

要访问数据库，你需要提供连接参数，例如运行数据库的计算机以及可能的登录凭据。你可以使用 SqlConnection 类连接到 SQL Server。

以下代码片段演示了如何创建、打开和关闭到 AdventureWorks2014 数据库的连接（代码文件 ConnectionSamples/Program.cs）：

```csharp
public static void OpenConnection()
{
    string connectionString = @"server=(localdb)\MSSQLLocalDB;" +
        "integrated security=SSPI;" +
        "database=AdventureWorks2014";
    var connection = new SqlConnection(connectionString);
    connection.Open();

    // Do something useful
    WriteLine("Connection opened");

    connection.Close();
}
```

> **注意** `SqlConnection` 类除了 `Close` 方法外，还实现了带有 `Dispose` 方法的 `IDisposable` 接口。两者作用相同，都是释放连接。因此，你可以使用 `using` 语句来关闭连接。

在示例连接字符串中，使用的参数如下（在连接字符串中参数以分号分隔）：

- `server=(localdb)\MSSQLLocalDB` — 指定要连接的数据库服务器。SQL Server 允许在同一台机器上运行多个独立的数据库服务器实例。这里，你连接的是 LocalDB 服务器以及随 SQL Server 安装创建的 MSSQLLocalDB 实例。如果你使用的是本地安装的 SQL Server，请将此部分更改为 `server=(local)`。除了使用关键字 `server`，你也可以使用 `Data Source`。连接到 SQL Azure 时，可以设置 `Data Source=servername.database.windows.net`。
- `database=AdventureWorks2014` — 指定要连接的数据库实例；每个 SQL Server 进程可以公开多个数据库实例。除了使用关键字 `database`，你也可以使用 `Initial Catalog`。
- `integrated security=SSPI` — 使用 Windows 身份验证连接到数据库。如果你使用 SQL Azure，则需要设置 `User Id` 和 `Password`。

> **注意** 你可以在 http://www.connectionstrings.com 找到许多不同数据库连接字符串的丰富信息。

ConnectionSamples 示例使用定义的连接字符串打开数据库连接，然后关闭该连接。打开连接后，你可以对数据源发出命令；完成后，可以关闭连接。

### 管理连接字符串

与其在 C# 代码中硬编码连接字符串，不如从配置文件读取。在 .NET 4.6 和 .NET Core 1.0 中，配置文件可以是 JSON 或 XML 格式，也可以从环境变量中读取。在下面的示例中，连接字符串从 JSON 配置文件读取（代码文件 ConnectionSamples/config.json）：

```json
{
  "Data": {
    "DefaultConnection": {
      "ConnectionString": "Server=(localdb)\\MSSQLLocalDB;Database=AdventureWorks2014;Trusted_Connection=True;"
    }
  }
}
```

可以使用 NuGet 包 Microsoft.Extensions.Configuration 中定义的 Configuration API 读取 JSON 文件。要使用 JSON 配置文件，还需要添加 NuGet 包 Microsoft.Extensions.Configuration.Json。为了读取配置文件，可以创建 ConfigurationBuilder。AddJsonFile 扩展方法将 JSON 文件 config.json 添加到配置读取中——如果该文件与程序在同一路径下。要配置不同路径，可以调用 SetBasePath 方法。调用 ConfigurationBuilder 的 Build 方法会从所有添加的配置文件中构建配置，并返回一个实现 IConfiguration 接口的对象。这样，就可以检索配置值，例如 Data:DefaultConnection:ConnectionString 的配置值（代码文件 ConnectionSamples/Program.cs）：

```csharp
public static void ConnectionUsingConfig()
{
    var configurationBuilder =
        new ConfigurationBuilder().AddJsonFile("config.json");
    IConfiguration config = configurationBuilder.Build();
    string connectionString =
        config["Data:DefaultConnection:ConnectionString"];
    WriteLine(connectionString);
}
```

### 连接池

多年前在构建两层应用程序时，在应用程序启动时打开连接并在应用程序关闭时才关闭它是一个好做法。如今，这不再是一个好做法。这种程序架构的原因是打开连接需要一些时间。现在，关闭连接并不会关闭与服务器的连接。相反，连接会被添加到连接池中。当你再次打开连接时，可以从池中取出，因此打开连接非常快；只有第一次打开连接才会耗时。

可以通过连接字符串中的多个选项来配置连接池。将 `Pooling` 选项设置为 false 将禁用连接池；默认情况下它是启用的——`Pooling = true`。`Min Pool Size` 和 `Max Pool Size` 使你可以配置池中的连接数。默认情况下，`Min Pool Size` 的值为 0，`Max Pool Size` 的值为 100。`Connection Lifetime` 定义连接在真正释放之前在池中保持不活动的时长。

### 连接信息

创建连接后，你可以注册事件处理程序以获取有关连接的一些信息。SqlConnection 类定义了

