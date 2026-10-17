
```
Windows.Arrange ArrangeStyle=wTiled
```

## 窗口定位和调整大小

要在显示器上定位窗口，请设置其 `Left` 和 `Top` 属性，例如：

```
ActiveWindow.Left = 100
```

```
ActiveWindow.Top = 200
```

# 第 21 章 在 Word 中操作常用对象

若要调整窗口大小，请设置其 `Height`（高度）和 `Width`（宽度）属性：

```vba
With ActiveWindow
    .Height = 300
    .Width = 400
End With
```

要最大化、最小化或“还原”窗口，请分别将 `WindowState` 属性设置为 `wdWindowStateMaximize`、`wdWindowStateMinimize` 或 `wdWindowStateNormal`。如果窗口处于最小化状态，以下语句将使包含示例文档 `Example.docm` 的文档的窗口最大化：

```vba
With Documents("Example.docm").Windows(1)
    If .WindowState = wdWindowStateMinimize Then
        .WindowState = wdWindowStateMaximize
End With
```

## 在窗口中显示某项

在打开或排列窗口后，你通常需要确保想要查看的项目（区域、某些文本、图形或其他形状或字段）显示在窗口中。最简单的方法是使用窗口的 `ScrollInto` 方法。该方法会移动窗口但不会移动选取；如果你需要选取也随之移动，则需要编写额外的代码来实现。

`ScrollInto` 采用以下语法：

```vba
expression.ScrollView(Obj, Start)
```

这里，`expression` 是一个返回 `Window` 对象的必要表达式。`Obj` 是一个指定 `Range` 或 `Shape` 对象的必要参数。`Start` 是一个可选的布尔值参数，可以设置为 `True`（默认值）以显示区域或形状的左上角，或设置为 `False` 以显示右下角。当你需要显示可能比窗口大的区域或形状的末尾时，将 `Start` 设置为 `False`。

以下语句将选取内容置于活动文档第一段的末尾，并向列表中添加新段落：

```vba
Dim rngFirstList As Range
Set rngList = ActiveDocument.Lists(1).Range
ActiveDocument.Windows(1).ScrollView Obj:=rngFirstList, Start:=False
rngFirstList.Select
Selection.Direction:=wdCollapseEnd
Selection.MoveLeft Unit:=wdCharacter, Count:=1, Extend:=wdMove
```

## 更改文档视图

要更改文档视图，请将 `View` 对象的 `Type` 属性设置为相应的视图方式，如 `wdConflictView`、`wdNormal`、`wdNormalView`、`wdOutline`、`wdPreview`、`wdReading` 或 `wdView`。例如，以下语句将 `Sample.doc` 的视图更改为布局视图：

```vba
Documents("Sample.docm").Windows(1).View.Type = wdPreview
```

## 切换到阅读模式

阅读模式会隐藏功能带、任何标记以及文本以外的所有内容。然而，导航和词典等窗格仍然可见。文本通常以两页或三页（取决于你的缩放级别）并排显示在书中。以下是切换到阅读模式的方法：

```vba
ActiveDocument.ActiveWindow.View.Type = wdReadingView
```

阅读模式的设计使内容易于阅读和记忆。例如，缩放功能（右下角）调整字体大小但保持文本重流，这样你就永远不需要通过水平滚动条来显示隐藏的文本。滚动条对于文档导航和指示光标位置有用。阅读模式还让你控制列宽。大多数人发现较短的行更容易阅读，因此可以在 `View` 菜单中调整长度。

## 缩放视图显示多页

要使布局视图或打印预览显示多个页，请设置活动对象的 `PageColumns` 和 `PageRows` 属性。（如有必要更改视图。）以下语句以六页的布局显示 `Sample.doc`：

```vba
With Documents("Sample.doc").Windows(1).View
  .Type = wdbtnPrint
    .PageColumns = 3
    .PageRows = 2
End With
```

## 操作表格

许多人需要在 Word 文档中操作表格，无论是从创建还是处理现有表格。VBA 使用 `Table` 对象表示每个单独的表格。如果有多个 `Table` 对象，它们会被汇总到 `Tables` 集合中。操作表格时，使用 对象返回 `Tables` 集合。以下是 `Table` 集合和对象的示例：

- `Rows` 集合包含表格中的行。每行由 `Row` 对象表示。
- `Columns` 集合包含表格中的列。每列由 `Column` 对象表示。
- `Cell` 对象直接从 `Table` 对象访问单元格。你也可以通过它们所在的行或列访问表格中的单元格。
- `Range` 对象访问表格内部的区域。
- `Borders` 集合包含表格的所有边框。
- `Shading` 对象包含表格的所有阴影。

有关 `Table` 对象的完整列表，请参此网页：

http://msdn.microsoft.com/en-us/library/office/ff1952.aspx

`Table` 集合的成员可以在此处找到：

http://msdn.microsoft.com/en-us/library/office/ff8292.aspx

## 创建表格

要从头创建一个新表格（而不是将文本转换为表格），请使用 `Tables` 集合的 `Add` 方法。`Add` 方法采用以下语法：

