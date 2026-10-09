
# 第 16 章

## ADO.NET

本章主题包括以下内容：

- `ADO.NET` 的主要组件
- 连接或创建数据库
- 从数据库访问数据
- 在表中插入行
- 更新表

对于一个功能齐全的网站来说，需要数据持久化是非常性质的。与产品、客户、用户、图片等相关的信息需要存储以供备后参考。数据库负责存储、检索和操作数据。数据库中的数据以表的形式维护，表又被分为行和列。表中的每一行都包含与产品、客户和用户相关的完整信息。行中存储的信息由多个属性组成，例如产品名称、价格、数量和制造数据。数据库中的数据可以在运行时存储和检索，这为动态网站提供了可能，根据用户输入的内容获取并显示信息。为了在数据库中存储、访问和操作信息，使用了一种名为结构化查询语言（`SQL`）的语言。

数据库有多种类型，但最流行且在网站中广泛使用的是关系型数据库。*关系型数据库*是指一个表的行可以与其他表的行关联的数据库。表与表之间的关系有助于避免表中重复或相同的数据。

`ADO` 代表 `Active Data Objects`（活动数据对象），`ADO.NET` 库是一个丰富的框架，它可以检索和更新各种关系型数据库中的信息，包括 `Microsoft SQL Server`、`Microsoft Access`、`Oracle` 和 `XML`。`ADO.NET` 依赖于 `.NET Framework` 的各种类来处理请求并在数据库系统与用户之间转换。

> 注意
> `ADO.NET Entity Framework` 提供了直接从代码更方便地访问数据库操作。

### 检查 ADO.NET 的主要组件

用于访问和操作数据的 `ADO.NET` 主要组件是 `DataSet` 和 `Data Provider`（数据提供程序）。表 16.1 显示了这些 `ADO.NET` 组件的简要描述。

| 表 16.1 ADO.NET 组件 |
| 组件 | 描述 |
| `DataSet` | `DataSet` 代表相关数据表的本地副本。换句话说，`DataSet` 由一个或多个 `DataTable` 对象组成，根据用户需求对它们进行操作和更新，然后通过特定的数据适配器处理修改后的数据。`DataSet` 可以与多个不同的数据源工作，包括 `XML` 数据。 |
| `DataTable` | 管理每个实体的信息。每个 `DataTable` 包含零或多行数据。表行中显示的单个数据值通过 `DataColumn` 定义来标识。`DataColumn` 定义包含了根据每列中存储的数据类型定义的类型声明。除了数据的行和列外，`DataTable` 还包括主键、外键、约束。 |
| `DataColumn` | （此处对应原文中重复的 `DataTable` 描述部分，按要求翻译或保持逻辑） |

### 连接或创建数据库

`SqlDataAdapter`, `OleDbAdapter`, 和 `ODBCDataAdapter`

用于处理 `DataSet` 和数据源之间的交互。帮助执行不同的 `SQL` 命令以填充 `DataSet` 并更新数据源。

`SqlDataReader`, `OleDbReader`, 和 `ODBCDataReader`

用于使用光标对数据进行向前且只读的访问。

`SqlParameter`, `OleDbParameter`, 和 `ODBCParameter`

用于定义传递存储过程的参数。

`SqlTransaction`, `OleDbTransaction`, 和 `ODBCTransaction`

用于表示在数据源中进行的事务。

© 2015 Cengage Learning®

这些类实现了在 `System.Data` 命名空间内定义的一组标准接口。这里给 `ADO.NET` 中使用的命名空间概述：

- `System.Data`—包含所有通用数据访问类
- `System.Data.Common`—包含各个数据提供程序共享或重写的的类
- `System.Data.EntityClient`—包含 `Entity Framework` 类
- `System.Data.Odbc.SqlClient`—包含 `LINQ to SQL` 提供程序类
- `System.Data.OleDb`—包含 `ODBC` 提供程序类
- `System.Data.ProviderBase`—包含新的基类和连接工厂类
- `System.Data.Sql`—包含 `SQL Server` 数据访问的通用接口和类
- `System.Data.SqlClient`—包含 `SQL Server` 提供程序类
- `System.Data.SqlTypes`—包含 `SQL Server` 数据类型

为了理解上述概念，你将学习创建数据库并查看数据是如何存储和从其中检索的。你将使用 `SQL Server` 完成此任务。

启动 `Visual Studio`，通过选择 `文件（File）`、`新建网站（New Web Site）` 创建一个新网站。从左侧选项卡选择 `Visual C#` 作为编程语言。由于你想创建一个不包含默认 Web 页面的空网站，请从已安装模板列表中选择 `ASP.NET` 空网站。`ASP` 代表 `Active Server Pages`。`Web location` 下拉列表提供以下三个选项：

- `File System`（文件系统）—这将在物理文件系统中创建网站文件夹，Web 将在 `Visual Studio` 内部 Web 服务器的帮助下执行，而不是在 `Internet Information Services（IIS）`。`IIS` 是用于运行 `ASP.NET` 应用程序的 Web 服务器。
- `HTTP`—这意味着你将创建的网页将使用 `IIS` 运行，且 Web 必须位于 `IIS` 虚拟目录中。虚拟目录将自动创建。假设你的应用程序名称为 `Website1`。可以通过 `http://localhost/Website1/Default.aspx` 访问网页。
- `FTP`—代表文件传输协议（`File Transfer Protocol`）。当你想要在远程位置开发网站时，使用 `FTP` 选项。系统提示输入远程服务器、`FTP` 用户 ID 和 `FTP` 密码。网站将在远程服务器上创建。

