

这样，你就可以在 DataGridView 控件中查看 Access 数据库的内容。同样地，你也可以通过代码隐藏文件检索数据库内容到 DataGridView 控件中。让我们在应用程序中添加代码来访问已添加到应用程序中的第二个 DataGridView 控件中的数据。为此，在 Button 控件的 Click 事件上添加以下代码，如清单 24.2 所示：

## Listing 24.2: Showing the Code for the Click Event of the Button Control

```
private void button1_Click(object sender, EventArgs e)
{
    OleDbConnection con = new OleDbConnection();
    con.ConnectionString = ("Provider=Microsoft.ACE.OLEDB.12.0;Data Source=D:\Black Books\C# 2010\Chapter 24\code\OLEDBDatabase\OLEDBDatabase\Northwind.accdb");
    OleDbDataAdapter da = new OleDbDataAdapter("select * from Employees", con);
    DataSet ds = new DataSet();
    da.Fill(ds);
    dataGridView2.DataSource = ds.Tables[0];
}
```

### NOTE

> 你应该在代码中更改连接字符串并使其符合你的系统。你还需要在 Form1.cs 页面中添加 System.Data.OleDb 命名空间。

点击 Generate Data 按钮后，应用程序的输出如图所示 Figure 24.29：

![](img/e073a4882197be4ab61103cbe0bcb394_1194_0.png)

## Figure 24.29: Accessing Data in the DataGridView Control

如前所述，OLE DB 也可以用于访问其他类型的数据源，例如 Excel 文件。你可以使用 OLE DB 将 Excel 文件的数据检索到 DataGridView 控件中。让我们再创建一个示例，看看如何通过执行以下步骤在 DataGridView 控件中检索 Excel 文件的数据：

- 1. 在 Visual Studio 2010 中创建一个名为 OLEDBExcel 的 Windows 应用程序（可在 CD-ROM 中获得）。
- 2. 向 Form1 添加一个 DataGridView 控件和一个 Button。
- 3. 将 Button 控件的 Text 属性更改为 Change to View Data。

当你点击 Button 控件时，DataGridView 控件中的数据将被检索。DataGridView 控件中使用的 Excel 文件是一个包含一些数据的简单 Excel 文件。我们已创建该 Excel 文件并在其中输入数据。Excel 文件的列名为 Emp_ID、Emp_Name、Emp_Number、Emp_Addresss 和 Emp_Salary。Excel 文件的工作表已重命名为 Contacts。在这些列下输入数据后，我们已将 Excel 文件保存在系统的 D:\ 驱动器中，文件名为 book1.xls。你需要在创建连接字符串时提供 Excel 文件在 Data Source 中的正确路径。

- 4. 将如清单 24.3 所示的代码添加到 Button 控件的 Click 事件中：

## Listing 24.3: Showing the Code for Click Event of the Button Control

```
private void button1_Click(object sender, EventArgs e)
{
    string ConnectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" + "Data Source=" + @"D:\\book1.xls;" + "Excel 12.0;HDR=YES;";
    OleDbConnection ExcelConnection = new OleDbConnection(ConnectionString);
    OleDbDataAdapter ad = new OleDbDataAdapter();
    ad.SelectCommand = new OleDbCommand("SELECT * FROM [contacts$]", ExcelConnection);
    DataTable dt = new DataTable();
    ad.Fill(dt);
    dataGridView1.DataSource = dt;
}
```

在清单 24.3 中给出的代码中，你可以在点击 Button 时使用 OLE DB 在 DataGridView 控件中查看 Excel 文件的数据。点击 Click the View Data 按钮后，你可以看到输出，如 Figure 24.30 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1195_0.png)

## Figure 24.30: Displaying the Record from an Excel File Using OLE DB

## ODBC Data Source

