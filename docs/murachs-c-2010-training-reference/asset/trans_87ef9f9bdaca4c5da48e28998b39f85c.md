

# 创建 SqlDataReader 对象的两种方法

```sql
sqlCommand.ExecuteReader()
sqlCommand.ExecuteReader(behavior)
```

# 常用的 CommandBehavior 枚举成员

| 成员 | 描述 |
| --- | --- |
| CloseConnection | 当读取器关闭时关闭连接。 |
| Default | 等同于未指定命令行为。 |
| SingleRow | 仅返回一行。 |

# SqlDataReader 类的常用成员

| 索引器 | 描述 |
| --- | --- |
| [columnname] | 获取指定名称列的值。 |
| [index] | 获取指定位置列的值。 |
| Property | 获取一个指示数据读取器是否已关闭的值。 |
| Method | 关闭读取器。 |
| Close() | 获取下一行并返回一个指示是否还有额外行的布尔值。 |

# 使用数据读取器读取 State 对象列表的代码

```sql
connection.Open();
SqlDataReader reader = selectCommand.ExecuteReader(CommandBehavior.CloseConnection);
List<State> states = new List<State>();
while (reader.Read()) {
  State s = new State();
  s.Code = reader["State"].ToString();
  s.StateName = reader["StateName"].ToString();
  states.Add(s);
}
reader.Close();
```

# 描述

- *在执行命令对象的 ExecuteReader 方法之前，你必须打开数据读取器所使用的连接。*
- 数据读取器在创建时会自动打开。在它打开期间，无法在同一连接上打开其他数据读取器。唯一的例外是你在使用 Oracle 数据读取器，在这种情况下，其他读取器可以同时打开。
- 当你创建数据读取器时，它位于结果集的第一行之前。要检索第一行，请使用 Read 方法。
- 你可以使用 And (&) 运算符组合两个或多个命令行为成员。

![](img/3148667e42d4db35b3d08576aaa1fa01_650_0.png)

# 如何执行返回单个值的查询

20-7 中的第一个示例向你展示了如何执行返回单个值（即标量值）的命令。要实现这一点，你使用命令的 ExecuteScalar 方法。在这种情况下，命令包含一个 Select 语句，用于检索 Invoices 表中发票总和。这个汇总值通常被称为聚合值。标量值也可以是单个列的值、计算值或从数据库中检索的任何其他值。

由于 ExecuteScalar 方法返回 Object 类型，你必须将该对象强制转换为适当的数据类型以获取其值。在示例中，该对象被转换为 decimal 类型。

在继续之前，你应该意识到，你可以对一个检索多个许多的 Select 语句使用 ExecuteScalar 方法。然而，在这种情况下，ExecuteScalar 方法只返回第一个值，其他值会被丢弃。

# 如何执行操作查询

如你所知，你可以使用 Insert、Update 或 Delete 语句对数据库执行操作。这些语句有时被称为操作查询。要执行操作查询，你使用命令的 ExecuteNonQuery 方法，如 20-7 中的第二个示例所示。

此示例执行了一个包含 Insert 语句的命令，该语句向 Products 表中添加了一行。请注意，ExecuteNonQuery 方法返回一个整数，表示数据库中受操作影响的行数。你可以使用此值来检查操作是否成功。你将在接下来的客户维护应用程序中看到相关示例。

# 创建并执行返回聚合值的命令的代码

```sql
string selectStatement = "SELECT SUM(InvoiceTotal) FROM Invoices";
SqlCommand selectCommand = new SqlCommand(selectStatement, connection);
connection.Open();
decimal invoiceTotal = (decimal)selectCommand.ExecuteScalar();
connection.Close();
```

# 创建并执行插入行的命令的代码

```sql
string insertStatement = "INSERT INTO Products "
+ "(ProductCode, Description, UnitPrice) "
+ "VALUES (@ProductCode, @Description, @UnitPrice)";
SqlCommand insertCommand = new SqlCommand(insertStatement, connection);
insertCommand.Parameters.AddWithValue("@ProductCode", product.Code);
insertCommand.Parameters.AddWithValue("@Description", product.Description);
insertCommand.Parameters.AddWithValue("@UnitPrice", product.Price);
try
{
    connection.Open();
    int productCount = insertCommand.ExecuteNonQuery();
} catch (SqlException ex)
{
    MessageBox.Show(ex.Message);
} finally
{
    connection.Close();
}
```

# 如何执行查询Scalar 返回单个值

- 你使用命令对象的 ExecuteScalar 方法来检索单个值，该值被称为标量值。
- 返回的值可以是数据库中单列单行的值、计算值、汇总数据库数据的聚合值，或从数据库中检索的任何其他值。
- 如果 Select 语句返回多列或多行，ExecuteScalar 方法将仅检索第一列和第一行的值。

# 如何执行操作查询

- 你使用命令对象的 ExecuteNonQuery 方法来执行 Insert、Update 或 Delete 语句，这些语句被称为操作查询。
- ExecuteNonQuery 方法返回一个整数，表示受查询影响的行数。
- 你还可以使用 ExecuteNonQuery 方法执行影响数据库对象结构的语句。欲更多信息，请参阅你的数据库管理系统的文档。

![](img/3148667e42d4db35b3d08576aaa1fa01_652_0.png)

# 使用命令的客户维护应用程序

在接下来的主题中，你将看到第 18 章首次介绍的客户维护应用程序的另一个版本。与该章节所示应用程序不同，此版本没有使用数据集和表适配器。相反，它使用命令从 Customers 表中检索、插入、更新和删除行。虽然这个介绍很冗长，但值得花时间仔细阅读，因为它将让你彻底理解如何使用命令构建应用程序。

## 用户界面

图 20-8 显示了客户维护应用程序的用户界面。如你所示，此应用程序由两个表组成。客户维护表允许用户选择现有客户并显示该客户的信息。然后，用户可以点击 Modify 按钮修改客户信息或点击 Delete 按钮删除客户。用户还可以点击 Add 按钮添加新客户。

如果用户点击 Add 或 Modify 按钮，将显示 Add/Modify Customer 表。此表的标题取决于是在添加还是修改客户。在这种情况下，正在修改在客户维护表中选中的用户。

在 Add/Modify Customer 表上输入适当的值后，用户可以点击 Accept 按钮或按 Enter 键接受新或修改的客户。或者，用户可以点击 Cancel 按钮或按 Esc 键取消操作。

如果用户点击 Delete 按钮，将显示如图所示的对话框以确认删除操作。然后，如果用户确认操作，客户将被删除，表单将被清空。

此时，你可能会疑惑为什么我使用两个表来实现客户维护应用程序。答案是，在现实世界中，大多数维护应用程序并不简单。在许多情况下，表的维护将与其他功能结合。事实上，即使维护是由单独应用程序提供的，使用两个表来实现应用程序可能会更容易，因为它简化了程序逻辑。

