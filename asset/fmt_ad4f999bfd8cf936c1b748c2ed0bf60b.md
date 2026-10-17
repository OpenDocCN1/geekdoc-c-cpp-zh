
第 4 行的语句调用 `productTableAdapter` 的 `Fill` 方法，并将数据集的 `Product` 表作为参数传递。`Fill` 方法使用 SQL 语句返回的行填充数据集表。现在让我们来看由 `Fill` 方法执行的 SQL 语句。在解决方案管理器中，你应该能看到一个名为 `ProductDataSet.xsd` 的项，如图 12-70 所示。这是描述 `productDataSet` 内容的架构定义文件。双击 `ProductDataSet.xsd` 在编辑器窗口中打开它，如图 12-71 所示。图表顶部区域显示了数据包含的列，底部区域显示了表适配器查询方法。

# 图 12-71 正在编辑的 ProductDataSet.xsd

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1668_0.png)

右键点击显示有 `Fill`、`GetData()` 的区域，如图 12-72 所示，从弹出菜单中选择“配置（Configure）”。这将显示图 12-73 所示的表适配器配置向导。注意表适配器配置向导窗口中出现的 SQL 查询。数据集由此 `Select` 语句返回的行填充。如果你更改此 `Select` 语句（例如添加 `Where` 子句然后点击“完成（Finish）”按钮），`DataGridView` 控件中最初显示的数据将相应改变。检查完该窗口后，点击“取消（Cancel）”按钮关闭它。

# 图 12-72 从弹出菜单选择 Select 配置

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1669_0.png)

# 图 12-73 表适配器配置向导

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1669_1.png)

注意 `Select` 语句中的表名前面带有 `dbo.` 前缀。`dbo` 前缀代表数据库所有者，是 SQL Server 命名规范的一部分。在我们的示例程序中 `dbo` 前缀是可选的。

# 添加新的表适配器查询

你可以将自己的 SQL 查询添加到表适配器中，并在 C# 代码中调用它们。在教程 12-6 中，你向表适配器添加了几个查询，然后在应用程序表单上创建了执行这些查询的按钮。

# 教程 12-6：创建产品查询应用程序

> 教程 12-6：创建产品查询应用程序

在本教程中，你将创建一个应用程序，在 `DataGridView` 控件中显示来自 `ProductDB.rdf` 数据库的 `Product` 表。你向表适配器添加了两个 SQL 查询。这些查询执行以下操作：

- 按价格升序返回所有行
- 仅返回库存数量大于 100 单位的行

然后，你在应用程序表单上创建了执行这些查询的按钮。

**步骤 1**：启动 Visual Studio。创建一个名为 `Product Queries` 的新 Windows Forms 项目。

**步骤 2**：将 `Form1` 表单的 `Text` 属性改为 `Product Queries`。

**步骤 3**：执行以下步骤将应用程序连接到 `ProductDB.mddf` 数据库并为数据集选择 `Product` 表：

- 从“项目（Project）”菜单中选择“添加新建数据源（Add New Data Source...）”。选择“数据库（Database）”并点击“下一步（Next）”。
- 选择“数据集（Dataset）”并点击“下一步（Next）”。
- 点击“连接（Connection...）”。
- 在“添加连接（Add Connection）”窗口中，确保选中了 `Microsoft SQL Database File (SqlClient)`。
- 在“添加连接”窗口中，点击“浏览（Browse）”，进入 Student Sample Programs 中的 `Chap12` 文件夹。选择 `ProductDB.mddf` 文件。点击“确定（OK）”。
- 点击“下一步（Next >）”，询问是否将文件复制到项目时，点击“是（Yes）”。
- 选择 `Product` 表作为数据库对象，并将数据集名称更改为 `ProductDataSet`。点击“完成（Finish）”。

> 注意
这是你在教程 12-3 步骤 3-11 中的相同操作。如果你需要更详细的指导，请返回该教程查看实际界面。

**步骤 4**：打开“数据源（Data Sources）”窗口，将 `DataGridView` 控件拖到表单上，并绑定到 `Product` 表。放置 `DataGridView` 控件后，调整控件的大小，如图 12-74 所示。

**图 12-74 应用程序**![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1672_0.png)

**步骤 5**：现在你添加按价格排序的第一个查询。在解决方案管理器中，双击 `DataSet`。这将打开架构。右键点击显示 `TableAdapter` 的区域，如图 12-75 所示。

