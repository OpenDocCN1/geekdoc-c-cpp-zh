

## 直接访问数据库的 ADO.NET 组件

![](img/c024ccf88e28c30c07dd410d4342288f_416_0.png)

**描述**

- 而不是使用数据适配器执行命令从数据库检索、插入、更新和删除数据，你可以直接执行这些命令。
- 要从数据库检索数据，你执行包含 Select 语句的命令对象。然后，命令对象使用连接连接到数据库并检索数据。你可以使用 *数据读取器* 对象逐行读取结果。
- 要在数据库中插入、更新或删除数据，你执行包含 Insert、Update 或 Delete 语句的命令对象。然后，命令对象使用连接连接到数据库并更新数据。然后你可以检查返回的值以确定操作是否成功。
- 如果你在维护数据库中数据的应用程序中使用此技术，你通常一次只处理一行数据。因此，并发错误的可能性降低了。

*图 12-10 如何在不使用数据适配器的情况下处理数据*

## ADO.NET 4 类简介

下面介绍的主题将介绍一些主要的 ADO.NET 4 类。当你使用下一章中描述的 SQL 数据源时，你不会直接使用这些类。相反，它们在幕后使用。

### SqlConnection 类

在你能够访问数据库中的数据之前，你必须创建一个定义数据库连接的连接对象。为此，你使用图 12-11 中介绍的 SqlConnection 类。

此类最重要的属性是 ConnectionString。连接字符串是一个提供连接数据库所需信息的字符串。这意味着它包括诸如数据库名称和数据库服务器之类的信息。它还可以包含身份验证信息，例如用户 ID 和密码。

图中所显示的此类两个方法可让你打开和关闭连接。一般来说，你应该仅在检索或更新数据时保持连接打开。当你使用数据适配器时，连接会为你打开和关闭，因此你不需要使用这些方法。

### SqlCommand 类

要对 SQL Server 数据库执行 SQL 语句，你创建一个包含该语句的 SqlCommand 对象。图 12-11 展示了你用来创建此对象的 SqlCommand 类。请注意，此类的 Connection 属性将命令与 SqlConnection 对象关联起来，而 CommandText 属性包含要执行的 SQL 语句。

CommandType 属性指示命令对象应如何解释 CommandText 属性的值。例如，除了为 CommandText 属性指定 SQL 语句外，你还可以指定存储过程的名称，该名称由一个或多个已编译并与数据库一起存储的 SQL 语句组成。

本章前面你了解到可以使用数据适配器执行命令对象。此外，你还可以通过使用图中所显示的三个 Execute 方法直接执行命令对象。例如，如果你对 Select 语句使用 ExecuteReader，结果将作为 DataReader 对象返回。如果使用 ExecuteScalar，则只返回查询结果的第一列和第一行的值。

如果命令包含 Insert、Update 或 Delete 语句，你将使用 ExecuteNonQuery 方法执行它。此方法返回一个整数值，表示受命令影响的行数。例如，如果命令删除单行，ExecuteNonQuery 方法返回 1。

**SqlConnection 类的常用成员**

| 属性 | 描述 |
| --- | --- |
| ConnectionString | 包含让你连接到 SQL Server 数据库的信息，包括服务器名称、数据库名称和登录信息。 |

| 方法 | 描述 |
| --- | --- |
| Open | 打开到数据库的连接。 |
| Close | 关闭到数据库的连接。 |

**SqlCommand 类的常用成员**

| 属性 | 描述 |
| --- | --- |
| Connection | 用于连接到数据库的 SqlConnection 对象。 |
| CommandText | SQL 语句的文本或存储过程的名称。 |
| CommandType | CommandType 枚举中的一个常量，指示 CommandText 属性是否包含 SQL 语句（Text）或存储过程的名称（StoredProcedure）。 |
| Parameters | 命令使用的参数集合。 |

| 方法 | 描述 |
| --- | --- |
| ExecuteReader | 执行查询并以 SqlDataReader 对象形式返回结果。 |
| ExecuteNonQuery | 执行命令并返回表示受影响行数的整数。 |
| ExecuteScalar | 执行查询并返回查询返回的第一行的第一列。 |

