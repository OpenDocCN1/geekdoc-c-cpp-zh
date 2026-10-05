The Grid.Row attribute is an example of an attached property. An attached property is one that a control receives from the container control that it's placed in. Outside a grid, a TextBlock doesn't have a Row property, as it would be meaningless. When positioned within a grid, the Row property is attached to the TextBlock control, and the TextBlock control can assign it a value. The Grid then uses this value to determine where to display the TextBlock control. Attached properties are easy to sort because they have the form ContainerType.PropertyName.

+   Remove the Margin property of the TextBlock control and set the HorizontalAlignment and VerticalAlignment properties to Center. This will cause the TextBlock to appear centered in the row. The XAML markup for the Grid and TextBlock controls should look like this (the changes to the TextBlock are highlighted in bold):

Click here to view code image

```
<Grid Margin="10,20,10,20">
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Adventure Works Customers" VerticalAlignment="Center"
FontSize="50"/>/>
</Grid>
```

+   After the TextBlock control, add another nested Grid control. This Grid control will be used to lay out the controls in the body of the form. It should appear in the third row of the outer Grid control (the row of size 10), so set the Grid.Row property to 2, as shown in the following code:

Click here to view code image

```
<Grid Margin="10,20,10,20">
  <Grid.RowDefinitions>
    <RowDefinition Height="2*/>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
    <RowDefinition Height="2*"/>
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" HorizontalAlignment="Center" ... />
```