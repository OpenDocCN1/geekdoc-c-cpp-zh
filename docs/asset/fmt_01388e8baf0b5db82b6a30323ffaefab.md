
![](/57baed2319be0bb1b5f98674846f2711_623_0.png)

图 14.39 | 键盘事件和事件参数。图 14.40 展示了如何使用按键处理程序显示用户按下的按键。程序是一个带有两个 Label 的 Form，其中一个显示按下的按键，另一个显示修饰键信息。

### 第 14 节 使用 Windows Forms 的图形用户界面：部分 I

| c) A A | d) Tab Tab |
| :--- | :--- |
| KeyDemo A | KeyDemo Tab |
| Key pressed: A | Key pressed: Tab |
| Alt: No | Alt: No |
| Shift: Yes | Shift: No |
| Ctrl: No | Ctrl: No |
| KeyCode: A | KeyCode: Tab |
| KeyData: A, Shift | KeyData: Tab |
| KeyValue: 65 | KeyValue: 9 |

图 14.40 | 显示关于按下的按键的信息。（部分 2）。

# 14.13 总结

默认情况下，键盘事件由当前获得焦点的控件处理。有时，让表单（Form）处理这些事件是合适的。这可以通过将 Form 的 `KeyPreview` 属性设置为 `true` 来实现，这会让 Form 在键盘事件传递给其他控件之前接收到它们——例如，即使 Form 内部的控件拥有焦点而不是 Form 本身，按键也会触发 Form 的 `KeyPress` 事件。

# 14.13 总结

本章介绍了常用的 GUI 控件。我们详细讨论了事件处理，并展示了如何创建事件处理器。我们展示了如何使用委托（delegates）将事件处理器连接到特定控件的事件。你学习了如何使用控件的属性和 Visual Studio 来指定 GUI 的布局。然后，我们演示了几个控件，从标签（Label）、按钮（Button）和文本框（TextBox）开始。你学习了如何使用组框（GroupBox）和面板（Panel）来组织其他控件。我们演示了复选框（CheckBox）和单选按钮（RadioButton），它们是允许用户在多个选项之间进行选择的状态按钮。我们在图片框（PictureBox）中显示图像，在 GUI 上使用工具提示（ToolTip）显示帮助文本，并使用数字数字框（NumericUpDown）为用户指定数值输入值的范围。然后，我们演示了如何处理鼠标和键盘事件。下一章将介绍额外的 GUI 控件。你将学习如何为你的 GUI 添加菜单，并创建显示多个 Form 的 Windows Forms。

# 摘要

# 第 14.1 节 引言

- 图形用户界面（GUI）允许用户通过视觉方式与程序进行交互。
- GUI 由 GUI 控件构建而成。
- GUI 控件是对象，可以在屏幕上显示信息，或允许用户通过鼠标、键盘或其他输入形式与应用程序交互。

# 第 14.2 节 Windows Forms

- Windows Forms 用于创建程序的 GUI。
- Form（表单）是出现在桌面上的一个图形元素；它可以是对话框、窗口或 MDI（多文档界面）窗口。
- 组件（component）是实现接口的类的实例，该接口定义了组件必须实现的行为，例如控件是如何加载的。
- 控件（control）是在运行时具有具有图形表示的组件。
- 某些组件缺乏图形表示（例如 Windows.Forms 命名空间下的 Timer 类）。此类组件在运行时是不可见的。
- 当屏幕上有多个窗口时，活动窗口是最前面的窗口，并且具有高亮显示的标题栏。当用户点击窗口内部时，该窗口就变成了活动窗口。
- 活动窗口被称为“拥有焦点”。
- Form 是控件和组件的容器。

# 第 14.3 节 事件处理

- GUI 是事件驱动的。
- 当用户与 GUI 组件交互时，这种交互（被称为事件）会触发程序执行任务。常见事件包括点击按钮、在文本框中输入内容、从菜单中选择项目、关闭窗口和移动鼠标。
- 响应事件执行任务的方法被称为事件处理器（event handler），而响应事件的整体处理过程被称为事件处理（event handling）。

