

# 使用 C# 进行 SQL Server 数据库编程

| 数据类型 | 关联的数据提供程序 |
|---|---|
| OdbcType | ODBC 数据提供程序 |
| ODbType | OLE DB 提供程序 |
| SqlDbType | SQL Server 数据提供程序 |
| OracleType | Oracle 数据提供程序 |

**图 3.9** 数据类型及其关联的数据提供程序。

第一个属性 `ParameterName` 包含选中参数的名称。第二个属性 `Value` 是所选参数的值，它是一个对象。第三个属性 `DbType` 用于定义所选参数的类型。

`Parameter` 对象中的所有参数都必须有一个数据类型，你可以通过指定 `DbType` 为所选参数指定数据类型。ADO.NET 和 ADO.NET Data Provider 对它们提供的数据类型有不同的定义。`DbType` 是 ADO.NET 使用的数据类型，但 ADO.NET Data Provider 还有四种常用的数据类型，每种类型都与一个数据提供程序相关联。3.9 列出了这些数据类型以及关联的数据提供程序。

即使 ADO.NET 和 ADO.NET Data Provider 提供的数据类型不同，但它们之间存在直接的联系。作为用户，你可以使用任何数据类型，如果你设置了其中一个，另一个将自动更改为对应的值。例如，如果你将 `SqlParameter` 对象的 `DbType` 设置为 `String`，则 `SqlDbType` 将被自动设置为 `Char`。在本书中，我们将使用 ADO.NET Data Provider 定义的数据类型，因为本节讨论的所有参数都与数据提供程序有关。`DbType` 属性的默认数据类型是 `String`。

## 3.4.3.3 参数映射

当你通过将 `Parameter` 对象附加到 `Command` 对象的 `Parameters` 属性来向 `Command` 对象添加 `Parameters` 集合时，`Command` 对象需要知道添加的参数与你在 SQL 查询字符串中使用 `SELECT` 语句时使用的参数之间的关系。换句话说，`Command` 对象需要识别所使用的参数应该映射到这个新添加的参数。不同的数据提供程序使用不同的参数映射。3.10 列出了这些映射。

OLE 和 ODB 数据提供程序都使用所谓的“位置参数映射”，这意味着 SQL 语句中定义的参数与添加到 `Parameters` 集合中的参数之间的关系在顺序上是一一对应的。换句话说，参数在 SQL 语句中出现的顺序与参数添加到 `Parameters` 集合的顺序应该是相同的。位置参数映射用问号 `'?'` 表示。

例如，以下 SQL 语句用作 OLE DB 数据提供程序的查询字符串：

```
SELECT user_name, pass_word FROM Login WHERE (user_name=?) AND (pass_word=?)
```

`user_name` 和 `pass_word` 映射到登录数据表中的两列。此 SQL 语句中用两个问号 `'?'` 表示两个动态参数。

| 参数映射 | 关联的数据提供程序 |
|---|---|
| 位置参数映射 | ODBC 数据提供程序 |
| 位置参数映射 | OLE DB 提供程序 |
| 命名参数映射 | SQL Server 数据提供程序 |
| 命名参数映射 | Oracle 数据提供程序 |

**图 3.10** 不同的参数映射。

## ADO.NET 简介

要向 `accCommand` `Command` 对象的 `Parameters` 集合中添加参数，你需要使用如下所示的 `Add()` 方法：

```
accCommand.Parameters.Add("user_name", OleDbType.Char).Value =
txtUserName.Text;
accCommand.Parameters.Add("pass_word", ODbType.Char, 8).Value =
txtPassWord.Text;
```

你必须小心添加这些参数（`user_name` 和 `pass_word`）的顺序，并确保该顺序与这两个动态参数在上述 SQL 语句中出现的顺序相同。

Server 和 Oracle 数据提供程序都使用“命名参数映射”，这意味着每个参数（无论是在 SQL 语句中定义的还是被添加到 `Parameters` 集合中的）都是通过名称识别的。换句话说，SQL 语句或存储过程中的参数名称必须与你添加到 `Parameters` 集合中的参数名称完全一致。例如，以下 SQL 语句用于 SQL Server 数据提供程序的查询：

```
SELECT user_name, pass_word FROM LOGIN WHERE user_name LIKE @Param1
AND (pass_word LIKE @Param2)
```

