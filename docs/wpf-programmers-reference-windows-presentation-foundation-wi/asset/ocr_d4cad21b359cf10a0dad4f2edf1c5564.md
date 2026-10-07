# GridSplitter 46

```
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<RowDefinitions>
<RowDefinition Height="*" />
<RowDefinition Height="*" />
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<GridSplitter Grid.Column="1" Grid.RowSpan="10"
HorizontalAlignment="Left"
VerticalAlignment="Stretch"
Background="Blue"
ShowsPreview="False"
Width="5" />
<GridSplitter Grid.Column="1" Grid.RowSpan="10"
HorizontalAlignment="Right"
VerticalAlignment="Stretch"
Background="Red"
ShowsPreview="False"
Width="5" />
</Grid>
```

The following code creates horizontal GridSplitters for the same Grid used in the previous example:

```
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<RowDefinitions>
<RowDefinition Height="*" />
<RowDefinition Height="*" />
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<GridSplitter Grid.Row="1" Grid.ColumnSpan="20"
HorizontalAlignment="Stretch"
VerticalAlignment="Top"
Background="Blue"
ShowsPreview="False"
Height="5" />
<GridSplitter Grid.Row="1" Grid.ColumnSpan="20"
HorizontalAlignment="Stretch"
VerticalAlignment="Bottom"
Background="Red"
ShowsPreview="False"
Height="5" />
<Image Source="baseball.jpg" Grid.Row="1" Grid.Column="1" />
</Grid>
```