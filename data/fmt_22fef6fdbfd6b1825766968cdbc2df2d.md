
最后一个绑定使用 `<<` 操作符将 `ScrollBar` 的值与 `Slider` 的值连接起来，后者被绑定到矩形的 y 值上。如果你移动其中一个，另一个也会移动，矩形的垂直位置也会之移动。在图 11.13 中，你可以看到 `ScrollBar` 和其上方的 `Slider` 相同的位置。

## 11.6.2 条件绑定

可以创建条件绑定。这是通过 `when`、`choose` 和 `otherwise` 实现的。为了说明这一点，我们有一个包含 `Slider` 和 `Label` 的简单脚本。`Label` 的位置由 `Slider` 决定。与之前的示例不同（之前的位置是平滑移动的），这里的位置是不连续的，因此它会跳跃

> 在编写此代码的 ScalaFX 版本中，由于绑定发生在场景尺寸确定之前，这会产生一个警告。这对脚本的行为没有产生负面性能影响，因此我们将忽略它。

当 Slider 越过中间值时，从左侧跳到右侧。背景颜色取决于鼠标是否悬停在 Label 上。

### 列表 11.16: ConditionalBindings.scala

```scala
import scalafx.Includes._
import scalafx.Scene
import scalafx.application.JFXApp
import scalafx.scene.control.Label
import scalafx.scene.control.Slider
import scalafx.scene.paint.Color

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Conditional Bindings"
    scene = new Scene(500, 250) {
      label = new Label("Hover to change background.")
    }
  }
}
val slider = new Slider(0,100,0)
slider.layoutX = 10
slider.layoutY = 10
slider.prefWidth = 180

content = List(label, slider)
label.layoutX <= when (slider.value < 50) choose 0 otherwise width
label.layoutY <= height/2
fill <= when (hover) choose Color.Red otherwise Color.White
```

在代码末尾，你可以看到是如何创建条件绑定的。`when` 后面跟着一个可观察布尔值，接着是 `choose` 如果为真时应使用的值。然后是 `otherwise` 如果假时应使用的值。与 `if` 和 `else` 不同，`when`、`choose` 和 `otherwise` 不是 Scala 语言的关键字，它们是 ScalaFX 库的一部分。`import Includes._` 使它们可见，而其他的实际上是以中表达式形式（infix style）使用的。图 11.14 显示了通过此脚本得到的窗口，其中 Slider 移动到了（未显示的）标签上方。记住，中表达式形式是将带有一个参数的方法放在对象和操作数之间，而不使用点号或括号。我们通常在符号操作符中使用它。

![](img/06d4e84f27a8884ea40ba6182ec7c78_330.png)

**图 11.14：** 此图显示了在滑块调整且鼠标悬停在标签上后，`ConditionalBindings.scala` 窗口。

## 11.7 布局与面板

虽然可以使用绑定在更改窗口大时处理周围物体，但这并不是构建复杂界面的方法。在 Scala 中构建复杂界面的正确方法是使用布局和面板。大部分这些位于 `scalafx.scene.layout` 包中，但一些位于 `scalafx.scene.control` 中。control 中的那些产生不与用户交互的简单布局。使用其中任何一种，都可以通过嵌套它们来创建复杂的显示。面板本身是节点，这样它们在整个尺寸变化时改变。以下列表是 `scalafx.scene.layout` 包中描述的类型：

- **AnchorPane**：允许你设置面板内部的位置。你可以调用 `AnchorPane.setAnchor(child, value)` 来指定元素在何处出现。
- **BorderPane**：提供了五个区域：顶部、底部、左侧、右侧和中心。它们占据面板的各个边缘空间。
- **FlowPane**：按照顺序排列元素。当它们超出空间时，会换行。
- **HBox**：水平排列元素。它们占据整个宽度。
- **StackPane**：将元素堆叠在一起。
- **TilePane**：以网格形式排列元素。元素的大小由内容决定。
- **VBox**：垂直排列元素。它们占据整个高度。

为了说明这项工作，以下代码创建了一个 GUI，它包含 `BorderPane` 作为主要内容，并带有 `VBox`、`FlowPane`、`StackPane` 和 `TilePane` 。

