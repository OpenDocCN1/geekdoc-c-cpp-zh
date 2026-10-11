
```scala
val boxBlur = makeText(20, 80, "BoxBlur", new BoxBlur(), false)

val displacementMap = makeText(20, 120, "DisplacementMap", new DisplacementMap(), false)

val gaussianBlur = makeText(20, 160, "GaussianBlur", new GaussianBlur(), false)

val innerShadow = makeText(20, 200, "InnerShadow", new InnerShadow(), false)

val lighting = makeText(20, 240, "Lighting", new Lighting(new Light.Distant(0, 45, Color.White)), true)

val motionBlur = makeText(20, 280, "MotionBlur", new MotionBlur(15, 10), false)

val perspective = makeText(20, 320, "Perspective", new PerspectiveTransform(500, 500, 400, 520), false)

val reflection = makeText(20, 360, "Reflection", new Reflection(0.5, 1.0, 0.0), false)

val shadow = makeText(20, 400, "Shadow", new Shadow(5, Color.Black), false)

root.children.addAll(bloom, boxBlur, displacementMap, gaussianBlur, innerShadow, lighting, motionBlur, perspective, reflection, shadow)

}

content = root

}

title = "Effects"

}

}

app.main(args)
```

![](img/06d4e84f27a8884ea40ba6182ec7c778_401_0.png)

图 12.12: 运行 Effects.scale 产生的窗口。

# 使用 Scala 进行编程与问题解决

## 列表 12.12: ImageEffects.scala

该程序的输出见图 12.13.¹1⁰

![](img/06d4e84f27a8884ea40ba6182ec7c778_403_0.png)

**图 12.13:** 运行 ImageEffects.scala 并使用四个示例图像后生成的窗口。左上角和右下角的图像设置为 ColorAdjust 效果，右上角使用了 SepiaTone，左下角使用了 Glow。

## 12.8 图表

当你拥有数据集时，在计算机上执行的一项常见任务是使用图表来绘制数据。因此，ScalaFX 包含一个 `scalafx.scene.chart` 包，其中包含许多不同的图表类型，以及构建这些图表所需的其他类型。该库中包含八种不同类型，它们如下：

- AreaChart - 面积图：根据一组或多组数值 x-y 数据，将从零到线条的区域进行填充。
- BarChart - 柱状图：为针对不同文本类别的柱状形式显示数据。
- BubbleChart - 气泡图：在数值 x-y 坐标处绘制不同大小的气泡。
- LineChart - 折线图：为一组数值 x-y 数据绘制折线。
- PieChart - 饼图：为一组带标签的数值数据绘制饼图。
- ScatterChart - 散点图：为一组 x-y 数据绘制散点图。
- StackedArea - 堆叠面积：为多系列 x-y 数据绘制堆叠的面积图。
- StackedBarChart - 堆叠柱状图：为不同类别绘制堆叠的柱体。

除了 PieChart 外，所有图表都继承自 `XYChart`，由于它是抽象的，因此未在此列出。`XYChart` 的所有子类型都需要两个轴以及要绘制的数据。Scala 提供了三种不同类型的轴（Axis），包括用于文本类别的 `CategoryAxis` 和用于数值的 `NumberAxis`。
为了帮助在程序中使用这些图表，以下代码根据关于我们太阳系的数据创建了三个不同的图表：PieChart、BarChart 和 ScatterChart。

### 代码列表 12.13：Charts.scala

```scala
import scalafx.Includes.

import scalafx.application.JFXApp

import scalafx.scene.Scene

import scalafx.scene.chart.

import scalafx.scene.control.

import scalafx.scene.layout.

import scalafx.collections.ObservableBuffer

import scalafx.geometry.Pos

val app = new JFXApp {

  stage = new JFXApp.PrimaryStage {

    title = "Charts"

    scene = new Scene(1000, 800) {

      class PlanetData(name:String, mass:Double, radius:Double)

      val planets = List(

        PlanetData("Mercury", 0.0553, 0.387),

        PlanetData("Venus", 0.815, 0.723),

        PlanetData("Earth", 1.0, 1.0),

        PlanetData("Mars", 0.107, 1.524),

        PlanetData("Jupiter", 31.83, 5.203)

      )

    }

  }

}
```

