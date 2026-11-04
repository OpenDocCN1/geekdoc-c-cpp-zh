

- **Convert：** 此方法从数据源获取值，并将它们转换为在屏幕上显示给用户的形式。
- **ConvertBack：** 此方法的作用相反 — 它从用户界面获取值，并将其转换为数据源所期望的形式。

需要注意的是，使用这些方法时，你不必受限于所绑定值的数据类型。例如，数据源中绑定的属性可以是 Date 数据类型，而 Convert 方法仍然可以向用户界面返回字符串值。

为了演示此功能，创建一个名为 BindingSample3 的新 WPF 应用程序项目。该项目是一个仪表板应用程序，可以显示网络中服务器的状态。在此项目中，你实现两个用户控件：RedX 和 GreenCheck。你还要创建一个名为 BooleanToIconConverter 的值转换器，它可将布尔值 False 转换为显示 RedX 控件，将 True 转换为显示 GreenCheck 控件。这些值指示服务器是否可用。

用户控件是可复用 XAML 的集合。它可以由任意数量的元素组成，并且实现规则与实现普通 Window 时相同（例如，只能有一个根元素）。你还可以在用户控件上定义属性（包括依赖属性！）。

该项目可在 Web 上以 BindingSample3 名称获取。

## 按照以下步骤创建示例：

- 1. 创建一个名为 BindingSample3 的新 WPF 应用程序。
- 2. 向项目中添加一个新的用户控件，并将其命名为 GreenCheck.xaml。
- 3. 用以下 XAML 替换 GreenCheck.xaml 中的 XAML：

```xml
<UserControl x:Class="BindingSample3.GreenCheck"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d" d:DesignWidth="50" d:DesignHeight="50">

    <Canvas x:Name="CheckCanvas" Width="50.4845" Height="49.6377" Canvas.Left="0" Canvas.Top="0">
        <Path x:Name="CheckPath" Width="43.4167" Height="45.6667" Canvas.Left="0" Canvas.Top="1.311e-006" Stretch="Fill" Fill="#FF00642" Data="M 19 0.0833,45.6667 43 41.667 2.16667L 38, 1.311e-006 0 19.0833,42.5833L 2.41667,25.333L 0, 27.9167L 17.4167,44.25"/>
    </Canvas>
</UserControl>
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_619_0.png)

你不必指望自己能够凭空想出 CheckPath 这样的东西。（路径描述了对勾的绘制方式。）在 Expression Suite 中，你可以找到设计器工具，这些工具允许你在图形程序中绘制项目，并以 XAML 格式导出最终图形。本例中的用户控件就是使用 Expression Design 创建的。

- 4. 向项目中添加另一个用户控件，并将其命名为 RedX.xaml。
- 5. 用以下 XAML 替换 RedX.xaml 文件中的 XAML：

```xml
<UserControl x:Class="BindingSample3.RedX"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    mc:Ignorable="d"
    d:DesignHeight="50" d:DesignWidth="50">

    <Canvas Width="44.625" Height="45.9394">

        <Path x:Name="Line1Path" Width="44.625" Height="44.375"
              Canvas.Left="0" Canvas.Top="0" Stretch="Fill"
              Fill="#FFD0D09" Data="F1 M 0.3,5L 3.5,0L 44.625,41.42L 42.125,44.375"/>

        <Path x:Name="Line2Path" Width="43.5772" Height="45.3813"
              Canvas.Left="0.20177" Canvas.Top="0.55809"
              Stretch="Fill"
              Fill="#FFD0D09" Data="F1 M 3.7719,45.9394L 0.20177,42.5115L 40.353,0.55809L 43.7784,2.98667"/>

    </Canvas>
</UserControl>
```

- 6. 添加一个名为 BooleanToIconConverter.cs 的新类。
- 7. 将以下 using 语句添加到你的类中：

```csharp
using System.Windows.Data;
```

- 8. 让 BooleanToIconConverter 继承 IValueConverter 接口。在 Convert 方法中，如果传入的值为 True，则返回 GreenCheck 用户控件的新实例。如果传入的值为 False，则让 Convert 方法返回 RedX 用户控件的实例。以下是 BooleanToIconConverter 类的代码：

```csharp
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
```

```csharp
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

- 9. 添加一个名为 `ServerStatus.cs` 的新类，该类具有三个属性：服务器名称、指示服务器是否在线的布尔值，以及当前连接的用户数。这将是应用程序中使用的数据类。以下是 `ServerStatus.cs` 的代码：

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

- 10. 在 `MainWindow.xaml.cs` 中，创建一个 `GenerateData()` 方法（在 `Window` 构造函数中的 `InitializeComponent()` 方法之后立即调用它），该方法将初始化一个包含几个 `ServerStatus` 对象的列表，并将该列表设置为窗口的 DataContext。代码如下：

```csharp
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

- 11. 保存并生成你的应用程序 — 这样做是为了使已定义的用户控件类可用于你的 XAML 文件。
- 12. 在 MainWindow.xaml 中，用以下代码段中的 XAML 替换现有 XAML。稍后我会介绍此标记的详细信息。

```xml
<Window x:Class="BindingSample3.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="clr-namespace:BindingSample3"
Title="MainWindow" Height="400" Width="525">
<Window.Resources>
<local:BooleanToIconConverter x:Key="BooleanToIconConverter" />

<DataTemplate x:Key="ServerTemplate">
<Border BorderBrush="Blue" Margin="3" Padding="3"
BorderThickness="2" CornerRadius="5"
Background="Beige">
```

