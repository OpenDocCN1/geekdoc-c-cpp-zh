Again, the height of each row is specified in relative terms, as is the width of each column. Also, you can clearly see that the TextBox elements for Email and Phone do not quite fit this grid pattern. If you were being pedantic, you might choose to define further grids inside the body of the form to make these items fit. However, you should keep in mind the purpose of this grid, which is to define the relative positioning and spacing of elements. Therefore, it is acceptable for an element to extend beyond the boundaries of a cell in the grid arrangement.

In the next exercise, you will modify the layout of the Customers app to use this grid format to position the controls.

# Modify the layout to scale to different form factors and orientations

+   1. In the XAML pane for the Customers app, add another Grid inside the existing Grid element. Give this new Grid a margin of 10 pixels from the left and right edges of the parent Grid and 20 pixels from the top and bottom, as shown in bold in the following code:

Click here to view code image

```
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid Margin="10,20,10,20">
    </Grid>
    <TextBlock HorizontalAlignment="Left" TextWrapping="Wrap" Text="Adventure Works Customers" ... />
    ...
</Grid>
```

You could define the rows and columns as part of the existing Grid, but to maintain a consistent look and feel with other UWP apps, you should leave some blank space to the left and at the top of a page.

+   2. Add to the new Grid element the following <Grid.RowDefinitions> section shown in bold.

Click here to view code image

```
<Grid Margin="10,20,10,20">
    <Grid.RowDefinitions>
        <RowDefinition Height="2*"/>
        <RowDefinition Height="*"/>
        <RowDefinition Height="10*"/>
        <RowDefinition Height="2*"/>
    </Grid.RowDefinitions>
</Grid>
```

The <Grid.RowDefinitions> section defines the rows for the grid. In this example, you have defined four rows. You can specify the size of a row as an absolute value specified in pixels, or you can use the * operator to indicate that the sizes are relative and that Windows should calculate the row sizes itself when the app runs, depending on the form factor and