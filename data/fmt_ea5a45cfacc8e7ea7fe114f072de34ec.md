
> **NOTE**  
> 你需要根据计算机配置修改 `ConnectionString` 属性的值。你需要在 `Form1.cs` 文件中添加 `System.Data.SqlClient` 命名空间。

当你按 F5 键执行代码时，你会发现 `combobox1` 中有值。这些值是 `Employee` 表的 `EmployeeID` 字段值。清单 24.5 中代码的输出如图所示 24.45：

![](img/e073a4882197be4ab61103cbe0bcb394_1203_0.png)

图 24.45：使用命令对象在组合框中检索数据

## 使用 `DataAdapters`

`DataAdapters` 是一组用于在数据源和 `DataSet` 之间交换数据的对象。这意味着 `DataAdapter` 负责从数据库读取数据到 `DataSet`，并将 `DataSet` 中更改的数据写回数据库。.NET Framework 中可用的 `DataAdapters` 如下：

- `OleDbDataAdapter` — 允许你使用 OLE DB 提供程序公开的任何数据源工作
- `SqlDataAdapter` — 仅适用于 SQL Server
- `OdbcDataAdapter` — 允许你访问 ODBC 数据源
- `OracleDataAdapter` — 与 Oracle 数据库一起工作

现在问题出现了，我们如何在应用程序中使用 `DataAdapter`。让我们在下面的示例中尝试回答这个问题。

## 从 `DataAdapter` 创建 `DataSet`

`DataSet` 是包含数据表以便临时存储数据的对象。`DataSet` 不依赖于数据源，与现有数据源的交互通过 `DataAdapter` 控制。你可以使用 `DataAdapter` 加载 `DataSet`。`DataAdapter` 的 `SelectCommand` 属性是一个从数据源检索数据的命令对象。你还可以使用 `DataAdapter` 的 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 属性来管理数据源中数据的任何更新。你可以使用 `DataAdapter` 的 `Fill()` 方法将使用 `SelectCommand` 检索的数据加载到 `DataSet` 中。让我们创建一个名为 DataSet from DataAdapters 的应用程序（可在 CD-ROM 上获得），以从 `DataAdapter` 创建 `DataSet`。添加一个按钮控件和一个 `DataGridView` 控件，并将按钮控件的 `Text` 属性更改为 Generate Data。现在，在按钮控件的 `Click` 事件上添加如清单 24.6 所示的代码：

### 清单 24.6：显示按钮控件 `Click` 事件的代码

```
private void button1_Click(object sender, EventArgs e)
{
    SqlConnection connection = new SqlConnection();
    connection.ConnectionString = "Data Source=umar-pc;Initial Catalog=Northwind;Integrated Security=True";
    connection.Open();
    SqlDataAdapter adp = new SqlDataAdapter("select * from Orders", connection);
    DataSet ds = new DataSet();
    adp.Fill(ds);
    dataGridView1.DataSource = ds.Tables[0];
}
```

> **NOTE**  
> 你需要根据计算机配置修改 `ConnectionString` 属性的值。你需要在 `Form1.cs` 文件中添加 `System.Data.SqlClient` 命名空间。

数据从 `Northwind` 数据库的 `Orders` 表生成。当你按 F5 运行代码并单击 Generate Data 按钮时，你可以看到输出，如图 24.46 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1204_0.png)

图 24.46：单击按钮生成数据

## 使用 `DataAdapters` 进行分页

ADO.NET 中的分页是按查询结果的较小数据子集或更具体地说是页面返回结果的过程。您可以使用此做法以小而易于管理的块显示结果。`DataAdapter` 提供了返回仅一页数据的功能。`DataAdapter` 只用请求的记录填充 `DataSet`。您需要使用 `startRecord` 参数返回数据页中的第一条记录，并使用 `maxRecords` 参数指定数据页中的记录数。让我们创建一个名为 `PagingData` 的应用程序（可在 CD-ROM 上获得），在其中您可以使用 `DataAdapters` 对数据进行分页。添加一个 `Button` 控件和一个 `DataGridView` 控件，并将 `Button` 控件的 `Text` 属性更改为 Load Page。现在，在 `Button` 控件的 `Click` 事件上添加代码，如清单 24.7 所示：

### 清单 24.7：显示 `Button` 控件的 `Click` 事件的代码

