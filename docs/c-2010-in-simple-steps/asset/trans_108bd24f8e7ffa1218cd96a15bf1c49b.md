
表 8.1：ADO.NET 数据提供程序的类型

| 数据提供程序 | 描述 |
|---|---|
| .NET Framework Data Provider for Oracle | 提供对 Oracle 数据库 8.1.7 及更高版本的访问。它使用 System.Data.OracleClient 命名空间。 |

数据提供程序包含以下四个主要对象：

- **Connection**：与数据库建立连接。所有 Connection 对象的基类是 DbConnection 类。Connection 对象具有打开和关闭连接的方法。.NET Framework 提供两种 Connection 对象：SqlConnection 对象，专门用于连接 Microsoft SQL Server；OleDbConnection 对象，用于为各种数据库（如 Microsoft Access 和 Oracle）提供连接。Connection 对象的一些常用方法是 Open() 和 Close() 方法。Open() 方法用于打开与数据库的连接，Close() 方法用于关闭连接。
- **Command**：对数据库执行命令并检索 DataReader 或 DataSet 对象。它还针对数据库执行 INSERT、UPDATE 或 DELETE 命令。所有 Command 对象的基类是 DbCommand 类。Command 对象由两个类表示：SqlCommand 和 OleDbCommand。Command 对象提供三种在数据库上执行命令的方法：ExecuteNonQuery()、ExecuteScalar() 和 ExecuteReader()。ExecuteNonQuery() 方法执行没有返回值的命令，如 INSERT、UPDATE 或 DELETE。ExecuteScalar() 方法从数据库查询返回单个值。ExecuteReader() 方法将结果集作为 DataReader 对象返回。
- **DataReader**：以只进只读模式从数据库检索数据。所有 DataReader 对象的基类是 DbDataReader 类。当调用 Command 对象的 ExecuteReader() 方法时，返回 DataReader 对象。
- **DataAdapter**：从数据库检索数据，并将该数据存储在 DataSet 对象中，同时将 DataSet 对象中所做的更改反映到数据库。所有 DataAdapter 对象的基类是 DbDataAdapter 类。DataAdapter 对象充当数据库与 DataSet 对象之间所有通信的中介。DataAdapter 对象用于通过 Fill() 方法使用数据库中的数据填充 DataTable 或 DataSet 对象。DataAdapter 对象通过调用 Update() 方法将更改提交到数据库。DataAdapter 对象提供四个表示数据库命令的属性：SelectCommand、InsertCommand、DeleteCommand 和 UpdateCommand。

## 数据集

ADO.NET 的另一个主要组件是 DataSet 对象。此对象始终与数据库保持断开连接，从而减少数据库的负载。DataSet 对象用于将 DataSet 对象连接到数据提供程序。DataAdapter 对象用作 DataSet 对象与数据提供程序之间的中介。由于 DataSet 对象维护数据库中数据的缓存副本，因此可以独立于数据库操作和更新 DataSet 对象中的数据。表 8.2 列出了构成 DataSet 对象的各种组件：

表 8.2：DataSet 对象的组件

| 组件 | 描述 |
|---|---|
| DataRelationCollection | 包含 DataSet 对象的 DataRelation 对象集合。DataRelation 类用于表示数据库中表之间的父/子关系。 |
| ExtendedProperties | 包含自定义信息，例如用于检索数据的 SQL 语句或从数据库检索数据的时间 |
| DataTableCollection | 包含从数据库检索到的所有表 |
| DataTable | 表示 **DataSet** 对象的 **DataTableCollection** 对象中的表 |
| DataRelation | 表示 **DataSet** 对象的 **DataRelationCollection** 对象中的关系 |
| DataRowCollection | 包含 **DataTable** 对象中的所有行 |
| DataView | 表示 **DataTable** 对象的固定自定义视图 |
| PrimaryKey | 表示在 **DataTable** 对象中唯一标识某一行的列 |
| DataColumnCollection | 包含 **DataTable** 对象中的所有列 |

