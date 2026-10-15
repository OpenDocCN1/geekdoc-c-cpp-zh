

你可以在 App.xaml.cs 文件中访问这些应用程序级设置，该文件是 App.xaml 的代码隐藏文件。你也可以在 App.xaml 的代码隐藏文件中为各种应用程序级事件指定事件处理程序。App.xaml.cs 文件的默认内容如下：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;

namespace SampleSilverlightApplication
{
    public partial class App : Application
    {
        public App()
        {
            this.Startup += this.Application_Startup;
            this.Exit += this.Application_Exit;
            this.UnhandledException += this.Application_UnhandledException;

            InitializeComponent();
        }
        private void Application_Startup(object sender, StartupEventArgs e)
        {
            this.RootVisual = new MainPage();
        }

        private void Application_Exit(object sender, EventArgs e)
        {
        }
        private void Application_UnhandledException(object sender,
            ApplicationUnhandledExceptionEventArgs e)
        {
            // 如果应用程序在调试器外部运行，则使用浏览器的异常机制报告异常。
            // 在 IE 上，这会在状态栏中显示一个黄色警告图标，
            // 而 Firefox 会显示脚本错误。
            if (!System.Diagnostics.Debugger.IsAttached)
            {
                // 注意：这将允许应用程序在抛出异常后继续运行，
                // 但该异常并未被处理。
                // 对于生产应用程序，此错误处理应替换为能够向网站报告错误
                // 并停止应用程序的机制。
                e.Handled = true;
                Deployment.Current.Dispatcher.BeginInvoke(delegate { ReportErrorToDOM(e); });
            }
        }

        private void ReportErrorToDOM(ApplicationUnhandledExceptionEventArgs e)
        {

```
```csharp
try
{
    string errormsg = e.ExceptionObject.Message +
        e.ExceptionObject.StackTrace;
    errormsg = errormsg.Replace("'", "\\'").Replace("\r\n", "@\n");

    System.Windows.Browser.HtmlPage.Window.Eval("throw new Error(\"Unhandled\nError in Silverlight Application \" + errormsg + \"\");");
}
catch (Exception)
{
}
```
```

在上述代码片段中，你可以看到 App 类，它继承自 Application 类。在 App 类的构造函数中，指定了 Startup、Exit 和 UnhandledException 事件的处理程序。

App 类具有一些可用于配置应用程序的属性。表 17.1 列出了 App 类中值得注意的属性：

| 表 17.1：App 类的值得注意的属性 |
|---|
| **属性** | **说明** |
| Host | 允许你检索有关承载 Silverlight 应用程序的 Web 应用程序的信息。 |
| Resources | 检索应用程序级资源的集合，例如样式和模板。 |
| RootVisual | 允许你设置或检索应用程序的主 UI 对象。默认情况下，它是一个 Page 对象。 |

现在，让我们讨论对应于 Silverlight 应用程序 UI 的 MainPage.xaml 和 MainPage.xaml.cs 文件。MainPage.xaml 文件是另一个 XAML 文件，其中包含若干个用于设计 Silverlight 应用程序 UI 的 XAML 元素。而 MainPage.xaml.cs 文件是代码隐藏文件，其中包含用于响应用户与页面交互的代码。Silverlight 应用程序的 MainPage.xaml 文件的默认内容如下所示：

```
```xml
<UserControl x:Class="SampleSilverlightApplication.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot" Background="White">
    </Grid>
</UserControl>
```
```

在上述代码片段中，你可以看到最顶层的元素是 UserControl 元素，它有一个 Grid 元素作为其子元素。你可能还会注意到 UserControl 元素具有五个属性——x:Class、xmlns、xmlns:x、Width 和 Height。x:Class 属性将 UserControl 元素绑定到代码隐藏（MainPage.xaml.cs）文件中 SampleSilverlightApplication 命名空间下的 Page 类的分部类。xmlns 和 xmlns:x 属性分别引用默认的 Silverlight 和 XAML 命名空间。UserControl 元素的 Width 和 Height 属性表示元素的宽度和高度。

接下来，让我们继续了解应用程序包（.xap 文件）。

## 应用程序包

当你编译 Silverlight 3.0 应用程序时，它们会被编译成应用程序包。应用程序包是扩展名为 .xap 的文件。.xap（读作 zap）文件包含运行 Silverlight 应用程序所需的所有必需文件和资源，如图 17.8 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_881_0.png)

# 图 17.8：展示 Silverlight 3.0 应用程序的 .xap 文件

请注意，只有 Silverlight 应用程序被编译后，你才能看到 .xap 文件（图 17.8）。此外，该文件出现在 Silverlight 应用程序项目文件夹内的 Bin→Debug 文件夹中。请注意，在解决方案资源管理器中，你可能无法在 Silverlight 应用程序项目文件夹内看到 .xap 文件。要查看 .xap 文件，请单击解决方案资源管理器工具栏中的“显示所有文件”按钮。

.xap 文件是一个部署单元，它包含应用程序清单和 Silverlight 应用程序的程序集。应用程序清单以 AppManifest.xaml 存储，是一个 XAML 文件，其中包含 Silverlight 应用程序中使用的程序集列表。应用程序清单包含 Deployment 和 AssemblyPart 元素，用于包含所需程序集以及应用程序程序集的列表。应用程序程序集在你编译应用程序后存在于 Bin→Debug 文件夹中，并且与 Silverlight 应用程序同名，例如，名为 MySilverlightApp1 的 Silverlight 应用程序的应用程序程序集是 MySilverlightApp1.dll。

> 注意
> 你可以将 .xap 文件的扩展名改为 .zip 并解压其中的文件。此外，在 ASP.NET 或 HTML 测试页面中初始化 Silverlight 应用程序时，.xap 文件被指定为 createObject() 或 createObjectEx() 方法中的参数之一。

现在，让我们学习如何开发 Silverlight 应用程序。

## Silverlight 应用程序中的控件

Visual Studio 2010 提供了大量控件来构建 Silverlight 3.0 应用程序的 UI。这些控件可以通过 XAML 和代码隐藏文件添加到 Silverlight 应用程序中。如前所述，默认情况下，会为 Silverlight 应用程序的 UI 创建一个 MainPage.xaml 文件。你可以在此文件中使用各种 XAML 元素来设计应用程序。你可以将元素相互嵌套，并设置这些元素的不同属性以获得所需的视觉效果。

Silverlight 中的控件对应于不同的 XAML 元素。你添加到 Silverlight 应用程序中的控件或元素成为层次树的一部分，然后该树会被渲染以显示给客户端。你可能还记得，在 Silverlight 应用程序中，UserControl XAML 元素是层次树的根元素。默认情况下，UserControl 元素有一个 Grid 元素作为其子元素。你需要将控件放置在 Grid 元素内部，使这些控件成为 Grid 元素的子元素。当你不断向 Silverlight 应用程序添加控件时，层次树结构会不断增长。

> 注意
> Grid 是一个容器控件，就像 Canvas 和 StackPanel 控件一样。这些控件或元素有助于你轻松方便地排列它们所包含的控件。

