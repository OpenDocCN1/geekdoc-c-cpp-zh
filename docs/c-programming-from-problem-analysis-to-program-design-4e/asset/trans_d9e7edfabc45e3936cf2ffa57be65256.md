
正如 MSDN 文档所述，从 `DBConnection` 类继承的类（例如 `OleDbConnection`）必须重写并为 `Close( )`、`BeginDbTransaction( )`、`ChangeDatabase( )`、`CreateDbCommand( )` 和 `OpenStateChange( )` 方法提供实现细节。必须为 `ConnectionString`、`Database`、`DataSource`、`ServerVersion` 和 `State` 定义属性。这确保所有数据提供程序连接对象都具有相似的功能，同时也可以进行优化，以便与其特定的 DBMS 交互。

除了表 14-2 中所示的特定数据提供程序命名空间之外，与 ADO.NET 类一起用于访问数据库的其他命名空间还包括：

- `System.Data.Common`——这些类由所有数据提供程序共享。
- `System.Data`——这些类表示 ADO.NET 体系结构，它使你能够构建使用来自多个数据源的数据的组件。

本章后续各节将使用每个核心类来检索和更新数据。最初的示例演示如何使用来自 Access 数据库的数据。后面的各节演示如何检索存储在 SQL Server 数据库中的数据。

## 连接到数据库

要访问使用 Microsoft Access 创建的数据库，请使用 `System.Data.OleDb` 命名空间中的类。为了避免对其命名空间中的类引用进行完全限定，需要使用以下 using 指令：

```csharp
using System.Data.OleDb;
```

连接对象是根据你使用的数据库类型或数据库提供程序类型来实例化的。.NET 在 `System.Data.OleDb` 命名空间中包含用于连接的 `OleDbConnection` 类。它表示到数据库的打开连接。要实例化此类的对象，需要指定一个连接字符串，其中包含实际的数据库提供程序和数据源。数据源是数据库的名称。你可以将数据库的完整路径作为字符串参数的一部分包含在内，也可以将数据库放在项目的 `bin\Debug` 子目录中。

> **注意**
>
> 当将完整路径指定为字符串的一部分时，逐字字符串很有用（逐字字符串使用 `@` 字符）。这消除了在路径中使用由两个反斜杠字符组成的转义字符序列（`\\`）的要求。

示例 14-1 使用针对 OleDb 数据提供程序的连接字符串实例化对象。`member.accdb` 数据库存储在项目的 `bin\Debug` 子目录中。在实例化 `OleDbConnection` 类的对象之后，使用 `OleDbConnection` 类的 `Open( )` 方法打开连接。

### 示例 14.1

```csharp
string sConnection;
sConnection = "Provider=Microsoft.ACE.OLEDB.12.0;" +
              "Data Source=member.accdb";

OleDbConnection dbConn;
dbConn = new OleDbConnection(sConnection);
dbConn.Open();
```

连接字符串特定于供应商。连接字符串的语法以提供程序或数据源名称开头，例如 "Provider=someValue"。在本书出版时，较新版本的 Access 对应的值为 "Microsoft.ACE.OLEDB.12.0"。如果你使用的是较旧版本的 Access，则数据提供程序会有所不同。

示例 14-2 演示如何实例化 SqlConnection 对象。连接字符串表明 Data Source 使用的是 Microsoft SQL Server Express 的本地副本。数据库名称为 RealEstateDb.mdf。连接字符串中的 IntegratedSecurity 属性设置为 true，表示使用当前 Windows 帐户凭据进行身份验证，而不是在连接字符串中指定用户 ID 和密码。

### 示例 14.2

```csharp
string sConnection = "Data Source=(localdb)\\v11.0;
    IntegratedSecurity=true;AttachDbFileName=RealEstateDb.mdf";
SqlConnection dbConn;
dbConn = new SqlConnection(sConnection);
dbConn.Open();
```

有时更具挑战性的部分是确定连接字符串中应包含什么。在撰写本书时，www.connectionstrings.com 列出了许多针对不同供应商的连接字符串。另一个网站 www.carlprothman.net/Default.aspx?tabid=81 也列出了连接字符串。如果你在这两个网站中的任何一个都没有找到所需的具体连接字符串，你可以使用你喜欢的搜索引擎，对 .NET、“connection string”和数据库供应商名称进行关键字搜索。另一种选择是使用某个 ConnectionStringBuilder 类来创建连接字符串。OleDbConnectionStringBuilder 类可用于为 Access 数据库创建连接字符串。还有用于 SQL Server 数据库（SqlConnectionStringBuilder）以及其他提供程序的类。这些类使你能够以编程方式创建连接字符串。