# 第 14.3.1 节 简单的事件驱动 GUI

- 只有当用户执行特定事件时，事件处理器才会执行。
- 每个事件处理器在被调用时会接收两个参数。第一个是通常命名为 `sender` 的对象引用，它是生成事件对象的引用。第二个是类型为 `EventArgs`（其派生类之一）的事件对象的引用，通常命名为 `e`。该对象包含有关发生事件的额外信息。
- `EventArgs` 是表示事件信息的类的基类。

# 第 14.3.2 节 自动生成的 GUI 代码

- Visual Studio 会创建初始化你在 GUI 设计窗口中构建的 GUI 的代码。这些自动生成的代码位于表单的 `Designer.cs` 文件中。
- 定义 GUI 的自动生成代码是 Form 类的一部分。在类声明中使用 `partial` 修饰符允许该类被拆分到多个文件中。
- `Designer.cs` 文件包含了你在设计模式下创建的的控件。
- `Designer.cs` 文件包含了用于释放资源的 `Dispose` 方法和 `InitializeComponent` 方法，后者设置了 Form 及其控件的属性。
- Visual Studio 使用 `InitializeComponent` 中的代码来创建你在设计视图中看到的 GUI。更改此方法中的代码可能会导致 Visual Studio 无法正常显示 GUI。

# 第 14.3.3 节 委托与事件处理机制

- 生成事件的控件被称为事件发送者（event sender）。
- 事件处理方法——被称为事件处理器（event handler））响应控件生成的特定事件。
- 当事件发生时，事件发送者将其事件发送给处理器以执行任务。
- .NET 事件处理机制允许你为事件处理方法自定义名称。然而，每个事件处理方法必须声明参数以接收其所处理的事件信息。
- 事件处理器通过称为委托（delegates）的特殊对象连接到控件的事件。
- 委托对象持有一个方法的引用，该签名由委托类型的声明指定。
- GUI 控件具有预定义的委托，对应于它们可以生成的每一个事件。
- 由于每个事件处理器都声明为委托，事件发送者可以在事件发生时调用相应的方法。
- 事件委托表示一组具有相同签名的方法，可以被用来处理事件的调用。
- 事件发生时，`MulticastDelegate` 允许调用多个方法。
- 事件委托派自 `MulticastDelegate`（来自 `System` 命名空间）。

# 第 14.3.4 节 另一种创建事件处理器的方法

- 在设计器中双击控件可以创建事件的处理器。
- 通常情况下，控件可以产生许多不同的事件，每个事件都有自己的事件处理器。
- 你可以通过属性窗口创建额外的事件处理器。
- 如果你选择了 Form 上的控件，点击属性窗口中的事件图标（闪电图标），将列出该控件的所有事件。双击事件名称可以在编辑器中显示事件处理器，或者创建相应的事件处理器。
- 如果你选择一个事件，使用右侧的下拉列表选择已存在的事件处理器。下拉列表中显示的方法具有处理该事件的正确签名。
- 单个事件可以处理多个控件的事件。

# 第 14.3.5 节 定位事件信息

- 阅读文档以了解每个控件触发的不同事件。要这样做，可以在 IDE 中选择控件并按 F1 键显示该控件的在线帮助。该网页包含有关控件类的基本信息。点击事件链接显示控件支持的事件。

# 第 14.4 节 控件属性与布局

- 控件派自 `System.Windows.Forms`。
- `Select` 方法将焦点转移到控件并使其变为活跃。
- `Enabled` 属性指示用户是否可以与控件交互以产生事件。
- 程序员可以通过将 `Visible` 属性设置为 `false` 或调用 `Hide` 来隐藏控件而不禁用它。
- 锚定（Anchoring）使控件在容器调整大时与侧边保持固定距离。
- 停靠（Docking）将控件附加到容器，使其跨越整个侧边或填充剩余空间。
- `Anchor` 和 `Dock` 属性相对于控件的父容器设置，父容器可以是 Form 或其他父容器（如 Panel）。
- Form（或其他控件）的最小和最大尺寸分别通过 `MinimumSize` 和 `MaximumSize` 设置。
- 在 Form 上拖动控件时，会出现蓝线（称为对齐线），帮助你将控件与其他控件以及 Form 的边缘对齐。
- Visual Studio 还提供了格式（Format）菜单，其中包含修改 GUI 布局的若干选项。

