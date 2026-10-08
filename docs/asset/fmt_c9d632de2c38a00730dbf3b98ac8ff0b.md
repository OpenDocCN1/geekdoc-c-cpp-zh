
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

# VBA 自动帮助你的代码添加标点符号

你会发现，在这个例中，每个 ampersand (`&`) 和等号的两边都出现了一个空格。你可以手动输入这些空格，也可以在按下 Enter 键或点击鼠标移动插入点到另一行时，让 VBA 为你输入。（将插入点移动到另一行会触发 VBA 检查你正在工作的行，并根据需要进行各种自动更改。例如，某些字符可能会变为大写，或者如果你输入 `EndIf`，VBA 会将其处理为两个单词，因为它应该是两个。）

# 为消息框选择按钮

`buttons` 参数控制消息框包含哪些按钮。VBA 提供了表 13.1 所示的消息框类型，由 `buttons` 参数进行控制。

# 表 13.1：由 `buttons` 参数控制的消息框类型

| VALUE | CONSTANT | BUTTONS |
| :--- | :--- | :--- |
| 0 | `vbOKOnly` | OK |
| 1 | `vbOKCancel` | OK, 取 |
| 2 | `vbAbortRetryIgnore` | 终止，重试，忽略 |

# 表 13.1：由 `buttons` 参数控制的消息框类型（续）

| VALUE | CONSTANT | BUTTONS |
| --- | --- | --- |
| 3 | `vbYesNoCancel` | 是，否，取消 |
| 4 | `vbYesNo` | 是，否 |
| 5 | `vbRetryCancel` | 重试，取消 |

你可以在代码中使用数值值或常量来指定这些消息框类型。例如，如果你指定 1 或 `vbOKCancel` 来生成一个带有“确定”和“取消”按钮的消息框。数值易于输入，而常量更易于阅读。在 PowerPoint 中运行时，执行以下任一条语句都会生成图 13.5 所示的消息框：

```
Dim lngR As Long
lngR = MsgBox("对幻灯片应用标准格式吗?", vbYesNo)
lngR = MsgBox("对幻灯片应用标准格式吗?", 4)
```

图 13.5

`vbYesNo` 常量会生成一个带有“是”和“否”按钮的消息框。

![](img/03e3cf21a6476d99c08c2f87b3092f20_362_0.png)

从 VBA 的角度来看，在宏的消息框中使用数值还是常量并不重要。但对于人类来说，文本常量要优越得多。即使你是唯一能看到自己代码的人，使用常量会让代码更易读。

# 为消息框选择图标

你还可以通过包含适当的值或常量参数为消息框添加图标。表 13.2 显示了这些选项。

# 表 13.2：消息框图标的参数

| VALUE | CONSTANT | DISPLAYS |
| --- | --- | --- |
| 16 | `vbCritical` | 停止图标 |
| 32 | `vbQuestion` | 问号图标 |
| 48 | `vbExclamation` | 感叹号图标 |
| 64 | `vbInformation` | 信息图标 |

再次，你可以通过使用数值或常量来引用这些图标。48 或 `vbExclamation` 将产生一个感叹号图标。同样，常量更易于阅读。

要将消息框的值与图标的值或常量关联，请使用加号。例如，为了生成一个带有“是”和“否”按钮且带有问号图标的消息框（见图 13.6），你可以输入 `vbYesNo + vbQuestion`（或 4 + 32，`vbYesNo = 32` 或 `+ vbQuestion`）：

```
lngR = MsgBox("对幻灯片应用标准格式", \
vbYesNo + vbQuestion)
```

图 13.6

添加图标使消息框具有更大的视觉冲击。

![](img/03e3cf21a6476d99c08c2f87b3092f20_363_0.png)

# 为消息框设置默认按钮

与 Windows 界面一样，用户会被提示消息框中的一个默认按钮。它是外框带有蓝色边框且文本区域上方有虚线的那个按钮（见图 13.6 中的按钮）。用户可以使用 Tab、Shift+Tab 或使用 $\leftarrow$、$\uparrow$ 或 $\downarrow$ 键将选择移动到另一个按钮。

