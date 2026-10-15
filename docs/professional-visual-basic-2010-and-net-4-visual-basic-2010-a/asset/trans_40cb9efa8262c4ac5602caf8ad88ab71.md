

Padding 属性适用于 FlowLayoutPanel 或其他容器控件。当控件嵌入到 FlowLayoutPanel 中时，FlowLayoutPanel 的 Padding.Left、Padding.Right、Padding.Top 和 Padding.Bottom 属性决定了控件应与容器内部边缘保持多远的距离。

你可以通过更改前一个示例中 FlowLayoutPanel 的 Padding 属性来看到 Padding 属性的实际效果。如果将所有 Padding 设置都设为 15 像素，并将第一个按钮的 Margin 属性重置回默认值，那么窗体在视觉设计器中看起来就像图 14-16 所示。

![](img/d99870e80390742f93963da7be0b2e61_566_0.png)

图 14-16

请注意，FlowLayoutPanel 中的所有控件现在都至少距离边缘 15 像素。

如果包含的控件的 Dock 属性已设置，则 Padding 属性也适用于其他容器控件。如果 Padding 设置不为零，则停靠的控件将根据 Padding 属性指定的量从容器边缘偏移。

## TableLayoutPanel 控件

另一个使用子控件动态布局的控件是 TableLayoutPanel。该控件由行和列的表格组成，形成一个矩形的单元格数组。你可以在每个单元格中放置一个控件。然而，该控件本身也可以是一个容器，例如 Panel 或 FlowLayoutPanel。

你可以通过设置一些关键属性来控制列和行的尺寸。对于列，使用 ColumnCount 属性设置列数，然后使用 ColumnStyles 集合控制每个单独的列。单击 ColumnStyles 集合的按钮时，会出现一个设计器窗口，使你能够为每列设置两个关键属性：SizeType 和 Width。

SizeType 可以设置为以下枚举之一：

- Absolute — 将列宽设置为像素中的固定大小
- AutoSize — 表示列的大小应由 TableLayoutPanel 管理，TableLayoutPanel 根据列中包含的最宽控件分配宽度给该列
- Percent — 设置使用 TableLayoutPanel 的百分比作为列宽

Width 属性仅在你未选择 AutoSize 的 SizeType 时才适用。它设置列宽的像素数（如果 SizeType 为 Absolute）或列的百分比宽度（如果 SizeType 为 Percent）。

同样，对于行，有 RowCount 属性来设置行数，以及 RowStyles 集合来管理行的大小。RowStyles 中的每一行都有一个 SizeType，其工作方式与列的 SizeType 相同，只是它管理行的高度而不是列的宽度。Height 属性用于行而不是 Width 属性，但其工作方式相对应。Height 要么是像素数（如果 SizeType 为 Absolute），要么是 TableLayoutPanel 高度的百分比（如果 SizeType 为 Percent）。如果 SizeType 为 AutoSize，则行会调整为该行中最宽控件的高度。

一种高级的 UI 布局技术是首先创建一个 TableLayoutPanel，然后在 TableLayoutPanel 的某些单元格中嵌入一个 FlowLayoutPanel。这使得可以在一个单元格中包含多个控件，并在单元格大小变化时重新定位它们。

使用 TableLayoutPanel 嵌入 FlowLayoutPanel 的逐步示例包含在下一章的“创建复合 UserControl”部分中。

## Panel 和 GroupBox 容器控件

当然，并非所有应用程序都需要前面讨论的容器的动态布局。Windows Forms 包含两个静态容器控件，其中包含的控件的位置和布局完全不会调整。

这两个容器，只有细微差别，是 GroupBox 控件和 Panel 控件。

这两个控件在以下方面相似：

- 它们可以作为其他控件的容器。
- 如果它们被隐藏或移动，则该操作会影响容器中的所有控件。

GroupBox 控件始终具有边框，并且如果需要可以具有标题。边框始终以相同的方式设置。图 14-17 显示了一个包含三个 RadioButton 控件的 GroupBox 控件的窗体。

Panel 控件与 GroupBox 控件有三个主要区别：

- 它在 BorderStyle 属性中有显示边框的选项，默认值为无边框。
- 如果其 AutoScroll 属性设置为 True，则具有滚动功能。
- 它不能设置标题或标题。

图 14-18 显示了一个包含 Panel 控件的窗体，其 BorderStyle 属性设置为 FixedSingle，通过将 AutoScroll 设置为 True 打开滚动，并包含一个太大而无法一次性显示的 CheckedListBox（这迫使面板显示滚动条）。

![](img/d99870e80390742f93963da7be0b2e61_567_0.png)

![](img/d99870e80390742f93963da7be0b2e61_567_1.png)

## Extender Providers

Windows Forms 具有一组只能与视觉控件关联使用的组件。这些组件被称为 extender providers。它们与 Visual Studio IDE 协同工作，导致窗体上的控件在属性窗口中出现新的属性。