## 图形与 ScalaFX

```scala
PlanetData("Saturn", 95.159, 9.537)
PlanetData("Uranus", 14.536, 19.191)
PlanetData("Neptune", 17.147, 30.069)
```

```scala
val pieChart = PieChart(ObservableBuffer(planets.map(p =>
    PieChart.Data(p.name, p.mass))))

val barSeries = XYChart.Series("Planetary Mass",
ObservableBuffer(planets.map(p => XYChart.Data(p.name,
    p.number))))

val barChart = BarChart(CategoryAxis("Mass [Earth Mass]"),
ObservableBuffer(barSeries))

val scatterSeries = XYChart.Series("Mass vs. Orbital Distance",
ObservableBuffer(planets.map(p => XYChart.Data(p.a,
    p.mass))))

val scatterChart = ScatterChart(NumberAxis("Semimajor Axis [AU]"),
NumberAxis("Mass [Earth Mass]"), ObservableBuffer(scatterSeries))

val tilePane = new TilePane
tilePane.children = List(pieChart, barChart, scatterChart)
tilePane.alignment = Pos.TopCenter
root = tilePane
```

运行此代码的结果可以在图 12.14 中看到。按照惯例，代码开头有很多导入，这次包含了 `scalafx.scene.chart`。紧接着是应用程序、阶段（stage）和场景（scene）的常规设置。第 14-22 行定义了一个类类和一个实例列表，该实例提供了绘图所需的数据。这些数据包含了我们太阳系的行星，其以地球质量为单位的质量以及以 AU（距离太阳的平均距离）为单位的半长轴¹

第 24 行创建了一个 PieChart，用于显示太阳系中太阳以外的部分。这是通过传递一个填充了 PieChart 数据的 PieChart ObservableBuffer 实现的。如果值发生变化，ScalaFX 中的所有图表都将更新。这可以用于在某些应用程序中观察效果。图表还有一个名为 `animated` 的属性，如果将其设置为 `true`，此类更改将以动画形式呈现。在这种情况下。

## 使用 Scala 进行编程和问题解决简介

## 12.9 媒体

媒体（无论是音频还是视频）已成为许多现代用户界面的重要部分。ScalaFX 包含了许多类型，我们可以在 `scalafx.scene.media` 包中通过这些类型为我们的应用程序添加媒体。我们将只介绍其中最重要的几个。

想要重复播放的短音频最适合用 `AudioClip` 类型表示。源需要是一个 URL。你可以使用 `new AudioClip(source: String)` 创建一个 AudioClip。如果你在当前目录下有一个文件，只需简单指定 `"file:filename"`。ScalaFX 支持包括 .wav 和 mp3 在内的多种音频格式。

较长的音频文件和漂亮的视频文件不应完全加载到内存中。`Media` 类型用于表示此类文件。你使用 `new Media(source: String)` 创建 `Media` 实例，其中源应该是一个 URL，就像 AudioClip 一样。除了上述提到的音频格式外，ScalaFX 对视频有相当通用的支持，但没有音频那么广泛。你可能会发现，你必须花一些精力来获取它接受的格式的视频文件。作者的经验是，你使用的 `Media` 实例需要一个 `MediaPlayer`。你可以使用 `new MediaPlayer(media: Media)` 创建 `MediaPlayer` 实例。如果 Media 是音频，这就是你需要的所有。对于视频，你会希望它在 GUI 中显示。这是通过使用 `new View(mediaPlayer: MediaPlayer)` 创建 `View` 完成的。`View` 是 `Node` 的子类型，可以添加到 GUI 中。调用 `MediaPlayer` 上的 `play`、`pause` 和 `stop` 方法将控制 `View` 中显示的内容。

