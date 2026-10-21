

## 在 Windows Forms 应用程序中访问数据源

你现在可以在 Form1 类中为 CellMouseEnter 事件定义一个私有处理函数，如下所示：

```
```cpp
private:
void OnCellMouseEnter(Object^ sender, DataGridViewCellEventArgs^ e)
{
  if(e->ColumnIndex >= 0 && e->RowIndex >= 0)   // Verify indexes non-negative
  {
    // Identify the cell we have entered
    DataGridViewCell^ cell =
              dataGridView->Rows[e->RowIndex]->Cells[e->ColumnIndex];

    // Save any old colors that are set
    oldCellBackColor = cell->Style->BackColor;
    oldCellForeColor = cell->Style->ForeColor;

    // Set highlight colors
    cell->Style->BackColor = Color::White;
    cell->Style->ForeColor = Color::Black;
  }
}
```
```

在确定两个索引值都为非负后，你获取鼠标光标进入的单元格的句柄。你通过先使用参数 e 的 RowIndex 属性值索引控件的 Rows 属性来选择行；然后使用 e 的 ColumnIndex 属性索引该行的 Cells 属性来在行内选择单元格。

获得单元格句柄后，很容易保存单元格的 Style 属性中 BackColor 和 ForeColor 属性的值，并设置新颜色以将单元格显示为白底黑字。Style 属性可能未被设置，在这种情况下访问该属性值会创建一个新的 DataGridViewCellStyle 对象作为值，其 BackColor 和 ForeColor 属性值为 Color::Empty。如果单元格的 Style 属性已被设置，你将获得包含为其设置的所有属性的对象。

CellMouseEnter 事件的处理函数必须将颜色恢复到原来的状态。你可以像这样实现此处理函数：

```
```cpp
private:
void OnCellMouseLeave(Object^ sender, DataGridViewCellEventArgs^ e)
{
  if(e->ColumnIndex >=0 && e->RowIndex >=0)
  {
    // Identify the cell we are leaving
    DataGridViewCell^ cell =
              dataGridView->Rows[e->RowIndex]->Cells[e->ColumnIndex];

    // Restore the saved color values
    cell->Style->BackColor = oldCellBackColor;
    cell->Style->ForeColor = oldCellForeColor;

    // Reset save stores to no color
    oldCellForeColor = oldCellBackColor = Color::Empty;
  }
}
```
```

## 第 22 章

再次在执行任何操作之前检查索引值是否为非负。与之前的处理函数中一样，在识别出单元格后，你将保存的颜色恢复到单元格的 Style 属性中。单元格的前景色和背景色的确定方式是通过你之前看到的优先级列表。如果单元格的 Style 属性未被设置，你恢复的值为 Color::Empty，在确定单元格颜色时会被忽略。因此，原来的颜色适用。如果 Style 属性已定义并设置了 ForeColor 和 BackColor 属性，则这些是你恢复的值，它们决定了单元格的格式颜色。

要注册函数处理程序，将以下语句添加到 Form1 类构造函数的末尾：

```
dataGridView->CellMouseEnter +=
    gcnew DataGridViewCellEventHandler(this, &Form1::OnCellMouseEnter);
dataGridView->CellMouseLeave +=
    gcnew DataGridViewCellEventHandler(this, &Form1::OnCellMouseLeave);
```

相同的委托适用于所有单元格事件，因此你使用 DataGridViewCellEventHandler 委托注册两个处理程序。

如果重新编译程序并再次运行，你应该可以看到单元格高亮的效果，如图 22-11 所示。

![](img/2359b0c604600c58fba3539c738a356e_1153_0.png)

图 22-11

嗯，它确实有效——至少大部分时间是这样。然而，Date 列中的红色单元格并未被高亮，那么发生了什么？

事件序列是问题的根源。CellFormatting 事件在 CellMouseEnter 事件之后触发，因此设置背景色为红色的处理函数具有最后决定权，并覆盖了 CellMouseEnter 事件处理函数的效果。你希望发生的是 CellFormatting 事件处理函数能够识别单元格已被高亮，并在这种情况下不执行任何操作。你可以通过在 Form1 类中添加另一个成员来存储当前被高亮的单元格的句柄来实现这一点：