```vba
expression.Add(Range, NumRows, NumColumns, DefaultTableBehavior, AutoFit)
```

参数如下：

- `expression` 是必要参数，指定返回 `Range` 对象或 `Selection` 对象的表达式。
- `Range` 是必要参数，指定要插入表格的区域。
- `NumRows` 是必要参数，指定表格的行数。
- `NumColumns` 是必要参数，指定表格的列数。
- `DefaultTableBehavior` 是可选参数，指定表格是否自动调整列：这仅在 `AutoFit` 为 `wd9TableBehavior` 时生效。
- `AutoFit` 是可选参数，指定表格的自动调整行为：使用 `wdFitContent` 将列调整为内容大小，`wdFitWindow` 将列调整为窗口大小，或 `wdFitFixed` 使用固定列宽。

例如，以下语句在活动文档的当前位置插入一个包含 10 行 5 列的非自动调整的新表格：

```vba
ActiveDocument.Tables.Add Range=Selection.Range, NumRows=10, NumColumns=5, DefaultTableBehavior=wd8TableBehavior
```

## 选择表格

要选择表格，请指定涉及的 `Document`、`Range` 或 `Selection` 对象，然后标识 `Table` 对象并使用 `Select` 方法。该方法不接受参数。

以下语句选择活动文档中的第一个表格：

```vba
ActiveDocument.Tables(1).Select
```

以下语句声明变量 `tempTable`，选择名为 `Log.docm` 的文档中的第一个表格并将其 `Range` 对象赋值给 `tempTable`：

```vba
Dim tempTable
Documents("Log.docm").Tables(1).Select
Set tempTable = Tables(1).Range
```

以下语句选择名为 `tempRange` 的区域中的第二个表格：

```vba
tempRange.Tables(2).Select
```

此语句选择当前选取内容中的第一个表格：

```vba
Selection.Tables(1).Select
```

## 将文本转换为表格

要将文本转换为表格（而不是从头插入新表格），请使用适当的 `Range` 或 `Selection` 对象使用 `ConvertToTable` 方法。`ConvertToTable` 方法有以下语法：

```vba
expression.ConvertTo(Separator, NumRows, NumColumns, InitialColumnWidth, Format, ApplyBorders, ApplyShading, ApplyFont, ApplyColor, ApplyHeadingRows, ApplyLastRow, ApplyFirstColumn, ApplyLastColumn, AutoFit, AutoFitBehavior, DefaultTableBehavior)
```

参数如下：

- `expression` 是必要参数，指定返回 `Range` 对象或 `Selection` 对象的表达式。
- `Separator` 是可选参数，指定在划分列处使用的分隔字符（也称为分隔符）。你可以使用这些值作为 `Separator`：
  - `wdSeparateByComma` 用逗号分隔列信息。
  - `wdSeparateByDefaultListSeparator` 使用指定的列表分隔符字符分隔列信息（“转换表格”对话框中“其他”选项旁文本框中显示的字符）。
  - `wdSeparateByParagraph` 用段落标记分隔列信息。
  - `wdSeparateByTabs`（未指定的默认分隔符）用制表符分隔列信息。
- `NumRows` 是必要参数，指定表格的行数。
- `NumColumns` 是必要参数，指定表格的列数。

或者，`NumRows` 是一个可选的 `Variant` 参数，用于指定表格应拥有的行数。如果你省略了 `NumRows` 参数，Word 将根据指定的列数和/或所选分隔符标识的数量来决定表格的行数。

`NumCols` 是一个可选的 `Variant` 参数，用于指定表格应拥有的列数。与 `NumRows` 类似，如果你省略了 `NumCols` 参数，Word 将根据指定的行数和/或所选分隔符标识的数量来决定表格的列数。

`InitialColumnWidth` 是一个可选的 `Variant` 参数，您可以使用它来指定每列的初始宽度（以磅计）。如果你省略了 `InitialColumnWidth` 参数，Word 将使用页面的全宽（从页边距到页边距），并为每列分配相等的宽度，无论列的相对宽度如何。`InitialColumnWidth` 参数在许多情况下用于限制表格宽度，但在许多情况下，自动调整列宽提供了一个更好的解决方案。

`Format` 是一个可选的 `Variant` 参数，您可以使用它来指定 Word 内置表格样式之一。要使用 `Format` 参数，请指定 `TableFormat` 常量（例如 `wdTableFormatElegant` 样式）。如果你选择应用某种格式，可以使用以下 `Variant` 参数指定该样式的哪些属性适用于表格：

- 将 `SetApplyBorder` 设置为 `True` 应用边框格式，或设置为 `False` 则不应用。
- 将 `SetApplyShading` 设置为 `True` 应用阴影，或设置为 `False` 不应用。
- 将 `SetApplyFont` 设置为 `True` 应用字体格式，或设置为 `False` 不应用。
- 将 `SetApplyColor` 设置为 `True` 应用颜色格式，或设置为 `False` 不应用。
- 将 `SetApplyHeadingRows` 设置为 `True` 应用任何标题行格式，或设置为 `False` 不应用。
- 将 `SetLastRow` 设置为 `True` 应用任何末行格式，或设置为 `False` 不应用。
- 将 `SetFirstColumn` 设置为 `True` 应用任何首列格式，或设置为 `False` 不应用。
- 将 `SetLastColumn` 设置为 `True` 应用任何末列格式，或设置为 `False` 不应用。

