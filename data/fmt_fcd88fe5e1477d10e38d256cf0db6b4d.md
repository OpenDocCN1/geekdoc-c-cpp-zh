
### 表 12.36：Timeline 类的属性

| 属性 | 描述 |
|---|---|
| `AccelerationRatio` | 获取或设置指定时间线持续时间的百分比，该百分比用于将时从零加速到其最大速率 |
| `AutoReverse` | 获取或设置一个值，该值指示时间线在完成一次正向迭代后是否以反向播放 |
| `BeginTime` | 获取或设置时间线应开始的时间 |
| `CanFreeze` | 检索指示对象是否可被设为不可修改的值 |

### 表 12.36：Timeline 类的属性

| 属性 | 描述 |
|---|---|
| `DecelerationRatio` | 获取或设置一个值，指定时间轴在其最大速率减速到零时花费的时间轴持续时间的百分比 |
| `DependencyObjectType` | 检索包装 `Timeline` 类的 CLR 类型的 |
| `Dispatcher` | 检索与 `DispatcherObject` 类关联的值 |
| `Duration` | 获取或设置时间轴播放的时间长度，不计重复 |
| `FillBehavior` | 获取或设置一个值，指定时间轴在其活动期结束后的行为 |
| `HasAnimatedProperties` | 检索一个值，指示是否有一个或多个 `AnimationClock` 对象与此对象的任何依赖属性关联 |
| `IsFrozen` | 检索一个值，指示对象当前是否可修改 |
| `IsSealed` | 检索一个值，声明 `Timeline` 类当前是否为只读 |
| `Name` | 获取或设置时间轴的名称 |
| `RepeatBehavior` | 获取或设置时间轴的重复行为 |
| `SpeedRatio` | 获取或设置时间相对于其父级进展的速率 |
| `DesiredFrameRate` | 获取或设置时间轴及其子时间轴的期望帧速率 |

`Timeline` 类的注目方法列于表 12.37：

### 表 12.37：Timeline 类的方法

| 方法 | 描述 |
|---|---|
| `Clone` | 创建 `Timeline` 对象的可修改克隆，复制对象值 |
| `CloneCurrentValue` | 创建 `Timeline` 对象的可修改克隆，复制对象当前值 |
| `CreateClock` | 从时间轴创建时钟 |
| `GetDesiredFrameRate` | 检索指定时间轴的期望帧速率 |
| `SetDesiredFrameRate` | 设置指定时间轴的期望帧速率 |

## 动画 Storyboard

`Storyboard` 是一个容器时间轴，它为其包含的时间轴提供目标信息。您可以使用 `Storyboard` 时间轴对多个动画进行分组，并且它具有控制动画播放的能力。例如，您可以暂停或停止动画，或更改动画的开始位置。`Storyboard` 类提供最基本的功能是其能够使用 `TargetName` 和 `TargetProperty` 属性指向特定属性和特定元素。因此，可以说 `Storyboard` 时间轴弥合了您的动画与您想要动画化的属性之间的差距。可控制的 `Storyboard` 时间轴可以暂停、恢复、停止、寻求，并且也可以在动画中被移除。要在 XAML 代码中使 `Storyboard` 时间轴可控制，您可以指定创建它的 `BeginStoryboard` 对象的 `Name` 属性。您也可以在代码中使 `Storyboard` 时间轴可控制，通过使用 `Storyboard.Begin()` 方法的适当重载并指定 `True` 使其可控制。您可以通过在应用程序中添加以下代码片段来添加 `Storyboard` 时间轴：

```
<Storyboard>
<!-- Children -->
</Storyboard>
```

`Storyboard` 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Animation.Timeline
            System.Windows.Media.Animation.TimelineGroup
              System.Windows.Media.Animation.ParallelTimeline
                System.Windows.Media.Animation.Storyboard
