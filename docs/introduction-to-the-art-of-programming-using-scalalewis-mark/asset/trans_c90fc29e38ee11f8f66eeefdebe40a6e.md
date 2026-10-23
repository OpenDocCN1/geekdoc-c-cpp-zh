

## 第12章
## 图形

- 12.1 自定义绘制面板 ................................................... 284
- 12.2 java.awt.Graphics2D ................................................... 284
- 12.2.1 形状 .............................................................. 285
- 12.2.2 设置 ............................................................. 287
- 12.2.2.1 填充 ............................................................. 287
- 12.2.2.2 笔触 ............................................................ 290
- 12.2.2.3 字体 .............................................................. 292
- 12.2.2.4 裁剪 .............................................................. 294
- 12.2.2.5 变换 ....................................................... 294
- 12.2.3 仿射变换 .................................................. 294
- 12.3 图像 ............................................................... 297
- 12.3.1 BufferedImage ...................................................... 297
- 12.3.2 读取和写入图像 ....................................... 298
- 12.3.3 双缓冲 .................................................. 298
- 12.3.4 重新审视 TexturePaint ........................................... 299
- 12.4 其他事件 ........................................................ 299
- 12.4.1 鼠标事件 ...................................................... 301
- 12.4.2 键盘事件 ................................................... 302
- 12.5 使用 Timer 的动画 ............................................... 303
- 12.6 综合应用 ................................................ 304
- 12.7 本章结束材料 ............................................ 307
- 12.7.1 概念总结 .............................................. 307
- 12.7.2 练习 ......................................................... 309
- 12.7.3 项目 .......................................................... 309

并非所有你可能想放入图形用户界面 GUI 中的内容都是标准 GUI 库的一部分。它们只添加了使用频率相当高的元素。也有时候你想要在 GUI 中显示自己的图形，完全独特于你的程序。在这种情况下，你必须能够编写图形代码。

Scala 没有自己的图形库。这是因为 Java 中的图形库相当完整，并且在 Scala 风格下使用良好。我们将使用的 Java 图形功能统称为 Java2D，因为它们是 Java 中的 2D 图形库。我们将使用的类型主要位于三个不同的包中：java.awt、java.awt.geom 和 java.awt.image。

### 12.1 自定义绘制面板

要在 GUI 中添加自己的图形，你需要创建一个在屏幕上显示时绘制你想要内容的面板。实现方法是创建一个新的面板，然后改变它绘制到屏幕的方式。Panel 类型中有一个名为 paint 的方法，它接收一个类型为 java.awt.Graphics2D 的单个参数。我们希望在我们的面板中替换此方法。改变方法行为的动作称为覆盖，我们将使用 override 关键字来实现。语法如下所示。

```
val panel=new Panel {
  override def paint(g:Graphics2D) {
    // Draw to g
  }
}
```

如果你在代码中尝试此操作，请确保导入 java.awt.Graphics2D，这样它就知道在哪里找到该类型。

然后可以将此面板以与将任何其他面板添加到 GUI 相同的方式添加到 GUI。对于本章，我们将简单地让我们的自定义绘制面板成为 Frame 的全部内容。

### 12.2 `java.awt.Graphics2D`

Java2D 库的主要功能是通过 java.awt 包中的 Graphics2D 类访问的。此类有许多不同的方法，我们可以将其分为不同的组。这里列出了其中一些。要查看全部内容，你需要查阅 Java API。

- 绘制/填充方法
  - `draw(s:Shape)`
  - `drawLine(x1:Int, y1:Int, x2:Int, y2:Int)`
  - `drawRect(x:Int, y:Int, width:Int, height:Int)`
  - `drawImage(img:RenderedImage, x:Int, y:Int, obs:ImageObserver)`
  - `drawImage(img:RenderedImage, x:Int, y:Int, width:Int, height:Int, obs:ImageObserver)`
  - `drawRenderedImage(img:RenderedImage, trans:AffineTransform)`
  - `drawString(str:String, x:Int, y:Int)`
  - `fill(s:Shape)`
  - `fillRect(x:Int, y:Int, width:Int, height:Int)`

