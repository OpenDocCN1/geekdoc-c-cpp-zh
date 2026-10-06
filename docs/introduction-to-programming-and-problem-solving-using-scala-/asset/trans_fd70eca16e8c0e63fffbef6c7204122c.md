

# 使用 Scala 进行编程与问题解决简介

- strokeLineJoin:
  - StrokeLineJoin.Bevel - 斜角 - 展平线段之间的连接处。
  - StrokeLineJoin.Miter - 接角 - 延伸线段以相交于一点。
  - StrokeLineJoin.Round - 圆角 - 将一个线段到下一个线段的过渡圆化。

- strokeMiterLimit: Double - 指定接角连接可以延伸程度。

- strokeType: StrokeType - 告诉形状绘制线条的位置。
  - StrokeType.Centered - 居中 - 在边缘上绘制。
  - StrokeType.Inside - 内部 - 在边缘内部绘制。
  - StrokeType.Outside - 外部 - 在边缘外部绘制。

- strokeWidth: Double - 指定描边的样式。

多态演示展示了 StrokeTypes 和 StrokeJoins。使用的样式从左到右依次是居中、内部和外部。连接方式从左到右依次是斜角、接角和圆角。底部的三条线展示了虚线和端点类型。这三条线都具有虚线结构，因此你可以看到不同端点类型的影响。线条使用的端点样式从上到部分别是平头（But）、接角（Miter）和方形（Square）。

## 12.2 基础键盘、鼠标和触摸输入

在第11章中，我们介绍了如何添加代码与各种 GUI 元素交互。通过获取键盘、鼠标以及触摸的单个动作，也可以在底层与用户进行交互。可以使用许多以 `on` 开头的不同属性来实现，每个属性都是在事件发生时被调用的函数。我们将针对不同的交互类型分别查看这些属性。

对于键盘，只有三个重要的属性：keyPressed、keyReleased 和 `onType`。`keyPressed` 函数在按键按下时调用。`keyReleased` 在按键松开时调用。`onType` 在字符完整输入时调用，且仅适用于带绑定的按键。这意味着 `onType` 不像 `keyPressed` 和 `keyReleased` 那样注册方向键、Shift 或 Ctrl 等内容。

这些处理器都接收一个 `scalafx.scene.KeyEvent` 的参数。这为你提供了有关按键如何作为事件一部分的信息，以及你可能需要知道的其他信息。`KeyEvent` 对象包含许多成员，如用于输入值的 `character`、`keyCode`（包括不可打印键），以及 `altDown`、`controlDown`、`metaDown` 和 `shiftDown`。`code` 成员的类型为 `scalafx.scene.keyCode`。你可以比较 `KeyCode` 中的值，例如 `KeyCode.A`、`KeyCode.F1`、`KeyCode.Left` 或许多代表键盘上可能按键的值。

在 11.5.1 节中，我们讨论了与文本控件相关的“焦点”概念。

> 注意，键盘具有“重复”速率，因此如果你按下并按住一个键，将会产生多次事件。

## 图形与高级 ScalaFX

相同的概念也适用于处理键盘事件。如果你在 GUI 中有多个元素，并且想处理某些元素的键盘事件，你必须对作为 `onMouseClicked` 句器的 `Node` 请求焦点，同时结合键盘处理，即当 `Node` 被点击时，你可以对其调用 `requestFocus`。

鼠标处理器只是你可以注册的用于使用鼠标处理用户交互的多个事件处理器之一。以下列表显示了不同的选项、这些处理器被调用的时机以及传递给它们的事件类型。

- onDragDetected - 接收一个 `MouseEvent`，并在检测到拖放时调用。

- onDragDone - 接收一个 `DragEvent`，并在释放后拖放 thả事件结束且当前 `Node` 是拖拽源时调用。

- onDragDropped - 接收一个 `DragEvent`，并在当前 `Node` 上的拖放操作结束并释放鼠标按键时调用。

- onDragEntered - 接收一个 `DragEvent`，并在拖放动作进入此 `Node` 时调用。

- onDragExited - 接收一个 `DragEvent`，并在拖放事件离开当前 `Node` 时调用。

- onDragOver - 接收一个 `DragEvent`，并在拖放事件移动到当前 `Node` 时调用。

