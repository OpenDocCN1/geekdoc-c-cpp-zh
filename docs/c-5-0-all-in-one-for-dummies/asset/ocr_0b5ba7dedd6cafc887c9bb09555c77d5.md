```
<StackPanel Orientation="Vertical"
VerticalAlignment="Center">

<TextBlock FontSize="25" Foreground="Goldenrod"
Text="{Binding Path=ServerName}" />

<TextBlock FontSize="18" Foreground="BlueViolet"
Text="{Binding Path=NumberOfConnectedUsers}" />
</StackPanel>

</StackPanel>
</Border>
</DataTemplate>

</Window.Resources>
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition />
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition />
</Grid.RowDefinitions>

<ListBox x:Name="listServers" Width="490" Height="350"
ItemsSource="{Binding}" Grid.Row="0" Grid.Column="0"
ItemTemplate="{StaticResource ResourceKey=ServerTemplate}" />
</Grid>
</Window>
```

The first thing to note in MainWindow.xaml is that the namespace for the local assembly (BindingSample3) was added to the Window (identified by the namespace definition in the Window tag with the prefix local). This enables you to instantiate classes that are defined in the current assembly in XAML, such as BooleanToIconConverter.

```
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:BindingSample3"
Title="MainWindow" Height="400" Width="525">
<Window.Resources>
<local:BooleanToIconConverter x:Key="BooleanToIconConverter" />
```

In the Window resources, you initialize an instance of your BooleanToIconConverter, which is available to you through the local namespace.

```
<local:BooleanToIconConverter x:Key="BooleanToIconConverter" />
```

The next Window resource that is defined is a data template. This data template provides a way to look at the data associated with a server's current status. The data template is defined as follows:

```
<DataTemplate x:Key="ServerTemplate">
<Border BorderBrush="Blue" Margin="3" Padding="3"
BorderThickness="2" CornerRadius="5" Background="Beige">
```