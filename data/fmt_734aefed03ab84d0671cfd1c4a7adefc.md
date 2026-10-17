
在 ODBC 连接字符串中，`Dsn` 是存储你数据源信息的唯一参数。

# 创建与数据库的连接

你需要连接到你想要操作的数据库。在 `Visual C#` 中，你可以通过两种方式创建连接。你可以通过 `Server Explorer` 或 `code-behind file` 创建数据库连接。正如你在“深入”部分所学到的，`ADO.NET` 提供了对 `SQL Server`、`OLEDB` 和 `XML` 等数据源的。然而，不同类型的数据源需要不同的连接。在接下来的章节中，你将通过两种方法学习连接到 `ADONET` 支持的所有类型数据库。

我们将显示来自 `Northwind` 示例数据库中 `Customers` 表格的数据。因此，我们需要连接到 `Northwind` 示例数据库。

## SQL Server 数据库

在 `.NET 4.5` 中，你可以通过两种方式连接到 `SQL Server` 数据库：向导或后代码文件。让我们创建一个名为 `SQLDatabase` 的 `Forms` 应用程序，在其中你可以通过两种方式从 `SQL Server` 获取数据。从 `SQL Server` 执行数据检索：

1. 从工具箱向表单添加一个按钮 `Button` 和两个 `DataGridView` 控件，如图 19.9 所示：

![](img/17af790174c480761404624aeed9b30b_938_0.png)

2. 在属性窗口将按钮控件的 `Text` 属性更改为 `Generate Data`（生成数据），如图 19.9 所示。
在第一个网格中，我们通过向导生成数据，在第二个网格中，我们在点击按钮时通过代码生成数据。让我们先通过以下步骤通过向导生成 `dataGridView` 控件：

1. 选择 `dataGridView` 控件并点击智能标签 `Smart Tag`。
2. 在 `dataGridView` 控件智能标签的 `Choose Data Source` 下拉列表中选择 `Add Project Source`（添加项目源）选项，如图 19.10 所示：

![](img/17af790174c480761404624aeed9b30b_939_0.png)

这将打开数据源配置向导（图 19.11）。
选择 `Database`（数据库）作为数据源类型并点击 `Next`（下一步）按钮，如图 19.11 所示：

![](img/17af790174c480761404624aeed9b30b_939_1.png)

出现 `Choose a Database Model`（选择数据库模型）页面（图 19.12）。

4. 在 `Choose a Database Model` 页面选择 `Dataset`（数据集）作为数据库模型（图 19.12）。
5. 点击 `Next`（下一步）按钮，如图 19.12 中的配置所示：

![](img/17af790174c480761404624aeed9b30b_940_0.png)

出现 `Choose your Data Connection`（选择你的数据连接）页面（图 19.13）。

6. 在 `Choose Your Data Connection` 页面点击 `New`（新建）按钮，如图 19.13 所示：

![](img/17af790174c480761404624aeed9b30b_940_1.png)

这将打开 `Add Connection`（添加连接）框。

7. 按照本章“创建连接字符串”部分的说明创建连接字符串。
创建连接字符串后，注意下拉列表中显示了数据库路径（图 19.14）。

8. 点击 `Next`（下一步）按钮，如图 19.14 所示：

![](img/17af790174c480761404624aeed9b30b_941_0.png)

图 19.14：显示数据连接

出现 `Save Connection String to the Application Configuration File`（将连接字符串保存到应用程序配置文件）页面（图 19.15）。
9. 取消选择 `Yes`，勾选 `save the connection as:` 复选框并点击 `Next`（下一步）按钮，如图 19.15 所示：

![](img/17af790174c480761404624aeed9b30b_941_1.png)

图 19.15：保存连接字符串

出现 `Choose Your Database Objects`（选择你的数据库对象）页面（图 19.16）。
10. 在 `DataGridView` 控件中选择你想要显示的表。在我们的案例中，我们选择了 `Customers` 表格（图 19.16）。

11. 点击 `Finish`（完成）按钮，如图 19.16 所示：

![](img/17af790174c480761404624aeed9b30b_942_0.png)

图 19.16：选择数据库对象

数据源配置向导关闭，你回到 Windows 表单。在 Windows 表单中，`dataGridView` 控件现在绑定到了 `Customers` 表格。

你可以看到 `customersBindingSource` 和 `customersTableadapter` 被自动添加了。你可以在运行程序之前预览数据。

12. 从 `dataGridView` 控件的智能标签中选择 `Preview Data`（预览数据）选项。这将打开 `Preview Data` 框（图 19.17）。
13. 点击 `Preview Data`，数据显示在图 19.17 中：

