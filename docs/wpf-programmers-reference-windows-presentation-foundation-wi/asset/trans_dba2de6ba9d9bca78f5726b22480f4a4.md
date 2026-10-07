
图 13-2 显示了 RedRectangles程序的运行情况。

ButtonStyles 示例程序显示了类似于 ButtonValues 和 ButtonResources 程序中显示的按钮状圆角（参见图 13-1），但它使用了样式（styles）来简化代码。该程序对其 Grid、Rectangle 和 TextBlock 控件使用了以下 XAML：

```
<Resources>
  ... 省略属性定义 ...
  <Style Key="btnRectStyle" TargetType="Grid">
    <Setter Property="Width">
    <Value="StaticResource btnWidth"/>
    <Setter Property="Height">
    <Value="StaticResource btnHeight"/>
    <Setter Property="Margin">
    <Value="StaticResource btnMargin"/>
  </Style>
  <Style Key="btnRectStyle" TargetType="Rectangle">
    <Setter Property="Fill">
    <Value="StaticResource btnFill"/>
    <Setter Property="Stroke">
    <Value="StaticResource btnStroke"/>
    <Setter Property="StrokeThickness">
    <Value="StaticResource btnStrokeThickness"/>
    <Setter Property="RadiusX">
    <Value="StaticResource btnRadiusX"/>
    <Setter Property="Radius">
    <Value="StaticResource btnRadius"/>
  </Style>
  <Style Key="btnTextBlockStyle" TargetType="TextBlock">
    <Setter Property="FontFamily">
    <Value="StaticResource btnFontFamily"/>
    <Setter Property="FontSize">
    <Value="StaticResource btnFontSize"/>
    <Setter Property="FontWeight">
    <Value="StaticResource btnFontWeight"/>
    <Setter Property="HorizontalAlignment">
    <Value="Center"/>
    <Setter Property="VerticalAlignment">
    <Value="Center"/>
    <Setter Property="BitmapEffect">
    <Value="StaticResource btnTextBlockBitmapEffect"/>
  </Style>
</Resources>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_254_0.png)

图 13-2

样式定义包含在 Window.Resources 元素中与其他资源定义一起。该程序包含了与 ButtonResources 程序使用的类似的资源定义（Width、Height、RadiusX、FontFamily 等），但为了节省空间，此处未显示。

以下代码显示了 ButtonStyles 程序如何使用这些样式来显示其 File 按钮：

```
<!-- File
<Grid Style="{StaticResource btnGridStyle}">
  <Rectangle Style="{StaticResource btnRectStyle}"/>
  <TextBlock Style="{StaticResource btnTextBlockStyle}"
    Text="{StaticResource btnText0}" />
</Grid>
```

ButtonStyles

这个版本比上一个短得多，与 ButtonResources 程序使用的 21 行代码（不计注释）相比，仅使用了 6 行代码。

这个版本也更容易理解。例如，Grid 的代码使用了 btnGridStyle，它定义了任何对 Grid 的适当属性。当你阅读这段代码时，你真的不需要知道那些值是什么，只需要知道它们对 Grid 来说是有意义的。这让你能够专注于 Grid、Rectangle 和 TextBlock 的布局，而不会被属性值分散注意力。

ButtonStyles 程序显示五个函数，因此代码行数和复杂性的节省累积成多。按钮定义代码仅占 30 行，而 ButtonResources 程序占了 105 行。

# 编程旁插

当你使用 C# 或 Visual Basic 编写 Windows Forms 程序时，Visual Studio 允许你在设计时设置控件属性，因此你的代码只需要处理在运行时更改的属性。

例如，你可以在表单设计器中设计时设置 Label 的字体、颜色、大小和位置。然后，运行时，程序的代码可能只需要更改 Label 的文本。Visual Studio 通过将其他属性隐藏在单独的生成器生成代码模块中让你忽略它们，你很少需要（如果真的需要的话）去查找该模块。

在 XAML 中，你无法将不变的属性移动移动相同的地方。如果你需要设置 Label 的字体、颜色和位置，那么这些属性与控件的声明在同一个文件中。这可能会导致代码变得杂乱且难以阅读。

样式允许你将不变的属性从控件声明中移出，从而更容易读取控件代码并理解程序的结构。你可以根据想要样式的范围，在容器、窗口提供的资源字典中或在应用程序级别上定义样式。

简化代码是样式的重要功能，所以不要害怕使用它们来使代码更简单。有时，如果能让控件声明更易读，创建一个仅供单个控件使用的样式也是值得的。

# 键和目标类型

元素的 x:Key 和 TargetType 属性有助于识别何时以及何地可以使用样式。至少有三种特别有趣且实用的使用这些属性的方法：非特定目标类型、多个目标类型和未命样式。

# 非特定目标类型

TargetType 决定了你可以使用样式的控件级别。虽然你需要以某种方式提供此信息，但不一定需要具体的。

例如，由于样式的 TargetType 被设置为 Button，因此两个按钮都可以此样式：

```
<Style Key="OrangeButtonStyle" TargetType="Button">
  <Setter Property="Width" Value="150" />
  <Setter Property="Height" Value="40" />
