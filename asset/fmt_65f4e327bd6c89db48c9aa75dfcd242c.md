
```csharp
public bool IsPresent(Control control, string name)
{
    if (control.GetType() == "System.Windows.Forms.TextBox")
    {
        TextBox textBox = (TextBox)control;
        if (textBox.Text == "")
        {
            MessageBox.Show(name + " is required.", "Entry Error");
            textBox.Focus();
            return false;
        }
    } else if (control.GetType() == "System.Windows.Forms.ComboBox")
    {
        ComboBox comboBox = (ComboBox)control;
        if (comboBox.SelectedIndex == -1)
        {
            MessageBox.Show(name + " is required.", "Entry Error");
            comboBox.Focus();
            return false;
        }
    }
    return true;
}

private void fillToolStripButton_Click(object sender, EventArgs e)
{
    try {
        this.customersTableAdapter.Fill(this.mmBooksDataSet);
    } catch (SqlException ex)
    {
        MessageBox.Show("Database error # " + ex.Number +
            ": " + ex.Message, ex.GetType().ToString());
    }
}
```

图 19-8 增强型客户维护应用程序（3 部分中的第 3 部分）

# 如何使用 DataGridView

在第 18 章中，你学习了如何使用 `DataGridView` 控件处理数据。现在，你将学习对 `DataGridView` 控件进行某些操作。

## 修改 DataGridView 的属性

当你使用 `DataGridView` 控件时，你可能需要自定义它的外观。为了实现这一点，你可以使用属性窗口。

要修改 `DataGridView` 控件的常用属性，你可以使用它的智能菜单（smart menu），如图 19-9 所示。要编辑列，可以点击“编辑列”（Edit Columns）命令来显示“编辑列”对话框。

要防止用户添加、更新或删除显示在 `DataGridView` 中的数据，可以取消勾选“启用添加”（Enable Adding）、“启用编辑”（Enable Editing）或“启用删除”（Enable Deleting）框。要允许用户通过拖动重新排列列，可以勾选“启用重排序”（Enable Reordering）。

### DataGridView 的智能菜单

![](img/3148667e42d4db35b3d08576aaa1fa01_622.png)

#### 说明

- 你可以使用 `DataGridView` 控件的智能菜单来编辑它的常用属性。
- 要编辑列，点击“编辑列”命令来显示“编辑列”对话框。然后你可以按照图中所示进行操作。
- 要防止用户添加、更新或删除显示在 `DataGridView` 中的数据，可以取消勾选“启用添加”、“启用编辑”或“启用删除”框。
- 要允许用户通过拖动重新排列列，可以勾选“启用重排序”复选框。
- 你可以使用属性窗口编辑 `DataGridView` 控件的其他属性。

图 19-9 修改 DataGridView 的属性

## 如何编辑 DataGridView 的列

图 19-10 显示如何使用“编辑列”对话框编辑 `DataGridView` 的列。在此对话框中，你可以通过选择列并点击“删除”（Remove）按钮来删除列。你还可以通过选择想要移动的列并点击列表右侧的上下箭头来更改列的顺序。

最后，你可以使用此对话框中的“添加”（Add）按钮向网格添加列。如果你删除了某个列又决定需要包含它，可能需要这样做。如果你想知道如何操作，请查看 Visual Studio 帮助。

一旦按照正确的顺序显示了列，就可以点击“添加”按钮将列绑定到网格。通过选择列，可以在“绑定列属性”窗口编辑该列的属性。例如，对于图中所示的每个列，我在列名的两个单词之间添加了空格。我更改了 `HeaderText` 属性以添加 `InvoiceID`、`SalesTax` 和 `Shipping` 列的宽度，并对 `InvoiceID` 列以外的所有列应用了适当的格式。

