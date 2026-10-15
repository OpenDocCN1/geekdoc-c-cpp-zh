
MediaPlayer 类的重要属性列于表 12.44 中：

**表 12.44：MediaPlayer 类的属性**

| 属性 | 描述 |
|---|---|
| Balance | 获取或设置左右扬声器音量之间的平衡 |
| BufferingProgress | 检索流式内容已完成的缓冲百分比 |
| CanPause | 检索一个值，指示媒体是否可以暂停 |
| Clock | 获取或设置与要播放的媒体时间线关联的 `MediaClock` 对象 |
| DownloadProgress | 检索位于远程服务器的内容的下载进度百分比 |
| HasAnimatedProperties | 检索一个值，该值指示是否有一个或多个 `AnimationClock` 对象与对象的任何依赖属性关联 |
| HasAudio | 检索一个值，指示媒体是否具有音频输出 |
| HasVideo | 检索一个值，指示媒体是否具有视频输出 |
| IsBuffering | 检索一个值，指示媒体是否正在缓冲 |
| IsFrozen | 检索一个值，指示对象当前是否可修改 |
| IsMuted | 检索一个值，指示媒体是否静音 |
| NaturalDuration | 检索媒体的自然持续时间 |
| NaturalVideoHeight | 检索视频的像素高度 |
| NaturalVideoWidth | 检索视频的像素宽度 |
| Position | 获取或设置媒体的当前位置 |
| ScrubbingEnabled | 获取或设置一个值，指示是否启用拖拽预览 |
| Source | 检索媒体的 Uri |
| SpeedRatio | 获取或设置媒体播放速度的比率 |
| Volume | 获取或设置媒体的音量 |

MediaPlayer 类的注目方法列于表 12.45：

| Table 12.45: Methods of the MediaPlayer Class |
|---|---|
| Method | Description |
| Close | 关闭媒体 |
| Play | 开始播放 |
| Pause | 暂停播放但不改变位置 |
| Stop | 停止播放并将位置重置到文件开头 |

`MediaElement` 控件是封装 `MediaPlayer` 类全部功能的 WPF 元素。你可以在 XAML 中声明 `MediaElement` 控件的实例。你需要注意的是，如果你使用 `MediaElement` 控件播放视频，你应该将其放置在视频窗口应出现的位置。`MediaElement` 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.MediaElement
```

MediaElement 类的注目属性列于表 12.46：

| Table 12.46: Properties of the MediaElement Class |
|---|---|
| Property | Description |
| Balance | 获取或设置扬声器间的音量比例 |
| BufferingProgress | 检索指示缓冲进度百分比的值 |
| CanPause | 检索指示媒体是否可暂停的值 |
| Clock | 获取或设置与控制媒体播放的媒体时间线关联的时钟 |
| DownloadProgress | 检索指示远程服务器上内容下载完成量的百分比值 |
| HasAudio | 检索指示媒体是否具有音频的值 |
| HasVideo | 检索指示媒体是否具有视频的值 |
| IsBuffering | 获取指示媒体是否正在缓冲的值 |
| IsMuted | 获取或设置指示音频是否静音的值 |
| LoadedBehavior | 获取或设置媒体的加载行为 `MediaState` |
| NaturalDuration | 检索媒体的自然时长 |
| NaturalVideoHeight | 检索媒体相关视频的高度 |
| NaturalVideoWidth | 检索媒体相关视频的宽度 |
| Position | 获取或设置通过媒体播放时间进行的当前进度位置 |
| ScrubbingEnabled | 获取或设置指示 `MediaElement` 控件在暂停时是否更新 seek 操作的帧的值 |
| Source | 获取或设置 `MediaElement` 控件上的媒体源 |
| SpeedRatio | 获取或设置媒体的速度比率 |
| Stretch | 获取或设置描述 `MediaElement` 控件如何填充目标矩形的 `Stretch` 值 |

## Table 12.46: Properties of the MediaElement Class

| Property | Description |
|---|---|
| UnloadedBehavior | 获取或设置媒体的 `MediaState` 对象的卸载行为 |
| Volume | 获取或设置媒体音量 |

MediaElement 类的注目方法列于表 12.47：

## Table 12.47: Methods of the MediaElement Class

| Method | Description |
|---|---|
| ArrangeOverride | 安排并调整 `MediaElement` 控件的大小 |
| MeasureOverride | 更新 `MediaElement` 控件的 `DesiredSize` 属性 |
| OnCreateAutomationPeer | 创建并返回 `MediaElement` 控件的 `AutomationPeer` 对象 |
| OnRender | 在 `MediaElement` 控件的渲染过程中绘制 `DrawingContext` 对象的 content |

你可以从工具箱拖放 `MediaElement` 控件并将其添加到 WPF 应用程序。添加到 WPF 应用程序的 `MediaElement` 控件如图 12.2 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_574_0.png)

## Figure 12.2: Displaying a MediaElement Control

你可以看到，当你从工具箱添加 `MediaElement` 控件时，XAML 代码会被添加到应用程序中。

### NOTE

你应将 `MediaElement` 控件的 `LoadedBehavior` 属性设置为 `Manual`，以便交互式地停止、暂停和播放媒体。

## Modes of Media Playback

你可以在两种不同模式下使用 `MediaPlayer` 和 `MediaElement` 类；独立模式和时钟模式。模式由 `Clock` 属性决定。如果 `Clock` 属性设置为 null，媒体对象处于独立模式。如果 `Clock` 属性设置为非 null，媒体对象处于时钟模式。默认模式为独立模式。你可以通过使用媒体对象控制方法 `Play`、`Pause`、`Close` 和 `Stop` 在独立模式下控制媒体播放。你可以通过使用 `ClockController` 类的控制方法在时钟模式下控制媒体播放。`ClockController` 对象是从 `MediaClock` 类的 `ClockController` 属性获得的。你不能在时钟模式下使用媒体对象控制方法。如果你尝试使用该方法，将抛出 `InvalidOperationException` 异常。

`MediaPlayer` 类用于两种不同模式：独立模式和时钟模式。在独立模式下，`MediaPlayer` 与图像相同，并且由 `Open` 方法打开的媒体驱动播放。在时钟模式下，`MediaPlayer` 类可以与动画组合，因此有相应的 `Timeline` 和 `Clock` 类附加到它。你应使用 `VideoDrawing` 类来显示使用 `MediaPlayer` 类加载的媒体。

`MediaElement` 类也可以在两种不同模式下使用：独立模式，独立模式，`MediaElement` 对象类似于图像，并且可以直接指定 `Source` URI。在时钟模式下，`MediaElement` 对象可以与动画一起使用，因此具有 `Timeline` 和 `Clock` 类。

## Chapter 12: Using Graphics and Multimedia in Windows Forms and WPF

## Immediate Solutions

### Using Graphics in Windows Forms

在本章的 In Depth 部分，你学习了 Windows Forms 中的图形。你还学习了有助于在 Windows Forms 中创建图形的不同类。你可以使用 `CreateGraphics()` 方法在 Windows 中创建图形。`Pen` 类用于绘制图形。`Brush` 和 `Color` 类用于在 Windows Form 中创建的形状中填充颜色。让我们在 Windows Forms 应用程序中使用图形。为此，创建一个名为 `UsingGraphics` 的 Windows Forms 应用程序（也在 CD 上提供）并向 `Form1` 表单添加两个 `Button` 控件（图 12.3）。你可以从属性窗口更改 `Button` 控件上显示的文本。我们已将 `button1` 的文本更改为 Shape，将 `button2` 的文本更改为 Color，如图 12.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_576_0.png)

Figure 12.3: Adding Buttons to Form1

现在，将给定的代码添加到 `Form1.cs` 文件中，如清单 12.1 所示：

## Listing 12.1: Creating Graphics

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace UsingGraphics
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            Graphics g = this.CreateGraphics();
            Pen pen = new Pen(Color.Tomato, 2);
            g.DrawEllipse(pen, 150, 25, 50, 50);
            g.DrawEllipse(pen, 160, 35, 10, 10);
            g.DrawEllipse(pen, 180, 35, 10, 10);
            g.DrawArc(pen, 150, 35, 50, 30, 45, 90);
            g.DrawRectangle(pen, 150, 75, 50, 100);
            g.DrawLine(pen, 175, 175, 150, 250);
            g.DrawLine(pen, 175, 175, 200, 250);
        }
        private void button2_Click(object sender, EventArgs e)
        {
            Graphics g = this.CreateGraphics();
            SolidBrush myBrush = new SolidBrush(Color.Teal);
            g.FillEllipse(myBrush, 150, 25, 50, 50);
            myBrush.Color = Color.Black;
            g.FillEllipse(myBrush, 160, 35, 10, 10);
            g.FillEllipse(myBrush, 180, 35, 10, 10);
            myBrush.Color = Color.Black;
            g.FillPie(myBrush, 150, 35, 50, 30, 45, 90);
            myBrush.Color = Color.GreenYellow;
            g.FillRectangle(myBrush, 150, 75, 50, 100);
        }
```

