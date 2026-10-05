You can expand and contract elements in the XAML pane of the Design View window and make the structure easier to read by selecting the + - signs that appear down the left edge of the XAML markup.

Click here to view code image

```
<Grid>
  <Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Collapsed">
  ..
  </Grid>
  <Grid x:Name="customersColumnView" Margin="10,20,10,20" Visibility="Visible">
  </Grid>
</Grid>
```

This Grid control will hold the "narrow" view of the form. The fields in this grid will be laid out in a columnar manner as described earlier.

+   3. In the customersColumnView Grid control, add the following row definitions:

Click here to view code image

```
<Grid x:Name="customersColumnView" Margin="10,20,10,20" Visibility="Visible">
  <Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
  </Grid.RowDefinitions>
</Grid>
```

You'll use the row to display the first and the second, much larger row to display the controls in which users enter data.

+   4. Immediately after the row definitions, the TextBlock control shown here in bold. This control displays a truncated title, Customers, in the first row of the Grid. Set FontSize to 30.

Click here to view code image

```
<Grid x:Name="customersColumnView" Margin="10,20,10,20" Visibility="Visible">
  <Grid.RowDefinitions>
  ...
</Grid>
```