```
Duration="0:0:3" AutoReverse="True"
    FillBehavior="Stop"
    RepeatBehavior="Forever"
    AccelerationRatio="0.9" DecelerationRatio="0.1"
    From="100" To="300" />
<ColorAnimation Storyboard.TargetName="ellipseBrush"
    Storyboard.TargetProperty="(SolidColorBrush.Color)"
    Duration="0:0:3" AutoReverse="True"
    FillBehavior="Stop" RepeatBehavior="Forever"
    From="Yellow" To="Red" />
</Storyboard>
</BeginStoryboard>
</EventTrigger.Actions>
</EventTrigger>
</Ellipse.Triggers>
</Ellipse>
```

*code snippet AnimationDemo/EllipseWindow.xaml*

Figures 35-29 and 35-30 show two states from the animated ellipse.

![](bbox=[0.8, 0.4, 0.92, 0.5])

Animations are far more than typical window-dressing animation that appears onscreen constantly and immediately. You can add animation to business applications that make the user interface more responsive.

![](bbox=[0.75, 0.58, 0.95, 0.7])

The following example demonstrates a decent animation and also shows how the animation can be defined in a style. Within the Window resources you can see the style AnimatedButtonStyle for buttons. In the template, a rectangle-named outline is defined. This template has a thin stroke with the thickness set to 0.4.

![](bbox=[0.78, 0.7, 0.95, 0.84])

The template defines a property trigger for the IsMouseOver property. The EnterActions property of this trigger applies as soon as the mouse is moved over the button. The action to start is BeginStoryboard. BeginStoryboard is a trigger action that can contain and thus start Storyboard elements. The Storyboard element defines a DoubleAnimation to animate a double value. The property value that is changed in this animation is the Rectangle.StrokeThickness of the Rectangle element with the name outline. The value is changed in a smooth way by 1.2, as the By property specifies, for a time length of 0.3 seconds as specified by the Duration property. At the end of the animation, the stroke thickness is reset to its original value because AutoReverse="True". To summarize: as soon as the mouse moves over the button, the thickness of the outline is incremented by 1.2 for 0.3 seconds. Figure 35-31 shows the button without animation, and Figure 35-32 shows the button 0.3 seconds after the mouse moved over it. (It's just not possible to show the smooth animation and intermediate looks in a print medium.)

![](bbox=[0.78, 0.86, 0.95, 0.97])

```
<Window x:Class="AnimationDemo.ButtonAnimationWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="ButtonAnimationWindow" Height="300" Width="300">
    <Window.Resources>
        <Style x:Key="AnimatedButtonStyle" TargetType="{x:Type Button}">
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate TargetType="{x:Type Button}">
                        <Grid>
                            <Rectangle Name="outline" RadiusX="9" RadiusY="9"
                                Stroke="Black" Fill="{TemplateBinding Background}"
                                StrokeThickness="1.6">
                            </Rectangle>
```