` 标签，我将根据你的要求将其整合并作为一个完整的翻译输出。以下是为你翻译的中文内容：

# 编辑 DataGridView 控制列的对话框

编辑列：

![](img/3148667e42d4db35b3d08576aaa1fa01_624_0.png)

## 列的常用属性

| 属性 (Property) | 说明 (Description) |
| --- | --- |
| HeaderText | 显示在列标题中的文本。 |
| Width | 用于列宽的像素数。 |
| DefaultCellStyle | 应用到单元格的样式。可以使用对话框设置颜色、格式和对齐等样式元素。 |
| ReadOnly | 决定列数据是否可以修改。 |
| SortMode | 决定网格数据是否根据列值排序以及如何执行排序。默认选项是 Automatic（自动），它使用内置排序机制。要提供自定义排序，选择 Programmatic（程序化）。要关闭排序，选择 NotSortable（不可排序）。 |

### 说明

- 你可以使用“编辑列”对话框来控制网格中显示哪些列并编辑这些列的属性。要显示此对话框，请从控件智能标记菜单中选择“编辑列”命令。
- 要从网格中删除列，选择该列并点击“删除”按钮。
- 要向网格中添加列，选择“添加”按钮并完成弹的对话框。此对话框允许你对列进行绑定和取消绑定操作。
- 要更改列的顺序，选择你想要移动的列，并点击列列表右侧的向上或向下箭头。
- 要编辑列的属性，选择该列并使用“绑定列（Bound Column）”窗口编辑属性。

图 19-10 如何编辑 DataGridView 控制的列

## 如何格式化 DataGridView 控制列中的数据

要格式化 `DataGridView` 控制的列，你可以使用图 19-11 所示的两个对话框。`CellStyle` 对话框允许你指定列的常规外观，包括字体和颜色。你还可以使用此对话框指定在空值处处要显示的值（默认为空字符串）以及列的布局。例如，在图中，你可以看到 `Alignment` 属性已设置为 `Middle`（居中）。

要格式化在列中显示的数据，可以使用 `Format String`（格式字符串）对话框。从此对话框中选择一种格式，然后输入任何其他选项。在图中，选中了 `Currency`（货币）格式，并使用了默认的小数位数（2）。当你接受此格式时，格式代码会被分配给 `CellStyle` 对话框中的 `Format` 属性，如此处所示。当然，如果你已经知道所需的格式代码，可以直接输入到 `CellStyle` 对话框中。

# 格式化 DataGridView 控制列的对话框

![](img/3148667e42d4db35b3d08576aaa1fa01_626_0.png)

### 说明

- 要显示 `CellStyle` 对话框，点击在“列”对话框中选择 `DefaultCellStyle` 属性时出现的省略号按钮。
- 要对列应用格式，选择 `Format` 属性，然后点击省略号按钮以显示 `Format String` 对话框。从列表中选择你需要的格式，并输入列表右侧出现的任何选项。

图 19-11 如何格式化 DataGridView 控制列中的数据

## 如何使用 DataGridView 控制创建主/从表（Master/Detail form）

显示主表和相关表数据的表单通常称为主/从表。图 19-12 显示了如何使用 `DataGridView` 控制创建主/从表。在此示例中，主表是 `Customers`（客户）表，相关表是 `Invoices`（发票）表。

你在图中首先应该的是数据源（Data Sources）窗口。虽然你预计此表单的数据源应包含 `Customers` 和 `Invoices` 表，但 `Invoices` 表在数据源窗口中出现了两次。首先，它与 `Customers` 表分开显示；其次，它作为 `Customers` 表的从属表显示。这表明 `Customers` 和 `Invoices` 表之间存在一对多的对应关系。这种关系基于每张表中的 `CustomerID` 列，Visual Studio 使用该列来生成显示相应数据的 `DataGridView` 控制。

要创建一个显示与表单主表相关的表之数据的 `DataGridView` 控制，你只需将从属表拖到表单上即可。当你这样做时，Visual Studio 会生成 `DataGridView` 控制以及相应的 `BindingSource` 和 `Table` 对象。此外，它还会设置 `BindingSource` 对象的属性，以便显示来自相关表的数据。

为了理解其工作原理，此图还展示了实现 `DataGridView` 控件绑定的 `BindingSource` 对象属性。首先，`DataSource` 属性不是为命名数据集，而是为主表命名绑定源。其次，`DataMember` 属性不是为命名数据表，而是命名关联两个表的外键。例如，在图中，`invoicesBindingSource` 对象的 `DataSource` 属性被设置为 `customersBindingSource`，而 `DataMember` 属性被设置为名为 `FK_Invoices_Customers` 的外键。

当你创建主/从表时，应该意识到默认情况下所有行都是从从表中检索的。例如，由于此处显示的 Customer Invoices 表单允许用户显示任何客户的所有发票，因此当表单加载时，会检索所有客户的发票。如果 `Invoices` 表包含大量行数据，这可能不是你想要的结果。在这种情况下，你可以创建一个参数化查询，仅检索用户选择的客户的发票。你将在接下来的 Customer Invoice 应用程序中看到相关示例。

# 使用 DataGridView 控制显示相关表数据的表单

CustomerDisplay - Microsoft Visual Studio

![](img/3148667e42d4db35b3d08576aaa1fa01_628_0.png)

# 用于显示相关表数据的两个 BindingSource属性

| 属性 (Property) | 说明 (Description) |
| --- | --- |
| DataSource | `BindingSource` 对象的数据源。要显示来自表单主表相关表的数据，此属性应设置为主表的 `BindingSource` 对象。 |
| DataMember | `BindingSource` 对象的数据源的子列表。要显示来自表单主表相关表的数据，此属性应设置为关联两个表的外键。 |

# invoicesBindingSource 对象的属性设置

| 属性 (Property) | 设置 (Setting) |
| --- | --- |
| DataSource | `customersBindingSource` |
| DataMember | `FK_Invoices_Customers` |

### 说明

- 如果一个表与另一个表存在一对多的关系，该表会在数据源窗口中作为主表的从属显示。然后，你可以将从属表拖到表单上，创建一个 `DataGridView` 控制，用于显示从属表中与主表当前行相关的行。

图 19-12 如何使用 DataGridView 控制创建主/从表

## 客户发票显示应用程序

现在你已经学习了处理 `DataGridView` 视图控件的一些额外技能，准备好查看一个使用了其中一些技能的客户发票显示应用程序了。

### 用户界面

图 19-13 展示了 Customer Invoice 应用程序的用户界面。如你所见，此应用程序由单个表单组成。此表单允许通过在工具栏中输入客户 ID 并点击“Get Customer”按钮来检索客户数据。客户数据显示在表单的文本框中，客户的发票显示在 `DataGridView` 控制中。注意，该控件的属性已设置好，允许用户添加、编辑或删除发票。

### 数据集架构

图 19-14 显示了此应用程序的数据集架构。正如你所期的，此架构包含了应用程序使用的两个表。这里最需要注意的是为每个表适配器创建的 `FillCustomerID` 查询。这些查询用于根据用户输入的客户 ID 检索相应数据。但请注意，当你使用关联了 `Customers` 和 `Invoices` 表的主/从表时，不需要 `Invoices` 表的 `FillCustomerID` 查询。对于此应用程序，`FillCustomerID` 查询仅用于提高应用程序的效率。你将在后续代码中看到如何使用该查询。你可以通过完成本文末的练习 19-2 来获得实践经验。

### Customer In 表的代码

图 19-15 展示了 Customer In 表的代码。你首先应该知道此表单不包含 `Load` 事件处理程序。由于由于，当应用程序启动时没有数据加载到数据集中。相反，当用户输入客户 ID 并点击“Get Customer”按钮时，将使用 `Customers` 表适配器的 `FillCustomerID` 查询将该客户的行加载到表中。此外，该客户的任何发票将使用 `Invoices` 表适配器的 `FillCustomerID` 查询加载到 `Invoices` 表中。你可以在此图事件处理程序中看到实现此操作的代码。

# 第 19 章 如何使用绑定控件和参数化查询

## 客户发票表

![](img/3148667e42d4db35b3d08576aaa1fa01_630_0.png)

### 描述

- 客户发票表是一个主从（Master/Detail）表单，用于显示所选客户的发票。为了提高效率，该表单在加载时不会检索任何数据。相反，当用户输入客户编号时，将检索该客户的客户信息和发票数据。
- 由于此应用程序不允许用户添加、修改或删除发票，因此从客户发票表中省略了绑定导航工具栏（binding navigator toolbar）。

图 19-13 发票显示应用程序的用户界面

## 数据集架构

![](img/3148667e42d4db35b3d08576aaa1fa01_631_0.png)

### 描述

- `MMABooks` 数据集定义了此应用程序使用的两个表：`Customers`（客户）和 `Invoices`（发票）。
- `Customers` 表适配器的 `FillByCustomerID` 查询用于检索显示在客户发票表上的客户数据。该查询基于用户在表单顶部工具栏中输入的客户 ID。
- `Invoices` 表适配器的 `FillByCustomerID` 查询用于检索显示在客户发票表上的发票数据。该查询同样基于用户在表单顶部工具栏中输入的客户 ID。

图 19-14 发票显示应用程序的数据集架构

## 客户发票表的代码

### 描述

- 此表所需的唯一代码是检索客户和发票数据的代码。当用户在客户发票表上输入客户 ID 并点击“Get Customer”（获取客户）按钮时，将执行此代码。

![](img/3148667e42d4db35b3d08576aaa1fa01_632_0.png)

### 观点

现在你已经完成了这一章，你应该能够使用数据源和数据集来开发大量的数据库应用程序。你还应该意识到你可以多快地完成这些原型。但如果你进行随后的练习（这些练习将引导你从零开始开发应用程序），你将开始发现使用数据源并不像表面看起来那么简单。因如此，你可能希望使用其他技术来开发更复杂的数据库应用程序。在下一章中，你将学习通过编写自己的 ADO.NET 代码来开发应用程序的基础。

## 术语

- 参数化查询 (parameterized query)
- 主从表 (Master/Detail form)

## 练习 19-1 构建客户维护应用程序

本练习将引导你开发图 19-8 中的应用程序。通过实践将学到很多。

### 构建用户界面

1. 在 `C:\C# 2010\Chapter 19` 目录下创建一个新项目 `CustomerMaintenance`。然后，创建一个包含 `Customers` 和 `States` 表中所有列的数据源。
2. 将与 `Customers` 表中 `State` 列关联的控件更改为组合框（combo box）。然后，将 `Customers` 表拖到表单上以生成详细控件，在顶部留出足够的空间放置两个工具栏。重新排列控件并更改任何必要的属性，使这些控件看起来与图 19-8 中的样式一致。
3. 使用 19-2 中的过程，将表单上的 State 组合框绑定到数据源中的 `States` 表。然后，将组合框的 `DropDownStyle` 属性设置为 `DropList (DataBindings)`，将 `Text` 属性设置为 `None`。
4. 测试应用程序以查看此用户界面如何工作。如果第一个客户显示的州（state）不正确，是因为 `Customers` 表在 `States` 表之前加载了。这意味着第一个客户在应用 State 组合框定义的绑定之前显示了。要修正此问题，结束应用程序并切换表单 `Load` 事件处理程序中的语句，以便先加载 `States` 表。
5. 再次运行应用程序以查看工作效果。然后，使用组合框更改一个 State 条目。结束应用程序，并检查为表单生成的其他代码。

### 添加参数化查询

6. 使用 19-4 中的过程添加一个名为 `FillByCustomerID` 的参数化查询，用于查找特定客户 ID 的客户行。然后，请注意已添加到表单上的工具栏。现在，检查添加到应用程序中的代码以及该应用程序的架构。
