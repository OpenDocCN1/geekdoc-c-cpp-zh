

# ServiceControllerInfo 类

ServiceControllerInfo 类还有一些其他属性用于启用启动、停止、暂停和继续按钮：`EnableStart`、`EnablePause` 和 `EnableContinue`。这些属性根据服务的当前状态返回布尔值（代码文件 `ServiceControlWPF/ServiceControllerInfo.cs`）：

```csharp
public class ServiceControllerInfo
{
  // etc.
  public bool EnableStart => Controller.Status == ServiceControllerStatus.Stopped;
  // etc.
}

public bool EnableStop => Controller.Status == ServiceControllerStatus.Running;

public bool EnablePause =>
    Controller.Status == ServiceControllerStatus.Running &&
    Controller.CanPauseAndContinue;

public bool EnableContinue => Controller.Status ==
    ServiceControllerStatus.Paused;
}
```

# ServiceControlWindow 类

在 `ServiceControlWindow` 类中，方法 `RefreshServiceList` 使用 `ServiceController.GetServices` 获取所有服务以在列表框中显示。`GetServices` 方法返回 `ServiceController` 实例的数组，表示操作系统上安装的所有 Windows 服务。`ServiceController` 类还具有静态方法 `GetDevices`，它返回表示所有设备驱动程序的 `ServiceController` 数组。返回的数组借助扩展方法 `OrderBy` 进行排序。排序依据是 `DisplayName`，如传递给 `OrderBy` 方法的 lambda 表达式所定义。使用 `Select`，将 `ServiceController` 实例转换为 `ServiceControllerInfo` 类型。在以下代码中，传递了一个 lambda 表达式，该表达式为每个 `ServiceController` 对象调用 `ServiceControllerInfo` 构造函数。最后，结果被分配给窗口的 `DataContext` 属性以进行数据绑定（代码文件 `ServiceControlWPF/MainWindow.xaml.cs`）：

```csharp
protected void RefreshServiceList()
{
    this.DataContext = ServiceController.GetServices().
        OrderBy(sc => sc.DisplayName).
        Select(sc => new ServiceControllerInfo(sc));
}
```

方法 `RefreshServiceList` 用于在列表框中获取所有服务，在 `ServiceControlWindow` 类的构造函数中调用。构造函数还定义了按钮的 `Click` 事件处理程序：

```csharp
public ServiceControlWindow()
{
    InitializeComponent();
    RefreshServiceList();
}
```

现在，你可以定义 XAML 代码以将信息绑定到控件。首先，为 `ListBox` 中显示的信息定义一个 `DataTemplate`。`ListBox` 包含一个 `Label`，其 `Content` 绑定到数据源的 `DisplayName` 属性。由于你绑定的是 `ServiceControllerInfo` 对象数组，`DisplayName` 属性是在 `ServiceControllerInfo` 类中定义的（代码文件 `ServiceControlWPF/MainWindow.xaml`）：

```xml
<Window.Resources>
    <DataTemplate x:Key="listTemplate">
        <Label Content="{Binding DisplayName}"/>
    </DataTemplate>
</Window.Resources>
```

位于窗口左侧的 `ListBox` 将 `ItemsSource` 属性设置为 `{Binding}`。这样，列表中显示的数据将从 `RefreshServiceList` 方法中设置的 `DataContext` 属性接收。`ItemTemplate` 属性引用了前面用 `DataTemplate` 定义的资源 `listTemplate`。`IsSynchronizedWithCurrentItem` 属性被设置为 `True`，因此同一窗口内的 `TextBox` 和 `Button` 控件绑定到 `ListBox` 当前选中的项：

```xml
<ListBox Grid.Row="0" Grid.Column="0" HorizontalAlignment="Left" Name="listBoxServices" VerticalAlignment="Top" ItemsSource="{Binding}" ItemTemplate="{StaticResource listTemplate}" IsSynchronizedWithCurrentItem="True">
</ListBox>
```

为了区分用于启动/停止/暂停/继续服务的 `Button` 控件，定义了以下枚举（代码文件 `ServiceControlWPF/ButtonState.cs`）：

```csharp
public enum ButtonState
{
    Start,
    Stop,
    Pause,
    Continue
}
```

对于 `TextBlock` 控件，`Text` 属性绑定到 `ServiceControllerInfo` 实例的相应属性。`Button` 控件的启用或禁用状态也由数据绑定决定，即把 `IsEnabled` 属性绑定到 `ServiceControllerInfo` 实例中返回布尔值的相应属性。按钮的 `Tag` 属性被赋值为先前定义的 `ButtonState` 枚举值，以便在同一个处理程序方法 `OnServiceCommand` 中区分按钮（代码文件 `ServiceControlWPF/MainWindow.xaml`）：

