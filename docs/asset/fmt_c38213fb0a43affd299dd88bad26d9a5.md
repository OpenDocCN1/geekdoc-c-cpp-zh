
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

与之前的示例一样，此代码定义了 `ScaleTransform`。`DepartmentPanel` `Style` 设置了 `Margin`。它将 `Opacity` 设置为 `0.5`，因此控件是淡化的。接下来，`Style` 将 `Background` 设置为 `Transparent`。

# 透明 Null

透明背景与透明相同。然而，如果鼠标悬停在控件上，`IsMouseOver` 会改变。

如果你想通过 `MouseOver` 属性来实现透明，请确保控件的背景不是透明的。`DepartmentPanel` `Style` 定义了它的 `MouseOver` `Trigger`。当 `MouseOver` 为 `True` 时，`Trigger` 设置了 `Opacity`，因此控件是完全不透明的。

# IsActiveAndFocused Triggers（激活与焦点触发器）

之前的几个触发器在 `MouseOver` 属性为 `True` 时执行操作。`MouseOver` 属性是一个很好的选择，因为你可以为任何属性编写触发器的良好的视觉反馈。

图 13-11 所示的 `ActiveTrigger` 示例程序演示了监控 `Window` 的 `IsActive` 属性和 `TextBox` 的 `IsFocused` 属性的两个触发器。

这些触发器提供了两种效果：

- 第一，当另一个应用程序拥有焦点时，程序将其 `Title` 更改为 `Inactive`。
- 第二，包含插入光标的 `TextBox` 显示为红色。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_270_0.png)

在窗口标签 `<Window>` 之后，`Style` 元素定义了窗口的 `Style`。此示例直接定义 `Style`，而不是在资源中定义以便稍后引用，部分原因由于文件中只有一个 `Window` 对象。

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

此 `Style` 的唯一技巧是它设置了窗口的 `Title` 属性。当 `IsActive` 属性为 `False` 时，`Trigger` 尝试将 `Title` 属性 设置为 `Inactive`。如果 `Window` 元素在属性中显式设置了 `Title` 的值，那么 `Trigger` 将无法覆盖该值。

以下代码显示了程序用于在文本框周围显示红色发光效果的资源：

```
<OuterGlowBitmapEffect x:Key="txtGlow" GlowColor="Red" GlowSize="10"/>
<Style TargetType="TextBox">
  <Setter Property="Margin" Value="5"/>
  <Setter Property="Width" Value="200"/>
  <Style.Triggers>
    <Trigger Property="IsFocused" Value="True">
      <Setter Property="Effect" Value="StaticResource txtGlow"/>
    </Trigger>
  </Style.Triggers>
</Style>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_271_0.png)

代码首先创建了一个 `OuterGlowBitmapEffect` 资源。它定义了一个 `TextBox` 样式，包含一个在 `IsFocused` 属性为 `True` 时激活的触发器。该触发器仅地将 `TextBox` 的 `BitmapEffect` 设置为之前定义的发光效果。

## 总结

样式（Styles）允许你定义许多控件可以共享的资源值包。共享样式为控件提供了更一致的外观和行为，使得更容易在不出错的情况下更改属性值，并简化了 XAML 代码，让你能够更容易关注窗口结构中有趣的部分，而不会被重复的属性值分散注意力。

如果你想将样式应用于单个控件，可以为样式指定一个 `x:Key` 值；或者你也可以省略它，使其应用于该样式类型的每个控件。

属性触发器（Property triggers）允许你定义当控件的属性取某个特定值时可以执行的简单行为。例如，你可以使用属性触发器提供额外的反馈，也许当用户将鼠标悬停在按钮上时，可能会更改按钮的字体、大小或颜色。

虽然属性触发器可以让控件采取行动，但它们仍然是局部的，并且旨在作用于定义它们的控件本身。例如，如果一个样式应用于 `Button`，那么它的属性可以影响该 `Button` 的属性，但它们并不打算修改 `Button` 旁边的 `Label`、包含 `Button` 的 `Grid` 或容载整个内容的 `Window`。

事件触发器（Event triggers）将在下一章解释，它们提供了一种绕过这种限制的方法。虽然你可以在样式内部定义事件触发器，但也可以在更全局的级别定义它们，这样在处理多个控件时更容易操作。例如，你可以在 `Button` 上定义一个事件触发器，改变另一个 `Button`、包含这些按钮的 `Grid` 或 `Window` 整体的颜色。

# 14 事件触发器与动画

上一章描述的属性触发器允许你检测特定的属性值并相应地更改某些属性的值。例如，按钮可以检测到 `IsMouseOver` 是否为 `True`，并更改其缩放以使按钮在鼠标悬停在其上方时变大；目前没有属性可以直接为事件提供反馈。

事件触发器和动画为这种类型的响应能力增加了一个新维度。事件触发器允许你检测事件的发生。动画（Animation）允许你在一系列平滑变化的步骤中更改属性值。结合起来，例如，你可以让按钮检测 `MouseOver` 事件并使用动画放大按钮，从而提供与之前的事件属性相似的图形化反馈。

那么，区别在哪里呢？WPF 控件并不是通过观察属性值来提供的。例如，虽然 `Button` 有一个 `IsMouseOver` 属性来告知鼠标是否悬停在其上方，但并没有属性直接对应于 `MouseEnter`、`MouseLeave`、`MouseDown`、`MouseUp`、`MouseMove` 和 `Click` 事件。

第二，属性触发器使用的设置器（setter）会立即更改属性的值。相比之下，动画使属性随时间逐渐变化。最终结果是，用户可以看到数值发生发生的变化。例如，动画不是让按钮突然跳变到新尺寸，而是让它逐渐变大。通常这种区别是关重要的——虽然按钮的最终尺寸是相同的，但让用户观察变化的过程提供了一种更具参与感的体验。

本章将解释事件触发器和动画。接下来的章节将解释你如何使用事件触发器来检测事件并执行故事板（storyboards）。接下来的部分将解释故事板如何工作以及它们可以执行的各种动画类型。

## 事件触发器

属性触发器在控件的属性具有特定值时采取行动。例如，下面的样式使按钮在鼠标悬停在其上方时增加其宽度和高度：

```
<Style x:Key="BtnPropertyGrowStyle" TargetType="Button">
  <Setter Property="Width" Value="100"/>
  <Setter Property="Height" Value="50"/>
  <Style.Triggers>
