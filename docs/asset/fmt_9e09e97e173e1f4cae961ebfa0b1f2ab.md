
| `DeleteCommand` | 此读/写属性设置或获取一个类型为 `SqlCommand` 的对象。此命令会自动执行以删除 SQL Server 中的现有记录。 |

`SqlDataAdapter` 类还提供了一个名为 `Fill()` 的方法。调用 `Fill()` 方法会自动执行由 `SelectCommand` 属性提供的命令，接收结果集并将其复制到 `DataTable` 对象中。

列表 8-9 中的代码示例说明了如何使用 `SqlDataAdapter` 类对象来填充 `DataTable` 对象。

# 列表 8-9：使用 SqlDataAdapter 对象填充 DataTable

```vb
<% Page Language="VB" %>
<% ImportNamespace=System.Data %>
<% ImportNamespace=System.Data.SqlClient %>
<% ImportNamespace=System.Configuration %>

<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
        If Not Page.IsPostBack Then
            Dim DataTable As DataTable = New DataTable()
            Dim Connection As SqlConnection = New SqlConnection()
            Connection.ConnectionString = ConfigurationManager.ConnectionString("DSN=Northwind").ConnectionString

            Dim MyCommand As SqlCommand = New SqlCommand()
            MyCommand.CommandText = "SELECT TOP 5 * FROM CUSTOMERS"
            MyCommand.CommandType = CommandType.Text
            MyCommand.Connection = Connection
            Dim MyDataAdapter As SqlDataAdapter = New SqlDataAdapter()
            MyDataAdapter.SelectCommand = MyCommand
            MyDataAdapter.Fill(DataTable)

            gvCustomers.DataSource = DataTable.DefaultView
            gvCustomers.DataBind()

            MyDataAdapter.Dispose()
            MyCommand.Dispose()
            Connection.Dispose()
        End If
    End Sub
</script>

<% Page Language="C#" %>
<% ImportNamespaces=System.Data %>
<% ImportNamespaces=System.Data.SqlClient %>
<% ImportNamespaces=System.Configuration %>
```

```csharp
MyAdapter.Fill(MyTable);
gvCustomers.DataSource = MyTable.DefaultView;
gvCustomers.DataBind();

MyAdapter.Dispose();
SqlCommand.Dispose();
MyConnection.Dispose();

<script>
```

列表 8-9 中的代码创建了一个 `Connection` 和 `Command` 对象，然后创建了一个 `SqlDataAdapter` 类的实例。它将 `DataAdapter` 对象的 `SelectCommand` 属性设置为之前创建的 `Command`。在 `DataAdapter` 准备好执行后，代码执行了 `Fill()` 方法，从而填充 `DataTable`。图 8-2 显示了执行此代码的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_381_0.png)

图 8-2

# 使用参数

大多数数据库编程，无论其多么简单，都需要你使用参数来配置 SQL 语句。使用参数可以防止可能的 SQL 注入攻击。显然，如果不考虑参数化语句的使用，那么对 ADO.NET 编程优势的讨论就是完整的。

创建参数非常简单，只需声明 `SqlParameter` 类的实例，并为其提供必要的信息，如名称、值、大小、方向等。表 8-6 显示了 `SqlParameter` 类的属性。

# 表 8-6

| 属性 (PROPERTY) | 说明 (DESCRIPTION) |

| --- | --- |

| ParameterName | 此读写属性设置或获取参数的名称。 |

| SqlDbType | 此读写属性设置或获取参数值的 SQL Server 数据库类型。 |

| Size | 此读写属性设置或获取参数值的大小。 |

| Direction | 此读写属性设置或获取参数的方向，例如：输入（Input）、输出（Output）或输入输出（InputOutput）。 |

# 基础 ADO.NET 特性

| 属性 (PROPERTY) | 说明 (DESCRIPTION) |

| --- | --- |

| SourceColumn | 此读写属性将 `DataTable` 中的列映射到参数。它允许你使用 `SqlDataAdapter` 对象执行多个命令，并在命令执行期间从 `DataTable` 列中选取正确的参数值。 |

| Value | 此读写属性设置或获取传递给参数对象的值。值在运行时传递给命令中定义的参数。 |

列表 8-10 修改了列表 8-5 显示的代码，以便在从数据库检索客户列表时使用两个参数。

# 列表 8-10：参数化 SQL 的使用

```vb
<%@ Language="VB" %>
<% ImportNamespace="System.Data" %>
<% ImportNamespace="System.Data.SqlClient" %>
<% ImportNamespace="System.Configuration" %>

<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
        If Not Page.IsPostBack Then
            Dim MyReader As SqlDataReader

            Dim CityParam As SqlParameter
            Dim ContactParam As SqlParameter

            Dim MyConnection As SqlConnection = New SqlConnection()
            MyConnection.ConnectionString = ConfigurationManager.ConnectionString("DSN=Northwind").ConnectionString
            Dim MyCommand As SqlCommand = New SqlCommand()
            MyCommand.CommandType = CommandType.Text
            MyCommand.CommandText = "SELECT * FROM CUSTOMERS WHERE CITY = @CITY AND CONTACTNAME = @CONTACT"
            MyCommand.Connection = MyConnection
            MyConnection.Open()

            Dim CityParam = New SqlParameter()
            CityParam.ParameterName = "@CITY"
            CityParam.DbType = SqlDbType.VarChar
            CityParam.Size = 15
            CityParam.Direction = ParameterDirection.Input
            CityParam.Value = "Berlin"

            Dim ContactParam = New SqlParameter()
            ContactParam.ParameterName = "@CONTACT"
            ContactParam.DbType = SqlDbType.VarChar
            ContactParam.Size = 15
            ContactParam.Direction = ParameterDirection.Input
            ContactParam.Value = "Maria Anders"

            MyCommand.Parameters.Add(CityParam)
            MyCommand.Parameters.Add(ContactParam)

            MyReader = MyCommand.ExecuteReader(CommandBehavior.CloseConnection)

            gvCustomers.DataSource = MyReader
            gvCustomers.DataBind()
        End If
        MyCommand.Dispose()
        MyConnection.Dispose()
    End Sub
</script>
```

