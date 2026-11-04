
10 单击“查询生成器”按钮以创建 SQL 语句，或选择现有的存储过程，以生成 SQL 语句。

“查询生成器”对话框与“添加表”对话框一起出现（图 C#8.13）。

11 从“添加表”对话框中选择一个表。在本例中，我们选择 Employees 表（图 C#8.13）。

12 单击“添加”按钮，将 Employees 表添加到“查询生成器”对话框中（图 C#8.13）。

13 单击“关闭”按钮关闭“添加表”对话框，如图 C#8.13 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_273_0.png)

图 C#8.13

Employees 表已添加到“查询生成器”对话框中（图 C#8.14）。

在“查询生成器”对话框顶部，可以看到 Employees 表的所有字段；可以根据需要从表中选择字段。

14 选中 Employees 表中 *(所有列) 选项旁的复选框（图 C#8.14）。

15 单击“确定”按钮创建 SQL 语句，如图 C#8.14 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_273_1.png)

图 C#8.14

SQL 语句出现在 **数据适配器配置向导** 页中（图 C#8.15）。

- 16. 单击 **下一步** 按钮，如图 C#8.15 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_274_0.png)

图 C#8.15

出现“数据适配器配置向导”页，并显示数据适配器已成功配置的信息。

- 17. 单击 **完成** 按钮，关闭 **数据适配器配置向导** 页。

sqlDataAdapter1 数据适配器和 sqlConnection1 连接对象出现在组件栏中，如图 C#8.16 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_274_1.png)

图 C#8.16

- 18. 从菜单栏中选择 **数据→预览数据**，以预览来自数据适配器的数据，如图 C#8.17 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_274_2.png)

图 C#8.17

出现“预览数据”对话框（图 C#8.18）。

- 19. 单击“预览”按钮，在“结果”窗格中查看来自数据库的数据（图 C#8.18）。
- 20. 单击“关闭”按钮关闭“预览数据”对话框，如图 C#8.18 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_275_0.png)

接下来，我们将学习如何使用数据集在 Windows 窗体应用程序中显示来自数据源的数据。

## 创建数据集

如前所述，数据集包含数据库表的缓存副本。数据集独立于数据库，因此与现有数据库的交互通过数据适配器进行控制。可以使用数据适配器的 Fill() 方法将数据填充到数据集中。

现在，我们执行以下步骤来创建数据集：

- 1. 打开 DatabaseOperationsExample 应用程序。
- 2. 从菜单栏中选择 **数据→生成数据集**，如图 C#8.19 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_275_1.png)

出现“生成数据集”对话框，提示你选择数据集（图 C#8.20）。

可以选择现有数据集或创建新数据集。默认情况下，选中“新建”单选按钮。可以为新数据集提供名称，或使用现有的默认名称 DataSet1。“生成数据集”对话框还提示你选择要添加到数据集的表。在“生成数据集”对话框中，可以为数据集对象提供名称，并选择要添加到数据集对象中的表。在本例中，我们保留了默认设置（图 C#8.20）。

- 3. 单击“确定”按钮，将数据集添加到 DatabaseOperationsExample 应用程序，如图 C#8.20 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_276_0.png)

图 C#8.20

数据集 dataSet1 已添加到组件栏中，如图 C#8.21 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_276_1.png)

图 C#8.21

创建数据集后，我们来学习如何使用数据适配器将数据检索到数据集中。

## 使用数据适配器将数据检索到数据集中

到目前为止，我们已经创建了数据适配器和数据集。现在来看看如何使用数据适配器和数据集在 DataGridView 控件上显示数据。为此，请执行以下步骤：

- 1. 打开 DatabaseOperationsExample 应用程序。
- 2. 从“工具箱”的“数据”选项卡中拖动 DataGridView 控件，并将其放到 Form1 窗体中。添加 DataGridView 控件时，会自动出现智能标记。
- 3. 单击“选择数据源”下拉列表，查看所有可用数据源的列表（图 C#8.22）。
- 4. 单击“其他数据源”选项前面的三角形图标以展开它（图 C#8.22）。
- 5. 单击“项目数据源”选项前面的三角形图标以展开它（图 C#8.22）。
- 6. 选择 DataSet1 数据源，如图 C#8.22 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_277_0.png)

**图 C#8.22**

**dataSet1BindingSource** 绑定源已添加到组件栏中（图 C#8.23）。绑定源是指可以从中获取数据的数据源。在本例中，数据通过数据集获取。

