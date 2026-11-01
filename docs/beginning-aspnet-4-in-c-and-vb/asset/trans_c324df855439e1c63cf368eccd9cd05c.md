
TableLayoutPanel 使用网格结构来控制控件的布局。任何 Windows 窗体控件都可以成为 TableLayoutPanel 的子控件，包括另一个 TableLayoutPanel。这允许非常灵活和动态的窗口设计。将控件添加到 TableLayoutPanel 时，属性页的“布局”类别中会添加四个附加属性。它们是 Column、ColumnSpan、Row 和 RowSpan。与网页上的 HTML 表格非常相似，可以为每个控件设置列跨度和行跨度。默认情况下，控件将居中于表格的单元格中，但可以通过使用 Anchor 和 Dock 属性来更改。

可以使用 RowStyles 和 ColumnStyles 集合更改行和列的默认样式。这些集合分别包含 RowStyle 和 ColumnStyle 对象。Style 对象有一个共同属性 SizeType。SizeType 使用 SizeType 枚举来确定列宽或行高应如何调整大小。值包括 AutoSize、Absolute 和 Percent。AutoSize 与其他同级控件共享空间。Absolute 允许为大小设置固定像素数，Percent 则指示控件将列或宽度的大小设置为父控件的百分比。

行、列和子控件可以在运行时添加或移除。GrowStyle 属性采用 TableLayoutPanelGrowStyle 枚举值，该值设置表格在向已满的表格添加新控件时，是添加一列或一行，还是保持固定大小。如果值为 FixedSize，则在尝试添加另一个控件时会抛出 ArgumentException。如果表格中的单元格已满，控件将被放置在空单元格中。此属性仅在表格已满且添加控件时生效。

示例代码包含一个同时具有流布局面板和表格布局面板的窗体，以演示调整窗体大小对面板内控件的影响。

## SplitContainer

SplitContainer 控件实际上是三合一控件。它有两个面板控件，中间有一个条或拆分器。用户可以移动该条并调整面板大小。当面板调整大小时，面板中的控件也可以调整大小。SplitContainer 的最佳示例是文件资源管理器。左侧面板包含文件夹的 TreeView，右侧包含文件夹内容的 ListView。当用户将鼠标移到拆分条上时，光标会改变，表明该条可以移动。SplitContainer 可以包含任何控件，包括布局面板和其他 SplitContainer。这允许创建非常复杂和精细的窗体。

拆分条的移动和位置可以通过 SplitterDistance 和 SplitterIncrement 属性来控制。SplitterDistance 属性确定拆分器相对于控件左侧或顶部开始的位置。SplitterIncrement 确定拖动时拆分器移动的像素数。面板的最小大小可以通过 Panel1MinSize 和 Panel2MinSize 属性设置。这些属性也以像素为单位。

Splitter 控件引发两个与移动相关的事件：SplitterMoving 事件和 SplitterMoved 事件。一个在移动过程中发生，另一个在移动完成后发生。两者都接收 SplitterEventArgs。SplitterEventArgs 包含用于 Splitter 左上角的 X 和 Y 坐标（SplitterX 和 SplitterY）以及鼠标指针的 X 和 Y 坐标（X 和 Y）的属性。

## TabControl 和 TabPages

TabControl 允许您将相关控件分组到一系列选项卡页上。TabControl 管理 TabPages 集合。有几个属性控制 TabControl 的外观。Appearance 属性使用 TabAppearance 枚举来确定选项卡的外观。值为 FlatButtons、Buttons 或 Normal。Multiline 属性是一个布尔值，用于确定是否显示多行选项卡。如果 Multiline 属性设置为 false，并且选项卡数量超过显示区域可容纳的数量，则会出现箭头，允许用户滚动查看其余的选项卡。

TabPage 的 Text 属性是选项卡上显示的内容。Text 属性也是构造函数重载中的一个参数。

创建 TabPage 控件后，它基本上是一个容器控件，您可以在其中放置其他控件。Visual Studio .NET 中的设计器通过使用集合编辑器，可以轻松地将 TabPage 控件添加到 TabControl 控件中。添加每个页面时，您可以设置各种属性。然后，您可以将其他子控件拖到每个 TabPage 控件上。

您可以通过查看 SelectedTab 属性来确定当前选项卡。每次选择新选项卡时都会引发 SelectedIndexChanged 事件。通过侦听 SelectedIndexChanged 事件，然后使用 SelectedTab 确认当前选项卡，您可以根据每个选项卡进行特殊处理。例如，您可以管理每个选项卡显示的数据。

## ToolStrip

ToolStrip 控件是一个容器控件，用于创建工具栏、菜单结构和状态栏。ToolStrip 直接用于工具栏，并用作 MenuStrip 和 StatusStrip 控件的基类。

当用作工具栏时，ToolStrip 控件使用一组基于抽象 ToolStripItem 类的控件。ToolStripItem 添加了常见的显示和布局功能，并管理控件使用的大多数事件。ToolStripItem 派生自 System.ComponentModel.Component 类，而不是 Control 类。基于 ToolStripItem 的类必须包含在基于 ToolStrip 的容器中。

