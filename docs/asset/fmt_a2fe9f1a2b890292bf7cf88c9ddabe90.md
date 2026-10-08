
```csharp
using System.windows.Input;
using System.windows.Media;
using System.windows.Media.Animation;
using System.windows.Shapes;

namespace SilverlightApplication
{
    public partial class App : Application
    {
        public App()
        {
            this.Start += this.Application_Start;
            this.Exit += this.Application_Exit;
            this.UnhandledException += this.Application_UnhandledException;

            InitializeComponent();
        }
        private void Application_startup(object sender, EventArgs e)
        {
            this.RootVisual = new MainPage();
        }

        private void Application_Exit(object sender, EventArgs e)
        {
        }

        private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
        {
            // 如果应用程序在调试器之外运行，则使用浏览器的异常机制
            // 报告异常。在 IE 上，这将状态栏中显示黄色警告
            // 图标，Firefox 将显示脚本错误。
            if (!System.Diagnostics.Debugger.IsAttached)
            {
                // 注意：这将允许应用程序在抛出异常
                // 但未被处理后继续运行
                // 对于生产级应用程序，此错误处理将被替换
                // 为某些会将错误报告给网站
                // 并停止应用程序的内容
                e.Handled = true;
                Deployment.Current.Dispatcher.BeginInvoke(delegate { ReportErrorToDOM(e); });
            }
        }

        private void ReportErrorToDOM(ApplicationUnhandledExceptionEventArgs e)
        {
            try
            {
                string errorMsg = e.ExceptionObject.Message + 
                                 e.ExceptionObject.StackTrace;
                errorMsg = errorMsg.Replace("'", "\\'").Replace("\r\n", "\r\n");
                System.windows.Browser.HtmlPage.window.Eval("throw new Error(\'Silverlight Application ' + errorMsg + '\');");
            } catch (Exception)
            {
            }
        }
    }
}
```

# 第 14 章：使用 Silverlight 5.0 增强 Web

## 深度解析

在前面的代码段中，我们拥有具有 `App`。在 `App` 的构造函数中指定了 `Startup` 和 `UnhandledException` 事件的处理程序。

`App` 类具有用于配置应用程序的属性。表 14.1 列出了 `App` 的属性：

| 表 14.1 App 类的重要属性 | 说明 |
| --- | --- |
| Host | 获取有关应用程序的信息。 |
| Resources | 获取应用程序级资源集合。 |
| RootVisual | 设置或获取主 UI。默认情况下是一个 Page。 |

现在，让我们讨论包含 UI 的 `MainPage.xaml` 和 `MainPage.cs` 文件。`MainPage.xaml` 是另一个包含设计 UI 的多个 XAML 元素的文件。`MainPage.cs` 是响应页面交互的后置代码。`MainPage.xaml` 的内容所示：

```xml
<UserControl x:Class="SilverlightApplication.MainPage"
     xmlns="http://schemas.microsoft.com/winfx/2008/presentation"
     xmlns:x="http://schemas.microsoft.com/winfx/2008/xaml"
     xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
     xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
     mc:Ignorable="d"
     d:Height="300" d:Width="400">
  <Grid Name="LayoutRoot" Background="White">
  </Grid>
</UserControl>
```

## 应用程序包

编译 Silverlight 5.0 应用程序时，它们会被编译为应用程序包。.xap 文件包含运行 Silverlight 应用所需的所有文件和资源，如图 14.8 所示：

![](img/17af790174c480761404624aeed9b30b_694_0.png)

图 14.8：Silverlight 5.0 的 .xap 文件

请注意，只有在编译 Silverlight 后才能看到 `.xaml` 文件（图 14-5）。此外，该文件出现在 Silverlight 项目文件夹内的 `BinDebug` 文件夹中。请注意，在解决方案资源管理器中，可能无法查看 Silverlight 应用项目文件夹内的 `.xaml` 文件。要查看 `.xaml` 文件，请点击解决方案资源管理器工具栏上的“显示所有文件”（Show All Files）。

