
```vba
Sub Add_Months()
    ' Add_Months 宏
    ' 填充全年的月份。由 Abe Normal 于 9/29/15 记录。
    ' 
    ' 
    ' 
    Range("A1").Select
    ActiveCell.FormulaR1C1="Jan-2016"
    Range("B1").Select
    ActiveCell.FormulaR1C1="Feb-2016"
    Selection.AutoFill Destination:=Range("B1:L1"), Type:=xlFillDefault
    Range("A1").Select
    ActiveCell.FormulaR1C1="Jan-2016"
    Range("B1").Select
    ActiveCell.FormulaR1C1="Feb-2016"
    Selection.AutoFill Destination:=Range("B1:L1"), Type:=xlFillDefault
End Sub
```

现在，通过以下步骤更改宏以显示第二行自动填充的值：

1. 将第 13 行改为单元格 `A2` 而不是单元格 `A1`：

   `Range("A2").Select`

2. 修改第 14 行，使其输入值 `1` 而不是 `Jan-2016`：

   `ActiveCell.FormulaR1C1=1`

3. 将第 15 行改为单元格 `L2` 而不是单元格 `B1`：

   `Range("L2").Select`

4. 修改第 16 行，使其输入值 `12` 而不是 `Feb-2016`：

   `ActiveCell.FormulaR1C1=12`

5. 修改第 17 行，使其对区域 `A2:L2` 执行自动填充操作，并将填充类型更改为 `xlFillSeries`：

   `Selection.AutoFill Destination:=Range("A2:L2"), Type:=xlFillSeries`

6. 点击保存按钮或选择“文件 ➤ 保存”以保存你所做的更改。

## 第 3 章 编辑已录制的宏

现在宏看起来应该像列表 3.5。

### 列表 3.5：精简版宏

```vba
Sub Add_Months()
    ' Add_Months 宏
    ' 填充全年的月份。由 Abe Normal 于 9/29/15 记录。
    Range("A1").Select
    ActiveCell.FormulaR1C1="Jan-2016"
    Range("B1").Select
    ActiveCell.FormulaR1C1="Feb-2016"
    Selection.AutoFillDestination:=Range("B1:L1"), Type:=xlFillDefault
    Range("A1").Select
    ActiveCell.FormulaR1C1="Jan-2016"
    Range("B1").Select
    ActiveCell.FormulaR1C1="Feb-2016"
    Selection.AutoFillDestination:=Range("B1:L1"), Type:=xlFillDefault
    Selection.AutoFillDestination:=Range("A2:L2"), Type:=xlFillSeries
End Sub
```

```  
```

*(注：此处原文代码块似乎存在逻辑截断或重复，翻译已根据原文结构保留格式)*

（抱歉，提供的原文文本末尾似乎有不完整的代码或重复，我已根据您提供的文本内容完成了翻译。）

第 13 行选择了 `Shapes` 集合中的第一个形状，第 14 行选择了形状中 `TextFrame` 对象中的 `TextRange` 对象。当你进行交互操作时，PowerPoint 会让这个过程变得无缝衔接：你点击显示“单击添加标题”（或其他内容）图例的形状，PowerPoint 就会选择该形状文本框中的范围——但你看到的只是该形状被选中了。在 VBA 中，在获取文本之前，你可能需要经过对象模型中的几个不可见的层级。

当你选择占位符文本时，PowerPoint 会将其移除。但当你通过 VBA 选择占位符文本时，会发生某些情况。因此，第 15 行在文本范围第一个字符处创建了一个新选择。选择的长度（`Length`）为 0，这意味着选择仅限于插入点，而不是包含任何字符。第 16 行开始了一个 `With` 语句，一直持续到第 30 行。第 16 行中的 `With ActiveWindow.Selection` 语句让第 17 行能够引用 `ActiveWindow` 对象中 `Selection` 对象的 `TextRange` 对象的 `Text` 属性（而不是 `ActiveWindow.Selection.Text`），并且第 18 行能够轻松引用 `ActiveWindow` 对象中 `Selection` 对象的 `TextRange` 对象的 `Font` 属性（而不是 `ActiveWindow.Selection.Font`）。

