
```xml
<Canvas.Background>
  <LinearGradientBrush StartPoint="0,0" EndPoint="3,3"
    MappingMode="Absolute">
    <SpreadMethod="Repeat">
      <GradientStop Color="LightGray" Offset="0"/>
      <GradientStop Color="Black" Offset="1"/>
    </SpreadMethod>
  </LinearGradientBrush>
</Canvas.Background>
<Grid>
  <Control.Triggers>
    <Trigger Property="IsEnabled" Value="False">
      <Setter TargetName="canDisabled"
        Property="Opacity" Value="0.5"/>
      <Setter TargetName="txtbContent"
        Property="Foreground" Value="Gray"/>
    </Trigger>
  </Control.Triggers>
</ControlTemplate>
</Grid>
```

此版本的模板包含一个 `Grid`，禁用的 label 和 `Canvas`。`Canvas` 填充了渐变画刷，且初始透明度为 0。模板的触发器部分当 `IsEnabled` 属性为 `False` 时会被激活。它会将 `Canvas` 的 `Opacity` 设置为 0.5，从而部分遮挡控件内容。它还将 `TextBlock` 的 `Foreground` 设置为 `Gray`。

## 模板技巧 1

使用 `Opacity = 0` 的控件是一种常用且实用的模板技巧。模板它可以显示新内容、覆盖某些内容，或者在示例中，部分遮挡它背后的内容。

你可以使用透明白色冲淡背后的内容，使用透明黑色加深背后的内容，或者使用不透明控件完全覆盖背景。

## 模板技巧 2

如果你为这些对象命名，触发器更容易操作模板和其他对象。在示例中，`TextBlock` 被命名为 `txtbContent`，透明 `Canvas` 被命名为 `canDisabled`，因此触发器很容易控制它们。如果你需要对其进行动画，请给它命名。

后续章节描述了一些改变 `Button` 工作方式的复杂模板。

# 玻璃按钮

图 15-6 所示的 `GlassButton` 示例程序使用模板赋予按钮玻璃质外观。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_307_0.png)

图 15-6

左侧禁用的按钮看起来褪色且没有响应。标记 `Default` 的第二个按钮与其他按钮的边框不同。当用户按下 `Enter` 键时，如果没有其他按钮拥有焦点，则该按钮将触发 `Click` 事件。在图 15-6 中，`TextBox` 拥有焦点，因此按下 `Enter` 键将触发默认按钮。

## 指定默认

> 仅仅因为按钮的 `IsDefault` 属性为 `True`，并不意味着该按钮在用户按下 `Enter` 时总是会触发。如果焦点在另一个按钮上，则 `Enter` 键将触发该按钮而不是默认按钮。

此外，当默认按钮拥有焦点时，它的行为与其他任何拥有焦点的按钮一样，因此并没有作为默认按钮运行。

默认按钮的外观在鼠标悬停上方时会改变。默认按钮的外观在被按下时也会改变。默认按钮的外观在被禁用时也会改变。当它拥有焦点时，外观也会改变。当它被禁用时，外观也会改变。当它拥有焦点时，外观也会改变。当它被禁用时，外观也会改变。当它拥有焦点时，外观也会改变。当它被禁用时，外观也会改变。

```xml
<LinearStop Color="LightGreen" Offset="1"/>
</LinearGradientBrush>
</Setter.Value>
</Setter Property="Stroke*">
<Setter.Value>
<LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
<LinearStop Color="DarkGreen" Offset="1"/>
<LinearStop Color="Black" Offset="0"/>
</LinearGradientBrush>
</Setter.Value>
</Setter>
</Style>
<!-- 禁用时的样式 -->
<Style x:Key="StyleDisabled" TargetType="Rectangle" BasedOn="StaticResource styBase">
<Setter Property="Opacity" Value="0.75"/>
<Setter Property="Fill">
<Setter.Value>
<LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
<LinearStop Color="Gray" Offset="0"/>
<LinearStop Color="White" Offset="1"/>
</LinearGradientBrush>
</Setter.Value>
</Setter>
<Setter Property="Stroke*">
<Setter.Value>
<LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
<LinearStop Color="Gray" Offset="1"/>
<LinearStop Color="White" Offset="0"/>
</LinearGradientBrush>
</Setter.Value>
</Setter>
</Style>
```

第一个 `Style` 是一个基础样式，设置了 `Rectangle` 的 `RadiusX`、`RadiusY` 和 `StrokeThickness` 属性。这些属性对于 `Button` 的所有状态都是相同的。由于 `Button` 的“普通”状态是一个未命名的 `Rectangle Style`，因此它总是会有其他 `Style` 覆盖它。它将 `Fill` 属性设置为一个 `LinearGradientBrush`，其颜色呈现从深绿色到浅绿色的渐变。然后，该 `Style` 将 `Stroke` 属性设置为一个产生相反效果的画刷：从浅绿色到深绿色的渐变。（这种极其简单的技术让 `Button` 具有了易读的 3D 外观）。