# 第 14.5 节 标签、文本框和按钮

- 标签（Label）提供了用户无法直接修改的信息（以及图像）。
- 文本框（TextBox 类）是程序可以显示文本或用户可以通过键盘输入文本的区域。
- 密码文本框是会隐藏用户输入信息的 TextBox。当用户输入时，密码文本框通过显示密码字符（*）掩盖用户输入。如果你将 `SystemPasswordChar` 属性设置为 `true`，则 TextBox 就会变成密码文本框。

# 第 14 章使用 Windows Forms 构建图形用户界面：第一部分

- 按钮（Button）是用户点击以触发程序中的操作或选择选项的控件。
- 所有按钮类都继承自 ButtonBase 类（System.Windows.Forms 命名空间），该类定义了共同特征。

## 第 14.6 节 组框 (GroupBox) 和面板 (Panel)

- GroupBoxes 和 Panels 用于 GUI 上排列控件。
- GroupBoxes 和 Panels 通常用于将多个功能类似的控件或与 GUI 相关的控件分组。
- GroupBox 可以显示标题（即文本）且不包含滚动条，而 Panel 可以包含滚动条且不包含标题。
- GroupBox 默认具有边框；Panel 可以设置其 `BorderBorderStyle` 以使其也具有边框。
- GroupBox 或 Panel 的控件被添加到它们的 `Controls` 属性中。
- 要启用滚动条，将 Panel 的 `AutoScroll` 属性设置为 `true`。如果 Panel 调整大小后无法显示所有控件，则会出现滚动条。

## 第 14.7 节 复选框 (CheckBox) 和单选按钮 (RadioButton)

- CheckBoxes 和 RadioButtons 可以处于开启/关闭/false 状态。
- CheckBox 和 RadioButton 类继承自 ButtonBase 类。
- CheckBox 是一个空白或包含勾选标记的小正方形。当 CheckBox 被选中时，方框内会出现一个勾选标记。可以同时选择多个 CheckBox。
- 通过将其 `ThreeState` 属性设置为 `true`，可以将 CheckBox 配置为三种状态：已选（checked）、未勾选（unchecked）和不确定（indeterminate）。
- 字体样式可以通过位运算符进行组合，例如逻辑或 (|) 运算符或逻辑异或 (^) 运算符。
- 单选按钮（通过 `RadioButton` 类定义）与 CheckBoxes 类似，它们有两个状态：已选中和未选中（也称为已取消选择）。
- RadioButtons 通常作为一个组运行，其中一次只能选择一个。选中其中一个 RadioButton 会强制其他按钮取消选中状态。因此，RadioButtons 用于表示一组互斥的选项。
- 添加到容器中的所有 RadioButtons 都会成为同一组的一部分。

## 第 14.8 节 图像框 (PictureBox)

- PictureBox 显示图像。
- `Image` 属性指定显示哪种图像（Normal, StretchImage, Autosize, CenterImage, 或 Zoom）。
- 你可以将图像作为资源嵌入到项目中。
- 嵌入的图像文件出现在解决方案资源生成器中名为 Resources 的文件夹中。
- `Resources` 类（位于项目的 Properties 命名空间）提供了对项目资源的访问。
- `ResourceManager` 提供了以编程方式访问项目资源的方法。
- 要访问项目资源中的图像（或其他任何资源），使用 `ResourceManager` 类的 `GetObject` 方法，该方法将 Resources 选项卡中的资源名称作为参数，并将资源作为 `Object` 返回。

## 总结

- `Resources` 类通过形如 `Resources.resourceName` 的表达式直接访问你定义的资源。

