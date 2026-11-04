
```csharp
while (reader.Read())
{
    // Processing each row of data
    int employeeId = reader.GetInt32(0);
    string employeeName = reader.GetString(1);
    Console.WriteLine($"Employee ID: {employeeId}, Employee Name: {employeeName}");
}
}
}
}
}
```

## 主要特性与改进

ADO.NET Core 相对于传统 ADO.NET 提供了若干关键特性与改进，例如：

- **跨平台兼容性：** ADO.NET Core 可运行于不同的操作系统，如 Windows、macOS 和 Linux。
- **性能提升：** ADO.NET Core 针对性能进行了优化，与传统 ADO.NET 相比提供了更好的性能。
- **更高的灵活性：** ADO.NET Core 更加灵活且模块化，允许开发者根据具体需求选择所需组件。
- **支持新的数据源：** ADO.NET Core 支持新的数据源，例如 NoSQL 数据库，而传统 ADO.NET 不支持这些数据源。

理解 ADO.NET Core 的核心组件与架构，对于构建安全且可扩展的数据访问解决方案至关重要。通过利用其模块化设计，开发者可以创建高效、灵活的应用程序，以满足现代数据访问不断变化的需求。

## 使用 ADO.NET Core 构建应用程序

在本节中，我们将重点介绍使用 ADO.NET Core 构建安全且可扩展的数据访问解决方案的实际方面。我们将涵盖连接数据库、执行查询和检索数据、执行 CRUD 操作、处理错误和异常、优化性能以及保护数据访问等主题。

### 连接数据库

连接数据库是使用 ADO.NET Core 构建应用程序的第一步。可以使用 SqlConnection、MySqlConnection 或 NpgsqlConnection 类来完成，具体取决于你所使用的数据库。连接字符串包含服务器名称、数据库名称和身份验证详细信息等信息。

```csharp
using System.Data.SqlClient;

string connectionString = "Server=localhost;Database=SampleDatabase;Integrated Security=true;";
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    // Your code here
}
```

### 执行查询和检索数据

ADO.NET Core 支持不同类型的命令，如 SqlCommand、MySqlCommand 和 NpgsqlCommand，用于执行 SQL 查询和存储过程。ExecuteReader、ExecuteScalar 和 ExecuteNonQuery 方法用于从数据库检索数据。

```csharp
using (SqlCommand command = new SqlCommand("SELECT * FROM Employees", connection))
{
    using (SqlDataReader reader = command.ExecuteReader())
    {
        while (reader.Read())
        {
            // Process each row of data
        }
    }
}
```

### 执行 CRUD 操作

ADO.NET Core 支持使用 SQL 命令或存储过程执行创建、读取、更新和删除（CRUD）操作。可以使用参数将值传递给 SQL 命令，以防止 SQL 注入攻击。

```csharp
using (SqlCommand command = new SqlCommand("INSERT INTO Employees (Name) VALUES (@name)", connection))
{
    command.Parameters.AddWithValue("@name", "John Doe");
    command.ExecuteNonQuery();
}
```

### 处理错误和异常

错误处理对于构建健壮的应用程序至关重要。ADO.NET Core 提供了多种处理错误和异常的技术，例如使用 try-catch 块或 SqlException 类。

### 保护数据访问

保护数据访问对于保护敏感信息至关重要。ADO.NET Core 提供了多种用于保护数据访问的功能，例如加密连接字符串和使用安全通信协议。

```csharp
string connectionString = "Server=localhost;Database=SampleDatabase;Integrated Security=true;Encrypt=true";
```

在本节中，我们探讨了如何使用 ADO.NET Core 构建应用程序，重点包括连接数据库、执行查询和检索数据、执行 CRUD 操作、处理错误和异常、优化性能以及保护数据访问。通过理解这些概念，开发者可以使用 ADO.NET Core 构建安全且可扩展的数据访问解决方案。