![](img/17af790174c480761404624aeed9b30b_942.png)

| CustomerID | CompanyName | ContactName | City | Region |
|---|---|---|---|---|
| ALFKI | Aquatic | Ana Anders | Seattle | WA |
| ANVTA | Antonio | Ana Anders | | | |

图 19.17：数据的预览

第 9 章：使用 ADO.NET 访问数据

这是在 `DataView` 控件中访问数据的简单方便的方法。现在，让我们通过后代码访问数据。为此，为我们添加的按钮生成点击事件。现在添加列表 19.1 所示的代码：

**列表 19.1：用于点击事件**

```csharp
private void button1_Click(object sender, EventArgs e)
{
    SqlConnection connection = new SqlConnection();
    connection.ConnectionString = "Data Source=pc\sqlserver;Initial Catalog=Network;Integrated Security=True";
    connection.Open();
    SqlDataAdapter adapter = new SqlDataAdapter("select * from Customers", connection);
    DataSet ds = new DataSet();
    adapter.Fill(ds);
    dataGridView1.datasource = ds.Tables[0];
}
```

> 注意
你需要根据系统更改代码中的连接字符串。你还需要在 `Form1.cs` 中添加 `System` 和 `System.Data` 命名空间。

现在，按 `F5` 键运行应用程序。点击按钮后的应用程序输出如图 19:18 所示。

![](img/17af790174c480761404624aeed9b30b_943_0.png)

图 19:18：`DataGridView` 控件中的数据

## OLEDDB 数据库

是微软设计的应用程序编程接口 `API`，用于访问存储在不同格式中的类型类型。你可以通过 `OLEDB`、`SQL Server` 甚至 `Access` 文件访问 `Access` 数据库。我们通过后代码两种方式访问 `Access` 数据库。在 `.NET 4.5` 中，你可以访问。让我们创建一个名为 `OLEDBDatabase` 的 Windows 应用程序，在其中你可以通过两种方式从 `Access` 文件获取数据。

1. 如我们在上一节所示，向 `Form1` 添加一个按钮和两个 `DataGridView` 控件。
2. 选择 `dataGridView` 控件并点击智能标签以选择 `dataGridView` 控件的内容。

4. 选择“数据库”作为数据源类型，并点击“下一步”按钮打开“选择数据库模型”页面。

5. 在“选择数据库模型”页面中选择“数据集”作为数据库模型，并点击“下一步”按钮打开“选择数据连接”页面。

6. 在“选择数据连接”页面中点击“新建连接”按钮。这将打开“添加连接”对话框（图 19.19）。

7. 点击“添加连接”对话框上的“更改”按钮，如图 19.19 所示。

![](img/17af790174c480761404624aeed9b30b_944_0.png)

图 19.19：添加连接对话框（图 19.20）。

出现“更改源”对话框。选择“文件”数据源并点击“确定”按钮，如图 19.20 所示：

8. 选择“Microsoft Access数据库文件”数据源并点击“确定”按钮，

![](img/17af790174c480761404624aeed9b30b_944_1.png)

图 19.20：选择数据源

选择数据源后，出现“添加连接”对话框（图 19.21）。

![](img/17af790174c480761404624aeed9b30b_944_2.png)

图 19.21：显示添加连接对话框

# 第 19 章：使用 ADO.NET 进行数据访问

9. 在“选择 Microsoft Access数据库”对话框中点击“浏览”按钮 (19.21)，浏览 Access 数据库文件的位置，并点击“打开”按钮（图 19.22）。

10. 选择一个 Access 数据库并点击“打开”按钮。在我们案例，我们选择了 `Northwind` 数据库，如图 19.22 所示：

![](img/17af790174c480761404624aeed9b30b_945_0.png)

图 19.22：选择 Access 数据库文件对话框

11. 点击“测试”按钮访问你创建的 Access 数据库连接。当你点击“测试连接”时，会弹出一个消息框显示消息“测试连接成功”（图 19.23）。

12. 点击“添加连接”对话框的“确定”按钮关闭对话框，如图 19.23 所示：

13. 点击“添加连接”对话框的“确定”按钮关闭对话框。

![](img/17af790174c480761404624aeed9b30b_945_1.png)

图 19.23：测试连接

你被重定向到“数据源配置向导”。注意，数据库的路径显示在下拉列表中（图 19.24）。

14. 点击**下一步**按钮，如图 19.24 所示：

![](img/17af790174c480761404624aeed9b30b_946_0.png)

**图 19.24：数据连接**

