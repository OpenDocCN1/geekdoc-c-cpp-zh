
```xml
<Window x:Class="Using2DShape.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="300" Width="300">
    <Canvas Background="LightBlue">
        <Ellipse Canvas.Left="86" Canvas.Top="41" Height="90" Name="ellipse1"
                 Stroke="Black" Width="96" Fill="AntiqueWhite" />
        <Ellipse Canvas.Left="105" Canvas.Top="62" Height="13" Name="ellipse2"
                 Stroke="Black" Width="14" Fill="Cornsilk" />
        <Ellipse Canvas.Left="144" Canvas.Top="62" Height="13" Name="ellipse3"
                 Stroke="Black" Width="14" Fill="Cornsilk" />
        <Ellipse Canvas.Left="112" Canvas.Top="68" Height="5" Name="ellipse4"
                 Stroke="Black" Width="5" Fill="Black" />
        <Ellipse Canvas.Left="151" Canvas.Top="67" Height="5" Name="ellipse5"
                 Stroke="Black" Width="5" Fill="Black" />
        <Rectangle Canvas.Left="105" Canvas.Top="129" Height="111" Name="rectangle1"
                   Stroke="Black" Width="59" Fill="HotPink" />
        <Ellipse Canvas.Left="127" Canvas.Top="128" Height="10" Name="ellipse6"
                 Stroke="Black" Width="9" Fill="Blue" />
        <Ellipse Canvas.Left="127" Canvas.Top="148" Height="10" Name="ellipse7"
                 Stroke="Black" Width="9" Fill="Blue" />
        <Ellipse Canvas.Left="127" Canvas.Top="168" Height="10" Name="ellipse8"
                 Stroke="Black" Width="9" Fill="Blue" />
        <Ellipse Canvas.Left="127" Canvas.Top="188" Height="10" Name="ellipse9"
                 Stroke="Black" Width="9" Fill="Blue" />
        <Ellipse Canvas.Left="127" Canvas.Top="208" Height="10" Name="ellipse10"
                 Stroke="Black" Width="9" Fill="Blue" />
        <Ellipse Canvas.Left="127" Canvas.Top="228" Height="10" Name="ellipse11"
                 Stroke="Black" Width="9" Fill="Blue" />
        <Line X1="12" X2="400" Y1="145" Y2="115" Stroke="Black" StrokeThickness="5" Height="158" Canvas.Left="131" Canvas.Top="114" Width="42" />
        <Path Name="path1" Stroke="Black" Data="M 60,113 Q 90,146 111,111" StrokeThickness="5" Height="134" Canvas.Left="48" Canvas.Top="-14" Width="145" />
        <Line X1="124" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="40" Canvas.Top="-7" Width="147" />
        <Line X1="145" X2="600" Y1="149" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="37" Canvas.Top="8" Width="178" />
        <Line X1="124" X2="170" Y1="145" Y2="16" Stroke="Black" StrokeThickness="5" Height="115" Canvas.Left="-42" Canvas.Top="65" Width="147" />
        <Line X1="115" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-50" Canvas.Top="11" Width="147" />
        <Polygon Points="10,110 60,10 110,110" Fill="Blue" Height="55" Canvas.Left="72" Canvas.Top="-7" Width="132" />
        <Line X1="11" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="163" Canvas.Left="83" Canvas.Top="110" Width="41" />
        <Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-23" Canvas.Top="94" Width="151" />
        <Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-1" Canvas.Top="94" Width="147" />
        <Line X1="11" X2="10" Y1="145" Y2="115" Stroke="Black" StrokeThickness="5" Height="158" Canvas.Left="121" Canvas.Top="-52" Width="42" />
        <Polyline Points="10,110 6,10 110,110" Stroke="Black" StrokeThickness="4" Height="52" Canvas.Left="209" Canvas.Top="210" Width="50"/>
        <Ellipse Canvas.Left="172" Canvas.Top="118" Height="100" Name="ellipse12" Stroke="Black" Width="87">
            <Ellipse.BitmapEffect>
                <OuterGlowBitmapEffect GlowColor="DarkViolet" />
            </Ellipse.BitmapEffect>
        </Ellipse>
    </Canvas>
</Window>
```

