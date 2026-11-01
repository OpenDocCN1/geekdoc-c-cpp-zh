
将在窗体上水平和垂直居中，这意味着 Label 将位于窗体的中间位置。

![](img/41d82527c4e41cdb7e56259564306ddc_36_0.png)

图 3.19. 将 Label 在窗体上居中

完成这些步骤后，窗体如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_36_1.png)

图 3.20. 窗体上居中的 Label

我们的 GUI 设计现在完成了。由于我们不希望 Hello World 应用程序具有交互性，因此不需要在这个项目中编写一行代码。然而，我想向您展示我们将在后续章节中进行实际编码的文件。正如我之前所说，Form1.cs 文件实际上由设计模式和代码模式组成。我们在这里处理了设计模式。为了在其中查看它，

![](img/41d82527c4e41cdb7e56259564306ddc_41_0.png)

图 3.29. 打开解决方案文件 Hello World.sln

本章就到这里。我们学习了如何创建一个新项目。在窗体上放置一个 Label 控件，以可视化方式设置 Label 的基本属性并将其居中。然后我们生成了项目并创建了可执行文件。

正如你可能已经从工具箱中注意到的，有很多控件可以用于 Windows 窗体。由于我们的目标是同时学习 GUI 设计和 C# 编程，所以需要了解如何使用其他控件类型，如 Button 或 TextBox。在接下来的两章中，我们将学习常用窗体控件的使用，以及相关的基础 C# 编程，然后进入后续章节的实际编程教学。

| 参考编号 | 名称 | 图像 | 说明 |
|---|---|---|---|
| 10 | MaskedTextBox | MaskedTextBox | 强制以指定格式输入文本的文本框 |
| 11 | MonthCalendar | MonthCalendar | 可从其中选择日期的日历控件 |
| 12 | NotifyIcon | NotifyIcon | 通知区域中的图标元素 |
| 13 | NumericUpDown | NumericUpDown | 提供一个可通过点击箭头更改的数值 |
| 14 | PictureBox | PictureBox | 用于显示图像 |
| 15 | ProgressBar | ProgressBar | 显示操作进度 |
| 16 | RadioButton | RadioButton | 允许从多个选项中选择一项 |
| 17 | RichTextBox | RichTextBox | 带有段落格式等的高级文本框 |
| 18 | TextBox | TextBox | 允许用户输入文本 |
| 19 | ToolTip | ToolTip | 当鼠标悬停时显示简短信息 |
| 20 | TreeView | TreeView | 显示分层项目 |
| 21 | WebBrowser | WebBrowser | 在窗体上显示网页 |

表 4.1. 常用控件（续）

你可以在工具箱的“公共控件”部分找到这些控件，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_45_0.png)

图 4.2. 工具箱中的公共控件

### 4.2. 容器和菜单

容器是用于对窗体中的其他元素进行分组的控件。Visual Studio 提供的容器类型如下：

| 参考编号 | 名称 | 图像 | 说明 |
|---|---|---|---|
| 1 | FlowLayoutPanel | FlowLayoutPanel | 提供流式布局 |
| 2 | GroupBox | GroupBox | 对其中的元素分组并绘制边框 |
| 3 | Panel | Panel | 仅对其元素进行分组 |

| 参考编号 | 名称 | 图像 | 说明 |
|---|---|---|---|
| 4 | SplitContainer | SplitContainer | 为容器提供两个可调整大小的垂直区域 |
| 5 | TabControl | TabControl | 提供选项卡区域以放置元素 |
| 6 | TableLayoutPanel | TableLayoutPanel | 表格形状的容器 |

表 4.3. 用于分组控件的容器（续）

容器在工具箱中列出，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_46_0.png)

图 4.2. 工具箱中的容器

另一方面，菜单和工具栏是特殊类型的控件，可在窗体上提供对命令的快捷访问。常用的例子包括窗体顶部的“文件”菜单，以及用于复制、粘贴等命令的右键菜单。Visual Studio 具有以下菜单和工具栏选项：

