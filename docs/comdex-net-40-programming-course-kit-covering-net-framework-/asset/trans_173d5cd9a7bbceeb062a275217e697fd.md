
出现“更改数据源”对话框，你可以在其中为应用程序选择数据源，如图C#-4.5所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_369_0.png)

Fig.C#-4.5

- 6. **选择** Microsoft SQL Server 作为数据源，以**连接到 SQL Server** 数据库（图C#-4.5）。
- 7. 单击**确定**按钮（图C#-4.5）。

**添加连接**对话框再次出现，其中已选择 **Microsoft SQL Server (SqlClient)** 选项作为数据源，如图C#-4.6所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_369_1.png)

Fig.C#-4.6

- 8. 从**服务器名**组合框中**选择**服务器名称（图C#-4.6）。

在“添加连接”对话框中，默认情况下，**使用 Windows 身份验证**选项旁边的单选按钮处于选中状态（图C#-4.7）。如果要使用 **SQL Server 身份验证**，则选择**使用 SQL Server 身份验证**选项旁边的单选按钮，并在“用户名”和“密码”文本框中**提供用户名和密码**进行身份验证。在本例中，为了连接到服务器，我们使用 **Windows 身份验证**。

- 9. 在**选择或输入数据库名称**组合框中**选择**数据库或输入要连接的数据库名称。在本例中，我们已选择 **northwind** 数据库，如图C#-4.7所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_370_0.png)

Fig.C#-4.7

- 10. 单击**测试连接**按钮。
    出现一个消息框，其中显示消息**测试连接成功**（图C#-4.7）。
- 11. 单击消息框中的**确定**按钮以关闭消息框（图C#-4.7）。
- 12. 单击**添加连接**对话框中的**确定**按钮（图C#-4.7）。

**添加连接**对话框关闭，数据源将添加到应用程序中。你可以在**服务器资源管理器**窗口中看到它，如图C#-4.8所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_370_1.png)

Fig.C#-4.8

### 使用代码编辑器建立连接

你也可以通过代码编辑器创建连接字符串。应用程序的连接字符串取决于要连接的数据源类型。对于 OLE DB 数据源（例如 **Microsoft Access**），使用 **OleDbConnection** 类的 **ConnectionString** 属性；对于 **SQL Server**，使用 **SqlConnection** 类的 **ConnectionString** 属性；对于 **Oracle** 数据源，使用 **OracleConnection** 类的 **ConnectionString** 属性。

连接字符串的基本语法包含一系列由分号分隔的关键字。等号连接每个关键字及其值。以下代码片段显示了用于连接 SQL Server 数据库的连接字符串：

```
Data Source=ANAMIKA-PC\SQLEXPRESS;Initial Catalog=northwind;Integrated Security=True
```

前面代码片段中所用术语的解释如下：

- **数据源**：表示要连接的 SQL Server 实例的名称或网络地址。
- **初始目录**：表示数据库的名称。
- **集成安全性**：接受布尔值，可以是 **True** 或 **False**。如果值为 **False**，则需要在连接字符串中指定**用户 ID**和**密码**。如果值为 True，则使用当前 Windows 帐户凭据进行身份验证。默认值为 True。

接下来，我们看看如何使用命令对象执行命令。

### 使用命令对象执行命令

与数据库建立连接后，你可以执行命令并从数据库获取结果。要访问数据库，数据命令应提供有关连接、SQL 语句或要执行的存储过程名称的信息。存储过程是一组一个或多个 SQL 语句，可以一起运行并存储在数据库中。

执行以下步骤创建一个名为 CommandObject 的应用程序（CD 上也提供），该应用程序演示如何使用命令对象访问数据库：

