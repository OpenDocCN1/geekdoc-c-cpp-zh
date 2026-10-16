
| Shape Class | Description |
|---|---|
| Line | 你可以绘制一条从坐标 x1, y1 到 x2, y2 的直线。 |
| Rectangle | 通过为此类指定 Width 和 Height，你可以绘制矩形。 |
| Ellipse | 你可以绘制一个椭圆。 |
| Path | 你可以绘制一系列直线和曲线。Data 属性是 Geometry 类型。你可以使用从基类 Geometry 派生的类来进行绘制，也可以使用路径标记语法来定义几何图形。 |
| Polygon | 你可以绘制由连接线构成的封闭形状。多边形由分配给 Points 属性的一系列 Point 对象定义。 |
| Polyline | 与 Polygon 类类似，你可以使用 Polyline 绘制连接的线。区别在于折线不一定是封闭形状。 |

## 几何图形

前面的示例显示，其中一种形状 Path 使用 Geometry 进行绘制。你还可以在其他地方使用 Geometry 元素，例如与 DrawingBrush 一起使用。

从某些方面来看，几何元素与形状非常相似。就像有 Line、Ellipse 和 Rectangle 形状一样，这些图形也有对应的几何元素：LineGeometry、EllipseGeometry 和 RectangleGeometry。但形状和几何图形之间也存在很大差异。Shape 是一个 FrameworkElement，你可以将它用于任何支持将 UIElement 作为其子元素的类。FrameworkElement 派生自 UIElement。形状参与布局系统并自行渲染。Geometry 类不能自行渲染，并且与 Shape 相比，功能更少，开销也更低。在 WPF 中，Geometry 类派生自 Freezable 基类，可以在多个线程之间共享。在 UWP 应用中，Geometry 类直接派生自 DependencyObject。此处不能使用 Freezable。

Path 类使用 Geometry 进行绘制。可以通过 Path 的 Data 属性设置几何图形。可以设置的简单几何元素包括用于绘制椭圆的 EllipseGeometry、用于绘制直线的 LineGeometry 和用于绘制矩形的 RectangleGeometry。

## 使用线段创建几何图形

你还可以使用线段创建几何图形。几何图形类 PathGeometry 使用线段进行绘制。以下代码段使用 BezierSegment 和 LineSegment 元素构建一个红色图形和一个绿色图形，如图 30.3 所示。第一个 BezierSegment 在点 70,40（图形的起点）和 150,63 之间绘制一条贝塞尔曲线，控制点为 90,37 和 130,46。接下来的 LineSegment 使用贝塞尔曲线的终点，并绘制一条到 120,110 的直线（代码文件 Geometry [WPF | UWP] / Main [Window | Page].xaml）：

![](img/3d365b72b289213a91ade7eb366b8f35_1096_0.png)

### 图 30.3

```
<Path Canvas.Left="0" Canvas.Top="0" Fill="Red" Stroke="Blue" StrokeThickness="2.5">
    <Path.Data>
        <GeometryGroup>
            <PathGeometry>
                <PathGeometry.Figures>
                    <PathFigure StartPoint="70,40" IsClosed="True">
                        <PathFigure.Segments>
                            <BezierSegment Point1="90,37" Point2="130,46" Point3="150,63" />
                            <LineSegment Point="120,110" />
                            <BezierSegment Point1="100,95" Point2="70,90" Point3="45,91" />
                        </PathFigure.Segments>
                    </PathFigure>
                </PathGeometry.Figures>
            </PathGeometry>
        </GeometryGroup>
    </Path.Data>
</Path>

<Path Canvas.Left="0" Canvas.Top="0" Fill="Green" Stroke="Blue" StrokeThickness="2.5">
    <Path.Data>
        <GeometryGroup>
            <PathGeometry>
                <PathGeometry.Figures>
                    <PathFigure StartPoint="160,70">
                        <PathFigure.Segments>
                            <BezierSegment Point1="175,85" Point2="200,99" Point3="215,100" />
                            <LineSegment Point="195,148" />
                            <BezierSegment Point1="174,150" Point2="142,140" Point3="129,115" />
```

