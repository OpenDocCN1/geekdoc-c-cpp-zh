```
<Grid x:Name="customersTabularView ...>
...
  <TextBox Grid.Row="1" Grid.Column="5" x:Name="firstName" ...
  Text="{Binding FirstName}" .../>
  <TextBox Grid.Row="1" Grid.Column="7" x:Name="lastName" ...
  Text="{Binding LastName}" .../>
  <TextBox Grid.Row="3" Grid.Column="3" Grid.ColumnSpan="5"
  x:Name="email" ... Text="{Binding EmailAddress}" .../>
  <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3"
  x:Name="phone" ... Text="{Binding Phone}" .../>
  
</Grid>
<Grid x:Name="customersColumnarView" Margin="10,20,10,20"
  Visibility="Collapsed">
  <TextBox Grid.Row="0" Grid.Column="1" x:Name="cId" ...
  Text="{Binding CustomerID}" .../>
  <TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName" ...
  Text="{Binding FirstName}" .../>
  <TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName" ...
  Text="{Binding LastName}" .../>
  <TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail" ...
  Text="{Binding EmailAddress}" .../>
  <TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone" ...
  Text="{Binding Phone}" .../>
</Grid>
```