**图 12-75 向表添加查询**![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1671_0.png)

> 注意
可能会在弹出菜单中看到“添加（Add）”。步骤 6：如图 12-76 所示出现了表适配器配置向导。确保选中了“使用语句（Use Statements）”，然后点击“下一步（Next）”。

**图 12-76 表适配器配置向导**![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1670_0.png)

**步骤 7**：向导现在提示你选择查询类型，如图 12-77 所示。选中“选择行（Select returns rows）”，然后点击“下一步（Next）”。

**图 12-77 选择查询类型**![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1669_0.png)

**步骤 8**：向导现在提示你指定 SQL 语句。已经显示了一个返回所有行的语句。如图 12-78 所示，在语句末尾添加 `Order By Price` 子句。点击“下一步（Next）”。

**图 12-78 指定 SQL 语句**![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1668_0.png)

**步骤 9**：勾选“填充数据集（Fill DataTable）”。在“填充数据集”下输入 `FillByPrice` 作为方法名称。这将将执行该语句的方法名称。不要勾选“返回数据集（Return a DataTable）”。

**步骤 10**：向导显示结果，如图 12-80 所示。点击“完成（Finish）”按钮。架构定义文件（`DataSet.xsd`）应该如图 12-81 所示。注意 `FillByPrice()` 方法现在出现在图表底部的区域。

**图 12-80 表适配器配置向导**![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1667_0.png)

# 图 12-81 架构定义文件中出现的 FillByPrice() 方法

| Product |
|------|
| Product_Number |
| Description |
| 49+60+53+31+50+7+21+37= |
| Price |
| TableAdapter |
| Fill,GetData() |
| FillByPrice() |

### 注意

在创建表适配器查询后，你可以通过右键点击数据集架构中的项对其进行编辑。

定义，然后从弹出菜单中点击配置（ . . 。

**第 11 步：** 接下来你添加第二个查询，该查询仅返回库存数量大于 100 的行。执行以下步骤（大部分步骤与你之前添加上一个查询时执行的操作相同）：

- 在架构定义中，右键点击显示为 *ProductTableAdapter* 的区域。
- 在弹出菜单中，选择 *Add（添加），然后点击 *Query . . .*（查询）（或者，如果你看到 *Add Query . . .*，则选择该项）。
- 接下来会出现 *TableAdapter 查询配置向导*。确保已选择 *Use SQL Statements（使用 SQL 语句），然后点击 *Next（下一步）。
- 向导现在提示你选择查询类型。确保已选择返回行的 *SELECT*，然后点击 *Next*（下一步）。
- 向导现在提示你*指定一个 SQL SELECT 语句*。界面上已显示了一个返回 *Product* 表中所有行的语句。在语句末尾添加 *Units_On_Hand > 100* 子句，如**图 12-82** 所示。点击 *Next*（下一步）。

## **图 12-82** TableAdapter 查询配置向导——指定一个 SQL SELECT 语句

## TableAdapter 查询配置向导

### 指定一个 SQL SELECT 语句

查询将使用该 SELECT 语句。

输入你的 SQL 语句或使用查询生成器构建它。应该加载哪些数据到表中？表中应该加载哪些数据？

```
SELECT Product_Number, Description, Units_On_Hand, Price FROM dbo.Product WHERE Units_On_Hand > 100
```

添加此 WHERE 子句。

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1680_0.png)

- 向导现在提示你选择生成的方法。进行以下选择：
  - 确保勾选了 *Fill a DataTable（填充数据表）*。
  - 在 Fill a DataTable 下下，输入 `FillByUnits` 作为方法名。这将是执行 SQL 语句的方法名。
  - 确保未勾选 *Return a DataTable（返回数据表）*。

- 窗口现在应如图 12-83 所示。点击 *Next*（下一步）。

## 图 12-83 TableAdapter 查询配置向导–选择生成的方法

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1681_0.png)

- 向导现在显示结果。点击 *Finish（完成）* 按钮。

架构定义文件 (`ProductDataSet.xsd`) 现在应如图 12-84 所示。注意你创建的方法 `FillByPrice()` 和 `FillByUnits()` 现在出现在图表底部的区域。

图 12-84 架构定义文件中的 FillByPrice() 和 FillByUnits() 方法

