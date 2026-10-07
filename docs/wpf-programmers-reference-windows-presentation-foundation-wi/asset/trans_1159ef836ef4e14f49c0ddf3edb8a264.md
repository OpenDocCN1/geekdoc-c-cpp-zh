
各种旋转标签都是围绕其左上角旋转的。

显示“Matrix”（矩阵）的标签使用矩阵来定义其变换。

## 组合变换

你可以使用旋转、缩放、倾斜和平移变换的任意组合来变换任何对象。要创建一个组合变换，请使用 `TransformGroup` 而不是单个变换对象。在组内部，你可以按照任何顺序放置其他变换。

例如，以下代码显示了一个用于 `Grid` 控件的 `TransformGroup`，它包含一个平移后跟一个旋转：

```
<Grid.RenderTransform>
<TransformGroup>
<TranslateTransform X="150" Y="0"/>
<RotateTransform Angle="60"/>
</TransformGroup>
</Grid.RenderTransform>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_398_0.png)

### 组合变换

注意，一组变换的顺序非常重要。如果你更改了变换的顺序，将得到不同的结果。

图 20-2 所示的 `CombinedTransformations` 示例显示了一个 `Border`（作为一个大型黑色边框矩形），它包含一个 `Canvas`。`Canvas` 包含了几个具有不同变换的对象。`Border` 和 `Canvas` 都没有将 `ClipBounds` 设置为 `True`，因此即使对象超出了 `Canvas` 和 `Border`，它们也是可见的。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_398_1.png)

由于对象包含在画布（canvas）内部，且画布填充了边框，因此对象的起点位于边框的左上角。

白色对象 0 是经过变换的对象。蓝色对象 1 经过了平移，蓝色对象 2 经过平移后进行了旋转。

绿色对象 1 经过旋转，绿色对象 2 经过旋转后进行了平移。

标记为 2 的两个对象使用了相同的旋转和平移，但顺序不同，产生了截然不同的结果。

> 中心化建议
> 从创建一个以原点为中心的对象开始，构建你所需的变换是最简单的。这样在将其平移到最终位置之前，你可以轻松地围绕其中心进行缩放、旋转或倾斜。

## 布局变换与渲染变换

WPF 控件有两个变换属性：`LayoutTransform` 和 `RenderTransform`。

WPF 在窗口上安排该控件和其他其他控件之前应用控件的 `LayoutTransform`。然后，它使用变换后控件的新宽度和高度来计算位置。例如，如果你将一个正方形旋转 45 度，结果是一个比原始更宽、更高的菱形。如果将正方形放在 `StackPanel` 中，`StackPanel` 将留出足够的空间让旋转后的正方形能够适应。

WPF 在控件安排之后、绘制之前应用 `RenderTransform`。这在排列如 `StackPanel` 和 `WrapPanel` 等控件时可能会产生一些奇怪的结果，导致控件超出它们所分配区域的边缘。

然而，如果控件的容器不使用控件的大小来排列子控件，`RenderTransforms` 就能良好工作。例如，`Canvas` 不使用控件的大小来排列控件，因此 `RenderTransforms` 在那里可以正常工作。

> 平移的复杂性
> 根据控件容器的不同，变换有时会产生意料之外的结果，或者可能没有明显的效果。

例如，假设你在 `Grid` 内部放置一个 `Label` 并给它一个变换。WPF 平移了该 `Label`，但将其在 `Grid` 中居中，因此它显示的位置与你没有特意平移时的位置一样。

在这种情况下，使用 `RenderTransform` 而不是 `LayoutTransform`，或者将控件移动到 `Canvas` 中更容易得到结果。

图 20-3 显示的 `LayoutVsRender` 示例程序演示了 `LayoutTransform` 和 `RenderTransform` 属性之间的区别。

左侧的 `StackPanel` 包含三个使用 `LayoutTransforms` 旋转的 `Label`，因此 `StackPanel` 为每个旋转的 `Label` 留出了足够的高度。在为 `Label` 留空间后，`StackPanel` 将每一个居中。

右侧的 `StackPanel` 包含三个使用 `RenderTransform` 旋转的 `Label`。`StackPanel` 只为每个 `Label` 在旋转前留出足够的垂直空间，然后无论 `Label` 是否超出空间都直接放入它们。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_399_0.png)

图 20-3

## 尺寸宽度

注意图 20-3 中右侧的 `Label` 如何延伸以匹配 `StackPanel` 的宽度，而左侧的那些则调整大小以适应其内容。

通常，`StackPanel` 会拉伸它的 `Label` 以适应宽度。然而，当使用图 20-3 左侧的 `Label` 时，`Layout Transforms` 在 `Label` 被拉伸之前应用，因此 `Label` 获得了它们期望的适应内容尺寸。相比之下，图 20-3 右侧的 `StackPanel` 先排列 `Label` 并将其拉伸，然后只返回结果。

## 效果

变换会修改对象的几何形状，而位图效果（bitmap effects）则修改对象绘制的方式。

要向对象添加效果，请给它提供一个包含效果元素的 `BitmapEffect` 属性元素。例如，以下代码定义了一个包含椭圆（Ellipse）和路径（Path）的 `Canvas`。

```
<Canvas Width="100" Height="100">
<Canvas.BitmapEffect>
  <DropShadowBitmapEffect />
