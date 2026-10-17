
## 排序参数

- `SortField`、`SortField2` 和 `SortField3` 是可选 `Variant` 参数，指定您对 `FieldNumber`、`FieldNumber2` 和 `FieldNumber3` 使用的排序类型。对于美国，选项有字母排序（`SortFieldAlphanumeric`）、数字排序（`SortFieldNumeric`）和日期排序（`SortFieldDate`）。

- `SortOrder`、`SortOrder2` 和 `SortOrder3` 是可选 `Variant` 参数，指定 `FieldNumber`、`FieldNumber2` 和 `FieldNumber3` 的排序顺序。使用 `wdOrderAscending` 指定升序排序（默认）或使用 `wdOrderDescending` 指定降序排序。

- `CaseSensitive` 是一个可选 `Variant` 参数，设置为 `True` 指定区分大小写的排序。默认为 `False`。

- 接下来的五个参数（`BidSort`, `Ignore`, `IgnoreKashida`, `IgnoreDiritics`, `IgnoreHe`）用于特殊排序（例如从右向左语言、阿拉伯语和希伯来语）。

- `LanguageID` 是一个可选 `Variant` 参数，您可以使用它来指定排序的语言。您可以指定 `wdLanguageLithuanian`。对于默认语言排序，可以省略此项。

## 在表格中添加列

要添加列，使用对应 `Table` 对象的 `Collections` 的 `Add` 方法。`Add [BeforeColumn]` 方法对于 `Collections` 的语法如下：

```
expression.Add [BeforeColumn]
```

在这里，`expression` 是返回 `Collections` 对象的必要表达式，`BeforeColumn` 是一个可选 `Variant` 参数，指定要在其左侧插入新列的列。

以下示例使用 `Count` 属性检查活动文档中表格的列数。如果此表格少于五列，则将添加更多列直到列数达到五列。每个新列都将添加到表格现有最后一列的之前（左侧）。

```
With ActiveDocument.Tables(1)
.Select
```

## 删除表格中的列

要删除一列，请先识别该列（例如，在以下语句中使用数字 1），然后使用 `Delete` 方法。`Delete` 不接受任何参数。以下语句将删除由对象变量 `myTable` 引用的表格中的第一列：

```
myTable.Columns(1).Delete
```

## 设置列宽

你可以通过使用 `AutoFit` 方法、使用 `SetWidth` 方法或通过指定列的 `Width` 属性来设置列宽。

`AutoFit` 方法会自动调整每列的宽度，以适应其内容。`AutoFit` 不接受任何参数。以下语句使用 `AutoFit` 方法重新调整活动文档中第一个表格的每列宽度：

```
ActiveDocument.Tables(1).Columns.AutoFit
```

`SetWidth` 方法允许你设置一或多列的宽度，并指定表格中其他列随之如何变化。`SetWidth` 方法的语法如下：

```
expression.SetWidth ColumnWidth, RulerStyle
```

在这里，`expression` 是一个返回 `Columns` 集合或 `Column` 对象的表达式，该对象具有你想要设置的宽度。`ColumnWidth` 是一个所需的 `Single` 类型参数，以磅为单位指定列或若干列的宽度。`RulerStyle` 是一个所需的 `Long` 类型参数，指定调整列宽的方式：

- `wAdjust` 设置指定的宽度，根据需要将其他列向左或右移动。此参数在交互式操作中等同于按住 Shift 拖动列边界。
- `wAdjustFirstColumn` 将指定的宽度应用于第一个指定的列，仅根据需要调整该列右侧的许多列。例如，稍微加宽表格中的第一列会导致第二列发生变化，但保持第三列及后续列不变。大幅加宽第一列会导致 Word 自动换行第二列和第三列，而让第四列及后续列保持不变。此参数在交互式操作中等同于拖动列边界。
- `wAdjustProportional` 将指定的宽度应用于第一个指定的列，保持表格右边缘在原有位置，并按比例调整所有未指定的列以适应此变化。

## 操作表格

`wdAdjustSameWidth` 将指定的宽度应用于第一个指定的列，保持表格右边缘在原有位置，并将所有其他列调整为相同的宽度以适应此变化。此参数在交互式操作中等同于按住 Ctrl 拖动列边界。

以下语句将活动文档中第一个表格的第二列宽度设置为 50 磅，并按比例调整第二列右侧的列：

```
ActiveDocument.Tables(1).Columns(2).SetWidth ColumnWidth=50,
Ruler=wdAdjustProportional
```

`Width` 属性允许你更改列的宽度，而无需担心对其他列的影响。在此示例中，以磅为单位指定所需的宽度 `width=`：

```
ActiveDocument.Tables(11).Columns(44).Width = 100
```

## 选择列

要选择一列，请对相应的 `Column` 对象使用 `Select` 方法。`Select` 接受参数。以下语句选择文档 `Original.docm` 中第三个表格的第二列：

```
Documents("Original.docm").Tables(3).Columns(2).Select
```

## 在表格中添加行

