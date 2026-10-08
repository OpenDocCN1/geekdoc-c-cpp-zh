
当控件数量超过可用空间所能显示的数量时，它们会被换行显示到下一列。

图 17.3 展示了一个使用 DockPanel 的示例。该布局的 XAML 代码如清单 17.4 所示。

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

## 使用图形、动画和媒体

WPF 提供了一个灵活且丰富的图形环境，支持分辨率和设备无关的图形、更高的精度、高级的图形和动画支持，以及硬件加速支持。无论实际屏幕分辨率如何，WPF 中的所有图形度量均使用像素（1/96 英寸）作为单位。

WPF 提供以下支持：

- 二维形状，如矩形和椭圆
- 用于创建自定义形状的二维几何图形
- 二维效果，如渐变、视频绘图、旋转和缩放
- 三维渲染，它与二维图形集成，使你可以显示渲染在三维形状上的二维图像

除了二维和三维图形功能外，WPF 还提供了动画支持。这使你可以让控件放大、抖动、旋转或淡入淡出，从而创建独特且有趣的过渡效果。

WPF 直接支持使用媒体（如图像、视频和音频）来传达信息。许多控件（包括 Image 控件）都隐式地知道如何显示图像。音频和视频都通过 MediaElement 控件获得支持，该控件功能强大，足以作为自定义媒体播放器的基础。

## 理解文本、排版和文档

通过 OpenType 字体支持和 ClearType 增强功能，WPF 支持高质量的文本渲染和操作。WPF 还内置了对处理流式文档、固定格式文档和 XML 纸张规范（XPS）文档的支持。

流式文档通过随窗口大小和显示设置的变化而动态重新排版内容，从而优化查看和可读性。当需要精确呈现时（例如在桌面出版应用中），可以使用固定格式文档。XPS 是一种开放、跨平台的文档格式，WPF 对 XPS 文档的支持建立在固定格式文档支持的基础上。

## 数据绑定

WPF 中的数据绑定是通过一个精密且灵活的绑定引擎处理的，该引擎允许你将控件（目标）绑定到数据（源）。此绑定引擎提供了一种简单且一致的方式来呈现和交互数据。许多控件内置了对显示单个数据项或数据项集合的支持，并且控件可以绑定到各种数据源，包括 .NET 对象和 XML。WPF 的数据绑定功能非常强大，许多以前只能通过代码实现的功能，现在可以直接在 XAML 中实现。

# 创建 WPF 应用程序

在接下来的本小时内容中，你将从创建一个新项目、布局窗体并添加控件开始，着手创建一个照片查看器应用程序。

首先，使用“新建项目”对话框创建一个新的 WPF 应用程序项目，如图 17.4 所示。在“名称”字段中输入 **PhotoViewer**。

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

# 第 17 小时：构建 Windows 应用程序

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_1.png)

最左侧的按钮显示一种树状视图，称为文档大纲，它展示了窗口中的所有可视化元素及其相互关系（参见图 17.10）。在本示例中，由于窗口没有其他元素，文档大纲并不重要。然而，当你开始添加控件和创建复杂布局时，文档大纲和所选元素轮廓都有助于在布局中进行导航。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_2.png)

如果你查看 Visual Studio 生成的 XML，`x:Class` 属性指定了实现该窗口的类的全限定名称。在这种情况下，该类是 **PhotoViewer** 命名空间中的 **MainWindow**。窗口的 **Title**（标题）、**Width**（宽度）和 **Height**（高度）也已指定。这些值可以直接在 XML 中或通过属性窗口进行修改，如图 17.11 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_392_3.png)

`xml:ns` 命名空间属性定义了 WPF 使用的模式。这些模式包含你可以集成到 WPF 应用程序中的所有控件和其他项的定义。

将窗口标题更改为 **WPF Photo Viewer**，可以通过属性窗口或直接修改 XAML 来完成。

## 创建布局

现在你可以开始为照片查看器应用程序创建布局了。如果你再次查看 XAML，你会注意到 `Window` 已经包含一个名为 `Grid` 的子元素。在这种情况下，`Grid` 未显式定义任何行或列，因此它是一个 1x1 的表格。对于照片查看器应用程序，你需要一个包含两行和两列的网格结构。

如果你点击设计选项卡中的大片空白区域，点击 XAML 中 `Grid` 元素之间的空行，或点击文档大纲中的 `Grid`，`Grid` 将成为所选元素。你可以通过鼠标在视觉上设计表格结构，将鼠标光标移到设计窗格中网格蓝色阴影的边缘。这会显示一条浅蓝色指导线，横跨网格，指示将创建行或列的位置。当指导线处于正确位置时，你可以点击鼠标左键来创建行或列。图 17.12 展示了这种操作示例的样子。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_393_0.png)

你也可以通过属性窗口编辑 `Grid` 的 `ColumnDefinitions` 和 `RowDefinitions` 属性来修改结构，如图 17.13 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_393_1.png)

这将显示一个集合编辑器对话框，如图 17.14 所示，使你可以轻松添加行和列，并同时配置它们的属性。使用集合编辑器通常是最简单的方法，特别是当你需要添加大量行或列时。事实上，如果你需要更改现有行或列的任何内容，必须使用集合编辑器或直接修改 XAML 来完成。