### 列表 11.17: Layouts.scala

```scala
import scalafx.Includes._
import scalafx.Scene
import scalafx.application.JFXApp
import scalafx.scene.control._
import scalafx.scene.layout.BorderPane
import scalafx.scene.layout.FlowPane
import scalafx.scene.layout.HBox
import scalafx.scene.layout.Pane
import scalafx.scene.layout.StackPane
import scalafx.scene.layout.TilePane
import scalafx.scene.layout.VBox
import scalafx.scene.layout.Background
import scalafx.scene.layout.BackgroundFill
import scalafx.scene.color.Color

def addControlsToPane(pane:Pane, fill:Color):Pane = {
  val button = new Button("Click Me")
  val label = new Label("Plain label")
  val field = new TextField
  field.text = "Text Field"
  val area = new TextArea
  area.text = "Text Area\nMultipleLines"
  area.prefWidth = 100
  area.prefHeight = 100
  val combo = new ComboBox(List("Alpha", "Beta", "Gamma"))
  val slider = new Slider
  pane.children = List(button, label, field, area, combo, slider)
  pane.background = new Background(Array(BackgroundFill(fill, null, null)))
  pane
}

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Layouts"
    scene = new Scene(750,600) {
      val borderPane = new BorderPane
      borderPane.top = addControlsToPane(new HBox(10), Color.gray(0.25))
      borderPane.left = addControlsToPane(new VBox(10), Color.gray(0.75))
      borderPane.bottom = addControlsToPane(new FlowPane(10, 10), Color.gray(0.5))
      borderPane.right = addControlsToPane(new StackPane, Color.gray(1.0))
      val tilePane = new TilePane
      tilePane.prefRows = 2
      borderPane.center = addControlsToPane(tilePane, Color.gray(0.0))
      tilePane.children.foreach(.managed = true)
      root = borderPane
    }
  }
}
app.main(args)
```

运行此程序的运行如图 11.15 所示。对控件的导入更改为使用下划线，因为这些细节在上面讨论过了。`addControlsToPane` 函数之所以编写，是因为相同的控件被添加到到

## GUI 界面

![](img/06d4e84f27a8884ea40ba6182ec7c778_333_0.png)

图 11.15：此图显示了在微调窗口大小后，运行 `Layouts.scala` 产生的窗口。

每一个不同的窗格（pane）我们都不希望重复那些代码。将其制作为一个 `Pane` 以便默认与所有窗格一起。设置了 `TextArea` 的首选大小，以便其不会在 GUI 中占用过多的空间。所有其他元素均保持默认大小。`addControlsToPane` 函数还接受一个参数，用于设置 `Pane` 的背景颜色。这是在函数末尾设置 `Pane.background` 时完成的。设置 `Pane` 的背景有许多选项，在后续的 GUI 设计中，我们不会不会书中书中讨论细节。

在顶部，我们看到 `HBox`，它具有深灰色背景颜色，水平方向排列控件，并且默认所有控件都与窗格对齐。注意，这可以通过设置 `alignment` 属性来更改。左侧是具有浅灰色背景色的 `VBox`，它的行为与 `HBox` 类似，但会将元素垂直堆叠并向左对齐。底部是一个具有中灰色背景的 `FlowPane`，从生成的结果上看与 `HBox` 相似，但有显著的差异需要注意。控件默认垂直居中，当窗口太小到无法容纳单行时，最后一个元素将移动到新的一的一行。如果窗口更小，`Slider` 在 `HBox` 中会被截断。传递给 `make FlowPane` 的两个参数是间距（spacing）值。这些值代表项目之间垂直和水平的像素数。可以使用 `Insets` 为所有元素添加间距，但我们不会详细介绍这些内容。

