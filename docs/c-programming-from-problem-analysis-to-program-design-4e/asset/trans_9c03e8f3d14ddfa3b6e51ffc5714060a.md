
可以通过几种方式完成。你可以编写包含 INSERT、DELETE 和 UPDATE 语句的 SQL 语句，然后通过调用 `OleDbCommand.ExecuteNonQuery( )` 方法执行这些查询。另一种更简单的方法是实例化数据集类和数据适配器类的对象。你使用数据适配器对象来填充数据集对象。数据适配器类具有 `Fill( )` 和 `Update( )` 等方法，可以省去编写 SQL 更新语句的需要。接下来的各节将解释如何实现这一点。

## 更新数据库数据

ADO.NET 并不要求你与数据库保持持续的活动连接，也不要求你一次处理一条检索到的记录。还有一些类可用于让你与数据库连接足够长的时间，以便将记录检索到内存中。随后可以更改数据，并重新连接到数据库以更新数据。这可以提高应用程序的性能，并允许其他应用程序在你以断开连接模式工作时访问数据库。这样做时，你会在内存中创建从数据库检索到的记录的临时副本，然后处理临时数据，而不是处理数据库中存储的实时数据。在 .NET 中，这是通过使用数据集来实现的。**数据集**是从某个数据源检索到的记录的缓存，其中可能包含来自该数据源的一个或多个表。数据集与实际数据库之间的交互通过数据适配器进行控制。

## 使用数据集处理数据库记录

与数据读取器对象一样，根据所访问的数据库类型，你会在每个不同的数据提供程序命名空间中使用不同的数据集类和数据适配器类。对于 Access 数据库提供程序类，你仍然需要添加：`using System.Data.OleDb;`

在处理从 SQL 查询检索到的数据之前，你需要包含与使用数据库读取器对象时相同的程序语句。你仍然要使用 OleDb 数据提供程序的连接字符串实例化连接对象，并且仍然要指定数据库名称。你将在本章后面的小节中了解到这一点，但是使用数据适配器对象时，不必调用连接对象的 `Open( )` 方法。这会自动为你处理。

你仍然通过执行 SQL SELECT 语句从数据库中选择记录（和字段）。正如你在示例 14–13 中看到的那样，SQL 语句封装在数据命令对象中。因此，你仍然需要实例化 `OleDbCommand` 类的对象，并将该类的 `CommandText` 属性设置为该 SQL 字符串。示例 14–13 中的这些语句在示例 14–14 中为你重复列出。到目前为止，使用数据库读取器类与使用数据集和数据适配器类之间的唯一区别是省略了 `dbConn.Open( )`。仍然需要连接对象和命令对象。

### 示例 14.14

```csharp
private OleDbConnection dbConn;
private OleDbCommand dbCmd;
private string sConnection;
private string sql;
:    // Colon indicates items missing

// Construct an object of the OleDbConnection
// class to store the connection string
// representing the type of data provider
// (database) and the source (actual db).
sConnection =
        "Provider=Microsoft.ACE.OLEDB.12.0;" +
        "Data Source=member.accdb";
dbConn = new OleDbConnection(sConnection);

// Construct an object of the OleDbCommand
// class to hold the SQL query. Tie the
// OleDbCommand object to the OleDbConnection
// object.
sql = "SELECT * FROM memberTable ORDER " +
       "BY LastName ASC, FirstName ASC;";
dbCmd = new OleDbCommand();
dbCmd.CommandText = sql;
dbCmd.Connection = dbConn;
```

### DATASET 对象

数据读取器对象一次保存查询结果中的一条记录。数据集对象存储整个类似关系表的结构。数据集对象可以存储多个表，以及数据库上的关系和约束。数据集被视为数据在内存中的表示。可以实例化 `DataSet` 类的对象，如示例 14–15 所示。

### 示例 14.15

```csharp
DataSet memberDS = new DataSet();
```

### DATAADAPTER 对象

使用 `DataSet` 对象的一种简单方法是实例化 `DataAdapter` 类的对象。适配器用于在数据库源和数据集对象之间交换数据。如果进行了更改，适配器还可以更轻松地更新数据库。可以实例化 OleDb 提供程序的 `DataAdapter` 类的对象，如示例 14–16 所示。

