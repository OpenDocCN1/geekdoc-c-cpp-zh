

可以在项目中选择数据库之前，使用 Windows 资源管理器重命名文件（如果存在，其配套的 pubs_log.ldf）。添加数据库到项目后，请勿尝试重命名数据库。

- STEP 4: 出现一条消息，提示您选择的连接使用的是不在当前项目中的本地数据文件，并询问是否要将其复制。选择 Yes。
- STEP 5: 接下来您可以选择保存连接字符串。保持选择 Yes（默认值）并单击 Next。
- STEP 6: 从数据库对象列表中展开 Tables 节点。然后展开 employee 表的节点。请注意，您可以展开该表并使用复选框选择想要的字段。选择 emp_id、fname、lname 和 hire_date。
- STEP 7: 默认名称为 PubsDataSet，已经很合适了。单击 Finish。请注意表格前面的图标（图 3.5）。该图标表示表格设置为 DataGridView。名称末尾的下拉箭头允许您选择不同的视图。稍后您将使用详细信息视图。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_136_0.png)

## Display Data in a Grid

在网格中显示数据

- STEP 1: 从 Data Sources 窗口中选择 employee 表并将其拖到窗体上。
- STEP 2: 查看组件托盘。它应包含 PubsDataSet、EmployeeBindingSource、EmployeeTableAdapter、TableAdapterManager 和 EmployeeBindingNavigator。
- STEP 3: 您需要按所需的外观调整窗体的大小并重新定位和调整网格的大小（图 3.6）。
- STEP 4: 启动程序；数据会自动显示（图 3.7）。显示数据时您编写了多少代码？
- STEP 5: 单击窗体的关闭按钮停止程序。如有必要，调整网格大小。

请注意窗体顶部的栏；这是从组件托盘中的 BindingNavigator 组件创建的 BindingNavigator 栏。该栏允许您定位到表中的任意记录，并使用按钮添加记录、删除记录或保存数据。请记住，更改会写入与原始数据文件断开连接的内存中 DataSet。

### Figure 3.6

窗体上的 DataGridView 控件，以及窗体组件托盘中的数据库组件。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_137_0.png)

### Figure 3.7

在 DataGridView 中显示 DataSet。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_137_1.png)

## Examine the Code

检查代码

停止执行后，查看自动生成的代码。EmployeeForm_Load 事件处理程序包含从表适配器填充 DataSet 的代码：

```
Me.EmployeeTableAdapter.Fill(Me.PubsDataSet.employee)
```

您还可以看到 BindingNavigator 的 SaveItem 事件处理程序。您将在第 5 章学习有关保存更改的内容，在那里您将学习如何处理更新数据库。

## Change the Column Headings

更改列标题

您可以通过更改列标题来提高网格的可读性。按照以下步骤将每列的 HeaderText 属性设置为所需的值。

- STEP 1: 单击网格的智能标记箭头并选择 Edit Columns。
- STEP 2: 在 Edit Columns 对话框中（图 3.8），请注意字段（列）出现在左侧窗格中，而所选列的属性显示在右侧的 Bound Column Properties 窗格中。HeaderText 属性决定网格上显示的标题。

**TIP**

在运行时单击网格中的列标题可按所选列对数据进行排序。

### Figure 3.8

更改所选列的 HeaderText 属性。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_138_0.png)

- STEP 3: 将 emp_id 的 HeaderText 改为 Employee ID，fname 改为 First Name，lname 改为 Last Name，hire_date 改为 Hire Date。请确保您更改的是 HeaderText 而不是 Name 属性。
- STEP 4: 单击 OK 并再次运行程序以查看更改。

## Grid Properties

网格属性

DataGridView 控件有许多属性，允许您指定用户如何与网格交互。以下是一些有用的属性：

| Property | Default setting |
|---|---|
| AllowUserToAddRows | True |
| AllowUserToDeleteRows | True |
| AllowUserToOrderColumns | False |
| AllowUserToResizeColumns | True |
| AllowUserToResizeRows | True |
| MultiSelect | True |
| RowHeadersVisible | True |

## The DataSet Designer

DataSet 设计器

在向项目添加新的数据源后，Solution Explorer 中的文件会添加一个扩展名为 .xsd 的文件。.xsd 文件包含模式定义。双击 .xsd 文件时，您会看到 DataSet Designer（图 3.9）。