右侧是 `StackPane`。它的背景不可见，因为 `TextArea` 覆盖了整个标题区域，不仅隐藏了背景，还隐藏了在 `TextArea` 之前添加的元素。这与其他窗格产生了非常不同的结果，因为控件是字面上一个堆叠在另一个之上的。中间是一个具有黑色背景的 `TilePane`。所有控件都被赋予与内容最大宽度和最大高度相等的空间。然后它们按行布局，根据需要形成新行。`TilePane` 的工作方式与 `FlowPane` 类似，不同在于元素的大小方式。

注意 `BorderPane` 被设置为 `Scene` 的根节点。如前所述，这导致它绑定到窗口的大小，因此当窗口大小改变时，控件会调整。如果你使用 `content`，默认情况下不会发生这种情况。

`GridPane` 比上一个例子中的窗格复杂一点，因此我们为它单独编写了一个。以下代码展示了如何使用 `GridPane` 为基础计算器布局一个 GUI。

### 列表 11.18: GridPane.scala

```scala
import scalax.includes._
import scalax.scene.Scene
import scalax.application.JFXApp
import scalax.scene.control.*
import scalax.scene.layout.GridPane
import scalax.scene.layout.Priority

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "GridPane"
    scene = new Scene(300,300) {
      val gridPane = new GridPane
      for (i <- 1 to 9) {
        val button = new Button(i.toString)
        gridPane.children += button
        gridPane.setColumnIndex(button, (i-1)%3)
        gridPane.setRowIndex(button, (i-1)/3+1)
        gridPane.setHgrow(button, Priority.Always)
        gridPane.setVgrow(button, Priority.Always)
        button.maxWidth = Int.MaxValue
        button.maxHeight = Int.MaxValue
      }
      val textField = new TextField
      gridPane.children += textField
      val zeroButton = new Button("0")
      gridPane.children += zeroButton
      gridPane.setConstraints(textField,0,0,4,1)
      gridPane.setVgrow(zeroButton,0,4,2)
      zeroButton.maxWidth = Int.MaxValue
      zeroButton.maxHeight = Int.MaxValue
      val periodButton = new Button(".*")
      gridPane.children += periodButton
      gridPane.setConstraints(periodButton,2,4)
      gridPane.setVgrow(periodButton, Priority.Always)
      periodButton.maxWidth = Int.MaxValue
      periodButton.maxHeight = Int.MaxValue
      val plusButton = new Button("+")
      gridPane.children += plusButton
      gridPane.setConstraints(plusButton,3,1)
      gridPane.setHgrow(plusButton, Priority.Always)
      plusButton.maxWidth = Int.MaxValue
      plusButton.maxHeight = Int.MaxValue
      val minusButton = new Button("-")
      gridPane.children += minusButton
      gridPane.setConstraints(minusButton,0,4)
    }
  }
}
```

此代码的结果可以在图 11.16 中看到。为了添加按钮，我们使用循环来避免重复编写九次代码。在每个 `Button` 创建并添加后，我们对其设置了约束。此代码通过单独调用设置了行和列值，然后设置约束的 `Hgrow` 和 `Vgrow` 值。如果没有这样做，行和列将不会扩展以填充窗口的所有空间，所有元素将保持聚集在左上角。

## 菜单栏

| 食谱列表 | 配料按钮 | 配料设置 |

|--- | --- | --- |

| | 配料列表 | |

| | 食谱步骤说明 | |

**图 11.18:** 这展示了用户为编辑食谱构建的 GUI 的可能布局。

## 11.8 整合在一起

现在我们已经简要探索了 ScalaFX GUI 的不同组件以及我们如何与它们交互，我们可以尝试将其中许多组件组合在一个更大的程序中。这个程序将类似于一个数字食谱本。对于每份食谱，它应该允许用户指定配料及其数量，以及烹饪步骤的文字描述。GUI 应该赋予用户添加和删除食谱的能力。他们应该能够选择食谱并编辑我们拥有的各种信息。

在分析的这一阶段，你可能想要画一个你想要的 GUI 型的简单草图。即图 11.18 中的这个 GUI。左侧由一个 `ListView` 占据，它显示食谱中所有的食谱，而相关信息应该显示在右侧。这包括所有配料列表和步骤。配料也可以被编辑，需要一些按钮来帮助完成。添加和删除食谱的选项将位于菜单中。
