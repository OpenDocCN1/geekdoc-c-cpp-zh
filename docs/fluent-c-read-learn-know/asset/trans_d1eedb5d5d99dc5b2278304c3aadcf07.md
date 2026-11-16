

## FLUENTDICTIONARY.XAML

```xml
<ResourceDictionary ... >
<GradientStopCollection x:Key="Stops">
<GradientStop Offset="0" Color="AntiqueWhite" />
...
</GradientStopCollection>
<Style x:Key="windowStyle" TargetType="Window">
<Setter Property="Background" Value="AntiqueWhite" />
<LinearGradientBrush GradientStops="{StaticResource Stops}" />
</Setter>
<Setter Property="FontFamily" Value="Arial" />
<Setter Property="FontSize" Value="14" />
</Style>
<Style TargetType="Button">
<Setter Property="Background" Value="AntiqueWhite" />
<Setter Property="Margin" Value="5" />
<Setter Property="Padding" Value="2" />
</Style>
<Style x:Key="BasicLabel" TargetType="Label">
<Setter Property="Margin" Value="5" />
<Setter Property="HorizontalAlignment" Value="Right" />
<Setter Property="VerticalAlignment" Value="Center" />
<Setter Property="FontWeight" Value="Black" />
</Style>
<Style x:Key="RequiredLabel" TargetType="Label">
<Setter Property="Margin" Value="5" />
<Setter Property="HorizontalAlignment" Value="Right" />
<Setter Property="VerticalAlignment" Value="Center" />
<Setter Property="FontWeight" Value="Black" />
<Setter Property="Foreground" Value="Chocolate" />
</Style>
</ResourceDictionary>
```

如果你没有偷看就搞明白了，给自己奖励几颗金星。这很棘手！

这看起来有问题吗？它能工作，但存在大量重复，而我们总是希望避免这种情况。我们将在下一页介绍几种消除重复的方法。

你在这里需要 key，因为存在 .NET 4.0 的背景错误。

通过在此处设置文本特性，窗口内的元素将继承这些特性。

## 样式层次结构

在上一个练习的解决方案中，我为 Label 元素创建了两个不同的样式，并指出存在大量重复。Style.BasedOn 属性可以让你避免重复：

### 而不是：

```xml
<Style x:Key="BasicLabel" TargetType="Label">
<Setter Property="Margin" Value="5" />
<Setter Property="HorizontalAlignment" Value="Right" />
<Setter Property="VerticalAlignment" Value="Center" />
<Setter Property="FontWeight" Value="Black" />
</Style>

<Style x:Key="RequiredLabel" TargetType="Label">
<Setter Property="Margin" Value="5" />
<Setter Property="HorizontalAlignment" Value="Right" />
<Setter Property="VerticalAlignment" Value="Center" />
<Setter Property="FontWeight" Value="Black" />
<Setter Property="Label.Foreground" Value="Chocolate" />
</Style>
```

### BasedOn 让我们这样做：

你可以在基于另一个样式的样式中指定 TargetType，但它必须是相同的类型，或原始类型的派生类型。

```xml
<Style x:Key="BasicLabel" TargetType="Label">
<Setter Property="Margin" Value="5" />
<Setter Property="HorizontalAlignment" Value="Right" />
<Setter Property="VerticalAlignment" Value="Center" />
<Setter Property="FontWeight" Value="Black" />
</Style>

<Style x:Key="RequiredLabel" BasedOn="{StaticResource BasicLabel}" TargetType="Label">
<Setter Property="Foreground" Value="Chocolate" />
</Style>
```

使用带有 key 的 BasedOn 属性更好，但这意味着父样式不能是隐式的。幸运的是，BasedOn 属性也可以使用 x:Type 标记扩展引用类型：

```xml
<Style TargetType="Label">
    <Setter Property="Margin" Value="5" />
    <Setter Property="HorizontalAlignment" Value="Right" />
    <Setter Property="VerticalAlignment" Value="Center" />
    <Setter Property="FontWeight" Value="Black" />
</Style>
```

```xml
<Style x:Key="RequiredLabel" BasedOn="{StaticResource {x:Type Label}}"
    TargetType="Label">
    <Setter Property="Label.Foreground" Value="Chocolate" />
</Style>
```

当你使用 x:Type 引用隐式类型时，必须指定 TargetType，并且它必须是相同的类型或子类型。

请注意，使用 x:Type 时需要另一组大括号。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_739_0.png)

## 自己动手

