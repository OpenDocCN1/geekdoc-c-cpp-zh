```
<Style x:Key="FontStyle" TargetType="TextBlock">
</Style>
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn={StaticResource FontStyle}>
  <Setter Property="HorizontalAlignment" Value="Center"/>
  <Setter Property="TextWrapping" Value="Wrap"/>
  <Setter Property="VerticalAlignment" Value="Center"/>
  <Setter Property="Foreground" Value="SteelBlue"/>
</Style>
```