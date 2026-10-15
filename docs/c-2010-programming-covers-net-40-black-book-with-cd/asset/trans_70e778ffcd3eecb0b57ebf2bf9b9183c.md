

## 图 9.9：创建独立的 WPF 4.0 应用程序

在图 9.9 中，你可以看到独立 WPF 应用程序的设计器界面与 Windows Forms 应用程序的设计器界面相似。例如，工具箱中有某些工具可用，中央有一个类似窗体的结构称为窗口。

本章后面会介绍 WPF 应用程序的设计器界面。现在让我们探索创建独立应用程序所需的初始文件。

## 独立 WPF 应用程序的文件

你可以通过打开解决方案资源管理器，并展开 References、App.xaml 和 MainWindow.xaml 节点，如图 9.10 所示，来探索构成独立 WPF 应用程序的不同文件：

## 图 9.10：显示独立 WPF 4.0 应用程序的文件结构

在 References 节点下，你可以查看基本的 .NET 命名空间和程序集，例如 PresentationCore、PresentationFramework 和 WindowsBase。当你展开 App.xaml 节点时，可以查看相应的代码隐藏文件 App.xaml.cs。App.xaml 和 App.xaml.cs 文件共同代表整个 WPF 应用程序。App.xaml 文件是 XAML 文件，而 App.xaml.cs 文件是应用程序的代码隐藏文件（in

![](img/e073a4882197be4ab61103cbe0bcb394_351_0.png)

![](img/e073a4882197be4ab61103cbe0bcb394_351_1.png)

C#）用于应用程序。在 App.xaml 文件中，你可以指定所需的 XML 命名空间、应用程序的启动文件以及资源。默认情况下，App.xaml 文件显示如下所示，如清单 9.2 所示：

## 清单 9.2：显示独立 WPF 应用程序的 App.xaml 文件的内容

```
<Application x:Class="WpfApplication1.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
    </Application.Resources>
</Application>
```

在清单 9.2 中，App.xaml 文件在尖括号（< >）内写有名称，类似于其他标记语言，例如 HTML 和 XML。尖括号内的名称是 XAML 中的标签或标记元素。App.xaml 文件中的第一个标记元素是 <Application> 元素，它对应于 Application 类。此外，Application 类是主要类，它为 WPF 应用程序提供常用的服务和功能，以帮助你正确管理 WPF 应用程序。本章后面会介绍 Application 类。

现在让我们查看在解决方案资源管理器中显示的 MainWindow.xaml 和 MainWindow.xaml.cs 文件。这两个文件共同对应于 WPF 4.0 应用程序的默认窗口。清单 9.3 显示了 MainWindow.xaml 文件的默认内容：

## 清单 9.3：WpfApplication1 应用程序中 MainWindow.xaml 文件的默认内容

```
<Window x:Class="WpfApplication1.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="350" Width="525">
    <Grid>
    </Grid>
</Window>
```

在清单 9.3 中，XAML 的 <Window> 元素代表独立 WPF 4.0 应用程序中的一个窗口。<Window> 元素是 MainWindow.xaml 文件中的最顶层元素。它与 MainWindow.xaml.cs 文件中的 MainWindow 部分类相关联。与窗口相关的应用程序逻辑在 MainWindow 部分类中指定。

## Window 类

在独立 WPF 4.0 应用程序中，应用程序的整个内容包含在一个或多个窗口中。窗口是 UI 上的一个矩形区域（类似于 Windows Forms 应用程序中的窗体），允许你显示 WPF 应用程序的内容。窗口具有边框、标题以及按钮，例如最大化、最小化和关闭。WPF 窗口还具有一个菜单，提供移动和调整窗口大小的选项。请注意，你只能在运行时看到最大化、最小化和关闭按钮以及菜单，而在设计时看不到。

