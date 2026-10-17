
```xml
<userControl x:Class="StudentRecords.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">
  <Grid Height="385" Width="384">
    <Grid x:Name="LayoutGrid_Old">
      <TextBlock Text="Student Records" Margin="10,0,0,0" HorizontalAlignment="Center"
                 Foreground="Purple" FontSize="24" FontWeight="Bold"/>
      <TabControl x:Name="TabControl1" Foreground="Purple" FontSize="14">
        <TabItem Header="Students">
          <Grid x:Name="Grid_K231" Height="342" Width="300">
            <Grid.RowDefinitions>
              <RowDefinition Height="73" />
              <RowDefinition Height="48" />
              <RowDefinition Height="45" />
              <RowDefinition Height="45" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
              <ColumnDefinition Width="150" />
              <ColumnDefinition Width="150" />
            </Grid.ColumnDefinitions>
            <Border BorderBrush="Black" BorderThickness="5" Grid.Row="0" Grid.Column="0">
              <TextBlock Text="Subject" HorizontalAlignment="Center" VerticalAlignment="Center" FontSize="16" Foreground="OrangeRed"/>
            </Border>
            <Border BorderBrush="Black" BorderThickness="3" Grid.Row="0" Grid.Column="1">
              <TextBlock Text="Marks" HorizontalAlignment="Center" VerticalAlignment="Center" FontSize="16" Foreground="OrangeRed"/>
            </Border>
            <Border BorderBrush="Black" BorderThickness="2" Grid.Row="1" Grid.Column="0">
              <TextBlock Text="English" HorizontalAlignment="Center" VerticalAlignment="Center"/>
            </Border>
            <Border BorderBrush="Black" BorderThickness="1" Grid.Row="1" Grid.Column="1">
              <TextBlock Text="91" HorizontalAlignment="Center" VerticalAlignment="Center"/>
            </Border>
            <Border BorderBrush="Black" BorderThickness="2" Grid.Row="2" Grid.Column="0">
              <TextBlock Text="Mathematics" HorizontalAlignment="Center"/>
            </Border>
          </Grid>
        </TabItem>
      </TabControl>
      </Grid>
  </Grid>
</userControl>
```

```xml
<xml>
  <HorizontalAlignment="Center"
  <VerticalAlignment="Center" />
  <TextBlock Grid="0" Row="2" Grid.Column="1" Text="97" />
  <HorizontalAlignment="Center" VerticalAlignment="Center" />
  <BorderBrush="Black" BorderThickness="2" Grid.Row="2"
  <TextBlock Grid="0" Row="3" Text="Science" />
  <HorizontalAlignment="Center"
  <VerticalAlignment="Center" />
  <TextBlock Grid="0" Row="3" Grid.Column="1" Text="85" />
  <HorizontalAlignment="Center" VerticalAlignment="Center" />
  <BorderBrush="Black" BorderThickness="2"
  <Grid.Row="3" Grid.RowSpan="1" Grid.ColumnSpan="2" />
</Grid>
</Canvas>
</xml>
  <xml:Canvas>
  <xml:TextBlock.Content>
  <xml:TextBlock Header="Harvey, Jack" Foreground="Purple" FontWeight="Bold"
  FontSize="18" />
  <xml:Canvas>
  <xml:TextBlock Text="Student ID: K6232" />
  <xml:Canvas Left="44" Canvas.Top="24" Width="300" />
  <xml:Grid.RowDefinitions>
  <xml:RowDefinition height="75" />
  <xml:RowDefinition height="45" />
  <xml:RowDefinition height="45" />
  </xml:Grid.RowDefinitions>
  <xml:Grid.ColumnDefinitions>
  <xml:ColumnDefinition width="150" />
  <xml:ColumnDefinition width="150" />
  </xml:Grid.ColumnDefinitions>
  <xml:BorderBrush="Black" BorderThickness="5" Grid.Row="4" Grid.ColumnSpan="2" />
  <xml:BorderBrush="Black" BorderThickness="5" Grid.Row="5" Grid.ColumnSpan="1" />
  <xml:TextBlock Grid.Row="0" Text="Subject" />
  <xml:HorizontalAlignment="Center"
  <xml:VerticalAlignment="Center" FontWeight="Bold" />
  <xml:TextBlock Grid.Row="0" Grid.Column="1" Text="Marks" />
  <xml:HorizontalAlignment="Center" xml:VerticalAlignment="Center" />
  <xml:FontWeight="Bold" FontSize="18" Foreground="OrangeRed" />
  <xml:BorderBrush="Black" BorderThickness="3" />
  <xml:TextBlock Grid.Row="1" Text="English" />
  <xml:HorizontalAlignment="Center" xml:VerticalAlignment="Center" />
  <xml:TextBlock Grid.Row="1" Grid.Column="1" Text="77" />
  <xml:HorizontalAlignment="Center" xml:VerticalAlignment="Center" />
  <xml:BorderBrush="Black" BorderThickness="2" />
  <xml:Grid.Row="2" Grid.ColumnSpan="2" />
  <xml:TextBlock Grid.Row="2" Text="Mathematics" />
  <xml:HorizontalAlignment="Center" />
</TabItem>
```

