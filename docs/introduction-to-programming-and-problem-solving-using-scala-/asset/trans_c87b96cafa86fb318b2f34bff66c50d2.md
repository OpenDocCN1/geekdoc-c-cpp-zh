

ColorAdjust - 此效果用于检测对色调、亮度和对比度的逐像素调整。你可以创建一个新的 `ColorAdjust(hue: Double, saturation: Double, brightness: Double, contrast: Double)`。

ColorInput - 渲染一个由灰色 `Paint` 填充的矩形区域。你可以创建一个新的 `ColorInput(x: Double, y: Double, width: Double, height: Double, paint: Paint)`。

DisplacementMap - 这会导致图像根据 `FlowMap`指定的偏移量进行渲染。这允许你执行诸如让 Node 呈现波状的操作。你可以创建一个新的 `DisplacementMap(mapData: FlowMap, offsetX: Double, offsetY: Double, scale: Double, scale: Double)` 或新的 `DisplacementMap(mapData: FlowMap)`。`FlowMap` 可以使用 `new FlowMap(width: Int, height: Int)` 创建，其中的值通过 `setDefs(x: Int, y: Int, s: Float, f: Unit)` 方法设置。

DropShadow - 给定内容根据指定的半径、偏移量和颜色渲染阴影。你可以创建一个新的 `DropShadow(radius: Double, offsetX: Double, offsetY: Double, color: Color)`、新的 `DropShadow(radius: Double, color: Color)` 或新的 `DropShadow(blurType: BlurType, color: Color, radius: Double, spread: Double, offsetX: Double, offsetY: Double)`。`BlurType` 可以是四个值之一：`BlurType.Gaussian`、`BlurType.OnePassBox`、`BlurType.ThreePassBox`、`BlurType.TwoPassBox`。

GaussianBlur - 使用指定半径的高斯函数对图像模糊。你可以创建一个新的 `GaussianBlur(radius: Double)`。

Glow - 让图像看起来在发光。你可以通过 `new Glow(level: Double)` 创建一个。

InnerShadow - 在某些内容的边缘内部根据指定的半径、偏移量和颜色渲染阴影。你可以创建一个新的 `InnerShadow(radius: Double, offsetX: Double, offsetY: Double, color: Color)`、新的 `InnerShadow(radius: Double, color: Color)` 或新的 `InnerShadow(blurType: BlurType, color: Color, radius: Double, choke: Double, offsetX: Double, offsetY: Double)`。`BlurType` 是与 `DropShadow` 使用的相同的值之一。

Lighting - 创建光线照射在元素上的效果，使其看起来更真实。你可以创建一个新的 `Lighting(light: Light)`。`Light` 类型通过实例化三个子类型之一创建：`Light.Distant`、`Light.Point` 或 `Light.Spot`。这些可以使用以下调用完成：

- `new Light.Distant (azimuth: Double, elevation: Double; color: Double, color: Color)`
- `new Light.Point (x: Double, y: Double, z: Double, color: Color)`

> ⁸ `FlowMap` 类型的不同“带”可以用于不同的地方。`DisplacementMap` 分别使用两个带用于 x 和 y 值。

> ⁹ 这些是编写本文时使用的名称。ScalaFX 的开发者似乎正在转向驼峰命名法，因此未来这些这些可能会被改为 `Gaussian`、`OnePassBox`、`ThreePassBox` 和 `TwoPassBox`。

# 图形与高级 ScalaFX

- `new Light.Spot(x: Double, y: Double, specularExponent: Double, color: Color)`

- MotionBlur - 创建由于运动引起的模糊效果。你可以通过 `new MotionBlur(angle: Double, radius: Double)` 创建一个。角度指定了感知的运动方向，半径告诉它需要多大的模糊。

- PerspectiveTransform - 此效果无法通过仿射变换实现，在透视视图中，平行线在远处似乎相交。你可以通过 `new PerspectiveTransform(ulx: Double, uly: Double, urx: Double, ury: Double, lx: Double, lry: Double, llx: Double, lly: Double)` 创建一个，传递的 `vals` 用于指定要映射的四边形或 Node 角的位置。

- Reflection - 这在实际内容下方渲染一个 Node的反射版本。你可以使用 `new Reflection(topOffset: Double, fraction: Double, topOpacity: Double, bottomOpacity: Double)` 创建一个。透明度允许反射具有渐变效果。

- SepiaTone - 对图像应用深褐色调颜色。你可以通过 `new SepiaTone(level: Double)` 创建一个。

- Shadow - 为其附带的 Node 创建阴影。与 `DropShadow` 不同，它不会同时显示原始内容和阴影。你可以通过 `new Shadow(radius: Double, color: Color)` 或 `new Shadow(blurType: BlurType, color: Color, radius: Double)` 创建一个。`BlurType` 具有与 `DropShadow` 中提到的相同的选项。

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

# 列表 12.12: ImageEffects.scala

该程序的输出见图 12.13.¹1⁰

