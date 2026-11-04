# Listing 2-11 (continued)

```
<TextBox Grid.Row="2" Grid.Column="2"
HorizontalAlignment="Stretch" />
<Label Grid.Row="3" Grid.Column="1" Content="City:"
HorizontalAlignment="Stretch" HorizontalContentAlignment="Right"/>
<TextBox Grid.Row="3" Grid.Column="2"
HorizontalAlignment="Stretch" />
<Button Grid.Row="3" Grid.Column="3" Content="Lookup"
Margin="3,0,3,0"/>
<Label Grid.Row="4" Grid.Column="1" Content="State:"
HorizontalAlignment="Stretch" HorizontalContentAlignment="Right"/>
<Grid Grid.Row="4" Grid.Column="2">
<Grid.RowDefinitions>
<RowDefinition Height="*"/>
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*"/>
<ColumnDefinition Width="Auto"/>
<ColumnDefinition Width="2*"/>
</Grid.ColumnDefinitions>
<TextBox Grid.Row="0" Grid.Column="0"
HorizontalAlignment="Stretch" />
<Label Grid.Row="0" Grid.Column="1" Content="Zip:"
HorizontalAlignment="Right" />
<TextBox Grid.Row="0" Grid.Column="2"
HorizontalAlignment="Stretch" />
</Grid>
<Grid Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="3">
<Grid.RowDefinitions>
<RowDefinition Height="Auto"/>
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*"/>
<ColumnDefinition Width="Auto"/>
<ColumnDefinition Width="Auto"/>
</Grid.ColumnDefinitions>
<Button Grid.Row="0" Grid.Column="1" Content="Save"
Margin="3,0"/>
<Button Grid.Row="0" Grid.Column="2" Content="Close"
Margin="3,0"/>
</Grid>
</Grid>
```

And yes, that's a lot of XAML! One of the many great things about WPF is the flexibility to be able to create just about any look and feel you can dream up. But, sometimes (well, most of the time) it will take a lot of angle-brackets.