
既然你已完成本书的前三部分，你应该已经熟悉了 `.NET Framework` 和 `C#` 语言。你学习了引用类型和值类型的基本区别，包括如何创建自己的类型。你了解了语言特性，如扩展方法、自动属性、Lambda 表达式、事件和异常。现在你知道了如何创建和查询数据集合，以及如何操作文件系统、XML 和数据库中的文件与目录。简而言之，你现在应该已经掌握了利用 `.NET Framework` 提供的所有必要的语言技能，来创建利用用户界面库的复杂应用程序。

尽管 `.NET Framework` 提供了两个用于开发 Windows 应用程序的不同类库——Windows Forms 和 Windows Presentation Foundation（WPF）库，但 WPF 提供了构建富 Windows 应用程序时更加完整和统一的模型。在本课时中，你将学习如何构建一个基本的 WPF 应用程序。你会看到如何通过可视化设计工具以及可扩展应用程序标记语言（XAML）以直观的方式来实现这一点。最后，你将学习如何使用 WPF 视觉样式来对应用程序进行样式化，从而构建一个易于定制的应用程序。

## 理解 WPF

Windows Presentation Foundation（WPF）提供了一个统一的编程模型，使你能够构建包含用户界面元素、媒体和文档的 Windows 应用程序。然而，WPF 不仅仅局限于用户界面。它是一个下一代呈现系统，使你能创建范围广泛的视觉丰富的独立和浏览器宿主应用程序。WPF 的核心是一个分辨率无关的基于矢量的渲染引擎，旨在充分利用现代图形硬件。WPF 是 `.NET Framework` 的一部分，你所需的大多数类型都位于 `System.Windows` 命名空间中。

### 处理标记和代码后置

如果你之前开发过 ASP.NET 应用程序，那么标记和代码后置的概念你应该已经非常熟悉。在 WPF 应用程序中，你使用标记语言来实现应用程序的外观；使用编程语言（如 `C#`）在标记“背后”实现行为。这种外观与行为的清晰分离带来了以下优势：
- 降低了开发和维护成本。
- 开发效率更高，允许应用程序的外观与其他实现应用程序行为的开发人员同时创建。
- 多个设计工具可以创建和共享标记。

### 标记

WPF 使用可扩展应用程序标记语言（XAML），它是一种基于 XML 的组合式标记语言。由于 XAML 基于 XML，由它组合的用户界面（UI）被组装成一个元素树，即嵌套元素的层次结构。元素树提供了一种创建和管理用户界面的逻辑方式。

图 17.1 展示了一个完全用 XAML 编写的简单 WPF 应用程序。具体来说，XAML 分别使用 `Window` 和 `Button` 元素定义了一个窗口和一个按钮，然后设置各种属性来指定文本、大小等。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_384_0.png)

图 17.1 WPF 中的“Hello World”

所需的 XAML 如清单 17.1 所示。

**清单 17.1 简单的 XAML**

```xml
<Window x:Class="WpfApplication1.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Hello World" Height="162" Width="328">

    <Grid Height="111" Width="303">
        <Button Content="Hello, world from WPF!"
            Margin="82,37,93,32"
            Name="button1"
            Height="42"
            HorizontalAlignment="Center"
            VerticalAlignment="Center" />
    </Grid>
</Window>
```

**`x:Class` 属性**

`x:Class` 属性指定类名，而不是包含该类的文件名称。如果你使用内置的重构支持重命名类，Visual Studio 会更新 XAML，但它不会更改实际的文件名。如果你重命名文件，Visual Studio 不会自动重命名该类。为了避免混淆，你的文件名和类名始终应该匹配。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_385_0.png)

### 代码后置

虽然这个简单应用程序包含一个按钮，但它并没有多大功能。该应用程序没有提供响应用户交互（如响应事件、调用业务逻辑或访问数据）的行为。这种行为通常在与标记关联的代码中实现，称为代码后置。

你可以通过向 `Button` 元素添加以下属性来响应按钮的 `Click` 事件：

```
Click="button1_Click"
```

这只是在标记中建立了事件与代码后置文件中方法之间的关联。所需的实际代码后置如清单 17.2 所示。在此示例中，代码后置实现了一个名为 `MainWindow` 的类，该类继承自 `Window` 类。标记中的 `x:Class` 属性将标记与其代码后置类关联起来。还会为你自动生成一个调用 `InitializeComponent` 的默认公共构造函数。`button1_Click` 方法实现了按钮 `Click` 事件的事件处理程序。

```csharp
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
    }

    private void button1_Click(object sender, RoutedEventArgs e)
    {
        MessageBox.Show("You clicked the button!");
    }
}
```

图 17.2 展示了点击按钮后的结果。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_386_0.png)

**应用程序**

