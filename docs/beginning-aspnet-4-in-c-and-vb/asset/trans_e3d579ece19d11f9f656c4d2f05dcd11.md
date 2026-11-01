
## 几何图形

其中一个形状 Path 使用 Geometry 进行绘制。几何元素也可以在其他地方使用，例如与 DrawingBrush 配合使用。

几何元素与形状非常相似。正如存在 Line、Ellipse 和 Rectangle 形状一样，这些绘图也有对应的几何元素：LineGeometry、EllipseGeometry 和 RectangleGeometry。形状和几何图形之间存在很大差异。Shape 是一个 FrameworkElement，可以与任何支持 UIElement 作为子元素的类一起使用。FrameworkElement 派生自 UIElement。形状参与布局系统并自行渲染。Geometry 类不能自行渲染，并且比 Shape 具有更少的功能和更低的开销。Geometry 类派生自 Freezable 基类，可以从多个线程共享。

Path 类使用 Geometry 进行绘制。几何图形可以通过 Path 的 Data 属性设置。可以设置的简单几何元素有用于绘制椭圆的 EllipseGeometry、用于绘制线的 LineGeometry 以及用于绘制矩形的 RectangleGeometry。如下一个示例所示，可以使用 CombinedGeometry 来组合多个几何图形。

CombinedGeometry 具有 Geometry1 和 Geometry2 属性，并允许它们通过 GeometryCombineMode 组合形成 Union、Intersect、Xor 和 Exclude。Union 合并两个几何图形。使用 Intersect 时，只有同时被两个几何图形覆盖的区域可见。Xor 与 Intersect 相反，显示由其中一个几何图形覆盖的区域，但不显示同时被两个覆盖的区域。Exclude 显示第一个几何图形的区域减去第二个几何图形的区域。

以下示例将 EllipseGeometry 和 RectangleGeometry 组合形成联合，如图 35-4 所示。

```
<Path Canvas.Top="0" Canvas.Left="250" Fill="Blue" Stroke="Black" >
  <Path.Data>
    <CombinedGeometry GeometryCombineMode="Union">
      <CombinedGeometry.Geometry1>
        <EllipseGeometry Center="80,60" RadiusX="80" RadiusY="40" />
      </CombinedGeometry.Geometry1>
      <CombinedGeometry.Geometry2>
        <RectangleGeometry Rect="30,60 105 50" />
      </CombinedGeometry.Geometry2>
    </CombinedGeometry>
  </Path.Data>
</Path>
```

代码片段 GeometryDemo/MainWindow.xaml

![](img/d7d2ffa0a76feaab821930e95daace93_1049_0.png)

几何图形也可以通过使用段来创建。几何类 PathGeometry 使用段进行绘制。以下代码段使用 BezierSegment 和 LineSegment 元素构建一个红色和一个绿色图形，如图 35-5 所示。第一个 BezierSegment 在点 70,40（即图形的起点）和 150,63 之间绘制一条贝塞尔曲线，控制点为 90,37 和 130,46。之后的 LineSegment 使用贝塞尔曲线的终点并绘制一条线到 120,110：

```
<Path Canvas.Left="0" Canvas.Top="0" Fill="Red" Stroke="Blue" StrokeThickness="2.5">
  <Path.Data>
    <GeometryGroup>
      <PathGeometry>
        <PathGeometry.Figures>
          <PathFigure StartPoint="70,40" IsClosed="True">
            <PathFigure.Segments>
              <BezierSegment Point1="90,37" Point2="130,46" />
```

```
<GradientStop Offset="0" Color="LightGreen" />
<GradientStop Offset="0.4" Color="Green" />
<GradientStop Offset="1" Color="DarkGreen" />
</LinearGradientBrush>
</Button.Background>
```

## 径向渐变画刷

使用 RadialGradientBrush 可以以辐射方式平滑颜色。在图 35-8 中，第三个元素是一个使用 RadialGradientBrush 的 Path。该画刷使用 GradientOrigin 点定义颜色起点：

```
<Canvas Width="200" Height="150">
  <Path Canvas.Top="0" Canvas.Left="20" Stroke="Black" >
    <Path.Fill>
      <RadialGradientBrush GradientOrigin="0.2,0.2">
        <GradientStop Offset="0" Color="LightBlue" />
        <GradientStop Offset="0.6" Color="Blue" />
        <GradientStop Offset="1.0" Color="DarkBlue" />
      </RadialGradientBrush>
    </Path.Fill>
    <Path.Data>
      <CombinedGeometry GeometryCombineMode="Union">
        <CombinedGeometry.Geometry1>
          <EllipseGeometry Center="80,60" RadiusX="80" RadiusY="40" />
        </CombinedGeometry.Geometry1>
        <CombinedGeometry.Geometry2>
          <RectangleGeometry Rect="30,60 105 50" />
        </CombinedGeometry.Geometry2>
      </CombinedGeometry>
    </Path.Data>
  </Path>
</Canvas>
```

## 绘图画刷

DrawingBrush 允许您定义一个使用画刷绘制的绘图。使用画刷显示的绘图在 GeometryDrawing 元素内定义。您可以在 Geometry 属性中看到的 GeometryGroup 由本章前面讨论过的 Geometry 元素组成：

