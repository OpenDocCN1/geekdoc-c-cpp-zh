```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="StaticResource FontStyle">
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="SteelBlue"/>
  <Setter Property="RenderTransformOrigin" Value="0.5,0.5"/>
  <Setter Property="RenderTransform">
    <Setter.Value>
      <CompositeTransform Rotation="-5"/>
    </Setter.Value>
  </Setter>
</Style>
```