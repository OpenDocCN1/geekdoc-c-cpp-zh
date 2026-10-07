

```xml
<Setter Property="Background" Value="Yellow" />
</Trigger>
</Style.Triggers>
</Style>
<Style TargetType="ComboBox">
<Style.Triggers>
<Trigger Property="Text" Value="*">
<Setter Property="Background" Value="Yellow" />
</Trigger>
</Style.Triggers>
</Style>
```

# TextTriggers（文本触发器）

这些 Style 中的每一个都定义了一个 Style.Triggers 部分，其中包含一个 Trigger，当控件的 Text 属性为空时，它会执行操作。当这种情况发生时，Style 的 Setter 会将控件的 Background 设置为黄色，以指示该值是必的。

图 13-7 中的 TextTriggers 示例程序使用此代码来标记带有值的必填字段。如果必填字段为空，其背景颜色将变为黄色。（在图 13-7 中，奥巴马先生尚未填写信息，因此城市、州、邮政编码、电话和电子邮件字段显示为黄色，以标记它们为缺失。）

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_266_0.png)

图 13-7

# 仅限精确匹配

遗憾的是，触发器只能检测属性的精确匹配，无法处理范围、不同的大小写情况或更复杂的情况。例如，你无法使用简单的触发器根据 TextBox 包含的值为它们设置不同的颜色（例如，负值显示为红色，0 到 10 之间的值显示为黄色，较大的值显示为绿色）。XAML 并不具备表示此类测试的表达能力。

# IsMouseOver Triggers（鼠标悬停触发器）

一种常见的触发器类型是在用户鼠标移动到某个物体上方时执行操作。这些触发器在 IsMouseOver 属性为 True 时执行其 Setters。

以下 XAML 代码定义了一个未命名的 Button Style。它设置了一些基本值，并定义了一个在 IsMouseOver 属性为 True 时执行的 Trigger。当鼠标移动到 Button 上时，Trigger 会改变 Button 并使其字体更大、加粗。

```xml
<Style TargetType="Button">
<Setter Property="VerticalAlignment" Value="Top"/>
<Setter Property="Margin" Value="10"/>
<Setter Property="Background" Value="Violet"/>
<Setter Property="Width" Value="100"/>
<Setter Property="Height" Value="30"/>
<Setter Property="FontSize" Value="16"/>
</Style>
<Trigger Property="IsMouseOver" Value="True">
<Setter Property="Width" Value="105"/>
<Setter Property="Height" Value="50"/>
<Setter Property="FontSize" Value="20"/>
<Setter Property="FontWeight" Value="Bold"/>
</Trigger>
</Style.Triggers>
</Style>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_267_0.png)

图 13-8 所示的 IsMouseOverTriggers 示例使用此代码在鼠标悬停在按钮上时提供反馈。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_267_1.png)

图 13-8

# 设置 Transform 和 BitmapEffect（变换与位图效果）

之前的 Trigger 为激活的 Button 提供了新的 Height 和 FontSize，使按钮变大。MenuMouseOverTriggers 示例以另一种方式实现了的效果。与其单独设置这些属性，不如使用一个 Setter 给激活的控件一个可以缩放控件的 LayoutTransform。

以下代码显示了程序如何在鼠标悬停在 MenuItem 上时放大它：

```xml
<Resources>
<ScaleTransform Key="mnuBigScale" ScaleX="1.25" ScaleY="1.25"/>
<OuterGlowEffect Key="mnuBitmapEffect"/>
<Style Key="mnu" TargetType="MenuItem">
<Trigger Property="IsMouseOver" Value="True">
<Setter Property="FontWeight" Value="Bold"/>
<Setter Property="Foreground" Value="Red"/>
<Setter Property="LayoutTransform" Value="StaticResource mnuBigScale"/>
<Setter Property="BitmapEffect" Value="StaticResource mnuBitmapEffect"/>
</Trigger>
</Style>
</Style.Triggers>
</Style>
<Window.Resources>
```

首先，程序定义了一个 ScaleTransform 资源和一个 OuterGlowBitmapEffect 资源。这些值是 Trigger 用来设置 MenuItem 属性的值。

程序定义了 MenuItem Style。Trigger 设置了 MenuItem 的 FontWeight 和 Foreground 简单属性。它还将控件的 LayoutTransform 和 BitmapEffect 属性 设置为之前定义的资源。

图 13-9 显示了结果。

你可以使用类似的技术来处理修改 LayoutTransform 和 BitmapEffect 属性的控件。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_268_0.png)

图 13-9

> 按钮背景
> 不要费力在鼠标悬停在按钮或 MenuItem 上时尝试更改它们的背景。Button 和 MenuItem 控件对于鼠标悬停时应该看起来什么样有非常明确的观点——用户看不到它们的颜色，或者在控件的自然行为接管并替换它们之前，可能会看到颜色短暂闪烁。

你可以更改这些控件在不同时间点的外观，但最好使用模板（Templates）而不是触发器（Triggers）。第 15 章详细解释了模板。

# 设置 Opacity（透明度）

图 13-10 所示的 ImageTriggers 示例程序使用 Triggers 来高亮图像。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_268_1.png)

图 13-10

这里的触发器是由于让程序变得更简单。如果你喜欢，可以从书下载下载示例。。触发器设置了  。。。 StackPanel 包含一个 Image 和一个 Label。代码代码显示了鼠标 的控件：

```xml
<StackPanel Style="DepartmentStyle">
  <Image Source="Engineering.jpg" />
  <Label Content="Engineering"/>
