
the status of servers on the network. In this project, you implement two user controls, RedX and GreenCheck. You also create a value converter named BooleanToIconConverter that converts a Boolean False value to display the RedX control and converts a True value to display the GreenCheck control. These values indicate whether the server is available.

A user control is a collection of reusable XAML. It can be made up of any number of elements and is implemented with the same rules as when you implement a normal Window (for instance, you can have only one root element). You can also define properties (including dependency properties!) on user controls.

![](img/80ff26f06fc9ab951e1cd4257b867366_640_0.png)

Project is available on the web under BindingSample3.

Follow these steps to create your sample:

- 1. Create a new WPF application named BindingSample3.
- 2. Add a new User Control to the project; name it GreenCheck.xaml.
- 3. Replace the XAML found in GreenCheck.xaml with this XAML:

```
<UserControl x:Class="BindingSample3.GreenCheck"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
d:DesignHeight="50" d:DesignWidth="50">

<Canvas x:Name="CheckCanvas" Width="50.4845" Height="49.6377"
Canvas.Left="0" Canvas.Top="0">

<Path x:Name="CheckPath" Width="43.4167" Height="45.6667"
Canvas.Left="0" Canvas.Top="1.3113e-006"
Stretch="Fill" Fill="#FF00642"
Data="F1 M 19.0833,45.6667 3.4167,2.16667 38,
1.3113e-006L 19.0833,42.58331 2.41667,25.3333L 0,
27.9167L 17.4167,44.25"/>

</Canvas>
</UserControl>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_640_1.png)

You’re not expected to come up with things like the CheckPath off the top of your head. (The path is what describes how the check mark is drawn.) In the Expression Suite, you find designer tools that allow you to draw items in a graphics program and export your final graphics in a XAML format. Expression Design was the tool used to create the user controls in this example.

- 4. Add another user control to the project; name it RedX.xaml.
- 5. Replace the XAML in the RedX.xaml file with this XAML:

```
<UserControl x:Class="BindingSample3.RedX"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
mc:Ignorable="d" d:DesignHeight="50" d:DesignWidth="50">

    <Canvas Width="44.625" Height="45.9394">

        <Path x:Name="Line1Path" Width="44.625" Height="44.375" Canvas.Left="0" Canvas.Top="0" Stretch="Fill" Fill="#FFDE0909" Data="F1 M 0,3.5L 3.5,0 44.625,41.125,44.375"/>

        <Path x:Name="Line2Path" Width="43.5772" Height="45.3813" Canvas.Left="0.20177" Canvas.Top="0.55809" Stretch="Fill" Fill="#4FDE0909" Data="F1 M 3.7719,45.93941 0.20177,42.5115L 40.353,0.55809L 43.7784,2.98867"/>

    </Canvas>
</UserControl>
```

- 6. Add a new class called BooleanToIconConverter.cs.
- 7. Add the following using statement to your class:
    - `using System.Windows.Data;`
- 8. Have the BooleanToIconConverter inherit the IValueConverter interface. In the Convert method, if the value passed in is True, have it return a new instance of the GreenCheck user control. If the value passed in is False, have the Convert method return an instance of the RedX user control.

Here’s the code for the BooleanToIconConverter class:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Data;

namespace BindingSample3
{
    public class BooleanToIconConverter : IValueConverter
    {
        public object Convert(object value, Type targetType,
            object parameter,
            System.Globalization.CultureInfo culture)
        {
            if (value != null)
            {
                bool boolValue = (bool)value;
                if (boolValue)
                    return new GreenCheck();
                else
return new RedX();
}
return value;
}
public object ConvertBack(object value, Type targetType,
object parameter,
System.Globalization.CultureInfo culture)
{
throw new NotImplementedException();
}
}
```

## 9. Add a new class called ServerStatus.cs that has three properties: the Server name, a Boolean indicator if the server is up, and a number of currently connected users.

This will be the data class used in the application. Here is the code for ServerStatus.cs:

```
public class ServerStatus
{
private string _serverName;

public string ServerName
{
get { return _serverName; }
set { _serverName = value; }
}
private bool _isServerUp;

public bool IsServerUp
{
get { return _isServerUp; }
set { _isServerUp = value; }
}
private int _numberOfConnectedUsers;

public int NumberOfConnectedUsers
{
get { return _numberOfConnectedUsers; }
set { _numberOfConnectedUsers = value; }
}
public ServerStatus() { }
}
```

## 10. In MainWindow.xaml.cs, create a GenerateData() method (call it immediately following the InitializeComponent() method in the Window constructor) that will initialize a list of a few ServerStatus objects and make that list the DataContext of the Window.

Here's the code:

```
private void GenerateData()
{
ServerStatus ss = new ServerStatus() {
ServerName = "HeadquartersApplicationServer1",
NumberOfConnectedUsers = 983,
        IsServerUp = true
    };

    ServerStatus ss2 = new ServerStatus()
    {
        ServerName = "HeadquartersFileServer1",
        NumberOfConnectedUsers = 0,
        IsServerUp = false
    };

    ServerStatus ss3 = new ServerStatus()
    {
        ServerName = "HeadquartersWebServer1",
        NumberOfConnectedUsers = 0,
        IsServerUp = false
    };

    ServerStatus ss4 = new ServerStatus()
    {
        ServerName = "HQDomainControllerServer1",
        NumberOfConnectedUsers = 10235,
        IsServerUp = true
    };

    List<ServerStatus> serverList = new List<ServerStatus>();
    serverList.Add(ss);
    serverList.Add(ss2);
    serverList.Add(ss3);
    serverList.Add(ss4);

    this.DataContext = serverList;
}
```

- 11. **Save and build your application.**
    
    You do this step so that the user control classes that you've defined are available to your XAML files.

- 12. **In MainWindow.xaml, replace the XAML with the XAML found in the following code segment.**

```
<Window x:Class="BindingSample.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:BindingSample"
    Title="MainWindow" Height="400" Width="525">
    <Window.Resources>
        <local:BooleanToIconConverter x:Key="BooleanToIconConverter" />

        <DataTemplate x:Key="ServerTemplate">
            <Border BorderBrush="Blue" Margin="3" Padding="3"
                BorderThickness="2" CornerRadius="5" Background="Beige">

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
