
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

### 3.4.3.5 Command 类的构造函数

`Command` 类的构造函数是一个重载方法，具有多个原型。图 3.13 列出了四种常用的原型（以 SQL Server Data Provider 为例）。

第一个构造函数是一个不带任何参数的空构造函数。如果你想使用此构造函数实例化一个新的 `Command` 对象，则必须创建并将每个属性赋值给 `Command` 对象的关联属性。

第二个构造函数包含两个参数；第一个是字符串变量类型的参数名，第二个是对象类型的值。第三个构造函数与第二个构造相似，区别在于包含了数据类型和数据大小参数。

图 3.14 显示了创建 `SqlCommand` 对象的示例。该示例包含以下功能：

- 1. 创建一个 `SqlCommand` 对象。
- 2. 创建两个 `SqlParameter` 对象。
- 3. 初始化两个 `SqlParameter` 对象。
- 4. 初始化 `SqlCommand` 对象。
- 5. 将两个 `Parameter` 对象添加到 `Command` 对象 `SqlCommand` 的 `Parameters` 集合中。

以下两行代码创建了带有两个动态参数 `user_name` 和 `pass_word` 的 SQL 语句。通过两个字符串拼接形成一个完整的字符串。在接下来的行中创建了两个 `SqlParameter` 和一个 `SqlCommand` 对象。

然后使用命名参数和关联的文本框对 `SqlParameter` 对象进行初始化。之后，使用 `Command` 类的四个属性初始化 `SqlCommand` 对象。

现在让我们来看 `Command` 类中常用的方法。

**图 3.13** `Command` 类构造函数的三种原型。

```sql
SqlCommand SqlCommand = new SqlCommand();
SqlCommand = new SqlCommand(connString);
SqlCommand = new SqlCommand(connString, SqlConnection);
SqlCommand = new SqlCommand(connString, SqlConnection, SqlTransaction);
```

```sql
string cmdString = "SELECT user_name, pass_word FROM Login "
cmdString += "WHERE (user_name = @Param1) AND (pass_word = @Param2)"
SqlParameter paramUserName = new SqlParameter();
SqlParameter paramPassWord = new SqlParameter();
SqlCommand AsCommand = new SqlCommand(cmdString);

paramUserName.ParameterName = "@Param1"
paramUserName.Value = txtUserName.Text;
paramPassWord.ParameterName = "@Param2"
paramPassWord.Value = txtUserName.Text;
SqlCommand.Connection = SqlConnection;
SqlCommand.CommandType = CommandType.Text;
SqlCommand.CommandText = cmdString;
SqlCommand.Parameters.Add(paramUserName);
SqlCommand.Parameters.Add(paramPassWord);
```

**图 3.14** 创建 `SqlCommand` 对象的示例。

# 使用 C# 进行 SQL Server 数据库编程

| 方法名称 | 功能 |
| --- | --- |
| `ExecuteReader()` | 执行返回行的命令，例如 SQL SELECT 语句。返回的行位于 `OleDbDataReader`、`OdbcDataReader` 或 `OracleDataReader` 中，取决于你使用的哪种 Data Provider。 |
| `ExecuteScalar()` | 从数据库中检索单个值。 |
| `ExecuteNonQuery()` | 执行非查询命令，如 SQL INSERT、DELETE、UPDATE 和 SET 语句。 |
| `ExecuteXml(SqlCommand)` | 与 `ExecuteReader` 方法类似，但返回的行必须使用 XML 表达式。此方法仅适用于 SQL Server Data Provider。 |

## 3.15 Command 类的方法

## 3.4.3.6 Command 类的方法

在上一节中，我们讨论了如何创建 `Command` 类的实例以及如何通过将 `Parameter` 附加到 `Command` 来初始化 `Command` 对象的 `Parameters` 集合。这些步骤是执行 `Command` 的前提。`Command` 对象的实际执行是运行 `Command` 类的一个方法来执行数据查询或数据操作。四种常用的方法被广泛用于数据驱动应用程序，图 3.15 列出了这些方法。

如上一节所述，`Command` 对象是依赖于 Data Provider 的对象，因此开发了四个版本的 `Command` 对象，每个版本由用户在应用程序中选择的 Data Provider 决定，例如 `OleDbSqlCommand`、`SqlCommandSqlCommand` 和 `OracleCommand`。虽然每个都依赖于 Data Provider，但 `Command` 对象的所有方法在功能上是类似的，并在数据驱动应用程序中具有相同的作用。

### 3.4.3.1 ExecuteReader 方法