## 第 14.9 节 工具提示 (ToolTips)

- 工具提示可以帮助你熟悉熟悉表单（Form）的功能，并作为每个控件功能的有用提醒。在属性窗口中，你可以通过设置 `componentName` 上的 `ToolTip` 为控件指定工具提示，其中 `componentName` 是 ToolTip 的名称。
- `ToolTip` 组件用于为你的应用程序添加工具提示。
- `ToolTip` 组件放置在组件托盘中——即设计模式下表单下方的灰色区域。

## 第 14.10 节 数值增大控件 (NumericUpControl)

- 有时，你想限制用户的输入在一个特定的数值范围内。这就是 `NumericUpControl` 的目的。
- `NumericUpControl` 表现为一个 TextBox，右侧有两个小按钮，一个带有向上箭头，另一个带有向下箭头。默认情况下，用户向此控件输入数字值（因为它是一个 TextBox），或者点击向上向下箭头来增加或减少控件中的值。
- 范围内的最大值和最小值分别通过 `Maximum` 和 `Minimum` 属性指定（类型均为 `decimal`）。
- `Increment` 属性（类型为 `decimal`）指定当用户点击控件的向上向下箭头时，控件中当前数字的变化量。
- 设置 `NumericUpControl` 的 `ReadOnly` 属性表示用户只能使用向上和向下箭头来修改 `NumericUpControl` 中的值。

## 第 14.11 节 鼠标事件处理

- 当鼠标与控件交互时，会发生并生成鼠标事件。
- 可以为 `System.Windows.Forms.Control` 的任何子类处理鼠标事件。
- `MouseEventArgs` 包含与鼠标事件相关的信息，如鼠标指针的 x 和 y 坐标、按下的鼠标按钮（左、右或中）以及鼠标点击次数。
- 当用户按住鼠标按钮时，系统生成 `MouseDown` 事件。
- 当用户释放鼠标按钮（完成“点击”操作）时，系统生成单个 `MouseUp` 事件。
- 每当鼠标移动到控件上方时，都会触发该控件的 `Mouse` 事件。

## 第 14.12 节 键盘事件处理

- 当键盘上的按键被按下和释放时，发生键事件。
- 有三种键事件：`KeyPress`、`KeyUp` 和 `KeyDown`。
- 当用户按下字符、空格键或退格键时，发生 `KeyPress` 事件。可以通过处理程序的 `KeyPressEventArgs` 的 `KeyChar` 属性确定特定按键。
- `KeyPress` 事件不指示在发生键事件时是否按下了修饰键。如果此信息很重要，应该使用 `KeyUp` 或 `KeyDown` 事件。

## 术语