- 设置方法
  - `setPaint(paint:Paint)`
  - `setStroke(stroke:Stroke)`
  - `setTransform(trans:Transform)`
  - `setFont(font:Font)`
  - `setClip(clip:Shape)`

- 获取方法
  - `getPaint:Paint`
  - `getStroke:Stroke`
  - `getTransform:Transform`
  - `getFont:Font`
  - `getClip:Shape`

- 其他方法
  - `rotate(theta:Double)`
  - `rotate(theta:Double, x:Double, y:Double)`
  - `scale(sx:Double, sy:Double)`
  - `shear(shx:Double, shy:Double)`
  - `translate(tx:Double, ty:Double)`

`draw` 和 `fill` 方法实际执行绘制。`set` 方法改变绘制方式，而 `get` 方法让我们查询当前设置。其他方法也影响绘制方式。

为了说明其工作原理，我们可以用一行最简单的绘制代码替换 `paint` 方法中的注释。

```
g.fillRect(20,20,200,200)
```

此行绘制一个矩形，其左上角位于左边缘右侧 20 像素、顶部下方 20 像素处。¹ 它还具有 200 像素的宽度和高度。添加此行的结果如图 12.1 所示。

你也可以对 `drawLine` 和 `drawRect` 进行类似调用。这些通过传入坐标调用的方法是早于 Java2D 的 Java 图形库的一部分。虽然它们使用简单，但缺乏灵活性和功能。

### 12.2.1 形状

Java2D 库通过提供接受 `Shape` 的 `fill` 方法增加了显著的抽象层次。这个方法非常强大，但在本章中我们只会看到其中一小部分功能。为了使用此方法或密切相关的 `draw` 方法，我们必须能够创建 `Shape` 类型的对象。`java.awt.Rectangle` 类型是一个 `Shape`。此外，大多数 `java.awt.geom` 包都致力于为你提供不同类型的 Shapes。以下是你可以选择的几种类型以及如何创建它们。如果你打算使用这些类型，你可能希望在代码中加入 `import java.awt.geom.*`。

> ¹ 术语 PIXEL 是 “picture element” 的缩写。它指的是图像中的一个点。这些点通常排列成称为光栅的网格。它们的大小取决于你使用的设备的分辨率。

![](img/157fcf510c119278e4b1267c62717fa8_321_0.png)

图 12.1：在 paint 内部执行简单的 fillRect 的结果。

- **Arc2D** – 这是一个椭圆弧。它可以创建为开放弧，也可以闭合为饼状切片或使用弦。可以使用 new Arc2D.Double(x:Double, y:Double, w:Double, h:Double, start:Double, extent:Double, type:Int) 创建。type 可以是 Arc2D.OPEN、Arc2D.CHORD 或 Arc2D.PIE。
- **Area** – 这是一种非常通用的形状类型，你可以从任何其他 Shape 使用 new Area(s:Shape) 初始创建。此类型的强大之处在于你拥有 add、intersect 和 subtract 等方法，可以组合区域以创建任意复杂的形状。
- **CubicCurve2D** – 制作一个由 x、y 和 z 中的三次多项式描述的曲线。你可以通过调用 new CubicCurve2D.Double(x1:Double, y1:Double, ctrlx1:Double, ctrly1:Double, ctrlx2:Double, ctrly2:Double, x2:Double, y2:Double) 创建此曲线。
- **Ellipse2D** – 一个椭圆，你可以使用 new Ellipse2D.Double(x:Double, y:Double, w:Double, h:Double) 创建。指定的 x 和 y 位置是椭圆边界矩形的左上角。
- **Line2D** – 一条线，你可以使用 new Line2D.Double(x1:Double, y1:Double, x2:Double, y2:Double) 或 new Line2D.Double(p1:Point2D, p2:Point2D) 创建。
- **Path2D** – 一个在 2D 空间中的通用路径，你可以将其构建为空或使用一个

