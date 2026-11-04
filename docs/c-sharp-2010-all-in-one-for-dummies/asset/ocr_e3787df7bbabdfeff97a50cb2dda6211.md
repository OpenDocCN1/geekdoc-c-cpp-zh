```
~~~xaml
<StackPanel Orientation="Horizontal">

    <Label Content="{Binding
        Path=IsServerUp,
        Converter={StaticResource BooleanToIconConverter}}" />

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
~~~
```

![](bbox=[0.095, 0.42, 0.235, 0.515])

In Chapter 1, I state that one of the main reasons to adopt WPF as a user interface technology is its data visualization flexibility. Data templates enable you to represent data contained in an object using any number of XAML elements. The world is your oyster, and you can get as creative as you want to relay application information to your user in the most usable, intuitive fashion using data templates.

Let’s analyze the ServerTemplate data template. This data template represents the display of an instance of a ServerStatus object. Look at the Label element in the data template:

```
~~~xaml
<Label Content="{Binding Path=IsServerUp,
    Converter={StaticResource BooleanToIconConverter}}" />
~~~
```

The Content property of the label is bound to the Boolean IsServerUp property of the ServerStatus object. You’ll also notice that there is another component to the binding expression, called Converter. This is where the Boolean value (IsServerUp) gets passed into the BooleanToIconConverter and is rendered as the RedX or the GreenCheck user control, depending on its value.

The rest of the data template simply outputs the server name of the ServerStatus object in yellow, and the number of connected users in blue-violet.

Within the Grid on the Window, a ListBox control is defined that displays a list of servers on the network. Let’s look at the definition of the ListBox:

```
~~~xaml
<ListBox x:Name="lstServers" Width="490" Height="350"
    Grid.Row="0" Grid.Column="0"
    ItemsSource="{Binding}"
    ItemTemplate="{StaticResource ResourceKey=ServerTemplate}" />
~~~
```