要添加行，请对表格的 `Rows` 集合使用 `Add` 方法。`Add` 方法用于 `Rows` 集合的语法如下：

```
expression.Add [BeforeRow]
```

在这里，`expression` 是一个返回 `Row` 对象的表达式，`BeforeRow` 是一个可选参数，指定你想将新行添加到的行。如果你省略了 `BeforeRow`，VBA 将在表格最后一行之后添加新行。

以下语句向对象变量 `myTable` 引用的表格添加一个新行：

```
myTable.Rows.Add BeforeRow:=1
```

你还可以在当前选择位置向表格中插入行，请使用 `InsertRowsBelow` 或 `InsertRowsAbove` 方法。指定插入的行数。在此示例中，在当前选择下方插入了一行：

```
Selection.InsertRowsBelow 1
```

## 删除表格中的行

要删除某行，请对相应的 `Row` 对象使用 `Delete` 方法。`Delete` 方法不接受任何参数。以下语句将删除对象变量 `myTable` 引用的表格中的第一行：

```
myTable.Rows(1).Delete
```

## 设置一或多行的高度

你可以通过让 Word 自动设置行高来设置行高、使用 `SetHeight` 方法指定精确高度或最小高度，或者直接设置行或若干行的 `Height` 属性。

要自动设置行高，请将行的 `Height` 属性设置为 `wdRowHeightAuto`。随后，Word 会调整行的高度以适应内容最多的单元格。以下语句将活动文档中第四个表格的第二行的 `HeightRule` 属性设置为 `wdRowHeightAuto`：

```
ActiveDocument.Tables(4).Rows(2).HeightRule = wdRowHeightAuto
```

要为一或若干行指定精确高度或最小高度，请对行或若干行使用 `SetHeight` 方法。`SetHeight` 方法的语法如下：

```
expression.SetHeight Row, [HeightRule]
```

在这里，`expression` 是一个返回 `Row` 对象或 `Rows` 集合的表达式。`HeightRule` 是一个 `Variant` 类型参数，指定设置高度的规则：使用 `wdRowHeightAtLeast` 指定最小高度，或使用 `wdRowHeightExactly` 指定精确高度（`HeightRule` 的第三种设置为 `wdRowHeightAuto`）。

以下语句将删除活动文档第一行的第一个单元格，并将第一行的其他单元格左移以填充空隙：

```
ActiveDocument.Tables(1).Rows.Cells(1).Delete _nShiftCells:=wdDeleteCellsShiftLeft
```

对于使用用户在表格内进行选择的宏，你可能想在决定如何移动单元格之前，先确定选择包含多少行或多少列。下面的示例检查了选择内容的行数和列数。如果选择仅为一个单元格，或者选择位于一列中，代码将删除该单元格或单元格，并将行中的其他单元格向左移动。如果选择的是一列中的多个单元格，代码将删除这些单元格并将列中的其他单元格向上移动。如果选择跨越了列，代码将显示消息框，要求用户仅在某行或某一列中选择：

```
With Selection
If .Columns.Count > 1 And .Rows.Count > 1 Then
 MsgBox "select cells in only one row " \
&or only one column."
End
Else
 If .Cells.Count > 1 Then
 If .Columns.Count > 1 Then
 .Cells.Delete ShiftCells:=wdDeleteCellsShiftUp
 Else
 .Cells.Delete ShiftCells:=wdDeleteCellsShiftLeft
 End If
Else
 .Cells.Delete ShiftCells:=wdDeleteCellsShiftLeft
 End If
End If
End With
```

## 选择单元格范围

要选择表格中的单元格范围，需要声明一个 `Range` 变量，将其分配给想要选择的单元格并选择该范围。下面的示例声明了 `Range` 变量 `myCells`，将其分配给活动文档第一个表格的前四个单元格，并选择了该范围：

```
Dim myCells As Range
With ActiveDocument
Set myCells = .Range(Start:=.Tables(1).Cell(1, 1).Range.Start, \
End:=.Tables(1).Cell(1, 4).Range.End)
myCells.Select
End With
```

## 将表格或行转换为文本

要将表格或若干行转换为文本，请指定指定的表格或行，并使用 `ConvertText` 方法。当你从网页上复制和粘贴时，这非常有用；这些页面通常包含表格，而你只需要内容而不是表格本身。由于用于描述网页布局的 HTML 语言存在局限性，HTML 表格有时用于间距或其他与显示实际表格数据的内容。这些伪“表格”在作为文本粘贴到 Word 或正文中时可能看起来非常奇怪。要查看如何消除这些烦人的痕迹，请参本节末尾的示例宏。对于 Word VBA 编辑器中的任何项目，这是一个非常有用的宏。

`ConvertText` 方法采用以下语法：

```
expression.ConvertText(Separator, Nested Tables)
```

`expression` 是必需的表达式，返回一个 `Table` 对象、`Row` 对象或 `Rows` 集合。`Separator` 是一个可选参数，用于指定用于标记列划分位置的分隔符（也称为定界符）。可能的值有：