然而，你可以在代码中指定想要哪个按钮作为默认按钮。

## 真实世界场景

## 默认按钮的实际应用

你可以通过在 `MsgBox` 中指定特定按钮来为消息框设置默认按钮。当你向不熟悉将发生什么的用户提供可能采取剧烈行动的宏时，指定默认按钮是明智的（用户可能会不小心碰到 Enter 键或点击高亮的按钮）。例如，考虑一个在不让用户关闭文档的情况下删除当前文档，然后切换到文件管理程序（如 Windows 资源管理器）或弄乱其中一个对话框（如打开或保存对话框）的宏。常见的对话框在第 12 章标题为“通过对话框控制用户输入”的真实世界场景中有所演示。

由于此类宏如果在无意中运行会破坏他人的工作，因此要在确认消息框中将“否”或“取消”设为默认按钮，以便用户必须选择宏的其余部分。消息框会停止执行，允许用户对操作表示同意或反对，然后根据点击了哪个按钮来执行用户的意愿。为什么 VBA 要包含默认按钮？这使用户只需按 Enter 键就能轻松选择普通按钮（确定）。在消息框或对话框上放置适当的按钮可以帮助用户更快地处理消息。程序员，在消息框或对话框上放置合适的按钮可以帮助用户更快速地处理消息。VBA 包含默认按钮是为了方便。除非另有指定，消息框中的第一个按钮是默认。表 13.3 列出了默认按钮的参数。

# 表 13.3：默认按钮的参数

| VALUE | CONSTANT | EFFECT |
| --- | --- | --- |
| 0 | `vbDefault1` | 第一个按钮 |
| 256 | `vbDefault2` | 第二个按钮 |
| 512 | `vbDefault3` | 第三个按钮 |
| 768 | `vbDefault4` | 第四个按钮 |

除非另有指定，消息框中的第一个按钮是默认。为了让不同的按钮默认，请将值或常量作为参数的一部分。在 PowerPoint 中，此语句会生成图 13.7 所示的消息框。

```
Dim LngQuery As Long
LngQuery = MsgBox("要删除此幻灯片吗?", _
vbYesNo + vbCritical + vbDefaultButton)
```

图 13.7

指定默认按钮以引导用户进入消息框中的按钮。

![](img/03e3cf21a6476d99c08c2f87b3092f20_365_0.png)

# 控制消息框的模态

VBA 理论上可以显示应用程序模态消息框和系统模态消息框。应用程序模态消息框在用户消除它们之前阻止你在当前应用程序中进行任何操作，而系统模态消息框在用户消除它们之前阻止你在整个计算机上进行任何操作。

大多数消息框是应用程序模态的，允许用户通过 Alt+Tab（或通过任务栏）切换到另一个应用程序。相比之下，消息框（通常在安装过程中使用）是系统模态的，强制用户将注意力集中在它们身上。你可能从经验中知道系统模态消息框在绝对必要时是多么沮丧——例如，某些操作可能会导致数据丢失或系统不稳定。对于大多数用途，应用程序模态消息框可以满足你的所有需求，而不会困扰或烦用户。

理论上，你可以使用表 13.4 所示的两个按钮来控制消息框的模态。

# 表 13.4：消息框模态的参数

| VALUE | CONSTANT | RESULT |
| --- | --- | --- |
| 0 | `vbApplicationModal` | 消息框是应用程序模态的 |
| 4096 | `vbSystemModal` | 消息框是系统模态的 |

在实践中，即使使用了 `vbSystemModal` 参数，用户也可以切换到另一个应用程序（只要该程序正在运行）并继续工作。然而，消息框会保持在“顶部”并显示——这足以让用户感到恼，但不会完全阻止他们访问另一个应用程序。

默认情况下，消息框是应用程序模态的，因此只有在需要系统模态消息框时才需要指定它。当你在按钮中添加 `vbSystemModal` 常量或 `4096` 值时：

```
Response = MsgBox("Do you want to delete this document?", \
vbYesNo + vbCritical + vbDefaultButton2 + vbSystemModal)
```