### 示例 14.16

```csharp
OleDbDataAdapter memberDataAdap = new OleDbDataAdapter();
```

> **注意**
>
> 有几个新类和一个 **数据源配置向导** 可用于简化连接数据库的过程。每个数据提供程序都提供了一个 `TableDataAdapter` 类。你将在本章后面体验使用该向导和新类。

### 命令生成器对象

还可以使用另一个类来自动生成 SQL 语句，这样除了用于检索记录的初始 `SELECT` 语句之外，你就不必进行额外的 SQL 编程。这就是 `OleDbCommandBuilder` 类。设置 `OleDbDataAdapter` 类的 `SelectCommand` 属性后，`OleDbCommandBuilder` 对象会自动生成用于更新的 SQL 语句。该属性被设置为从数据库检索数据的 SQL 语句。示例 14-17 的以下代码段展示了该类的实例化和属性设置。

### 示例 14.17

```csharp
private OleDbCommandBuilder cBuilder;
:    // Colon indicates items missing
cBuilder = new OleDbCommandBuilder(memberDataAdap);
memberDataAdap.SelectCommand = dbCmd;
```

> **注意**
>
> `CommandBuilder` 对象只能用于映射到单个数据库表的数据集。用于设置 `SelectCommand` 属性的 SQL 语句还必须返回至少一个主键或唯一列。主键是唯一标识行的值。例如，每个学生都有一个唯一的学生 ID。它很适合作为主键。如果不存在主键，则会生成 `InvalidOperation` 异常，并且不会生成命令。

### 使用数据适配器填充数据集

在实例化了 *数据适配器*、*数据集* 和 *命令生成器* 类的对象之后，你就可以开始了。通过指定要用作数据源的表名，使用数据适配器填充数据集，如示例 14-18 所示。

### 示例 14.18

```csharp
memberDataAdap.Fill(memberDS, "memberTable");
```

`Fill()` 方法可以在不编写额外 SQL 语句的情况下使用，因为你实例化了命令生成器类的对象。命令生成器会自动为 `DataAdapter` 类的 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 属性生成 SQL 语句。你可以采用与设置 `SelectCommand` 属性完全相同的方式设置每个属性的值——使用包含 SQL 语句的字符串。

**注意** 如果你的应用程序要求数据集包含来自两个或更多表的值，则不能让命令生成器类自动为你生成 SQL 语句。在这种情况下，必须设置 `DataAdapter` 类的 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 属性。为此，请使用 SQL INSERT 语句设置 `DataAdapter` 对象的 `InsertCommand` 属性，使用 SQL DELETE 语句设置 `DeleteCommand` 属性，并使用 SQL UPDATE 语句设置 `UpdateCommand` 属性。

这就是从数据库检索记录所需的全部内容。为了显示表的内容并允许用户进行更改，需要一个表示层用户界面层。表值可以显示在控制台屏幕上，也可以显示在 Windows 应用程序的控件上。网格控件特别适合数据集对象。下一节将解释如何将数据集对象绑定到 Windows 应用程序中的数据网格。

### 添加 DataGridView 控件以承载数据集

要查看数据库中的数据，可以将记录放入 Windows 窗体上的 `DataGridView` 对象中。`DataGridView` 控件创建的结构分为行和列，非常像你联想到的关系数据库表结构。除了可以在数据网格中导航之外，你还可以通过编辑当前记录以及插入和删除新记录来进行更改。要将 `DataGridView` 对象绑定到数据集，请使用 `dataGridView` 对象的 `DataSource` 和 `DataMember` 属性，如示例 14-19 所示。

### 示例 14.19

```csharp
dataGridView1.DataSource = memberDS;
dataGridView1.DataMember = "memberTable";
```

**注意** 有 50 多种不同的 `Windows.Forms` 控件可以添加到应用程序中。下拉列表中并未显示所有控件。可以使用 **工具** 菜单中的 **选择工具箱项** 将其他控件添加到工具箱中。