**第 12 步：** 现在你向应用程序的表单添加用于执行 SQL 查询的按钮（Button）控件。在**Designer（设计器）**中打开 Form1，并添加**图 12-85** 所示的两个按钮控件。

## **图 12-85** 添加到表单上的按钮控件

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1682_0.png)

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1683_0.png)

**第 13 步：** 双击 `sortByButton` 控件。通过在 Program 12-4 的第 37 行输入代码来完成 `sortByButton_Click` 事件处理。此语句调用了表适配器的 **FillByPrice** 方法。

**第 14 步：** 在**Designer（设计器）**中切换视图回 Form1，并双击 `unitsGreater100Button` 控件。通过在 Program 12-4 的第 42 行输入代码完成 `unitsGreater100Button_Click` 事件处理。此语句调用了表适配器的 **FillByUnits** 方法。

第 15 步：保存项目并运行应用程序。当你点击 `unitsGreater100Button` 时，DataGridView 仅显示 Units_On_Hand 大于 100 的行。当你点击 `sortByButton` 时，DataGridView 将按价格排序。

# 从 Product 中选择 Avg(Price)

窗口应如图 12-86 所示。点击下一步。

图 12-86 TableAdapter 查询配置向导——指定 SQL SELECT 语句

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1689_0.png)

**第 6 步：** 向导提示你选择函数名称（Choose Function Name）。你在在此窗口中指定的名称将作为执行查询的方法名称。如图 12-87 所示，将名称更改为 AveragePrice，然后点击下一步。

图 12-87 TableAdapter 查询配置向导——选择函数名称

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1690_0.png)

**第 7 步：** 向导现在向你显示结果。点击*完成*（*Finish*）按钮。程序架构定义文件（ProductDataSet.xsd）现在应该出现，如**图 12-88**所示。注意，*AveragePrice* 方法出现了，以及你之前创建的其他方法。

**图 12-88** *在程序架构定义文件中显示的 AveragePrice() 方法*

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1690_1.png)

**第 8 步：** 接下来你向应用程序的表单添加一个按钮（Button）控件，用于执行表适配器的 AveragePrice 方法。在设计器中打开 Form1，以及图 12-89 所示的 averagePriceButton 控件。

图 12-89 添加到表单上的 averagePriceButton 控件

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1691_0.png)

**第 9 步：** 双击 averagePriceButton 控件。通过在 Program 12-5 的第 47–55 行中输入代码，完成 averagePriceButton_Click 事件处理程序。让我们仔细查看代码：

**第 48 行：** 该语句声明了一个名为 averagePrice 的本地 decimal 类型变量。

**第 51 行：** 该语句调用了表适配器的 AveragePrice 方法，该方法返回你在第 4 步中编写的 Select 语句的结果。该值被赋值给 averagePrice 变量。注意，我们必须使用强制转换符显式地将值转换为 decimal。

**第 54–55 行：** 该语句显示一个消息框，显示表中所有项目的平均价格。点击-

**第 10 步：** 保存项目并运行应用程序。点击“所有项目的平均价格”（Average Price of All Items）按钮。你应该能看到一个消息框，其中显示一条关于所有项目平均价格的消息。完成后，关闭应用程序表单以退出。

# 程序 12-5 Product 查询 应用程序中完成的 Form1 代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Product_Queries
{
    public partial class Form1 : Form
    {
```

```csharp
public Form1() 
{
    InitializeComponent();
}
private void productBindingNavigatorSaveItem_Click(object sender, EventArgs e)
{
    this.Validate();
    this.productBindingSource.EndEdit();
    this.tableAdapterManager.UpdateAll(this.productDataSet);
}
private void Form1_Load(object sender, EventArgs e)
{
    // TODO: 这行代码
    // 将数据加载到 . . .
    this.productDataAdapter.Fill(this.productDataSet.Product);
}
private void sortByPriceButton_Click(object sender, EventArgs e)
{
    this.productDataAdapter.FillByPrice(this.productDataSet.Product);
}
private void unitsGreater100Button_Click(object sender, EventArgs e)
{
    this.productDataAdapter.FillByUnits(this.productDataSet.Product);
}
private void
averagePriceButton_Click(object sender,
EventArgs e)
{
    // 声明一个变量来
// 保存平均价格。
    decimal averagePrice;

    // 获取平均价格。
    averagePrice = (decimal)
this.productTableAdapter.AveragePrice();

    // 显示平均
// 价格。
    MessageBox.Show("Average
```