打包基于 XAML 的内容并将其作为应用程序交付给用户所需的类型和服务，是 WPF 所称的**应用程序模型**的一部分。通过应用程序模型，你可以创建独立和浏览器宿主应用程序。

由于独立应用程序和浏览器宿主应用程序通常很复杂，并且需要应用程序范围的服务（如共享属性和启动管理），WPF 提供了 `Application` 类。与其他基于 WPF 的资源一样，`Application` 类由标记和代码后置组成。清单 17.3 展示了清单 17.1 中应用程序的 Application 标记组成的 XAML。

```xml
<Application x:Class="WpfApplication1.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resources> </Application.Resources>
</Application>
```

你已经在上一节中看到了一个独立应用程序的示例。这些应用程序使用 `Window` 类来创建窗口和对话框，这些窗口和对话框可以通过菜单、工具栏和其他 UI 元素访问。窗口的主要目的是托管和显示内容，如媒体、XAML 页面、Web 页面和文档。

浏览器宿主应用程序，也称为 XAML 浏览器应用程序（XBAP），使用页面（来自 `Page` 类）和页面功能（来自 `PageFunction<T>` 类）。使用 XBAP，你可以使用超链接在页面之间导航。由于 XBAP 托管在浏览器中（Internet Explorer 6 或更高版本），它们使用部分信任安全沙箱来强制执行类似施加于基于 HTML 的应用程序的限制。XBAP 可以在完全信任沙箱下运行，但用户会收到安全警告对话框，使它们可以决定是否运行该应用程序。

### 理解 WPF 布局

创建用户界面要求你按位置和大小排列控件，形成一个布局，该布局必须适应窗口大小和显示设置的变化。WPF 提供了一个强大的布局和渲染系统，为你处理这些复杂性。布局系统基于相对定位而不是固定定位，并管理控件之间的交互以确定布局。WPF 为你提供了几种布局控件，并且你可以使用自己定制的布局控件来扩展布局系统。默认的布局控件如下：
- **`Canvas`**——你可以将 `Canvas` 布局想象成艺术家的画布。`Canvas` 的所有子控件必须提供自己的布局。应谨慎使用 `Canvas`，因为它没有固有的布局特性，并使用精确定位。`Canvas` 提供的布局系统类似于 Windows Forms 或其他使用精确 x 和 y 坐标来定位控件的布局系统。
- **`DockPanel`**——子控件对齐到面板的边缘。默认情况下，`DockPanel` 的最后一个控件填充剩余空间。
- **`Grid`**——子控件通过行和列进行定位，很像表格。
- **`StackPanel`**——子控件垂直或水平堆叠。
- **`WrapPanel`**——子控件按从左到右的顺序排列，当控件数量超过所提供的空间能显示的数量时，它们会换行到下一行。`WrapPanel` 还支持从上到下的顺序，其中当控件数量超过可用空间所能显示的数量时，它们会被换行显示到下一列。

图 17.3 展示了一个使用 `DockPanel` 的示例。该布局的 XAML 代码如清单 17.4 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_388_0.png)

## 清单 17.4 使用 DockPanel 创建布局的 XAML 代码

```xml
<Window x:Class="WpfApplication1.Layouts"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Layouts" Height="182" Width="272">
    <Grid>
        <DockPanel>
            <Border DockPanel.Dock="Top" BorderThickness="1" BorderBrush="Black">
                <TextBlock Height="35">Dock = "Top"</TextBlock>
            </Border>
            <Border DockPanel.Dock="Bottom" BorderThickness="1" BorderBrush="Black">
                <TextBlock Height="31" >Dock = "Bottom"</TextBlock>
            </Border>
            <Border DockPanel.Dock="Left" BorderThickness="1" BorderBrush="Black">
                <TextBlock Width="93">Dock = "Left"</TextBlock>
            </Border>
            <Border BorderThickness="1" BorderBrush="Black">
                <TextBlock>Fill</TextBlock>
            </Border>
        </DockPanel>
    </Grid>
</Window>
```

与所有 WPF 元素一样，布局可以嵌套使用，从而允许你创建复杂的布局。

### 使用图形、动画和媒体

WPF 提供了一个灵活且丰富的图形环境，支持分辨率和设备无关的图形、更高的精度、高级的图形和动画支持，以及硬件加速支持。无论实际屏幕分辨率如何，WPF 中的所有图形度量均使用像素（1/96 英寸）作为单位。

WPF 提供以下支持：
- 二维形状，如矩形和椭圆
- 用于创建自定义形状的二维几何图形
- 二维效果，如渐变、视频绘图、旋转和缩放
- 三维渲染，它与二维图形集成，使你可以显示渲染在三维形状上的二维图像