```xml

<HorizontalAlignment="Center"

<VerticalAlignment="Center" />

<TextBlock Grid="0" Row="2" Grid.Column="1" Text="97" />

  <HorizontalAlignment="Center" VerticalAlignment="Center" />

  <BorderBrush="Black" BorderThickness="2" Grid.Row="2"

  <TextBlock Grid="0" Row="3" Text="Science" />

  <HorizontalAlignment="Center"

  <VerticalAlignment="Center" />

  <TextBlock Grid="0" Row="3" Grid.Column="1" Text="85" />

  <HorizontalAlignment="Center" VerticalAlignment="Center" />

  <BorderBrush="Black" BorderThickness="2"

  <Grid.Row="3" Grid.RowSpan="1" Grid.ColumnSpan="2" />

</Grid>

</Canvas>

  </xml>

  <xml:Canvas>

  <xml:TextBlock.Content>

  <xml:TextBlock Header="Harvey, Jack" Foreground="Purple" FontWeight="Bold"

  FontSize="18" />

  <xml:Canvas>

  <xml:TextBlock Text="Student ID: K6232" />

  <xml:Canvas Left="44" Canvas.Top="24" Width="300" />

  <xml:Grid.RowDefinitions>

  <xml:RowDefinition height="75" />

  <xml:RowDefinition height="45" />

  <xml:RowDefinition height="45" />

  </xml:Grid.RowDefinitions>

  <xml:Grid.ColumnDefinitions>

  <xml:ColumnDefinition width="150" />

  <xml:ColumnDefinition width="150" />

  </xml:Grid.ColumnDefinitions>

  <xml:BorderBrush="Black" BorderThickness="5" Grid.Row="4" Grid.ColumnSpan="2" />

  <xml:BorderBrush="Black" BorderThickness="5" Grid.Row="5" Grid.ColumnSpan="1" />

  <xml:TextBlock Grid.Row="0" Text="Subject" />

  <xml:HorizontalAlignment="Center"

  <xml:VerticalAlignment="Center" FontWeight="Bold" />

  <xml:TextBlock Grid.Row="0" Grid.Column="1" Text="Marks" />

  <xml:HorizontalAlignment="Center" xml:VerticalAlignment="Center" />

  <xml:FontWeight="Bold" FontSize="18" Foreground="OrangeRed" />

  <xml:BorderBrush="Black" BorderThickness="3" />

  <xml:TextBlock Grid.Row="1" Text="English" />

  <xml:HorizontalAlignment="Center" xml:VerticalAlignment="Center" />

  <xml:TextBlock Grid.Row="1" Grid.Column="1" Text="77" />

  <xml:HorizontalAlignment="Center" xml:VerticalAlignment="Center" />

  <xml:BorderBrush="Black" BorderThickness="2" />

  <xml:Grid.Row="2" Grid.ColumnSpan="2" />

  <xml:TextBlock Grid.Row="2" Text="Mathematics" />

  <xml:HorizontalAlignment="Center" />

</TabItem>
```
