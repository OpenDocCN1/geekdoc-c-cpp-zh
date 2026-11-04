Figure 2-9:
Grid with row and column spans.

![](bbox=[0.22, 0.17, 0.34, 0.35])

# Listing 2-9: Column and Row Span XAML

```
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="2*" />
        <RowDefinition Height="3*" />
        <RowDefinition Height="5*" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="3*"/>
        <ColumnDefinition Width="3*"/>
    </Grid.ColumnDefinitions>
    <Border Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
        <TextBlock Text="0,0 - 0,1"/>
    </Border>
    <Border Grid.Row="1" Grid.Column="0" Grid.RowSpan="2" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
        <TextBlock Text="1,0 - 2,1"/>
    </Border>
    <Border Grid.Row="1" Grid.Column="1" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
        <TextBlock Text="1,1"/>
    </Border>
    <Border Grid.Row="2" Grid.Column="1" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
        <TextBlock Text="2,1"/>
    </Border>
</Grid>
```

# Horizontal and vertical alignment within parent container's layout slot

You align an element within a container's layout slot by setting the VerticalAlignment and HorizontalAlignment properties (see the Border element in Listing 2-9 for an example). Horizontal settings are Center, Left, Right, and Stretch. Vertical options are Center, Top, Bottom, and Stretch. Stretch specifies the element to fill all available space. Explicit sizing of elements overrides the Stretch setting.

# Content alignment within Content Controls

The same options can be used for setting the alignment of the Content within a Content Control by using the HorizontalContentAlignment and VerticalContentAlignment properties in the control.