```csharp
<%@ Page Language="C#" %>
<% Import Namespace="System.Data" %>
<% Import Namespace="System.Data.Client" %>
<% Import Namespace="System.Configuration" %>

<script runat="server">
protected void Page_Load(object sender, EventArgs e)
{
    if (!Page.IsPostBack)
    {
        SqlDataReader MyReader;
        SqlParameter CityParam;
        SqlParameter ContactParam;

        SqlConnection MyConnection = new SqlConnection();
        MyConnection.ConnectionString = ConfigurationManager.ConnectionStrings["DSN=Northwind"].ConnectionString;

        SqlCommand MyCommand = new SqlCommand();
        MyCommand.CommandText = "SELECT * FROM CUSTOMERS WHERE CITY = @CITY AND CONTACTNAME = @CONTACT";
        MyCommand.CommandType = CommandType.Text;
        MyCommand.Connection = MyConnection;

        SqlParameter CityParam = new SqlParameter();
        CityParam.ParameterName = "@CITY";
        CityParam.DbType = SqlDbType.VarChar;
        CityParam.Size = 15;
        CityParam.Direction = ParameterDirection.Input;
        CityParam.Value = "Berlin";

        SqlParameter ContactParam = new SqlParameter();
        ContactParam.ParameterName = "@CONTACT";
        ContactParam.DbType = SqlDbType.VarChar;
        ContactParam.Size = 15;
        ContactParam.Direction = ParameterDirection.Input;
        ContactParam.Value = "Maria Anders";

        MyCommand.Parameters.Add(CityParam);
        MyCommand.Parameters.Add(ContactParam);

        MyConnection.Open();
        MyReader = MyCommand.ExecuteReader(CommandBehavior.CloseConnection);
        gvCustomers.DataSource = MyReader;
        gvCustomers.DataBind();

        MyCommand.Dispose();
        MyConnection.Dispose();
    }
}
</script>
```

列表 8-8 显示的代码使用了参数化 SQL 语句，接收城市名称和联系人以缩小结果集。这些参数通过实例化 `SqlParameter` 类的实例并为每个 `SqlParameter` 对象填充适当的名称、类型、大小、方向和值提供的。从那里，通过调用 `Parameters` 集合的 `Add()` 方法将填充的参数添加到 `Command` 对象中。图 8-3 显示了执行此代码的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_384_0.png)

图 8-3

# 理解 DataSet 和 DataTable

大多数程序员在真实世界的数据库驱动应用程序中将 `DataSet` 作为最常用的 ADO.NET 工具。该类提供了在我们脱离数据源时管理数据的机制。这种处理离线状态下数据的能力是在 .NET 的 ADO.NET 1.0 版本中引入的。当 ADO.NET 3.5 版本 发布时，它增强了所有功能并提供了一些新的、急需的功能。你也将在 .NET Framework 4 中找到这些功能。

从 `DataSet` 创建的对象作为从 `DataTable` 创建的其他对象的容器。`DataTable` 代表内存中的一个逻辑表。它包含行、列、主键以及与其他 `DataTable` 的关系。因此，你可以拥有一个由两个不同表（如 `Customers` 表和 `Orders` 表）组成的 `DataSet`。你可以像使用任何其他数据源一样使用 `DataSet` 来管理两个表之间的关系，以便显示特定客户的所有表。

当实际上使用 `DataSet` 中的一个或多个 `DataTable` 对象处理离线数据时，之前的 ADO.NET 版本并不允许你直接对 `DataTable` 执行某些非常重要的任务，例如从 XML 文件读取和写入数据。它甚至不允许独立于更大且包含它的 `DataSet` 对象之外地对 `DataSet` 对象进行序列化。这种限制要求你始终使用 `DataSet` 来对 `DataTable` 执行任何操作。当前的 ADO.NET 版本消除了这一限制，允许你直接通过 `DataTable` 处理你的所有需求。事实上，我们建议除非你需要处理多个对象以及容器对象来管理它们，否则不要使用 `DataSet`。如果你只处理单个表的信息，那么使用 `DataTable` 对象的实例比只包含单个 `DataTable` 的 `DataSet` 更好。

当前的 ADO.NET 提供了一种通过使用 `DataReader` 消耗数据源并在内存中加载 `DataTable` 的能力。过去，你被限制为创建相同方法的副本来同时处理 `DataReader` 和 `DataTable` 对象。现在你有了

# 326 | 第 8 章 使用 ADO.NET 进行数据管理

灵活编写一次访问代码并重复使用 DataReader——无论是直接使用还是填充 DataTable，如列表 8-11 所示。

# 列表 8-1: 如何从 DataReader 加载 DataTable
