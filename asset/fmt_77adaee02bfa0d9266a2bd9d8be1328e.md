
> 图 8-24：选中的项目现在倒置显示

# 动画

动画通常被认为是视觉装饰且并非必要的，但如果由专业人士以克制的方式设计，动画在增强产品整体用户体验方面起着至关重要的作用。在现实世界中，过渡并不是瞬间发生的（少数例外外，例如打开灯）。它们具有速度、加速度和减速。动画和过渡还可以帮助引导用户的注意力，解释事情发生的原因（例如，当你将窗口最小化到任务栏时，短动画显示了窗口消失的位置），并通常使虚拟体验更加流畅，使其更接近现实世界。

在 Silverlight 中，动画在技术上不仅仅是属性随时间的渐变变化。Silverlight (`WPF`) 动画是基于时间而非帧的。这意味着如果一个动画被设置为 2 秒，那么它将恰好花费 2 秒，即使计算机非常忙，在动画运行期间也只能显示几帧。除了基于时间的动画更具预测性外，它还允许 Silverlight 运行时通过跳过或插值动画帧来持续适应计算机性能。

# 故事板与动画

创建复杂动画的最佳工具是 Blend。然而，要理解动画的工作原理，只需从 XAML 中的简单示例开始，如列表 8-16 所示。

### 代码列表 8-16: BouncingCircle.xaml

```xml
<UserControl
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
xmlns:i="clr-namespace:System.Interactivity;assembly=System.Interactivity"
xmlns:local="clr-namespace:Microsoft.Expression.Interactivity.Media;assembly=Microsoft.Expression.Interactions"
x:Class="AnimationDemo.BouncingCircle"
d:Height="300" d:Width="400">

<UserControl.Resources>
<Storyboard x:Name="Storyboard1">
<DoubleAnimation TargetProperty="Canvas.Left" />
<Storyboard.TargetName="ellipse" To="320" />
<DoubleAnimation TargetProperty="Canvas.Top" />
<Storyboard.TargetName="ellipse" To="320" />
</Storyboard>
</UserControl.Resources>
<Canvas x:Name="LayoutRoot">
<Ellipse x:Name="ellipse" Fill="Black" Height="50" Width="50" />
<i:Interaction.Triggers>
<i:EventTrigger EventName="MouseLeft">
<DoubleAnimation TargetProperty="Canvas.Left" To="20" />
</i:EventTrigger>
</i:Interaction.Triggers>
</Canvas>
</UserControl>
```

代码文件 `[BouncingCircle.xaml]` 可在 Wrox.com 下载。

之前显示的动画示例是为了易理解而创建的，但在性能方面并不理想。这是因为弹跳循环动画了 `Canvas.Left` 和 `Canvas.Top` 属性。这反过来触发了对 `Canvas` 和 `Ellipse` 布局的重新计算。尽管在示例中并不明显，但布局重新计算是一项昂贵的操作——视觉树中受影响的部分必须通过 `MeasureOverride` 和 `ArrangeOverride` 方法进行遍历。可以想象复杂的场景将消耗大量时间，导致动画卡顿。

变换允许移动、旋转、缩放（更改大小）和倾斜任何 UI 元素。Silverlight 3.3 还引入了平面投影（`PlaneProjection`），它可以在三维空间中旋转二维元素。

针对 `ellipseTranslate` 元素的动画，该元素定义在 `Ellipse` 标签内：

```xml
<Ellipse x:Name="ellipse" Fill="Black" Height="50"
  Canvas.Left="20" Canvas.Top="20" Width="50">
  <Ellipse.RenderTransform>
    <TranslateTransform x:Name="ellipseTranslate" />
  </Ellipse.RenderTransform>
</Ellipse>
```

通过 Silverlight 的渲染变换更改大小、位置、旋转或其他变换不会触发布局重新计算。这意味着 CPU 的工作量减少；因此，在性能开始下降之前可以执行更复杂的动画。`WPF` 具有影响布局的“布局变换”概念——这在某些情况下非常有用。对于 Silverlight，Silverlight Toolkit 包含一个 `LayoutTransformer`，其功能几乎相同。

![](img/b5597c749e848b27b0d305153ae16106_386_0.png)

图 8-28 显示了 Silverlight 中可用的变换，`TranslateTransform` 除外，后者仅仅是移动元素的位置。

> 图 8-28：Silverlight 中的渲染变换

## 媒体

