
在讨论了 WPF 4.0 的改进之后，现在让我们解释 WPF 4.0 架构。

## 解释 WPF 4.0 架构

WPF 4.0 既有托管组件，也有非托管组件。托管组件是指在 .NET 环境中使用公共语言运行时（CLR）服务（例如垃圾回收和类型安全）的组件，而非托管组件则是不使用 CLR 服务的组件。WPF 4.0 的托管组件和非托管组件如图 VB-5.1 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_184_0.png)

图 VB-5.1

如图 VB-5.1 所示，WPF 4.0 的架构包含各种组件，例如 PresentationFramework、PresentationCore、CLR、User32 和 DirectX。WPF 4.0 的核心组件是 PresentationFramework、PresentationCore 和 milcore。现在让我们逐一讨论 WPF 4.0 架构的核心组件。

### PresentationFramework 组件

**PresentationFramework** 组件指的是 .NET Framework 4.0 中的 **PresentationFramework.dll** 程序集。它提供各种类，例如 Calendar 和 DataGrid，用于操作 WPF 4.0 应用程序的外观和呈现。它还提供最终用户呈现功能，例如布局、动画和数据绑定。**PresentationFramework** 组件支持更高层次的程序抽象实现，例如样式。

### PresentationCore 组件

**PresentationCore** 组件指的是 **PresentationCore.dll** 程序集。它实现 WPF 的核心服务，使你能够管理属性和事件。它支持基类型，例如 UIElement 和 Visual，这些类型是所有控件和形状的父类型。请注意，**PresentationCore** 组件不像 PresentationFramework 组件那样为 WPF 4.0 应用程序的 UI 提供类。

### Milcore 组件

**Milcore** 或 **媒体集成层 (MIL)** 是 WPF 4.0 的非托管组件。它与 **DirectX** 交互，DirectX 是处理所有与设计相关的元素以在 WPF 4.0 应用程序中显示 2D 和 3D 图形内容的组件。它是 MIL 的基础，也是 WPF 的核心呈现系统。

现在让我们了解 WPF 4.0 支持的不同类型的应用程序。

## 描述 WPF 应用程序的类型

WPF 是一个 UI 框架，可帮助你创建交互式应用程序。WPF 支持各种应用程序开发功能，例如控件、图形、布局和数据绑定。它是下一代 UI 框架，使你能够开发具有丰富用户体验的应用程序。你可以使用 WPF 创建 Windows 和 Web 应用程序。

WPF 应用程序主要分为以下两种类型：

- 独立 WPF 应用程序
- XAML 浏览器应用程序 (XBAP)

让我们逐一了解这些类型的应用程序。

### WPF 独立应用程序

WPF 独立应用程序与 Windows Forms 应用程序类似，因为你可以将 WPF 应用程序安装到计算机上，并从 **开始** 菜单中查看它们。Visual Studio 2010 提供了一个项目模板，可用于创建 WPF 独立应用程序。使用该模板开始创建应用程序时，一些基本文件（如 Application.xaml 和 MainWindow.xaml）会自动添加到项目中。

执行以下步骤，在 Visual Studio 2010 中创建示例 WPF 独立应用程序：

1. 启动 Visual Studio 2010。
2. 从菜单栏选择 **文件→新建→项目**。**新建项目** 对话框打开（图 VB-5.2）。
3. 在 **新建项目** 对话框左窗格的 **已安装的模板** 部分中，选择 **Visual Basic→Windows**（图 VB-5.2）。Visual Basic 中可用于开发基于 Windows 的应用程序的项目模板显示在 **新建项目** 对话框的中间窗格中。
4. 在中间窗格中选择 **WPF 应用程序** 模板，以创建 WPF 独立应用程序（图 VB-5.2）。
5. 在 **名称** 文本框中输入应用程序的名称（图 VB-5.2）。在本例中，我们输入了 **MyWPFApplication**（也随 CD 提供）作为应用程序的名称。
6. 在 **位置** 组合框中输入应用程序的合适位置（图 VB-5.2）。在本例中，我们输入了 D:\Comdex\Applications\Visual Basic 2010\Chapter 5\。
7. 单击 **确定** 按钮关闭 **新建项目** 对话框，如图 VB-5.2 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_185_0.png)

图 VB-5.2

**MyWPFApplication** 应用程序已创建，如图 VB-5.3 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_186_0.png)

图 VB-5.3

你可以从图 VB-5.3 中注意到，与 Windows Forms 应用程序类似，新的 WPF 独立应用程序的设计界面有一个包含各种工具的 **工具箱**，以及一个称为*窗口*的空白矩形区域。你将在本章后面进一步了解 WPF 独立应用程序的设计界面。

