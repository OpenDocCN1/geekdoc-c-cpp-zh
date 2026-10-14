At this stage, it would be possible to reference the FontStyle style in every TextBlock control that required this font, but this approach would not provide any advantage over simply setting the FontFamily directly in the markup for each control. The real power of styles occurs when you combine multiple properties, as you will see in the next few steps.

Click here to view code image

```
Add the HeaderStyle style shown here to the AppStyles.xaml file:
<Style x:Key="FontStyle"
TargetType="TextBlock">
...
</Style>
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="
{StaticResource FontStyle}">
    <Setter Property="HorizontalAlignment" Value="Center"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Foreground" Value="SteelBlue"/>
</Style>
```

This is a composite style that sets the HorizontalAlignment, TextWrapping, VerticalAlignment, and Foreground properties of a TextBlock. Additionally, the HeaderStyle style references the FontStyle style by using the BasedOn property. The BasedOn property provides a simple form of inheritance for styles.

You will use this style to format the labels that appear at the top of the customersTabularView and customersColumnarView controls. However, these headings have different font sizes (the heading for the tabular layout is bigger than that of the columnar layout), so you will create two more styles that extend the HeaderStyle style.

# 12. Add the following styles to the AppStyles.xaml file:

Click here to view code image

```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn="
{StaticResource FontStyle}">
...
</Style>
<Style x:Key="TabularHeaderStyle" TargetType="TextBlock"
BasedOn="{StaticResource HeaderStyle}">
    <Setter Property="FontSize" Value="40"/>
</Style>

<Style x:Key="ColumnarHeaderStyle" TargetType="TextBlock"
BasedOn="{StaticResource HeaderStyle}">
    <Setter Property="FontSize" Value="30"/>
</Style>
```

Note that the font sizes for these styles are slightly smaller than the font sizes currently used by the headings in the Grid controls. This is because