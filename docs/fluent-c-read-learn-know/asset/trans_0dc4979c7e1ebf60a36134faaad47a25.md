

## 示例

令人惊讶的是，有那么多依赖属性被定义为双精度浮点数，所以让我们来看一个简单的 DoubleAnimation 示例，只是为了了解你能做什么（当然，也包括如何做到。）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_756_0.png)

By 允许你指定一个相对量，从当前值中加上（如果是负数则减去）该量。

From 和 To 允许你为属性设置绝对的起始值和结束值。

请记住，DoubleAnimation 继承了 Timeline 的属性，因此它也公开了 Duration 和 AccelerationRatio 等属性。

你可以将缓动函数视为 AccelerationRatio 和 DecelerationRatio 的更高级版本，它允许你做出诸如让动画弹跳之类的效果。

IsAdditive 和 IsCumulative 决定动画是从属性的“原生”值开始，还是在应用任何先前动画后从其当前值开始。

## 更进一步

事实上，WPF 动画有如此多的旋钮和按钮可供调整，以至于从头开始编写代码可能很困难，对于任何非常棘手的东西，你都需要进行大量实验。（如果你打算做大量动画，你可能会想探索 Microsoft Expression Blend，它具有定义各种复杂分镜的绝佳交互式工具。）

## 动动脑筋

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_757_0.png)

这里有一对简单的动画，当鼠标进入和离开按钮时会改变按钮的大小。在 StackPanel 内创建一个带有几个按钮的新项目，将样式添加到 app.xaml 文件的 `<Resources>` 元素中，然后回答下面的问题。

```
<Style TargetType="Button">
<Style.Triggers>
<EventTrigger RoutedEvent="Button.MouseEnter">
<BeginStoryboard>
<Storyboard>
<DoubleAnimation Storyboard.TargetProperty="FontSize" To="36" />
<DoubleAnimation Storyboard.TargetProperty="Height" To="75" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
<EventTrigger RoutedEvent="Button.MouseLeave">
<BeginStoryboard>
<Storyboard >
<DoubleAnimation Storyboard.TargetProperty="FontSize" />
<DoubleAnimation Storyboard.TargetProperty="Height" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Style.Triggers>
</Style>
```

通过省略 From 属性，动画将从属性的当前值开始。

你可以使用附加的 TargetProperty 为每个 Timeline 指定不同的目标。

通过同时省略 From 和 To，动画将属性返回到其原始值。

- 除非你显式设置按钮的 Height 属性，否则动画将无法工作。你能想出原因吗？
- 如果将 MouseEnter 动画的 Height 属性更改为 By="25"，然后在动画完成恢复到原始大小之前重新进入按钮，会发生什么？你能想到哪些情况下这可能是你想要的行为吗？
- 尝试将缓动函数添加到 MouseEnter Storyboard 的 Height 动画中。框架定义了几个。（Intellisense 会在此处帮助你。）你认为哪个在此情况下最合适？
- 当你将 TargetProperty 设置为附加属性时，需要用括号括起来：Foreground.(SolidColorBrush.Color)。使用此语法，尝试添加一个更改文本颜色的 ColorAnimation。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_757_1.png)

## 你做得怎么样？

这次有很多东西需要你去弄明白，不是吗？除了让你有机会构建一些动画之外，这个练习让你体验了一下程序员经常做的事情：从一些不太符合你要求的示例代码开始，将其改造成你需要的样子，并在遇到问题时逐一解决。

除非你显式设置按钮的 Height 属性，否则动画将无法工作。你能想出原因吗？

如果你没有弄明白这一点，也不要难过。还记得我们讨论过 WPF 除非你显式设置属性值，否则不会为属性创建存储空间吗？情况就是这样。如果你不显式设置 Width 属性，它就没有值，WPF 会将其报告为 NaN（"not a number" 的缩写），而 DoubleAnimation 不知道如何处理非数字的东西。你需要小心，确保你试图动画化的属性实际上存在于目标元素上。做到这一点的一种方法是将它们包含在元素模板中。我们将在下一章中看到如何做到这一点。

如果将 MouseEnter 动画的 Height 属性更改为 By="25"，然后在动画完成恢复到原始大小之前重新进入按钮，会发生什么？你能想到哪些情况下这可能是你想要的行为吗？

因为我们没有设置 From 属性，动画总是从当前值开始。动画的原始版本在 To 属性中指定了一个绝对值，那就是动画的最大值。改为设置 By 只是在当前值的基础上加 25，因此按钮会越来越大、越来越大、越来越大。

这种行为在我们的示例中不合适，但有时可能很有用，尽管由于重入问题，可能不适用于 MouseEnter 触发器。但是，如果你希望用户能够通过单击元素来设置一组元素的相对重要性，那会怎样呢？每次单击时让元素变大，这正是你想要的。

将缓动函数添加到 MouseEnter Storyboard 的 Height 动画中。你认为哪个在此情况下最合适？

```
<DoubleAnimation Storyboard.TargetProperty="Height" To="75" >
    <DoubleAnimation.EasingFunction>
        <BackEase />
    </DoubleAnimation.EasingFunction>
</DoubleAnimation>
```

每个缓动函数都公开了一些属性来控制它们，但它们在默认配置下也能工作得相当好。

缓动函数难道不有趣吗？我认为在此处 BackEase 最好，但这只是个人判断，你可能更喜欢另一个。

当你将 TargetProperty 设置为附加属性时，需要用括号括起来：Foreground.(SolidColorBrush.Color)。使用此语法，尝试添加一个更改文本颜色的 ColorAnimation。

```
<ColorAnimation Storyboard.TargetProperty="Foreground.(SolidColorBrush.Color)" To="Green" />
```

在此示例中，(Foreground).(SolidColorBrush.Color) 有效，但 (Foreground).(SolidColorBrush).(Color) 无效，因为 Color 不是附加属性。有时只需通过少量试错来确定确切的语法。

## 转换

即使你的应用程序不涉及狡猾的小兔子，你也经常希望在动画中移动元素。如你所见，你可以使用 DoubleAnimation 更改 Width 和 Height 属性，但这只能让你更改大小；它不允许你旋转或倾斜元素之类的操作。此外，对 Width 和 Height 的更改总是会导致其容器重新排列子元素，而这可能不是你想要的。解决方案是 System.Windows.Media 命名空间中的转换类。有四种基本转换

### ROTATETRANSFORM

围绕你可以指定的中心点旋转元素。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_760_0.png)

### 做个笔记

WPF 还有一个 MatrixTransform 类，允许你将这四种转换的任意组合指定为 3x3 仿射变换，适合喜欢这种东西的人。（等我把烤箱清理干净后再找我。）

### TRANSLATETRANSFORM

水平或垂直移动元素。

### SCALETRANSFORM

更改元素的大小。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_761_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_761_2.png)

### SKEWTRANSFORM

围绕你可以指定的中心点水平或垂直倾斜元素。