使用 BasedOn 编辑你的示例应用程序以消除重复定义。尝试在不查看此处示例的情况下完成。

运行应用程序测试更改时，将鼠标悬停在一个按钮上。它们会改变颜色，但不会变成你为渐变选择的颜色。你认为如何修复这个问题？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_739_1.png)

## 休息一下

更新示例后，在我们继续学习触发器之前，为什么不休息一下呢？

## 属性触发器

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_740_0.png)

基本样式有很多好处。它们有助于确保视觉一致性，使将图形移交给不同团队更加容易，并减少重复代码。但它们有一个缺点：每个客户只有一个样式。许多元素，如 Button，实际上有多种外观，具体取决于各种条件，例如它们是否被选中或用户是否将鼠标悬停在其上。解决方法是 Style 对象公开的 Triggers 集合。

有三种触发器。属性触发器（PROPERTY TRIGGERS），我们将在本节中研究，当属性具有指定值时应用。事件触发器（EVENT TRIGGERS），我们将在下一节中研究，当事件发生时应用其值。最后，数据触发器（DATA TRIGGERS）类似于属性触发器，但基于绑定值。我们将在第 22 章中研究这些。

触发器和常规 Setter 元素可以在 Style 中共存。

```xml
<Style ...>
<Setter ...>
...
<Style.Triggers>
<Trigger Property="IsMouseOver" Value="True">
<Setter ...>
...
<EnterActions>...</EnterActions>
<ExitActions>...</ExitActions>
</Trigger>
</Style.Triggers>
</Style>
```

Trigger 属性可以是任何依赖属性。你通常会使用表示状态的 Is-Something 属性。

触发器包含一组 Setter 对象。它们与 Style 的 Setters 集合中包含的对象相同。

触发器公开两组 TriggerAction 对象，当元素变为活动或非活动状态时将执行这些对象。我们将在下一节中研究 TriggerAction。

## 动动脑筋...

尝试将一些触发器添加到我们一直在使用的 FluentDictionary 中来试用触发器。

- 1. 向 TextBox 添加一个触发器，使其在获得焦点时将 FontStyle 设置为 Italic。触发属性不是 IsSelected。那是什么？（你可以查看 MSDN 或对象浏览器，了解 TextBox 类公开的属性列表。）
- 2. 向 Button 样式添加一个触发器，使其在按钮被按下时将 FontWeight 更改为 Bold，将 FontStyle 更改为 Italic。
- 3. 为按钮编写一个触发器，当 IsMouseOver 为 true 时反转渐变。提示：你需要更改起点和终点，但可以使用相同的步骤集合。
- 该触发器可能无法正常工作。在我们学习下一章的控件模板之前，无法修复它，但你能找出问题所在吗？（如果你的机器非常非常快，可能无法发现。）
- 4. 当指定属性具有指定值时，将应用触发器。当值不再为 true 时会发生什么？（要测试这一点，尝试在示例窗口的一个 TextBox 元素之间切换 Tab 键。）

## 你做得怎么样？

- 1
```xml
<Style TargetType="TextBox">
...
<Style.Triggers>
<Trigger Property="IsFocused" Value="true">
<Setter Property="FontStyle" Value="Italic" />
</Trigger>
</Style.Triggers>
</Style>
```

- 2
```xml
<Style TargetType="Button">
...
<Style.Triggers>
<Trigger Property="IsPressed" Value="true">
<Setter Property="FontWeight" Value="Bold" />
<Setter Property="FontStyle" Value="Italic" />
</Trigger>
</Style.Triggers>
</Style>
```

- 3
```xml
<Trigger Property="IsMouseOver" Value="true">
<Setter Property="Background">
<Setter.Value>
<LinearGradientBrush StartPoint="1,0.5" EndPoint="1,0">
<GradientStops>
<StaticResource Stops />
</GradientStops>
</LinearGradientBrush>
</Setter.Value>
</Setter>
</Trigger>
```

当你将鼠标悬停在按钮上时，渐变会短暂改变，但随后会恢复为 Windows 默认值。这是因为 WPF 默认按钮样式的另一部分接管了。我们将在下一章学习模板时了解如何修复它。目前，你应该记住，如果样式的工作方式不符合你的预期，可能不是因为你做错了什么，而是因为还有其他情况发生。

- 4. 当触发器条件不再为 true 时，元素将恢复到其上一个样式。你不需要做任何事情来实现这一点；WPF 会自动为你处理。

