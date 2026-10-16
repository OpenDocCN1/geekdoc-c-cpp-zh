set the Width property to *. To have the size doubled for another column, you specify 2*. The sample code, which defines two columns and three rows, doesn't define additional settings with the column and row definitions; the default is the star sizing.

The grid contains several Label and TextBox controls. Because the parent of these controls is a grid, you can set the attached properties Column, ColumnSpan, Row, and RowSpan (code file LayoutSamples/GridWindow.xaml):

```
<Grid ShowGridLines="True">
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition />
        <RowDefinition />
        <RowDefinition />
    </Grid.RowDefinitions>
    <Label Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" VerticalAlignment="Center" HorizontalAlignment="Center" Content="Title" />
    <Label Grid.Column="0" Grid.Row="1" VerticalAlignment="Center" Content="Firstname:" Margin="10" />
    <TextBox Grid.Column="1" Grid.Row="1" Width="100" Height="30" />
    <Label Grid.Column="0" Grid.Row="2" VerticalAlignment="Center" Content="Lastname:" Margin="10" />
    <TextBox Grid.Column="1" Grid.Row="2" Width="100" Height="30" />
</Grid>
```

The outcome of arranging controls in a grid is shown in Figure 34.9. For easier viewing of the columns and rows, the property ShowGridLines is set to true.