从 `Web Location` 下拉列表中选择 `File System` 选项。输入应用程序名称为 `WebApp1`（见图 16.1）。点击确定。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_506_0.png)

**图 16.1** 创建一个新的空网站。
经微软许可使用。

`Visual Studio` 创建了一个名为 `WebApp` 的网站以及一个名为 `Web.config` 的配置文件。对于该空网站，你可以通过在解决方案管理器（`Solution Explorer`）中右键点击你的应用程序，并选择添加（`Add`）、添加新项（`Add New Item`）来添加 Web 表单。打开添加新项对话框（见图 16.2），选择 `Web Form`（`Web 表单`）。让 Web 表单的默认名称为 `Default.aspx`，然后点击按钮。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_507_0.png)

图 16.2
向应用程序添加 Web 表单。
经微软许可使用。

你将获得一个设计界面，用于从工具箱放置控件，如图 16.3 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_507_1.png)

图 16.3
`Default.aspx` 设计窗口。
经微软许可使用。

两个用于连接的简要介绍：

- `服务器资源管理器（Server Explorer）` 在不提供用户 ID 或密码的情况下访问数据库（使用 Windows 身份验证）。你将在示例中使用它。
- `数据连接（Data Connections）` 显示表列表。
- `服务器（Servers）` 列出可用服务器。
- `Windows Azure`—访问数据库。

从数据源框中，选择你需要连接的数据源类型。默认情况下，数据源框显示你的应用程序的数据源。点击更改（`Change`）按钮打开数据源对话框（见图 16.5）。从数据源下拉列表中选择 `Microsoft SQL Server`，从提供程序下拉列表中选择 `.NET Framework Data Provider for SQL Server`。点击确定返回。

`服务器名称`—显示服务器的名称。要选择不同的服务器，从下拉列表中选择所需的选项。对于 `SQL Server Express` 实例，需要在本地计算机名称后附加 `\LEXPRESS`。使用完整 `SQL Server` 时不需要 `\LEXPRESS` 后缀。对于托管在相同系统上的 `SQL Server` 实例，可以使用 `(local)` 作为服务器名称。要指定本地 `SQL Server Express`，在文本框中输入 `.\sqlexpress`。在服务器名称框中输入 `(local)` 以访问相同系统上的 `SQL Server`（见图 16.4）。

- 使用 Windows 身份验证（`Use Windows Authentication`）在不提供用户 ID 或密码的情况下访问数据库。
- 使用 SQL Server 身份验证（`Use SQL Server Authentication`）需要有效的用户名和密码来打开数据库连接。
- 用户名（`User Name`）输入访问数据库的用户 ID。提供的用户名必须有访问指定数据库的权限。
- 密码（`Password`）输入密码的文本框。
- 保存我的密码（`Save My Password`）保存并加密密码，这样你每次打开连接时都无需输入密码。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_509_0.png)

图 16.4
左）向服务器添加连接的对话框。
右）填写服务器信息后的对话框。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_510_0.png)

图 16.5
更改数据源信息的对话框。

- 选择或输入数据库名称—显示您可以连接的可用数据库。若要创建一个新数据库，您需要向文本框中输入其名称并点击 `OK` 按钮。这将创建一个名为 `SharpSampleDatabase` 的新数据库（参见图 16.4 [右侧]）。
- 附加数据库文件—将现有的数据库名称附加到应用程序中。点击“浏览”来定位数据库文件。
- 逻辑名称—显示此数据库连接的名称。
- 高级—显示“高级属性”对话框，您可以使用该对话框来指定或查看连接的设置。
- 测试连接—在不关闭对话框的情况下测试与已附加数据库的连接。如果所选数据库的设置输入正确，将显示“测试连接成功”的消息。点击“OK”保存连接设置。请记住：如果您尝试对不存在的数据库进行测试，测试连接将失败。

在“选择或输入数据库名称”框中输入数据库名称 `SharpSampleDatabase` 并点击 `OK` 后

![](img/3ca47f8f6f5560f07650d3563e2f2c05_511_0.png)

**图 16.6** 服务器资源管理器窗口显示了新创建的数据库及其文件夹。经微软许可使用。

新创建的数据库 `CSharpSampleDatabase` 现在是空的。若要添加新数据库表，请右键点击服务器资源管理器中的“表”节点并选择“添加新表”。使用表格编辑器，您可以向新表添加以下列：

- **Code**—添加新表的以下列：在“选择或输入数据库名称”框中输入数据库名称 `SharpSampleDatabase` 并点击 `OK` 后，主键。
- **ProdName**—使用 `varchar(50)` 类型，存储产品名称。
- **Quantity**—使用 `int` 类型，存储数量。
- **Category**—使用 `varchar(30)` 类型，存储类别。
- **Price**—使用 `money` 类型，存储价格。

请忘记，当尝试对不存在的数据库进行测试时，测试连接将失败。

在定义了数据库的连接字符串后，新创建的表结构如图 16.7 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_511_0.png)

**图 16.7** 数据库结构。

服务器资源管理器窗口中显示了新创建的数据库及其文件夹。经微软许可使用。

## 从数据库访问数据

与本地计算机上的 `CSharpSampleDatabase` 建立连接：

```csharp
SqlConnection conn = new SqlConnection("Server=(local);Initial Catalog=CSharpSampleDatabase;");
```

此属性是可选的。换句话说，当你要连接到特定的计算机但不连接到任何数据库时，可以忽略它。

此属性实现了与数据库的安全性连接。
你可以为此属性指定值 `true`、`false`、`yes`、`no` 或 `SSPI`。
在建立受信任连接或不需要验证的连接时，你可以为此属性赋值 `true` 或 `SSPI`（安全支持提供程序接口），如下所示：

```csharp
```
