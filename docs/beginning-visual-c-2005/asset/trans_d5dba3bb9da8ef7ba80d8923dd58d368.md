

## 第22章

所有标题单元格的高度都会调整以适应最大单元格内容。如果您只想调整特定列标题的高度，可以使用接受指定要调整列索引的参数的重载版本函数。

如果您不想让行或列标题可见，可以通过将控件的 RowHeadersVisible 属性和/或 ColumnHeadersVisible 属性的值设置为 false 来使其消失。

## 格式化列

第一列包含对 DateTime 对象的句柄。应用程序目前只是调用对象的 ToString() 函数来获取要显示的内容，但您可以做得更好。您可以为列的 DefaultCellStyle 属性设置 Format 属性，然后此格式规范将用于显示单元格的内容：

```
dataGridView->Columns[0]->DefaultCellStyle->Format = L"y";
```

这将 Format 属性设置为包含 DateTime 对象的 y 格式规范的字符串，该规范以月加年形式呈现对象的简短日期形式。您可以使用几种其他 DateTime 对象的格式说明符。例如，D 显示日期、月份和年份，而 F 和 F 显示时间以及日期。

如果您已将所有这些代码添加到 Form1 类构造函数中，现在是戴上墨镜并试用示例的时候了。如果编译并运行它，您应该会看到类似图 22-7 所示的应用程序窗口。

![](img/2359b0c604600c58fba3539c738a356e_1147_0.png)

图 22-7

我在图 22-7 中调整了窗口的宽度以显示更多列。不幸的是，在书中应用程序窗口以灰色调出现，但您应该在屏幕上看到它以绚丽的彩色显示。

如果您单击控件左侧的其中一个行标题，您应该会看到行被高亮显示，如图 22-8 所示。

## 在 Windows Forms 应用程序中访问数据源

![](img/2359b0c604600c58fba3539c738a356e_1148_0.png)

行中单元格的背景颜色是您为控件的 DefaultCellStyle 属性的 `SelectionBackColor` 属性设置的颜色。您也可以通过单击来选择单个单元格，单元格的背景颜色会变为绿色。

基于任何给定列对行进行排序的能力已内置于 `DataGridView` 控件中。您可以尝试单击列标题，查看按您选择的列对行进行排序。如果再次单击列标题，行将按相反顺序排列。您可以为列中的每一列添加工具提示以解释排序的可能性。将此循环添加到 `Form1` 类构造函数即可实现：

```
for each(DataGridViewColumn^ column in dataGridView->Columns)
    column->ToolTipText = L"Click to\nsort rows";
```

`Columns` 属性值是一个列集合，其中每个列都是 `DataGridViewColumn` 类型的对象。循环遍历每一列并设置 `ToolTipText` 属性的值。图 22-9 显示了其中一个列标题的工具提示。

![](img/2359b0c604600c58fba3539c738a356e_1148_1.png)

这些工具提示仅在鼠标光标位于列标题单元格上方时显示。您可以通过为单元格对象设置 ToolTipText 属性为任何显示数据的单元格设置工具提示。

## 自定义交替行

当您显示许多外观相似的行时，很难看出您正在查看哪一行。您可以通过为控件对象的 AlternatingRowsDefaultCellStyle 属性的 BackColor 属性设置不同的颜色来为交替行着色以帮助克服此问题：

```
dataGridView->AlternatingRowsDefaultCellStyle->BackColor = Color::Blue;
```

您可能希望更改 AlternatingRowsDefaultCellStyle 属性的 ForeColor 属性以获得文本与背景之间合理的对比度：

```
dataGridView->AlternatingRowsDefaultCellStyle->ForeColor = Color::White;
```

现在行以粉色和蓝色交替显示，如图 22-10 所示（当然在灰色调中，因为书中没有颜色）。

![](img/2359b0c604600c58fba3539c738a356e_1149_0.png)

图 22-10

现在很容易区分行，并且白色文本在蓝色背景上清晰可见。您仍然可以通过单击行标题来选择一行，并看到所选行呈绿色。单击列标题左侧末端的单元格将选择所有行。

## 动态设置单元格样式

通过处理 DataGridView 控件的事件，您有几种可能性来更改单元格的外观。DataGridView 控件的 CellFormatting 事件在单元格内容需要格式化以便显示时触发，因此通过为此事件添加处理程序，您可以根据内容调整任何单元格的外观。我现在想探讨您如何扩展 Ex22_02 来实现这一点。

## 在 Windows Forms 应用程序中访问数据源

例如，假设在 Ex22_02 中您希望将 Date 列中单元格的背景颜色设置为红色，如果日期早于 2000 年。请记住，从第 9 章事件的讨论中，要注册事件处理程序，您将委托的实例添加到事件。CellFormatting 事件的委托类型为 DataGridViewCellFormattingEventHandler，它期望两个参数：第一个参数的类型为 Object^，标识事件的来源，第二个参数是对 DataGridViewCellFormattingEventArgs 类型对象的句柄。

