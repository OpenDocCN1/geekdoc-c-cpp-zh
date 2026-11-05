
![](img/3005a4307e6d8f3bb7e76eea28a92357_465_0.png)

图 16.5.1 数据集

## 16.6 处理数据

### 16.6.1 ADO .NET——通过数据操作类处理数据

- 使用数据库时，会按顺序实例化以下层次结构。

![](img/3005a4307e6d8f3bb7e76eea28a92357_465_1.png)

图 16.6.1 数据库对象创建

### 1. 创建 SqlConnection 对象

- SqlConnection 是一个对象，就像任何其他 C# 对象一样，其声明和实例化如下，

```
SqlConnection conn = new SqlConnection(
"Data Source=(local);Initial Catalog=Northwind;Integrated Security=SSPI");
```

上面实例化的 SqlConnection 对象使用带有一个 string 类型参数的构造函数。此参数称为连接字符串。

- 连接字符串的常见部分

ADO.NET 连接字符串包含某些键/值对，用于指定如何建立数据库连接。它们包括数据库的位置、名称和安全参数。

| 连接字符串参数名称 | 描述 |
|---|---|
| Data Source | 标识服务器。可以是本地计算机、计算机域名或 IP 地址。 |
| Initial Catalog | 数据库名称。 |
| Integrated Security | 设置为 SSPI 以使用用户的 Windows 登录建立连接 |
| User ID | 在 SQL Server 中配置的用户名。 |
| Password | 与 SQL Server 用户 ID 匹配的密码。 |

- 以下语句展示了一个连接字符串，出于安全目的使用 User ID 和 Password 参数，

```
SqlConnection conn = new SqlConnection(
    "DataSource=DatabaseServer;Initial Catalog=Northwind;UserID=ValidUserID;Password=ValidPassword");
```

- 请注意 Data Source 如何设置为 DatabaseServer，以表明可以标识位于不同计算机上、通过局域网或通过 Internet 访问的数据库。此外，User ID 和 Password 替换了 Integrated Security 参数。

### C# ADO.NET 连接字符串

- 连接字符串是一种普通的 String 表示形式，包含用于在数据库和应用程序之间建立连接的数据库连接信息。连接字符串包括驱动程序名称、服务器名称和数据库名称等参数，以及用户名和密码等安全信息。
- 通常，数据提供程序使用包含一组参数的连接字符串，通过应用程序与数据库建立连接。.NET Framework 主要提供三种数据提供程序，分别是 Microsoft SQL Server、OLEDB、ODBC。

### 构建 Microsoft SQL Server 连接字符串

```
connectionString = "Data Source=ServerName;Initial Catalog=Databasename;
User ID=UserName;Password=Password"
```

### 构建 OLEDB 数据提供程序连接字符串

```
connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;
Data Source=yourdatabasename.mdb;"
```

### 构建 ODBC 连接字符串

```
connectionString = "Driver={Microsoft Access Driver (*.mdb)};
DBQ=yourdatabasename.mdb;"
```

- 必须为连接字符串属性提供必要的连接信息，以便构建连接字符串。

### 2. 使用 SqlConnection

创建 SqlConnection 对象的目的是对数据库进行操作。其他 ADO.NET 对象（如 SqlCommand 和 SqlDataAdapter）将连接对象作为参数。SqlConnection 生命周期中发生的操作顺序可以是：

- 1. 实例化 SqlConnection。
- 2. 打开连接。
- 3. 将连接传递给其他 ADO.NET 对象。
- 4. 使用其他 ADO.NET 对象执行数据库操作。
- 5. 关闭连接。

### 示例

```csharp
// Illustration of working with SqlConnection objects
using System;
using System.Data;
using System.Data.SqlClient;

class SqlConnectionDemo
{
    static void Main()
    {
        // 1. Instantiate the connection object
        SqlConnection sqlconn = new SqlConnection(
            "Data Source=(local);Initial Catalog=Northwind;Integrated Security=SSPI");

        SqlDataReader sqldr = null;

        try
        {
            // 2. Open the connection
            sqlconn.Open();

            // 3. Pass the connection to a command object
            SqlCommand sqlcmd = new SqlCommand("select * from Books", conn);

            //
            // 4. Use the connection
            //
```
```
// get query results
sqlrdr = sqlcmd.ExecuteReader();

// print the BookID of each record
while (sqlrdr.Read())
{
    Console.WriteLine(sqlrdr[0]);
}
finally
{
    // close the reader
    if (sqlrdr != null)
    {
        sqlrdr.Close();
    }

    // 5. Close the connection
    if (sqlconn != null)
    {
        sqlconn.Close();
    }
}
}
```