`ExecuteReader()` 是一个查询方法，它可以用于从数据库中执行读取操作。最常用的匹配操作是使用此方法执行 SQL SELECT 语句，并将行返回给 `DataReader`。取决于你使用的哪种 Data Provider，应该利用不同的 `DataReader` 作为接收者来持有返回的行。记住，`DataReader` 类是一个只读类，可以作为数据持有器。你不能使用 `DataReader` 执行任何数据更新。

下面的示例代码可以执行 SQL SELECT 语句，如图 3.16 所示。

如图 3.16 所示，当调用 `ExecuteReader()` 时，将执行 SQL SELECT 语句从表中检索 id、`user_name` 和 `pass_word`。返回的行

```sql
string cmdString = "SELECT user_name, pass_word FROM Log ";
SqlCommand SqlCommand = new SqlCommand();
SqlCommand.Connection = sqlConnection;
SqlCommand.CommandType = CommandType.Text;
SqlCommand.CommandText = cmdString;
SqlDataReader reader = SqlCommand.ExecuteReader();
```

图 3.16 执行 `ExecuteReader` 方法的代码。

# ADO.NET 简介 73

```sql
string cmdString = "SELECT pass_word FROM Login WHERE (user_name = ybai)";
SqlCommand SqlCommand = new SqlCommand();
string password = string.Empty;

SqlCommand.Connection = sqlConnection;
SqlCommand.CommandType = CommandType.Text;
SqlCommand.CommandText = cmdString;
passWord = SqlCommand.ExecuteScalar();
```

**图 3.17** 使用 `ExecuteScalar` 方法的示例代码。请注意，在调用 `ExecuteReader()` 方法之前，`SqlCommand` 对象应该已经创建并初始化。

### 3.4.3.6.2 ExecuteScalar 方法

`ExecuteScalar()` 用于从数据库中检索单个值。此方法比 `ExecuteReader()` 方法更快，且开销小得多。当需要从源检索单个值时，您应该使用此方法。

一个 SQL 语句示例用于根据用户名 ybai 从 `Login` 表获取密码。此密码可以被视为单个值。在创建并初始化 `SqlCommand` 后调用 `ExecuteScalar()` 方法。返回值是一个 `String`，并赋值给字符串变量 `password`。

第 5 章第 5.8 节提供了该方法的示例，用于获取 `CSE_DEPT` 表中的单个值密码。

### 3.4.3.6.3 ExecuteNonQuery 查询方法

所述，`ExecuteNonQuery` 方法是一个只读方法，仅用于执行数据任务。要执行不同的 SQL 语句如 INSERT、UPDATE 或 DELETE 命令，需要 `ExecuteNonQuery` 方法。

图 3.18 显示第一个 SQL 语句尝试向 `Login` 数据表插入一个新*值*。在创建并初始化 `SqlCommand` 对象后，调用 `ExecuteNonQuery()` 方法执行 INSERT 语句。对 DELETE 语句执行类似的步骤。

现在来看 DataProvider 中的类，`DataAdapter`。

```sql
string cmdString1 = "INSERT INTO Login (pass_word) VALUES ('reback')";
string cmdString2 = "DELETE FROM Login WHERE (user_name = ybai)";
SqlCommand SqlCommand = new SqlCommand();

SqlCommand.Connection = sqlConnection;
SqlCommand.CommandType = CommandType.Text;
SqlCommand.CommandText = cmdString1;
SqlCommand.ExecuteNonQuery();
SqlCommand.CommandText = cmdString2;
SqlCommand.ExecuteNonQuery()();
```

## 3.4.4 DataAdapter 类

`DataAdapter` 充当 `DataSet` 和数据源之间的桥梁，用于检索和保存数据。`DataAdapter` 通过映射 `Fill()`（更改 `DataSet` 中的数据）和 `Update`（更改数据源数据以匹配 `DataSet` 中的数据）来提供此桥梁。

`DataAdapter` 使用 `Connection` 对象连接到数据库，并使用 `Command` 对象从数据库检索数据并填充到 `DataSet` 以及相关类（如 `DataTables`）中。`DataAdapter` 使用 `Command` 对象将数据从数据库发送到数据库。

要执行从数据库到 `DataSet` 的查询，`DataAdapter` 使用合适的 `Command` 对象并将它们分配给适当的 `DataAdapter` 属性（如 `SelectCommand`），然后执行。要执行其他操作，`DataAdapter` 使用相同的 `Command` 对象，但分配给不同的属性（如 `InsertCommand`、`DeleteCommand`）以处理关联的数据操作。

