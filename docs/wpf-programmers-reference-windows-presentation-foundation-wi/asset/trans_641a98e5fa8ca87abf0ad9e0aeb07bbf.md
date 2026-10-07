

# 总结

Visual Studio 提供了构建 WPF 的基本工具。窗口设计器（Window Designer）让你构建 XAML 界面，而代码编辑器（Code Editors）允许你创建位于控件后的 C# 或 Visual Basic 代码。

虽然你可以使用 Visual Studio 完成工作，但它会让某些任务变得相当繁琐。例如，它没有为视觉画刷（visual brushes）等复杂对象提供编辑器，并且对创建属性动画没有提供任何帮助。要在 Visual Studio 中构建这些内容，你需要手动编写 XAML 代码。

下一章介绍的 Expression Blend 工具提供了一些 Visual Studio 缺少的有用工具。例如，它允许你交互式地创建复杂的视觉画刷和属性动画，而不是通过编写 XAML 代码。你仍然希望使用 Visual Studio 来编写界面背后的代码，但 Expression Blend 可以让一些琐事变得简单得多。

# 3 Expression Blend

Visual Studio 为编写 C# 或 Visual Basic 提供了良好的环境，但在创建 XAML 界面方面表现平平。Expression Blend 提供了相反的体验：它是创建 XAML 界面的良好环境，但是创建 C# 和 Visual Basic 后置代码的工具却很很乏力。

幸运的是，Expression Blend 与 Visual Studio 良好集成，因此你可以根据需要在这两个工具之间切换。

本章将解释如何使用 Expression Blend 编写演示基础框架 (WPF) 用户界面 (UI)。它解释了如何启动新项目、向窗口添加控件、指定基本控件属性以及创建简单动画。

# 安装 EXPRESSION BLEND

为了充分利用本章内容，你需要安装 Expression Blend。遗憾的是，Expression Blend 非常昂贵，而且不像 Visual Studio，它没有免费版。幸运的是你可以下载 60 天试用版。你可以在 expression.microsoft.com/cc13653.aspx 更多关于 Expression Blend 或下载试用版。

Expression Blend 是一个巨大复杂的应用程序，具有许多构建 XAML 用户界面的强大功能，而本书仅涵盖了构建 WPF 应用的最少需要。关于 Expression Blend 细节的更多详细信息，请参考专注于 Expression Blend 的书籍，如《Foundation Blend 3 with Silverlight》(Victor Gaudioso, friends of ED, 2009) 或《Microsoft Expression Blend Unleashed》(Brennan Williams, Sams, 2008)。

> 如果你有丰富的 Expression Blend 备经验，这里的大部分内容对你来说将是熟悉且易于理解的，因此你可能想跳过章。

# 新项目

在 Expression Blend 中启动 WPF 项目非常简单。打开“文件”菜单并选择“新建项目”，即可显示图 3-1 所示的新项目对话框。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_75_0.png)

图 3-1

选择你想要构建的项目类型。为项目输入一个描述性名称以及你想要构建它的目录。选择你想用于后置代码的编程语言（C# 或 Visual Basic）并点击确定创建项目。

> 如果你只想制作松散的 XAML 页面，请选择 WPF 应用项目并任选编程语言。稍后你可以从项目目录中复制构建的 XAML 文件并丢弃其他内容。

图 3-2 显示了 Expression Blend 中一个典型的 WPF 应用。

> 并非如所示
Expression Blend 的外观可能与本章图中所示的不完全相同。虽然它不像 Visual Studio 那样可以配置，但仍然有许多方法可以调整大小、折叠、隐藏或通过改变 Expression Blend 窗口的外观。如果你找不到某个窗口，请寻找其标题旁边的箭头，该箭头指示窗口已被折叠。如果你仍然找不到，请查看“窗口”菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_76_0.png)

以下列表列出了图 3-2 中高亮的编号部分。

- 1. 资源 (Assets) 窗口
- 2. 项目 (Projects) 窗口选项卡
- 3. 窗口设计器，设计视图 (Design view)
- 4. 窗口设计器，XAML 视图
- 5. 属性 (Properties) 窗口
- 6.  (Resources) 窗口选项卡
- 7. 对象和时间轴 (Objects and Timeline)
- 8. 触发器 (Triggers) 窗口选项卡
- 9. 控件工具箱 (Control Toolbox)

后续章节将详细详细描述图 3-2 的每个部分。

> 术语
窗口设计器的设计视图也称为画布 (artboard)。

# 资源窗口 (ASSETS WINDOW)

资源窗口列出了你在构建项目时可以使用的工具。选择左侧的类别（项目、控件、样式等）以查看右侧符合该类别的项目。例如，在图 3-2 中选择了“控件”类别，因此右侧列表显示了常用控件。你可以展开“控件”类别，从所有、数据可视化和面板子类别中进行选择。

# 项目窗口选项卡 (PROJECTS WINDOW TAB)

项目窗口列出了项目中的文件。这些包括应用程序文件、资源文件（如图像和视频）、XAML 定义文件以及文件的后置代码。

项目窗口提供了多种编辑不同文件的方法。如果你双击 XAML 文件，Expression Blend 会在窗口设计器（下文描述）中打开它。

如果你双击后置代码文件，Expression Blend 会用带有 IntelliSense 的内部代码编辑器打开它。

> 缺失的编辑器

遗憾的是，Expression Blend 缺少 Visual Studio 拥的一些额外编辑器，用于编辑位图、图标、光标等。
如果你在 Expression Blend 中双击图像文件且打开了窗口设计器，Expression Blend 将图像添加到所选控件中。如果你没有打开窗口设计器，它将使用默认应用程序打开该文件，通常是画画。
或者，你可以右键点击文件并选择“外部编辑”，在外部编辑器中打开。

最棒的是，你可以右键点击 XAML 或后置代码文件并选择“在 Visual Studio 中编辑”，在 Visual Studio 中打开整个 WPF 项目。这让你利用 Visual Studio 的完整功能轻松编辑代码。

# 窗口设计器 (WINDOW DESIGNER)

窗口设计器允许你编辑窗口并定义动画。本章后续的 Storyboards 部分将解释如何使用窗口设计器构建动画。本节解释了如何使用它构建窗口的基本界面。

当你专注于窗口设计器时，Expression Blend 允许你隐藏包含项目窗口、触发器和其他窗口的侧面板。要隐藏或恢复面板，打开“窗口”菜单并选择“自动隐藏所有面板”。

图 3-3 显示了隐藏了侧面板的窗口设计器。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_78_0.png)

图 3-3

此图的上部显示了画布 (artboard)。在这里你可以添加、选择、调整大小、移动和删除控件。窗口设计器用蓝色线条高亮当前选中的控件，并在左上角显示控件名称（图 3-3 中的 "rectContent"）。

设计界面的下方是 XAML 编辑器。在这里你可以查看和编辑 XAML 代码。在图 3-3 中，设计面上选中的矩形在 XAML 编辑器中被高亮。

设计界面的右上角有三个按钮（图 3-3 中圈），允许你只查看设计界面、XAML 编辑器或类似于图 3-3 所示的分屏视图。

设计界面和 XAML 编辑器之间有一个缩放下拉菜单，图 3-3 中显示为“100%在使用设计器时通过下拉菜单选择不同的比例。

缩放下拉菜单右侧的按钮允许你关闭渲染效果（为了性能）、显示或隐藏捕捉网格（如图 3-3 所示）、开启或关闭网格对齐、开启或关闭捕捉线对齐以及显示和隐藏注释。

屏幕左边缘显示的是控件工具箱。关于此区域的更多信息，请参见本章后续的“控件工具箱”章节。