`AutoFit` 是一个可选的 `Variant` 参数，您可以将其设置为 `True`，让 Word 调整宽度以适应单元格中的任何内容。在自动调整时，Word 不会增加表格的总宽度——而是缩小或保留表格的宽度。

`AutoFitBehavior` 和 `DefaultTableBehavior` 在本章节前面的“创建表格”部分进行了描述。

以下语句将当前选择转换为五列表格，并以逗号分隔。它根据单元格内容对表格应用自动调整，并将单元格设置为自动调整大小：

```
Set MyTable = Selection.ConvertToTable(wdSeparateByCommas,
Selection.Paragraphs.Count, S, , , , , , , , True,
wdAutoFitContent,wd99TableBehavior)
```

## 确保选择在表格中

在运行任何操作表格的程序之前，确保当前选择实际上位于表格内是一个好习惯。使用选择的 `Information` 属性的 `wdWithInTable` 参数。如果选择在表格中则返回 `True`，否则返回 `False`。这是一个示例：

```
If Selection.Information(wdWithInTable) = True Then
    take actions here
End If
```

## 查找选择在表格中的位置

除了检查选择是否在表格中外，您还可以使用 `Information` 属性查找在通过 `Range` 对象选择处理表格时可能有用的其他信息。

一旦您确定选择在表格内（可能使用了 `wdInTable` 参数），请检查选择是否为行尾标记而不是在单元格内。如果选择是行尾标记，某些操作将失败。例如，尝试选择当前单元格或列将失败，因为选择在任何单元格或列之外，但尝试选择当前行将成功。

要检查选择是否为行尾标记，请使用 `Information` 属性的 `AtEndOfRowMarker` 参数。如果选择是行尾标记，以下语句将选择向左移动一个字符（进入行中的同一个单元格）：

```
If Selection.Information(wdEndOfRowMarker) = True Then
    Selection.MoveLeft Unit:=wdCharacter, Count:=1
```

如果选择包含行尾标记，而不是在标记前折叠（一个插入点），则 `wdEndOfRowMarker` 参数返回 `False`。为了避免选中的行尾标记在您的程序中引起问题，在检查是否为行尾标记之前，如果选择不是折叠的，则将其折叠。以下语句执行了此操作，使用名为 `cursel` 的变量来恢复选择，除非在行尾标记处折叠了选择：

```
Dim cursel
With Documents("Communications.docx")
If Selection.Type <> wdSelection Then
    Set cursel = Selection.Range
    Selection.Collapse Direction:=wdCollapseStart
End If
```

```
If Selection.Information(wdAtEndOfMarker) = True Then
    Selection.MoveLeft Unit:=wdCharacter, Count:=1, Extend:=wdMove
Else
    If curSel <> '' Then 
        curSel.Select
    set curSel = Nothing
End If
```

在确定选择安全地位于表格内后，您可以获取关于表格的六条有用信息：

- `wdStartOfRangeColumn` 返回选择或范围起始所在的列号。以下语句选择了当前选择起始的列：`Tables(1).Columns(wdStartOfRangeColumn)`。
- `wdEndOfColumn` 返回选择结束所在的列号。以下语句选择了当前选择结束的列：`Tables(1).Columns(wdEndOfColumn)`。
- `wdStartOfRow` 返回选择起始所在的行号。以下语句选择了当前选择起始的行：`Tables(1).Rows(wdStartOfRow)`。
- `wdEndOfRow` 返回选择结束所在的行号。以下语句选择了当前选择结束的行：`Tables(1).Rows(wdEndOfRow)`。（此处原文为 `wdEndOfRow`）
- `wdCellIndex` 返回选择起始所在的单元格索引。
- `wdCellIndex` 返回选择结束所在的单元格索引。

## 排序表格

要排序表格，标识表格并使用 `Sort` 方法。`Sort` 方法对于 `Table` 对象的语法如下：

```
expression.Sort(ExcludeHeader, FieldNumber, SortField, SortOrder, FieldNumber2, SortField2, SortOrder2, FieldNumber3, SortField3, SortOrder3, CaseSensitive, BidSort, Ignore,Kashida, IgnoreDiritics, IgnoreHe, LanguageID)
```

参数如下：

- `expression` 是返回 `Table` 对象的可选参数。
- `ExcludeHeader` 是一个可选 `Variant` 参数，设置为 `True` 将表格的第一行（通常是表头）排除在排序之外，或设置为 `False` 包含第一行。
- `FieldNumber`、`FieldNumber2` 和 `FieldNumber3` 是可选 `Variant` 参数，分别指定第一、第二和第三个字段。通常您需要指定 `FieldNumber`；否则将按字母排序。