**SqlParameter 类的常用成员**

| 属性 | 描述 |
| --- | --- |
| ParameterName | 参数的名称。 |
| Value | 分配给参数的值。 |
| SqlDbType | 参数的 SQL 数据类型。 |

**描述**

- 需要 SqlConnection 对象来建立与 SQL Server 数据库的连接。
- SqlCommand 对象用于对 SQL Server 数据库执行 SQL 命令。
- SqlParameter 对象用于将变量信息传递给 SQL 命令。

### SqlParameter 类

SqlParameter 类也在图 12-11 中显示，可让你将参数值传递给 SQL 命令。参数通常用于限制 Select 语句检索的行数。例如，你可以通过将 ProductID 作为参数传递来检索特定产品的 Product 行。或者，你可以通过将 CategoryID 作为参数传递来检索给定类别的所有产品。参数也常用于将列值传递给 Insert、Update 和 Delete 语句。

### SqlDataReader 类

图 12-12 列出了 SqlDataReader 类最重要的成员。你使用此类创建数据读取器对象，它提供了一种高效的方式来读取数据库查询返回的结果集中的行。事实上，当你使用数据适配器检索数据时，数据适配器使用数据读取器读取结果集中的行并将它们存储在数据集中。

### SqlDataAdapter 类

正如你所学，数据适配器的任务是提供数据库和数据集之间的链接。例如，图 12-12 中列出的 SqlDataAdapter 类的四个属性标识数据适配器用于将数据从数据库传输到数据集以及反之的四个 SQL 命令。SelectCommand 属性标识用于从数据库检索数据的命令对象。而 DeleteCommand、InsertCommand 和 UpdateCommand 属性标识用于根据对数据集中的数据所做的更改来更新数据库的命令。

要执行 SelectCommand 属性标识的命令并将检索到的数据放入数据集中，你使用 Fill 方法。然后，应用程序可以在不影响数据库中的数据的情况下处理数据集中的数据。如果应用程序对数据集中的数据进行了更改，它可以使用数据适配器的 Update 方法执行 DeleteCommand、InsertCommand 和 UpdateCommand 属性标识的命令并将更改发布回数据库。

**SqlDataReader 类的常用成员**

| 索引器 | 描述 |
| --- | --- |
| `[index]` | 从当前行访问指定索引的列。 |
| `[name]` | 从当前行访问指定名称的列。 |

| 属性 | 描述 |
| --- | --- |
| `IsClosed` | 获取一个布尔值，指示数据读取器是否已关闭。 |

| 方法 | 描述 |
| --- | --- |
| `Read` | 读取下一行。如果还有更多行则返回 True。否则返回 False。 |
| `Close` | 关闭数据读取器。 |

**SqlDataAdapter 类的常用成员**

| 属性 | 描述 |
| --- | --- |
| `SelectCommand` | 表示用于查询数据库的 Select 语句的 SqlCommand 对象。 |
| `DeleteCommand` | 表示用于从数据库删除行的 Delete 语句的 SqlCommand 对象。 |
| `InsertCommand` | 表示用于向数据库添加行的 Insert 语句的 SqlCommand 对象。 |
| `UpdateCommand` | 表示用于更新数据库中行的 Update 语句的 SqlCommand 对象。 |

| 方法 | 描述 |
| --- | --- |
| `Fill` | 执行 SelectCommand 属性标识的命令并将结果加载到数据集对象中。 |
| `Update` | 对数据集中被删除、添加或更新的每一行执行 DeleteCommand、InsertCommand 和 UpdateCommand 属性标识的命令。 |

**描述**

- 数据读取器提供对数据库中数据的只读、只进访问。由于它不需要数据集的开销，因此比使用数据适配器更高效。然而，它不能用于更新数据。
- 当数据适配器的 Fill 方法用于从数据库检索数据时，数据适配器使用数据读取器将结果加载到数据集中。

![](img/c024ccf88e28c30c07dd410d4342288f_420_0.png)

