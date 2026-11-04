
网络上的服务器状态。在这个项目中，你将实现两个用户控件：RedX 和 GreenCheck。你还要创建一个名为 BooleanToIconConverter 的值转换器，它将布尔值 False 转换为显示 RedX 控件，将 True 转换为显示 GreenCheck 控件。这些值指示服务器是否可用。

用户控件是可重用 XAML 的集合。它可以由任意数量的元素组成，并且实现规则与实现普通 Window 时相同（例如，只能有一个根元素）。你还可以在用户控件上定义属性（包括依赖属性！）。

![](img/80ff26f06fc9ab951e1cd4257b867366_640_0.png)

该项目可在网上以 BindingSample3 名称获取。

按以下步骤创建你的示例：

- 1. 创建一个名为 BindingSample3 的新 WPF 应用程序。
- 2. 向项目中添加一个新的用户控件；将其命名为 GreenCheck.xaml。
- 3. 将 GreenCheck.xaml 中的 XAML 替换为以下 XAML：

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

你不需要凭空想出类似 CheckPath 这样的东西。（路径是描述对勾如何绘制的。）在 Expression Suite 中，你可以找到设计器工具，它们允许你在图形程序中绘制项目，并以 XAML 格式导出最终图形。Expression Design 就是用于创建本示例中用户控件的工具。

- 4. 向项目中添加另一个用户控件；将其命名为 RedX.xaml。
- 5. 将 RedX.xaml 文件中的 XAML 替换为以下 XAML：

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

- 6. 添加一个名为 BooleanToIconConverter.cs 的新类。
- 7. 向你的类中添加以下 using 语句：
    - `using System.Windows.Data;`
- 8. 让 BooleanToIconConverter 继承 IValueConverter 接口。在 Convert 方法中，如果传入的值是 True，则返回 GreenCheck 用户控件的新实例。如果传入的值是 False，则让 Convert 方法返回 RedX 用户控件的实例。

以下是 BooleanToIconConverter 类的代码：

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

## 9. 添加一个名为 ServerStatus.cs 的新类，该类具有三个属性：服务器名称、一个指示服务器是否启动的布尔值，以及当前连接的用户数。

这将是应用中使用的数据类。以下是 ServerStatus.cs 的代码：

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

## 10. 在 MainWindow.xaml.cs 中，创建一个 GenerateData() 方法（在 Window 构造函数中的 InitializeComponent() 方法之后立即调用它），该方法将初始化一个包含几个 ServerStatus 对象的列表，并将该列表设置为 Window 的 DataContext。

代码如下：

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

- 11. **保存并生成你的应用程序。**
    
    执行此步骤是为了让你已定义的用户控件类可供你的 XAML 文件使用。

- 12. **在 MainWindow.xaml 中，将 XAML 替换为以下代码段中的 XAML。**

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

在 MainWindow.xaml 中，首先要注意的是，本地程序集（BindingSample3）的命名空间已添加到 Window 中（通过 Window 标签中带有 local 前缀的命名空间定义来标识）。这使你可以在 XAML 中实例化当前程序集中定义的类，例如 BooleanToIconConverter。

```
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:BindingSample3"
Title="MainWindow" Height="400" Width="525">
<Window.Resources>
<local:BooleanToIconConverter x:Key="BooleanToIconConverter" />
```

在 Window 资源中，你初始化了一个 BooleanToIconConverter 的实例，该实例可通过 local 命名空间获得。

```
<local:BooleanToIconConverter x:Key="BooleanToIconConverter" />
```

定义的另一个 Window 资源是一个数据模板。该数据模板提供了一种查看与服务器当前状态相关数据的方式。数据模板定义如下：

```
<DataTemplate x:Key="ServerTemplate">
<Border BorderBrush="Blue" Margin="3" Padding="3"
BorderThickness="2" CornerRadius="5" Background="Beige">
```
