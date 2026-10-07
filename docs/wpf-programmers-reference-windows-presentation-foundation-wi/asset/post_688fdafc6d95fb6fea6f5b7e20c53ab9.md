
# CHAPTER 15 TEMPLATES

Note that this only works if the ContentPresenter is trying to display text. For example, if you build the Label control so that it contains a Button as shown in the code, the TextBlock won't display:

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

InterestingLabelTemplates

# TEMPLATE EVENTS

The Label control used in the process is one of the simplest controls. It mostly sits there looking pretty without interacting with the user.

But more complicated controls like Button, CheckBox, Slider must perform all sorts of stunts as the mouse moves, presses, drags, and releases over them.

To make a template control respond to events, you can add property and event triggers to the template as you added them to styles in Chapters 13 and 14.

In addition to events caused by user actions such as moving or pressing the mouse, controls must respond to changes in state. For example, although a Label mostly sits around nothing, it should also change its appearance when it is disabled. If you need to display complex animations, then it can simply respond with Sets in a property Trigger that when the Enabled property is False.

The DisabledLabel example program shows that a disabled Label gives a distinctive appearance.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_305_0.png)

FIGURE 15-5

The following code shows that the disabled label gives its appearance:

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

This version of the Template starts with a Grid control that contains a Border and a Canvas. The Border holds a TextBlock that displays the control's ContentPresenter as before. The Canvas Border, is filled with a linear gradient brush, and initially has Opacity 0 so it is invisible.

The template's Triggers section contains a property that activates when the control's IsEnabled property is False. When that happens, the trigger sets the Canvas's Opacity property to 0.5 so it partially obscures the control's content. It also changes the TextBlock's Foreground to Gray.

# TEMPLATE TRICKS 1

Using a control with Opacity = 0 is a common and particularly useful template trick. The template can use it to display something new, cover something over, or in this example, partially obscure whatever lies behind it.

You can use a translucent white color to wash out whatever is behind, a translucent black color to darken whatever is behind, or an opaque control to cover the background controls completely.

# TEMPLATE TRICKS 2

It's easier for triggers to manipulate the template's controls and other objects if you give those objects names. In this example, the TextBlock is named txtbContent and the translucent Canvas is named canDisabled, so it's easy for triggers to control them. If you'll need to animate it, give it a name.

The following sections describe some more complex templates that change the way Buttons work.

# GLASS BUTTON

The GlassButton example program shown in Figure 15-6 uses a template to give its buttons a glassy appearance.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_307_0.png)

FIGURE 15-6

The disabled button on the left looks washed-out and doesn't respond to the user.
The second button labeled *Default* has a different border from that of the other buttons. If no other button has the focus when the user presses the [Enter] key, that Button fires its Click event. In Figure 15-6, the TextBox has the focus, so pressing the [Enter] key will fire the default Button.

# DESIGNATED DEFAULT

> Just because a Button's *IsDefault* property is True, that doesn't mean that the Button always fires when the user presses [Enter]. If the focus is on another Button, then the [Enter] key fires that Button instead of the default.

Also, when the default Button has the focus, it behaves like any other Button with the focus, so it is not acting as the default.

The default button's appearance is changed when the mouse is over it. The default button's appearance is also changed when it is pressed. The default button's appearance is also changed when it is disabled. The default button's appearance is also changed when it has the focus. The default button's appearance is also changed when it is disabled. The default button's appearance is also changed when it has the focus. The default button's appearance is also changed when it is disabled. The default button's appearance is also changed when it has the focus. The default button's appearance is also changed when it is disabled. The default button's appearance is also changed when it has the focus. The default button's appearance is also changed when it is disabled.
