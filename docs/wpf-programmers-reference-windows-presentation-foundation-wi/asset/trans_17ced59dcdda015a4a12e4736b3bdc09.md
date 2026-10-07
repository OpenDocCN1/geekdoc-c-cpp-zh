

# 第 15 章模板

请注意，这仅在 ContentPresenter 尝试显示文本时才有效。例如，如果你像代码所示构建 Label 控件并使其包含一个 Button，那么 TextBlock 将不会显示：

```xml
<Label Margin="Right"
    HorizontalAlignment="Center"
    VerticalAlignment="Center"
    BorderBrush="Yellow Thickness="2"
    Foreground="StaticResource brForeground"
    Background="StaticResource brBackground"
    Template="StaticResource temWrappedLabel">
    <Button Content="Click Me"/>
</Label>
```

有趣的 Label 模板

# 模板事件

在过程中使用的 Label 控件是最简单的控件之一。它大部分时候只是静止地在那里保持美观，而不与用户进行交互。

但像 Button、CheckBox、Slider 这样更复杂的控件必须在鼠标在它们上方移动、按下、拖拽和释放时执行各种动作。

要让模板控件对事件做出响应，你可以像在第 13 和第 14 章中向样式添加触发器一样，向模板中添加属性触发器和事件触发器。

除了移动或按下鼠标等用户操作引起的事件外，控件还必须对状态的变化做出响应。例如，尽管 Label 大多数时间闲置，但当它被禁用时，它也应该改变外观。如果你需要显示复杂的动画，那么简单地通过属性触发器中的 Sets 在当 Enabled 属性为 False 时做出响应即可。

DisabledLabel 示例程序显示了禁用的 Label 具有独特的视觉。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_305_0.png)

图 15-5

以下代码显示了禁用的 label 如何呈现其外观：

```xml
<ControlTemplate x:Key="temWrappedLabel" TargetType="Label">
<Grid>
    <Border Name="Border"
        Background="{Template Background}"
        BorderBrush="{Template BorderBrush}"
        Thickness="{Template BorderThickness}">
        <TextBlock Name="txtContent"
            Margin="4"
            TextWrapping="Wrap"
            Text="{Binding ContentPresenter.Content}"/>
    </Border>
</Grid>
<Canvas Name="canDisabled" Opacity="0">
```

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

此版本的模板包含一个 Grid，禁用的 label 和 Canvas。Canvas 填充了渐变画刷，且初始透明度为 0。模板的触发器部分当 IsEnabled 属性为 False 时会被激活。它会将 Canvas 的 Opacity 设置为 0.5，从而部分遮挡控件内容。它还将 TextBlock 的 Foreground 设置为 Gray。

# 模板技巧 1

使用 Opacity = 0 的控件是一种常用且实用的模板技巧。模板它可以显示新内容、覆盖某些内容，或者在示例中，部分遮挡它背后的内容。

你可以使用透明白色冲淡背后的内容，使用透明黑色加深背后的内容，或者使用不透明控件完全覆盖背景。

# 模板技巧 2

如果你为这些对象命名，触发器更容易操作模板和其他对象。在示例中，TextBlock 被命名为 txtbContent，透明 Canvas 被命名为 canDisabled，因此触发器很容易控制它们。如果你需要对其进行动画，请给它命名。

后续章节描述了一些改变 Button 工作方式的复杂模板。

# 玻璃按钮

图 15-6 所示的 GlassButton 示例程序使用模板赋予按钮玻璃质外观。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_307_0.png)

图 15-6

左侧禁用的按钮看起来褪色且没有响应。标记 Default 的第二个按钮与其他按钮的边框不同。当用户按下 Enter 键时，如果没有其他按钮拥有焦点，则该按钮将触发 Click 事件。在图 15-6 中，TextBox 拥有焦点，因此按下 Enter 键将触发默认按钮。

# 指定默认

> 仅仅因为按钮的 IsDefault 属性为 True，并不意味着该按钮在用户按下 Enter 时总是会触发。如果焦点在另一个按钮上，则 Enter 键将触发该按钮而不是默认按钮。

此外，当默认按钮拥有焦点时，它的行为与其他任何拥有焦点的按钮一样，因此并没有作为默认按钮运行。

默认按钮的外观在鼠标悬停上方时会改变。默认按钮的外观在被按下时也会改变。默认按钮的外观在被禁用时也会改变。当它拥有焦点时，外观也会改变。当它被禁用时，外观也会改变。当它拥有焦点时，外观也会改变。当它被禁用时，外观也会改变。当它拥有焦点时，外观也会改变。当它被禁用时，外观也会改变。