第 17 行将 `ActiveWindow.Selection.Text` 的属性设置为用户输入的文本。

第 18 行开始了一个嵌套的 `With` 语句，用于设置 `TextRange` 对象的 `Font` 对象的属性。第 19 行将 `Font` 对象的属性命名为 `Arial`；第 20 行将 `Font` 的 `Size` 属性设置为 44；第 21 行将 `Font` 的 `Bold` 属性设置为 `msoFalse`；这里还有 Microsoft Office (`mso`) 常数等。这些语句对于我们这个宏的用途来说并不是必要的，但它们是无害的，所以如果你愿意，可以把它们留在代码中，也可以删除整个代码块（我们稍后会这样做）。第 29 行结束了 `With` 语句。

### With 块可以嵌套

`With` 语句是指放在另一个 `With` 语句内部，并指定 `With` 语句所指定对象内部对象的语句。必要时，你可以嵌套多层级的 `With` 语句。你可以看到第 18 行开始的 `With` 块嵌套在第 16 行开始的另一个块中。

第 31 行使用 `Select` 方法选择文本范围中的第 1 到 42 个字符。这等同于按下 `Ctrl+Shift+Home` 组合键。因为此语句指定了要选择的字符，如果你更改了此宏插入的文本，就需要更改它。（如果在少于 42 个字符的文本范围上运行该语句，它将返回错误。如果你在超过 42 个字符的文本范围上运行它，它只会选择文本范围中的前 42 个字符——这不是你想要的。）

## 第 3 章编辑录制的宏

- 第 32 行开始了另一个 `With` 语句，用于处理 `TextRange` 对象的 `Font` 对象。该 `With` 语句决定当用户打开并修改字体对话框时会发生什么。

- 第 43 行结束了 `With` 语句，第 44 行结束了宏。

现在尝试通过精简宏并更改其插入的文本来编辑此宏：

1. 删除第 18 行到第 29 行中不必要的 `With` 语句。

2. 删除第 30 行。

3. 将第 16 行和第 17 行合并为不带 `With` 的单一语句：

`ActiveWindow.Selection.TextRange.Text = "The quick brown dog jumped over the lazy fox"`

4. 现在更改第 16 行插入的新文本。在双引号之间输入你喜欢的任何类型。

5. 修改第 31 行，使其对文本范围使用 `Select` 方法，而不是指定要选择哪些字符。删除 `Characters (Start:=1, Length:=42)`，留下此语句：

`ActiveWindow.Selection.ShapeRange.TextRange.Select`

通过指定范围而不是特定的字符数，你就可以避免每次更改消息时出现之前的问题。指定字符数被称为“硬编码”（hard-coding），应尽可能避免。如果有方法（如 `TextRange` 属性那样），就让计算机来计算数量，而不是在代码中指定。

6. 点击工具栏上的保存按钮或选择“文件 > 保存”来保存你所做的更改。在“另存为”对话框中，找到“保存类型”下拉列表，将其从默认的 `.pptx`（不能包含宏）更改为 `.pptm` 类型（可以包含）。

你现在的代码应该看起来像 3.7。

### 列表 3.7：精简和修改后的宏

| 行号 | 代码 |
| :--- | :--- |
| 1 | AddSlide_and_Format_Placeholder() |
| 2 |  |
| 3 | 用于幻灯片、格式化占位符并向其 |
| 4 | 添加文本的宏。12/4/15 Rodney制。 |
| 5 |  |
| 6 | ActiveWindow.View.Slide.Index:= |
| 7 | Presentation.Slides.Add(Index:=2, |
| 8 | Layout:=ppLayoutText).SlideIndex |
| 9 | ActiveWindow.Selection.SlideRange.Layout = ppLayoutTitle |
| 10 | ActiveWindow.Selection.SlideRange.Shapes(1).Select |
| 11 | With ActiveWindow.Selection.ShapeRange |
| 12 | IncrementLeft -60 |
| 13 | IncrementTop -20 |
| 14 | End With |
| 15 | ActiveWindow.Selection.ShapeRange.TextRange.Text = "Welcome to VBA" |
| 16 | ActiveWindow.Selection.ShapeRange.TextRange.Select |
| 17 | With ActiveWindow.Selection.ShapeRange.TextRange.Font |
| 18 | .Name = "Arial" |
| 19 | .Size = 44 |
| 20 | .Bold = msoFalse |
| 21 | End With |
| 22 | End Sub |