ODBC 是在关系型和非关系型数据库管理系统异构环境中访问数据的接口。使用 ODBC 数据源的最佳示例是访问 Microsoft Access 数据库。你可以通过向导以及代码创建 ODBC 数据源。在创建 ODBC 数据源之前应先创建 ODBC 用户数据源。此用户数据源存储有关如何连接到特定数据提供程序的信息。你需要注意，用户数据源仅对你可见，只能在你的机器上使用。让我们先通过执行以下步骤创建一个 ODBC 用户数据源：

- 1. 打开控制面板，从管理工具中选择数据来源（ODBC）。

### NOTE

> ProgramData 文件夹是一个隐藏文件，除非你选择显示隐藏文件和文件夹选项，否则不会显示。

这将打开 ODBC 数据源管理器对话框（Figure 24.31）。

- 2. 在 ODBC 数据源管理器对话框的 User DSN 选项卡中点击 Add 按钮，如 Figure 24.31 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1196_0.png)

## Figure 24.31: Creating User Data Source

这将打开创建新数据源对话框（Figure 24.32）。

- 3. 在创建新数据源对话框中选择 Microsoft Access Driver，然后点击 Finish 按钮，如 Figure 24.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1196_1.png)

## Figure 24.32: Selecting Driver for the New Data Source

这将打开 ODBC Microsoft Access 设置对话框（Figure 24.33）。

- 4. 在 ODBC Microsoft Access 设置对话框中输入数据源名称。在我们的例子中，我们将数据源名称输入为 myDSN（Figure 24.33）。
- 5. 点击数据库组中的 Select 按钮，如 Figure 24.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1197_0.png)

## Figure 24.33: Showing the Access Setup

选择数据库对话框出现（Figure 24.34）。

- 6. 从目录列表框中导航到存储在你机器上的 Access 数据库文件。所选 Access 文件的名称出现在数据库名称列表框中（Figure 24.34）。
- 7. 在数据库名称列表框中选择文件（在我们的例子中我们选择 Northwind.accdb）并点击 OK 按钮，如 Figure 24.34 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1197_1.png)

## Figure 24.34: Showing the Select Database Dialog Box

选择数据库对话框关闭。

- 8. 点击 ODBC Microsoft Access 设置对话框的 OK 按钮（Figure 24.33）。你可以看到 myDSN 数据源已添加到 ODBC 数据源管理器对话框（Figure 24.35）。
- 9. 如 Figure 24.35 所示，点击 ODBC 数据源管理器对话框上的 OK 按钮：

![](img/e073a4882197be4ab61103cbe0bcb394_1197_2.png)

## Figure 24.35: Showing the Added Data Source

数据源已创建，你可以使用 ODBC 数据源并将其附加到你的应用程序。

现在，让我们创建一个附加了 ODBC 数据源的应用程序。为此，创建一个名为 ODBCDataSource 的 Windows 应用程序（可在 CD-ROM 中获得）并向其添加两个 DataGridView 控件和一个 Button。将 Button 控件的文本更改为 Click to Generate Data，如 Figure 24.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1198_0.png)

Figure 24.36: Adding Controls and a Button

我们将通过向导在第一个 DataGridView 控件中生成数据，并在点击 Button 时在第二个 DataGridView 控件中生成数据。让我们先通过向导在第一个 DataGridView 控件中生成数据。

- 10. 选择 dataGridView1 控件并点击 Smart Tag 以选择 dataGridView1 控件的内容。
- 11. 从 dataGridView1 控件的 Smart Tag 中的 Choose Data Source 下拉列表中选择 Add Project Data Source 选项。这将打开数据源配置向导。
- 12. 选择 Database 作为数据源类型并点击 Next 按钮以打开选择数据库模型页面。
- 13. 在选择数据库模型页面中选择 Dataset 作为数据库模型并点击 Next 按钮以打开选择你的数据连接页面。
- 14. 在选择你的数据连接页面中点击 New Connection 按钮。这将打开添加连接对话框（Figure 24.37）。
- 15. 如 Figure 24.37 所示，点击添加连接对话框的 Change 按钮：