```
private void button1_Click(object sender, EventArgs e)
{
    int pageSize = 5;
    SqlConnection connection = new SqlConnection();
    connection.ConnectionString = "Data Source=umar-pc;Initial Catalog=Northwind;Integrated Security=True";
    connection.Open();
    string ordersSQL = "SELECT TOP " + pageSize + " * FROM Orders ORDER BY OrderID";
    SqlDataAdapter adapter = new SqlDataAdapter(ordersSQL, connection);
    DataSet DataSet = new DataSet();
    adapter.Fill(DataSet, "Orders");
    dataGridView1.DataSource = DataSet.Tables["Orders"];
}
```

当您运行应用程序并单击 Load Page 按钮时，您可以看到仅加载了 `Order` 表的五条记录。`pageSize` 变量指定要加载到 `DataGridView` 控件的数据量。单击 Load Page 按钮后应用程序的输出如图所示 24.47：

![](img/e073a4882197be4ab61103cbe0bcb394_1205_0.png)

图 24.47：设置 `DataGridView` 控件的页面大小后显示的数据

## 使用 `DataAdapters` 更新

您可以使用 `DataAdapter` 更新数据源。`DataAdapter` 的 `Update()` 方法用于将 `DataSet` 中的更改解析回数据源。当您调用 `Update()` 方法时，`DataAdapter` 会分析所做的更改并执行命令。当 `DataAdapter` 遇到 `DataRow` 的更改时，它会使用 `UpdateCommand` 处理该更改。您必须注意，`Update()` 方法是按行执行的。当应用程序调用 `Update()` 方法时，`DataAdapter` 会检查 `RowState` 属性并为每一行执行所需的 `INSERT`、`UPDATE` 或 `DELETE` 语句。让我们创建一个名为 `UpdatingData` 的应用程序（可在 CD-ROM 上获得），在其中您可以使用 `DataAdapter` 更新数据。为此，您首先需要在 `Form1` 上添加一个 `Button` 和一个 `DataGridView` 控件。之后，您需要将 `Button` 的文本属性更改为 Update Data，并通过向导将项目数据源添加到 `DataGridView` 控件，如本章“创建数据库连接”一节所示。添加数据源后，在 `Button` 控件的 `Click` 事件上添加代码，如清单 24.8 所示：

### 清单 24.8：显示 `Button` 控件的 `Click` 事件的代码

```
private void button1_Click(object sender, EventArgs e)
{
    employeesTableAdapter.Update(northwindDataSet);
}
```

正如您已经学到的那样，`employeesTableAdapter` 和 `northwindDataSet` 是在您通过向导创建数据源连接时自动生成的。

当您运行应用程序时，原始表会生成在 `DataGridView` 控件中。您可以在应用程序运行时在 `DataGridView` 控件中添加全新的行，然后单击 Update Data 按钮。新的数据将添加到 `DataGridView` 控件和数据源中。按 F5 后 `Form1` 的输出如图所示 24.48：

![](img/e073a4882197be4ab61103cbe0bcb394_1206_0.png)

图 24.48：运行时更新数据

## 向 `DataSet` 添加多个表

单个 `DataSet` 可以包含多个表。您需要创建一个单一的 `DataSet` 并将其中的不同表添加到应用程序中的不同 `DataGridView` 控件中。让我们创建一个名为 `MultiTable` 的应用程序（可在 CD-ROM 上获得），在其中您可以使用单个 `DataSet` 向应用程序添加多个表。现在，向 `Form1` 添加两个 `DataGridView` 控件和两个标签。之后，将两个 `Label` 控件的文本分别更改为 Order Details Table 和 Orders Table，并将代码如清单 24.9 所示添加到 `Form1` 的 `Load` 事件中：

### 清单 24.9：显示 `Form1` 的 `Load` 事件的代码

```
private void Form1_Load(object sender, EventArgs e)
{
    SqlConnection connection = new SqlConnection();
    connection.ConnectionString = "Data Source=umar-pc;Initial Catalog=Northwind;Integrated Security=True";
    connection.Open();
    DataSet ds = new DataSet();
    SqlDataAdapter dap = new SqlDataAdapter("select * from [Order Details]", connection);
    dap.Fill(ds, "[Order Details]");
    dataGridView1.DataSource = ds.Tables["[Order Details]"];
    SqlDataAdapter dap1 = new SqlDataAdapter("select * from Orders", connection);
    dap1.Fill(ds, "Orders");
    dataGridView2.DataSource = ds.Tables["Orders"];
}
```

> **NOTE**  
> 您需要根据计算机配置修改 `ConnectionString` 属性的值。您需要在 `Form1.cs` 文件中添加 `System.Data.SqlClient` 命名空间。

