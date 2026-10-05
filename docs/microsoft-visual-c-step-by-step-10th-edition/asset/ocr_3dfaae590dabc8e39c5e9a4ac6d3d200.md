```
<Setter Property="VerticalAlignment" Value="Center"/>
<Setter Property="Foreground" Value="SteelBlue"/>
</Style>
```

This is a composite style that sets the HorizontalAlignment, TextWrapping, VerticalAlignment, and Foreground properties of a TextBlock object. Additionally, the HeaderStyle references the FontStyle by using the BasedOn property. The BasedOn property provides a simple form of inheritance for styles.

You'll use this style to format the labels that appear at the top of the customersTableView and customersColumn controls. However, these headings have different font sizes (the heading for the tabular layout is bigger than that of the columnar layout), so you'll create two more styles to extend the HeaderStyle.

15. Add the styles shown here in bold to the AppStyles.xaml file:

Click here to view code image

```
<Style x:Key="HeaderStyle" TargetType="TextBlock" BasedOn={StaticResource FontStyle}
  ..
</Style>
<Style x:Key="TabularHeaderStyle" TargetType="TextBlock" BasedOn={StaticResource HeaderStyle}>
  <Setter Property="FontSize" Value="40"/>
</Style>
<Style x:Key="ColumnarHeaderStyle" TargetType="TextBlock" BasedOn={StaticResource HeaderStyle}>
  <Setter Property="FontSize" Value="30"/>
</Style>
```

Note that the font sizes for these styles are slightly smaller than the font sizes currently used by the headings in the Grid controls. This is because Segoe Print font is bigger than the default font.

Click here to view code image

```
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
```