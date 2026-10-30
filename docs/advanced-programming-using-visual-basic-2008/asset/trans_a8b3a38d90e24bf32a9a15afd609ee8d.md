
这最后一章将向你介绍编程的一些附加功能。随着市场上移动设备越来越多，拥有一个可扩展的开发环境变得愈发重要。Visual Studio 正好满足这一需求：你可以使用自己已经熟悉的工具为移动设备编程。

本章的另一个主题——本地化，也涉及通信设备在全球范围内的日益广泛使用。当你在创建可供多个国家用户查看的应用程序时，应考虑每个国家用户的需求。

本章还涉及在后台（异步）运行进程，以提高耗时任务的性能。

WPF 为开发人员提供了创建一流界面的工具。其编程方式与之前的 Visual Basic 应用程序保持一致。本章演示了 WPF 在 Windows 应用程序中的使用。

LINQ 是本章的最后一个主题，它提供了一种用于查询多种类型数据的一致语言。

## 设备应用程序

为 PDA、手机和寻呼机创建输出需要不同的协议，但你可以使用 Visual Basic 来开发针对这些移动设备的应用程序。Visual Studio IDE 具有创建可部署到智能设备的解决方案的功能。智能设备是指那些运行精简版和移动版 Windows 的移动设备。

## 使用模拟器

当你使用 VS 开发智能设备应用程序时，可以在常规窗口中查看输出，也可以在模拟器中查看。模拟器会在计算机屏幕上显示设备的图像，让你更直观地了解最终输出效果。可以想象，手机设备上的屏幕与 Pocket PC 或 SmartPhone 等设备上的屏幕看起来大不相同。Visual Studio Professional Edition 安装时带有针对 Windows Mobile 5.0 Pocket PC SDK、Pocket PC 2003、Windows CE 和 Windows Mobile 5.0 Smartphone SDK 的目标平台。自动安装的模拟器会根据你选择的 Windows 版本而有所不同。你可以为其他 SDK（如 Windows Mobile 6.0）下载额外的模拟器。图 13.1 显示了在设备模拟器中显示的应用程序。

## 智能设备应用程序

当你为智能设备开始一个新项目时，需要在“项目类型”中选择“智能设备”，并选择“智能设备项目”模板（图 13.2），而不是“Windows 应用程序”模板。工具栏和工具箱看起来与 Windows 应用程序的类似，但设备控件与 Windows 控件集不同。你会发现设备控件可用的属性比对应的 Windows 控件少得多。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_532_0.png)

*在模拟器中显示的智能设备应用程序。*

### 图 13.1

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_532_1.png)

*通过选择“设备应用程序”模板来开始新的智能设备应用程序。*

### 图 13.2

## 第一个智能设备应用程序——分步详解

是时候再来一个 Hello World 应用程序了。

### 创建项目

- 步骤 1：新建一个项目，选择“智能设备”项目类型和“智能设备项目”模板。将项目命名为 `Ch13Hello-WorldSmartDevice`。
- 步骤 2：单击“确定”后，会出现另一个对话框，其中包含“目标平台”的下拉框。选择 Windows Mobile 5.0 Smartphone SDK 和“设备应用程序”模板（图 13.3）。

选择移动设备的类型。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_533_0.png)

为其他设备获取模拟器

- 步骤 3：请注意，窗体将显示在模拟器中（图 13.4）。你可以通过“工具” / “选项” / “设备工具” / “在 Windows 窗体设计器中显示外观”选择显示或隐藏模拟器图像。
- 步骤 4：将窗体命名为 `HelloWorldForm`，并将 Text 属性设置为 Hello World。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_535_0.png)

### 编写代码

**步骤 1：** 编写菜单项的代码，以在文本框中显示名称。

```
Private Sub DisplayMenuItem_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles DisplayMenuItem.Click
    ' Display the Hello World message.

    HelloLabel.Text = "Hello " & NameTextBox.Text
End Sub
```

**步骤 2：** 为 *退出* 菜单项编写代码。

```
Private Sub ExitMenuItem_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles ExitMenuItem.Click
    ' Exit the application.

    Me.Close()
End Sub
```

## 运行应用程序

步骤 1：运行程序并选择任意设备模拟器（图 13.6）。单击“部署”。注意，如果你有真机需要连接，可以选择不是模拟器的选项。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_536_0.png)

### 图 13.6

选择运行程序时要使用的模拟器。

步骤 2：稍等片刻。你的项目需要一些时间加载，但请记住，这是一个完整的设备模拟器。

起初，你会看到模拟器显示的是虚拟数据。当应用程序实际加载后，你将看到 Hello World 界面。闲暇时，你可能会想试用模拟器的许多功能。现在，你需要输入一个名称，然后点击“显示”菜单项（图 13.7）。要显示菜单，请单击模拟器屏幕下方左侧的银色按钮。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_536_1.png)