Image 和 Text 可能是最常设置的属性。可以使用 Image 属性设置图像，也可以使用 ImageList 控件并将其设置为 ToolStrip 控件的 ImageList 属性来设置图像。然后可以设置各个控件的 ImageIndex 属性。

ToolStripItem 上文本的格式通过 Font、TextAlign 和 TextDirection 属性来处理。TextAlign 设置文本相对于控件的对齐方式。这可以是 ContentAlignment 枚举值中的任意一个。默认值为 MiddleRight。TextDirection 属性设置文本的方向。值可以是 ToolStripTextDirection 枚举值中的任意一个，包括 Horizontal、Inherit、Vertical270 和 Vertical90。Vertical270 将文本旋转 270 度，Vertical90 将文本旋转 90 度。

DisplayStyle 属性控制在控件上显示文本、图像、文本和图像，还是不显示任何内容。当 AutoSize 设置为 true 时，ToolStripItem 将调整自身大小，以便仅使用最少的空间。

下表列出了直接派生自 ToolStripItem 的控件。

| ToolStrip 项 | 描述 |
|---|---|
| ToolStripButton | 表示用户可以选择的一个按钮。 |
| ToolStripLabel | 在 ToolStrip 上显示不可选择的文本或图像。ToolStripLabel 还可以显示一个或多个超链接。 |
| ToolStripSeparator | 用于分隔和分组其他 ToolStripItem。项目可以根据功能进行分组。 |
| ToolStripDropDownItem | 显示下拉项。是 ToolStripDropDownButton、ToolStripMenuItem 和 ToolStripSplitButton 的基类。 |
| ToolStripControlHost | 在 ToolStrip 上承载其他非 ToolStripItem 派生的控件。是 ToolStripComboBox、ToolStripProgressBar 和 ToolStripTextBox 的基类。 |

列表中的最后两项 ToolStripDropDownItem 和 ToolStripControlHost 值得进一步讨论。ToolStripDropDownItem 是用于构建菜单结构的 ToolStripMenuItems 的基类。ToolStripMenuItems 添加到 MenuStrip 控件中。如前所述，MenuStrip 派生自 ToolStrip 控件。当需要操作或扩展菜单项时，这一点很重要。因为工具栏和菜单派生自相同的类，所以创建用于管理和执行命令的框架要容易得多。

ToolStripControlHost 可用于承载其他不从 ToolStripItem 派生的控件。请记住，ToolStrip 可以直接承载的唯一控件是那些从 ToolStripItem 派生的控件。

## MenuStrip

MenuStrip 控件是应用程序菜单结构的容器。如前所述，MenuStrip 派生自 ToolStrip 类。菜单系统是通过向 MenuStrip 添加 ToolStripMenuItem 对象来构建的。您可以在代码中或 Visual Studio 的设计器中执行此操作。在设计器中，将 MenuStrip 控件拖到窗体上，MenuStrip 将允许直接在菜单项上输入菜单文本。

MenuStrip 控件只有几个附加属性。GripStyle 使用 ToolStripGripStyle 枚举将手柄设置为可见或隐藏。MdiWindowListItem 属性接受或返回一个 ToolStripMenuItem。此 ToolStripMenuItem 是显示 MDI 应用程序中所有打开窗口的菜单。

## ContextMenuStrip

要显示上下文菜单（即用户右键单击鼠标时显示的菜单），可使用 ContextMenuStrip 类。与 MenuStrip 一样，ContextMenuStrip 是 ToolStripMenuItems 对象的容器。但是，它派生自 ToolStripDropDownMenu。创建 ContextMenu 的方式与创建 MenuStrip 相同。添加 ToolStripMenuItems，并定义每个项的单击事件以执行特定任务。上下文菜单分配给特定的控件。这是通过设置控件的 ContextMenuStrip 属性来完成的。当用户右键单击控件时，将显示菜单。

## ToolStripMenuItem

ToolStripMenuItem 是构建菜单结构的类。每个 ToolStripMenuItem 对象表示菜单系统上的一个菜单选项。每个 ToolStripMenuItem 都有一个 ToolStripItemCollection 来维护子菜单。此功能继承自 ToolStripDropDownItem。

因为 ToolStripMenuItem 派生自 ToolStripItem，所以所有相同的格式属性都适用。图像显示为菜单文本右侧的小图标。使用 Checked 和 CheckState 属性，菜单项旁边可以显示复选标记。

可以为每个菜单项分配快捷键。快捷键通常由两个键组成，例如 Ctrl+C（复制的常用快捷键）。分配快捷键后，可以通过将 ShowShortcutKey 属性设置为 true 来选择性地在菜单上显示它。

为了使菜单项有用，它必须在用户单击它或使用定义的快捷键时执行某些操作。最常见的方法是处理 Click 事件。如果使用了 Checked 属性，则可以使用 CheckStateChanged 和 CheckedChanged 事件来确定选中状态的更改。

## ToolStripManager

菜单和工具栏结构可能变得庞大且难以管理。ToolStripManager 类提供了创建更小、更易于管理的菜单或工具栏结构片段，然后在需要时组合它们的能力。一个示例是窗体上有多个不同的控件。
