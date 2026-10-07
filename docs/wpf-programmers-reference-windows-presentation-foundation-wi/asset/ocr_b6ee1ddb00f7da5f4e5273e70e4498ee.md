# CHAPTER 2 WPF IN VISUAL STUDIO

![](bbox=[0.095, 0.096, 0.656, 0.468])

FIGURE 2-6

For example, the Window Designer will not create or apply styles, templates, storyboards, although if you enter them in the XAML code, it will use its best to honor them.

Sometimes it's easier to edit the XAML than to use the Window Designer. For example, setting exact row and column sizes in a Grid can be tricky in the Window Designer, but it's easy in XAML. Define some row and columns in the Grid, find the RowDefinition and ColumnDefinition elements, and set their Height and Width attributes.

For example, the following code gives a Grid two rows, one of height 30 pixels and one using all the remaining vertical space. It gives the Grid three columns of equal widths.

```
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="30" />
    <RowDefinition Height="*" />
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="33*" />
    <ColumnDefinition Width="33*" />
    <ColumnDefinition Width="33*" />
  </Grid.ColumnDefinitions>
</Grid>
```

You could finely set the Grid's column widths in the Window Designer, but it would be tricky to make them exactly equal. The Window Designer also can set a row to a fixed value such as 30 pixels.