```

### 第 14 章 事件触发器与动画

```
<Trigger Property="IsMouseOver" Value="True">
  <Setter Property="Width" Value="150"/>
  <Setter Property="Height" Value="75"/>
</Trigger>
</Style.Triggers>
</Style>
```

相比之下，事件触发器在控件事件发生时采取行动。事件触发器不是在 `MouseOver` 属性为 `True` 时采取行动，而是可能在 `MouseEnter` 事件触发时采取行动，这表示鼠标已移动到控件上。另一个事件触发器可以在 `MouseLeave` 事件触发时采取其他操作，该事件在鼠标移出控件时发生。

要创建事件触发器，请在控件定义或样式中创建一个 `Triggers` 元素。在 `Triggers` 内部，添加 `EventTrigger` 元素。

每个 `EventTrigger` 都有一个 `RoutedEvent` 属性，它指示了执行触发器的事件。`RoutedEvent` 应该包含引发事件的类名（`Button`、`Label`、`Grid` 等），后跟着一个点和事件名称。例如，`Button` 的 `Click` 事件的 `RoutedEvent` 名称为 `Button.Click`。

在触发器内部，放置一个 `Actions` 部分来容纳你想要让触发器执行的操作。在 `Actions` 元素内部，你可以放置代码通过执行故事板来运行动画。

例如，下面的代码显示了一个在它触发 `MouseEnter` 事件时采取行动的 `Button`（尽管它没有显示该操作可能是什么）：

```
<Button Width="100" Height="50" Content="Click Me">
<Button.Triggers>
  <EventTrigger RoutedEvent="Button.MouseEnter">
    <EventTrigger.Actions>
      ... 在此处执行某些操作 ...
    </EventTrigger.Actions>
  </EventTrigger>
</Button.Triggers>
</Button>
```

通常，事件触发器使用 `BeginStoryboard` 元素来调用故事板。其他层级详细描述了故事板，但现在假设你在资源中定义了一个名为 `sbBigScale` 的故事板。下面的代码显示了按钮如何调用该故事板：

```
<Button Width="100" Height="50" Content="Click Me">
<Button.Triggers>
  <EventTrigger RoutedEvent="Button.MouseEnter">
    <EventTrigger.Actions>
      <BeginStoryboard Storyboard="{StaticResource sbBigScale}"/>
    </EventTrigger.Actions>
  </EventTrigger>