Silverlight 中的媒体包括播放音频和视频文件、访问计算机上的麦克风和摄像头、DRM 以及 Deep Zoom。本节介绍了 Silverlight 媒体的基础知识。

## 音频和视频播放

使用 `MediaElement` 控件播放音频或视频文件非常简单。编译并运行此代码后，它在 Channel9 上展示了“设计师与开发者”的视图对比：

```xml
<UserControl x:Class="Mediaelems.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
c:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot" Background="White">
  <MediaElement Source="http://mschnlnline.llwd.net/dl/ch9/0/8/7/7/7/4/SL3ExpressionLaunch_ch9.wmv"
Stretch="Uniform" />
</Grid>
</UserControl>
```

`MediaElement` 可以同时播放音频和视频文件。它支持多种交付方式（包括渐进式下载、基于 HTTP 的 Windows Media 流媒体、ASX、服务器端列表或自定义的 `MediaStreamSource`，开发者可以实现自己的媒体流源）。

微软编码家族支持 Windows Media Audio (`WMA`) 标准版和专业版，以及 Windows Media Video 7、8 和 9 编码格式。此外，它还支持 `MP3` 以及视频 `H.264`（最广泛的在线视频格式）。

> 如需有关支持的交付方式、容器和编码器的完整参考，请查看 Silveright 文档。

`MediaElement` 可以 `Play`、`Pause` 和 `Seek` 媒体，它会触发事件来跟踪播放状态、缓冲以及媒体中的当前位置。还可以控制 `Volume`。`Stretch` 属性的行为在 `Videobox` 的情况下完全相同。

`MediaElement` 是一个矩形元素。Silverlight 有一个可以通过 `SourceName` 属性关联 `MediaElement` 的 `VideoBrush`。如果使用 `VideoBrush` 填充元素或形状的 `Stroke`，视频将在元素内播放。当 `VideoBrush` 用作 `TextBlock` 的 `Foreground` 时，会产生有趣的效果。

```xml
<UserControl.Resources>
<VideoBrush x:Key="myVideoBrush"
SourceName="myMediaElement" Stretch="UniformToFill"/>
</UserControl.Resources>
<Grid Name="LayoutRoot" Background="White">
<MediaElement Visibility="Collapsed" x:Name="myMediaElement"
Source="http://msichlinellnw.net/dl/ch9/0/8/7/7/4/SLExpression3launch_ch9.wmv"
Stretch="Uniform" />
<TextBlock Text="Text with a VideoBrush"
Foreground=(StaticResource myVideoBrush)
FontFamily="Arial" FontWeight="Bold"
FontSize="72" />
</Grid>
```

图 8-29 显示了输出。

> 图 8-29：带有 VideoBrush 的文本

## Deep Zoom

另一个示例展示了 `VideoBrush` 的威力，即可以在 http://demo.thestream.com/videopuzzle/ 的视频。图 30 显示了游戏。

![](img/b5597c749e848b27b0d305153ae16106_388_0.png)

> 图 30：由 MS LLC 开发的视频游戏（Copyright 2004-2008）

Silverlight 独特的 Deep Zoom 功能（`WPF` 中可用）允许访问者快速、流畅地浏览数百张高分辨率图像。这里的“高分辨率”意味着像素级。Bing Maps（图 31 和 32）使用 Deep Zoom 提供平滑的缩放体验，从整个世界开始，缩放到直到人脸因隐私原因变得模糊的级别。

![](img/b5597c749e848b27b0d305153ae16106_388_1.png)

> 图 31：Bing maps 上的地球

![](img/b5597c749e848b27b0d305153ae16106_389_0.png)

> 图 32：缩放到街景视图后的 Bing Maps

Deep Zoom 是基于微软获得的技术。该技术的一个关键属性是性能和所需的带宽取决于屏幕上的像素数量，而不是显示图像的大小。Deep Zoom 通过创建不同分辨率的图像小瓦片，并利用先进的启发式算法下载视口内所需的瓦片来实现魔法。Deep Zoom（或者说是 `MultiScaleImage` 控件）也可以同时处理大量图像。在约 1000 张图像处，Silverlight 的性能开始下降。图 33 显示了一个示例。

![](img/b5597c749e848b27b0d305153ae16106_389_1.png)

> 图 33：Zoomery (www.zoomery.com)

## 流畅流媒体

