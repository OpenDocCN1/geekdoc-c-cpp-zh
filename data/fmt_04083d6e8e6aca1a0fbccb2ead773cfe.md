
前面的代码片段确保您连接的每条记录中的`CustomerID`字段都匹配。您还可以执行内部连接，其中记录必须同时存在于两个表中，或外部连接，其中记录可以存在于任一表中。

## DROP 语句

SQL 中的`DROP`语句从数据库中删除对象。您可以使用`DROP`语句删除表、用户甚至整个数据库。您可以按如下所示的 SQL 查询语句从数据库中删除`Customers`表：

## 理解 ADO.NET

ADO.NET 是 Visual C# 使用的数据访问和操作协议。它采用断开式数据架构，这意味着你所处理的数据只是实际数据库中数据的一份副本。微软选择断开式数据架构有多种原因。在传统的客户端/服务器应用程序中，你需要获取数据库连接并在应用程序运行期间保持该连接处于打开状态。然而，维持这些连接会占用大量服务器资源。此外，如果希望迁移到互联网环境，就必须维护断开的`DataSet`，而不是维持直接且持续的连接。

ADO.NET 提供了一组用于创建分布式应用程序的组件。它是 .NET Framework 中一个重要且不可或缺的组成部分。ADO.NET 提供对数据源的一致访问，例如 Microsoft SQL Server、对象链接和嵌入数据库（OLEDB）以及可扩展标记语言（XML）。此外，你可以使用 ADO.NET 来检索、操作和更新这些数据源中存在的数据。ADO.NET 包括用于连接数据库、执行命令和检索结果的数据提供程序。这些结果要么被直接处理，要么被放入 ADO.NET `DataSet`对象中以临时方式呈现给用户。ADO.NET 类位于 `System.Data.dll` 中，并与 `System.Xml.dll` 中的 XML 类集成在一起。ADO.NET 的一些重要功能如下：

- LINQ — 即语言集成查询（Language Integrated Query），它集成到 .NET 框架中数据访问的各个方面，包括 `DataSet`断开式编程模型和现有的 SQL Server 数据库架构。LINQ to ADO.NET 包含两种独立的技术：LINQ to DataSet 和 LINQ to SQL。LINQ to DataSet 提供对 `DataSet` 更出色的查询能力。LINQ to SQL 使你能够直接查询 SQL Server 数据库。
- LINQ to DataSet — 为存储在 `DataSet` 中的断开式数据提供 LINQ 功能。LINQ to DataSet 使得对 `DataSet` 对象中缓存的数据进行查询更简便、更快速。LINQ to DataSet 功能使你能够更高效地工作。
- LINQ to SQL — 提供将关系数据作为对象进行管理的运行时基础架构。你可以使用 ADO.NET 的 LINQ to SQL 功能，以访问内存中集合的相同方式，利用 LINQ 技术访问 SQL 数据库。LINQ to SQL 支持你在使用 SQL 时所期望的所有关键功能。你可以对表中的信息执行插入、更新和删除操作。

> 注意
> 你将在第 27 章“LINQ 查询”中更详细地了解 LINQ。

以下是最常见的 ADO.NET 对象列表：

- `Connection` 对象 — 提供与数据源的连接，借助 `OleDbConnection`、`OdbcConnection`、`OracleConnection` 或 `SqlConnection` 对象来读写数据。
- `DataAdapter` 对象 — 提供数据源与 `DataSet` 之间的通信。通常，你使用 SQL 来配置 `DataAdapter`，使其对数据源执行操作。可用的 `DataAdapter` 包括 `OleDbDataAdapter`、`OdbcDataAdapter`、`OracleDataAdapter`、`AccessDataAdapter` 和 `SqlDataAdapter` 对象。
- `Command` 对象 — 允许 `DataAdapter` 读取、添加、更新和删除数据源中的记录。`DataAdapter` 支持四个属性，使你能够访问这些命令对象——`SelectCommand`、`InsertCommand`、`UpdateCommand` 和 `DeleteCommand`。
- `DataSet` 对象 — 将数据存储在断开式缓存中。`DataSet` 的结构类似于关系数据库；它使你能够访问表、行和列的对象模型；并且包含为表定义的约束和关系。`DataSet` 由 `DataSet` 对象提供支持。
- `DataTable` 对象 — 保存来自数据源的数据表。数据表包含两个重要属性——`Columns`，即表示表中数据列的 `DataColumn` 对象的集合；以及 `Rows`，即表示表中数据行的 `DataRow` 对象的集合。
- `DataReader` 对象 — 保存来自数据库的只读、只进（只能从一条记录移动到下一条记录，不能向后移动）的数据集。使用数据读取器可以提高速度，因为内存中一次只保留一行数据。
- `DataView` 对象 — 表示单个表的自定义视图，可以对该视图进行筛选、搜索或排序。换句话说，数据视图（由 `DataView` 类支持）是一种占用极少资源的数据库快照。
- `Constraint` 对象 — 借助 `DataSet` 检查数据完整性。约束（由 `Constraint` 类支持）是一种规则，可以在插入、更新或删除行时使用，以检查操作后所受影响的表。约束有三种类型：唯一约束，检查列中的新值在整个表中是否唯一；外键约束，指定当另一个表中的记录被更新时，相关记录应如何更新；以及主键约束，其工作方式与唯一约束类似。唯一约束与主键约束之间的区别在于，唯一约束允许空值；而主键约束不允许空值。此外，唯一约束可以应用于表中的多个列；而主键约束只能应用于一个列。
- `DataRelation` 对象 — 基于两个表共享的键，指定父表和子表之间的关系。
- `DataRow` 对象 — 对应于数据表中的特定行。你可以使用 `Item` 属性获取或设置该行中特定字段的值。
- `DataColumn` 对象 — 对应于表中的列。每个对象都有一个 `DataType` 属性，用于指定每列包含的数据种类，例如整数或字符串值。