</Button.Triggers>
</Button>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_273_0.png)

可在 Wx.com 下载。

### GrowingButtons

### 事件触发器

`BeginStoryboard` 对象的 `Storyboard` 属性提供了要执行的故事板。此示例使用 `StaticResource` 来运行窗口中定义的故事板。

### BEGINSTORYBOARD 是什么意思？

每当我看到 `BeginStoryboard` 元素时，我都会认为“这是故事板定义的开始”，并期望后续代码定义故事板。不幸的是，这并不是 `BeginStoryboard` 的意思。正如前面的示例所示，`BeginStoryboard` 元素不需要包含对故事板引用之外的任何内容。

`beginStoryboard` 真正的意思是“执行”或“运行”，所以当你看到这个元素时，你应该认为是“运行这个故事板”。如果微软将此元素命名为 `RunStoryboard`（至少对我来说）可能就不会那么困惑。

## 事件触发器位置

放置事件触发器最明显的地方是引发事件的控件。例如，下面的代码定义了一个在点击时运行 `sbSpin` 故事板的 `Button`：

```
<Button Content="Spin Me!">
<Button.Triggers>
  <EventTrigger RoutedEvent="Button.Click">
    <EventTrigger.Actions>
      <BeginStoryboard Storyboard="{StaticResource sbSpin}"/>
    </EventTrigger.Actions>
  </EventTrigger>
</Button.Triggers>
</Button>
```

`sbSpin` 故事板将按钮旋转 360 度。图 14-1 显示了故事板刚开始时的 `SpinButton` 示例。

之前的代码已经使用了一些技术使得按钮代码更易读。一个未命名的样式设置了按钮的 `Width` 和 `Height`。它还将按钮的 `RenderTransform` 设置为 `RotateTransform` 对象，以便故事板可以旋转按钮。

图 14-1

### 变换技巧

`Storyboard` 可以更改变换的属性，但它不能从零开始创建一个新的变换。在旋转按钮的示例中，`Storyboard` 可以更改 `RenderTransform` 的旋转角度，但它不能凭空产生 `RenderTransform`，因此 `Button Style` 创建了一个初始的 `RenderTransform`，将按钮旋转 0 度。

在通常情况下，如果你想旋转、拉伸或其他更改控件的变换，你必须为它提供一个初始变换，以便 `Storyboard` 进行修改。

`sbSpin` `Storyboard` 也被定义为资源以进一步简化 `Button` 的代码。你甚至可以在 `Button Style` 中定义 `EventTrigger`，使 `Button` 的代码变得非常简单。在某些情况下，定义相同或相似的触发器是有意义的：例如，考虑图 14-2 所示的 `CentralizedTriggers` 示例程序。该程序在左侧显示了一系列缩略图。当你点击其中一张时，图像会展开并移动以填充右侧区域。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_275_0.png)

图 14-2

在这个示例中，所有缩略图的操作都大同相同：它们都会展开自己的图像。在像显示一系列具有相似用途控件的程序中，如果它们的触发器都放在一起，可能会让程序的逻辑更容易理解。这对于一系列缩略图、按钮、菜单项、单选按钮或任何执行大致相同操作的控件组都是意义意义。

当路由事件（routed event）被触发时，它会在包含启动它的控件层次结构中移动。`CentralizedTriggers` 示例控件显示在 `Canvas` 上，当用户点击其中一个缩略图（一个 `Image` 控件）时，`MouseLeftDown` 事件从缩略图开始，移动到 `Canvas`，然后再次移动到 `Window`。程序代码可以在任何级别捕捉事件。

以下代码片段显示了 `CentralizedTriggers` 程序 `Canvas` 控件的结构：

```
<Canvas Margin="5">
  <Canvas.Resources>
    <!-- 定义一个未命名的 Image Style。 -->
    <Style TargetType="Image">
      <Setter Property="Opacity" Value="0.5"/>
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="100"/>
      <Setter Property="Stretch" Value="Uniform"/>
      <Setter Property="BitmapEffect">
        <DropShadowBitmapEffect/>
      </Setter>
    </Style>
  </Canvas.Resources>
```

```
<!-- 为每个 Image 定义一个 Storyboard. -->
<Storyboard x:Key="sbImg1">
  Code omitted ...
</Storyboard>
定义其他 Storyboards
</Canvas.Resources>
```