WPF 窗口是 Window 类的实例，其类层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Window
```

Window 类提供了许多属性和方法，允许你在 WPF 应用程序中处理窗口。表 9.1 列出了 Window 类的一些值得注意的属性：

## 表 9.1：Window 类的值得注意的属性

| Property | Description |
|---|---|
| AllowsTransparency | 设置或检索一个值，该值指示窗口是否可以透明 |
| DialogResult | 设置或检索对话框的结果，例如单击 OK 或 Cancel 按钮的结果 |
| Height | 设置或检索窗口的高度 |
| Icon | 设置或检索窗口的图标 |
| IsActive | 检索一个值，该值指示窗口是否处于活动状态，即窗口是否位于应用程序中所有其他窗口之上 |
| Left | 设置或检索窗口左侧或边缘相对于屏幕的当前位置 |
| LogicalChildren | 检索窗口的逻辑子元素的枚举器 |
| Name | 设置或检索窗口的名称 |
| OwnedWindows | 检索由当前窗口拥有的窗口集合 |
| Owner | 设置或检索当前窗口的所有者窗口 |
| ResizeMode | 设置或检索来自 ResizeMode 枚举的值，以指定窗口是否可以调整大小 |
| RestoreBounds | 检索窗口在恢复时的大小和位置 |
| ShowInTaskbar | 允许你指定窗口是否出现在任务栏中 |
| SizeToContent | 设置或检索来自 SizeToContent 枚举的值，以指定窗口是否自动调整大小以适应内容 |
| Title | 设置或检索窗口的标题 |
| Top | 设置或检索窗口顶部边缘相对于屏幕的当前位置 |
| Topmost | 设置或检索一个值，该值指示窗口是否始终显示在其他窗口之上 |
| Width | 设置或检索窗口的宽度 |
| WindowStartupLocation | 设置或检索窗口的启动位置 |
| WindowState | 设置或检索窗口的当前状态，即窗口是最小化、最大化还是恢复 |
| WindowStyle | 设置或检索窗口边框的当前样式 |

表 9.2 列出了 Window 类的值得注意的方法：

## 表 9.2：Window 类的值得注意的方法

| Method | Description |
|---|---|
| Activate | 通过将其显示在前台来激活窗口 |
| AddChild | 将控件或元素作为子元素添加到窗口 |
| Close | 关闭窗口 |
| DragMove | 允许你通过按住鼠标左键并拖动鼠标来移动窗口 |
| GetWindow | 检索托管给定依赖对象的窗口 |
| Hide | 隐藏窗口 |
| OnClosed | 为窗口引发 Closed 事件 |
| OnClosing | 为窗口引发 Closing 事件 |
| OnLocationChanged | 为窗口引发 LocationChanged 事件 |
| OnStateChanged | 为窗口引发 StateChanged 事件 |
| OnStyleChanged | 允许你检查窗口的样式 |
| Show | 显示窗口 |
| ShowDialog | 显示对话框 |

表 9.3 列出了 Window 类的值得注意的事件：

## 表 9.3：Window 类的值得注意的事件

| Event | Description |
|---|---|
| Activated | 当窗口被激活时发生，即当窗口成为活动窗口时 |
| Closed | 在窗口关闭前发生 |
| Closing | 在窗口关闭前发生，但为你提供取消窗口关闭的选项 |
| ContentRendered | 在窗口内容呈现后发生 |
| Deactivated | 当窗口不再是活动窗口时发生 |
| LocationChanged | 当窗口位置发生变化时发生 |
| StateChanged | 当窗口状态发生变化时发生 |

如前所述，独立 WPF 应用程序可以有多个窗口。然而，只有一个主应用程序窗口，默认情况下它是第一个窗口。

> NOTE
> 独立 WPF 应用程序以当前用户的全部权限运行。

## XAML 浏览器应用程序

顾名思义，XAML 浏览器应用程序（XBAP，发音为 x-bap）是在 Web 浏览器中运行的由 Web 服务器托管的 WPF 应用程序。XBAP 由多个页面组成，用户可以通过浏览器访问和导航。这类似于传统网站的工作方式。与独立 WPF 应用程序不同，XBAP 未安装在用户计算机上。这意味着如果用户离线（与互联网或托管 XBAP 的服务器断开连接），他们无法访问 XBAP。请注意，XBAP 可以从 Internet Explorer 和 Firefox Web 浏览器访问。XBAP 与独立 WPF 应用程序之间的另一个关键区别是，XBAP 具有有限的权限，而独立 WPF 应用程序以当前登录的桌面用户的权限运行。

> NOTE
> 如果用户计算机上存在 .NET Framework，则可以访问 XBAP。当你编译 XBAP 时，它会被编译为 .xbap 扩展名，而 Windows 应用程序会被编译为 .exe 扩展名。

## XBAP 的项目模板和文件

Visual Studio 2010 提供了用于创建 XBAP 的项目模板。执行以下步骤创建 XBAP：

- 1. 单击 开始 → 所有程序 → Microsoft Visual Studio 2010 → Microsoft Visual Studio 2010 选项。Visual Studio 2010 IDE 打开。