## 描述 ADO.NET 的架构

ADO.NET 由两个基本组件组成：`DataSet`（与数据源断开连接，不需要知道数据从何处检索）和 .NET 数据提供程序（允许你连接到数据源并对其执行 SQL 命令）。`DataSet` 旨在实现独立于任何数据源的数据访问。它可以用相同的方式操作来自传统数据源或 XML 文档的数据。数据提供程序则是为数据操作和只读数据访问而设计的。ADO.NET 的架构如图 24.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1175_0.png)

图 24.1：展示 ADO.NET 架构

如图 24.1 所示，数据提供程序包含 `Connection`、`Command`、`DataReader` 和 `DataAdapter` 对象。`Connection` 对象提供与数据源的连接。`Command` 对象允许访问数据库命令，例如返回数据、修改数据和发送数据。`DataReader` 对象提供来自数据源的高性能数据流。`DataAdapter` 对象使用 `Command` 对象来执行 SQL 命令。`DataAdapter` 对象用数据填充 `DataSet`，并且还将对 `DataSet` 中数据所做的更改解析回数据源。你将在下一节中更详细地了解数据提供程序和 `DataSet`。

## ADO.NET 中的数据提供程序

数据提供程序是一组相互关联的组件，它们协同工作，以高效的方式提供数据。它在 ADO.NET 中用于连接数据库、执行命令和检索结果。结果要么被直接处理，要么在各层之间进行处理，并在与多个来源合并后显示。数据提供程序在不影响功能的前提下提高了性能。

### 数据提供程序的对象

ADO.NET 中的数据提供程序由以下四个对象组成：

- `Connection` — 创建与数据源的连接。所有 `Connection` 对象的基类是 `DbConnection` 类。`Connection` 对象具有用于打开和关闭连接以及开始事务的方法。此外，它们还具有用于设置连接超时时间段的属性。.NET 框架提供了两种类型的 `Connection` 类：`SqlConnection` 对象，专门用于连接 Microsoft SQL Server；以及 `OleDbConnection` 对象，旨在提供对各种数据库（如 Microsoft Access 和 Oracle）的连接。

- `Command` — 对数据源执行命令并检索 `DataReader` 或 `DataSet`。它还针对数据源执行 `INSERT`、`UPDATE` 或 `DELETE` 命令。所有 `Command` 对象的基类是 `DbCommand` 类。`Command` 对象由两个类表示：`SqlCommand` 和 `OleDbCommand`。`Command` 对象提供了三种用于在数据库上执行命令的方法。`ExecuteNonQuery()` 方法用于执行没有返回值的命令，例如 `INSERT`、`UPDATE` 或 `DELETE`。`ExecuteScalar()` 方法从数据库查询中返回单个值。`ExecuteReader()` 方法通过 `DataReader` 对象返回结果集。

- `DataReader` — 提供只进和只读的连接型结果集。所有 `DataReader` 对象的基类是 `DataReader` 类。`DataReader` 对象不能直接实例化。