现在，您已经了解了 **DataSet** 对象的一些重要组件，我们来讨论使用 ADO.NET 可以对数据库执行的基本操作。

## ADO.NET 中的基本操作

使用 ADO.NET，您可以以一致的方式访问、处理和更新数据库中的数据。在以下部分中，您将学习利用 ADO.NET 的不同组件来连接数据库、创建命令、创建 **DataSet** 对象、使用数据适配器检索数据集中的数据、使用数据集更新数据库，最后使用数据读取器。

### 创建与数据库的连接

要处理数据库中的数据，首先需要与数据库建立连接。要创建与数据库的新连接，可以利用 **添加连接** 对话框，或在代码隐藏文件中指定连接字符串。我们先学习如何使用 **添加连接** 对话框连接到数据库。

### 使用“添加连接”对话框

您可以使用 **添加连接** 对话框为任何数据提供程序创建连接字符串。在本例中，我们向您展示如何连接到 **NORTHWND** 数据库。让我们在名为 **DatabaseOperationsExample** 的 Windows 窗体应用程序中，使用 **添加连接** 对话框为 Microsoft SQL Server 创建连接字符串。为此，请执行以下步骤：

- 1. **单击** **开始➤所有程序➤Microsoft Visual Studio 2010➤ Microsoft Visual Studio 2010** 以打开 Microsoft Visual Studio 2010。
- 2. **选择**菜单栏中的 **文件➤新建➤项目**。将出现 **新建项目** 对话框。
- 3. **选择** **已安装的模板** 窗格下的 **Visual C#**，并从 **新建项目** 对话框的中间窗格中选择 **Windows 窗体应用程序**。
- 4. **输入**应用程序的名称 **DatabaseOperationsExample**，并在 **位置** 组合框中指定应用程序的位置。
- 5. **单击** **确定** 按钮创建 **DatabaseOperationsExample** 应用程序。
- 6. **选择**菜单栏中的 **视图➤服务器资源管理器**，打开 **服务器资源管理器** 窗口，如图 C-8.2 所示。

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_266_0.png)

**图 C-8.2**

服务器资源管理器窗口出现（图 C-8.3）。

- 7. 在服务器资源管理器窗口中右键单击“数据连接”选项，然后从上下文菜单中选择“添加连接”选项，如图 C-8.3 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_267_0.png)

图 C-8.3

出现“添加连接”对话框，您可以在其中选择要附加到应用程序的数据源类型。

- 8. 单击“更改”按钮，为应用程序选择数据源。

出现“更改数据源”对话框，您可以在其中选择数据源（图 C-8.4）。

- 9. 选择 Microsoft SQL Server 作为数据源，以连接到 SQL Server 数据库（图 C-8.4）。

- 10. 单击“确定”按钮，如图 C-8.4 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_267_1.png)

图 C-8.4

“添加连接”对话框再次出现，并已选择 Microsoft SQL Server (SqlClient) 选项作为数据源（图 C-8.5）。

- 11. 从“服务器名”下拉列表中选择服务器名，如图 C-8.5 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_268_0.png)

图 C-8.5

默认情况下，选中“使用 Windows 身份验证”单选按钮（图 C-8.6）。如果要使用 SQL Server 身份验证，则选择“使用 SQL Server 身份验证”单选按钮，并提供用于身份验证的用户名和密码。在本例中，我们使用 Windows 身份验证连接到服务器。

- 12. 在“选择或输入数据库名称”下拉列表中选择数据库，或输入要连接的数据库的名称（图 C-8.6）。
- 13. 单击“测试连接”按钮。将出现一个消息框，其中显示消息“测试连接成功”（图 C-8.6）。
- 14. 单击消息框中的“确定”按钮以关闭消息框，如图 C-8.6 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_268_1.png)

图 C-8.6