</StackPanel>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_269_0.png)

精确匹配时，Style 触发器是以下代码：

```xml
<ScaleTransform Key="BigScale" ScaleX="1.1" ScaleY="1.1"/>
<StackPanel x:Key="DepartmentPanel">
  <Setter Property="Margin" Value="10"/>
  <Setter Property="Opacity" Value="0.5"/>
  <Setter Property="Background" Value="Transparent"/>
  <Style.Triggers>
    <Trigger Property="IsMouseOver" Value="True">
      <Setter Property="Opacity" Value="1"/>
      <Setter Property="LayoutTransform" Value="{StaticResource BigScale}"/>
    </Trigger>
  </Style.Triggers>
</StackPanel>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_269_1.png)

与之前的示例一样，此代码定义了 ScaleTransform。DepartmentPanel Style 设置了 Margin。它将 Opacity 设置为 0.5，因此控件是淡化的。接下来，Style 将 Background 设置为 Transparent。

# 透明 Null
透明背景与透明相同。然而，如果鼠标悬停在控件上，IsMouseOver 会改变。

如果你想通过 MouseOver 属性来实现透明，请确保控件的背景不是透明的。DepartmentPanel Style 定义了它的 MouseOver Trigger。当 MouseOver 为 True 时，Trigger 设置了 Opacity，因此控件是完全不透明的。

# IsActiveAndFocused Triggers（激活与焦点触发器）

之前的几个触发器在 MouseOver 属性为 True 时执行操作。MouseOver 属性是一个很好的选择，因为你可以为任何属性编写触发器的良好的视觉反馈。

图 13-11 所示的 ActiveTrigger 示例程序演示了监控 Window 的 IsActive 属性和 TextBox 的 IsFocused 属性的两个触发器。

这些触发器提供了两种效果：

- 第一，当另一个应用程序拥有焦点时，程序将其 Title 更改为 Inactive。
- 第二，包含插入光标的 TextBox 显示为红色。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_270_0.png)

在窗口标签 <Window> 之后，Style 元素定义了窗口的 Style。此示例直接定义 Style，而不是在资源中定义以便稍后引用，部分原因由于文件中只有一个 Window 对象。

```xml
<Style>
  <Style TargetType="Window">
    <Setter Property="Title" Value="ActiveTrigger"/>
    <Triggers>
      <Trigger Property="IsActive" Value="False">
        <Setter Property="Title" Value="Inactive"/>
      </Trigger>
    </Triggers>
  </Style>
</Style>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_270_1.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_270_2.png)

此 Style 的唯一技巧是它设置了窗口的 Title 属性。当 IsActive 属性为 False 时，Trigger 尝试将 Title 属性 设置为 Inactive。如果 Window 元素在属性中显式设置了 Title 的值，那么 Trigger 将无法覆盖该值。