- 1. *打开* **Microsoft Visual Studio 2010**。
- 2. 从菜单栏中*选择* **文件→新建→项目**。出现**新建项目**对话框。
- 3. 从**已安装的模板**窗格中*选择* Visual C#→Windows，并从中间窗格中选择**Windows 窗体应用程序**选项。
- 4. 在**名称**文本框中*输入*应用程序名称 **CommandObject**，并在**位置**组合框中为应用程序输入适当位置。
- 5. *单击***确定**按钮以关闭**新建项目**对话框。**CommandObject**应用程序已创建。
- 6. 从**工具箱**中*拖动***Label**控件，并将其*放到***Form1**上（图C#-4.9）。
- 7. 将**Label**控件的**Text**属性*更改*为**选择员工 ID**（图C#-4.9）。
- 8. 从**工具箱**中*拖动***ComboBox**控件，并将其*放到***Form1**上（图C#-4.10）。

![](img/9862a98a1a2d3bb14334137965a1ec60_371_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_371_1.png)

- 9. *双击***Form1**。这会打开代码编辑器。
- 10. 将清单4.1中给出的代码*添加*到**Form1.cs**文件中。

**清单4.1：** 显示创建命令对象的代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.Sql;
using System.Data.SqlClient;

namespace CommandObject
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            SqlConnection connection = new SqlConnection();
            connection.ConnectionString = "Data Source=ANAMIKA-PC\\SQLEXPRESS;Initial Catalog=northwind;Integrated Security=True;User Instance=True";
            connection.Open();
            SqlCommand cmd = new SqlCommand("select * from Employees", connection);
            SqlDataAdapter adp = new SqlDataAdapter(cmd);
            DataSet ds = new DataSet();
            adp.Fill(ds, "Employees");
            comboBox1.DataSource = ds.Tables["Employees"];
            comboBox1.DisplayMember = "EmployeeID";
            comboBox1.ValueMember = "EmployeeID";
        }
    }
}
```

在清单4.1中，首先创建一个 SqlConnection 对象 connection。使用连接对象的 ConnectionString 属性，该连接对象接受一个连接字符串并使用它创建新连接。此连接字符串包含数据源名称和数据库名称。之后，创建 SqlCommand 类的对象 cmd，该对象针对 SQL Server 数据库执行 Select 命令。

> **在清单4.1中，你需要根据系统设置更改连接字符串。**

- 11. 按 F5 键运行应用程序。输出出现，如图C#-4.11所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_372_0.png)

Fig.C#-4.11

在图C#-4.11中，ComboBox 控件包含 northwind 数据库中 Employees 表的 EmployeeID 字段的值。

### 添加和配置数据适配器

数据适配器使你能以断开连接的体系结构访问数据库中的数据。操作、更新和修改数据源中的数据所需的所有命令都可在 DataAdapter 对象中使用。

执行以下步骤创建一个名为 **DataAdapter** 的应用程序（CD 上也提供），以通过数据适配器访问数据库中的数据：

- 1. *打开* Microsoft Visual Studio 2010。
- 2. 从菜单栏中*选择* **文件→新建→项目**。**新建项目**对话框打开。
- 3. 在**新建项目**对话框中，从**已安装的模板**窗格中*选择* **Visual C#→Windows**，并从中间窗格中选择**Windows 窗体应用程序**选项。
- 4. 在**名称**文本框中*输入*应用程序名称 **DataAdapter**，并在**位置**组合框中为应用程序输入适当位置。
- 5. *单击***确定**按钮以关闭**新建项目**对话框。**DataAdapter**应用程序已创建。

如果**工具箱**中不存在**SqlDataAdapter**控件，请执行步骤6到8，将**SqlDataAdapter**控件添加到**工具箱**的**数据**选项卡；否则直接转到步骤9。

- 6. *右击***工具箱**的**数据**选项卡，然后从上下文菜单中*选择***选择项**选项，如图C#-4.12所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_373_0.png)

Fig.C#-4.12

出现“选择工具箱项”对话框，如图C#-4.13所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_373_1.png)

Fig.C#-4.13

- 7. 在**选择工具箱项**对话框中，在 **.NET Framework 组件**选项卡下，*选择***SqlDataAdapter**选项旁边的复选框（图C#-4.13）。
- 8. *单击***确定**按钮以关闭**选择工具箱项**对话框（图C#-4.13）。