- 7. 单击 **选择数据源** 下拉箭头，并从出现的下拉列表中选择 **Employees** 表，如图 C#8.23 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_277_1.png)

**图 C#8.23**

**employeesBindingSource** 绑定源已添加到组件栏中，如图 C#8.24 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_277_2.png)

**图 C#8.24**

- 8. 调整窗体（**基本数据库操作**）的大小，以容纳 **Employees** 表的数据。

9 使用 using 语句将 System.Data.SqlClient 命名空间导入 DatabaseOperationsExample 应用程序，如下面的代码片段所示：

```
using System.Data.SqlClient;
```

10 在 Form1 窗体的 Load 事件中添加清单 8.2 中突出显示的代码，以在 DataGridView 控件上显示员工详细信息：

### 清单 8.2：填充数据集

```
private void Form1_Load(object sender, EventArgs e)
{
    sqlDataAdapter1.Fill(dataSet1);
}
```

清单 8.2 显示，Fill() 方法用于将员工详细信息填充到 dataSet1 数据集中。

11 按键盘上的 F5 键执行 DatabaseOperationsExample 应用程序。输出如图 C#8.25 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_278_0.png)

图 C#8.25

如图 C#8.25 所示，SqlDataAdapter 类的 Fill() 方法用于使用 SQL Server 的 NORTHWND 表中的数据填充 DataSet 对象 dataSet1。

接下来，我们来了解 Windows 窗体中不同类型的数据绑定。

## Windows 窗体中数据绑定的类型

数据绑定是指将控件绑定到来自数据源的数据以显示数据。在传统数据绑定中，数据绑定操作主要针对存储在数据库中的数据执行。但是，使用 Windows 窗体数据绑定，现在可以绑定来自 SQL Server 数据库以及其他结构（如集合和数组）的数据。

可以通过绑定表中的特定字段或将整个表绑定到控件，来使用 SQL Server 数据库执行数据绑定。例如，可以将文本框绑定到表的 ProductName 字段，或将整个表绑定到 DataGridView 控件。

### 使用 BindingContext 类的简单数据绑定

简而言之，简单数据绑定是控件绑定单个数据元素的能力。

执行以下步骤来演示简单数据绑定：

- 1. **创建** 一个名为 **WindowsFormsDataBinding** 的应用程序。
- 2. **设置** **Form1** 的 **Text** 属性为 **简单数据绑定**。
- 3. **拖动**并放置以下控件到 **Form1** 上，并设置其属性值，如表 8.3 所示：
- 4. **导入** **System.Data.SqlClient** 命名空间到 **WindowsFormsDataBinding** 应用程序的代码隐藏文件中，使用 using 语句，如下面的代码片段所示：
- 5. **添加**清单 8.3 中突出显示的代码到 **Form1** 窗体的 **Load** 事件中，以显示 **EmployeeID** 为 6 的员工的详细信息：
- 6. **按** **F5** 键执行 **WindowsFormsDataBinding** 应用程序。输出如图 C#8.26 所示：

### 表 8.3：控件及其属性和值

| 控件名称 | 属性名称 | 值 |
|---|---|---|
| label1 | Text | 员工 ID |
| label2 | Text | 名 |
| label3 | Text | 姓 |
| label4 | Text | 职务 |
| textBox1 | Enabled | False |
| textBox2 | Enabled | False |
| textBox3 | Enabled | False |
| textBox4 | Enabled | False |

```csharp
using System.Data.SqlClient;
```

### 清单 8.3：显示简单数据绑定

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    SqlConnection con;
    con = new SqlConnection("Data Source=TEMP-PC\\SQLEXPRESS;Initial Catalog=\\SQL SAMPLE DATABASE\\NORTHWND.MDF;Integrated Security=True");
    con.Open();
    DataSet ds = new DataSet();
    SqlDataAdapter da = new SqlDataAdapter("Select * from Employees where EmployeeID=6", con);
    da.Fill(ds,"Employees");
    textBox1.DataBindings.Add("Text", ds, "Employees.EmployeeID");
    textBox2.DataBindings.Add("Text", ds, "Employees.LastName");
    textBox3.DataBindings.Add("Text", ds, "Employees.FirstName");
    textBox4.DataBindings.Add("Text", ds, "Employees.Title");
}
```

在清单 8.3 中，DataBindings 属性用于将文本框绑定到 Employees 表。
