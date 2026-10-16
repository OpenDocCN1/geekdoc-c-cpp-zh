```
<Label Content="{Binding DisplayName}"/>
</DataTemplate>
</Window.Resources>
```

The ListBox that is placed in the left side of the window sets the ItemsSource property to {Binding}. This way, the data that is shown in the list is received from the DataContext property that was set in the RefreshServiceList method. The ItemTemplate property references the resource listTemplate that is defined with the DataTemplate shown earlier. The property IsSynchronizedWithCurrentItem is set to True so that the TextBox and Button controls inside the same window are bound to the current item selected with the ListBox:

```
<ListBox Grid.Row="0" Grid.Column="0" HorizontalAlignment="Left" Name="listBoxServices" VerticalAlignment="Top" ItemsSource="{Binding}" ItemTemplate="{StaticResource listTemplate}" IsSynchronizedWithCurrentItem="True">
</ListBox>
```

To differentiate the Button controls to start/stop/pause/continue the service, the following enumeration is defined (code file ServiceControlWPF/ButtonState.cs):

```
public enum ButtonState
{
    Start,
    Stop,
    Pause,
    Continue
}
```

With the TextBlock controls, the Text property is bound to the corresponding property of the ServiceControllerInfo instance. Whether the Button controls are enabled or disabled is also defined from the data binding by binding the IsEnabled property to the corresponding properties of the ServiceControllerInfo instance that return a Boolean value. The Tag property of the buttons is assigned to a value of the ButtonState enumeration defined earlier to differentiate the button within the same handler method OnServiceCommand (code file ServiceControlWPF/MainWindow.xaml):

```
<TextBlock Grid.Row="0" Grid.ColumnSpan="2" Text="{Binding /DisplayName, Mode=OneTime}" />
<TextBlock Grid.Row="1" Grid.ColumnSpan="2" Text="{Binding /ServiceStatusName, Mode=OneTime}" />
<TextBlock Grid.Row="2" Grid.ColumnSpan="2" Text="{Binding /ServiceTypeName, Mode=OneTime}" />
<TextBlock Grid.Row="3" Grid.ColumnSpan="2" Text="{Binding /ServiceName, Mode=OneTime}" />
<Button Grid.Row="4" Grid.Column="0" Content="Start" IsEnabled="{Binding /EnableStart, Mode=OneTime}" Tag="{x:Static local:ButtonState.Start}" Click="OnServiceCommand" />
<Button Grid.Row="4" Grid.Column="1" Name="buttonStop" Content="Stop" IsEnabled="{Binding /EnableStop, Mode=OneTime}" Tag="{x:Static local:ButtonState.Stop}" Click="OnServiceCommand" />
```