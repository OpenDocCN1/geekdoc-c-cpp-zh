

## 594 编辑、验证、转换和可视化你的数据

你不需要凭空想出 CheckPath 的内容。（路径描述了如何绘制勾选标记。）在 Expression Suite（表达式套件）中，你可以找到一些设计工具，这些工具允许你在图形程序中绘制项目，并以 XML 格式导出你的最终图形。Expression Design 是此示例中用于创建用户控件的工具。

- 4. 向项目中添加另一个用户；命名为 RedX.xaml。

- 5. 将 RedX 文件中的 XAML 替换为以下 XAML：

```xml
<Control x:Class="BindingSample3.Redx"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:mc xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
mc:Ignorable="d"
d:Height="50" d:Width="50">

<Canvas Width="44.65" Height="44.65" 44.375">
<Path Name="Line1" Width="44.65" Height="44.375"
Canvas.Left="0" Canvas.Top="0" Stroke="F1"
Fill="#FEDE009"
Data="M 0.3,5.1 3.5,0 L 44.625,42.1 L 44.375/" />
<Path Name="Line2" Width="43.5772" Height="45.3813"
Canvas.Left="0.201177" Canvas.Top="0.55809"
Fill="#FEDE009" Data="M 3.7719,45.9394 L0.201177,42.5115 L 0.3,0.55809 L 43.7784,2.98867/"/>
</Canvas>
</Control>
```

- 6. 添加一个新类 BooleanToIconConverter.cs。

- 7. 在你的类中添加以下语句：

```csharp
using System.Windows.Data;
```

- 8. 让 BooleanToIconConverter 继承 IValueConverter 接口。在 Convert 方法中，如果传递的值为 True，则让它返回一个 GreenCheck 用户控件的新实例。如果传递的值为 False，则 Convert 方法返回一个 RedX 用户控件的实例。以下是 BooleanToIconConverter 类的代码：

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
        object parameter,
        System.Globalization.CultureInfo culture)
        {
          if (value != null) {
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

 9.. **一个名为 ServerStatus 的新类，具有三个属性：服务器名称、服务器是否开启的指示器以及连接的用户数。这些将在应用程序中使用。以下是 ServerStatus 的代码：**

```csharp
public class ServerStatus {
  private string _serverName;

  public string ServerName {
    return _serverName; }
    set { _serverName = value; }
  }

  private bool _isUp;

  public bool IsServerUp {
    return _isUp; }
    set { _isUp = value; }
  }

  private int _numberOfUsers;

  public int NumberOfUsers {
    return _numberOfUsers; }
    set { _numberOfUsers = value; }
  }

  public ServerStatus() { }
}
```

- 10. **在 MainWindow.cs 中，创建一个 GenerateData() 方法（跟在 Window 构造函数中的 InitializeComponent() 之后），它将初始化一个 ServerStatus 对象列表并将列表设置为 Window 的 DataContext。以下是其代码：**

```csharp
private void GenerateData()
{
    ServerStatus ss = new ServerStatus();
    ss.ServerName = "HeadquartersApplication1";
    ss.NumberOfUsers = 983;
    ss.IsServerUp = true;

    ServerStatus ss2 = new ServerStatus();
    ss2.ServerName = "HeadquartersFiles1";
    ss2.NumberOfUsers = 0;
    ss2.IsServerUp = false;

    ServerStatus ss3 = new ServerStatus();
    ss3.ServerName = "HeadquartersWebServer1";
    ss3.NumberOfUsers = 0;
    ss3.IsServerUp = false;

    ServerStatus ss4 = new ServerStatus();
    ss4.ServerName = "DomainController1";
    ss4.NumberOfUsers = 12;
    ss4.IsServerUp = true;

    List<ServerStatus> list = new List<ServerStatus>();
    list.Add(ss);
    list.Add(ss2);
    list.Add(ss3);
    list.Add(ss4);

    this.DataContext = list;
}
```

- 11. 保存并生成你的应用程序。

- 12. 在 MainWindow.xaml 中，将 XAML 替换为以下代码以显示数据：

```xml
<Window x:Class="BindingSample3.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:local="clr-namespace:BindingSample3"
        mc:Ignorable="d"
        d:Height="450" d:Width="800" Title="MainWindow">
    <Grid>
        <ListBox x:Name="listServers">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <Border BorderBrush="#FEDE00" Margin="5" Padding="5" CornerRadius="5">
                        <StackPanel Orientation="Horizontal">
                            <Label Content="{Binding IsServerUp, Converter={StaticResource BooleanToIconConverter}}" />
                            <StackPanel Orientation="Vertical">
                                <TextBlock Text="{Binding ServerName}" FontWeight="Bold" FontSize="16"/>
                                <TextBlock Text="{Binding NumberOfUsers, StringFormat='Users: {0}'}" />
                            </StackPanel>
                        </StackPanel>
                    </Border>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
    </Grid>
    <Window.Resources>
        <local:BooleanToIconConverter x:Key="BooleanToIconConverter" />
    </Window.Resources>
</Window>
```