## 核心要点

在 Visual Basic 编辑器中测试宏。当你需要修改或调试宏时，Visual Basic 编辑器是你最好的朋友。它包含了许多让你的工作变得轻松的工具。

掌握它：打开一个宏；然后单步执行以查看是否有错误。

设置断点并使用注释。设置断点允许你按 `F5` 执行宏，但当执行到达设置断点的行时，强制编辑器进入中断模式（Break mode）。在执行宏代码期间，“注释掉”一行代码有时是查看该行是否导致你正在追踪的错误的好**方法。

掌握它：在宏中设置断点并添加注释。

编辑录制的宏。对 Word 宏进行一些更改。

掌握它：在打开 Visual Basic 编辑器的情况下，选择一个宏并对其进行修改。

# 第 4 章

## 在 Visual Basic 编辑器中从头创建代码

在本章中，你将练习 Visual Basic 编辑器中从头创建宏（过程）。示例将引导你完成在 Word、Excel 和 PowerPoint 中创建宏的过程。为了在视觉上设置特定的方式，并设置要求显式声明变量（这被认为是一种良好的编程习惯），我们将从本章开始确保满足这些条件。

对于书中的示例，Visual Basic 编辑器应该以特定的视觉方式设置。

本章的目的是让你在后续章节学习语言细节之前，对在 Visual Basic 编辑器中创建代码有一个感觉。在这里，你将简要地接触 VBA 元素（如对象、属性、方法、变量和常量），你将在本书的以后学习更多内容。在此过程中，你将遇到 Visual Basic 编辑器提供的许多有用工具，包括宏录制器、对象浏览器和帮助系统。你将在本书的后续部分更深入地探索这些工具。

在本章中，你将学习以下内容：

- 设置 Visual Basic 编辑器以创建宏

- 为 Word 创建宏

- 为 Excel 创建宏

- 为 PowerPoint 创建宏

- 为 Access 创建宏

## 设置 Visual Basic 编辑器以创建宏

如果你以默认配置设置 Visual Basic 编辑器，那么遵循后续宏（以及书中其余部分）指令将会容易得多。（对 VBA 编辑器所做的任何更改将适用于所有启用 VBA 的应用程序。）因此，如果你按照描述设置了编辑器，无论你在 Excel、Access、Outlook 还是 PowerPoint 中打开它，它看起来都是这样。

以下步骤描述了如何设置 Visual Basic 编辑器使其看起来像图 4:1 所示：

- 1. 打开 Visual Basic 编辑器。

- 2. 如果没有显示项目资源管理器，选择“视图” > 项目资源管理器或按 `Ctrl+R` 显示它。

- 3. 如果没有显示属性窗口，选择“视图” > 属性窗口或按 `F4` 键显示它。

- 4. 除非你有其他偏好，否则将项目资源管理器停靠在 Visual Basic 编辑器区域左角的常规位置。将属性窗口停靠在项目资源管理器下方，同样位于其默认位置。（要更改停靠，选择“工具” > “选项”，点击“停靠”选项卡并选择“选项”。）要停靠未停靠（窗口），双击其标题栏。

- 5. 设置 Visual Basic 编辑器要求声明变量。这将强制执行一条规则：在代码中使用每个变量之前，必须正式声明它。选择“工具” > “选项”，确保勾选了“选项”对话框，然后点击确定按钮。我们将在书的以后详细讨论变量声明，但这里有一个简要总结。此设置将使 Visual Basic 编辑器从现在起为你创建的所有模块和用户窗自动输入 `Explicit` 语句。该语句会导致编辑器在运行时检查任何隐式声明的变量（被认为是不良习惯），并提醒你必须这样声明：

