Be aware that you won't see this change in the Design View window because the customersColumnarGridView control is collapsed by default. However, you will see the effects of this change when you run the app later in this exercise.

19. Return to the AppStyles.xaml style in the Code and Text Editor window. Modify the HeaderStyle with the additional property Setter elements shown in the following example:

Click here to view code image

```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="StaticResource FontStyle">
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="SteelBlue"/>
  <Setter Property="RenderTransformOrigin" Value="0.5,0.5"/>
  <Setter Property="RenderTransform">
    <CompositeTransform Rotation="-5"/>
  </Setter.Value>
</Setter>
</Style>
```

This example rotate the text displayed in the header about its midpoint by an angle of 5 degrees using a transformation.

![](bbox=[0.134, 0.587, 0.863, 0.873])