“默认” `Style` 使用相同的 `Fill` 属性，但让 `Stroke` 笔刷呈现从深绿色到黑色的渐变。（这种差异非常微妙。你可能想尝试更大的变化，也许添加一个完全黑色的轮廓）。

“禁用” `Style` 将 `Rectangle` 的 `Opacity` 属性设置为 0.75，使其变为半透明。它还更改了 `Rectangle` 的 `Fill` 和 `Stroke` 属性，使其在灰色和白色之间渐变。

## 玻璃按钮触发器

以下代码显示了模板的触发器（`Trigger`）。响应事件和控件属性的变化，触发器会设置新的属性值并应用样式。

```xml
<!-- 鼠标悬停 -->
<Trigger Property="IsMouseOver" Value="True">
  <Setter TargetName="grdMain" Property="Opacity" Value="0.75"/>
</Trigger>

<!-- 聚焦 -->
<Trigger Property="IsFocused" Value="True">
  <Setter TargetName="grdMain" Property="Opacity" Value="0.75"/>
</Trigger>

<!-- 默认值 -->
<Trigger Property="IsDefaulted" Value="True">
  <Setter TargetName="rectMain" Property="Style" Value="StaticResource styDefault"/>
</Trigger>

<!-- 按下。位于 Focus 之后，因此具有优先级。 -->
<Trigger Property="IsPressed" Value="True">
  <Setter TargetName="grdMain" Property="Opacity" Value="1"/>
</Trigger>

<!-- 禁用。位于最后，因此具有最高优先级。 -->
<Trigger Property="IsEnabled" Value="False">
  <Setter TargetName="rectMain" Property="Style" Value="StaticResource styDisabled"/>
</Trigger>
```

当控件的 `IsMouseOver` 属性为 `True` 时，第一个触发器将 `Grid` 的 `Opacity` 属性设置为 0.75。这比原始的 0.5 值要大，因此控件变得更不透明了。

当控件接收焦点时，第二个触发器也会将 `Grid` 的 `Opacity` 属性设置为 0.75。

当控件的 `IsDefaulted` 属性为 `True` 时，下一个触发器会将 `Rectangle` 的 `Style` 设置为“默认”样式。

当 `IsPressed` 属性为 `True` 时，接的触发器将 `Grid` 的 `Opacity` 设置为 1，使其完全不透明。

最后，当控件的 `IsEnabled` 属性为 `False` 时，最后一个触发器会将 `Rectangle` 的 `Style` 设置为“禁用”样式。`Button` 控件会自动停止与用户交互，因此你不需要担心这一点。

## 重要顺序

注意，模板触发器的顺序非常重要。后定义的触发器会被后应用——如果两个触发器同时激活，第二个将覆盖第一个。

在这个示例中，`IsPressed` 触发器必须在 `MouseOver` 触发器之后。否则，当用户按下按钮时，`IsPressed` 触发器会先发生。但此时，由于鼠标正位于 `Button` 之上，`MouseOver` 触发器也会应用并覆盖 `IsPressed` 触发器，导致用户永远看不到按钮被按下的状态。

同样，`IsEnabled` 触发器位于最后，因此它会覆盖所有其他触发器。如果按钮被禁用，它不应该显示任何其他外观。

# 椭圆按钮

图 15-9 所示的 `EllipseButton` 示例程序使用模板制作了一个椭圆按钮，这与上一节描述的玻璃按钮非常不同。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_312_0.png)

图 15-9

左侧的禁用按钮比其他按钮颜色淡，且不对用户做出响应。

默认按钮比其他按钮亮，并沿边框显示黄色高亮。

图 15-10 显示了鼠标悬停在按钮 3 上时的程序。鼠标下的按钮比默认按钮更亮，并在边缘处显示黄色高亮。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_312_1.png)

图 15-10

这很难察觉，但图 15-10 中鼠标下的按钮在数字 3 上显示了一个额外的白色高亮。每秒，该高亮绕按钮圆周移动，以吸引用户的注意力。这是一个微小的高亮，所以效果非常微妙。

## 动画建议

动态是可以添加到程序中最吸引眼球的效果之一，但也可能是最分散注意力且令人烦人的效果。鼠标悬停时闪烁颜色或不断改变尺寸的按钮会干扰用户。`EllipseButton` 程序显示的移动高亮很微妙，或者只触发一次——例如当鼠标进入按钮时，所以不要让你的用户抓狂。在极端情况下，快速闪烁的光灯会导致某些人产生癫痫，特别是在 2 到 55 Hz 的频率之间。更好的做法是给用户禁用此类动画的方法。此外请注意，有特殊需求（如色盲或视觉障碍）的用户可能无法很好或完全看到微妙动画。不要仅仅依赖微妙动画来向用户提供信息。

