
此列表并未涵盖属性值可能更改的所有方式，但它涵盖了最直观和实用的方式。其他方式超出了本章的范围。关于属性值优先级的更多信息，请参阅微软的“依赖属性值优先级”（Dependency Property Value Precedence）网页 mdn.microsoft.com/ms743230.aspx。

# 无样式 (NO STYLE)

假设你定义了一个无名的样式，但不想让该样式应用于特定类型的控件。此时，你可以将 Style 设置为特殊值 (x:Null)，以表示它不应该有任何样式。例如，以下代码创建了一个没有样式的 Label：

```xml
<Label Style="x:Null" Content="Test" />
```

# 样式继承 (STYLE INHERITANCE)

你将相同的属性值应用到多个控件的资源。样式允许你将资源分组包，从而更容易地为控件提供共同的外观。

样式继承允许你基于另一个样式构建一个样式。这使得为控件提供共同外观变得更加容易，即使它们没有共享相同的最终样式。

子元素继承父样式定义的所有 Setters 和其他值。然后，你可以根据需要覆盖其中的某些值。

要让一个样式继承另一个样式，请在其起始元素上添加 `BasedOn` 属性，并将该属性的值设置为父 Style。注意，Style 是在资源字典中定义的对象，因此你应该使用 `StaticResource` 语句来设置它。

例如，以下代码为样式定义了两个渐变画刷：

```xml
<LinearGradientBrush Key="GreenBrush" StartPoint="0,0" EndPoint="1,0">
  <GradientStop Color="Green" Offset="0"/>
  <GradientStop Color="Lime" Offset="0.3"/>
  <GradientStop Color="Transparent" Offset="0.8"/>
</LinearGradientBrush>
```

```xml
<LinearGradientBrush Key="BlueBrush" StartPoint="0,0" EndPoint="1,0">
  <GradientStop Color="Blue" Offset="0"/>
  <GradientStop Color="White" Offset="1"/>
</LinearGradientBrush>
```

```xml
<Style Key="SizeType" TargetType="FrameworkElement">
  <Setter Property="Width" Value="150"/>
  <Setter Property="Height" Value="30"/>
  <Setter Property="HorizontalAlignment" Value="Left"/>
  <Setter Property="VerticalAlignment" Value="Top"/>
  <Setter Property="Margin" Value="5"/>
</Style>
```

```xml
<Style TargetType="Rectangle" BasedOn="(StaticResource SizeStyle)">
  <Setter Property="Fill" Value="(StaticResource BlueBrush)"/>
  <Setter Property="RadiusX" Value="10"/>
  <Setter Property="RadiusY" Value="10"/>
</Style>

<Style TargetType="Label" BasedOn="(StaticResource SizeStyle)">
  <Setter Property="FontWeight" Value="Bold"/>
</Style>

<Style TargetType="Button" BasedOn="(StaticResource SizeStyle)">
  <Setter Property="Background" Value="(StaticResource GreenBrush)"/>
  <Setter Property="Margin" Value="2,5,5,5"/>
  <Setter Property="FontWeight" Value="Bold"/>
  <Setter Property="Width" Value="100"/>
</Style>
```

代码定义了一个名为 `GreenBrush` 的线性渐变画刷，它从绿色渐变到青绿色再到透明。它还创建了一个名为 `BlueBrush` 的画刷，它从蓝色渐变到白色。

接下来的代码为 Rectangle 定义了一个无名样式。它基于 `SizeStyle`，并设置了尺寸和对齐属性。新样式为 Rectangle 的属性 `Fill`（使用 `BlueBrush` 资源）、`RadiusX` 和 `RadiusY` 添加了值。

随后代码段定义了 Label 的无名样式。该样式继承了 `SizeStyle` 的大小和对齐属性，并添加了一个新的 `FontWeight` Setter。

最后，代码定义了 Button 的无名样式。该样式设置了 `Background`、`Margin` 和 `FontWeight` 属性。在此中，无名的 Button 覆盖了它从 `SizeStyle` 继承的 `Margin` 和 `Width` 值。