将代码添加到应用程序中即可创建一个卡通形象。你可以注意到，应用程序中使用了所有形状来创建该卡通形象。运行应用程序（按键盘上的 `F5` 键）时，你会得到如图 12.6 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_579_0.png)

## 创建可伸缩形状

WPF 中的所有形状都有一个 `Stretch` 属性，该属性决定 `Shape` 对象的内容如何拉伸以填充布局空间中的 `Shape` 对象。布局空间是指通过使用 `Height` 和 `Width` 属性分配给 `Shape` 对象的空间。`Stretch` 属性可以取以下值：

- `None`
- `Fill`
- `Uniform`
- `UniformToFill`

让我们创建一个带有 `Stretch` 属性的形状。为此，创建一个名为 `StretchableShape` 的 WPF 应用程序（也可在 CD 中找到），并将清单 12.3 中给出的代码添加到 `MainWindow.xaml` 文件中：

**清单 12.3：应用 `Stretch` 属性**

```xml
<Window x:Class="StretchableShape.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Grid>
        <StackPanel>
            <Polyline Fill="Pink" Points="100,100 100,200 200,200 200,100" Stroke="Red" StrokeThickness="5" Stretch="Fill"/>
            <Polyline Fill="LightBlue" Points="100,100 100,200 200,200 200,100" Stroke="Red" StrokeThickness="2" Stretch="Uniform" />
        </StackPanel>
    </Grid>
</Window>
```

在清单 12.3 中，添加了两个形状，并对两者应用了不同的 `Stretch` 属性。第一个形状的 `Stretch` 属性设置为 `Fill`，第二个形状的 `Stretch` 属性设置为 `Uniform`。当你运行应用程序（按键盘上的 `F5` 键）时，你会得到如图 12.7 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_580_0.png)

图 12.7：创建可伸缩形状

## 绘制几何图形

`Geometry` 类使您能够描述二维形状的几何结构。从 `Geometry` 类派生的类包括 `EllipseGeometry`、`PathGeometry` 和 `CombinedGeometry`。您可以使用几何图形创建简单形状，也可以通过组合两个几何图形创建复杂形状。让我们创建一个使用 `Geometry` 类的应用程序。为此，创建一个名为 `DrawingGeometry` 的 WPF 应用程序（也可在 CD 中找到），并将清单 12.4 中给出的代码添加到 `MainWindow.xaml` 文件中：

**清单 12.4：使用 `Geometry` 类**

```xml
<Window x:Class="DrawingGeometry.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Grid>
        <Path Stroke="Black" StrokeThickness="1" Fill="LightPink">
            <Path.Data>
                <GeometryGroup>
                    <EllipseGeometry Center="75,70" RadiusX="60" RadiusY="40" />
                    <RectangleGeometry Rect="25,55 100 25" />
                </GeometryGroup>
            </Path.Data>
        </Path>
    </Grid>
</Window>
```

```xml
</Path.Data>

</Path>

</Grid>

</window>
```

在前面的代码中，`EllipseGeometry` 类用于创建圆形，`RectangleGeometry` 类用于创建矩形。当你按下键盘上的 `F5` 键运行应用程序时，你会得到输出，如图 12.8 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_581_0.png)

图 12.8：绘制几何图形

## 组合多个几何图形

你可以使用 `CombinedGeometry` 类在 WPF 中组合多个几何图形。`GeometryCombineMode` 属性用于使用 `Exclude`、`Intersect`、`Union` 和 `Xor` 值来组合几何图形。让我们使用 `CombinedGeometry` 类组合本章“深入”部分中讨论的两个几何图形。为此，创建一个名为 `CombiningGeometry` 的 WPF 应用程序（可在 CD 上获得）并将 `Listing 12.5` 中的代码添加到 `MainWindow.xaml` 文件中：

### Listing 12.5: Showing the Use of the `CombinedGeometry` Class
