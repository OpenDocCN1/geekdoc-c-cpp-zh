10 pixels. The size of the second ellipse is also determined by the size of the top-right cell, minus the specified Margin.

The third Ellipse is placed in the second row. It also has a ColumnSpan attribute set to 2, so that it will occupy both cells in the second row.

If the intention is for the contents of a Cell to not occupy the entire space, you must change the HorizontalAlignment and VerticalAlignment properties. These properties default to Stretch, but you can also take on the value of HorizontalAlignment.Left, HorizontalAlignment.Center, HorizontalAlignment.Right, or VerticalAlignment.Top, VerticalAlignment.Center, VerticalAlignment.Bottom, respectively. In this case, you can use the Margin property to set the distance from the edges of the cell.

# Viewbox

Viewbox is a new addition to the Silverlight core framework. It is part of the Silverlight Toolkit before Silverlight 4.0 (Silverlight Toolkit is a set of Open Source controls developed by Microsoft that is not part of the Silverlight core platform.) Just like Border, Viewbox can have only one child. The goal of the Viewbox is to provide resizing strategies if the content does not fit in the available space.

This example has a Grid with four equally sized cells; every cell has a Viewbox in it. The most important property if a Viewbox is the Stretch property. The Stretch property defines how the content of the Viewbox is resized.

```
<Grid xName="LayoutRoot" Background="White">
<Grid.RowDefinitions>
  <RowDefinition Height="150" />
  <RowDefinition Height="150" />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
  <ColumnDefinition Width="200" />
  <ColumnDefinition Width="200" />
</Grid.ColumnDefinitions>
<Viewbox Stretch="None">
  <Button Content="Stretch:None" />
</Viewbox>
<Viewbox Stretch="Fill" Grid.Column="1">
  <Button Content="Stretch:Fill" />
</Viewbox>
<Viewbox Stretch="Uniform" Grid.Row="1">
  <Button Content="Stretch:Uniform" />
</Viewbox>
<Viewbox Stretch="UniformToFill" Grid.Column="1" Grid.Row="1">
  <Button Content="Stretch:UniformToFill" />
</Viewbox>
</Grid>
```