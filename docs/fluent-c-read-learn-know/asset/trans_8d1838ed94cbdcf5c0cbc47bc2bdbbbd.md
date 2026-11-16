

## 戴上你的思考帽

是时候扩展画笔资源管理器了。你需要两个标签页；我的版本如下。这次，我希望你使用资源管理器来弄清楚每个属性的作用。（可以参考 MSDN 获取一些指导，但尽量通过实验来弄清楚它们的作用。）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_698_0.png)

要获取一个可用的图像，将其添加到项目中，然后将画笔的 `ImageSource` 属性设置为其名称。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_698_1.png)

## ImageBrush 属性

当 `Stretch` 属性设置为 `Fill` 时，调整窗口大小会对图像产生什么影响？

当 `Stretch` 属性设置为 `Uniform` 时，这种行为有何不同？我的示例图像是正方形，因此 `Uniform` 和 `UniformToFill` 之间没有区别。当你使用矩形图像时会发生什么？

要查看 `AlignmentX` 和 `AlignmentY` 属性的效果，`Stretch` 属性需要设置为什么？

Viewbox 的宽度和高度设置为多少才能仅显示图像的左上角？

## TileBrush 属性

如果不更改 Viewport，将 TileMode 设置为 Tile 会发生什么？

将 TileMode 设置为 None 且 Viewport 设置为默认值时会发生什么？

FlipX 有什么作用？FlipY 呢？FlipXY 呢？

## 你做得怎么样？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_700_0.png)

## ImageBrush 属性

当 `Stretch` 属性设置为 `Fill` 时，调整窗口大小会对图像产生什么影响？

图像会变形以填充空间。

当 `Stretch` 属性设置为 `Uniform` 时，这种行为有何不同？我的示例图像是正方形，因此 `Uniform` 和 `UniformToFill` 之间没有区别。当你使用矩形图像时会发生什么？

图像会调整大小，但保持宽高比。

要查看 `AlignmentX` 和 `AlignmentY` 属性的效果，`Stretch` 属性需要设置为什么？

None。

Viewbox 的宽度和高度设置为多少才能仅显示图像的左上角？

两者均为 0.5。

## TileBrush 属性

如果不更改 Viewport，将 TileMode 设置为 Tile 会发生什么？

没有任何变化。

将 TileMode 设置为 None 且 Viewport 设置为默认值时会发生什么？

仅显示一张小图像。

FlipX 有什么作用？FlipY 呢？FlipXY 呢？

翻转每隔一个平铺块

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_700_1.png)

## 休息一下

画笔部分到此结束。在完成复习并进入 Pens（简单得多）之前，为什么不休息一下呢？

## 复习

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_701_0.png)

使用 RadialGradientBrush 时，你可以在 0.25 处添加一个渐变停止点，并将 RadiusX 属性设置为 0.25。这两个值都表示“四分之一处”——但分别指的是什么？（在每种情况下都不同。）

ARGB 代表什么字母？

为了确保始终显示整个内容，应该给 TileBrush 的 ViewportUnits 属性设置什么值？

如果一个边界框的宽度是长度的两倍，那么其左下角的 x 和 y 坐标分别是多少？

当渐变轴未到达边界框边缘时，你设置哪个属性来控制显示哪些颜色？

ScRGB 和 SRGB 有什么区别？

围绕圆形对象的边界框是什么形状？

我们的资源管理器标签页会受益于一个重置函数，该函数将标签页上的所有值恢复为默认值。在一个或多个标签页上添加一个重置按钮。

## 画笔（Pens）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_702_0.png)

WPF Pen 用于绘制线。我相信你会很高兴地知道，它远不如 Brush 复杂。只有一个类（如果需要，你也可以派生自己的类），以及几个属性。

你可以使用任何类型的画笔来绘制 Pen。我们将在下一个练习中使用渐变，但你可以使用纯色画笔、图像，或者任何适合你目的的东西。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_702_1.png)

