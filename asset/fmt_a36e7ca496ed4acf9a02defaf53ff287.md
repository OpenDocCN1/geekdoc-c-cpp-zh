
```scala
import scalafx.Includes._
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.image.{Image, ImageView, WritableImage, PixelWriter}
import scalafx.scene.control.Label
import scalafx.scene.layout.TilePane
import scalafx.scene.paint.Color

if (args.length < 1) {
  println("You must provide an argument with the name of a file to load.")
  sys.exit(0)
}

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    scene = new Scene(800,200) {
      val original = Image("file:"+args(0), 200, 200, true)
      val (red, green, blue) = original.match {
        case Some(reader) =>
          val rim = new WritableImage(original.width.value.toInt, original.height.value.toInt)
          val writer = rim.pixelWriter
          val gimg = new WritableImage(original.width.value.toInt, original.height.value.toInt)
          val gwriter = gimg.pixelWriter
          val bimg = new WritableImage(original.width.value.toInt, original.height.value.toInt)
          val bwriter = bimg.pixelWriter
          for (i <- 0 until original.width.value.toInt) {
            for (j <- 0 until original.height.value.toInt) {
              val c = reader.getColor(i, j)
              writer.setColor(i, j, Color(c.red, 0, 0, 1.0))
              writer.setColor(i, j, Color(0, c.green, 0, 1.0))
              writer.setColor(i, j, Color(0, 0, c.blue, 1.0))
            }
          }
          (new ImageView(rim), new ImageView(gimg), new ImageView(bimg))
        case None =>
          (new Label("No Reader"), new Label("No Reader"), new Label("No Reader"))
      }
      val tilePane = new TilePane
      tilePane.children = List(new ImageView(original), red, green, blue)
      root = tilePane
    }
  }
}
app.main(args)
```

该程序的可能输出可见图 12.5。值得注意的是，你可以使用代码 `Button(text: String, graphic: Node)` 并提供适当的图形 `ImageView` 将图像放置到按钮上。

## 12.3.1 将图像写入文件

虽然 JavaFX（因此 ScalaFX）支持许多功能，但有一项重要的功能它们并没有添加：将图像写入文件。为了实现这一点，我们必须通过一些旧的基于 JavaFX 的库。JavaFX 中读写图像的功能由 `java.image.ImageIO` 类型提供。该类型有一个名为 `write` 的方法，可以从旧库中的 `BufferedImage` 创建图像文件，挑战在于 `ImageIO` 使用的是 `BufferedImage`。幸运的是，有方法可以使用 `scalafx.embed.swing.SwingFXUtils` 对象将我们使用的 `Image` 类型转换为 `BufferedImage`。以下行代码会将名为 `out` 的 `Image` 写入由 `java.io.File` 指定名为 `file` 的 PNG 文件。

```java
ImageIO.write(SwingFXUtils.fromImage(img, null), "png", file)
```

你可能会发现你想将整个 `Scene` 或特定的 `Node` 保存为文件。

## 图形与高级 ScalaFX

![](img/06d4e84f27a8884ea40ba6182ec7c778_373_0.png)

**图 12.5：** 运行 `ImageView.scala` 配合示例图像生成的窗口。

# 使用 Scala 进行编程与问题解决介绍

接受 `PixelReader` 的两个版本会为 `PixelReader` 挂载的图像创建一个副本，并可能带有偏移量和不同的缩放比例。最后一个版本创建一个指定宽度和高度的空白透明图像。

一旦你拥有了 `WritableImage`，就可以调用 `PixelWriter` 方法来获取一个 `PixelWriter`。`PixelWriter` 中有三个方法对我们这里很重要。在这里我们使用 `setArg(x: Int, y: Int, argB: Int, unit: Int)`、`setColor(x: Int, y: Int, color: Color)` 以及 `setPixels(dstX: Int, dstY: Int, src: Int, w: Int, h: Int, reader: PixelReader, src: Scene)`。`PixelWriter` 中的两个并行方法可以将图像中的单个像素设置为特定的 RGB 值或特定颜色。最后一个方法在由第一个参数定义的位置和大小设置一个矩形像素区域，并使用来自 `PixelReader` 中指定位置的值。

