

# Path 微语言

要使用 Path 微语言，你需要控制 `Data` 属性。该属性包含一系列单字母缩写的绘图命令，命令之间穿插着决定绘制位置的点坐标。

图 8-2 显示了一个绘制 Path、Polygon（多边形）和 Polyline（折线）的程序，它们都使用了相同的点坐标数据。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_185_0.png)

下面的 XAML 代码显示了程序如何绘制其 Path。`Data` 属性包含了路径微语言中的系列命令。`M1,3` 命令将绘制位置移动到点 (4, 3)。`L` 后面跟着一系列坐标，绘制一系列连接的线。

```
<Path Margin="15" HorizontalAlignment="Center"
Alignment="Top" Width="Auto" Height="Auto"
Fill="#FF0000" Stroke="#F00000" StrokeThickness="5"
Data="M1,3 L2,70 78,32 31,59 64,41.3"/>
```

许多路径语言命令后面都跟着一个或多个作为参数的点。使用逗号或空格来分隔点，或点内部的坐标。为了使代码更易读，我使用逗号来分隔点的 X 和 Y 坐标，使用空格来分隔不同的点。

几个微语言命令有大写和小写两种版本。大写版本意味着随后的点是绝对坐标的，而小写版本意味着随后的点相对于上一个点。

下表描述了 Path 微语言的命令：

| 命令 | 含义 |
|--- |--- |
| F0 | 使用奇偶性填充规则（参见图 8-3）。 |
| F1 | 使用非零填充规则（参见图 8-3）。 |
| M 或 m | 移动到下一个点。 |
| L 或 l | 向下一个点绘制直线。 |
| H 或 h | 在给定的 X 坐标处绘制水平线。 |
| V 或 v | 在给定的 Y 坐标处绘制垂直线。 |
| C 或 c | 绘制三次贝塞尔曲线。此命令接受三个点作为参数：两个控制点和一个端点。曲线从当前点开始向第一个控制点移动，并在端点处远离第二个控制点的方向结束。（参见图 8-4。） |

# 命令 含义

S s 绘制平滑贝塞尔曲线。此命令接受两个点作为参数：一个控制点和一个端点。该曲线通过反射上一个 `s` 命令的最后一个控制点来定义一个初始控制点。它使用新定义的控制点和两个参数绘制三次贝塞尔曲线。这使得第二条曲线与前一个曲线平滑地衔接。（参见图 8-4。）

Q q 绘制二次贝塞尔曲线。此命令接受两个点作为参数：一个控制点和一个端点。曲线从当前点开始向控制点移动，并在端点处远离控制点的方向结束。（参见图 8-4。）

T t 绘制由单点定义的平滑贝塞尔曲线。此命令接受一个点作为参数，并并向该点绘制平滑曲线。它通过反射上一个 `T` 命令的控制点，以为新的曲线段定义一个控制点并绘制二次贝塞尔曲线。其结果是一条通过连续发送给 `T` 的点的平滑曲线。（参见图 8-4。）

+   A a 绘制从当前点开始并由五个参数定义的弧：
- size — 弧的 X 和 Y 半径
- rotation_angle — 椭圆旋转的角度（度为单位）
- large_angle — 如果弧跨越超过180度则为 0；如果跨越 180度或更多则为 1
- sweep_direction — 逆时针为 0；顺时针为 1
- end_point — 弧结束的点

Z z 通过从当前点到第一个点绘制一条直线来闭合图形。

图 8-3 显示了奇偶性规则和非零填充规则之间的区别。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_186_0.png)

图 8-4 中的 PathBezier 示例演示了 Path 微语言的贝塞尔曲线命令。程序用粗蓝线绘制每条曲线，然后在曲线上绘制黑色线段，连接到其控制点所在的位置。

# 包含对象的 Path

Path 微语言不是绘制 Path 对象的唯一方法。你不仅不使用微语言，还可以在 Path 对象内部放置其他对象来表示形状。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_186_1.png)

图 8-4

图 8-3

图 8-5 显示的 PathObjects 示例程序使用以下 XAML 代码绘制两条曲线。代码首先使用 Path 微语言绘制曲线，然后通过在 Path 控件内部放置对象来绘制相同的曲线。

```
<!-- 使用 Path 微语言绘制。 -->
<Path Stroke="Red" StrokeThickness="5">
<Path Data="60,20 Q140,150 150,140 0,30/100"/>

<!-- 使用对象绘制。 -->
<Path Stroke="Red" StrokeThickness="5">
<Path.Data>
  <Geometry>
  <FigureCollection>
    <PathFigure>
      <PathFigure StartPoint="60,20">
      <Segments>
      <PathSegmentCollection>
        <QuadraticBezierSegment Points="140,150 150,140 0,30/100"/>
      </PathSegmentCollection>
      </Segments>
    </PathFigure>
  </FigureCollection>
  </Geometry>
</Path.Data>
</Path.>
</Path>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_187_0.png)

两种方法产生相同的输出，但 Path 微语言要简单且简洁得多。

# POLYGON（多边形）

Polygon 对象绘制连接一系列点的线。它通过连接第一个点和最后一个点来完成绘制。

下面的 XAML 代码绘制了图 8-2 所示的多边形。末尾的 `Points` 属性包含了多边形的坐标。

```
<Polygon Margin="15" HorizontalAlignment="Center"
Alignment="Top" Width="Auto" Height="Auto"
Fill="#FF0000" Stroke="#F00000" StrokeThickness="5"
Data="M1,3 L2,70 78,32 31,59 64,41.3"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_187_1.png)

# Polyline（折线）

Polyline 对象绘制连接一系列点的线。与 Polygon 对象不同，它不会通过连接第一个点和最后一个点来完成绘制。

事实上，即使你在末尾重复该点，得到的结果也与 Polygon 对象不完全相同。

图 8-6 中的 PolygonPolylineDifference 示例程序绘制了一个多边形和一个折线。对于 Polyline 来说，第一条和最后一条线是相同的，因此它闭合了形状。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_188_0)

如果你观察图 8-6，你会发现左侧用 Polygon 绘制的点与右侧用 Polyline 绘制的点并不完全相同。Polyline 将此连接处视为角，因此它获得了一个完美的点。

图 8-6

下面的 XAML 代码显示了 PolylelineDifference 程序如何绘制其多边形和折线：

```
<StackPanel Orientation="Horizontal">
  <Polygon Margin="15,5,0,0"
           HorizontalAlignment="Center" VerticalAlignment="Top"
           Fill="Yellow" Stroke="Black" StrokeThickness="10"
           Points="50,100 100,100 100,100"/>
  <Label HorizontalAlignment="Center" Content="Polygon"/>
</StackPanel>
<StackPanel>
  <Polyline Margin="25,5,0,0"
           HorizontalAlignment="Center" VerticalAlignment="Top"
           Fill="Yellow" Stroke="Black" StrokeThickness="10"
           Points="50,100 100,100 150,100"/>
  <Label HorizontalAlignment="Center" Content="Polyline"/>
</StackPanel>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_188_1.png)

# RECTANGLE（矩形）

Rectangle 控件绘制一个不能包含任何子元素的简单矩形。控件的位置和布局与 Ellipse 类似。Rectangle的大小由其 Width 和 Height 属性决定，其位置由其容器以及其 Margin、HorizontalAlignment 和 VerticalAlignment 属性决定。

