
### 7. 为你的 TextBox Style 添加 Style 属性，如下所示：

`Style={StaticResource ResourceKey=errorAwareTextBox}`

现在当你运行应用程序并删除 TextBox 控件中的文本时，TextBox 会显示带有实际错误消息的工具提示。（见图 3-5）。

![](img/6df7bb88e9302e98442acc219cfbd7fc_639_0.png)

**图 3-5：** 使用 Styles 显示错误消息。

## 转换你的数据

WPF 提供了让用户界面对用户来说直观的能力。有时这意味着让他们以符合他们直觉的不同格式输入数据，这让你你负责将他们的数据输入转换为数据源允许的格式。反之亦然；你希望从你的数据源转换成对用户来说更直观的形式。这种类型转换的一个流行用例是数据值的字符串表示，或者当你想要显示红色或绿色圆形而不是 True 或 False 值时。

WPF 通过提供一个名为 `IConverter` 的简单接口使数据转换变得简单。该接口包含两个方法：

- `Convert`：该方法从数据源获取值并将其合并到给用户控件的表单中。
- `ConvertBack`：该方法执行相反的操作——它从用户界面获取值并将其合并到数据源期望的格式中。

注意的是，通过这些方法，你并不受限于与绑定值相同的数据类型。例如，你绑定的数据属性可以是 `Date` 类型，而 `Convert` 方法仍然可以向用户界面返回字符串值。

为了演示此功能，创建一个名为 `BindingSample3` 的新 WPF 项目。该项目是一个仪表板应用程序，可以显示网络上服务器的状态。在这个项目中，你实现了两个用户控件：`RedX` 和 `GreenCheck`。你还创建了一个名为 `BooleanToIconConverter` 的值，它将 `Boolean False` 转换为显示 RedX 控件，将 `True` 值转换为显示 GreenCheck 控件。这些值表示服务器是否可用。

用户控件是可重用 XAML 的集合。它可以由任意数量的元素组成，实现规则与普通 Window 相同（例如，你可以只有一个根元素）。你还可以在用户控件上定义属性。

![](img/6df7bb88e9302e98442acc219cfbd7fc_640_png)

`BindingSample3` 项目可用。

按照以下步骤创建你的示例：

- 1. 创建名为 `BindingSample3` 的新 WPF 应用程序。
- 2. 向项目添加一个新的用户控件；将其命名为 `GreenCheck.xaml`。
- 3. 替换 `GreenCheck.xaml` 中的 XAML：

```xml
<UserControl x:Class="BindingSample.Check"
xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.org/markup-compatibility"
xmlns:mc="http://schemas.microsoft.com/expression/blend/2008"
:IgnIgn="="d"d:Width="50" d:Height="50">
<Canvas x:Name="Canvas" Width="50.4845" Height="49.6377" Canvas.Left="0" Top="0">
  <Path x:Name="CheckPath" Width="43.4167" Height="45.6667" Canvas.Left="0" Top="1.3113" Stretch="Fill" Fill="#FF006D3"
  Data="M 19.0833,45.6667 L 41.4167,26.6667 L 38,31.3113 L 19.0833,48.5283 L 24.2617,25.5333 L 30,27.9267 L 17.4167,44.225"/>
</Canvas>
</UserControl>
```

你不需要凭记忆写出 `CheckPath` 这样的内容（路径描述了如何绘制勾号）。在 Expression Suite 中，设计工具允许你在程序中绘制图形并以 XAML 格式导出最终图形。Expression Design 是此示例中创建用户控件的工具。

![](img/6df7bb88e9302e98442acc219cfbd7fc_640_1.png)

- 4. 向项目添加另一个用户控件；将其命名为 `RedX.xaml`。
- 5. 替换 `RedX.xaml` 文件中的 XAML：

```xml
<UserControl x:Class="BindingSample3.Xaml"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
mc:Ignorable="d"
d:DesignHeight="50" d:DesignWidth="50">
<Canvas Width="45.625" Height="49.6377">
  <Path x:Name="CheckPath" Width="43.4167" Height="45.6667" Canvas.Left="0" Top="1.3113" Stretch="Fill" Fill="#FF006D3"
  Data="M 19.0833,45.6667 L 41.4167,26.6667 L 38,31.3113 L 19.0833,48.5283 L 24.2617,25.5333 L 30,27.9267 L 17.4167,44.225"/>
</Canvas>
</UserControl>
```