- `DataAdapter` — 使用数据源中的数据更新 `DataSet`。所有 `DataAdapter` 对象的基类是 `DbDataAdapter` 类。`DataAdapter` 充当数据库与 `DataSet` 之间所有通信的中介。`DataAdapter` 使用 `Fill()` 方法将数据库中的数据填充到 `DataTable` 或 `DataSet` 中。`DataAdapter` 通过调用 `Update()` 方法将更改提交到数据库。`DataAdapter` 提供了四个表示数据库命令的属性：`SelectCommand`、`InsertCommand`、`DeleteCommand` 和 `UpdateCommand`。

### ADO.NET 中的数据提供程序类型

ADO.NET 中包含的不同类型的数据提供程序如下：

- .NET Framework Data Provider for SQL Server — 提供对 Microsoft SQL Server 的访问。它使用 `System.Data.SqlClient` 命名空间及其自己的协议与 SQL Server 通信。在访问 SQL Server 时，它表现出良好的性能。无需添加 OLE DB 或 ODBC（开放数据库连接）层即可访问该数据提供程序。当你能够访问 SQL Server 7.0 或更高版本时，可以使用 .NET Framework Data Provider for SQL Server。

- .NET Framework Data Provider for OLE DB — 提供对通过 OLE DB 公开的数据源的访问。它使用 `System.Data.OleDb` 命名空间，并支持本地和分布式事务。

- .NET Framework Data Provider for ODBC — 提供对通过 ODBC 公开的数据源的访问。它使用 `System.Data.Odbc` 命名空间，并支持本地和分布式事务。

- .NET Framework Data Provider for Oracle — 通过 Oracle 客户端连接软件提供对 Oracle 数据源的访问。它使用 `System.Data.OracleClient` 命名空间，并且包含在 `System.Data.OracleClient.dll` 程序集中。当你编译使用 .NET Framework Oracle 数据提供程序的应用程序时，必须同时引用 `System.Data.dll` 和 `System.Data.OracleClient.dll`。它支持本地和分布式事务。

## DataSet

`DataSet` 是一种非常有用的内存中数据的表示形式，是各种基于数据的应用程序的核心。`DataSet` 可以被视为数据库相关部分的本地副本。`DataSet` 中的数据可以独立于数据库进行操作和更新。你可以从任何有效源加载 `DataSet` 中的数据，例如 Microsoft SQLServer 数据库、Oracle 数据库或 Microsoft Access 数据库。

### Components of DataSets

构成 `DataSet` 的各种组件如下所示：

- `DataTable` — 由 `DataRow` 和 `DataColumn` 组成，并以表格行格式存储数据。`DataTable` 是 ADO.NET 库的核心对象，与数据库中的表类似。你应该注意 `DataTable` 对象是区分大小写的。例如，`EmployeeDetails` 表与 `employeedetails` 表不同。一个 `DataSet` 可以包含两个具有相同 `TableName` 属性但 `Namespace` 属性值不同的 `DataTable` 对象。`NewRow()` 方法用于向 `DataTable` 添加一行。`DataTable` 可以包含的最大行数固定为 16,777,216。`DataTable` 还包含一个 `Constraint` 对象集合，用于确保数据的完整性。

- `DataView` — 代表 `DataTable` 的自定义视图，用于排序、过滤、搜索、编辑和导航。`DataView` 允许你基于 `RowStateFilter` 属性中指定的预设条件在 `DataTable` 上创建一个视图，以查看数据的子集。`DataView` 可用于从 `DataTable` 中呈现数据的子集。

- `DataColumn` — 由构成 `DataTable` 的多列组成。`DataColumn` 是 `DataTable` 的基本构建块。`DataColumn` 的 `DataType` 属性决定列保存的数据类型。你还可以将控件绑定到 `DataTable` 中的特定列。

- `DataRow` — 代表 `DataTable` 中的一行。你可以使用 `DataRow` 对象及其属性和方法来检索、评估、插入、删除和更新 `DataTable` 中的值。你可以使用 `DataTable` 的 `NewRow()` 方法创建新的 `DataRow`，并使用 `Add()` 方法将新的 `DataRow` 添加到 `DataTable`。你也可以通过调用 `Remove()` 方法删除 `DataRow`。

- `DataRelation` — 允许你指定各种表之间的关系。简单来说，`DataRelation` 用于通过 `DataColumn` 对象将两个 `DataTable` 对象相互关联。关系是在父表和子表中匹配的列之间创建的。为此，两个列的 `DataType` 值必须相同。`DataRelation` 对象包含在 `DataRelationCollection` 中，你可以通过 `DataSet` 的 `Relations` 属性访问它。

### Typed Vs. Untyped DataSets