```

`Storyboard` 类的属性与 `Timeline` 类相同。与 `Timeline` 类不同的 `Storyboard` 类的注目属性列于表 12.38：

### 表 12.38：Storyboard 类的属性

| 属性 | 描述 |
|---|---|
| `SlipBehavior` | 获取或设置一个值，指定当一个或多个其时间轴子项滑落时此时间轴的行为 |

`Storyboard` 类的注目方法列于表 12.39：

### 表 12.39：Storyboard 类的方法

| 方法 | 描述 |
|---|---|
| `Begin` | 启动与 `Storyboard` 时间轴关联的动画集 |
| `Clone` | 创建 `Storyboard` 时间轴的可修改克隆 |
| `GetCurrentGlobalSpeed` | 检索为 `Storyboard` 时间轴创建的 `Clock` 类的 `CurrentGlobalSpeed` 对象 |
| `GetCurrentIteration` | 检索为 `Storyboard` 时间轴创建的 `Clock` 类的 `CurrentIteration` 对象 |
| `GetCurrentProgress` | 检索为 `Storyboard` 时间轴创建的 `Clock` 类的 `CurrentProgress` 对象 |
| `GetCurrentState` | 检索为 `Storyboard` 时间轴创建的 `Clock` 类的 `CurrentState` 对象 |
| `GetCurrentTime` | 检索为 `Storyboard` 时间轴创建的 `Clock` 类的 `CurrentTime` 对象 |
| `GetIsPaused` | 检索一个值，指示为 `Storyboard` 时间轴创建的 `Clock` 类是否已暂停 |
| `Pause` | 暂停为 `Storyboard` 时间轴创建的时钟 |
| `Resume` | 恢复与 `Storyboard` 时间轴实例关联的动画时钟或运行时状态 |
| `Seek` | 在下一次时钟滴答发生时将 `Storyboard` 时间轴寻求到新位置 |
| `SeekAlignedToLastTick` | 立即将 `Storyboard` 时间轴寻求到新位置 |
| `SetSpeedRatio` | 设置为 `Storyboard` 时间轴创建的 `Clock` 类的交互式速度比率 |
| `Stop` | 停止为 `Storyboard` 时间轴创建的 `Clock` 类 |

如果您使用代码将 `Storyboard` 对象添加到应用程序，您必须为 `FrameworkElement` 对象创建一个 `NameScope` 并使用该 `FrameworkElement` 注册要动画化对象的名称。要在 XAML 中启用对 `FrameworkElement` 对象的定位，您设置其 `Name` 属性。在应用程序的代码隐藏文件中，您需要使用 `RegisterName()` 方法将元素名称与您为其创建了 `NameScope` 的元素注册。

您可以在 `Storyboard` 时间轴启动后交互式地控制它。表 12.40 列出了您与事件触发器一起使用的 `Storyboard` 操作来控制 `Storyboard` 时间轴：

## WPF 4.0 中的多媒体

在本节中，您将学习 WPF 的多媒体功能。多媒体功能允许您将声音和视频集成到应用程序中以增强用户体验。WPF 包括对 Windows Media Player 支持的音频和视频文件的播放支持。它还允许您同时播放多个媒体文件。WPF 中多媒体最令人印象深刻的部分是它为您提供了将视频内容与 UI 其余部分集成的工具。例如，您可以将视频窗口放置在旋转的 3-D 立方体上。WPF 中的多媒体包括图像、音频和视频，它们是传达信息和用户体验的丰富方式。在本节中，您将学习关于：

- WPF 图像
- WPF 中的音频和视频

让我们详细讨论这些。

### WPF 图像

WPF 中的图像是大多数应用程序的核心部分。它们包括图标、背景，甚至动画的一部分。在 WPF 中，您可以显示、转换或格式化图像。WPF 成像旨在克服 GDI 的不足并提供一套新的应用程序编程接口（APIs）来在应用程序中显示和使用图像。您可以通过两种方式访问 WPF 成像 API，一个托管组件和一个非托管组件。托管 WPF 成像在 `System.Windows.Media.Imaging` 命名空间和 `System.Windows.Media` 命名空间中可用。托管组件利用非托管组件提供图像与其他 WPF 功能（如动画和图形）的集成。非托管组件在本地图像格式上提供改进的性能和安全性，这些格式包括位图（BMP）、联合图像专家组（JPEG）、便携式网络图形（PNG）、标记图像文件格式（TIFF）、Microsoft Windows Media Photo、图形交换格式（GIF）和图标（.ico）。

在 WPF 中，`Image` 类表示显示图像的控件。您可以使用 `Image` 控件加载 WPF 支持的所有图像类型。`Image` 控件的 `Stretch` 属性决定图像如何拉伸以填充图像元素。您可以通过添加以下代码片段将 `Image` 控件添加到应用程序：

```
<Image .../>
```

`Image` 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Image
```

`Image` 类的注目属性列于表 12.41：

### 表 12.41：Image 类的属性

| 属性 | 描述 |
|---|---|
| `Stretch` | 获取或设置一个值，描述 `Image` 对象应如何拉伸以填充目标矩形 |
| `Source` | 获取或设置图像的 `ImageSource` 对象 |

您可以从工具箱拖放 `Image` 控件并将其添加到 WPF 应用程序。添加到 WPF 应用程序的 `Image` 控件如图 12.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_570_0.png)

**图 12.1：显示图像控件**

可以看到，当您从工具箱中添加 `Image` 控件时，XAML 代码也会随之添加到应用程序中。现在让我们来了解 WPF 中使用的不同图像格式。

## BitmapSource 类

在 WPF 中，您使用编解码器来解码或编码特定的图像格式。WPF 包含以下图像类型的编解码器，如 BMP、JPEG、TIFF、PNG、Windows Media Photo、GIF 和 Icon。`BitmapSource` 类是一个抽象类，用于解码和编码图像。它可以执行以下两种功能之一：它可以是多帧图像的单个帧，也可以是对其执行变换的结果。它不用于表示多帧图像或动画。`BitmapSource` 类表示在特定大小和分辨率下的单一、恒定的像素集。`BitmapSource` 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.ImageSource
            System.Windows.Media.Imaging.BitmapSource