- 活动控件 (active control)
- 活动窗口 (active window)
- 锚定控件 (anchor a control)
- 位运算符 (bitwise operator)
- 按钮属性和事件 (Button properties and events)
- MouseEventArgs 的按钮属性 (Button property of class MouseEventArgs)
- ButtonBase 类 (ButtonBase class)
- 复选框 (checkbox)
- CheckBox 类 (CheckBox class)
- CheckBox 的选中属性 (Checked property of class CheckBox)
- RadioButton 的选中属性 (Checked property of class RadioButton)
- CheckBox 的 Changed 事件 (Changed event of class CheckBox)
- CheckBox 的 State 属性 (State property of class CheckBox)
- Color 结构 (Color structure)
- 组件 (component)
- 组件托盘 (component tray)
- 容器 (container)
- Control 类 (Control class)
- 容器的 Controls 属性 (Controls property of a)
- 默认事件 (default event)
- 委托 (delegate)
- 委托类 (delegate class)
- 委托关键字 (delegate keyword)
- 取消选择状态 (deselected state)
- DialogResult 枚举 (DialogResult enumeration)
- 停靠控件 (dock a control)
- Control 的 Dock 属性 (Dock property of class Control)
- Control 的 Enabled 属性 (Enabled property of class Control)
- 事件 (event)
- 事件驱动编程 (event-driven programming)
- 事件处理器 (event handler)
- 事件处理 (event handling)
- 事件多路 (event multicasting)
- 事件发送者 (event sender)
- Graphics 的 Ellipse 方法 (Ellipse method of class Graphics)
- Button 的 FlatStyle 属性 (FlatStyle property class Button)
- 焦点 (focus)
- Font 类 (Font class)
- FontStyle 枚举 (FontStyle enumeration)
- ResourceManager 的 GetObject 方法 (GetObject method of class ResourceManager)
- Graphics 类 (Graphics class)
- GroupBox 类 (GroupBox class)
- Size 结构 (Height property structure Size)
- IComponent 接口 (IComponent interface)
- NumericUpDown 的 Increment 属性 (Increment property of class NumericUpDown)
- 键码 (key code)
- 键事件 (key event)
- KeyPressEventArgs 的 KeyChar 属性 (KeyChar property of class KeyPressEventArgs)
- KeyEventArgs 的 KeyCode 属性 (KeyCode property of class KeyEventArgs)
- KeyEventArgs 的 KeyData 属性 (KeyData property of class KeyEventArgs)
- Control 的 KeyDown 事件 (KeyDown event of class Control)
- KeyEventArgs
- Control 的 KeyPress 事件 (KeyPress event of class Control)
- Keys 枚举 (Keys enumeration)
- Control 的 KeyUp 事件 (KeyUp event of class Control)
- Control 的 Maximum 属性 (Maximum property of class Control)
- Control 的 Minimum 属性 (Minimum property of class Control)
- Control 的 MinimumSize 属性 (MinimumSize property of Control)
- 鼠标点击 (mouse click)
- 鼠标事件 (mouse event)
- MouseDown 事件 (MouseDown event)
- MouseEvent 类 (MouseEvent class)
- 鼠标移动 (MouseMove)
- MouseUp 事件 (MouseUp event)
- 多路委托 (multicast delegate)
- Multicast 类 (Multicast class)
- 多个文档 (multiple document)
- 互斥 (mutual exclusion)
- NumericUpDown 类 (NumericUpDown class)
- Control 的 Padding 属性 (Padding property of class Control)
- Panel 类 (Panel class)
- 部分类类 (partial class)
- Picture 类 (Picture class)
- 单选按钮 (radio button)
- RadioButton组 (RadioButton group)
- Control 的 ReadOnly 属性 (ReadOnly property of class Control)
- ResourceManager 类 (ResourceManager class)
- Resources 类 (Resources class)
- Control 的 Select 方法 (Select method of class Control)
- 选择状态 (selected state)
- Control 的 Size 属性 (Size property of class Control)
- Size 结构 (Size structure)
- SolidBrush (SolidBrush)
- 状态 (state)
- Font 的 Style (Style of Font)
- Control 的 TabIndex 属性 (TabIndex of class Control)
- Control 的 TabStop 属性 (TabStop property of class Control)
- ToolTip 类 (ToolTip class)
- CheckBox 的 ThreeState 属性 (ThreeState property of CheckBox)
- TextBox 的 UsePasswordChar (UsePasswordChar of class TextBox)
- NumericUpDown 的 Value 属性 (Value property of class NumericUpDown)
- Control 的 Visible 属性 (Visible property of class Control)
-  结构 (width property structure)

## 总结

- Resources 类通过形如 `Resources.resourceName` 的表达式直接访问你定义的资源。

## 第 14.9 节 工具提示

- 工具提示可以帮助你熟悉表单（Form）的功能，并作为每个控件功能的有用提醒。在属性窗口中，你可以通过设置 `componentName` 上的 `ToolTip` 为控件指定工具提示，其中 `componentName` 是 ToolTip 的名称。
- ToolTip 组件用于为你的应用程序添加工具提示。
- ToolTip 组件放置在组件托盘中——即设计模式下表单下方的灰色区域。

## 第 14.10 节 数值增大控件 (NumericUpControl)