Extender providers 除与其他控件结合外没有可见表现，因此出现在组件托盘中。随 Windows Forms 2.0 提供的三个 extender providers 是 HelpProvider、ToolTip 和 ErrorProvider。全部三个基本以相同的方式工作。每个 extender provider 实现“附加”到其他控件的属性。最好的了解其工作原理的方法是通过示例，因此让我们用 ToolTip 组件来做。

### ToolTip

ToolTip 是内置 extender providers 中最简单的。它为每个控件添加一个属性：ToolTip on ToolTip1（假设 ToolTip 控件具有默认名称 ToolTip1）。该属性的工作方式与 VB6 中的 ToolTipText 属性非常相似，实际上取代了它。

要亲眼看到这一点，创建一个 Windows Forms 应用程序。在为项目创建的空白 Form1 上放置几个按钮。查看 Button1 的属性窗口。请注意，它没有任何 ToolTip 属性。

拖动 ToolTip 控件，它将被放置在组件托盘中。返回到 Button1 的属性窗口。现在会出现一个名为 ToolTip on ToolTip1 的属性。为此属性设置任何你喜欢的字符串值。

运行项目并将鼠标指针悬停在 Button1 上。你将看到一个包含你为 ToolTip on ToolTip1 属性输入的字符串值的 ToolTip。

ToolTip 组件的其他属性使你能够控制 ToolTip 的其他特性，例如 ToolTip 出现前的初始延迟。

Windows Forms 2.0 中的新功能是可以将 ToolTips 的形状更改为“气球”。这是通过将 ToolTip 组件的 IsBalloon 属性设置为 True 来完成的。不是悬浮的矩形 ToolTip，ToolTip 具有圆角矩形轮廓，并指向其关联的控件，不像漫画条中的对话框气球。图 14-19 显示了一个示例。

![](img/d99870e80390742f93963da7be0b2e61_567_2.png)

### HelpProvider

HelpProvider 使控件能够通过按 F1 获得关联的上下文相关帮助。当 HelpProvider 添加到窗体时，窗体上的所有控件都会获得表 14-3 中显示的新属性，这些属性会出现在控件的属性窗口中。

### 表 14-3：HelpProvider 组件的属性

| 属性 | 用途 |
|---|---|
| HelpString on HelpProvider1 | 当控件获得焦点并按下 F1 时，为控件提供弹出式 ToolTip。如果 HelpKeyword 和 HelpNavigator 属性（稍后描述）被设置为提供对帮助文件的有效引用，则 HelpString 值将被帮助文件信息忽略。 |
| HelpKeyword on HelpProvider1 | 为此控件的上下文相关帮助提供帮助文件中的关键字或其他索引。HelpProvider1 控件有一个属性来指示使用哪个帮助文件。这取代了 VB6 中的 HelpContextID 属性。 |
| HelpNavigator on HelpProvider1 | 包含一个枚举值，确定 HelpKeyword 中的值如何用于引用帮助文件。有几个可能的值用于在帮助文件中显示主题、索引或目录等元素。 |
| ShowHelp on HelpProvider1 | 确定 HelpProvider 控件是否对此控件处于活动状态 |

填写 HelpString 属性会立即导致控件在控件获得焦点并按下 F1 时提供 ToolTip 帮助。HelpProvider 控件有一个属性指向帮助文件（HTML 帮助文件或 Win32 帮助文件），并且 HelpTopic 属性中的帮助主题指向此文件中的主题。

### ErrorProvider

ErrorProvider 组件以简单、视觉的方式向用户指示窗体上的控件与其关联的错误。控件在表单上使用 ErrorProvider 时添加的属性称为 Error on ErrorProvider1（假设 ErrorProvider 具有默认名称 ErrorProvider1）。将此属性设置为字符串值会导致错误图标出现在控件旁边。此外，文本会在鼠标悬停在错误图标上时出现在 ToolTip 中。

图 14-20 显示了一个包含多个文本框的屏幕，其中一个文本框旁边有一个错误图标（带 ToolTip）。错误图标和 ToolTip 由 ErrorProvider 显示和管理。

ErrorProvider 组件的默认图标是一个带有感叹号的红色圆圈。当文本框的 Error 属性被设置时，图标会闪烁几秒钟，悬停在图标上会使 ToolTip 出现。编写自己的代码来设置 Error 属性在“在代码中使用 Extender Providers”部分中进行了说明。

![](img/d99870e80390742f93963da7be0b2e61_568_0.png)

# 图 14-20

### Extender Providers 的属性

除了为其他控件提供属性外，extender providers 也有自己的属性。例如，ErrorProvider 有一个名为 BlinkStyle 的属性。当它设置为 NeverBlink 时，受 ErrorProvider 影响的所有控件的图标闪烁都会停止。

ErrorProvider 的其他属性使你能够更改诸如使用的图标以及图标相对于包含错误字段的位置等内容。例如，你可能希望图标出现在字段左侧而不是默认的右侧。你也可以在窗体上使用多个错误提供程序。例如，你可能希望向用户发出警告，而不是错误。第二个带有黄色图标的错误提供程序可用于此功能。

