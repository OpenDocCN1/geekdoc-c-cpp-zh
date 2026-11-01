
The code for this layout is as follows (you can find it in the downloadable code at LayoutExamples\DockPanels.xaml):

```
<Window x:Class="LayoutExamples.DockPanels"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:local="clr-namespace:LayoutExamples"
mc:Ignorable="d"
Title="DockPanel" Height="300" Width="300">
<DockPanel Background="AliceBlue">
<Border DockPanel.Dock="Top" Padding="10" Margin="5"
Background="Aquamarine" Height="45">
<Label>1) DockPanel.Dock="Top"</Label>
</Border>
<Border DockPanel.Dock="Top" Padding="10" Margin="5"
Background="PaleVioletRed" Height="45" Width="200">
<Label>2) DockPanel.Dock="Top"</Label>
</Border>
<Border DockPanel.Dock="Left" Padding="10" Margin="5"
Background="Bisque" Width="200">
<Label>3) DockPanel.Dock="Left"</Label>
</Border>
<Border DockPanel.Dock="Bottom" Padding="10" Margin="5"
Background="Ivory" Width="200" HorizontalAlignment="Right">
<Label>4) DockPanel.Dock="Bottom"</Label>
</Border>
<Border Padding="10" Margin="5" Background="BlueViolet">
<Label Foreground="White">5) Last control</Label>
</Border>
</DockPanel>
</Window>
```

This code uses the Border control introduced earlier to clearly mark out the docked control regions in the example layout, along with Label controls to output simple informative text. To understand the layout, you must read it from top to bottom, looking at each control in turn:

- 1. The first Border control is docked to the top of the DockPanel. The total area taken up in the DockPanel is the top 55 pixels (Height + 2 × Margin). Note that the Padding property does not affect this layout, as it is inside the edge of the Border, but this property does control the positioning of the embedded Label control. The Border control fills any available space along the edge it is docked to if not constrained by Height or Width properties, which is why it stretches across the DockPanel.
- 2. The second Border control is also docked to the top of the DockPanel, and takes up another 55 pixels from the top of the display area. This Border control also includes a Width property, which causes the border to take up only a portion of the width of the DockPanel. It is positioned centrally, as the default value for HorizontalAlignment in a DockPanel is Center.
- 3. The third Border control is docked to the left of the DockPanel and takes up 210 pixels of the left of the display.
- 4. The fourth Border control is docked to the bottom of the DockPanel and takes up 30 pixels plus the height of the Label control it contains (whatever that is). This height is determined by the Margin, Padding, and contents of the Border control, as it is not specified explicitly. The Border control is locked to the bottom-right corner of the DockPanel, as it has a HorizontalAlignment of Right.
- 5. The fifth and final Border control fills the remaining space.

Run this example and experiment with resizing content. Note that the further up the stacking order a control is, the more priority is given to its space. By shrinking the window, the fifth Border control can be completely obscured by controls further up the stacking order. Be careful when using DockPanel control layout to avoid this, perhaps by setting minimum dimensions for the window.

## StackPanel

You can think of StackPanel as being a slimmed down version of DockPanel, where the edge to which child controls are docked is fixed for those controls. The other difference between these controls is that the last child control of a StackPanel doesn't fill the remaining space. However, controls will, by default, stretch to the edges of the StackPanel control.

The direction in which controls are stacked is determined by three properties. Orientation can be set to Horizontal or Vertical, and HorizontalAlignment and VerticalAlignment can be used to determine whether control stacks are positioned next to the top, bottom, left, or right edge of the StackPanel. You can even make the stacked controls stack at the center of the StackPanel using the Center value for the alignment property you use.

Figure 14-5 shows two StackPanel controls, each of which contains three buttons. The top StackPanel has its Orientation property set to Horizontal and the bottom one has Orientation set to Vertical.

![](img/cf72ea860016d2d680fc085fc06f265a_455_0.png)

FIGURE 14-5

The code used here is as follows (you can find it in the downloaded code at LayoutExamples\StackPanels.xaml):

```xml
<Window x:Class="LayoutExamples.StackPanels"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:local="clr-namespace:LayoutExamples"
mc:Ignorable="d"
Title="StackPanel" Height="300" Width="300">
    <Grid>
        <StackPanel HorizontalAlignment="Left" Height="128" VerticalAlignment="Top" Width="284" Orientation="Horizontal">
            <Button Content="Button" Height="128" VerticalAlignment="Top" Width="75"/>
            <Button Content="Button" Height="128" VerticalAlignment="Top" Width="75"/>
            <Button Content="Button" Height="128" VerticalAlignment="Top" Width="75"/>
        </StackPanel>
        <StackPanel HorizontalAlignment="Left" Height="128" VerticalAlignment="Top" Width="284" Margin="0,128,0,0" Orientation="Vertical">
            <Button Content="Button" HorizontalAlignment="Left" Width="284"/>
            <Button Content="Button" HorizontalAlignment="Left" Width="284"/>
            <Button Content="Button" HorizontalAlignment="Left" Width="284"/>
        </StackPanel>
    </Grid>
</Window>
```

## WrapPanel

WrapPanel is essentially an extended version of StackPanel; controls that “don’t fit” are moved to additional rows (or columns). Figure 14-6 shows a WrapPanel control containing multiple shapes, with the window resized to two sizes.

![](img/cf72ea860016d2d680fc085fc06f265a_456_0.png)

FIGURE 14-6

The code to achieve this effect is shown here (you can find it in the downloaded code at LayoutExamples\WrapPanel.xaml):

```xml
<Window x:Class="LayoutExamples.WrapPanel"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
```

> NOTE You can also define rows and columns in the grid by clicking the edges of the grid in the Design View. If you move the mouse pointer to the edge of the grid, a yellow line is drawn across the Design View; if you click the edge, the necessary XAML is inserted. When you do this, the Width and Height properties of the rows and columns are always set by the designer, but you can delete them or drag the lines to suit your needs.

You can control the resizing with the Width, Height, MinWidth, MaxWidth, MinHeight, and MaxHeight properties. For example, setting the Width property of a column ensures that the column stays at that width. You can also set the Width property of a column to *, which means "fill the remaining space after calculating the width of all other columns." This is actually the default. When you have multiple columns with a Width of *, then the remaining space is divided between them equally. The * value can also be used with the Height property of rows. The other possible value for Height and Width is Auto, which sizes the row or column according to its content. You can also use GridSplitter controls to enable users to customize the dimensions of rows and columns by clicking and dragging.

Child controls of a Grid control can use the attached Grid.Column and Grid.Row properties to specify which cell they are contained in. Both these properties default to 0, so if you omit them, then the child control is placed in the top-left cell. Child controls can also use Grid.ColumnSpan and Grid.RowSpan to be positioned over multiple cells in a table, where the upper-left cell is specified by Grid.Column and Grid.Row.

## TRY IT OUT Using Rows and Columns: Ch14Ex01\MainWindow.xaml

Return to the example from the beginning of the chapter with the two buttons and follow these steps.

- 1. Select the Grid control by clicking in the XAML View.
- 2. Move the mouse pointer to the top edge of the grid in Design View; you'll see an orange line appear across the surface of the grid. Allow room for a button and click to create two columns.
- 3. Repeat Step 2 on the left edge of the window, creating two rows.
- 4. Select the first of the two buttons. Note that the action of adding the rows and columns automatically added the Grid.Row and Grid.Column properties to the button. Change the Grid.Row and Grid.Column attached properties to 0.
- 5. Adjust the Margin property to make the button fully visible in the cell.
- 6. The second button has also been adjusted. For example, a Margin has been added. Now delete the Margin property from the second button.