图 13-6 所示的 InheritedStyles 示例使用了这些样式在 Grid 顶部显示 Rectangle、Label 和 Button。Rectangle 太大无法放入 Grid 单元格，因此它们的圆角在顶部被截断了。Button 使用了 `GreenBrush` 背景，因此它们从绿色渐变到透明，允许窗口的浅绿色背景在它们的右边缘显示出来。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_263_0.png)

图 13-6

在此示例中，无名的 Rectangle 和 Label 样式从 `SizeStyle` 继承了定位属性，因此它们对齐正常。

注意，你只能使用 TargetType 为新样式基类的另一个样式来作为基类。例如，在上一个示例中，无名的 Rectangle、Label 和 Button 样式都是基于 TargetType 为 `FrameworkElement` 的样式。这之所以有效，是因为 Rectangle、Label 和 Button 都继承自 `FrameworkElement`。

相比之下，你不能将 Button 样式基于 Label 样式，因为 Button 并不继承自 Label。

# 混合继承 (MIXED ANCESTRY)

然而，例如，以下代码定义了样式 `lblStyle`。此样式实际上用于 Label，但它没有 `TargetType`，因此 WPF 不会强制执行该意图。`btnStyle` 是 Button 并不继承自 Label，尽管 `btnStyle` 的：

```xml
<Style X:Key="lblStyle">
    <Setter Property="Label.Background" Value="Yellow"/>
    <Setter Property="FontWeight" Value="Bold"/>
</Style>

<Style X:Key="btnStyle" BasedOn="(StaticResource lblStyle)" TargetType="Button">
    <Setter Property="Width" Value="100"/>
    <Setter Property="Margin" Value="2,5,5,5"/>
</Style>
```

你可以使用继承来实现跨窗口的一致性。例如，你可以在 App.xaml 中定义全局样式。这些样式可能会定义你想要的颜色、字体和尺寸。

# 触发器 (TRIGGERS)

228 | 第 13 章 样式与属性触发器

到目前为止描述的样式总是将它们的属性值应用到控件上。

样式还可以定义触发器，即在特定条件下允许使用 setter 的对象。例如，一个触发器可能会更改 Label 的颜色。

WPF 提供了几种触发器，包括属性触发器、事件触发器和数据触发器。本节介绍属性触发器。事件触发器与动画紧密相关，因此在第 14 章中描述。数据触发器在此未介绍，尽管它们与数据绑定密切相关，数据绑定将在第 18 章中解释。

属性触发器当特定属性具有特定值时执行其操作。例如，如果 TextBox 的属性值为 Test，属性触发器可以调用一个或多个 Setter。（它们被称为属性触发器，是因为属性值触发了操作。）

当属性不再具有触发值时，触发器将失效并返回原始属性值。例如，当用户鼠标移出 Label 时，Label 返回到原始的颜色、字体和大小。

这种在运行时响应属性变化的能力赋予了控件新的行为，使应用程序对用户的响应更加敏感。

要制作属性触发器，创建一个样式并赋予一个 `Style.Triggers` 属性元素。在 `Style.Triggers` 部分，你可以添加 `Trigger` 元素。

使用每个 Trigger 的 `Property` 和 `Value` 属性来指示激活触发器的属性值。在 Trigger 元素内部，放置你想让触发器执行的任何 Setters。

> 触发器位置

你必须将属性触发器放在样式内部——而不是框架元素的 Triggers 区域。例如，你不能将属性触发器放置在 Window.Triggers 或 Grid.Triggers 中。IntelliSense 会假装这是可行的，但实际上，这些部分只能包含事件触发器（在下一章中描述）。

始终将属性触发器放在样式中。

以下章节提供了一些实用的触发器示例。

# 文本触发器 (Text Triggers)

以下 XAML 代码定义了两个无名样式，一个用于 TextBox，一个用于 ComboBox：

```xml
<Style TargetType=TextBox>
  <Setter Property="HorizontalAlignment" Value="Left" />
  <Setter Property="VerticalAlignment" Value="Center" />
  <Setter Property="Width" Value="220" />
  <Style.Triggers>
    <Trigger Property="Text" Value="">
```