</Style>
```

OrangeStyle

但如果你想将该样式用于 Label，则需要创建第二个样式。如果你以后更改了样式的属性，你需要更新两个样式。

另一种方法是将 TargetType 设置为两个控件共同祖先的类。Button 和 Label 都继承自 Control，所以如果你将 TargetType 设置为 Control，该样式就可以应用于两者。

以下代码显示了新样式，它包含了之前的 Setters 以及针对 Label 属性的 Setter：

```
<Style Key="OrangeStyle" TargetType="Control">
  <Setter Property="Width" Value="150" />
  <Setter Property="Height" Value="40" />
  <Setter Property="Background" Value="Orange" />
  <Setter Property="Foreground" Value="Yellow" />
  <Setter Property="Margin" Value="5" />
</Style>
```

到目前为止良好，但如果你想为一个没有这些属性的控件指定值呢？例如，Label 有 BorderBrush 和 BorderThickness 属性。Button 没有这些属性，因此你需要将它们添加到样式中。幸运的是，控件会忽略它任何不理解的属性。

以下代码显示了新样式：

```
<Style Key="OrangeControlStyle" TargetType="Control">
  <Setter Property="Width" Value="150" />
  <Setter Property="Height" Value="40" />
  <Setter Property="Background" Value="Orange" />
  <Setter Property="Foreground" Value="Yellow" />
  <Setter Property="Margin" Value="5" />
  <Setter Property="BorderBrush" Value="Black" />
  <Setter Property="BorderThickness" Value="2" />
</Style>
```

图 13-3 所示的 ControlExample 使用以下代码显示两个按钮和一个 Label。上方的按钮使用 OrangeButtonStyle；下方的按钮和 Label 都使用 OrangeStyle。

```
<StackPanel VerticalAlignment="Center">
  <Button Style="{StaticResource OrangeButtonStyle}" Content="Button" />
  <Button Style="{StaticResource OrangeStyle}" Content="Button" />
  <Label Style="{StaticResource OrangeStyle}" Content="Label" />
</StackPanel>
```

# 多个目标类型

上一节介绍了如何通过将样式的 TargetType 设置为共同祖先类来构建可以影响两个控件类型（Button 和 Label）的样式。（Button 和 Label 都继承自 Control。）

但如果你还想让样式影响 Rectangle：Button 和 Label 有 Control 类共同祖先，但 Rectangle 继承自 Shape 类而不是 Control。如果你在继承层次结构向上爬一点，你会发现 Control 和 Shape 都继承自 FrameworkElement，所以你可能认为自己自由了。你可以简单创建一个 TargetType 为 FrameworkElement 的样式并按 usual构建 Setter。

但遗憾的是，FrameworkElement 不支持所有属性。例如，如果你尝试将样式的 TargetType 更改为 FrameworkElement，Expression Blend 会 Background、Foreground、BorderBrush 和 BorderThickness 属性上标记错误。

问题在于 Button、Label 和 Rectangle 的第一个共同祖先不支持你想要使用的所有属性。幸运的是，还有另一种方法来指定提供样式属性的对象。

不要在 Style 元素的 TargetType 属性中指示类，而是在 Setter 的 Property 属性中指示它。