## 将现有 ADO.NET 应用程序迁移到 ADO.NET Core

在本节中，我们将探讨如何将现有 ADO.NET 应用程序迁移到 ADO.NET Core。

- **1. 更新引用：** 将现有 ADO.NET 应用程序迁移到 ADO.NET Core 的第一步是更新项目中的引用。你需要将 ADO.NET 引用替换为 ADO.NET Core 引用，这些引用包含在 Microsoft.EntityFrameworkCore.SqlServer 包中。你可以使用 Visual Studio 中的 NuGet 包管理器或手动编辑项目文件来完成此操作。
- **2. 更新代码：** 接下来，你需要更新代码以使用 ADO.NET Core 的类和方法。这可能涉及更改连接字符串、数据读取器和数据适配器代码，以及与数据库交互的任何其他代码。
- **3. 测试：** 更新代码后，你需要测试应用程序，以确保它在 ADO.NET Core 下按预期工作。这可能涉及在测试环境（如虚拟机或云服务）中运行应用程序，并验证所有数据库操作是否按预期工作。
- **4. 部署：** 最后，在测试完应用程序后，你需要使用 ADO.NET Core 进行部署。这可能涉及将应用程序打包为 Docker 容器、发布到云服务或部署到 Web 服务器。

在本节中，我们探讨了如何将现有 ADO.NET 应用程序迁移到 ADO.NET Core。我们讨论了更新引用、更新代码、测试和部署。将现有 ADO.NET 应用程序迁移到 ADO.NET Core 可能是一个复杂的过程，但通过仔细规划和测试，你可以确保平稳过渡。在下一节中，我们将深入探讨数据提供程序的使用，敬请期待！

# 模块 5：使用数据提供程序

数据提供程序是使 .NET 应用程序能够与数据库交互的关键组件。在本模块中，我们将探讨不同类型的数据提供程序、它们的功能以及如何为你的应用程序选择合适的数据提供程序。

## 数据提供程序概述

数据提供程序是一组类，为 .NET 应用程序提供与特定数据库交互的方式。针对不同类型的数据库（如 SQL Server、Oracle、MySQL 和 SQLite）有多种数据提供程序可用。每个数据提供程序都有自己的一组用于执行数据库操作的类和方法。

## .NET 内置数据提供程序

.NET Framework 包含多个内置数据提供程序，例如用于 SQL Server 的 System.Data.SqlClient、用于 Oracle 的 System.Data.OracleClient，以及用于 OLE DB 数据库的 System.Data.OleDb。这些数据提供程序针对性能进行了优化，并与其各自的数据库系统提供了高水平的兼容性。

## 第三方数据提供程序

除了内置数据提供程序之外，还有适用于 .NET 应用程序的第三方数据提供程序。这些数据提供程序可能提供 .NET Framework 本机不支持的特定数据库系统的额外功能或支持。一些流行的第三方数据提供程序包括 Devart dotConnect、用于 PostgreSQL 的 Npgsql 和 MySQL Connector/.NET。

## 选择合适的数据提供程序

为你的应用程序选择数据提供程序时，需要考虑多个因素，例如你正在使用的数据库系统、所需的功能以及应用程序的性能要求。选择一款非常适合你特定需求的数据提供程序至关重要，以确保最佳性能和兼容性。

学完本模块后，你将深入了解数据提供程序及其在 .NET 应用程序中的作用。你还将知道如何为你的应用程序选择合适的数据提供程序，并准备好开始在 .NET 项目中与数据库打交道。

## 数据提供程序概述

在本节中，我们将概述数据提供程序，它们对于连接到各种数据库系统和执行数据库命令至关重要。

### 什么是数据提供程序？

数据提供程序是一组类和接口，允许你连接到数据库系统、执行数据库命令以及检索和操作数据。每个数据提供程序都特定于某个数据库系统，例如 SQL Server、MySQL 或 Oracle。

### .NET 内置数据提供程序