DataSet Designer 是一个可视化工具，可用于查看和修改 DataSet 的定义。在 DataSet Designer 中，您可以添加字段、表和关系。您还可以使用设计器查看数据库中的数据。可视化显示在每个表的每个主键前面显示一个键图标。

### Figure 3.9

您可以使用 DataSet Designer 修改 DataSet 的属性。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_139_0.png)

请注意每个表的 TableAdapter，它处理该表的 Fill 和 GetData 方法。右键单击 TableAdapter 下的 Fill、GetData() 行并选择 Configure，以查看用于从 DataSet 选择数据的 SQL 语句。查看完毕后单击 Cancel 关闭对话框。

> Note: 有几种其他技术可用于在 Query Builder 中显示和编辑 TableAdapter 的 SQL 语句。您将在本章后面的“SQL”部分看到这些技术。

## Preview the DataSet Data

预览 DataSet 数据

- STEP 1: 在 Solution Explorer 中，双击 PubsDataSet.xsd 文件以查看 DataSet Designer。
- STEP 2: 右键单击表名并选择 Preview Data。
- STEP 3: 单击 Preview 按钮（图 3.10）。

### Figure 3.10

在 DataSet Designer 中右键单击表名并选择 Preview Data 以预览 DataSet 的数据。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_139_1.png)

## View the Designer's Code

查看设计器的代码

您可以通过几种方式查看设计器生成的代码。您可以在 Solution Explorer 中选择 Show All Files 后出现的 DataSetName.Designer.vb 文件中显示代码。要查看代码的执行情况，请在程序中 Form_Load 事件处理程序中包含 Fill 方法的代码行上设置断点。运行程序并使用 Step Into 命令（F8 或 F11，具体取决于键盘设置）逐步进入代码。

## Displaying Data in Individual Fields—Step-by-Step

在单个字段中显示数据—逐步操作

您可以在文本框、标签或其他类型的控件中轻松显示单个字段。接下来您将修改逐步程序以在文本框中显示数据。当您从 Data Sources 窗口选择一个表时，右侧会出现一个下拉箭头。从下拉菜单中，您可以选择 DataGridView，即默认值，或 Details。显示详细信息的默认控件是文本框。

> Note: 必须在设计器中打开一个窗体，Data Sources 窗口中的下拉箭头才会出现。

## Convert from a Grid to Details View

从网格转换为详细信息视图

- STEP 1: 从窗体中删除数据网格。
- STEP 2: 单击 Data Sources 窗口中 employee 表旁的向下箭头；选择 Details（图 3.11）。请注意，表的图标已更改以匹配视图。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_140_0.png)

> Note: 如果向下箭头未出现，请单击 Document 窗口中的窗体，然后再次单击 Data Sources 窗口中的表名。

- STEP 3: 将表拖到窗体左上角附近的位置。
- STEP 4: 按需更改标签上的文本。
- STEP 5: 运行项目。

每个字段都显示在文本框中（图 3.12），日期除外，日期默认使用 DateTimePicker 控件。在下一节中，您将学习如何为每个字段选择控件类型。

## Selecting the Control Type for Details View

选择详细信息视图的控件类型

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_141_0.png)

您可以在详细信息视图中为每个数据库字段选择使用的控件类型。您还可以更改默认值；例如，您可以设置文本字段的默认值为始终使用标签而不是文本框。请注意，您必须在将表拖到窗体之前进行选择；放置到窗体上后，如果不删除控件并重新开始，就无法更改控件类型。

要在当前项目中更改字段的控件类型，请在 Data Sources 窗口中选择数据库字段。然后展开单个字段的列表（图 3.13）并进行选择。您可以更改一个或多个字段的控件类型。然后确保表的选择为 Details View 并将表拖到窗体上。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_141_1.png)

要选择列表中没有的控件类型，请选择 Customize 并在所需控件的框中放置一个复选标记。例如，您可能希望将掩码文本框、复选框或图片框添加到控件类型列表中。如果您的应用程序显示特殊格式的字段，例如社会安全号码、电话号码或日期，您可以使用掩码文本框，然后设置 Mask 属性来处理显示的格式。