传递给 CellFormatting 事件处理程序的第二个参数通过以下属性提供有关事件的附加信息：

| 属性 | 描述 |
|----------|-------------|
| Value | 值是对正在格式化的单元格内容的句柄。 |
| DesiredType | 值是对 Type 类型对象的句柄，标识正在格式化的单元格内容的<|message|>。 |
| CellStyle | 获取或设置与格式化事件关联的单元格样式，因此值是对 DataGridViewCellStyle 类型对象的句柄。 |
| ColumnIndex | 值是正在格式化的单元格的列索引。 |
| RowIndex | 值是正在格式化的单元格的行索引。 |
| FormattingApplied | 值 true 或 false 表示是否已应用单元格内容的格式化。 |

这些属性使您能够了解有关正在格式化的单元格所需的所有信息——单元格的行和列、当前生效的样式以及单元格的内容。

处理 CellFormatting 事件的第一步是为其定义一个处理程序函数。处理程序代码需要尽可能简短高效，因为该函数在控件的每个单元格需要格式化时都会被调用。您可以将以下函数添加到 Form1 类中作为 CellFormatting 事件的处理程序函数：

```
private:
void OnCellFormatting(Object^ sender, DataGridViewCellFormattingEventArgs^ e)
{
// Check if it's the date column
if(dataGridView->Columns[e->ColumnIndex]->Name == L"Date")
{
// If the cell content is not null and the year is less than 2000
// Set the background to red
if(e->Value != nullptr && safe_cast<DateTime^>(e->Value)->Year < 2000)
{
e->CellStyle->BackColor = Color::Red;
e->FormattingApplied = false; // We did not format the data
}
}
}
```

您首先检查当前列是否为 Date 列，因为您只对修改该列中的单元格感兴趣。对于 Date 列中的单元格，您检查单元格内容是否确实存在，并且如果存在 DateTime 对象，则年份是否小于 2000。在这种情况下，您将 CellStyle 属性返回的对象 的 BackColor 属性设置为 Color::Red。您将 FormattingApplied 属性设置为 false 以指示您未格式化内容。这不是严格必要的，因为该值最初为 false。如果您在处理程序中负责格式化内容，则会将其设置为 true，这将防止使用 Format 属性的值进行后续格式化。

要将此函数注册为 CellFormatting 事件的处理程序，请将以下语句添加到 Form1 类构造函数的末尾：

```
dataGridView->CellFormatting +=
    gcnew DataGridViewCellFormattingEventHandler(this, &Form1::OnCellFormatting);
```

委托的第一个参数是对包含处理程序函数的对象的句柄，即当前的 Form1 对象。第二个参数是事件新处理程序的函数的地址。如果重新编译示例并再次执行它，您应该会看到 Date 列中所有包含 2000 年之前日期的单元格的背景颜色为红色。

DataGridView 控件定义了 CellMouseEnter 和 CellMouseLeave 事件，当鼠标光标进入或离开单元格时触发。您可以为这些事件实现处理程序，通过更改其背景颜色来突出显示鼠标光标所在的单元格。您可以在 CellMouseEnter 事件的处理程序中设置新的背景和前景颜色，并在 CellMouseLeave 事件的处理程序中恢复原始颜色。这其中有一些棘手的地方，因此值得具体研究。

### 试一试 高亮鼠标光标下的单元格

这将是对 Ex22_02 的扩展，包括最新的 CellFormatting 事件处理程序的添加，而不是从头开始的新示例。您需要将旧的背景和前景颜色存储在某个地方，因此将以下私有数据成员添加到 Form1 类：

```
// Stores for old cell colors in mouse enter event handler
// for restoring later in mouse leave event handler
private: Color oldCellBackColor;
private: Color oldCellForeColor;
```

您应该在 Form1 类构造函数中将两者都初始化为 Color::Empty。

CellMouseEnter 或 CellMouseLeave 事件的委托的第一个参数是对引发事件的对象的句柄，即 DataGridView 控件。两个委托的第二个参数都是对 DataGridViewCellEventsArg 类型对象的句柄，提供有关事件的附加信息。此对象具有 RowIndex 和 ColumnIndex 属性，这些属性的值使您能够找到鼠标进入或离开的单元格；您可以使用前者索引 Rows 属性以选择包含单元格的行，并使用后者索引 Cells 属性以在行内选择单元格本身。需要注意一件事——当鼠标光标位于列标题行时，RowIndex 属性的值为 -1，而当鼠标光标位于行标题上方时，ColumnIndex 属性的值为 -1。您需要检查这些可能性，因为使用负索引对 Rows 属性值进行操作会引发异常，使用负值对行的 Cells 属性进行索引也会引发异常。

