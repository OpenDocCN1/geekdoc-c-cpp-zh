```
...
<TextBlock Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="2" Style="{StaticResource ErrorMessageStyle}" Text="{Binding LastError}"/>
```

3. The TextBox and ComboBox controls that display customer data on the form should allow the user to modify this data only if the ViewModel is in Adding or Editing mode; otherwise, they should be disabled. Add the IsEnabled property to each of these controls and bind it to the IsAddingOrEditing property of the ViewModel as follows:

Click here to view code image

```
...
<TextBox Grid.Row="1" Grid.Column="1" x:Name="id" IsEnabled="{Binding IsAddingOrEditing}" .../>
<TextBox Grid.Row="1" Grid.Column="5" x:Name="firstName" IsEnabled="{Binding IsAddingOrEditing}" .../>
<TextBox Grid.Row="1" Grid.Column="7" x:Name="lastName" IsEnabled="{Binding IsAddingOrEditing}" .../>
<ComboBox Grid.Row="1" Grid.Column="3" x:Name="title" IsEnabled="{Binding IsAddingOrEditing}" .../>
...
<TextBox Grid.Row="3" Grid.Column="3" ... x:Name="email" IsEnabled="{Binding IsAddingOrEditing}" .../>
...
<TextBox Grid.Row="5" Grid.Column="3" ... x:Name="phone" IsEnabled="{Binding IsAddingOrEditing}" .../>
...
<TextBox Grid.Row="0" Grid.Column="1" x:Name="cId" /> IsEnabled="{Binding IsAddingOrEditing}" .../>
<TextBox Grid.Row="2" Grid.Column="1" x:Name="cFirstName" IsEnabled="{Binding IsAddingOrEditing}" .../>
<TextBox Grid.Row="3" Grid.Column="1" x:Name="cLastName" IsEnabled="{Binding IsAddingOrEditing}" .../>
<ComboBox Grid.Row="1" Grid.Column="1" x:Name="cTitle" IsEnabled="{Binding IsAddingOrEditing}" .../>
...
<TextBox Grid.Row="4" Grid.Column="1" x:Name="cEmail" IsEnabled="{Binding IsAddingOrEditing}" .../>
...
<TextBox Grid.Row="5" Grid.Column="1" x:Name="cPhone" IsEnabled="{Binding IsAddingOrEditing}" .../>
```

4. Add a command bar to the bottom of the page, immediately after the top command bar, using the <Page.BottomAppBar> element. This command bar should contain buttons for the AddCustomer, EditCustomer, SaveChanges, and DiscardChanges commands, as follows:

Click here to view code image

```
<Page ...>
...
<Page.TopAppBar >
```