如前所述，当你使用 **WPF 应用程序** 模板创建 WPF 独立应用程序时，应用程序将创建使用 WPF 应用程序所需的 Application.xaml 和 MainWindow.xaml 文件。这些文件会自动添加到应用程序中。你可以在 **解决方案资源管理器** 窗口中查看这些文件；可通过从菜单栏选择 **视图→解决方案资源管理器** 或按键盘上的 **CTRL+ALT+L** 键打开该窗口（图 VB-5.4）。

你可以从图 VB-5.4 中注意到，默认情况下，**Application.xaml** 和 **MainWindow.xaml** 两个文件显示在 **解决方案资源管理器** 窗口中。**Application.xaml** 节点包含另一个文件 **Application.xaml.vb**，你可以通过展开该节点来显示它。**Application.xaml** 和 **Application.xaml.vb** 文件共同表示整个 WPF 应用程序。**Application.xaml** 文件是一个 XAML 文件，即用 XAML 编写的文件，而 **Application.xaml.vb** 文件是其代码隐藏文件（用 Visual Basic 编写）。你可以使用这些文件指定应用程序级设置和逻辑。**MainWindow.xaml** 节点还包含另一个文件 **MainWindow.xaml.vb**，你可以通过展开该节点来显示它。**MainWindow.xaml** 和 **MainWindow.xaml.vb** 文件对应于 WPF 独立应用程序的默认 UI，该 UI 由一个空白窗口组成。**MainWindow.xaml** 文件是一个 XAML 文件；而 **MainWindow.xaml.vb** 文件是其代码隐藏文件（用 Visual Basic 编写）。这两个文件包含 WPF 独立应用程序中默认窗口的设置和逻辑。

> WPF 独立应用程序中的窗口是 Window 类的对象。

默认情况下，**解决方案资源管理器** 窗口不会显示独立应用程序中的所有文件。你需要单击 **解决方案资源管理器** 窗口工具栏中的 **显示所有文件** 按钮，以查看独立应用程序中包含的所有文件（图 VB-5.4）。

当你单击 **解决方案资源管理器** 窗口中的 **显示所有文件** 按钮时，独立应用程序中包含的所有文件都会变为可见（图 VB-5.5）。例如，默认情况下不可见的文件会出现在 **解决方案资源管理器** 窗口的 **引用**、**bin** 和 **obj** 节点下。

**解决方案资源管理器** 窗口中的 **引用** 节点显示对设计和开发独立应用程序所需的基本程序集的引用。你需要单击 **解决方案资源管理器** 窗口中 **引用** 节点旁边的加号 (+)，以查看对这些程序集的引用（图 VB-5.5）。

该应用程序引用了 **PresentationCore.dll**、**PresentationFramework.dll** 和 **WindowsBase.dll** 程序集（图 VB-5.6）。

![](img/9862a98a1a2d3bb14334137965a1ec60_187_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_187_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_187_2.png)

现在让我们了解 WPF 4.0 中的 XBAP。

## XBAP 应用程序

XBAP（读作 x-baps）是托管在 Web 服务器上并在 Web 浏览器（如 Windows Internet Explorer 或 Mozilla Firefox）中运行的 WPF 应用程序。XBAP 类似于网站，因为它由类似于网站中网页的页面组成，允许用户在 Web 浏览器中导航。但是，如果用户处于脱机状态（与 Internet 或承载 XBAP 的 Web 服务器断开连接），则无法访问该 XBAP。

> **必须在客户端计算机上安装 .NET Framework 才能访问 XBAP 应用程序。**

与独立应用程序一样，Visual Studio 2010 提供了一个项目模板，可用于创建 XBAP。

执行以下步骤，在 Visual Studio 2010 中创建示例 XBAP：

1. 启动 Visual Studio 2010。
2. 从菜单栏选择 文件→新建→项目。新建项目 对话框打开（图 VB-5.7）。
3. 从新建项目对话框左窗格的已安装的模板部分选择 Visual Basic→Windows（图 VB-5.7）。
4. 在中间窗格中选择 **WPF 浏览器应用程序** 模板，以创建 WPF XBAP 应用程序（图 VB-5.7）。
5. 在 **名称** 文本框中输入应用程序的名称（图 VB-5.7）。在本例中，我们输入了 **MyWPFBrowserApplication**（也随 CD 提供）作为应用程序的名称。
6. 在 **位置** 组合框中输入应用程序的合适位置（图 VB-5.7）。在本例中，我们输入了 `D:\Comdex\Applications\Visual Basic 2010\Chapter 5\`。
7. 单击 **确定** 按钮关闭 **新建项目** 对话框，如图 VB-5.7 所示。