请注意，系统模态消息框的外与应用程序消息框相同。

## 为消息框指定标题

消息框的下一个组件是它的标题，由可选的 `title` 参数控制。如果你使用 `title`，VBA 将应用程序显示为名称，但宏的用户将从提供更有帮助的标题中受益。

`title` 字符串长度可达 1024 个字符（较长的字符串会在没有警告或错误的情况下被截断，但在实践中，任何超过 75 个字符的标题都会被截断并带有省略）。如果你想阅读消息框的标题，25 个字符左右是一个合理的最大值。

## 标题栏可以提供有用信息

标题栏是用户注意到的消息框的第一部分，因此请让你的标题栏尽可能有用。习惯惯例是将宏的名称放在消息框的标题栏中，然后使用 `prompt` 参数来解释消息框中的按钮将触发什么操作。

此外，如果你需要修改宏，你可能会发现包含它们的版本号会很有帮助，这样用户就可以轻松地检查他们正在使用哪个版本的宏（并根据需要更新到较新的版本）。例如，`Delete Workbook` 宏在图 13.8 所示的消息框中被识别为版本 12.39。

图 13.8

通常，你需要为消息框指定 `title` 参数。你可能还想包含一个版本号。

![](img/03e3cf21a6476d99c08c2f87b3092f20_366_0.png)

像所示在按钮参数之后指定 `title` 参数：

```
Dim lngQuery As Long
lngQuery = MsgBox("Do you want to delete this workbook?", vbYesNo \
+ vbCritical + vbDefaultButton2, "Delete Workbook 12.39")
```

你可以使用字符串变量作为 `title` 参数。例如，你可以声明一个字符串变量，并使用它为宏调用的每个消息框提供标题。或者，你可能需要在消息框的标题中显示在宏中创建或存储的字符串。

## 避免在标题中使用特殊字符

不要尝试在 `title` 参数中放入换行符、回车符或制表符。VBA 会忽略它们。

## 为消息框添加帮助按钮

要为消息框添加帮助按钮，请使用 `vbMsgBoxHelpButton` 常量。你可以将此参数添加到你为消息框指定的指定的任何按钮中：

```
LngQuery = MsgBox("Do you want to delete this workbook", vbYesNo \
+ Critical + vbDefaultButton2 + vbMsgBoxHelpButton, \
"Delete Workbook")
```

添加 `vbMsgBoxHelpButton` 参数只是在消息框中放置帮助按钮——它并不会让帮助按钮在用户点击时显示帮助文件。你还必须指定你想要的帮助文件和主题（详情见下节）。图 13.9 显示了该语句产生的消息框。

图 13.9

使用 `vbMsgBoxHelpButton` 常量为消息框添加帮助按钮。

![](img/03e3cf21a6476d99c08c2f87b3092f20_367_0.png)

## 为消息框指定帮助文件

你可以为消息框使用的最后两个参数是 `helpfile` 和 `context` 参数：

- `helpfile` 参数是一个字符串，用于指定当用户从消息框调用帮助时 VBA 显示的帮助文件的名称和位置。
- `context` 参数是帮助文件中的一个帮助上下文编号。帮助上下文编号控制显示哪个帮助文件-主题。

`helpfile` 和 `context` 参数在你编写自己的帮助文件时主要有用，因为否则很难访问埋在官方帮助文件中的帮助上下文编号。

如果你正在编写自己的帮助文件，指定 `helpfile` 和 `context` 参数的语法非常简单：

```
Dim lngQuery As Long
MsgBox("Do you want to delete this workbook?", vbMsgBoxButton, + vbCritical + vbDefaultButton2, "Delete Workbook", "C:\Windows\Help\My_Help.chm", 1012)
```

