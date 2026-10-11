
```
if (rightPressed) player = player.copy(x = player.x+speed*dt)

if (upPressed) player = player.copy(y = player.y-speed*dt)

if (downPressed) player = player.copy(y = player.y+speed*dt)

}
```

## 370 使用 Scala 进行编程与问题解决介绍

```scala
def moveEnemies(t:Double, dt:Double):Unit = {
  enemies for (e <- enemies; e.time+enemyLifespan>t) yield {
    val speed = if (inMud(e.x,e.y)) 15 else 0
    val dx = if (e.x < player.x) speed else if (e.x > player.x) -speed else 0
    val dy = if (e.y < player.y) speed else if (e.y > player.y) -speed else 0
    e.copy(x=e.x+dx(util.Random.nextInt(5)-2)*dt,
    y=e.y+dy(util.Random.nextInt(5)-2)*dt)
  }
}
```

```scala
def checkKill():Unit = {
  for (enemy <- enemies) {
    val dx = enemy.x-player.x
    val dy = enemy.y-player.y
    if (dx*dx+dy*dy < 25) {
      playerDead = true
      timer.stop
    }
  }
}
```

```scala
def updatePlayers(dt:Double):Unit = {
  puddles = puddles.filter(_.size > 1).map(p => p.copy(size =
    math.sqrt(p.size*p.size-5)))
}
```

```scala
val timer = AnimationTimer(t => {
  if (lastTime != 0) {
    val dt = (t-lastTime)/1e9
    movePlayer(dt)
    moveEnemies(t/1e9, dt)
    checkKill()
    updatePuddles(dt)
    regenDelay = -dt
    if (regenDelay < 0) {
      val cx = util.Random.nextInt(CanvasSize-10)
      val cy = util.Random.nextInt(CanvasSize)
      enemies += Enemy(10+cx*(CanvasSize-20), cy, t/1e9)
      if (math.random<0.1)enemyLifespan += 1
      regenDelay = 10.0
    }
  }
  lastTime = t
})
```

```scala
// Draw stuff
gt.fill = Color.Black
gt.fillRect(0, 0, canvas.width, canvas.height)
for (p <- puddles) {
  gt.fill = Color.Brown
  gt.fillOval(p.x-p.size, p.y-p.size, p.size*2, p.size*2)
}
for (enemy <- enemies) {
  gt.fill = Color(0, 0, 0, (t/1e9-enemy.time)/enemyLifespan.toFloat)
  gt.fillOval(enemy.x-5, enemy.y-5, 10, 10)
}
```

## 图形与高级 ScalaFX

![](img/06d484f27a88ea40ba618ec778395_0.png)

**图 12.11:** 运行 `EvadeGame.scala` 在绘制附近的水洼后产生的窗口。

```scala
}
gt.fill = Color.Green
gt.fillOval(player.x-5, player.y-5, 10, 10)
if (playerDead) {
    gt.fill = Color.White
    gt.fillText("You Lose!", 200, 200)
}
}
startItem.onAction = (e:ActionEvent) => {
  canvas.requestFocus()
  timer.start
}
exitItem.onAction = (e:ActionEvent) => sys.exit(0)
}
}
app.main(args)
```

# 使用 Scala 进行编程与问题解决

你可以在图 12.11 中看到这个游戏的样式。前 28 行是各种声明。后面带有 `Stage` 和 `Scene` 的 `app` 声明。第 35 到 46 行构建了一个简单的布局，顶部是 `MenuBar`，中间是 `Canvas`。

第 48 到 61 行建立了画布上的事件处理。鼠标点击和拖动向水洼添加元素。按键按下和释放改变变量的值。玩家的实际移动发生在 72 到 78 行的 `movePlayer` 函数中。这有两个优点：允许运动成为游戏正常计时的一部分，并轻松处理多个按键按下；它还允许对角线运动，如果我们在 `onKeyPressed` 处理程序中移动玩家，这是无法实现的。

第 64 到 103 行有一些辅助函数，仅用于拆分逻辑并使代码更易读易写。

第 105 到 140 行是 `AnimationTimer` 的声明，这是执行实际工作的地方。包含了移动玩家、敌人和蒸发水洼的辅助函数。它还包含定期间隔创建新敌人的代码。在该代码之后，代码将游戏实际绘制到画布的 `GraphicsContext`（存储在第 62 行的变量 `gt` 中）。它首先填充一个整个画布大小的黑色矩形，然后绘制水洼、敌人和玩家。如果玩家死亡，还会绘制文本消息。