如前一节所述，`DataAdapter` 是数据提供程序（Data Provider）的子组件，这意味着 `DataAdapter` 根据所使用的数据提供程序有不同的版本。常见的 `DataAdapter` 包括：`OleDataAdapter`、`SqlDataAdapter` 和 `OracleDataAdapter`。不同的 `DataAdapter` 位于不同的命名空间。

如果你连接到服务器数据库，可以通过使用 `SqlDataAdapter` 及其相关的 `SqlCommand` 和 `SqlConnection` 对象来提高整体性能。对于支持 OLE DB的数据源，使用 `OleDataAdapter` 及其相关的 `OleCommand` 和 `OleDbConnection` 对象。对于 ODBC 数据源，使用 `OdbcDataAdapter` 及其相关的 `OdbcCommand` 和 `OdbcConnection` 对象。对于 Oracle 数据库，使用 `OracleDataAdapter` 及其相关的 `OracleCommand` 和 `OracleConnection`。

### 3.4.4.1 DataAdapter类的构造函数

`DataAdapter` 类的构造函数是一个重载方法，它有多个协议。图 3.19 列出了两种常用的协议（以 SQL Server 数据提供程序为例）。第一个构造函数通常用于大多数数据驱动的应用程序。

### 3.4.4.2 DataAdapter类的属性

图 3.20 列出了 `DataAdapter` 类的一些属性。

| 构造函数 | 描述 |
| --- | --- |
| `SqlDataAdapter()` | 初始化 `DataAdapter` 的类的新实例 |
| `SqlDataAdapter(from)` | 从现有相同类型对象初始化 `DataAdapter` 的类的新实例 |

图 3.19 `DataAdapter` 类的构造函数。

| 属性 | 描述 |
| --- | --- |
| `AcceptChangesDuringFill` | 获取一个值，表示在任何 `Fill` 操作期间将 `DataRow` 添加到 `DataTable` 后，是否在 `DataRow` 上调用了 `AcceptChanges` |
| `MissingMappingAction` | 决定当传入的数据没有匹配的表或列时要采取的操作 |
| `MissingSchemaAction` | 决定当现有的 `DataSet` 架构与传入的数据不匹配时要采取的操作 |
| `TableMappings` | 获取一个提供源表和 `DataTable` 之间主映射的集合 |

图 3.20 `DataAdapter` 类的公共属性。

## ADO.NET 简介

| 方法 | 描述 |
|---|---|
| `Dispose` | 释放 `DataAdapter` 使用的资源。 |
| `Fill` | 使用 `DataSet` 名称添加或刷新 `DataSet` 中的行以匹配数据源中的行，并创建一个 `DataTable`。将 `DataTable` 添加到指定的 `DataSet` 中。 |
| `GetParameters` | 获取用户执行 SQL 语句时设置的参数。 |
| `ToString` | 返回代表组件的字符串（如果有）。此方法不应被重写。 |
| `Update` | 为指定 `DataSet` 中来自命名 `DataTable` 的每个插入、更新或删除的行调用 INSERT、UPDATE 或 DELETE 语句。 |

图 3.21 `DataAdapter` 类的公共方法。

### 3.4.4.3 DataAdapter类的方法

`DataAdapter` 有超过 10 个方法可以帮助用户开发专业的数据驱动应用程序。图 3.21 列出了一些最常用的方法。

在这些方法中，**`Dispose`**、**`Fill`**、**`FillSchema`** 和 ** `Update`** 是最常用的方法。**`Dispose()`** 方法应在 `DataAdapter` 完成工作后用于释放 `DataAdapter`。**`Fill()`** 方法应在 `Command` 初始化并准备好就绪后用于填充 `DataSet`。如果你想向 `DataSet` 中添加新的 `DataTable`，应调用 **`FillSchema()`** 方法，如果你想对数据库和 `DataSet` 执行某些插入、更新和删除等数据操作，则应使用 **`Update()`** 方法。

### 3.4.4.4 DataAdapter类的事件

`DataAdapter` 类中有两个常用的事件被广泛使用，这些事件列在图 3.22 中。

在完成此之前，提供了一个代码示例，向读者展示如何使用 `DataAdapter` 在你的 `DataSet` 和数据库之间执行某些数据和操作。图 3.23 显示了使用 SQL ServerDataAdapter 的示例（假设已创建了 Connection 对象 **`SqlConnection`**）。

从步骤 A 开始，创建一个 SQL SELECT 语句以及其他对象的声明，例如 `SqlCommand` 的新实例和 `DataSet` 的新实例。`DataSet` 类将在下一节中讨论，**`Fill()`** 方法将用于填充。

在步骤 B，使用 `Connection` 对象初始化 `SqlCommand` 填充数据。

在步骤 C，`SqlDataAdapter` 使用命令字符串初始化。
