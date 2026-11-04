The program uses several Styles to make building the list of images easier. They’re rather long, so they aren’t shown here. You can download the example program from the book’s web site and take a look if you like.

The bottom of the program’s window contains a series of StackPanel controls, each of which holds an Image and a Label. The following code shows how the program displays the controls for the Engineering department on the right:

![](bbox=[0.212, 0.231, 0.251, 0.283])

```
```xml
<StackPanel Style="{StaticResource DepartmentStackPanel}">
    <Image Source="Engineering.jpg" />
    <Label Style="{StaticResource ImageLabelStyle}" Content="Engineering" />
</StackPanel>
```
```

The key is the DepartmentStackPanel Style defined in the following code:

![](bbox=[0.212, 0.353, 0.251, 0.397])

```
```xml
<ScaleTransform x:Key="BigScale" ScaleX="1.1" ScaleY="1.1"/>

<Style x:Key="DepartmentStackPanel" TargetType="StackPanel">
    <Setter Property="Margin" Value="10"/>
    <Setter Property="Opacity" Value="0.5"/>
    <Setter Property="Background" Value="Transparent"/>
    <Style.Triggers>
        <Trigger Property="IsMouseOver" Value="True">
            <Setter Property="Opacity" Value="1"/>
            <Setter Property="LayoutTransform"
                    Value="{StaticResource BigScale}"/>
        </Trigger>
    </Style.Triggers>
</Style>
```
```

# EVENT TRIGGERS AND ANIMATION

An event trigger lets you detect when an event occurs. Animation lets you change property values in a series of smoothly varying steps. Together, for example, you can make a Button detect the MouseOver event and use animation to enlarge the Button, providing graphical feedback similar to the experience provided by the previous property event.

# Event Triggers

A *property trigger* takes action when a control’s property has a certain value.

In contrast, an *event trigger* takes action when a control event occurs. Rather than acting when the IsMouseOver property is True, an event trigger might take action when the MouseEnter event fires, indicating that the mouse moved over the control. Another event could take some other action when the MouseLeave event fires, which occurs when the mouse moves off the control.