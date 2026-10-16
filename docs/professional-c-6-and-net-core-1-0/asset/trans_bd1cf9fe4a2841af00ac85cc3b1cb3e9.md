

![](img/3d365b72b289213a91ade7eb366b8f35_1104_0.png)

## Figure 30.10

## SolidColorBrush

Figure 30.10 中的第一个按钮使用了 SolidColorBrush，其名称所示，使用纯色。整个区域都用相同的颜色绘制。

你只需将 Background 属性设置为定义纯色的字符串即可定义纯色。该字符串在 BrushValueSerializer 的帮助下被转换为 SolidColorBrush 元素（代码文件 Brushes [WPF|UWP]/Main [Window|Page].xaml）：

```
<Button Height="30" Background="#FFC9659C">Solid Color</Button>
```

当然，通过设置 Background 子元素并添加 SolidColorBrush 元素作为其内容，也能得到相同的效果（代码文件 BrushesDemo/MainWindow.xaml）。应用程序中的第一个按钮使用十六进制值作为纯色背景：

```
<Button Content="Solid Color" Margin="10">
<Button.Background>
<SolidColorBrush Color="#FFC9659C" />
</Button.Background>
</Button>
```

## LinearGradientBrush

为了实现平滑的颜色变化，你可以使用 LinearGradientBrush，如 Figure 30.10 中的第二个按钮所示。此画刷定义了 StartPoint 和 EndPoint 属性。通过此属性，你可以为线性渐变分配二维坐标。默认渐变是从 0,0 到 1,1 的对角线性渐变。通过定义不同的值，渐变可以采用不同的方向。例如，StartPoint 为 0,0 且 EndPoint 为 0,1 时，可得到垂直渐变。StartPoint 和 EndPoint 值为 1,0 时会创建水平渐变。

通过此画刷的内容，你可以使用 GradientStop 元素在指定偏移处定义颜色值。停止点之间颜色会被平滑过渡（代码文件 Brushes [WPF|UWP]/Main [Window|Page].xaml）：

```
<Button Content="Linear Gradient Brush" Margin="10">
<Button.Background>
<LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
<GradientStop Offset="0" Color="LightGreen" />
<GradientStop Offset="0.4" Color="Green" />
<GradientStop Offset="1" Color="DarkGreen" />
```
```
</LinearGradientBrush>
</Button.Background>
</Button>
```

## ImageBrush

要将图像加载到画刷中，可以使用 `ImageBrush` 元素。通过此元素，会显示由 `ImageSource` 属性定义的图像。图像可以从文件系统访问，也可以从程序集内的资源中访问。在代码示例中，图像是从文件系统添加的（代码文件

Brushes [WPF | UWP] / Main [Window | Page] .xaml )：

```
<Button Content="Image Brush" Width="100" Height="80" Margin="5" Foreground="White">
    <Button.Background>
        <ImageBrush ImageSource="Build2015.png" Opacity="0.5" />
    </Button.Background>
</Button>
```

## WebViewBrush

仅在 UWP 应用中可用的强大画刷是 `WebViewBrush`。此画刷使用 `WebView` 的内容作为画刷。

使用 `WebView` 控件时，可以使用随应用程序一起分发的本地 HTML 文件，使用 `ms-appx-web` 前缀，如示例代码所示（代码文件 BrushesUWP/MainPage.xaml）：

```
<WebView x:Name="webView1" Source="ms-appx-web:///HTML/HTMLBrushContent.html" LoadCompleted="OnWebViewCompleted" Width="100" Height="80" />
```

除了使用随应用程序分发的文件外，还可以访问 Internet 并使用 `http://` 检索 HTML 文件。当使用 `ms-appdata:///` 前缀时，可以使用本地文件系统中的文件。

`WebViewBrush` 通过 `SourceName` 属性引用 `WebView`：

```
<Button Content="WebView Brush" Width="300" Height="180" Margin="20">
    <Button.Background>
        <WebViewBrush x:Name="webViewBrush" SourceName="webView1" Opacity="0.5" />
    </Button.Background>
</Button>
```

`WebViewBrush` 在 XAML 加载时就会绘制。如果此时 `WebView` 尚未加载源，则需要重绘画刷。这就是为什么 `WebView` 定义了 `LoadCompleted` 事件的原因。通过与此事件关联的事件处理程序，通过调用 `Redraw` 方法重绘 `WebViewBrush`，并将 `WebView` 的 `Visibility` 属性设置为 `Collapsed`。如果 `WebView` 控件从一开始就被折叠，画刷将永远不会显示 HTML 内容（代码文件 BrushesUWP/MainPage.xaml.cs）：

```
private void OnWebViewCompleted(object sender,
NavigationEventArgs e)
{
    webViewBrush.Redraw();
    webView1.Visibility = Visibility.Collapsed;
}
```

## WPF-Only Brushes

上一节中介绍的 WebViewBrush 仅在 UWP 应用中可用，但现在我们将转向仅在 WPF 中可用的画刷类别。以下各节中描述的所有画刷只能与 WPF 一起使用。Figure 30.11 显示了仅限 WPF 的画刷 RadialGradientBrush、DrawingBrush 和 VisualBrush（两次）。让我们从 RadialGradientBrush 开始。

![](img/3d365b72b289213a91ade7eb366b8f35_1106_0.png)

![](img/3d365b72b289213a91ade7eb366b8f35_1106_1.png)

![](img/3d365b72b289213a91ade7eb366b8f35_1106_2.png)

![](img/3d365b72b289213a91ade7eb366b8f35_1106_3.png)

Figure 30.11

## RadialGradientBrush

RadialGradientBrush 与 LinearGradientBrush 相似之处在于你可以为渐变外观定义一系列颜色。使用 RadialGradientBrush 可以以径向方式平滑颜色。在 Figure 30.11 中，最左边的元素是一个使用 RadialGradientBrush 的 Path。此画刷使用 GradientOrigin 点定义颜色起点（代码文件 BrushesWPF/MainWindow.xaml）：

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

## DrawingBrush

DrawingBrush 使你能够定义一个使用画刷创建的绘图。Figure 30.11 中 Content 值为 Drawing Brush 的按钮使用 DrawingBrush 定义背景。此画刷使用 GeometryDrawing 元素。GeometryDrawing 又使用两个 SolidColorBrush 元素：一个红色，一个蓝色。红色画刷用作背景，蓝色画刷用作画笔，从而在几何元素周围产生描边。GeometryDrawing 的内容由 PathGeometry 定义，该几何在本书本章的“Geometry”部分中已讨论过（代码文件 BrushesWPF/MainWindow.xaml）：

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
                    <GeometryDrawing.Geometry>
                        <PathGeometry>
                            <PathGeometry.Figures>
                                <PathFigure StartPoint="70,40">
                                    <PathFigure.Segments>
                                        <BezierSegment Point1="90,37" Point2="130,46" Point3="150,63" />
                                        <LineSegment Point="120,110" />
                                        <BezierSegment Point1="100,95" Point2="70,90" Point3="45,91" />
                                        <LineSegment Point="70,40" />
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

## VisualBrush

VisualBrush 使你能够在画刷中使用其他 XAML 元素。以下示例（代码文件 BrushesWPF/MainWindow.xaml）将包含 Rectangle 和 Button 元素的 StackPanel 添加到 Visual 属性。Figure 30.11 中从左数第三个元素包含一个 Rectangle 和一个 Button：

```
<Button Content="Visual Brush" Width="100" Height="80">
```