- `wdSeparateByDefaultList` 用逗号分隔列信息。
- `wdSeparateByParagraphs` 用指定的 `Other` 列表分隔符（“将表格转换为文本”对话框中“其他”选项旁文本框中显示的字符）分隔列信息。
- `wdSeparateByTabs`（如果不指定，则默认分隔符）用制表符分隔列信息。
- 或者，你可以通过字符串或双引号之间指定你选择的分隔符。例如，输入 `Separator="|"` 以使用竖线 `||` 作为分隔符。（尽管你可以在此处提供多个分隔符，但 Word 仅使用第一个。）

以下语句将当前选择中的表格转换为使用星号 (`*`) 作为分隔符：

```
Selection.Tables(1).ConvertText Separator="="*"
```

你可以对 `Table` 对象、`Row` 对象或 `Rows` 集合使用 `ConvertText` 方法。以下语句仅将所选表格的第一行转换为制表符分隔的文本。

```
Selection.Tables(1).Rows(1).ConvertText Separator=wdSeparateByTabs
```

如果你需要继续处理已转换表格的内容，可以在转换时将一个范围（Range）分配给该表格。此之后，你可以通过操作 `Range` 对象来处理这些信息。例如，以下语句将名为 `Cleveland Report.docm` 的文档中的第一个表格转换为段落分隔的文本，并将范围 `exTable` 分配给转换后的信息，然后复制该范围，创建新文档并粘贴信息：

```
Dim exTable As Range
set exTable = Documents("Cleveland Report.doc").Tables(1). _
ConvertToText(Separator=wdSeparateByParagraphs)
exTable.Copy
Documents.Add
Selection.Paste
```

当你从网页上复制并粘贴信息时，它是表格格式的。如果你将这些表格粘贴到 Word，它们看起来不对，过于臃肿，并且难以编辑或格式化。换句话说，你可能想移除网页表格定义，但保留数据。

下面的宏可以实现这一点：

```
Sub Untable()
On Error Resume Next

Selection.ConvertText Separator=wdSeparateByCommas, NestedTables:=
True
Selection.MoveDown Unit=Line, Count=1

If Err Then MsgBox("No table was detected, dude.")

End Sub
```

要使用此宏，[内容丢失或损坏 - 第 21 节位置错误或第 22 节开始]。

## 第 21 节 Word 中的常用对象

## 第 22 节 Word 中的常用对象

### 理解对象模型和关键对象

本节向你介绍了如何开始使用 Excel 对象模型，即 Excel 的底层架构。它向你展示了如何使用常用的 Excel 对象执行任务。这些对象包括 `Workbooks` 集合和 `Workbook` 对象、`ActiveCell` 对象以及 `Range` 对象。你还将看到如何设置选项。

在本节中，你将学习：

- 处理工作簿
- 处理工作表
- 处理活动单元格或选择
- 处理范围
- 设置选项

## 第 22 章：理解 Excel 对象模型和关键对象

# 图 22.1

Excel 对象引用中的条目将帮助你编写自己的 VBA 代码。

Office 开发 | Office 客户端 | Excel | Excel VBA 参考 | 对象模型

- Office 开发
- Office 客户端
- Excel
- Excel VBA 参考
- 对象模型
- 工作簿对象 (Workbook Object)
- 动作对象 (Action Object)
- 动作集合 (Actions Object)
- 添加对象 (Adds Object)
- 地址对象 (Address Object)
- 调整对象 (Adjustments Object)
- AllEditRange
- AllEditorsRange
- 应用对象 (Application Object)
- 箭头对象 (Arrow Object)
- 自动更正对象 (AutoCorrect Object)
- 自动筛选对象 (AutoFilter Object)

### 对象模型 (Excel VBA)

其他版本

贡献

使用 GitHub 提交并建议更改。查看我们的 VBA 文档。

Excel 开发者参考此部分包含 Excel 对象模型的方法的文档和示例。

你正在查看 Office 产品中的帮助吗？

如果你正在安装的设备版本内部查看帮助，请使用导航窗格浏览主题。要打开帮助窗口中的目录表工具栏，请点击目录表中的主题。

## 从早期版本 Office 产品迁移遗留代码时

如果你有在早期版本 Office 中编写的 VBA 代码，这些过程可能包含已更改的对象、方法和属性。这种情况不太可能，但确实。请记住，对对象模型的修改通常很少，但可能会出现某些不兼容性并“破坏”代码，使其无法正常运行。坦率地说，你可以下载一个免费工具——Office 代码兼容性检查器（Office Code Compatibility Inspector），它可以标记已更改的对象和方法。将当前 Office 对象模型与在早期版本中编写的 VBA 代码进行文本比较。在检查系统要求和安装信息后，你可以从此网页下载兼容性检查器：

`www.microsoft.com/en-us/download/details.aspx?id=15001`

## 理解 Excel的可创建对象

Excel 暴露了各种可创建对象（供你在代码中使用），这意味着你可以在不显式地通过（提及）Application 对象的情况下，使用其对象模型中的大多数重要对象。对于大多数编程目的，这些可创建对象是最常用的对象。以下是列表：