图 15-11 显示了用户按下按钮时的程序。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_313_0.png)

图 15-11

当你按下按钮时，它的背景会轻微移动，并在文字下方显示更大的光晕。如果你在按下状态下将鼠标移出按钮，按钮将回到“聚焦鼠标悬停”外观。如果你松开鼠标，按钮将回到“聚焦鼠标悬停”外观。

以下部分描述模板。内表面（Inner surface）由一个呈现从深绿色到浅绿色渐变的画刷填充。外边缘（Outer edge）是一个椭圆，其 `Stroke` 属性设置为一个呈现从浅绿色到深绿色的渐变的画刷。

以下部分描述模板。内表面（Inner surface）由一个呈现从深绿色到浅绿色渐变的画刷填充。外边缘（Outer edge）是一个椭圆，其 `Stroke` 属性设置为一个呈现从浅绿色到深绿色的渐变的画刷。

## 椭圆按钮控件

图 15-12 显示了鼠标悬停在按钮 3 上时的程序。鼠标下的按钮比默认按钮亮，并在文字下方显示黄色光晕。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_314_0.png)

| Grid | 外边缘 | 内表面 | 边缘高亮 |
|---|---|---|---|
|  | 上高亮 | 下高亮 | ContentPresenter |

## 椭圆按钮触发器

当事件发生时，模板的触发器（triggers）会对控件的外观做出相应的更改。这些通常涉及改变不透明（`Opacity`）值，使某些控件更可见，同时隐藏其他控件。

后续代码所示的 `IsMouseOver` 属性是该面板触发器中最感兴趣的：

```
<Trigger Property="IsMouseOver" Value="True">
  <Setter TargetName="ellipseLeftHighlight" Property="Opacity" Value="1"/>
  <Setter TargetName="ellipse" Property="Opacity" Value="0"/>
  <Setter TargetName="content" Property="Opacity" Value="1"/>
  <Setter TargetName="content" Property="BitmapEffect" Value="StaticResource bmeMouseOver"/>
  <Setter TargetName="sparkle" Property="Opacity" Value="0.75"/>

<!-- Start the sparkle animation. -->
<Trigger.EnterActions>
  <BeginStoryboard StoryName="begSparkle">
    <Storyboard BeginTime="0:0:1" RepeatBehavior="Forever">
      <DoubleAnimationUsingKeyFrames
        Duration="0:0:2"
        Storyboard.TargetName="transSparkle
        Storyboard.Target="Angle">
        <LinearDoubleKeyFrame
          Value="0" KeyTime="0:0:0"/>
        <LinearDoubleKeyFrame
          Value="360" KeyTime="0:0:1"/>
        <LinearDoubleKeyFrame
          Value="360" KeyTime="0:0:2"/>
      </DoubleAnimationUsingKeyFrames>
    </Storyboard>
  </BeginStoryboard>
</Trigger.EnterActions>

<!-- Stop the sparkle animation. -->
<Trigger.ExitActions>
  <StopStoryboard BeginName="begSparkle"/>
</Trigger.ExitActions>
</Trigger>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_315_0.png)

此代码使用简单的 `Setter`（setters）在启动时立即执行以下操作：

- 将左上角的高亮变为完全不透明而非半透明。

- 将降低其他控件的浅灰色变为透明，以便所有其他控件都恢复完全亮度。

- 将 `ContentProperty` 变为完全不透明而非半透明。

为 `ContentPresenter` 提供一个 `OuterGlowmapEffect`（定义在模板的 `Resources` 部分）。将白色闪烁高亮的 `Opacity` 设置为 0.75 以可见。这使得左边缘比右侧高亮亮，并为后续描述的闪烁动画做好准备。

触发器的 `EnterActions` 在 `MouseOver` 属性变为 `True` 时发生。此代码启动了一个 `Storyboard`，它使用 `DoubleAnimationUsingKeyFrames` 对象来对闪烁高亮画刷进行动画处理。画刷使用名为 `sparkle` 的 `RotateTransform`，其初始 `Angle` 为 0，因此画刷没有旋转。动画使 `Angle` 在 1 秒内从 0 度扫描到 360 度，并无限循环。

触发器的 `ExitActions` 在 `MouseOver` 属性不再为 `True`（换句话说变为 `False`）时发生。当发生这种情况时，代码停止动画闪烁的 `Storyboard`。

模板的其他触发器要简单得多。以下代码显示了用户按下按钮时执行的 `IsPressed` 属性：
