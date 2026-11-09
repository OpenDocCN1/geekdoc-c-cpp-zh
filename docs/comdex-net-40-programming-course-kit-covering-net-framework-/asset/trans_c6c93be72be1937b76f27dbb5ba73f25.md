
- **自跟踪实体：** 指在与 n 层应用程序一起工作时能够跟踪自身更改的实体。这些更改会保存到数据库。.NET Framework 4.0 引入了 T4 模板来生成自跟踪实体。
- **模型优先开发：** 允许你创建自己的 EDM，然后基于该 EDM 生成 Transact-SQL (T-SQL) 和自定义代码（关系模型）数据库，并带有匹配的表和关系。
- **内置函数：** 使你能够直接在查询中使用内置的 SQL Server 函数，例如日期和时间函数。
- **更好的 N 层支持：** 支持应用程序编程接口 (API) 和模板，以便借助 Entity Framework 更轻松地开发 n 层应用程序。

## ADO.NET 的组件

ADO.NET 包含一组公开数据访问服务的类。它还提供丰富的组件来创建分布式应用程序。ADO.NET 采用逻辑流程来访问数据库中的数据，如图 C#-4.1 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_366_0.png)

图 C#-4.1

如图 C#-4.1 所示，ADO.NET 中用于访问和操作数据的两个主要组件是数据提供程序和 **DataSet** 对象。数据提供程序包含 **Connection**、**Command**、**DataReader** 和 **DataAdapter** 对象。

现在，让我们详细了解数据提供程序和数据集。

### 数据提供程序

数据提供程序用于与数据库建立连接、从数据库检索数据、将数据存储在数据集中、读取数据，最后更新数据库。数据提供程序可在不影响功能的情况下提高应用程序性能。

表 4.1 列出了 ADO.NET 中包含的不同类型的数据提供程序：

| 数据提供程序 | 描述 |
|---|---|
| 用于 SQL Server 的 .NET Framework 数据提供程序 | 通过使用 **System.Data.SqlClient** 命名空间提供对 Microsoft SQL Server 7.0 或更高版本的访问。 |
| 用于 OLE DB 的 .NET Framework 数据提供程序 | 通过使用 **System.Data.OleDb** 命名空间提供对向 OLE DB 公开的数据库的访问。 |
| 用于 ODBC 的 .NET Framework 数据提供程序 | 通过使用 **System.Data.Odbc** 命名空间提供对向 ODBC 公开的数据库的访问。 |
| 用于 Oracle 的 .NET Framework 数据提供程序 | 通过使用 **System.Data.OracleClient** 命名空间提供对 Oracle Database 8.1.7 或更高版本的访问。 |

数据提供程序主要包含以下四个对象：

- **Connection：** 与数据库建立连接。所有 **Connection** 对象的基类是 **DbConnection** 类。Connection 对象包含打开和关闭连接的方法。

  .NET Framework 提供两种类型的 Connection 对象：**SqlConnection** 对象，专门用于连接 Microsoft SQL Server；以及 **OleDbConnection** 对象，用于提供与各种数据库（例如 Microsoft Access 和 Oracle）的连接。**Connection** 对象的一些常用方法是 **Open()** 和 **Close()** 方法。**Open()** 方法用于打开与数据库的连接，**Close()** 方法用于关闭连接。