```
<Button Content="Drawing Brush" Margin="10" Padding="10">
  <Button.Background>
    <DrawingBrush>
      <DrawingBrush.Drawing>
        <GeometryDrawing Brush="Red">
          <GeometryDrawing.Pen>
            <Pen>
              <Pen.Brush>
                <SolidColorBrush>Blue</SolidColorBrush>
              </Pen.Brush>
            </Pen>
          </GeometryDrawing.Pen>
        </GeometryDrawing>
        <GeometryDrawing.Geometry>
          <PathGeometry>
            <PathGeometry.Figures>
              <PathFigure StartPoint="70,40">
                <PathFigure.Segments>
```

```
<BezierSegment Point1="90,37" Point2="130,46" Point3="150,63" />
<LineSegment Point1="120,110" />
<BezierSegment Point1="120,100" Point2="70,90" Point3="45,91" />
<LineSegment Point1="70,40" />
</PathFigure.Segments>
</PathFigure>
</PathGeometry.Figures>
</PathGeometry>
</GeometryDrawing.Geometry>
</GeometryDrawing>
</DrawingBrush.Drawing>
</DrawingBrush>
</Button.Background>
</Button>
```

## 图像画刷

要将图像加载到画刷中，可以使用 ImageBrush 元素。使用此元素，将显示 ImageSource 属性定义的图像。图像可以从文件系统访问，也可以从程序集内的资源访问。在示例中，图像作为资源添加到程序集中，并使用程序集和资源名称引用：

```
<Button Content="Image Brush" Width="100" Height="80" Margin="5"
Foreground="White">
<Button.Background>
<ImageBrush ImageSource="/BrushesDemo;component/Budapest.jpg" />
</Button.Background>
</Button>
```

## 可视画刷

VisualBrush 允许您在画刷中使用其他 WPF 元素。在这里，您可以将 WPF 元素添加到 Visual 属性。图 35-8 中的第六个元素包含一个 Rectangle 和一个 Button：

```
<Button Content="Visual Brush" Width="100" Height="80">
<Button.Background>
<VisualBrush>
<VisualBrush.Visual>
<StackPanel Background="White">
<Rectangle Width="25" Height="25" Fill="Blue" />
<Button Content="Drawing Button" Background="Red" />
</StackPanel>
</VisualBrush.Visual>
</VisualBrush>
</Button.Background>
</Button>
```

您可以将任何 UIElement 添加到 VisualBrush。一个例子是您可以使用 MediaElement 播放视频：

```
<Button Content="Visual Brush with Media" Width="200" Height="150"
Foreground="White">
<VisualBrush>
<VisualBrush.Visual>
<MediaElement Source="./Stephanie.wmv" />
</VisualBrush.Visual>
</VisualBrush>
</Button.Background>
</Button>
```

| 简单控件 | 描述 |
|---|---|
| PasswordBox | 此控件用于输入密码，并具有用于密码输入的特定属性，例如 PasswordChar，用于定义用户输入密码时应显示的字符，或 Password 用于访问输入的密码。密码更改后会立即调用 PasswordChanged 事件。 |
| ScrollBar | 此控件包含一个 Thumb，用户可以在其中选择值。例如，如果文档不适合屏幕，则可以使用滚动条。某些控件包含滚动条，当内容过大时滚动条会显示。 |
| ProgressBar | 使用此控件，您可以指示长时间操作的进度。 |
| Slider | 使用此控件，用户可以通过移动 Thumb 选择一系列值。ScrollBar、ProgressBar 和 Slider 派生自同一个基类 RangeBase。 |
| TextBox | 用于显示简单、无格式的文本。 |
| RichTextBox | 在 FlowDocument 类的帮助下支持富文本。RichTextBox 和 TextBox 派生自同一个基类 TextBoxBase。 |
| Calendar | Calendar 控件在 .NET 4 中新增——它显示月份、年份或十年。用户可以选择日期或日期范围。 |
| DatePicker | DatePicker 是一个控件，可在屏幕上打开 Calendar 以供用户选择日期。 |

> 尽管简单控件没有 Content 属性，但您可以通过定义模板完全自定义控件的外观。模板将在本章后面讨论。

## 内容控件

ContentControl 具有 Content 属性，可通过该属性向控件添加任何内容。Button 类派生自基类 ContentControl，因此您可以向此控件添加任何内容。在之前的示例中，您看到了 Button 内的 Canvas 控件。内容控件在下表中描述。

| 内容控件控件 | 描述 |
|---|---|
| Button<br>RepeatButton<br>ToggleButton<br>CheckBoxRadioButton | 类 Button、RepeatButton、ToggleButton 和 GridViewColumnHeader 派生自同一个基类 ButtonBase。所有按钮都对 Click 事件做出反应。RepeatButton 会在按钮释放前重复触发 Click 事件。ToggleButton 是 CheckBox 和 RadioButton 的基类。这些按钮具有开和关状态。CheckBox 可以由用户选中和清除；RadioButton 可以由用户选中。清除 RadioButton 必须以编程方式完成。 |
| Label | Label 类表示控件的文本标签。此类还支持访问键，例如菜单命令。 |
| Frame | Frame 控件支持导航。您可以使用 Navigate() 方法导航到页面内容。如果内容是 Web 页面，则使用 Web 浏览器控件进行显示。 |
| ListBoxItem | ListBoxItem 是 ListBox 控件中的一个项。 |
| StatusBarItem | StatusBarItem 是 StatusBar 控件中的一个项。 |
| ScrollViewer | ScrollViewer 控件是一个包含滚动条的内容控件。您可以将任何内容放入此控件；滚动条会根据需要显示。 |
| ToolTip | ToolTip 创建一个弹出窗口以显示控件的附加信息。 |

