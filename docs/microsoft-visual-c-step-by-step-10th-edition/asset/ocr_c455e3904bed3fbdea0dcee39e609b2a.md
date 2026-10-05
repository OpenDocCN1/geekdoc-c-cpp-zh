```
<Grid.Row="2">
  <Grid.RowDefinitions>
    ...
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    ...
  </Grid.ColumnDefinitions>
  ...\n  <TextBox ... x:Name="email" .../> .../>
  <TextBlock Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" TextWrapping="Wrap" Text="Phone" VerticalAlignment="Center" FontSize="20"/>
  <TextBox Grid.Row="5" Grid.Column="3" Grid.ColumnSpan="3" x:Name="phone" HorizontalAlignment="Left" TextWrapping="Wrap" Text="" VerticalAlignment="Center" Width="200" FontSize="20"/>
</Grid>
```