演示使用这些媒体类型的程序将播放 AudioClip 的顶部波形，按钮上有一个按钮控制它。大多数显示显示带有按钮的视频。

### 列表 12.14: Media.scala

```scala
import scalafx.Includes.-

import scalafx.application.JFXApp

import scalafx.scene.Scene

import scalafx.scene.media.-

import scalafx.scene.layout.-

import scalafx.scene.control.Button

import scalafx.event.ActionEvent

val app = new JFXApp {

  stage = new JFXApp.PrimaryStage {

    title = "Media"

    scene = new Scene(600, 350) {

      val audioClip = new AudioClip("file:Laser-Cannon-sound.mp3")

    }

  }

}

val playButton = new Button("Play!")

playButton.setOnAction = (ae:ActionEvent) => audioClip.play

playButton.prefWidth = Int.Max
```

> 12 编写时，JavaFX 8 支持 MP3、未压缩 PCM、WAV 未压缩 PCM、MPEG-4 多媒体容器 (AAC)

> 13 编写时，JavaFX 8 支持 FLV 视频和 MP3 音频；MPEG-4 多媒体容器包含 H.264/AVC (视频)

> 14 AudioClip 的声音是从 http://soundbibible.com/Laser-Cannon.html 下载的。

## 图形与高级 ScalaFX

![](img/06d4e84f27a8884ea0182c77_0.png)

```scala
val media = new Media("http://techslides.com/demos/videos/small.mp4")

val mediaPlayer = new MediaPlayer(media)

val mediaView = new MediaView(media)

val playButton = new Button("Play")

playButton.onAction = (ae:ActionEvent) => mediaPlayer.play

val pauseButton = new Button("Pause")

pauseButton.onAction = (ae:ActionEvent) => mediaPlayer.pause

val stopButton = new Button("Stop")

stopButton.onAction = (ae:ActionEvent) => mediaPlayer.stop

val borderPane = new BorderPane

borderPane.top = playButton

borderPane.left = new VBox(playButton, pauseButton, stopButton)

borderPane.center = mediaView

root = borderPane

app.main(args)
```

图 12.15：运行 Media.scala 产生的窗口。

此代码产生的窗口如图所示。

## 12.10 Web

正如媒体文件在应用程序中变得越来越重要，Web 也是如此。ScalaFX 包含了 `scalafx.scene.web` 包中的类型，允许你将 Web 引入应用程序。其中最明显的是 `WebView`，它基本上是 `Node` 中的全功能浏览器，你可以将其添加到任何想要显示 Web 内容的 GUI 中。`WebView` 实际上是 `WebEngine` 的图形界面，由它执行相关工作。

下面的示例使用了 `WebView` 和 `TextField` 来制作一个 Web 浏览器。它们位于 `BorderPane` 中，顶部是 `TextField`，中间是 `WebView`。`WebView` 初始化显示 Scala 页面。

### 列表 12.15: Web.scala

```scala
import scalafx.Includes._

import scalafx.application.JFXApp

import scalafx.event.ActionEvent

import scalafx.scene.Scene

import scalafx.scene.control.TextField

import scalafx.scene.layout.BorderPane

import scalafx.scene.web.-

val app = new JFXApp {

  stage = new JFXApp.PrimaryStage {

    title = "Web"

    scene = new Scene(750, 600) {

      val textField = new TextField

      val webView = new WebView

      webView.engine.load("http://www.scala-lang.org")

      textField.text = webView.location.value

    }

    val borderPane = new BorderPane

    borderPane.top = textField

    borderPane.center = webView

    root = borderPane

    textField.onAction = (ae:ActionEvent) => {

      webView.engine.load(textField.text)

    }

    webView.location.onChange(textField.text = webView.location.value)

  }

}

app.main(args)
```