在清单 12.1 中，我们在 `Form1` 上绘制形状。通过按键盘上的 F5 键运行应用程序。当你在 `Form1` 上单击 Shape 按钮时，你会得到如图 12.4 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_577_0.png)

## Figure 12.4: Clicking the Shape Button

我们还使用 `Color` 结构与 `SolidBrush` 类为 `Form1` 上创建的形状着色。你可以在 `button2` 的 Click 事件上添加代码并通过按键盘上的 F5 键运行应用程序。当你在 `Form1` 上单击 Color 按钮时，你会得到如图 12.5 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_577_1.png)

## Figure 12.5: Clicking the Color Button

图 12.5 所示的输出是应用程序的最终输出。

## 在 WPF 4.0 中使用二维图形

WPF 中的二维图形包括形状（shapes）、几何图形（geometries）和画笔（brushes）。通过组合这些元素，你可以创建图形丰富、外观精美的应用程序。你已经在本书“深入解析”部分学习了二维图形的相关知识。在本节中，你将实际应用 WPF 中提供的形状、几何图形和画笔。在本节中，你将了解：

- 使用二维形状
- 创建可伸缩形状
- 绘制几何图形
- 组合多个几何图形
- 变换形状
- 使用 `Path` 和 `PathGeometry` 类
- 使用画笔
- 更改画笔的平铺大小和图案
- 使用 `VisualBrush` 创建反射效果
- 保持图像的纵横比

让我们逐一详细讨论这些内容。

### 使用二维形状

WPF 中可用的形状包括 `Line`、`Polyline`、`Rectangle`、`Polygon`、`Ellipse` 和 `Path`。这些形状包含在 `Shape` 类中。你已经在本章“深入解析”部分学习了 `Shape` 类以及 WPF 中的各种形状。你可以使用形状来创建视觉吸引力强的图形。让我们在一个应用程序中使用所有形状来创建一个卡通形象。为此，创建一个名为 `Using2DShape` 的 WPF 应用程序（也可在 CD 中找到），并将清单 12.2 中给出的代码添加到 `MainWindow.xaml` 文件中：

**清单 12.2：在 WPF 中创建二维形状**