> **注意**
>
> 使用数据库时可能会引发异常。你可以将建立数据库连接的语句括在 `try` 块中，并在 `catch` 子句中编写程序语句，以应对无法建立连接的那些异常情况。

## 从数据库中检索数据

连接到数据库后，以编程方式从数据库检索记录的一种方法是发出结构化查询语言（SQL）查询。每个不同的数据提供程序命名空间中都有另一个类，即命令类，用于保存 SQL 语句。OleDbCommand 类用于保存针对 OleDb 数据库管理系统（例如 Microsoft Access）的 SQL 语句或存储过程。构造 OleDbCommand 类的对象后，它具有若干属性，使你能够将命令（SQL 查询）与连接字符串关联起来。示例 14-3 实例化 OleDbCommand 类的对象，并设置该类的 CommandText 和 Connection 属性。示例 14-3 将示例 14-1 中实例化的 OleDbConnection 对象 dbConn 赋给 OleDbCommand 对象的 Connection 属性。

### 示例 14.3

```csharp
string sql;
sql = "SELECT * FROM memberTable ORDER BY LastName ASC, "
     + "FirstName ASC;";   // Note the two semicolons.

OleDbCommand dbCmd = new OleDbCommand();
dbCmd.CommandText = sql;    // Set the command to the SQL string.
dbCmd.Connection = dbConn;  // dbConn is the connection object
                            // instantiated in Example 14-1.
```

### SQL 查询

SQL（正式发音为“S-Q-L”，但通常发音为“sequel”）由 IBM 的一个团队于 20 世纪 70 年代开发，作为一种提供关系数据库系统接口的语言。关系模型由同样在 IBM 的 Edgar Codd 发明。SQL 是一种通用语言，可用于许多数据库产品，包括 SQL Server 和 Microsoft Access。SQL 是一种基于关键字的语言，每条语句都以唯一的关键字开头。SQL 语法不区分大小写；然而，常见做法是将关键字大写输入。每种产品都有各自不同的专有扩展或方言。SQL 中的查询可用于 SELECT、INSERT、UPDATE、DELETE 以及 FIND 数据在表中的位置。

示例 14-3 中显示的 SELECT 语句 SELECT * FROM memberTable ORDER BY LastName ASC, FirstName ASC; 是一条简单的 SQL 语句，用于检索 memberTable 表中的每一行和每一列。SQL 查询中使用的星号（*）指定选择名为 memberTable 的数据库表中的所有字段。ASC 是 ascending（升序）的缩写——表示查询结果将按 LastName 升序列出返回。由于 FirstName 也包含 ASC，任何重复的姓氏都会按名字升序排列。请注意，SQL 查询以分号结尾，整个查询放在双引号内，而该查询又以另一个分号结尾。最后一个分号用于结束将查询赋给名为 sql 的字符串变量的赋值语句。

连接打开后，可以使用任何有效的 SQL 语句来检索数据。图 14–1 显示了此示例使用的 Access 数据库表。

![](img/36e48639a06772bcb0fa1ea2525b33a3_941_0.png)

图 14–1 Access 数据库表

如果你不想检索所有字段，可以将示例 14–3 中显示的星号（*）替换为一个或多个数据字段名（用逗号分隔）。数据字段名是数据库表中的列标题。仅检索名字、姓氏和电话号码的 SQL 语句如示例 14-4 所示。

### 示例 14.4

```sql
SELECT FirstName, LastName, PhoneNumber FROM memberTable;
```

示例 14–4 中包含的 SQL 语句是最基本格式的示例。它只从单个表中检索指定的列。检索所有行。要从表中检索单行或仅检索部分行，需要向 SQL 查询添加 WHERE 子句。例如，要检索与 Gary Jones 关联的电话号码，SQL 语句应如示例 14-5 所示。

### 示例 14.5

```sql
SELECT PhoneNumber FROM memberTable
WHERE FirstName = 'Gary' AND LastName = 'Jones';
```

此语句仅返回电话号码，因为这是 SELECT 语句之后指定的唯一字段。它不返回姓名。请注意，对于 SQL 语句，字符串字面量值（'Gary' 和 'Jones'）括在单引号中。另外请注意