```

`BitmapSource` 类的重要属性列于表 12.42 中：

**表 12.42：BitmapSource 类的属性**

| 属性 | 描述 |
|---|---|
| `CanFreeze` | 检索一个值，该值指示对象是否可以被设为不可修改 |
| `DependencyObjectType` | 检索包装此实例的 CLR 类型的值 |
| `Dispatcher` | 检索通过与 `DispatcherObject` 对象关联而获取的值 |
| `DpiX` | 检索图像的水平每英寸点数 (dpi) |
| `DpiY` | 检索图像的垂直 dpi |
| `Format` | 检索位图数据的本机 `PixelFormat` 对象 |
| `HasAnimatedProperties` | 检索一个值，该值指示是否有多个 `AnimationClock` 对象与任何 `BitmapSource` 类依赖属性关联 |
| `Height` | 以设备无关单位检索源位图的高度 |
| `IsDownloading` | 检索一个值，该值指示 `BitmapSource` 内容当前是否正在下载 |
| `IsFrozen` | 检索一个值，该值指示对象当前是否可修改 |
| `IsSealed` | 检索一个值，该值声明 `BitmapSource` 类实例当前是否为只读 |
| `Metadata` | 检索与位图图像关联的元数据 |
| `Palette` | 检索位图的颜色调色板 |
| `PixelHeight` | 以像素为单位检索位图的高度 |
| `PixelWidth` | 以像素为单位检索位图的宽度 |
| `Width` | 以设备无关单位检索位图的宽度 |

`BitmapSource` 类的重要方法列于表 12.43 中：

**表 12.43：BitmapSource 类的方法**

| 方法 | 描述 |
|---|---|
| `Clone` | 创建 `BitmapSource` 对象的可修改克隆 |
| `CloneCurrentValue` | 创建 `BitmapSource` 对象的可修改克隆，并复制对象的当前值 |
| `Create` | 使用像素数组创建新的 `BitmapSource` 对象 |
| `CopyPixels` | 将像素数据复制到特定的矩形 |

`BitmapFrame` 类用于存储图像格式的实际位图数据。GIF 和 TIFF 等格式支持每幅图像多个帧，但某些图像格式仅支持单个 `BitmapFrame` 对象。

## 图像元数据

元数据描述文件的内容或特征。每幅图像都关联着不同的元数据，但 WPF 映像为每幅图像提供了一种统一存储和检索元数据的方式。您可以通过 `BitmapSource` 对象的 `Metadata` 属性访问图像的元数据。`Metadata` 属性返回一个 `BitmapMetadata` 对象，该对象包含图像包含的所有元数据信息。`BitmapMetadata` 对象可以是单个架构，也可以是架构的集合。WPF 映像支持的图像元数据架构包括可交换图像文件 (Exif)、tEXt（PNG 文本数据）、图像文件目录 (IFD)、国际新闻电信理事会 (IPTC) 和可扩展元数据平台 (XMP)。

如果 `BitmapMetadata` 对象由使用 `BitmapDecoder` 类获得的 `BitmapFrame` 对象公开，则默认情况下它是只读的。可变操作会引发异常。如果 `BitmapMetadata` 对象由包装另一个 `BitmapSource` 对象的 `BitmapFrame` 对象公开，则它在构造时是可变的。您可以使用 `GetQuery()` 和 `SetQuery()` 方法分别读取和构造元数据查询。

## 音频和视频

在本节中，您将学习 WPF 的另外两个领域：音频和视频。WPF 使您能够播放各种声音格式，包括 Windows Media Player 支持的任何格式。同样，WPF 还支持视频格式，包括运动图像专家组 (MPEG) 和 Windows Media Video (WMV) 文件。您还可以将音频和视频集成到 WPF 应用程序的其余部分中。例如，您可以将视频与 3-D 对象和动画结合使用。您可以在应用程序中集成音频和视频内容。WPF 使用 `MediaElement` 控件来播放视频和音频。

### MediaElement 和 MediaPlayer 类

在 WPF 中，`MediaElement` 和 `MediaPlayer` 类用于呈现音频、视频以及带音频内容的视频。`MediaElement` 类是一个 `UIElement`，可以作为许多控件的内容使用。它可以在 XAML 和代码中使用。`MediaPlayer` 类是为 Drawing 对象设计的。`MediaPlayer` 类不能在 XAML 中使用。您不能在 XAML 中声明 `MediaPlayer` 类的实例；您不能在不使用代码的情况下加载和播放媒体。要在 XAML 中播放媒体，您需要使用 `MediaElement` 控件。

`MediaPlayer` 类位于 `System.Windows.Media` 命名空间中。您需要创建一个 `MediaPlayer` 对象，然后调用 `Open` 方法加载音频文件，并调用 `Play()` 方法开始播放。使用 `MediaPlayer` 类播放的音频是异步播放的；没有同步播放的选项。`MediaPlayer` 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.MediaPlayer
```