出现一个消息，要求将数据库的本地文件复制到你的应用程序（图 19.25）。

15. 点击**是**按钮将数据文件复制到你的应用程序，如图 19.25 所示：

![](img/17af790174c480761404624aeed9b30b_946_1.png)

**图 19.25：消息框**

这将你重定向到“将连接字符串保存到应用程序配置”页面（图 19.26）。

![](img/17af790174c480761404624aeed9b30b_946_2.png)

**图 19.26：保存连接字符串**

907

# 第 19 章：使用 ADO.NET 进行数据访问

出现“选择你的数据库对象”页面 (19.27)。

17. 在 `DataGridView` 控制中选择你想显示的表。在我们案例中，我们选择了 `Employees` 表（图 19.27）。

18. 点击“完成”按钮，如图 19.27 所示：

![](img/17af790174c480761404624aeed9b30b_947_0.png)

源配置向导已关闭。

一旦完成，你将回到你的表单，此时 `dataGridView` 控制现在已绑定到 `Employees` 表。`employeesBindingSource` 和 `employeesTableDataAdapter` 会自动添加到应用程序中。你可以在运行程序之前预览数据。

- 1. 从 `dataGridView` 控制的智能标记 `Smart Tag` 中选择“预览”选项。这将打开“预览数据”对话框（图 19.28）。
- 2. 点击“预览”按钮，数据将显示在结果部分，如图 19.28 所示：

![](img/17af790174c480761404624aeed9b30b_947_1.png)

## 立即解决方案

通过这种方式，你可以查看 `DataGridView` 控制中 `Access` 数据库的内容。同样地，你可以通过后台代码在已添加的第二个 `DataGridView` 控制中检索数据库的内容。此代码见列表 19.2，位于按钮点击事件：

列表 19.2：按钮点击代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    OleDbConnection connection = new OleDbConnection(
        "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\CSharp 2012 Black Book\Northwind.accdb");
    OleDataAdapter adapter = new OleDataAdapter("select * from Employees", connection);
    DataSet ds = new DataSet();
    adapter.Fill(ds);
    dataGridView2.DataSource = ds;
}
```

你需要更改代码中的连接字符串以匹配你的系统。你还需要需要在 `Form1.cs` 中添加 `System.OleDb` 命名空间。

数据的输出所示图 19.2：

![](img/17af790174c480761404624aeed9b30b_948_0.png)

| ID | LastName | FirstName |
| :--- | :--- | :--- |
| 1 | Davolio | Nancy |
| 2 | Fuller | James |
| 3 | Leveling | Janet |
| 4 | Peacock | Margaret |
| 5 | Buchanan | Steven |
| 6 | Suazman | Michael |
| 7 | Price | Anna |
| 8 | Callahan | Laura |
| 9 | Dodworth | Anne |

图 19.2：在 `DataGridView` 控制中访问数据

## ODBC 数据源

如前，`OLE DB` 可访问其他类型的数据源，例如 `Excel` 文件。你可以使用 `OLE DB` 将 `Excel` 文件的数据检索到 `DataGridView` 控制。通过以下步骤创建一个在 `DataGridView` 控制中检索 `Excel` 文件数据的示例：

- 1. 在 `Visual 2012` 中创建一个 Windows Form。
- 2. 向表单添加 `DataGridView` 控制和按钮。
- 3. 将按钮控件的文本更改为“查看数据”。

当你点击按钮时，会检索 `DataGridView` 控制中的数据。使用的是我们创建并输入数据的 `Excel` 文件。`Excel` 文件具有 `Emp_ID`、`Emp_Name`、`Emp_Number`、`Emp_Address` 和 `Emp_Salary` 列。`Excel` 文件的表已重命名为 `Contacts`。在这些列下输入数据后，我们将 `Excel` 文件保存为名为 `book1.xls` 文件，位于 `D:\CSharp 2012 Black Book\Chapter 19` 位置。在创建连接字符串时，你需要提供 `Excel` 文件的正确路径。

# 第 19 章：使用 ADO.NET 进行数据访问

4. 将列表 19.3 所示的代码添加到按钮的点击事件中：

列表 19.3：按钮点击事件代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    string connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +
        "D:\CSharp 2012 Black Book\Excel 19-book1.xlsx" + "Excel=12.0;HDR=YES;";
    OleDbConnection connection = new OleDbConnection(connectionString);
    OleDbDataAdapter ad = new OleDbDataAdapter("SELECT * FROM [Customers]", connection);
    DataTable dt = new DataTable();
    ad.Fill(dt);
    dataGridView1.DataSource = dt;
}
```
