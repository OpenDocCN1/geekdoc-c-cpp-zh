
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

在代码末尾添加了处理器，这样当用户在 `TextField` 中输入 URL 并按回车时，将显示页面；当页面由于点击链接等发生更新时，将显示显示的文本。如果你输入完整的 URL 并运行它，请注意你有一个完整的 URL，并使用协议（通常是 http）以便其工作。

图 12.16 显示了该脚本运行时的样子。你可以用这少量代码在 Web 上查看更多内容。它不会做的主要事情之一是播放像 YouTube 等网站上的媒体。

`scalafx.scene.web` 包中的另一个 `Node` 类型是 `HTMLEditor`。正如名称所示，该类型为你提供了一个可以用于编辑格式化文本的编辑器。用户看到的是带有显示方式控制的编辑器。后端表示使用 HTML 的事实不会对用户暴露。如果你想允许用户编辑 `TextArea` 纯文本之间的文本，这就是你在 ScalaFX 中想要执行的地方。下面的代码显示了一个使用该类型的脚本，并带有用于保存和打开文件到功能编辑器的菜单选项。

**图 12.16：**运行 Web.scala 产生的窗口。

![](img/06d4e84f27a8884ea0182c77_0.png)

```
import scalafx.Includes._

import scalafx.application.JFXApp

import scalafx.event.ActionEvent

import scalafx.scene.Scene

import scalafx.scene.control._

import scalafx.scene.layout._

import scalafx.scene.web._

import scalafx.stage.FileChooser

import io

val app = new JFXApp {

  stage = new JFXApp.PrimaryStage {

    title = "Rich Editor"

    scene = new Scene(600, 400) {

      val menuBar = new MenuBar

      val fileMenu = new Menu("File")

      val openItem = new MenuItem("Open")

      val saveItem = new MenuItem("Save")

      val exitItem = new MenuItem("Exit")

      fileMenu.items = List(openItem, saveItem, SeparatorMenuItem, exitItem)

      menuBar.menus = List(fileMenu)

      menuBar.prefWidth = Int.Max

    }

  }

}

val editor = new HTMLEditor
```

```scala
val borderPane = new BorderPane
borderPane.top = menuBar
borderPane.center = editor
root = borderPane
openItem.setOnAction = (ae:ActionEvent) => {
  val chooser = new FileChooser
  chooser.showDialog(stage) match {
    case null =>
    case file =>
      val source = io.Source.FromFile(file)
      editor.htmlText = source.mkString
      source.close
  }
}
saveItem.setOnAction = (ae:ActionEvent) => {
  val chooser = new FileChooser
  chooser.showSaveDialog(stage) match {
    case null =>
    case file =>
      val pw = new java.io.PrintWriter(file)
      pw.print(editor.htmlText)
      pw.close()
  }
}
exitItem.setOnAction = (ae:ActionEvent) => {
  sys.exit(0)
}
app.main(args)
```

运行此文本创建的窗口如图 12.17 所示。（等等，图片引用缺失）

到为止，我们所做的一切都是明显的 2D 内容。这有几个原因，主要原因是 2D 图形要简单得多。尽管相对“简单”，但我们仍然在这个主题上花费了超过 50 页的内容。3D 图形的细节比我们在本节中涵盖的要多得多。这将是对该主题的一个非常基础的介绍，提供足够进行 3D 图形基础操作的知识。

## 12.11 3D 图形

我们将讨论的最后一个 ScalaFX 主题是 3D 图形。

# 图形与进阶 ScalaFX

![](img/06d4e84f27a8884ea40ba6182ec7c778_413_0.png)

这是一段文本。

这段文本是**粗体**的。

这段文本带有下划线。

现在是一个列表：

- * 一个

- 两个

- 三个

文本甚至可以有不同的颜色。

图 12.17：运行 HTMLEEditor.scala 产生的窗口。

`scalafx.scene.shape` 类型中提供了四种不同的 3D 形状。这些形状是 `Box`、`Cylinder`、`MeshView` 和 `Sphere`。除了 `MeshView` 之外，这些作为基础 3D 形状应该是相当自而易懂的。`MeshView` 涵盖了除这三种形状之外的所有内容，让你通过三角形创建复杂的几何体。`MeshView` 的正确覆盖超出了我们讨论的范围。

对于 2D 形状，你需要指定用于绘制它们的字段。当你进入 3D 模式时，这变为了材质（material）。ScalaFX 为此目的提供了 `scalafx.scene.paint.PhongMaterial` 类型。你可以通过 `new PhongMaterial(diffuseColor: Color, diffuseMap: Image, specularMap: Image, bumpMap: Image, selfIllumination: Map)` 或 `new PhongMaterial(diffuseColor: Color)` 来实例化该类型。第一种选项对材质外观提供了显著的控制。例如，`diffuseMap` 允许你为形状的表面应用纹理。