在这种情况下，文件被指定为 `\Windows\Help\` 文件夹下的 `My_Help.chm`。VBA 显示主题编号 1012。

当用户点击消息框中的帮助按钮时，VBA 在帮助文件中显示指定的主题。消息框保持在屏幕上，因此当用户完成查阅后，可以在消息框中做出选择。

帮助文件启动屏幕的帮助上下文为 0。当你需要显示一个不知道帮助的帮助文件时，使用 0。VBA 提供了三个特殊常量来实现特定效果：

- **vbMsgForeground**: 告诉 VBA 使消息框处于前台。
- **vbMsgRight**: 告诉 VBA 从右到左排列文本。
- **vbMsgBidi**: 告诉 VBA 从左到右排列文本（双向系统）。

`helpfile` 和 `context` 参数在你编写自己的帮助文件时主要有用，因为否则很难访问埋在官方帮助文件中的帮助上下文编号。

例如，为了检查一个 vbYesNo 消息框以查看用户选择了哪个按钮，你可以使用一个简单的 If..Then..Else 语句：

```
Dim lngUserChoice As Long
lngUserChoice = MsgBox("Do you want to create the daily report?", - 
vbYesNo + vbQuestion, "Create Daily Report")
If lngUserChoice = vbYes Then
Goto CreateDailyReport
Else
Goto Bye
EndIf
```

如果用户选择“是”按钮，VBA 将跳转到由 `CreateDailyReport` 标签标识的代码行，并从那里继续执行宏；否则，它将跳转到末尾的 `Bye` 标签以终止宏。`If` 条件检查用户在消息框中选择的生成的响应，以确定其是否为 vbYes（通过点击 Yes 按钮或按下选中的 Yes 按钮生成）。`Else` 语句返回响应不是 vbYes——即如果用户点击了“否”按钮或按了 Esc 键。

## 输入框 (Input Boxes)

消息框告诉 VBA 用户点击了哪个按钮。有时你希望用户为你的宏提供一些文本，例如他们的姓名或生日。

当你想要从用户那里获取一个简单的文本信息时，请使用输入框。如果你不熟悉它的名称，一定对它的外观很熟悉：它们通常看起来像图 13.10 所示所示。

图 13.10

使用输入框从用户那里获取单条信息。

![](img/03e3cf21a6476d99c08c2f87b3092f20_370_0.png)

## 为复杂交互创建自定义框

为了从用户那里获取两个或多个信息，你可以连续使用两个或多个输入框，但对于用户来说，创建一个自定义对话框通常会更简单。你将在第 14 章开始学习构建自定义对话框。

## 输入框语法 (Input-Box Syntax)

显示输入框的语法与消息框的语法一样：

```
InputBox(prompt[, title] [, default], [xpos], [ypos], [helpfile, context])
```

以下是参数的含义：

- **Prompt** 一个必选的字符串，用于指定输入框中显示的提示内容。与 MsgBox 一样，prompt 的长度可达 1024 个字符，你可以使用换行符常量 (`vbCr`) 来强制换行。与 MsgBox 的 prompt 参数一样，如果提示内容超过 35 个字符，InputBox 会自动换行。
- **Title** 一个指定输入框标题栏文本的字符串。如果你没有指定 title 参数，VBA 将提供应用程序名称。
- **Default** 你可以使用此字符串来指定显示在输入框中的文本。默认参数也是个好主意，无论当默认值可能适用时（用户只需按 Enter 键即可接受），或者当你需要显示示例文本以便让用户理解你正在寻找什么类型的响应时。

这里有一个提示用户的合适文本示例：如果你显示一个询问用户姓名的输入框，可以像这样从 `ActiveDocument` 的 `BuildDocumentProperties` 集合中获取 Name 值：

```
Dim strAuthor As String
strAuthor = ActiveDocument.BuildDocumentProperties(wdPropertyLastAuthor)
```

- **xpos and ypos** 这些是指定屏幕上框位置的可选值。xpos 值控制输入框左边缘距离屏幕左边缘（而非 Word 窗口）的水平位置，而 ypos 控制输入框顶部距离屏幕顶部的垂直位置。每个测量单位都是 twips，如本章侧边栏“输入框通常显示在屏幕中心”中描述。如果你省略这两个参数，VBA 将输入框显示在屏幕中间的默认位置。
- **helpfile and context** 可选参数，用于指定从输入框跳转到用户的帮助文件和上下文。如果你使用了 helpfile，则必须也使用 context。

## 输入框通常显示在屏幕中心