- 有时，你想限制用户的输入在一个特定的数值范围内。这就是 `NumericUpControl` 的目的。
- NumericUpControl 表现为一个 TextBox，右侧有两个小按钮，一个带有向上箭头，另一个带有向下箭头。默认情况下，用户向此控件输入数字值（因为它是一个 TextBox），或者点击向上向下箭头来增加或减少控件中的值。
- 范围内的最大值和最小值分别通过 `Maximum` 和 `Minimum` 属性指定（类型均为 `decimal`）。
- `Increment` 属性（类型为 `decimal`）指定当用户点击控件的向上向下箭头时，控件中当前数字的变化量。
- 设置 `NumericUpControl` 的 `ReadOnly` 属性表示用户只能使用向上向下箭头来修改 `NumericUpControl` 中的值。

## 第 14.11 节 鼠标事件处理

- 当鼠标与控件交互时，会发生并生成鼠标事件。
- 可以为 `System.Windows.Forms.Control` 的任何子类处理鼠标事件。
- MouseEventArgs 包含与鼠标事件相关的信息，如鼠标指针的 x 和 y 坐标、按下的鼠标按钮（左、右或中）以及鼠标点击次数。
- 当用户按住鼠标按钮时，系统生成 `MouseDown` 事件。
- 当用户释放鼠标按钮（完成“点击”操作）时，系统生成单个 `MouseUp` 事件。
- 每当鼠标移动到控件上方时，都会触发该控件的 `Mouse` 事件。

## 第 14.12 节 键盘事件处理

- 当键盘上的按键被按下和释放时，发生键事件。
- 有三种键事件：`KeyPress`、`KeyUp` 和 `KeyDown`。
- 当用户按下字符、空格键或退格键时，发生 `KeyPress` 事件。可以通过处理器的 `KeyPressEventArgs` 的 `KeyChar` 属性确定特定按键。
- `KeyPress` 事件不指示在发生键事件时是否按下了修饰键。如果此信息很重要，应该使用 `KeyUp` 或 `KeyDown` 事件。

## 自测练习

### 14.1 说明以下每个陈述的正确与否。如果是错误的，请解释原因。

- a) 活动控件包含关于修饰键的数据。
- b) 表单（Form）是一个容器。
- c) 所有的 Form、控件都是类。
- d) 复选框（CheckBox）用于表示一组互斥的选项。
- e) 标签（Label）显示可以编辑。
- f) 按钮按下产生事件。
- g) 所有事件使用相同的事件参数。
- h) Visual Studio 可以注册事件并创建事件处理器。
- i) 数字减少控件用于指定数值范围。
- j) 控件的工具提示使用 `ToolTip` 属性设置。

### 14.2 填空下列句子的空白：

- a) 活动控件被认为具有焦点。
- b) Form 充当添加的控件的____。
- c) GUI 是____ 驱动的。
- d) 每个处理事件的方法都具有相同的____。
- e) ____ 处理带有字符的输入。
- f) 类和____帮助 GUI 上的控件并为单选按钮提供逻辑分组。
- g) 事件在键盘按键被按下或释放时发生。
- h) 修饰键是____和____。
- i) 一个____可以用于调用多个方法。

## 自测练习答案

14.1 a) 正确；c) 正确；d) 错误。单选按钮（RadioButtons）用于表示一组互斥的选项。e) 错误。标签（Label）的文本无法由用户编辑。f) 正确；g) 错误。某些鼠标事件使用 `MouseEvents`；h) 正确；j) 错误。控件的工具提示使用一个必须添加到应用程序中的 `ToolTip` 属性。

14.2 a) 焦点; b) 容器; c) 事件; d) 签名; e) 密码; f) GroupBox、Panel; g) 鼠标点击、鼠标移动; h) 键; i) Shift、Ctrl、Alt; j) 多路调用。

**14.3 扩展 14.26 中的程序，为每种字体样式包含一个 CheckBox。[提示：使用逻辑异或 (^) 而不是显式测试它。]**

**14.4 创建 14.41 中的 GUI（你不需要提供功能）。**