为了说明这些不同类型的用法，以下示例使用了在命令行指定的图像，并将其缩放为宽度仅为 200 像素。它尝试获取该图像的 `PixelReader`。如果可以，它将创建 `WritableImages` 及其关联的 `PixelWriter`，并将红、绿、蓝分量复制到这些图像中。然后它们被放入视图并存储在变量 `red`、`green` 和 `blue` 中。如果无法获取读取器，这些变量简单地获取为相应的标签。随后所有四幅图像都被添加到 `TilePane` 中。

## 12.4 变换

几乎所有图形界面的基本能力之一都是变换形状的能力。你可以在下面的列表中看到这种示例：

- `rotate`（旋转）：围绕某个点旋转对象。
- `translate`（平移）：按特定距离移动对象。
- `scale`（缩放）：改变对象的大小。
- `shear`（倾切）：倾斜对象。

应用这些变换的最常见方法是使用 `Transform` 类。这些变换在计算机中使用仿射矩阵表示。仿射变换是线性变换后的平移。这包括旋转、缩放和剪切，它们都是相对于原点进行的。

# 使用 Scala 进行编程与问题解决简介

![](img/06d4e84f27a8884ea40ba6182ec7c778_376_0.png)

图 12.6：运行 `SimpleTransforms.scala` 产生的窗口。

```scala
val lines4 = makeParallelLines
lines4.transforms = List(Transform.translate(300,300),
    Transform.shear(0.1,0.2))

content = List(lines1, lines2, lines3, lines4)
```

`app.main(args)`

这段代码的输出如图 12.6 所示。
此示例展示了我们之前未见过的另一种用法，即在场景图（scene graph）中结合“组（Groups）”与“节点（Nodes）”使用。平行线是 `Line` 对象，我们希望为每个对象提供相同的变换。这通过将两条线放入一个组中，对该组应用变换，并将该组添加到场景（Scene）中来实现。你还可以将组嵌套在组内部，以创建更复杂的结构。这种能力我们称之为 ScalaFX 使用了场景图，如果你打算使用 Scalafx 中的几何类型构建更复杂的图形，就应该利用这一特性。

# 12.5 动画

到为止，GUI 中发生的任何变化都必须完全由用户用户程序的交互驱动。也就是说，当用户点击鼠标或按下按键时，我们可以更改 GUI 的某些方面。考虑 `DrawMaze.scala` 示例，鼠标导致线条的绘制，按键导致圆形的移动。在用户交互之间发生，或者可能在用户不进行任何操作的情况下发生，对于许多类型的应用程序至关重要。这就是动画的领域。ScalFX 提供了一个动画包，其中包含许多有助于创建动画的类型，包括 `Animation`。`Animation` 有两个子类型，称为 `Transition` 和 `Timeline`，可用于产生不同类型的动画。还有一个 `AnimationTimer`，它允许你在应用程序中以固定的间隔执行任何想要的操作。这三种方法将在接下来的小节中介绍。

`Animation` 类型提供了许多实用的成员和方法，这些方法适用于 `Transitions` 和 `Timeline`。以下是其中部分的列表：

- `autoReverse`: 这是一个 `BooleanProperty`，用于告知动画在到达末尾时应反向。
- `currentRate`: 这是一个 `ReadOnlyDoubleProperty`，告知动画播放的当前方向和速度。
- `currentTime`: 这是一个 `ReadOnlyProperty[Duration]`，告知动画播放的当前位置。使用 `scalafx.util.Duration` 类型表示时间长度，将在下文更详细地介绍。
- `cycleCount`: 一个 `IntegerProperty` 定义了动画应该循环的次数。
- `cycleDuration`: 一个 `ReadOnlyProperty[Duration]` 给出了运行整个动画需要多长时间。
- `delay`: 这个 `ObjectProperty[Duration]` 可用于获取或设置动画开始之前的延迟。
- `jumpTo(cuePoint: String)` - 跳跃到动画中预定义的位置。
- `jumpTo(time: Duration)` - 跳跃到动画中指定的时间点。
- `onFinished` - 此 `EventHandler` 可以赋予一段在动画结束时应该执行的代码。你可以用它来安排后续动画。
- `pause()` - 暂停动画的播放。
- `play()` - 导致动画开始播放。
- `playFrom(cuePoint: String)` - 从预定义点开始播放动画。
- `playFrom(time: Duration)` - 从指定时间开始播放动画。
- `playStart()` - 从动画开头开始播放。
- `rate` - 这个 `DoubleProperty` 可用于设置动画的播放速度和方向。
- `status` - 这个 `ReadOnlyProperty[Animation.Status]` 允许你确定动画的当前状态。可能的状态有 `Animation.Status.Paused`、`Animation.Status.Running` 和 `Animation.Status.Stopped`。
- `stop()` - 停止动画播放并将其重置为开头