除了形状之外，当你转向 3D 时，还会使用相机和光照，这两者都定义在 `scalafx.scene` 包中。提供了两种类型的相机。默认情况下你使用 `ParallelCamera`（平行相机）。当你使用 `ParallelCamera` 时，物体不会随着远离相机而变小。在这种视图中，远离观察者的平行线保持平行。这在现实生活中并非如此，但对于某些应用程序已经足够了。`PerspectiveCamera`（透视相机）更接近我们真实的观察方式，物体会随着距离变远而缩小，一切都汇聚到远处的一点。你通过 `new ParallelCamera` 创建 `ParallelCamera`。要创建 `PerspectiveCamera`，使用 `new PerspectiveCamera(fixedEyeAt:Boolean)`。`Stage` 有一个名为 `camera` 的成员，你可以将其分配为你所需的相机类型。

ScalaFX 中有两种类型的光。它们是 `AmbientLight`（环境光）和

> 15 整个舞台只能有一个相机的能力可能有点局限性。`scalafx.scene` 包

`PointLight`（点光源）。`AmbientLight` 照亮所有地方，而 `PointLight` 可以移动，它就像那里有一盏光一样照亮场景中的物体。它们通过 `new` 创建，并需要一个 `Color` 类型参数，即光的颜色。

以下代码展示了 ScalaFX 中这些 3D 图形功能的示例。它向场景中各添加了一个底座和一个每种类型的的光源。有控件可以让你选择相机类型和光的颜色。你还指定了是否要为 `Sphere` 设置纹理。它初始是平坦的红色，但如果你选择了 `CheckBox`，它将使用火星表面贴图进行纹理化。

Listing 12: 3D.scale

```
1 import scalafx.Includes_
2 import scalafx.application.JFXApp
3 import scalafx.scene.(Scene, ParallelCamera, PerspectiveCamera, AmbientLight,
PointLight)
4 import scalafx.scene.Image
5 import scalafx.scene.paint.{Color, PhongMaterial}
6 import scalafx.scene.shape.{Box, Cylinder, MeshView, Sphere}
7 import scalafx.scene.control.
8 import scalafx.event.ActionEvent
9
10 val app = new JFXApp {
11 stage = new JFXApp.PrimaryStage {
12 title = "3D"
13 scene = new Scene(400, 400),
14 val marsImage = new Image("file:marssurface.jpg")
15 val sphere = new Sphere(50)
16 sphere.translateX = 200
17 sphere.translateY = 200
18 val sphereMaterial = new PhongMaterial(Color.Red)
19 sphere.material = sphereMaterial
20
21 val cylinder = new Cylinder(40, 100),
22 cylinder.translateX = 100
23 cylinder.translateY = 100
24 cylinder.material = new PhongMaterial(Color.Green)
25
26 val box = new Box(50, 40, 60)
27 box.translateX = 300
28 box.translateY = 300
29 box.material = new PhongMaterial(Color.Blue)
30
31 val ambient = new AmbientLight(Color.Gray)
32 val point = new PointLight(Color.White)
33 point.translateX = 400
34 point.translateZ = -400
35
36 val usePerspective = new CheckBox("Perspective View")
37 usePerspective.layout = 270
38 usePerspective.setOnAction = (e:ActionEvent) => {
39 if (usePerspective.selected.value) {
40 camera = new PerspectiveCamera(false)
```

还有一种名为 `SubScene` 的类型，它是 `Node` 的子类型。每个 `SubScene` 都有自己的相机，这样你可以通过这种方式创建多个视图。

```
else if {
    camera = new PerspectiveCamera
}

val useTexture = new CheckBox("Texture")
useTexture.layout = 270
useTexture.setOnAction = (e:ActionEvent) => {
    if (useTexture.selected.value) {
        camera = new PerspectiveCamera(false)
```

（注：此处根据代码逻辑推断了缺失的对应关系，但严格遵循翻译要求，仅翻译可见文本）

此外，还有一种名为 `SubScene` 的类型，它是 `Node` 的子类型。每个 `SubScene` 都有自己的相机，这样你可以通过这种方式创建多个视图。

```
else if {
    camera = new PerspectiveCamera
}

val useTexture = new CheckBox("Texture")
useTexture.layout = 270
useTexture.setOnAction = (e:ActionEvent) => {
    if (useTexture.selected.value) {
        camera = new PerspectiveCamera(false)
```

material.diffuseMap = marsImage

sphereMaterial.diffuseColor = Color.White

    } else {

sphereMaterial.diffuseMap = null

sphereMaterial.diffuseColor = Color.Red

    }

}

val ambientPicker = new CheckBox(ambient.value)

ambient.color <== ambientPicker

ambientPicker.layout = 330

val pointPicker = new CheckBox(point.value)

point.color <== pointPicker

pointPicker.layout = 360

content = List(sphere, cylinder, box, usePerspective,useTexture)
```