- onMouseClicked - 当鼠标在此 `Node` 上点击时，接收一个 `MouseEvent`。

- mouseDragEntered - 接收一个 `MouseDragEvent`，并在鼠标按键按下时鼠标进入 `Node` 时调用。

- mouseDragExited - 接收一个 `MouseDragEvent`，并在鼠标按键按下时鼠标离开 `Node` 时调用。

- mouseDragOver - 接收一个 `MouseDragEvent`，当在此 `Node` 上发生完整的鼠标拖动释放手势时调用。

- mouseDragReleased - 接收一个 `MouseDragEvent`，当在此 `Node` 上结束鼠标按下-拖动-释放时调用。

- mouseDragged - 接收一个 `MouseDragEvent`，当鼠标在此 `Node` 上被按下并拖动时调用。

- mouseEntered - 当鼠标进入此 `Node` 时，接收一个 `MouseEvent`。

- mouseExited - 当鼠标离开此 `Node` 时，接收一个 `MouseEvent`。

- mouseMoved - 当鼠标在此 `Node` 内移动且没有按下按键时，接收一个 `MouseEvent`。

- mousePressed - 当鼠标按键在此 `Node` 上按下时，接收一个 `MouseEvent`。

- mouseReleased - 当鼠标按键在此 `Node` 上松开时，接收一个 `MouseEvent`。

- onScroll - 接收一个 `ScrollEvent`，并在用户执行滚动动作时调用。

- onScrollFilled - 接收一个 `ScrollEvent`，并在用户完成一次滚动动作时调用。

- onScrollStarted - 接收一个 `ScrollEvent`，并在用户开始滚动动作时调用。

`MouseEvent` 对象包含了你需要的关于鼠标状态的所有信息以及该特定事件的所有其他信息。以下列表显示了你可能需要的 `MouseEvent` 类型的重要成员：

- altDown - 告知 Alt 键是否按下。
- button - 告知鼠标按键类型（如 `MouseButton`）。
- clickCount - 告知连续点击的次数。
- controlDown - 告知 Control 键是否按下。
- metaDown - 告知 Meta 键是否按下。
- middleDown - 告知鼠标中键是否按下。
- pickResult - 告知拾取结果类型。
- primaryButtonDown - 告知主按键是否按下。
- source - 告知事件的源。
- stillSincePress - 告知自上一次按下以来是否保持状态。
- shiftDown - 告知 Shift 键是否按下。
- shortcutDown - 告知快捷键组合是否按下。
- x - 鼠标的 X 坐标。
- y - 鼠标的 Y 坐标。
- z - 鼠标的 Z 坐标（深度）。

`DragEvent` 是 `MouseEvent` 的子类，用于确定拖拽开始的对象。`DragEvent` 移除了关于按键的成员，取而有一个返回 `Drag` 对象的 `drag` 方法。`ScrollEvent` 具有 `MouseEvent` 的许多关于键和位置的方法，并增加了滚动特定的方法。

鼠标和键盘交互在以下程序中演示，该程序允许用户使用鼠标绘制路径，然后使用方向键移动一个小圆。圆圆不允许跨越线条。

# Listing 12.4: DrawMaze.scala

```
import scalafx.Imports._
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.paint.Color
import scalafx.scene.shape._
import scalafx.scene.input.MouseEvent
import scalafx.scene.input.KeyCode
val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Draw Maze"
    scene = new Scene(500,500) {
      val polyline = Polyline(0, 0, 500, 0, 500, 500, 0, 500, 0, 0)
      var walls = List(polyline)

      val ball = Circle(21, 21, 20)

      content = List(ball) = (e:MouseEvent) => {
        println("Pressed")
        val oldX = ball.centerX.value
        val oldY = ball.centerY.value
        if (e.code == KeyCode.Up) ball.centerY = ball.centerY.value - 2
        if (e.code == KeyCode.Down) ball.centerY = ball.centerY.value + 2
        if (e.code == KeyCode.Left) ball.centerX = ball.centerX.value - 2
        if (e.code == KeyCode.Right) ball.centerX = ball.centerX.value + 2

        // 碰撞检测
        val clear = walls.forall(shape =>
          Shape.intersect(ball,shape).boundsInLocal.value.isEmpty
        )
      }
    }
  }
}
```