</Canvas.BitmapEffect>
  <Ellipse Stroke="Blue" Fill="Yellow" Width="100" Height="100"/>
  <Path Data="M 20,50 A 30,30 0 0,1 80,50" Stroke="Blue" StrokeThickness="2"/>
</Canvas>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_400_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_400_1.png)

由于变换修改了对象的几何形状，位图效果修改了对象绘制的方式。

要向对象添加效果，请给它提供一个包含效果元素的 `BitmapEffect` 属性元素。例如，以下代码定义了一个包含椭圆和路径的 `Canvas`。 (此处为重复翻译内容，根据逻辑处理)

以下列表总结了 WPF 的位图效果类：

- **Bevel**（倒角）：添加边缘。该效果具有几个重要属性。`BorderWidth` 决定倒角边缘。`LightAngle` 决定光线照射倒角边缘的角度。`Relief` 决定凹凸。`Smoothness` 决定平滑度。
- **Blur**（模糊）：模糊对象。`Radius` 决定模糊范围。
- **DropShadow**（投影投影）：在对象后面添加阴影。该效果最有用的属性是 `Color`（决定阴影颜色）和 `Direction`（决定阴影方向）。`ShadowDepth` 决定阴影深度。
- **Emboss**（浮雕）：在对象周围添加光。
- **OuterGlow**（外光）：在对象周围添加光。`GlowSize` 决定光的大小。`GlowColor` 决定光的颜色。

如果你想同时使用多个效果，请使用一个包含 `BitmapGroup` 的 `BitmapEffect` 元素。在 `BitmapGroup` 内部放置使用的效果。例如，以下代码使用了 `EmbossBitmapEffect` 后跟 `BevelBitmapEffect`。

```
<Canvas.BitmapEffect>
  <BitmapGroup>
    <EmbossBitmapEffect />
    <BevelBitmapEffect BevelWidth="10"/>
  </BitmapGroup>
</Canvas.BitmapEffect>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_401_0.png)

## 第20 章 变换与效果

## 有效的效果

> 注意效果的顺序。通常，以不同顺序应用效果会产生不同的结果。

图 20-4 所示的 `Effects` 示例显示了一个未修改的对象以及使用五种基础位图效果的相同对象。右下方的两个版本显示了组合效果的对象。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_401_1.png) (此处重复)

`BevelBitmapEffect` 类的 `EdgeProfile` 属性决定倒角边缘的精确形状。图 20-5 所示的 `BevelEffects` 示例演示了该属性的所有可能值。

## 效果 | 365

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_402_0.png)

图 20-5

所有的位图效果仅作用于可见的像素。如果某个区域未填充或填充颜色为透明（Transparent），则该效果将忽略该区域。

> 填充内容
> 要让一个区域未填充，通常只需不填充即可。例如，如果不指定 `Ellipse` 的 `Fill` 属性，那么 `Ellipse` 就是未填充的。
> 要显式地让一个区域未填充，请在 XAML 代码中使用 `(x:Null)`，在 C# 中使用 `null`，在 Visual Basic 中使用 `Nothing`。

图 20-6 所示的 `TransparentEffects` 示例程序绘制的笑脸与 `Effects` 程序绘制的相似，只是主椭圆是透明的而不是黄色。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_402_1.png)

图 20-6

图 20-6 所示的效果仅使用实际绘制的像素。这对于模糊、投影投影和外光效果看起来是合理的，但对于倒角和浮雕效果看起来并不那么好。倒角和浮雕效果需要填充区域来发挥作用，在此示例中作用不大。（你仍然可以在眼睛和鼻子处看到它们的效果，因为它们是填充的。）