```
Dim txtName As String
```

![](img/03e3cf21a6476d99c08cf87b3092f20_129_0.png)

# 第 4 章在 Visual Basic 编辑器中从零创建代码

在您访问过的“修订”对话框中，记录的不仅仅是您选择并修改的单个选项。简要浏览代码，查看从图 4.2 所示对话框选项中记录的许多设置。

如果你查看该图，可以看到代码如何表示你第二次访问对话框时几乎完全相同的设置。例如，找到 `.SplitCell = wdCellColorOrange` 这行代码，并在对话框中定位该设置。

- 5. 对话框的第二组几乎完全相同的设置。特别注意第 9 行和第 35 行；这些是关键。第 35 行反映了你第二次访问时做的更改——将 `Options` 对象的 `DeletedTextMarkStrikethrough` 属性指定为“隐藏”而非“删除线线”。同样，请注意此属性的值（当你记录了“删除内容不带删除线”时）和 `wdDeletedTextMarkHidden`（当你将其设置为“隐藏”时）。

- 6. 现在在编辑器中，选择整个录制的宏（从 `Sub` 语句到 `End` 语句），并按 `Delete` 键将其删除。

- 7. 确保 Visual Basic 编辑器已按照章节前面的“为创建宏设置 Visual Basic 编辑器”所述进行了设置。

- 8. 在项目资源窗口中，右键点击 `Normal` 项的任何位置，从右键菜单选择“插入 > 模块”。Visual Basic 编辑器会在 Normal 模板中插入一个新模块并显示代码窗口。

- 9. 按 `F4` 键激活新模块的属性窗口。（激活的意思是将焦点移到——无论当前焦点在哪里，即可以显示输入内容或鼠标点击生效的地方）。Visual Basic 编辑器选择了 `(Name)` 属性，这是该新模块唯一的可用属性。（令人困惑的是，属性名称包含在括号中）。

- 10. 在属性窗口中为新模块输入名称。在本例中，删除默认名称（Module1、Module2 或其他名称）并输入名称 `Procedures_to_Keep_1`。

- 11. 按 `F7` 键或点击代码窗口激活它。

- 12. 验证 Visual Basic 编辑器是否在代码顶部（代码区域）的声明部分输入了 `Option` 语句。如果没有，返回完成本章开头列表中的第 4 步。

- 13. 在 `Option explicit` 语句下方，输入程序的 `Sub` 语句并按回车键。创建程序 `Toggle_Track_Changes_between_Hidden_and_Strikethrough`。

- 14. 当你按回车键时，Visual Basic 编辑器会在 `Sub` 语句结束插入所需的括号、一个空行以及 `End` 语句，并将插入点放在空行上，准备让你开始编程：

```
Toggle_Track_Changes_between_Hidden_and_Strikethrough()
End Sub
```

- 15. 按 `Tab` 键对 `Sub` 语句之前的行进行缩进。

- 16. 输入 `if options.`（全小写，并确保以句号结尾）。现在编辑器显示列表属性/方法下拉列表。

- 17. 在列表中向下输入（输入 d、e，然后是 l），并使用 ↓ 键或滚动鼠标来选择 `DeletedTextMark` 符号。

- 18. 现在只需输入 `=`（等号）。Visual Basic 编辑器会为你输入命令，后跟等号，然后显示可以与 `DeletedTextMark` 属性配合使用的列表属性/方法 (4.3)。

## 4.3

Visual Basic 编辑器的列表方法显示了 `DeletedTextMark` 属性可用的常量。

![](img/03e3cf21a6476d99c08c2f87b3092f20_134_0.png)

- 19. 选择 `DeletedTextMarkHidden` 项，通过 `Tab` 键编码下一行或双击它进入。

- 20. 输入 `Then` 并按回车键。注意，当你开始下一行代码（通过按回车）时，Visual Basic 会检查该行代码。如果你在语句的 If 部分使用小写，Visual Basic 编辑器会应用大写字母（这只是为了——VBA 并不关心这个）。