```
private: DataGridViewCell^ highlightedCell;    // The currently highlighted cell
```

你还应该在 Form1 类构造函数中将此新成员初始化为 nullptr。

## 在 Windows Forms 应用程序中访问数据源

你现在需要修改 CellMouseEnter 事件的处理程序，以将高亮单元格的句柄存储在新成员中：

```
void OnCellMouseEnter(Object^ sender, DataGridViewCellEventArgs^ e)
{
    if(e->ColumnIndex >= 0 && e->RowIndex >= 0)    // Verify indexes non-negative
    {
        // Identify the cell we have entered
        highlightedCell = dataGridView->Rows[e->RowIndex]->Cells[e->ColumnIndex];

        // Save any old colors that are set
        oldCellBackColor = highlightedCell->Style->BackColor;
        oldCellForeColor = highlightedCell->Style->ForeColor;

        // Set highlight colors
        highlightedCell->Style->BackColor = Color::White;
        highlightedCell->Style->ForeColor = Color::Black;
    }
}
```

你可以将 CellMouseLeave 事件处理程序的实现更改为如下：

```
void OnCellMouseLeave(Object^ sender, DataGridViewCellEventArgs^ e)
{
    if(e->ColumnIndex >=0 && e->RowIndex >=0)
    {
        // Restore the saved color values
        highlightedCell->Style->BackColor = oldCellBackColor;
        highlightedCell->Style->ForeColor = oldCellForeColor;

        // Reset save stores to no color
        oldCellForeColor = oldCellBackColor = Color::Empty;

        highlightedCell = nullptr;    // Reset highlighted cell handle
    }
}
```

你不再需要确定单元格句柄，因为它可在 Form1 类的 highlightedCell 成员中使用。你甚至不必检查它，因为 CellMouseLeave 事件必须始终由 CellMouseEnter 事件先行。你将高亮单元格的句柄重置为 null，因为这是良好的编程实践。

你现在可以修改 CellFormatting 事件的处理程序：

```
void OnCellFormatting(Object^ sender, DataGridViewCellFormattingEventArgs^ e)
{
    // Check whether the cell is highlighted
    if(dataGridView->Rows[e->RowIndex]->Cells[e->ColumnIndex] == highlightedCell)
        return;

    // Check if it's the date column
    if(dataGridView->Columns[e->ColumnIndex]->Name == L"Date")
    {
```

```
// If the cell content is not null and the year is less than 2000
// Set the background to red
if(e->Value != nullptr && safe_cast<DateTime^>(e->Value)->Year < 2000)
{
    e->CellStyle->BackColor = Color::Red;
    e->FormattingApplied = false;      // We did not format the data
}
}
```

如果重新构建示例，你现在应该可以看到所有单元格都被高亮。

你现在应该对如何为 DataGridView 控件实现事件处理程序有了一个很好的概念。有大量其他事件，因此你有很大的空间可以动态地做更多事情，以根据应用程序需求自定义控件。

## 使用绑定模式

在绑定模式下，DataGridView 控件显示的数据源由其 DataSource 属性的值指定，通常你可以将其设置为实现以下任何接口的 ref 类对象的类型：

| 接口 | 描述 |
|---|---|
| System::Collections::IList | 实现此接口的类表示可通过单个索引访问的对象集合。所有 C++/CLI 一维数组都实现此接口，因此 DataGridView 对象可以使用任何一维数组作为显示数据的来源。IList 接口继承了在 System::Collections 命名空间中定义的 ICollection 和 IEnumerable 接口类的成员。 |
| System::ComponentModel::IListSource | 实现此接口的类将数据作为 IList 对象的列表提供。该列表可以包含也实现 IList 接口的对象。 |
| System::ComponentModel::IBindingList | 此接口类扩展了 IList 接口类，以允许处理更复杂的数据绑定情况。 |
| System::ComponentModel::IBindingListView | 为 IBindingList 接口添加排序和筛选功能。你将在本章稍后遇到的 BindingSource 类定义了一个实现此接口的控件。 |

