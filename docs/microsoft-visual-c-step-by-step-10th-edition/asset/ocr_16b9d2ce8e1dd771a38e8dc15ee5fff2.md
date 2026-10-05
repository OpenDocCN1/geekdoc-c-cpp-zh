```
<Grid x:Name="customersTabularView" Margin="10,20,10,20" Visibility="Visible">
  ...
  <Grid Grid.Row="2">
    ...\n    <TextBlock Grid.Row="0" Grid.Column="1" Style="{StaticResource TLabel} Text="ID"/>
    <TextBlock Grid.Row="0" Grid.Column="3" Style="{StaticResource TLabel} Text="Title"/>
    <TextBlock Grid.Row="0" Grid.Column="5" Style="{StaticResource TLabel} Text="First Name"/>
    <TextBlock Grid.Row="0" Grid.Column="7" Style="{StaticResource TLabel} Text="Last Name"/>
    ...\n    <TextBlock Grid.Row="3" Grid.Column="1" Style="{StaticResource TLabel} Text="Email"/>
    ...\n    <TextBlock Grid.Row="5" Grid.Column="1" Style="{StaticResource TLabel} Text="Phone"/>
    ...\n  </Grid>
  <Grid x:Name="customersColumnarView" Margin="10,20,10,20" Visibility="Collapsed">
    ...\n    <Grid Grid.Row="1">
      ...\n      <TextBlock Grid.Row="0" Grid.Column="0" Style="{StaticResource TLabel} Text="ID"/>
      <TextBlock Grid.Row="1" Grid.Column="0" Style="{StaticResource TLabel} Text="Title"/>
      <TextBlock Grid.Row="2" Grid.Column="0" Style="{StaticResource TLabel} Text="First Name"/>
      <TextBlock Grid.Row="3" Grid.Column="0" Style="{StaticResource TLabel} Text="Last Name"/>
      ...\n      <TextBlock Grid.Row="4" Grid.Column="0" Style="{StaticResource TLabel} Text="Email"/>
      ...\n      <TextBlock Grid.Row="5" Grid.Column="0" Style="{StaticResource TLabel} Text="Phone"/>
    />
  </Grid>
</Grid>
```