- 6. 添加新类 `BooleanToIconConverter.cs`。
- 7. 为你的类添加以下 `using` 语句：
- 8. 让 `BooleanToIconConverter` 继承 `IConverter` 接口。在 `Convert` 方法中，如果值为 `True`，它返回一个新的 `GreenCheck` 控件实例。如果传入的值为 `False`，`Convert` 方法返回一个 `RedX` 控件实例。

以下是 `BooleanToIconConverter` 的代码：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Data;
namespace BindingSample3
{
    public class BooleanToIconConverter : IConverter
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
            return null;
        }
        public object ConvertBack(object value, Type targetType,
            object parameter,
            System.Globalization.CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```

- 9. 添加新类 `ServerStatus.cs`，它包含三个属性：服务器名称、服务器是否运行的布尔指示以及当前连接的用户数。

这将是应用程序使用的数据类。`ServerStatus.cs`：

```csharp
public class ServerStatus
{
    private string _serverName;
    public string ServerName
    {
        get { return _serverName; }
        set { _serverName = value; }
    }
    private bool _isServerUp;
    public bool isServerUp
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

- 10. 在 `MainWindow.xaml` 中，创建一个 `GenerateData()` 方法（在窗口构造函数中 `InitializeComponent()` 方法之后立即调用它），该方法将初始化几个 `ServerStatus` 对象列表，并将列表映射到窗口的 `Data`。

以下是代码：

```csharp
private void GenerateData() {
    ServerStatus ss = new ServerStatus() {
        ServerName = "HeadquartersApplicationServer1",
        NumberOfConnectedUsers = 983;
    };
}
```

# 618 编辑、验证、转换和可视化你的数据

```csharp
IsServerUp = true
);
ServerStatus ss2 = new ServerStatus()
{
    ServerName = "HeadquartersFileServer",
    NumberOfConnectedUsers = 0,
    IsServerUp = false
}
ServerStatus ss3 = new ServerStatus()
{
    ServerName = "HeadquartersWebServer",
    NumberOfConnectedUsers = 0,
    IsServerUp = false
}
ServerStatus ss4 = new ServerStatus()
{
    ServerName = "HQDomainControllerServer",
    NumberOfConnectedUsers = 10235,
    IsServerUp = true
}
List<ServerStatus> serverList = new List<ServerStatus>();
serverList.Add(ss1);
serverList.Add(ss2);
serverList.Add(ss3);
serverList.Add(ss4);
this.DataContext = serverList;
```

# 11. 保存并生成你的应用程序。

执行此步骤是为了使你定义的用户控件类可以在你的 XAML 文件可用。

# 12. 在 MainWindow.xaml 中，将 XAML 替换为以下代码段中的 XAML：

```xml
<Window Class="BindingSample3" MainWindow
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:BindingSample3"
Title="MainWindow" Width="400" Height="525">
<Window.Resources>
    <local:BooleanToIconConverter x:Key="BooleanToIconConverter" />
</Window.Resources>
<DataTemplate x:Key="ServerTemplate">
    <Border BorderBrush="Blue" Margin="3" Padding="3"
            BorderThickness="2" CornerRadius="5" Background="Beige">
        <StackPanel Orientation="Horizontal">
            <Label Content="{Binding Path=IsServerUp, Converter={StaticResource BooleanToIconConverter}}" />
        </StackPanel>
    </Border>
</DataTemplate>
```

# 编辑、验证、转换和可视化你的数据 619

```xml
<StackPanel Orientation="Vertical"
    VerticalAlignment="Center">
    <Block FontSize="25" Foreground="Goldenrod"
        Text="{Binding Path=ServerName}" />
    <Block FontSize="18" Foreground="BlueViolet"
        Text="{Binding Path=NumberOfConnectedUsers}" />
</StackPanel>
<StackPanel>
    <Border />
</StackPanel>
<DataTemplate>
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
            ItemTemplate={StaticResource ServerTemplate} />
    </Grid>
</Window>
```

在 `MainWindow.xaml` 中完成的第一件事是将本地程序集（`BindingSample3`）的命名空间添加到 Window 中（通过 Window 标签中带有 `local` 前缀的命名空间定义来识别）。这允许你在 XAML 中实例化当前程序集中定义的类，例如 `BooleanToConverter`。

```xml
xmlns:local="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:BindingSample3"
Title="MainWindow" Height="400" Width="525">
<Window.Resources>
    <local:BooleanToConverter x:Key="BooleanToConverter" />
</Window>
```

在资源中，初始化你的 `BooleanToConverter` 实例，你可以通过本地命名空间使用它。

```xml
<local:BooleanToConverter x:Key="BooleanToConverter" />
```