```
<LineSegment Point="160,70" />
</PathFigure.Segments>
</PathFigure>
</PathGeometry.Figures>
</PathGeometry>
</GeometryGroup>
</Path.Data>
</Path>
```

除了 BezierSegment 和 LineSegment 元素之外，你还可以使用 ArcSegment 在两点之间绘制椭圆弧。使用 PolyLineSegment 可以定义一组直线：PolyBezierSegment 由多条贝塞尔曲线组成，QuadraticBezierSegment 创建二次贝塞尔曲线，PolyQuadraticBezierSegment 由多条二次贝塞尔曲线组成。

## 使用 PML 创建几何图形

在本章前面，你已经看到了将 PML 用于 Path 形状的示例。使用 PML 时，WPF 会在后台使用 StreamGeometry 创建高速绘图。UWP 应用的 XAML 会创建图形和线段。以编程方式，你可以通过创建直线、贝塞尔曲线和弧线来定义图形。使用 XAML 时，你可以使用 PML 语法。你可以在 Path 类的 Data 属性中使用 PML。特殊字符定义点的连接方式。在以下示例中，M 标记起点，L 是绘制到指定点的直线命令，Z 是关闭图形的 Close 命令。图 30.4 显示了结果。路径标记语法还允许更多命令，例如水平线（H）、垂直线（V）、三次贝塞尔曲线（C）、二次贝塞尔曲线（Q）、平滑三次贝塞尔曲线（S）、平滑二次贝塞尔曲线（T）和椭圆弧（A）（代码文件 Geometry[WPF|UWP]/Main[Window|Page].xaml）：

![](img/3d365b72b289213a91ade7eb366b8f35_1098_0.png)

### 图 30.4

```
<Path Canvas.Left="0" Canvas.Top="200" Fill="Yellow"
Stroke="Blue"
    StrokeThickness="2.5"
    Data="M 120,5 L 128,80 L 220,50 L 160,130 L 190,220 L 100,150
        L 80,230 L 60,140 L0,110 L70,80 Z"
StrokeLineJoin="Round">
</Path>
```

## 组合几何图形（WPF）

WPF 为几何图形提供了另一个功能特性。使用 WPF，你可以使用 CombinedGeometry 类组合几何图形，如下一个示例所示。

CombinedGeometry 具有 Geometry1 和 Geometry2 属性，并允许使用 GeometryCombineMode 将它们组合为 Union、Intersect、Xor 和 Exclude。Union 合并两个几何图形。使用 Intersect 时，只有两个几何图形都覆盖的区域可见。Xor 与 Intersect 相反，它显示仅被其中一个几何图形覆盖的区域，而不显示被两者覆盖的区域。Exclude 显示第一个几何图形的区域减去第二个几何图形的区域。

以下示例（代码文件 GeometryWPF/MainWindow.xaml）

将 `EllipseGeometry` 和 `RectangleGeometry` 组合成一个联合，如图 30.5 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1099_0.png)

### 图 30.5

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

图 30.5 展示了此 XAML 代码的不同变体——从左到右依次为 `Union`、`Xor`、`Intersect` 和 `Exclude`。

## 变换

由于 XAML 基于矢量，你可以调整每个元素的大小。在下一个示例中，基于矢量的图形将进行缩放、旋转和倾斜。命中测试（例如，通过鼠标移动和鼠标单击）仍然有效，但无需手动计算位置。

图 30.6 以几种不同形式显示一个矩形。所有矩形都放置在水平方向的 `StackPanel` 元素中，使矩形并排排列。第一个矩形保持原始大小和布局。第二个被调整大小，第三个被移动，第四个被旋转，第五个被倾斜，第六个使用变换组进行变换，第七个使用矩阵进行变换。接下来的章节将详细介绍所有这些选项的代码示例。

![](img/3d365b72b289213a91ade7eb366b8f35_1099_1.png)

### 图 30.6

## 缩放

