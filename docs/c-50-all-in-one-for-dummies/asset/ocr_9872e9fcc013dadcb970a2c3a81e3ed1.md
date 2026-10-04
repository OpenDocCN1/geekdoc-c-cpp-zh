# Exploring Common XAML Controls 597

Both the ComboBox and ListBox shown in Figures 2-19 and 2-20 use the exact same XAML between the DataTemplate tags, so only the ComboBox XAML is shown in List 2-15.

The following XAML will not produce the right output without additional code in the code-behind file. The [Binding] element in line 3 needs some code output.

# Listing 2-15: ComboBox XAML

```
<ComboBox Margin="5,0" HorizontalAlignment="Stretch" HorizontalContentAlignment="Stretch"
  Source={Binding Path=People}">
  <DataTemplate>
    <Border HorizontalAlignment="Stretch" BorderBrush="AliceBlue"
      Thickness="1">
      <Grid HorizontalAlignment="Stretch">
        <Grid.RowDefinitions>
          <Row Height="Auto"/>
          <Row Height="Auto"/>
          <Row Height="Auto"/>
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
          <ColumnDefinition Width="Auto"/>
          <ColumnDefinition Width="Auto"/>
          <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="3" Margin="5,0" Text="{Binding Name}"/>
        <TextBlock Grid.Row="1" Grid.Column="0" Text="{Binding Address}"/>
        <TextBlock Grid.Row="2" Grid.Column="0" Margin="5,0" Text="{Binding City}"/>
        <TextBlock Grid.Row="2" Grid.Column="1" Margin="5,0" Text="{Binding State}"/>
        <TextBlock Grid.Row="2" Grid.Column="2" Margin="5,0" Text="{Binding Zip}"/>
      </Grid>
    </Border>
  </DataTemplate>
</ComboBox.ItemTemplate>
```

![](bbox=[0.125, 0.188, 0.195, 0.255])

Figure 2-19: The Combo-Box.

![](bbox=[0.215, 0.725, 0.415, 0.835])