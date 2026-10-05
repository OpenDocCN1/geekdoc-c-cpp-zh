```
</Grid.RowDefinitions>
<TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Customers" VerticalAlignment="Center" FontSize="30"/>
</Grid>
```

5. Add another Grid to row 1 of the customersColumnarView Grid control, directly after the TextBlock control that contains the Customers title. This Grid control will display the labels and data-entry controls in two columns, add the row and columns definitions shown in bold in the following code example to this Grid control:

Click here to view code image

```
<TextBlock Grid.Row="0" ... />
<Grid Grid.Row="1">
<Grid.ColumnDefinitions>
<ColumnDefinition/>
<ColumnDefinition/>
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition/>
<RowDefinition/>
<RowDefinition/>
<RowDefinition/>
<RowDefinition/>
<RowDefinition/>
</Grid.RowDefinitions>
</Grid>
```

> > **Note**
>
If all the rows or columns in a set have the same height or width, you don't need to specify their size.

6. Copy the XAML markup for the ID, Title, First Name, and Last Name TextBlock controls from the customersTabularView Grid to the new Grid control, immediately after the row definitions that you just added. Put the ID control in row 0, the Title control in row 1, the First Name control in row 2, and the Last Name control in row 3. Place all controls in column 0.