### 图 13.7

在设备模拟器中运行的 Hello World 应用程序。

使用 Windows Mobile 5.0 Pocket PC2 模拟器运行 Ch13SmartDeviceDatabase 项目。有关输出，请参阅图 13.1。

## 更改列样式

数据网格列的格式与你熟悉的 Windows DataGridView 不同。数据网格包含一个 TableStyles 属性，它是一个集合。在 DataGridTableStyle 集合编辑器中，选择 GridColumnStyles 集合。在 DataGridColumnStyle 集合编辑器（图 13.9）中，你可以更改各列的宽度或标题文本。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_538_0.png)

## 创建数据窗体

数据网格的智能标记提供了“生成数据窗体”选项。选择该项后，你将生成一个窗体，同时窗体上会出现一个“新建”菜单项，用于向数据库添加新项。如果你不是在创建数据库更新程序，可以删除“新建”菜单项及其关联代码。

当你向数据网格应用程序添加数据窗体后，可以双击数据网格中的某一行，该条记录就会显示在数据窗体上（图 13.10）。

## 更新数据库

使用模拟器测试数据库更新程序比较困难，因为除非进行一些高级配置，否则模拟器不会在两次运行之间保留数据库。如果你有真实的智能设备连接到计算机，则可以将数据库文件传输到设备上，并实际测试更新过程。

> 提示：选择保存模拟器状态的选项；项目在后续执行时会加载得更快。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_538_1.png)

## 在详细信息视图中显示记录

与 Windows 项目一样，“数据源”窗口允许你拖拽表以创建数据网格或详细信息视图。你会立即注意到的一个区别是缺少绑定导航器。

Ch13ProductDetails 程序显示 Product ID、Product Name、Unit Price、Units In Stock 和 Discontinued 字段。如图 13.11 所示，Product Name 位于一个组合框中，用于选择要导航到的记录。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_539_0.png)

图 13.10
在网格中双击一行，即可在窗体中显示单行记录。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_539_1.png)

图 13.11
使用组合框进行导航，记录以详细信息视图显示。

设置组合框的数据绑定属性与 Windows 控件类似。在智能标记中，设置 DataSource 和 DisplayMember 属性。然后滚动到“属性”窗口顶部，展开 (DataBindings) 项，选择 (Advanced)，并将 Data Source Update Mode 设置为 Never。

## 自测题 13.1

什么是智能设备应用程序？

## Windows Presentation Foundation (WPF)

界面设计正在发生巨大变化，相关工具也在变化。使用 Visual Studio 2008 中包含的全新功能——Windows Presentation Foundation (WPF)，你可以创建在 Windows Vista 应用程序中看到的各种特效。你可以为 Windows XP 和 Windows Vista 编写 WPF 应用程序，但除非在运行 XP SP2 的机器上安装插件，否则这些特效不会在 XP 中显示。

微软已向开发人员宣布，他们将逐步淘汰 Windows Forms，转而采用 WPF。因此，你可以选择使用 WPF 而不是 Windows Forms 来编写所有 Windows 应用程序；编程方式基本相同。目前，Windows XP 和 Windows Forms 比 Vista 和 WPF 应用程序更为普及，但你可以预计在未来几年内这种情况会发生变化。

WPF 包含用于 Windows 和 Web 应用程序的开发平台。你可以编写独立的 WPF Windows 应用程序、在浏览器中运行的应用程序，以及显示 XPS 文档（例如从 Office 2007 生成的文档）的程序。你可以在 http://windowsclient.net/community/showcase.aspx 查看各种 WPF 设计示例。

Silverlight 是一种相关技术，它拥有 WPF 的部分功能，但能够运行在多种浏览器平台上。通过 Visual Studio 创建的浏览器应用程序要求客户端计算机上安装 .NET 组件，并且只能在 Internet Explorer 中运行。在管理员可以控制计算机配置的本地 intranet 之外，这一限制使得 Silverlight 成为一种更通用的开发选择。

## 设计人员与程序员的角色

包含如此多特效的新用户界面通常同时需要设计人员和程序员的参与。新工具使得设计工作与编程工作可以轻松分离。

WPF 开发既可以在 Visual Studio 中进行，也可以在 Expression Interactive Designer 中进行。程序员通常使用 Visual Studio，而设计人员更偏好 Expression Interactive Designer。程序员可以在 Visual Studio 中创建窗口，同一个 window.xaml 文件可以在 Expression 中打开和修改。例如，程序员可以在窗口上放置一个按钮，然后设计人员可以将该按钮变为华丽的设计元素；按钮背后的编程仍由程序员完成，他们使用 VB 或 C# 编写，就像在 Windows Forms 应用程序中一样。