除了二维和三维图形功能外，WPF 还提供了动画支持。这使你可以让控件放大、抖动、旋转或淡入淡出，从而创建独特且有趣的过渡效果。

WPF 直接支持使用媒体（如图像、视频和音频）来传达信息。许多控件（包括 `Image` 控件）都隐式地知道如何显示图像。音频和视频都通过 `MediaElement` 控件获得支持，该控件功能强大，足以作为自定义媒体播放器的基础。

### 理解文本、排版和文档

通过 OpenType 字体支持和 ClearType 增强功能，WPF 支持高质量的文本渲染和操作。WPF 还内置了对处理流式文档、固定格式文档和 XML 纸张规范（XPS）文档的支持。

流式文档通过随窗口大小和显示设置的变化而动态重新排版内容，从而优化查看和可读性。当需要精确呈现时（例如在桌面出版应用中），可以使用固定格式文档。XPS 是一种开放、跨平台的文档格式，WPF 对 XPS 文档的支持建立在固定格式文档支持的基础上。

### 数据绑定

WPF 中的数据绑定是通过一个精密且灵活的绑定引擎处理的，该引擎允许你将控件（目标）绑定到数据（源）。此绑定引擎提供了一种简单且一致的方式来呈现和交互数据。许多控件内置了对显示单个数据项或数据项集合的支持，并且控件可以绑定到各种数据源，包括 `.NET` 对象和 XML。WPF 的数据绑定功能非常强大，许多以前只能通过代码实现的功能，现在可以直接在 XAML 中实现。

## 创建 WPF 应用程序

在接下来的本小时内容中，你将从创建一个新项目、布局窗体并添加控件开始，着手创建一个照片查看器应用程序。

首先，使用“新建项目”对话框创建一个新的 WPF 应用程序项目，如图 17.4 所示。在“名称”字段中输入 `PhotoViewer`。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_390_0.png)

与处理控制台应用程序一样，Visual Studio 为你创建了一个解决方案和项目。这一次，Visual Studio 不再显示生成的 *C#* 类文件，而是显示应用程序主窗口的可视化设计器、控件工具箱和属性窗口。图 17.5 展示了刚刚创建完项目后 Visual Studio 应呈现的样子。

基于 XAML 的用户界面可视化设计器分为两个部分。默认情况下，上半部分显示布局的可视化表示，下半部分显示 XAML。你可以在两个部分中进行修改，在一个部分中所做的更改将反映到另一个部分中。图 17.6 展示了 XAML 设计器的更详细视图。

你可以轻松地在 XAML 和设计窗格之间切换，包括交换它们的位置，使用选项卡和“交换窗格”按钮（图中以圆圈标出），如图 17.7 所示。

你还可以通过“设计”和“XAML”选项卡右侧的按钮更改窗格的方向，在水平（默认）或垂直布局之间切换，或者完全折叠 XAML 窗格，如图 17.8 所示。

编辑窗口的底部是所选元素的轮廓，如图 17.9 所示。这直观地展示了你当前选中的元素（以粗体显示）以及包含当前选中元素的可视化元素路径。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_391_0.png)

**图 17.5**

创建 WPF 应用程序后的 Visual Studio

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_391_1.png)

**图 17.6**

XAML 编辑界面的详细视图

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_391_2.png)

**图 17.7**

设计和 XAML 选项卡

## 第 17 小时：构建 Windows 应用程序

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_1.png)

最左侧的按钮显示一种树状视图，称为文档大纲，它展示了窗口中的所有可视化元素及其相互关系（参见图 17.10）。在本示例中，由于窗口没有其他元素，文档大纲并不重要。然而，当你开始添加控件和创建复杂布局时，文档大纲和所选元素轮廓都有助于在布局中进行导航。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_2.png)

如果你查看 Visual Studio 生成的 XML，`x:Class` 属性指定了实现该窗口的类的全限定名称。在这种情况下，该类是 `PhotoViewer` 命名空间中的 `MainWindow`。窗口的 `Title`（标题）、`Width`（宽度）和 `Height`（高度）也已指定。这些值可以直接在 XML 中或通过属性窗口进行修改，如图 17.11 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_3.png)

`xml:ns` 命名空间属性定义了 WPF 使用的模式。这些模式包含你可以集成到 WPF 应用程序中的所有控件和其他项的定义。

将窗口标题更改为 `WPF Photo Viewer`，可以通过属性窗口或直接修改 XAML 来完成。

### 创建布局

现在你可以开始为照片查看器应用程序创建布局了。如果你再次查看 XAML，你会注意到 `Window` 已经包含一个名为 `Grid` 的子元素。在这种情况下，`Grid` 未显式定义任何行或列，因此它是一个 1x1 的表格。对于照片查看器应用程序，你需要一个包含两行和两列的网格结构。
