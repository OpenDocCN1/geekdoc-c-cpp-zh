```
<Trigger Property="IsDefaulted" Value='False'>
  <SSetter TargetName="ellEdgeHighlight" Property="Stroke"
    Value={StaticResource brEdgeHighlight}/>
</Trigger>
```

```
<!-- Disabled. This comes last so it gets ultimate precedence. -->
<Trigger Property="IsEnabled" Value="False'>
  <SSetter TargetName="ellCover" Property="Opacity" Value="0.6"/>
</Trigger>
```

![](bbox=[0.785, 0.223, 0.882, 0.249])

These triggers are fairly straightforward, giving controls new Stroke values and shuffling around Opacity values.

# TEMPLATE TRICKS 3

+   The EllipseExample demonstrates several useful template tricks including:
* Using BlurBitmapEffect to make an object appear three-dimensional(the outer edge with blurred highlight on it)
* Using Opacity <1 to make translucent highlights
* Using brushes that blend from a color to transparent to make highlights fade away
* Using brushes that blend a color to transparent and back to a color to make objects that are visible in multiple places
* Using different brushes for different control states (the normal vs. defaulted highlights)
* Using different BitmapEffects for different control states (the smaller glow for IsMouseOver and the larger glow for IsPressed)
* Animating changes to the brush's transformation

# RESEARCHING CONTROL TEMPLATES

To effectively build templates, you need to learn how the control provides for you and what behaviors you need to provide for it. You also need to determine what events the control provides so that you know you have a chance to make the control take action.

For example, WPF provides a confusing assortment of events including Mouse.MouseEnter, IsMouseOver, MouseLeftDown, Pressed, and Click. If you're trying to write a Button template, mouse events can you use to change the Button's appearance? Which properties and behaviors does the Button provide for you, and which ones do you need to implement?