

## 第 18 章 如何与数据源和数据集工作 559

## 产品维护应用程序的用户界面

![](img/3148667e42d4db35b3d08576aaa1fa01_578_0.png)

## Visual Studio 生成的代码

```csharp
private void FormLoad(object sender, EventArgs e)
{
// TODO: 这行代码将数据加载到
// 'mMBooksDataSet.Products' 中。
// 你根据需要移动或删除它。
this.productsTableAdapter.Fill(this.mMBooksDataSet);
}
```

```csharp
private void voidProductsBindingNavigatorSaveItem_Click(object sender, EventArgs e)
{
    this.Validate();
    this.productsBindingSource.EndEdit();
    this.tableAdapterManager.UpdateAll(this.mMBooksDataSet);
}
```

## Fill 方法的语法

```csharp
tableAdapter.Fill(dataSet.TableName)
```

## UpdateAll 方法的语法

```csharp
tableAdapterManager.UpdateAll(dataSet)
```

## 描述

- 当你将数据源拖到表单上时，Visual Studio 会自动生成代码。如有必要，你可以编辑这些代码。
- 生成的代码使用为生成的 TableAdapter 对象的 `Fill` 方法从数据库读取数据，并使用为数据集生成的 TableAdapterManager 对象的 `UpdateAll` 方法将数据写入数据库。它使用 BindingSource 的 `EndEdit` 方法将对当前行做的任何更改保存到数据集中。
- `Validate` 方法会导致失去焦点的控件触发 `Validating` 和 `Validated` 事件。你可以使用 `Validating` 事件对表单执行任何需要的数据验证。
- DataGridView 控件的用户可以通过点击列标题并拖动列分隔符向左或向右对行进行排序。如果启用选项，他们还可以通过拖动列来重新排列顺序（见图 19-9）。

图 18-9 使用 DataGridView 控件的产品维护应用程序

对于你开发的任何生产应用程序，都需要添加适当的异常处理代码，以防止它们崩溃。你将在本章的后续部分学习如何这样做。

## 如何更改与数据源关联的控件

如果 DataGridView 控件不适用于你的应用程序，你可以如图 18-10 所示，将数据源的列绑定到单个控件上。在这里，数据源由 Customers 表中的列组成。

要将表中的列与单个控件关联，可以在“数据源（Data Sources）”窗口选择表时，从下拉列表中选择“详细信息（Details）”选项。如图图中所示。然后，如果你将表从“数据源”窗口拖到表单上，Visual Studio 会为表中的每个列生成一个标签（Label）和一个绑定的控件。

对于大多数字符串和数字型列，Visual Studio 会生成一个 TextBox 控件。Customers 表就是如此，正如你在下一张图中看到的。但是，如果你想更改与列关联的控件类型，可以从“数据源”窗口中选择该列，然后使用显示的下拉列表选择不同类型的控件。你可以在此图的第二个屏幕看到可用的控件列表。

## 如何更改数据表的默认控件

![](img/3148667e42d4db35b3d08576aaa1fa01_580_0.png)

## 如何更改数据表中列的默认控件

![](img/3148667e42d4db35b3d08576aaa1fa01_580_1.png)

- 默认情况下，数据表与 DataGridView 控件关联。要更改此设置以便表中的每列都显示在单独的控件中，请从表的下拉列表中选择“详细信息（Details）”。

- 默认情况下，数据表中大多数字符串和数字型列与 TextBox 控件关联。要更改此设置，请从列的下拉列表中选择你想使用的控件类型。

图 18-10 如何更改与数据源关联的控件

## 如何从数据源生成详细控件

如果你将与表关联的控件类型从 DataGridView 更改为详细信息（Details）”，并将该表从“数据源”窗口拖到表单上，Visual Studio 将向表单添加适当的控件，如图 18-11 所示。它会将控件绑定到表中的相应列，并为每个列添加一个 Label 控件以进行标识。例如，你可以看到 Visual Studio 为 Customers 表的六列中的每一列都添加了一个 TextBox 控件和一个 Label 控件。此外，它还添加了 DataSet、BindingSource、TableAdapter、TableAdapter 对象以及一个绑定导航工具栏，就像它生成 DataGridView 控件时一样。

当你使用文本框处理表中的数据时，每次只显示表的一行。然后，Visual Studio 使用简单数据绑定将每个文本框连接到单个列值。为了实现这一点，它将 `DataBindings` 集合中的 `Text` 属性设置为控件所绑定的数据列名。例如，在图中，你可以看到 `DataBindings` 集合的 `Text` 属性的下拉列表。它显示 Customer ID 框绑定到 `customersSource` 对象的 `CustomerID` 列。

一旦标签和文本框显示在表单上，你就可以对它们进行操作。例如，你可以看到 `DataBindings` 集合的 `Text` 属性的下拉列表。它显示 Customer ID 框绑定到 `customersSource` 对象的 `CustomerID` 列。你可以修改该标签的文本。如果你不想让用户向特定列输入数据，可以将该文本框的 `ReadOnly` 属性设置为 `True`。此外，如果你不想在该列上显示数据，可以编辑工具栏以移除添加、删除和更新按钮。你将在下一章学习如何这样做。

## 第 18 章 如何与数据源和数据集工作

## 将表拖到表单后的界面

![](img/3148667e42d4db35b3d08576aaa1fa01_582_0.png)

## 描述

- 当你将关联单个控件的表拖到表单上时，Visual Studio 会向表单添加适当的控件，如上所示。它会将控件绑定到表中的相应列，并为每个列添加一个标识它的 Label 控件。

- 为了在文本框中显示列的值，Visual Studio 会将 `DataBindings` 集合中的 `Text` 属性设置为该列名。这被称为*简单绑定*，因为控件仅绑定到一个列值。要更改此绑定，你可以使用上文所示 `Text` 属性下拉列表。

- 要在使用单个控件时禁用行的添加、删除或更新，可以从工具栏移除这些按钮。请参见第 19 章。

## 注意

- 当你将单个控件拖到表单时，不要将它们放在表单的顶部。工具栏会覆盖第一个标签和文本框，导致它们难以移动。

图 18-11 从数据源生成详细控件

## 使用 TextBox 控件的客户维护应用程序

图 18-12 显示了使用图中所示 Label 和 TextBox 控件的客户维护应用程序的用户界面。然而，我对这些控件进行了重新排列并做了更改。

首先，我将 City 文本框的标签改为“City, State, Zip”，并删除了 State 和 Zip Code 文本框的标签。接下来，我调整了文本框的大小，使其适用于要显示的数据。然后，我移动了 State 和 Zip Code 文本框，使其与 City 文本框水平对齐。最后，我将 Customer ID 文本框的 `ReadOnly` 属性设置为 `True`，以便用户无法向此控件输入数据，并将此文本框的 `TabStop` 属性设置为 `False`，使其不在制表顺序中。

此图还显示了客户维护应用程序的代码。如果你将此代码与图 18-9 中产品维护应用程序的代码进行比较，你会发现它们几乎相同。唯一的区别是，客户维护应用程序的代码处理 Customers 表、表适配器和绑定源，而不是 Products 表、表适配器和绑定源。