Axaml 文件是部署的一部分，它包含了 Silverlight 程序的清单和程序集。应用程序清单（或 `AppManifest.xaml`）是一个 XAML 文件，其中列出了 Silverlight 应用程序中使用的程序集。应用程序清单包含 `Deployment` 和 `AssemblyPart` 元素，用于包含所有程序集以及应用程序程序集。编译应用程序后，应用程序程序集存在 `BinDebug` 文件夹中，名称为 Silverlight，例如，名为 `MySilverlightApp` 的 Silverlight 应用程序的程序名为 `MySilverlightApp.dll`。

> 注意
> 你可以更改 zip 文件的提取范围以及其中包含的文件。此外，在 ASP.NET 或 HTML 页面初始化 Silverlight 应用程序时，zip 文件被指定为 `createObject` 或 `createOperationContext` 的参数之一。

现在，让我们来看看 Silverlight 应用程序中的控件。

## Silverlight 中的控件

Visual Studio 2012 提供了许多控件来构建 Silverlight 5.0 应用程序的 UI。这些控件可以通过 XAML 和后代码文件添加到 Silverlight 应用程序中。如前所述，为 Silverlight 运行时 UI 创建默认的 `Main.xaml` 文件。你可以使用此文件中的各种 XAML 元素来设计应用程序。你可以相互嵌套这些元素并设置它们的属性以获得所需的外观。

Silverlight 中的控件使用不同的 XAML 元素。你添加到 Silverlight 应用程序中的控件或元素将成为层次树的一部分，并渲染显示给客户端。你可能记得，在 Silverlight 应用程序中，`UserControl` XAML 元素是层次树的根元素。默认情况下，`UserControl` 元素有一个 `Grid` 元素作为子元素。你需要将控件放在 `Grid` 元素内部，这样在不断向 Silverlight 应用程序添加控件时，层次树结构就会不断增长。

> 注意
> `Grid` 就像 `Canvas` 和 `StackPanel` 控件一样。这些控件或元素可以帮助你方便快捷地安排包含在其中的控件。

Silverlight 5.0 拥有常规控件，如 `Button`、`TextBox`、`RadioButton` 和 `Scrollbar`，以及其他控件，如 `Calendar`、`DatePicker` 和 `TabControl`。这些控件帮助你为用户提供动态、交互且具有吸引力的 UI。Silverlight 5.0 包含了许多以前版本 Silverlight 运行时（插件）使用的控件（例如 Silverlight 2.0）或作为 Silverlight SDK 部分的控件。要按顺序使用这些控件（例如 `DatePicker`、`GridSplitter` 和 `TabControl`），你必须引用相应的程序集和命名空间。然而，你只需将它们拖放到 Silverlight 界面中，相应的程序集和命名空间会自动添加到你的 Silverlight 应用程序中。

### 表 14.2：Silverlight 5.0 中的控件