`DataSet` 可以分为两种类型：Typed 或 Untyped。两者的区别在于 Typed DataSet 具有模式，而 Untyped DataSet 没有。Typed DataSet 是从基 `DataSet` 类派生的。它使用来自 DataSet 设计器中的信息，例如表、列和属性，该信息存储在 XML Schema（`.xsd`）文件中，以生成新的数据集类。这些信息被生成并编译为一组主类对象和属性到这个新的数据集类中。Typed DataSet 假设 `DataSet` 类的所有功能，并且可以与将 `DataSet` 类的实例作为参数的方法一起使用。

Untyped DataSet 没有像 Typed DataSet 那样的内置模式。Untyped DataSet 包含与 Typed DataSet 相同的表和列，但仅作为集合访问。

## DataReader

在 ADO.NET 中，`DataReader` 用于顺序读取来自数据源的数据。`DataReader` 允许在给定时间访问单行数据，具有单个记录加载在内存中，而不管结果集的大小。需要 `Command` 对象才能使用 `DataReader` 从数据库检索数据。创建 `Command` 对象后，通过调用 `Command.ExecuteReader` 创建 `DataReader` 以从数据源检索行。你应该使用 `DataReader` 对象的 `Read()` 方法从查询结果中获取一行。当你检索大量数据时，`DataReader` 是一个不错的选择，因为数据不会存储在缓存内存中。每次使用完 `DataReader` 对象后调用 `Close()` 方法。这是必要的，因为如果你的 `Command` 包含返回值，它们在你关闭 `DataReader` 对象之前将不可用。

可能会在你脑中产生一个问题是，如果 `DataReader` 和 `DataSet` 都用于检索数据，那么两者之间有什么区别？答案在于两者的功能。当你决定应用程序应使用 `DataReader` 还是 `DataSet` 时，你应该考虑应用程序所需的类型功能。你可以在以下情况下使用 `DataSet`：

- 使用 `DataSet` 操作数据。
- 使用 `DataSet` 在层之间远程传输数据。
- 使用 `DataSet` 动态交互数据。通过交互意味着将数据绑定到 Window Form 或从多个源组合数据。
- 使用 `DataSet` 执行大量处理而无需保持与数据源的打开连接。
- 使用 `DataReader` 以仅向前和只读的方式返回数据。

## ADO.NET Entity Framework

ADO.NET 的 Entity Framework 允许你通过对象模型而不是关系模型关注数据。Entity Framework 允许你编写更少的数据访问代码、减少维护、使数据结构对用户友好并促进数据的持久化。你可以直接使用名为 `EntityClient` 的新数据提供程序和名为 Entity SQL 的新语言在应用程序中使用 Entity Framework。`EntityClient` 使用 `EntityConnection` 和 `EntityCommand` 对象返回一个 `DbDataReader`。你也可以通过使用 Entity SQL 的 `ObjectQuery` 对象或 LINQ to Entities 来使用 Object Services。你可以在图 24.2 中看到 ADO.NET Entity Framework 的架构：

![](img/e073a4882197be4ab61103cbe0bcb394_1178_0.png)

图 24.2：显示 Entity Framework 的架构

Entity Framework 包括以下组件：

- Entity Data Model (EDM) – 定义可以使用 `DataReader` 以序列化形式读取的概念实体。
- **Entity SQL** – 定义一种通用的基于 SQL 的查询语言，该语言扩展以根据 EDM 概念表达查询。它同时得到 `EntityClient` 和 Object Services 的支持。
- `EntityClient` – 为实体级查询提供网关，该查询通过通用的 Entity SQL 语言进行查询。
- **Object Services** – 允许你通过一组 CLR 类与概念层交互。Object Services 还通过提供诸如状态管理、标识解析和查询构建支持等服务来支持 Entity Framework。
- **LINQ to Entities** – 为查询实体提供 LINQ 支持。

## Immediate Solutions

### Creating Connection Strings

与以前版本类似，.NET Framework 4.0 提供了处理连接字符串的功能。连接字符串包含作为参数从数据提供程序传递到数据源的初始化信息。每个在 .NET 中可用的数据提供程序的连接字符串都不同。连接字符串在尝试打开连接时被解析。`DbConnectionStringBuilder` 是创建连接字符串的基类。它可用于创建、编辑、读取和保存连接字符串到配置文件。不同类型的数据源有不同的连接字符串。你可以在表 24.1 中找到创建连接字符串的所有可用提供程序列表：

**Table 24.1: Data Providers in .NET**