- Flat
- Square
- Round
- Triangle

DashCap、StartLineCap 和 EndLineCap 控制线条或虚线末端的形状。不幸的是，你无法定义自己的端点样式来显示，例如箭头。你必须从 Pen.LineCap 枚举中定义的样式中选择一个。

LineJoin 属性控制 Pen 转弯时发生的情况。同样，你无法定义自己的样式；必须使用 Pen.LineJoin 枚举的成员。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_703_0.png)

就像用于 SolidColorBrush 的 Colors 类一样，框架定义了一组可供使用的有用虚线样式。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_703_1.png)

你可以定义自己的虚线样式。DashStyle 类的 Dashes 集合包含一组 Double 值，表示 Pen 的 Thickness 的百分比。

Solid（默认值）
那只棕色的懒狗。

### Dot (0.2) Dash (2,2)

那只棕色的懒狗，那只棕色的懒狗。

### DashDotDot (2.2,0.2,0.2) DashDot (2.2,0.2)

那只棕色的懒狗。那只棕色的懒狗。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_703_2.png)

MiterLimit 属性控制斜接可以延伸多远。它表示为 Pen 宽度的百分比。

## 文本装饰（Text Decorations）

在 WPF 中，画笔主要用于定义图形形状，但当你想要使用带有 Pen 作为属性的 TextDecoration 类来给文本添加下划线或删除线等“装饰”时，也会用到它们。TextBlock 是一个公开 TextDecorations 集合的控件，我们将使用它来探索 Pen 的属性。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_704_0.png)

Location 属性决定装饰将显示在何处。

TextDecorations 是一个集合，因此你的文本可以，例如，同时显示下划线和删除线。

PenOffset 属性将装饰从其默认位置向上或向下移动。

TextDecorationUnit（由 PenOffsetUnit 和 PenThicknessUnit 使用）允许你确定如何解释 PenThickness 和 PenOffset 属性。

## 戴上你的思考帽

回到我们的资源管理器。你能复制（或改进）我的版本吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_705_0.png)

这是一个 TextBlock。LinearGradientBrush 在 XAML 中声明并显示为下划线，因为这是 TextDecoration 的默认行为。引用画笔的等效 C# 代码是：

```
TextBlock.TextDecorations[0].TextDecoration.Pen.Brush
```

XAML 语法在下一页的解决方案中，但看看你能否在没有帮助的情况下弄清楚如何操作。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_705_1.png)

在代码中，请记住，除了 Location 之外的所有控件都表示 TextDecoration.Pen 的属性，而不是装饰本身。

一旦让示例正常工作，你能识别出这些线条各自的位置吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_705_2.png)

## 你做得怎么样？

这个练习比我们的其他示例稍微棘手一些，因为你正在处理嵌套对象。以下是设置该初始渐变的 XAML：

```
<TextBlock ... >
    <TextBlock.TextDecorations>
        <TextDecoration x:Name="Decoration">
            <TextDecoration.Pen>
                <Pen>
                    <Pen.Brush>
                        <LinearGradientBrush>
                            <GradientStop ... />
                            <GradientStop ... />
                            <GradientStop ... />
                        </LinearGradientBrush>
                    </Pen.Brush>
                </Pen>
            </TextDecoration.Pen>
        </TextDecoration>
    </TextBlock.TextDecorations>
</TextBlock>
```

```
if (endSquare.IsChecked == true)
{
    Decoration.Pen.StartLineCap =
    PenLineCap.Square;
    Decoration.Pen.EndLineCap =
    PenLineCap.Square;
}
```

以下是一个代码片段，向你展示如何在按钮的 Click 事件处理程序中设置更改画笔属性。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_706_0.png)

## 休息一下

这是一个棘手的练习，可能花费了你一些时间，所以在我们深入探索 WPF 文本之前，为什么不休息一下呢？