流畅流（或自适应流媒体）是网络视频最有趣的交付方式之一。随着人们家里可用带宽越来越大，用户对高质量视频的需求日益增加。Silverlight 旨在成为高质量在线视频的最佳解决方案。

当今在线视频有几个流媒体旨在解决的问题。之一是网络带宽。虽然 HD 质量视频可以以每秒 2-3 Mbps 的速度传输，许多互联网连接超过了此带宽，但仍有数千个连接低于此。如果可用带宽不足以播放，缓冲期间会频繁中断。此外，播放器与媒体服务器之间的实际带宽可能会差异很大——媒体服务器可能会过载，或者当同一网络上的其他人（例如家庭）也在下载文件时，终端用户可能只有部分带宽。

另一个影响终端用户播放体验的重要因素是所用计算机的计算能力。解码和显示 HD 视频是一项非常密集的任务——像素值每秒必须计算 30 次。任何计算机无法胜任时（例如 CPU 正在忙于其他事情，或者计算机本身就不强大），卡顿现象都是明显的。

在电影中进行跳转也很困难。某些使用渐进式下载的播放器在整个文件下载完成之前不允许跳转到电影末尾。这不仅让用户感到沮丧，如果用户只想看最后五分钟，这还会浪费内容提供者的带宽。

为了解决这些问题，内容制作人员为不同的比特率对视频进行编码。然而，为了选择最佳质量，用户必须了解许多技术细节，并在电影期间可能手动多次切换“高带宽”和“低带宽”版本。

流畅流媒体还需要内容以多种比特率进行编码。巨大的优势是流媒体会持续监控可用带宽和 CPU 负载——如果这些任何因素表明需要较低的带宽，流媒体播放器会自动无缝地切换到低质量版本。结果是即使在带宽和 CPU 条件糟糕的情况下，用户获得最好的连续播放。

在直播的情况下，流畅流媒体可以暂停和回退视频，保留上述优势。然而，直播编码比视频点播服务的编码要困难得多。Expression Encoder 4 可以执行流畅流媒体，但你需要一个 6-8 核的 CPU 来执行直播编码，即使如此你也必须关闭一个

大量的质量优化，并将广播限制在少数几个带宽上。如今最好的妥办法是使用专用的硬件编码器。

> > 如果您想亲自体验流畅的流传输，请访问 http://www.iis.net/media/experiencessmootestreaming。

## 摄像头和麦克风访问

Silverlight 4 引入了一个深受需求的功能：摄像头和麦克风访问。一个简单的 Webcam 应用程序包含列表 8-17 显示的 XAML 文件和列表 8-18 显示的 cs 文件。

### 列表 8-17: Webcam.xaml

```xml
<UserControl x="Class:MediaDemos.Webcam"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignWidth="300">
  <Grid x:Name="LayoutRoot" Background="White">
    <Button Content="Enable Camera" Click="Button_Click" />
    <Ellipse x:Name="ellipse" Stroke="Black" StrokeThickness="1" />
  </Grid>
</UserControl>
```

| 代码文件 | Webcam.xaml | 可在 Wrox.com 下载 |

| :--- | :--- | :--- |

### 列表 8-18: Webcam.cs

```csharp
using System.Windows;
using System.Windows.Controls;
using System.Windows.Media;

namespace MediaDemos
{
  public partial class Webcam : UserControl
{
    private VideoBrush webcamBrush;

    public Webcam()
  }
```

```csharp
{
  InitializeComponent();
}

private void Button_Click(object sender, EventArgs e) {
  if (!DeviceConfiguration.RequestDeviceAccess()) {
    MessageBox.Show("In that case, I won't show anything for you");
    return;
  }

  var videoDevice = DeviceConfiguration.GetDefaultVideoCapture();
  var cs = new CaptureSource();
  cs.VideoCaptureDevice = videoDevice;
  webcamBrush = new VideoBrush();
  webcamBrush.SetSource(cs);
  ellipse.Fill = webcamBrush;
  cs.Start();
}
```

代码文件 `[Webcam.cs]` 可在 Wrox.com 下载。

8-34 显示了运行该应用程序如何揭露您的真脸。

要开始使用摄像头，用户必须允许访问捕获设备。出于隐私考虑，只能从用户触发的操作请求访问。因此，你需要一个按钮并启用其 Click 事件。如果请求成功，将设置默认的 VideoSource 对象。最后，使用 CaptureSource 对象创建一个 VideoBrush 并开始捕获。