- **Command：** 对数据库执行命令，并检索 **DataReader** 或 **DataSet** 对象。它还会对数据库执行 **INSERT**、**UPDATE** 或 **DELETE** 命令。所有 **Command** 对象的基类是 **DbCommand** 类。**Command** 对象由两个类表示：**SqlCommand** 和 **OleDbCommand**。它提供三个方法：**ExecuteNonQuery()**、**ExecuteScalar()** 和 **ExecuteReader()**，用于在数据库上执行命令。**ExecuteNonQuery()** 方法执行没有返回值的命令，例如 **INSERT**、**UPDATE** 或 **DELETE** 命令。**ExecuteScalar()** 方法从数据库查询中返回单个值。**ExecuteReader()** 方法以 **DataReader** 对象的形式返回结果集。
- **DataReader：** 以只进、只读模式从数据库检索数据。所有 **DataReader** 对象的基类是 **DbDataReader** 类。**DataReader** 对象是调用 **Command** 对象的 **ExecuteReader()** 方法后返回的结果。
- **DataAdapter：** 从数据库检索数据，将数据存储在数据集中，并将数据集中所做的更改反映到数据库。所有 **DataAdapter** 对象的基类是 **DbDataAdapter** 类。**DataAdapter** 对象充当数据库与 **DataSet** 对象之间所有通信的中介。**DataAdapter** 对象的 **Fill** 方法用于使用数据库中的数据填充 **DataTable** 或 **DataSet** 对象。**DataAdapter** 对象通过调用 **Update()** 方法将更改提交到数据库。它提供四个属性，分别表示四个数据库命令：**SelectCommand**、**InsertCommand**、**DeleteCommand** 和 **UpdateCommand**。

### 数据集

ADO.NET 的另一个主要组件是 **DataSet** 对象。此对象与数据库保持断开连接；因此，这减轻了数据库的负载。由于数据集维护着数据库数据的缓存副本，因此数据集中的数据可以独立于数据库进行操纵和更新。

表 4.2 列出了构成 **DataSet** 对象的各个组件：

**表 4.2：DataSet 对象的组件**

| 组件 | 描述 |
|---|---|
| DataTableCollection | 包含从数据库检索到的所有表 |
| DataTable | 表示数据集 **DataTableCollection** 对象中的表 |
| DataRowCollection | 包含 **DataTable** 对象中存在的所有行 |
| DataColumnCollection | 包含 **DataTable** 对象中存在的所有列 |
| ConstraintCollection | 包含 **DataTable** 的约束集合 |
| DataRelationCollection | 包含数据集中各表之间的关系和链接 |

现在，让我们了解如何在 ADO.NET 中访问数据。

## 在 ADO.NET 中访问数据

使用 ADO.NET，你可以以一致的方式对数据库执行各种操作，例如访问、处理和更新数据库中的数据。要执行这些操作中的任何一种，你需要先与数据库建立连接。在接下来的几节中，你将学习如何利用 ADO.NET 的不同组件连接到数据库、使用数据库对象、配置数据适配器、创建数据集，以及使用数据适配器从数据集检索数据。

### 建立与数据库的连接

要处理数据库中的数据，你需要先建立到数据库的连接。你可以通过以下任意方式创建新连接：

- “添加连接”向导
- 代码编辑器中的连接字符串

首先，我们来看如何使用“添加连接”向导建立到数据库的连接。

### 使用“添加连接”向导建立连接

你可以使用“添加连接”向导为任何数据提供程序创建连接字符串。在本例中，我们将建立与 Northwind 数据库的连接。

执行以下步骤，使用“添加连接”向导为 Microsoft SQL Server 创建连接字符串：

1. 打开 Microsoft Visual Studio 2010。
2. 在菜单栏上单击“视图”→“服务器资源管理器”，以打开“服务器资源管理器”（图 C#-4.2）。  
   “服务器资源管理器”会出现（图 C#-4.3）。

   ![](img/9862a98a1a2d3bb14334137965a1ec60_368_0.png)

   ![](img/9862a98a1a2d3bb14334137965a1ec60_368_1.png)

3. 在“服务器资源管理器”中右键单击“数据连接”选项。将出现一个上下文菜单（图 C#-4.3）。
4. 从上下文菜单中选择“添加连接”选项（图 C#-4.3）。  
   将出现“添加连接”对话框，你可以在其中选择要附加到应用程序的数据源类型（图 C#-4.4）。
5. 在“添加连接”对话框中单击“更改”按钮，如图 C#-4.4 所示：

   ![](img/9862a98a1a2d3bb14334137965a1ec60_368_2.png)
