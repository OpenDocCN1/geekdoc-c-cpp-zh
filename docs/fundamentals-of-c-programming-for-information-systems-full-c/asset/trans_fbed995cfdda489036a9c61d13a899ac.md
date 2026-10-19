

## 图 12-2：选择数据源类型

![](img/143bad48262566137acc9c41f668a88f_356_0.png)

步骤 1-4：选择数据库并单击下一步。你将被要求选择一个数据库模型。

步骤 1-5：对于数据库模型，选择数据集。你将被要求选择数据连接，如图 12-3 所示。

## 图 12-3：选择数据连接

你的应用程序应使用哪种数据连接来连接到数据库？

![](img/143bad48262566137acc9c41f668a88f_356_1.png)

步骤 1-6：如果下拉列表显示数据库文件名 HR.mdf，你可以直接进入步骤 1-8。如果没有，单击新建连接按钮。如果显示添加连接窗口，单击更改按钮。选择数据源窗口打开，如图 12-4 所示。

## 图 12-4：添加连接

![](img/143bad48262566137acc9c41f668a88f_356_2.png)

步骤 1-7：为数据源选择 *Microsoft SQL Server Database File*。数据提供程序的下拉列表应显示 .Net Framework Data Provider for Microsoft SQL Server。

单击 *Continue*。会出现以下添加连接窗口：

![](img/143bad48262566137acc9c41f668a88f_357_0.png)

单击 *Browse*，并从本地目录中选择 HR.mdf。单击 *Open*。

单击 *OK*。如果数据库与当前 SQL Server 实例不兼容，你将被要求是否要升级数据库。选择 *Yes*。

# 步骤 1-8：单击 *Next*。你可能会被要求是否要将文件复制到你的项目中。确保选择 *No*。

如果你回答 *Yes*，Visual Studio 将把数据库文件复制到项目目录中，并且默认情况下，在项目运行时对数据库所做的更改将在下次运行项目时丢失。

单击 *Next*。你将被要求是否要保存连接字符串。

接受默认值（*Yes*），并单击 *Next*。你将被要求选择数据库对象，如图 12-5 所示。

## 图 12-5：选择数据库对象

![](img/143bad48262566137acc9c41f668a88f_357_1.png)

## 12.3 在 DataGridView 中显示数据

![](img/143bad48262566137acc9c41f668a88f_361_0.png)

从单元格样式生成器窗口中选择格式，并单击右侧的省略号以打开格式字符串对话框窗口。

选择货币，并将小数位数指定为 0。

接下来，运行项目。你将看到员工记录显示在网格中，如图 12-11 所示。

要测试表单，请更改一条记录，单击保存并关闭表单。现在重新打开表单以确保更改已保存。测试添加新记录和删除记录是否正常工作。

## 图 12-11：DataGridView 中的员工表

![](img/143bad48262566137acc9c41f668a88f_361_1.png)

## 数据绑定控件

数据绑定控件是链接到数据源的用户界面控件。当你将员工数据表拖放到表单上时，向导将 DataGridView 添加到表单中，并通过绑定源将其绑定到员工数据表。如图 12-12 所示，DataGrid 的 Data Source 属性设置为 employeeBindingSource。

第 23 行中的语句，
    this.employeeTableAdapter.Fill(this.hRDataSet.Employee);
使用表适配器的 Fill 方法将数据从数据库表加载到数据表 Employee 中。

将更改从 DataGridView 保存到数据库表是一个两步过程：

- 1. 将更改从 DataViewGrid 保存到数据表 Employee。这是通过在第 29 行使用绑定源的 EndEdit 方法完成的：
-       this.employeeBindingSource.EndEdit(),
- 2. 将更改从数据表保存到数据库表。这是通过在第 30 行使用 tableAdapterManager 的 UpdateAll 方法完成的：
-       this.tableAdapterManager.UpdateAll(this.hRDataSet);

## 查看或编辑连接字符串

步骤 1-14：要查看或编辑连接字符串信息，请在解决方案资源管理器中双击属性下的设置，如图 12-15 所示。

图 12-15：查看 ConnectionString 信息

![](img/143bad48262566137acc9c41f668a88f_363_0.png)

你将看到连接字符串信息，如图 12-16 所示。

图 12-16：ConnectionString 信息