| 参考编号 | 名称 | 图像 | 说明 |
|---|---|---|---|
| 1 | ContextMenuStrip | ContextMenuStrip | 右键菜单 |
| 2 | MenuStrip | MenuStrip | 按功能对命令分组，如“文件”菜单 |

![](img/41d82527c4e41cdb7e56259564306ddc_53_0.png)

图 4.9. 当 Anchor 属性更新为 Top、Left、Right 时，按钮会拉伸

17. Dock：用于将控件停靠在窗体上的五个区域之一。停靠选项如下图所示。注意，与其他属性一样，单击右侧的箭头即可打开其选项框。

![](img/41d82527c4e41cdb7e56259564306ddc_53_1.png)

图 4.10. 停靠选项（默认选择 None）

18. Location：此属性定义控件相对于窗体左上角在窗体上的位置。

19. MaximumSize：此属性设置控件的最大允许大小。实践中用于窗体而不是控件。

20. MinimumSize：这设置控件的最小允许大小。

21. Size：以像素为单位设置控件的尺寸。

选择一个属性后，属性的简短说明会出现在属性窗口的底部空间中，如图 4.11 所示。

控件和其他窗体元素的属性也可以在运行时通过编程方式实时更改。

![](img/41d82527c4e41cdb7e56259564306ddc_54_0.png)

图 4.11. 所选属性的简短说明出现在属性窗口的底部

### 4.6. 控件的事件

事件处理窗体上发生的事情。单击按钮或从下拉框中选择选项都是事件的示例。事件发生时将要执行的代码写在项目的 .cs 文件中。

每种控件类型都有一个默认事件，只需双击控件即可在代码中创建该事件。例如，让我们通过拖放将 CheckBox 放到窗体上，如图 4.12 所示。Form1 处于 [Design] 模式，如椭圆内所示。当我们双击此窗体上的 checkBox1 时，编辑器中会打开 Form1 的代码视图，如图 4.13 所示。

CheckBox 的默认事件是 CheckChanged 事件，当 CheckBox 的选中状态改变时（即被选中或取消选中时）触发（执行）。当在窗体上双击 checkBox1 时，会创建名为 checkBox1_CheckChanged(...) 的默认事件处理方法，如图 4.13 中的矩形所示。

![](img/41d82527c4e41cdb7e56259564306ddc_57_0.png)

图 4.14. 按类别列出的 CheckBox 控件的所有事件

| 参考编号 | 名称 | 触发时机 | 方法格式 |
|---|---|---|---|
| 1 | BackColorChanged | 背景颜色更改时 | ControlName_BackColorChanged(...) |
| 2 | BackgroundImageChanged | 背景图像更改时 | ControlName_BackgroundImageChanged(...) |
| 3 | CursorChanged | 光标类型更改时 | ControlName_CursorChanged(...) |
| 4 | KeyPressed | 控件处于活动状态时按下键盘上的某个键 | ControlName_KeyPressed(...) |
| 5 | Load | 加载窗体时（程序开始执行时） | FormName_Load(...) |

![](img/41d82527c4e41cdb7e56259564306ddc_60_0.png)

## 第 5 章

### 常用控件

在本章中，我们将详细研究常用控件，因为它们是 GUI（窗体）设计的支柱。我们将在小项目中使用它们，并对其属性和事件进行编程。这将是我们 C# 编程之旅的温和开端。

### 5.1. Button

按钮用于触发操作。

![](img/41d82527c4e41cdb7e56259564306ddc_60_1.png)

图 5.1. 一个按钮

按钮具有以下属性：

- **Image**：按钮的前景图像。
- **TextAlign**：按钮上文本的对齐方式。
- **FlatStyle**：设置按钮的外观。

> 请注意，这里讨论的属性是上一章讨论的公共属性之外的附加属性。

一个简单的 Button 示例：让我们逐步创建一个包含 Button 的小项目：

- 1. 在 Visual Studio 中创建一个新的 C# 项目。
- 2. 在窗体上放置一个 Button。
- 3. 将 Button 的 Text 属性设置为 Change。
- 4. 将 Button 的 Name 属性设置为 changeButton。