## 线程处理

ScalaFX 的一个我们没有真正关注的方面是某些类型的更改只能在代码的某些部分进行。特别是，ScalaFX 有一个线程用于处理所有发生的事件和绘制。对线程的适当讨论超出了本书的范围（在《使用 Scala 的面向对象、抽象和数据结构》中有所介绍），但有时你需要考虑它。问题在于，你应该只在该线程内更改场景图中对象的值，或向 `GraphicsContext` 绘制。这意味着要么在事件处理器内部，要么在定时器内部（基本上是 ScalaFX 调用的东西）。如果你想在这些代码块之外更改值或绘制内容，你需要调度它在事件线程中运行。你可以通过调用 `Platform.runLater(op)` 实现，其中 `op` 是你放入其中的任何代码。

## 效果 12.7

ScalaFX 的另一个酷炫功能是允许将效果附加到节点上。这是 `scalafx.scene.effect` 包中列出的效果。感兴趣的读者被鼓励进一步研究这些主题。

- **Blend**: 这种效果决定了像素如何组合。默认情况下，绘制的像素会覆盖。你可以使用 `Blend(mode: BlendMode)` 创建。这里列出了不同的混合模式。
    - **Add**: 添加颜色值和透明度值。
    - **Blue**: 替换颜色的蓝色分量。
    - **ColorBurn**: 反转底部颜色，然后用顶部颜色除之，再次反转。
    - **ColorDodge**: 将底部颜色除以顶部颜色的反转。
    - **Darken**: 取两个输入中较暗的。
    - **Difference**: 从较亮的输入减去较暗的输入并显示结果。
    - **Exclusion**: 两个输入的颜色分量相乘并双倍。从底部颜色减去得到结果颜色。
    - **Green**: 替换颜色的绿色分量。
    - **HardLight**: 根据顶部输入颜色，输入颜色分量要么相乘要么变亮。
    - **Lighten**: 取两个输入中较亮的。
    - **Multiply**: 乘颜色分量以得到结果颜色。
    - **Overlay**: 根据底部输入颜色，输入颜色分量要么相乘要么变亮。
    - **Red**: 替换颜色的红色分量。
    - **Screen**: 将顶部和底部的颜色分量反转，乘以 1，然后反转得到结果颜色。
    - **SoftLight**: 底部颜色分量在顶部输入上变暗或变亮。
    - **SrcAtop**: 顶部输入位于底部输入内部的部分与底部输入混合。
    - **SrcOver**: 将输入叠加在底部输入之上。
- **Bloom**: 这让图像的较亮部分发光。你可以使用 `new Bloom(threshold: Double)` 创建。
- **BoxBlur**: 使用框形滤波器内核模糊图像。你使用 `new BoxBlur(width: Double, height: Double, iterations: Int)` 创建。宽度和高度指定了模糊区域的大小，迭代次数告诉应该处理多少次。次数越多，模糊越严重。

`ColorAdjust` - 此效果用于检测对色调、亮度和对比度的逐像素调整。你可以创建一个新的 `ColorAdjust(hue: Double, saturation: Double, brightness: Double, contrast: Double)`。

`ColorInput` - 渲染一个由灰色 `Paint` 填充的矩形区域。你可以创建一个新的 `ColorInput(x: Double, y: Double, width: Double, height: Double, paint: Paint)`。

`DisplacementMap` - 这会导致图像根据 `FlowMap`指定的偏移量进行渲染。这允许你执行诸如让 Node 呈现波状的操作。你可以创建一个新的 `DisplacementMap(mapData: FlowMap, offsetX: Double, offsetY: Double, scale: Double, scale: Double)` 或新的 `DisplacementMap(mapData: FlowMap)`。`FlowMap` 可以使用 `new FlowMap(width: Int, height: Int)` 创建，其中的值通过 `setDefs(x: Int, y: Int, s: Float, f: Unit)` 方法设置。

`DropShadow` - 给定内容根据指定的半径、偏移量和颜色渲染阴影。你可以创建一个新的 `DropShadow(radius: Double, offsetX: Double, offsetY: Double, color: Color)`、新的 `DropShadow(radius: Double, color: Color)` 或新的 `DropShadow(blurType: BlurType, color: Color, radius: Double, spread: Double, offsetX: Double, offsetY: Double)`。`BlurType` 可以是四个值之一：`BlurType.Gaussian`、`BlurType.OnePassBox`、`BlurType.ThreePassBox`、`BlurType.TwoPassBox`。

