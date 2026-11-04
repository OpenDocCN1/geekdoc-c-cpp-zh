

![](img/3f5ef6be1748bb746e5f71a483bba4d0_441_0.png)

图 14.10 | 单击事件详细信息。

## 14.4 控件属性与布局

本节概述许多控件共有的属性。控件派生自类 Control（命名空间 System.Windows.Forms）。图 14.11 列出了类 Control 的一些属性和方法。这里显示的属性可以为许多控件设置。例如，Text 属性指定控件上显示的文本。此文本的位置因控件而异。在 Form 中，文本显示在标题栏中，但 Button 的文本显示在其表面上。

| 类 Control 的属性和方法 | 描述 |
|---|---|
| 常见属性 | |
| BackColor | 控件的背景色。 |
| BackgroundImage | 控件的背景图像。 |
| Enabled | 指定控件是否启用（即用户是否可以与之交互）。通常，禁用控件的部分会显示为“灰色”，以向用户直观指示该控件已禁用。 |
| Focused | 指示控件是否具有焦点（仅在运行时可用）。 |

图 14.11 | 类 Control 的属性和方法。（第 1 部分，共 2 部分。）

例如，状态栏之类的控件通常应保留在 Form 的底部并横跨该 Form 的整个底部，无论 Form 的宽度如何。当父控件调整大小时，停靠控件也会调整大小。

### 锚定演示

当窗口（或其他类型的容器，如 Panel）调整大小时，锚定控件会被移动（并可能调整大小），以便它们所锚定的边到控件的距离保持不变。默认情况下，大多数控件锚定到 Form 的左上角。要查看锚定控件的效果，请创建一个包含两个 Button 的简单 Windows Forms 应用。通过设置 Anchor 属性（如图 14.12 所示），将一个控件锚定到右侧和底部。让另一个控件保持默认锚定（顶部、左侧）。运行该应用并放大 Form。锚定到右下角的 Button 始终与右下角保持相同距离（图 14.13）。另一个控件则与其左上角保持原始距离。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_443_0.png)

图 14.12 | 操作控件的 Anchor 属性。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_443_1.png)

图 14.13 | 锚定演示。

在图 14.14 中，一个 Button 停靠在 Form 的顶部（横跨顶部部分）。当 Form 调整大小时，Button 会调整为 Form 的新宽度。Form 具有 Padding 属性，用于指定停靠控件与 Form 边缘之间的距离。此属性指定四个值（每边一个），每个值默认设置为 0。图 14.15 总结了一些常见的控件布局属性。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_444_0.png)

图 14.14 | 将 Button 停靠到 Form 的顶部。

| 控件布局属性 | 描述 |
|---|---|
| Anchor | 使控件即使在容器调整大小时也与其容器的一侧或多侧保持固定距离。 |
| Dock | 允许控件横跨其容器的一侧，或填充容器中的剩余空间。 |
| Padding | 设置容器边缘与停靠控件之间的空间。默认值为 0，使控件看起来与容器两侧齐平。 |
| Location | 指定控件左上角相对于其容器左上角的位置（作为一组坐标）。 |
| Size | 以 Size 对象（具有 Width 和 Height 属性）的形式指定控件的大小（以像素为单位）。 |
| MinimumSize、MaximumSize | 分别指示 Control 的最小和最大大小。 |

图 14.15 | 控件布局属性。

Control 的 Anchor 和 Dock 属性是相对于 Control 所在的容器（称为父容器）设置的，该容器可以是 Form 或其他容器（如 Panel）。Form（或其他 Control）的最小和最大大小可以分别通过 MinimumSize 和 MaximumSize 属性设置。两者均为 Size 类型，具有 Width 和 Height 属性。MinimumSize 和 MaximumSize 属性允许你针对给定的大小范围设计 GUI 布局。用户不能将 Form 设置为小于 MinimumSize 属性指定的大小，也不能将 Form 设置为大于 MaximumSize 属性指定的大小。要将 Form 设置为固定大小（即用户无法调整 Form 的大小），请将其最小大小和最大大小设置为相同的值。

### 14.4.2 使用 Visual Studio 编辑 GUI 布局