```xml
<TextBlock Grid.Row="0" Grid.ColumnSpan="2" Text="{Binding /DisplayName, Mode=OneTime}" />
<TextBlock Grid.Row="1" Grid.ColumnSpan="2" Text="{Binding /ServiceStatusName, Mode=OneTime}" />
<TextBlock Grid.Row="2" Grid.ColumnSpan="2" Text="{Binding /ServiceTypeName, Mode=OneTime}" />
<TextBlock Grid.Row="3" Grid.ColumnSpan="2" Text="{Binding /ServiceName, Mode=OneTime}" />
<Button Grid.Row="4" Grid.Column="0" Content="Start" IsEnabled="{Binding /EnableStart, Mode=OneTime}" Tag="{x:Static local:ButtonState.Start}" Click="OnServiceCommand" />
<Button Grid.Row="4" Grid.Column="1" Name="buttonStop" Content="Stop" IsEnabled="{Binding /EnableStop, Mode=OneTime}" Tag="{x:Static local:ButtonState.Stop}" Click="OnServiceCommand" />
<Button Grid.Row="5" Grid.Column="0" Name="buttonPause"
        Content="Pause"
        IsEnabled="{Binding /EnablePause, Mode=OneTime}"
        Tag="{x:Static local:ButtonState.Pause}"
        Click="OnServiceCommand" />
<Button Grid.Row="5" Grid.Column="1" Name="buttonContinue"
        Content="Continue"
        IsEnabled="{Binding /EnableContinue, Mode=OneTime}"
        Tag="{x:Static local:ButtonState.Continue}"
        Click="OnServiceCommand" />
<Button Grid.Row="6" Grid.Column="0" Name="buttonRefresh"
        Content="Refresh"
        Click="OnRefresh" />
<Button Grid.Row="6" Grid.Column="1" Name="buttonExit"
        Content="Exit" Click="OnExit" />
```

## 控制服务

使用 `ServiceController` 类，您还可以向服务发送控制请求。下表描述了可以应用的方法。

| 方法 | 描述 |
|--------|-------------|
| `Start` | 告知 SCM 应启动服务。在示例服务程序中，将调用 `OnStart`。 |
| `Stop` | 如果服务类中的属性 `CanStop` 为 true，则在 SCM 的帮助下调用示例服务程序中的 `OnStop`。 |
| `Pause` | 如果属性 `CanPauseAndContinue` 为 true，则调用 `OnPause`。 |
| `Continue` | 如果属性 `CanPauseAndContinue` 为 true，则调用 `OnContinue`。 |
| `ExecuteCommand` | 允许向服务发送自定义命令。 |

以下代码控制服务。由于启动、停止、挂起和暂停的代码类似，四个按钮只使用一个处理程序（代码文件 `ServiceControllerWPF/MainWindow.xaml.cs`）：

```csharp
protected void OnServiceCommand(object sender, RoutedEventArgs e)
{
    Cursor oldCursor = this.Cursor;
    try
    {
        this.Cursor = Cursors.Wait;
        ButtonState currentButtonState = (ButtonState)(sender as Button).Tag;
        var si = listBoxServices.SelectedItem as ServiceControllerInfo;
        if (currentButtonState == ButtonState.Start)
        {
            si.Controller.Start();
        }
        si.Controller.WaitForStatus(ServiceControllerStatus.Running, TimeSpan.FromSeconds(10));
    }
}
```

# 两种旋流喷嘴的比较研究

带有切向入口的旋流喷嘴比带有导流叶片的普通旋流喷嘴具有更高的流量系数和更稳定的流场。

| 类型 | 流量系数 | 流场稳定性 |
| --- | --- | --- |
| 切向入口 | 更高 | 更稳定 |
| 导流叶片 | 较低 | 稳定性较差 |

实验结果表明，带有切向入口的旋流喷嘴比带有导流叶片的普通旋流喷嘴具有更高的流量系数和更稳定的流场。

旋流喷嘴是一种燃油喷嘴，广泛应用于航空航天发动机。

本文比较了两种旋流喷嘴：一种带有切向入口，另一种带有导流叶片。

对流量系数和流场稳定性进行了测量和分析。

> 带有切向入口的旋流喷嘴具有更高的流量系数和更稳定的流场。

实验结果表明，带有切向入口的旋流喷嘴比带有导流叶片的普通旋流喷嘴具有更高的流量系数和更稳定的流场。

旋流喷嘴是一种燃油喷嘴，广泛应用于航空航天发动机。

![](img/3d365b72b289213a91ade7eb366b8f35_1517_0.png)

将以下内容添加到项目中（应用程序清单文件 `ServiceControlWPF/app.manifest`）：

```xml
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly manifestVersion="1.0"
    xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
    xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
```