| 控件 | 描述 | XAML 元素示例 |
| --- | --- | --- |
| Border | 允许为某些其他控件添加边框和背景。 | <Border BorderBrush="Blue" BorderThickness="3"/> |
| Button | 允许你提供一个响应鼠标和键盘事件的按钮。 | <Button Content="Hello" ClickMode="Press"/> |
| 控件 | XAML 元素示例 |
| --- | --- |
| Calendar | 允许你查看日历并对日、月、年进行操作。 | <Calendar DisplayMode="Month" IsTodayHighlighted="True"/> |
| Canvas | 允许你在给定位置定位并安排包含的控件。 | <Canvas><Button Content="Hello" Canvas.Left="50" Top="50" /></Canvas> |
| CheckBox | 允许你提供数据来检查选择或清除选项。复选框可以同时处于已选中、未勾选或不确定状态。 | <CheckBox ClickMode="Press" IsChecked="False" Content="Apple" /> |
| ContentControl | 指向仅包含一个内容的控件。多个控件派生自 ContentControl 类。 | <ContentControl Content="Silver" /> |
| DataGrid | 允许你以行和列网格的形式显示数据。 | <DataGrid ItemsSource="Silverlight" AutoGenerateColumns="True" ColumnHeaderHeight="0" AlternatingRow="Orange" /> |
| DatePicker | 允许你从给定日历或所需的日期选择日期。 | <DatePicker SelectedDateFormat="Short" /> |
| Ellipse | 允许你提供椭圆形形状。 | <Ellipse Height="100" Width="180" /> |
| Grid | 允许你按行和列安排包含的控件。 | <Grid Background="Yellow" ShowGridLines="True"><RowDefinitions><Row Height="50" /><Row Height="50" /></RowDefinitions><Button Content="Silverlight" /></Grid> |
| GridSplitter | 允许你提供一个 UI 元素，用户可以通过移动它调整网格行列之间的空间。 | <GridSplitter Row="0" ShowPreview="True" Height="10" Width="300" /> |
| HyperlinkButton | 允许你显示带有超链接的按钮。 | <HyperlinkButton Content="URL for Google" NavigateUrl="http://google.com"/> |
| Image | 允许你显示图像。 | <Image Height="100" Width="180" /> |
| ItemsControl | 允许你显示项集合。许多控件都可以显示此项。 | <ItemsControl Source="Silverlight" /> |
| Line | 允许你画一条线。 | <Line Stroke="Red" StrokeThickness="5" /> |
| ListBox | 允许你显示项列表。 | <ListBox><ListBoxItem Content="Apple"/><ListBoxItem Content="Mango"/><ListBoxItem Content="Strawberry"/></ListBox> |
| 控件 | 描述 | XAML 元素示例 |
| --- | --- | --- |
| MediaElement | 允许你托管音频和视频文件。 | <MediaElement Height="100" Width="100" Source="Butterfly.wmv" |
| Popup | 允许在控件上方临时显示信息。 | <Popup Open="True"><PopupChild><Button Name="button" Height="30" /></PopupChild></Popup> |
| RadioButton | 允许你显示一个代表选项的单选按钮。 | <RadioButton ClickMode="Press" Content="Apple" /> |
| Rectangle | 允许你显示一个矩形。 | <Rectangle Fill="Violet" Height="100" Width="100" /> |
| RepeatButton | 提供一个在鼠标释放时定期引发点击事件的按钮。 | <RepeatButton Content="Hello" Delay="30" Interval="90" /> |
| ScrollBar | 允许你提供一个带有滑块的滚动条，你可以通过它更改值。 | <ScrollBar Minimum="0" Maximum="10" ViewportSize="1" Height="30" Width="7" /> |
| ScrollViewer | 允许你使用水平或垂直条查看某些内容。 | <ScrollView Content="Silverlight" Height="100" Width="100" ScrollScrollBar="Visible" VerticalScrollBar="Visible" /> |
| Slider | 允许你提供一个带有滑块的滑器，你可以移动它在给定的值范围内选择特定值。 | <Slider Orientation="Horizontal" Value="5" Maximum="100" Minimum="0" /> |
| StackPanel | 允许你水平或垂直堆叠包含的控件。 | <StackPanel><Button Content="Apple"/><Button Content="Mango"/><Button Content="Strawberry"/></StackPanel> |
| TabControl | 允许通过标签页显示信息。每个标签都可以包含各种类型的其他控件。 | <TabControl Height="280" Width="250"><TabItem Header="General" Content="This has some general information"/><TabItem Header="Academics"/><TabItem Header="Professional"/></TabControl> |
| TextBlock | 允许你显示文本。 | <TextBlock Text="Hello" /> |
| TextBox | 允许你显示文本或从用户获取文本。在 Silverlight 5.0 中，TextBox 控件可以显示多行文本并在控件周围换行。 | <TextBox Text="Hello, this is the TextBox control in Silverlight 2" IsReadOnly="False" Height="75" Width="75" TextWrapping="Wrap" /> |
| ToggleButton | 允许你提供一个可以在点击和未点击状态之间切换的按钮。 | <ToggleButton Content="Hello" ClickMode="Press" IsThreeState="True" Height="30" /> |