### 代码片段说明

- 通过调用 SqlConnection 实例 sqlconn 的 Open() 方法打开连接。对尚未打开的连接执行任何操作都会生成异常。因此，必须先打开连接，然后才能使用它。
- 在使用 SqlCommand 之前，ADO.NET 应知道应用程序需要哪个连接。SqlCommand 对象的第二个参数设置为 SqlConnection 对象 sqlconn。使用 SqlCommand 执行的任何操作都将仅使用此连接。
- 使用连接的代码是一个 SqlCommand 对象，它对 Book 表执行查询。结果集以 SqlDataReader 形式返回，while 循环读取结果集每一行的第一列，即 BookID 列。
- 连接对象使用完毕后，必须关闭它。否则可能会对应用程序的性能和可伸缩性造成严重后果。在 finally 块中调用 Close() 方法，并确保在关闭连接之前连接不为 null。

### 3. SqlCommand 对象

- SqlCommand 对象允许指定对数据库的操作。例如，对数据库表中的数据行执行 select、insert、modify 和 delete 命令。SqlCommand 对象也可以使用 SqlDataAdapter 来支持断开连接的数据管理场景。
- Command 对象使用连接对象来执行 SQL 查询。
- 查询可以采用内联文本、存储过程或直接表访问的形式。
- Command 对象的一个重要特性是它可以用于执行带参数的查询和存储过程。
- 如果发出 select 查询，它返回的结果集通常存储在 DataSet 或 DataReader 对象中。

### SqlCommand 类的关联属性

| 属性 | 访问类型 | 描述 |
|---|---|---|
| Connection | 读/写 | 命令对象用于执行 SQL 查询或存储过程的 SqlConnection 对象。 |
| CommandText | 读/写 | 表示 T-SQL 语句或存储过程的名称。 |
| CommandType | 读/写 | 此属性指示应如何解释 CommandText 属性。可能的值有：1. Text（T-SQL 语句）2. StoredProcedure（存储过程名称）3. TableDirect |
| CommandTimeout | 读/写 | 此属性指示执行特定命令时要等待的时间。命令执行的默认时间为 30 秒。命令超时后会被中止，并引发异常。 |

### Command 对象的方法

| 属性 | 描述 |
|---|---|
| ExecuteNonQuery | 此方法执行指定的命令，并返回受影响的行数。 |
| ExecuteReader | ExecuteReader 方法执行指定的命令，并返回 SqlDataReader 类的实例。 |
| ExecuteScalar | 此方法执行指定的命令，并返回结果集第一行第一列。其余行和列将被忽略。 |
| ExecuteXMLReader | 此方法执行指定的命令，并返回 XmlReader 类的实例。此方法可用于以 XML 文档形式返回结果集 |

### 创建 SqlCommand 对象

```csharp
SqlCommand sqlcmd = new SqlCommand("select BookCategoryName from BookCategories", sqlconn);
```

上述语句接受一个包含要执行命令的字符串参数，以及对 SqlConnection 对象的引用。

### 查询数据

使用 SQL select 命令时，会检索数据集以供查看。若要检索数据，使用 ExecuteReader 方法，它返回一个 SqlDataReader 对象。

```csharp
// 1. Instantiate a new command with a query and connection
SqlCommand sqlcmd = new SqlCommand("select BookCategoryName from BookCategories", sqlconn);
// 2. Call Execute reader to get query results
SqlDataReader sqldr = sqlcmd.ExecuteReader();
```

在上述代码片段中，通过将命令字符串和连接对象传递给构造函数来实例化 SqlCommand 对象。然后，通过调用 SqlCommand 对象 sqlcmd 的 ExecuteReader 方法获得 SqlDataReader 对象。

### 插入数据

要将数据插入数据库，使用 SqlCommand 对象的 ExecuteNonQuery 方法。

```csharp
// Illustration of insert data into a database table.
// Prepare command string
string insertString = "@"
insert into BookCategories
(BookCategoryName, Description)