# 使用 Scala 进行编程与问题解决简介

![](img/06d4e84f27a8884ea40ba6182ec7c778_378_0.png)

**图 12.7：** 左侧是你看到的 `Interpolator.EaseBoth` 的示例。右侧是你看到 `Interpolator.Linear` 的示例。

- **targetRate**: `Double` - 告知此动画预期播放的最大帧率。
- **totalDuration** - 一个 `ReadOnlyProperty[Duration]` 告知你播放整个动画的时间，包括任何重复。

动画执行需要时间，这一事实导致上述列出的许多方法都与 `scalafx.util.Duration` 配合工作。该类型的实例表示以毫秒为单位的时间持续。你可以通过 `new Duration(millis: Double)` 来创建一个。你可以在 `Durations` 之间执行标准的数学运算和比较。还定义了 `Duration.Indefinite`、`Duration.One`、`Unknown` 和 `Duration.Zero` 等特殊值。

## 12.5.1 Transitions

我们想要考虑的 Animation 的第一个子集是 `Transition` 类型。`Transition` 类型具有上述列出的所有 `Animation`成员，但增加了一个名为 `interpolator` 的 `ObjectProperty[Interpolator]`，它控制动画从开始到结束的方式。

你可以将动画想象为消耗 0.0 到 1.0 的时间，动画中的位置从 0.0 到 1。`Interpolator` 是一个接收值并返回值的函数。以下是可选选项：

- **Discrete**: 动画从一个值跳跃到下一个值。
- **EaseBoth**: 动画在开始和结束时减速。
- **EaseIn**: 动画在开始时减速。
- **EaseOut**: 动画在结束时减速。
- **Linear**: 动画以匀速移动。
- **Spline**: 动画遵循三次曲线。

# 图形与高级 ScalFX

- **Tangent(t1:Duration, v1:Double, t2:Duration, v2:Double)**: 这使用指定的控制点创建一个三次曲线。

- `PauseTransition` - 这不执行任何操作，只是在完成后调用 `onFinished` 代码。你可以通过 `new PauseTransition(duration: Duration)` 创建它。

- `RotateTransition` - 通过过渡动画旋转 Node。你可以通过 `new RotateTransition(duration: Duration, node: Node)` 或 `new RotateTransition(duration: Duration)` 创建其中一个。你应该指定轴，它是一个 `scalafx.geometry.Point3D`。你还应该设置 `angle` 或 `byAngle` 属性。

- `ScaleTransition` - 通过过渡动画缩放给定的 Node。你可以使用 `new ScaleTransition(duration: Duration)` 创建实例。

```
new ScaleTransition(duration: Duration)
```

或者

```
new ScaleTransition(duration: Duration, node: Node).
```

你应该指定 `fromX`、`fromY` 和 `fromZ` 属性。然后你可以指定 `tX`、`tY` 和 `tZ` 或者 `byX`、`byY` 和 `bZ`。

- `SequentialTransition` - 这是另一种组合过渡动画的方法。放入 `SequentialTransition` 中的过渡动画将一个接一个地发生。你可以使用 `new SequentialTransition(children: Seq[Animation])`、`new SequentialTransition(node: Node)` 或 `new SequentialTransition(node: Node, children: Seq[Animation])` 创建实例。如果你使用的选项没有提供这些属性，则需要指定 `node` 或 `children` 属性。

- `StrokeTransition` - 修改 Shape 上描边（stroke）的颜色。你可以使用 `new StrokeTransition(duration: Duration)`、`new StrokeTransition(duration: Duration, shape: Shape)`、`new StrokeTransition(duration: Duration, fromValue: Color, toValue: Color)` 创建实例。

或者

```
new StrokeTransition(duration: Duration, shape: Shape, fromValue: Color, toValue: Color).
```