| Provider | Description |
|----------|-------------|
| SQL Server Data Provider (`System.Data.SqlClient`) | 为 Microsoft SQL Server 7.0 或更高版本提供数据访问 |
| OLE DB Data Provider (`System.Data.OleDb`) | 为使用 OLE DB 的数据源提供数据访问 |
| ODBC Data Provider (`System.Data.Odbc`) | 为使用 ODBC 的数据源提供数据访问 |
| Oracle Data Provider (`System.Data.OracleClient`) | 为 Oracle 8.1.7 或更高版本提供数据访问 |
| EntityClient Provider (`System.Data.EntityClient`) | 为 Entity Data Model (EDM) 应用程序提供数据访问 |

你可以在 Visual Studio 2010 中为任何数据提供程序创建连接字符串。让我们通过执行以下步骤为 Microsoft SQL Server 创建连接字符串：

1. 打开 Visual Studio 2010 IDE 的 Server Explorer。
2. 右键单击 Data Connections 并选择 Add Connection，如图 24.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1180_0.png)

**Figure 24.3: Selecting the Add Connection Option**

Add Connection 对话框打开（见图 24.4），你可以在其中选择要连接到应用程序的数据源类型。

> NOTE
> 当你第一次创建连接时，首先会出现 Change Data Source 对话框。

3. 单击 Change 按钮，如图 24.4 所示：

**图 24.4：选择数据源**

![](img/e073a4882197be4ab61103cbe0bcb394_1181_0.png)

单击 Change 按钮后，会出现 Change Data Source 对话框，让您可以为应用程序选择数据源（图 24.5）。

4. 从 Change Data Source 对话框中显示的列表中选择一个数据源。在我们的例子中，我们选择了 Microsoft SQL Server 作为数据源，如图 24.5 所示。

**图 24.5：更改数据源**

![](img/e073a4882197be4ab61103cbe0bcb394_1181_1.png)

5. 单击 OK 按钮（图 24.5）。单击 OK 按钮后，您将返回到 Add Connection 对话框，其中选项有所不同（图 24.6）。

6. 在 Server name 组合框中输入或选择您的 SQL Server 的服务器名称。在我们的例子中，我们输入了 UMAR-PC（图 24.6）。

7. 在 Log on to the server 组中选择 Use Windows Authentication 单选按钮（图 24.6）。

8. 在 Connect to a database 组中 Select or enter a database name 下拉列表中输入数据库名称。在我们的例子中，我们输入了 Northwind 数据库（图 24.6）。

9. 单击 Test Connection 按钮。会出现一个消息框，显示消息 Test Connection succeeded，如图 24.6 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1182_0.png)

图 24.6：测试连接

10. 单击消息框的 OK 按钮（图 24.6）。
11. 单击 Add Connection 对话框的 OK 按钮（图 24.6）。

您会注意到数据源已添加到 Server Explorer 中的应用程序中，如图 24.7 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1182_1.png)

图 24.7：在 Server Explorer 中显示添加的连接

12. 在 Server Explorer 中选择数据源并按 F4 以在 Properties 窗口中查看数据源的属性，如图 24.8 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1183_0.png)

**图 24.8：连接字符串的属性**

您可以在属性窗口中找到有关连接字符串的完整详细信息。`Name` 是您与应用程序关联的数据库的名称。`Case Sensitive` 属性表示连接字符串是否区分大小写。在本例中，`Case Sensitive` 的值为 `False`。`Connection String` 属性指定数据源的连接字符串的完整路径。`Owner` 属性指定您当前正在工作的系统的管理员名称。属性窗口还指定了该特定连接字符串的 `Provider`，在本例中为 .NET Framework Data Provider for SQL Server。`State` 指定连接是 `Open` 还是 `Close`。`Type` 属性指定您使用的数据源的类型，在本例中为 Microsoft SQL Server。

连接字符串的语法取决于数据提供程序。语法错误会导致运行时异常。在验证连接字符串的语法后，数据源会打开连接。您可以使用 `OleDbConnection` 类的 `ConnectionString` 属性获取或设置 OLE DB 数据源（如 Microsoft Access）的连接字符串。对于 SQL Server，您可以使用 `SqlConnection` 类的 `ConnectionString` 属性设置连接字符串。`OracleConnection` 的 `ConnectionString` 属性允许您获取或设置 ORACLE 数据源的连接字符串。连接字符串的基本语法包括一系列由分号分隔的关键字。等号连接每个关键字及其值。值必须用双引号括起来。每个数据源的连接字符串的语法都不同。您可以通过向导创建连接字符串，如本章所示。在某些情况下，您可以通过代码隐藏文件创建连接字符串。为此，您应该了解每个数据源的连接字符串的语法。让我们看看每个数据源的不同连接字符串的语法。

对于 Microsoft SQL Server 数据源，您需要传递以下连接字符串：
