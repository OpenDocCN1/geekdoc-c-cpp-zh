Grid.Column property for the First Name label to 5, and the Grid.Column property for the Last Name label to 7.

+   10. Remove the Margin property from each of the TextBlock controls and set the HorizontalAlignment and VerticalAlignment properties to Center. The XAML markup for these controls should look like this (the changes are highlighted in bold):

Click here to view code image

```
<Grid Grid.Row="2">
  <Grid.RowDefinitions>
    ..
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    ..
  </Grid.ColumnDefinitions>
  <TextBlock Grid.Rows="0" Grid.Column="1" HorizontalAlignment="Center"
  <TextWrapping="Wrap" Text="ID" VerticalAlignment="Center" FontSize="20"/>
  <TextBlock Grid.Rows="0" Grid.Column="3" HorizontalAlignment="Center"
  <TextWrapping="Wrap" Text="Title" VerticalAlignment="Center" FontSize="20"/>
  <TextBlock Grid.Row="0" Grid.Column="5" HorizontalAlignment="Center"
  <TextWrapping="Wrap" Text="First Name" VerticalAlignment="Center" FontSize="20"/>
  <TextBlock Grid.Row="0" Grid.Column="7" HorizontalAlignment="Center"
  <TextWrapping="Wrap" Text="Last Name" VerticalAlignment="Center" FontSize="20"/>
</Grid>
```

+   11. Move the id, firstName, and lastName TextBox controls and the title ComboBox control inside the nested Grid control, immediately after the Last NameTextBlock control. Place these controls in row 1 of the Grid control. Put the id control in column 1, the title control in column 3, the firstName control in column 5, and the lastName control in column 7.

+   12. Remove the Margin of each of these controls and set the VerticalAlignment property to Center. Remove the Width property and set the HorizontalAlignment to Stretch. This causes the control to occupy