Visual Studio 可帮助你进行 GUI 布局。当你在 Form 上拖动控件时，会出现蓝色对齐线，帮助你相对于其他控件（图 14.16）和 Form 边缘定位控件。此功能使正在拖动的控件看起来与其他控件一起“吸附到位”。Visual Studio 还提供 Format 菜单，其中包含用于修改 GUI 布局的选项。只有在设计视图中选择一个或多个控件时，Format 菜单才会出现在 IDE 中。选择多个控件时，可以使用 Format 菜单的 Align 子菜单对齐它们。Format 菜单还使你能够修改控件之间的间距或将控件居中于 Form 上。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_445_0.png)

**图 14.16** | 用于对齐控件的对齐线。

## 14.5 标签、文本框和按钮

标签提供文本信息（以及可选图像），由类 Label（Control 的派生类）定义。Label 显示用户无法直接修改的文本。可以通过修改 Label 的 Text 属性以编程方式更改 Label 的文本。图 14.17 列出了常见的 Label 属性。

| 常见 Label 属性 | 描述 |
|---|---|
| Font | Label 上文本的字体。 |
| Text | Label 上的文本。 |
| TextAlign | Label 文本在控件上的对齐方式——水平方向（左、中或右）和垂直方向（上、中或下）。默认值为左上。 |

**图 14.17** | 常见 Label 属性。

文本框（类 TextBox）是一个区域，程序可以在其中显示文本，用户也可以通过键盘在其中输入文本。密码 TextBox 是一种隐藏用户输入信息的 TextBox。当用户键入字符时，密码 TextBox 通过显示密码字符来掩蔽用户输入。如果将属性 UseSystemPasswordChar 设置为 true，则 TextBox 变为密码 TextBox。用户在登录计算机或网站时经常会遇到这两种 TextBox——用户名 TextBox 允许用户输入其用户名；密码 TextBox 允许用户输入其密码。图 14.18 列出了 TextBox 的常见属性和一个常见事件。

按钮是一种控件，用户单击它可触发特定操作或选择程序中的选项。正如你将会看到的，程序可以使用多种类型的按钮，例如复选框和单选按钮。所有按钮类都派生自类 ButtonBase（命名空间 System.Windows.Forms），该类定义常见的按钮功能。本节讨论类 Button，它通常使用户能够向应用发出命令。图 14.19 列出了类 Button 的常见属性和一个常见事件。

| TextBox 属性和事件 | 描述 |
|---|---|
| *常见属性* | |
| AcceptsReturn | 如果多行 TextBox 中为 true，则在 TextBox 中按*Enter*会创建新行。如果为 false（默认值），则按*Enter*与按 Form 上的默认 Button 相同。默认 Button 是指分配给 Form 的 AcceptButton 属性的 Button。 |
| Multiline | 如果为 true，则 TextBox 可以跨多行。默认值为 false。 |
| ReadOnly | 如果为 true，则 TextBox 具有灰色背景，并且其文本无法编辑。默认值为 false。 |
| ScrollBars | 对于多行文本框，此属性指示显示哪些滚动条（None——默认值、Horizontal、Vertical 或 Both）。 |
| Text | TextBox 的文本内容。 |
| UseSystemPasswordChar | 当为 true 时，TextBox 变为密码 TextBox，系统指定的字符会掩蔽用户键入的每个字符。 |
| *常见事件* | |
| TextChanged | 当 TextBox 中的文本更改时（即当用户添加或删除字符时）生成。在**设计**模式下双击 TextBox 控件时，会为此事件生成一个空事件处理程序。 |

图 14.18 | TextBox 属性和事件。

| Button 属性和事件 | 描述 |
|---|---|
| *常见属性* | |
| Text | 指定显示在 Button 表面上的文本。 |
| FlatStyle | 修改 Button 的外观——Flat（Button 显示为无三维外观）、Popup（Button 在用户将鼠标指针移到 Button 上之前显示为平面）、Standard（三维）和 System，其中 Button 的外观由操作系统控制。默认值为 Standard。 |
| *常见事件* | |
| Click | 当用户单击 Button 时生成。在设计视图中双击 Button 时，会为此事件创建一个空事件处理程序。 |

图 14.19 | Button 属性和事件。

图 14.20 使用了一个 TextBox、一个 Button 和一个 Label。用户在密码框中输入文本并单击 Button，导致输入的文本显示在 Label 中。通常，我们不会显示此文本——密码 TextBox 的目的是隐藏用户正在输入的文本。当用户单击 **显示给我看** 按钮时，此应用会检索用户在密码 TextBox 中键入的文本，并将其显示在 Label 中。