# 第 14 章 使用 Windows Forms 构建图形用户界面：第一部分

![](img/57baed2319be0bb1b5f98674846f2711_634_0.png)

图 14.41 | 计算器 GUI。

## 14.5 创建图 14.42 中的 GUI（你不需要提供功能实现）。

![](img/57baed2319be0bb1b5f98674846f2711_634_1.png)

图 14.42 | 打印机 GUI。

### 14.6 (长度转换) 编写一个长度转换程序，将米转换为英尺、英寸和厘米。米的长度应从键盘（通过 TextBox）输入。应使用三个 TextBox 来显示英尺、英寸和厘米的长度。使用以下公式进行转换：1 米 = 3.28084 英尺 = 39.37 英寸 = 100 厘米

### 14.7 (增强型画板) 扩展图 14.43 的程序，包含更改绘制线条的大小和颜色的选项。创建一个与图 14.43 类似的 GUI。用户能够在程序的 Panel1 上绘图。要获取用于绘制的 Graphics 对象，请调用方法 `methodName.Graphics()`，并替换为你的 Panel 名称。

![](img/57baed2319be0bb1b5f98674846f2711_634_2.png)

图 14.43 | 绘图面板 GUI。

# 强化练习题

**14.8** (猜数字游戏) 编写一个按以下方式运行“猜数字”的程序：你的程序通过在 1–1000 范围内选择一个 `int random` 来确定数字。程序在标签中显示以下文本：

我有一个 1 到 1000 之间的数字——你能猜出我的数字吗？
请输入你的第一次猜测。

应使用 TextBox 输入猜测数字。每输入一次猜测，背景颜色就应该变为红色或蓝色。红色表示用户正在“接近”（warmer），蓝色表示用户正在“远离”（cooler）。标签应显示“太高”或“太低”，以帮助用户找到正确答案。当用户得到正确答案时，在消息框中显示“正确！”，将 Forms 的背景颜色改为绿色并禁用 TextBox（像其他控件一样，可以通过设置控件的 `enabled` 属性为 `false` 来禁用）。提供一个按钮允许用户重新玩。当点击按钮时，生成一个新的随机数，将背景恢复为默认颜色并启用 TextBox。

**14.9** (文具中心) 编写一个允许用户处理文具折扣的应用。该应用应计算在扣除适用折扣并添加购买商品价格（以及税费）后的价格。提供了用于输入发票号、订单号、客户名称和办公地址的 TextBox。最初，这些字段包含描述其用途的文本。使用 CheckBox 选择项目，使用 TextBox 输入项目数量。当用户更改任何数量值时，应用程序应更新小计、总计（折后后）、税额和金额。应用程序还应包含一个按钮，点击后可将所有字段恢复到原始值。如果小计超过 $500，则使用 5% 的折扣。税额为总额的 15%。所有字段都必须填写，且必须勾选一项以便用户为该项目输入数量。

# 强化练习题

**14.10** (Econfont 字体) Econfont——由 SPRANG（一家位于荷兰的公司）开发——这种字体旨在减少高达 20% 的打印墨水消耗，进一步减少墨盒的使用量以及制造和运输过程对环境的影响（使用更少的墨水、更少的燃料等）。该字体基于无衬线字体 Verdana，具有在小字号下不可见的小“孔”——例如使用的 9 号或 10 号字体。使用 Econfont 网站上的字体下载免费版 Econfont http://www.ecofont.com/en/products/green/font_vera_sans.ttf。

接下来，开发一个基于 GUI 的程序，允许你在 TextBox 中输入文本以便以 Econfont 字体显示。创建“增大字体”和“减小字体”按钮，以允许你放大或缩小 10 磅字。将 TextBox 字体设置为 9 点 Econfont。将 TextBox 的 `Multiline` 属性设置为 `true`，以便用户可以输入多行文本。随着放大，你将能够更清楚地看到字母中的孔。随着缩小，字体将变得不明显。要通过编程方式更改 TextBox 的字体，请使用如下形式的语句：

```