您可以通过首先创建连接来使用单个 `DataSet` 显示多个表。之后，您需要在应用程序中添加一个名为 `ds` 的 `DataSet`。此外，您需要为第一个 `DataGridView` 控件 `dataGridView1` 创建名为 `dap` 的 `SqlDataAdapter`，然后为第二个 `DataGridView` 控件 `dataGridView2` 创建另一个名为 `dap1` 的 `SqlDataAdapter`。您会注意到单个 `DataSet` 用于在两个 `DataGridView` 控件中填充不同的数据。当您运行应用程序时，您可以看到输出，如图所示 24.49：

![](img/e073a4882197be4ab61103cbe0bcb394_1207_0.png)

图 24.49：显示多个表

## 创建 `DataView`

您可以使用 `DataView` 获取表中数据的快照并对其进行操作。`DataView` 与只读迷你 `DataSets` 相同；您通常只将 `DataSet` 的子集加载到数据视图中。`DataView` 提供数据的动态视图。它根据特定筛选器或排序顺序从表中提供 `DataRow` 数组。您可以使用 `DataView` 应用不同的排序和筛选条件。让我们创建一个名为 `DataViews` 的应用程序（可在 CD-ROM 上获得），在其中您可以对数据进行排序和查看。添加两个 `Button` 和一个 `DataGridView` 控件，并将 `button1` 和 `button2` 控件的 `Text` 属性分别更改为 Sort by City 和 Only in Mexico。现在，将代码如清单 24.10 所示添加到 `Form1.cs` 文件中：

### 清单 24.10：显示 `Form1.cs` 文件的代码

```
using System;
using System.Collections.Generic;
```

根据清单 24.10，当您运行应用程序时，数据会检索到 `DataGridView` 控件中。应用程序的初始输出如图所示 24.50：

![](img/e073a4882197be4ab61103cbe0bcb394_1209_0.png)

图 24.50：显示应用程序的初始输出

单击 `Sort by City` 按钮，您可以根据 `city` 字段按升序对 `DataGridView` 控件的数据进行排序。单击 `Sort by City` 按钮后的输出如图所示 24.51：

![](img/e073a4882197be4ab61103cbe0bcb394_1209_1.png)

图 24.51：显示排序后的数据

单击 `Only in Mexico` 按钮，您可以筛选数据并仅显示 `City` 字段包含 Mexico 的记录。单击 `Only in Mexico` 按钮后的输出如图所示 24.52：

![](img/e073a4882197be4ab61103cbe0bcb394_1209_2.png)

图 24.52：显示筛选后的数据

## 使用 `DataReader` 工作与数据库

您可以通过使用 `DataReader` 而不是 `DataAdapter` 在 Windows 应用程序中检索数据。您可以使用 `ExecuteReader` 从数据源检索行。`DataReader` 的 `Read()` 方法用于从数据源获取一行。不同数据源有不同的 `DataReaders`。例如，`OleDbDataReader` 提供从 OLE DB 数据提供程序读取仅向前的数据行流的方式。`SqlDataReader` 提供从 SQL Server 数据源读取仅向前的数据行流的方式。让我们创建一个名为 `UsingDataReader` 的应用程序（可在 CD-ROM 上获得），在其中您可以使用 `DataReader` 从数据源检索数据。为此，您首先需要在 `Form1` 上添加 `Button`、`Label`、`TextBox` 和 `ListBox` 控件。添加控件到 `Form1` 后，将 `Label` 控件的 `Text` 属性更改为 Enter Text to Find，并将 `Button` 控件的 `Text` 属性更改为 FIND。

现在，在 `Button` 控件的 `Click` 事件上添加代码，如清单 24.11 所示：

### 清单 24.11：显示 `Button` 控件的 `Click` 事件的代码

```
private void button1_Click(object sender, EventArgs e)
{
    SqlDataReader rdr = null;
    SqlConnection con = null;
    SqlCommand cmd = null;
    try
    {
        string ConnectionString = "Data Source=umar-pc;Initial Catalog=Northwind;Integrated Security=True";
        con = new SqlConnection(ConnectionString);
        con.Open();
        string CommandText = "SELECT FirstName, LastName" + " FROM Employees" + " WHERE (LastName LIKE @Find)";
        cmd = new SqlCommand(CommandText);
        cmd.Connection = con;
        cmd.Parameters.Add(new SqlParameter("@Find", System.Data.SqlDbType.Nvarchar, 20, "LastName"));
        cmd.Parameters["@Find"].Value = textBox1.Text;
        rdr = cmd.ExecuteReader();
        listBox1.Items.Clear();
        while (rdr.Read())
        {
            listBox1.Items.Add(rdr["FirstName"].ToString() + " " + rdr["LastName"].ToString());
        }
    }
    catch (Exception ex)
    {
```