![](img/143bad48262566137acc9c41f668a88f_363_1.png)

步骤 1-15：在值下的最右侧列中单击，并单击省略号以打开允许你编辑信息的连接属性窗口。
单击取消并关闭设置窗口。

## 数据集的结构

添加数据源还会将文件 HRDataset.xsd（xsd 代表 XML Schema Document）添加到解决方案资源管理器窗口。

步骤 1-16：要查看数据集中表的结构，请在解决方案资源管理器中双击 HRDataset.xsd。你将看到 HRDataSet.xsd 窗口，其中显示员工数据表及其关联的表适配器，如图 12-17 所示。

## 12.4 从 DataGridView 访问数据项

除了查看和编辑数据库表外，你还可以使用 DataGridView 的属性和事件访问单个数据项。图 12-18 显示了 DataGridView 的一些主要属性和事件。

图 12-18：DataGridView 的属性和事件

| 属性 | 描述 |
|---|---|
| ColumnCount | 列数。 |
| Columns | 所有列的集合。 |
| CurrentRow | 包含当前单元格的行。每一行都由 Cells 集合表示的单元格集合组成。 |
| CurrentCell | 当前单元格。Value 属性给出单元格的值。 |
| 启用添加（编辑、删除）- 这是单击右上角箭头（智能标记）时显示的任务面板中的一项。 | 选中时，用户可以添加（编辑、删除）列。默认情况下，它是选中的。 |
| RowCount | 行数，包括新记录的行。 |
| Rows | 所有行的集合。使用列索引或列名访问单元格（例如，Rows[3].Cells[4]；或 Rows[3].Cells["Phone"]）。使用 Value 属性获取与单元格关联的值（对象类型）（例如，Rows[3].Cells["Phone"].Value）。 |
| SelectedColumns | 用户选择的列的集合。 |
| SelectedRows | 用户选择的行的集合。 |
| 事件 | |
| CellClick | 当单元格被单击时。 |
| CurrentCellChanged | 当当前单元格更改时。 |

让我们看看一些使用这些属性和事件与表交互的示例。

## Rows 和 Cells 集合

你可以使用 Rows 和 Cells 集合通过指定其列和行索引来访问任何单元格。例如，第 2 行第 8 列中的数据项由以下代码给出

```
employeeDataGridView.Rows[1].Cells[7].Value.ToString()
```

请注意，行 1 的索引为 0，行 2 的索引为 1，以此类推。

## Value 属性

Value 属性给出与单元格关联的值。ToString 方法将 Value（对象类型）转换为字符串。

你也可以使用列名代替列索引，如下所示

```
employeeDataGridView.Rows[1].Cells["Salary"].Value.ToString()
```

## 列名

上述语句假定 Salary 字段的列名已从其原始名称 salaryDataGridViewTextBoxColumn 更改为 Salary，如图 12-19 所示。虽然 DataGridView 中的列标题（HeaderText 属性）与字段名相同，但列名不同，如图 12-19 所示。因此，如果你在代码中使用列名，你可能希望更改这些列的名称，使列名与字段名和列标题相同。如前所述，你可以通过单击 DataGridView 的 Columns 属性右侧的省略号来显示编辑列窗口。

选择 DataGridView，并从属性窗口中选择 Columns。单击属性右侧的省略号 (...) 以显示编辑列窗口。

图 12-19：DataGridView 的列属性

![](img/143bad48262566137acc9c41f668a88f_366_0.png)

## 显示所选单元格的值

你可以使用 CurrentCellChanged 事件处理程序和 CurrentCell 属性，在用户单击单元格时自动显示单元格的值。图 12-20 显示了在标签中显示当前单元格值的代码。

图 12-20：DataGridView 的 CurrentCellChanged 事件处理程序

```
33  private void employeeDataGridView_CurrentCellChanged(object sender, EventArgs e)
34  {
35      lblCurrentCell.Text = employeeDataGridView.CurrentCell.Value.ToString();
36  }
```

步骤 1-18：添加一个名为 lblCurrentCell 的标签和另一个显示提示“Current Cell”的标签，如图 12-21 所示。

创建 DataGridView 的 CurrentCellChanged 事件处理程序并添加图 12-20 中的代码。单击一个单元格来测试代码。标签应显示所选单元格中的数据项。