`user_name` 和 `pass_word` 映射到 Log 数据表中的两列。与上述 SQL 语句相比，SQL 语句中没有使用动态参数 `@Param1` 和 `@Param2` 的名称来表示两个动态参数。这两个参数的运算符被替换为了关键字 `LIKE`。这是 SQL Server 数据提供程序的要求。

然后，你需要与你的 `Command` 对象关联两个 `Parameter` 对象，初始化这两个 `Parameter` 对象的示例见图 3.11。

当你为 `ParameterProperties` 分配了动态参数 `"@Param1"` 和 `"@Param2"` 时，`Param1` 和 `Param2` 都是动态参数的符号名称，并且在每个参数前面都有一个符号，因为这是在 SQL 语句中使用动态参数时 SQL Server 数据库的要求。

从这段代码中可以看出，用于每个 `Parameter` 对象的每个参数名称必须与你在 SQL 语句中定义的名称完全一致。由于 SQL Server 和 Oracle 数据提供程序使用命名参数映射，你不需要担心将 `Parameter` 对象添加到 `Command` 对象 `Parameters` 集合的顺序。

要向 `Command` 的 `Parameters` 集合中添加参数，你需要使用 `ParameterClass` 中定义的一些方法。

## 3.4.3.4 ParameterCollection 类的方法

每个 `ParameterClass` 都有十多个方法，但在数据驱动应用中常用的两种方法是 `Add()` 和 `AddWithValue()`。在执行查询之前，需要将这些参数添加到 `Command` 的 `Parameters` 集合中。

```
SqlParameter userName = new SqlParameter();
SqlParameter passWord = new SqlParameter();

userName.ParameterName = "@Param1"; userName.Value = txtUserName.Text;
passWord.ParameterName = "@Param2"; passWord.Value = txtPassWord.Text;
```

图 3.11 初始化这两个 Parameter 对象的示例

# 使用 C# 进行 SQL Server 数据库编程

正如我们所提到的，如果你使用的是 SQL Server 或 Oracle 数据提供程序，就不需要担心将 `Parameter` 对象添加到 `Command` 对象 `Parameters` 集合的顺序。然而，如果你使用的是 ODBC 数据提供程序，则必须注意将参数添加到 `Parameters` 对象的顺序。

要向 `Command` 的 `Parameters` 集合中添加参数，通常采用两种常用方法是 `Add()` 方法和 `AddWithValue()`。`Add()` 方法是重载方法，有五种格式，但只有两种被广泛使用。这两种方法的格式如下：

```
ParameterCollection.Add(SqlParameter value);
ParameterCollection.Add(string parameterName, Object value);
```

第一个方法需要一个 `Parameter` 对象作为参数，在调用此 `Add()` 将其添加到集合之前，该 `Parameter` 对象应该已经初始化。第二个方法包含两个参数：第一个是包含 `ParameterName` 的字符串，第二个是包含该参数值的对象。`AddValue()` 方法类似于 `Add()` 方法的第二个格式：

```
ParameterCollection.AddWithValue(string parameterName, Object value);
```

图 3.12 使用这些方法将参数添加到集合中的一个示例。上半部分用于创建和初始化 `Parameter` 对象，我们在之前的节中已经讨论过。首先执行 `Add()` 将两个参数（`userName` 和 `password`）添加到 `Command` 的 `Parameters` 集合中。要使用此方法，这两个 `Parameter` 对象应该已经初始化。实现此操作的另一种方法是使用 `AddValue()` 方法添加这两个 `Parameter` 对象，这类似于 `Add()` 方法的第二个格式。

> Command 类中的 `Parameters` 是 `Parameter` 对象的集合。你需要创建并初始化 `Parameter` 对象，然后就可以将 `Parameter` 对象添加到 `Parameters` 集合中。通过这种方式，你可以将其赋值给 `Command` 对象。

```
SqlParameter userName = new SqlParameter();
SqlParameter passWord = new SqlParameter();

userName.ParameterName = "@Param1";
userName.Value = txtUserName.Text;
passWord.ParameterName = "@Param2";
passWord.Value = txtPassWord.Text;

SqlCommand.Parameters.Add(userName);
SqlCommand.Parameters.Add(passWord);

SqlCommand.Parameters.AddWithValue("@Param1", txtUserName.Text);
SqlCommand.Parameters.AddWithValue("@Param2", txtPassWord.Text);
```

图 3.12 添加参数的两种方法。

