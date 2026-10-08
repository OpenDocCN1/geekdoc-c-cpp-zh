```
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="136" />
<ColumnDefinition Width="264" />
</Grid.ColumnDefinitions>
<Ellipse Stroke="Black" StrokeThickness="1" Fill="White" />
<Ellipse Stroke="Black" StrokeThickness="3" Fill="White" Grid.Column="1" 
Margin="10,10,10,0" />
<Ellipse Stroke="Black" StrokeThickness="5" Fill="White" Grid.Row="1" 
Grid.ColumnSpan="2" />
</Grid>
```

![](bbox=[0.095, 0.313, 0.536, 0.574])

FIGURE 8-13: Grid as a layout container

This XAML snippet creates a Grid with gray background. The Grid has two rows: the second is twice as big as the first one. This means that if the Grid is 300 pixels high, the first row will be 100 pixels, and the second 200 pixels high. The Grid also has two columns; they have a fixed size of 136 and 264 pixels. It is also possible to have a row or column auto-sized. In this case, the size of the content and the remaining space from the other rows or columns determine the size of the row or column.

The Grid has three Ellipses in it. The first one is in Column 0 and Row 0 (if no Grid.Row or Grid.Column attributes are specified, the size of the first Ellipse is determined by the size of the top-left cell).

The Grid.Column="1" attribute of the second Ellipse puts it in the second column of the first row. This Ellipse also has a Margin="10,10,10,0", meaning that the top and left margins are