`GaussianBlur` - 使用指定半径的高斯函数对图像模糊。你可以创建一个新的 `GaussianBlur(radius: Double)`。

`Glow` - 让图像看起来在发光。你可以通过 `new Glow(level: Double)` 创建一个。

`InnerShadow` - 在某些内容的边缘内部根据指定的半径、偏移量和颜色渲染阴影。你可以创建一个新的 `InnerShadow(radius: Double, offsetX: Double, offsetY: Double, color: Color)`、新的 `InnerShadow(radius: Double, color: Color)` 或新的 `InnerShadow(blurType: BlurType, color: Color, radius: Double, choke: Double, offsetX: Double, offsetY: Double)`。`BlurType` 是与 `DropShadow` 使用的相同的值之一。

`Lighting` - 创建光线照射在元素上的效果，使其看起来更真实。你可以创建一个新的 `Lighting(light: Light)`。`Light` 类型通过实例化三个子类型之一创建：`Light.Distant`、`Light.Point` 或 `Light.Spot`。这些可以使用以下调用完成：

- `new Light.Distant (azimuth: Double, elevation: Double; color: Double, color: Color)`
- `new Light.Point (x: Double, y: Double, z: Double, color: Color)`

> ⁸ `FlowMap` 类型的不同“带”可以用于不同的地方。`DisplacementMap` 分别使用两个带用于 x 和 y 值。

> ⁹ 这些是编写本文时使用的名称。ScalaFX 的开发者似乎正在转向驼峰命名法，因此未来这些这些可能会被改为 `Gaussian`、`OnePassBox`、`ThreePassBox` 和 `TwoPassBox`。

# 图形与高级 ScalaFX

- `new Light.Spot(x: Double, y: Double, specularExponent: Double, color: Color)`

- `MotionBlur` - 创建由于运动引起的模糊效果。你可以通过 `new MotionBlur(angle: Double, radius: Double)` 创建一个。角度指定了感知的运动方向，半径告诉它需要多大的模糊。

- `PerspectiveTransform` - 此效果无法通过仿射变换实现，在透视视图中，平行线在远处似乎相交。你可以通过 `new PerspectiveTransform(ulx: Double, uly: Double, urx: Double, ury: Double, lx: Double, lry: Double, llx: Double, lly: Double)` 创建一个，传递的 `vals` 用于指定要映射的四边形或 Node 角的位置。

- `Reflection` - 这在实际内容下方渲染一个 Node的反射版本。你可以使用 `new Reflection(topOffset: Double, fraction: Double, topOpacity: Double, bottomOpacity: Double)` 创建一个。透明度允许反射具有渐变效果。

- `SepiaTone` - 对图像应用深褐色调颜色。你可以通过 `new SepiaTone(level: Double)` 创建一个。

- `Shadow` - 为其附带的 Node 创建阴影。与 `DropShadow` 不同，它不会同时显示原始内容和阴影。你可以通过 `new Shadow(radius: Double, color: Color)` 或 `new Shadow(blurType: BlurType, color: Color, radius: Double)` 创建一个。`BlurType` 具有与 `DropShadow` 中提到的相同的选项。

对这些内容的精通用法在下面的代码中显示。特别是，这段代码显示了适用于文本的效果。对图像效果最好的显示在第 12.3 节。

# 列表 12.11: Effects.scala

```
import scalafx.Includes.
import scalafx.application.JFXApp
import scalafx.scene.
import scalafx.scene.effect.
import scalafx.scene.paint.
import scalafx.scene.shape.
import scalafx.scene.text.

def makeText(x: Double, y: Double, s: String, effect: Effect, darkBack: Boolean):Node = {
 val text = new Text(x, y, s)
text.font = Font("serif", FontWeight.Bold, 40)
text.effect = effect
if (darkBack) {
 val group = new Group
val r = new Rectangle(text.bounds)
r.fill = Color.Black
group.children.addAll(r, text)
group
} else {
  text
}
}

val app = new JFXApp {
  stage = new Stage {
    scene = new Scene {
      val root = new VBox(10) {
        val bloom = makeText(20, 40, "Bloom", new Bloom(), true)
```
