

与桌面应用程序的生命周期不同。

## 应用生命周期

Windows 8 为应用引入了一种全新的生命周期，它与桌面应用程序的生命周期完全不同。这种情况在 Windows 8.1 中略有改变，在 Windows 10 中又一次改变。如果你使用的是 Windows 10 且处于 *平板模式*，应用的生命周期与 *桌面模式* 下是不同的。在平板模式下，应用通常为全屏显示。你可以通过断开键盘连接来自动切换到平板模式（对于 Microsoft Surface 等平板设备），也可以使用操作中心里的“平板模式”按钮进行切换。当你在平板模式下运行一个应用时，如果应用转到后台（用户切换到另一个应用），它会被挂起，并且不再占用任何 CPU 资源。这样应用就不会消耗任何电量。应用在后台时只使用内存，一旦用户切换回这个应用，它就会重新被激活。

如果内存资源不足，Windows 可以终止已挂起的应用。终止应用时，进程会被直接结束。不会有任何信息发送给应用，因此应用无法对这个事件做出响应。这就是为什么应用应该在收到挂起事件时采取行动，并在此时保存其状态。等到被终止时再保存状态就太迟了。

当收到挂起事件时，应用应将其状态存储到磁盘上。如果应用再次启动，它可以向用户呈现得好像从未被终止过一样。你只需要存储有关页面堆栈的信息，以便将用户导航到他/她上次离开的页面；通过恢复页面返回堆栈允许用户返回；并用用户输入的数据初始化字段。

本节示例应用——`ApplicationLifetimeSample`——做的正是这件事。通过这个应用，多个页面之间可以进行导航，并且可以输入状态。当应用被挂起时，页面堆栈和状态都会被保存；当应用启动时，两者都会被恢复。

## 应用程序执行状态

应用程序的状态通过 ApplicationExecutionState 枚举来定义。该枚举定义了 NotRunning、Running、Suspended、Terminated 和 ClosedByUser 这些状态。应用需要感知并存储其状态，因为返回应用的用户期望从他们上次离开的地方继续。

通过 App 类中的 OnLaunched 方法，你可以使用 LaunchActivatedEventArgs 参数的 PreviousExecutionState 属性获取应用程序之前的执行状态。如果应用程序是在安装后首次启动，或在重启后启动，或是用户从任务管理器中结束了进程后启动，那么以前的执行状态就是 NotRunning。如果用户在应用已经运行时通过另一个磁贴激活它，或者它通过某个激活契约被激活，那么应用就处于 Running 状态。当应用程序之前被挂起时，PreviousExecutionState 属性返回 Suspended。通常情况下，在这种情况下不需要做任何特殊处理，因为状态仍保留在内存中。在挂起状态下，应用不消耗任何 CPU 周期，也不访问磁盘。

> 注意：应用程序可以实现一个或多个激活契约，然后可以通过其中一个契约被激活。这类契约的一个例子是共享。通过这个契约，用户可以从另一个应用共享一些数据，并通过将 UWP 应用作为共享目标来启动它。本章后面的“共享数据”一节会介绍如何实现共享契约。

## 页面之间的导航

用于演示 Windows 应用生命周期的示例应用（`ApplicationLifetimeSample`）是基于空白应用模板创建的。创建项目后，你添加 Page1 和 Page2 页面来实现页面之间的导航。

在 `MainPage` 中，添加两个 `Button` 控件用于导航到 Page1 和 Page2，并添加两个 `TextBox` 控件以允许通过导航传递数据（代码文件 `ApplicationLifetimeSample/MainPage.xaml`）：

```
<Button Content="Page 1" Click="{x:Bind GotoPage1}" Grid.Row="0" />
<TextBox Text="{x:Bind Parameter1, Mode=TwoWay}" Grid.Row="0" Grid.Column="1" />
<Button Content="Page 2" Click="{x:Bind GotoPage2}" Grid.Row="1" />
<TextBox Text="{x:Bind Parameter2, Mode=TwoWay}" Grid.Row="1" Grid.Column="1" />
```

代码隐藏文件包含导航到 Page1 和 Page2 的事件处理程序以及用于参数的属性（代码文件 `ApplicationLifetimeSample/MainPage.xaml.cs`）：

```
public void GotoPage1()
{
    Frame.Navigate(typeof(Page1), Parameter1);
}

public string Parameter1 { get; set; }

public void GotoPage2()
{
    Frame.Navigate(typeof(Page2), Parameter2);
}

public string Parameter2 { get; set; }
```

Page1 的 UI 元素显示了导航到该页面时接收到的数据、一个允许用户导航到 Page2 的 Button，以及一个允许用户输入一些应在应用终止时保存的状态信息的 TextBox（代码文件 ApplicationLifetimeSample/Page1.xaml）：

```
<TextBlock FontSize="30" Text="Page 1" />
<TextBlock Grid.Row="1" Text="{x:Bind ReceivedContent, Mode=OneTime}" />
<TextBox Grid.Row="2" Text="{x:Bind Parameter1, Mode=TwoWay}" />
<Button Grid.Row="3" Content="Navigate to Page 2" Click="{x:Bind GotoPage2, Mode=OneTime}" />
```

与 MainPage 类似，Page1 的导航代码为通过导航传递的数据定义了一个自动实现的属性，并实现了一个用于导航到 Page2 的事件处理程序（代码文件 ApplicationLifetimeSample/Page1.xaml.cs）：

```
public void GotoPage2()
{
    Frame.Navigate(typeof(Page2), Parameter1);
}

public string Parameter1 { get; set; }
```

在代码隐藏文件中，导航参数在 OnNavigatedTo 方法的重写中接收。接收到的参数被赋值给自动实现的属性 ReceivedContent（代码文件 ApplicationLifetimeSample/Page1.xaml.cs）：

```
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    base.OnNavigatedTo(e);
    //...
    ReceivedContent = e.Parameter?.ToString() ?? string.Empty;
    Bindings.Update();
}

public string ReceivedContent { get; private set; }
```

在导航实现方面，Page2 与 Page1 非常相似，因此这里不再重复其实现。

使用系统后退按钮将在第 32 章“Windows 应用：用户界面”中介绍。在这里，后退按钮的可见性和处理程序在 BackButtonManager 类中定义。如果 Frame 实例的 CanGoBack 属性返回 true，构造函数实现会使后退按钮可见。OnBackRequested 方法用于在页面堆栈可用时返回上一页（代码文件 ApplicationLifetimeSample/Utilities/BackButtonManager.cs）：

```
public class BackButtonManager: IDisposable
{
    private SystemNavigationManager _navigationManager;
    private Frame _frame;

    public BackButtonManager(Frame frame)
    {
        _frame = frame;
        _navigationManager =
SystemNavigationManager.GetForCurrentView();
        _navigationManager.AppViewBackButtonVisibility =
frame.CanGoBack ?
    AppViewBackButtonVisibility.Visible:
    AppViewBackButtonVisibility.Collapsed;
        _navigationManager.BackRequested += OnBackRequested;
    }

    private void OnBackRequested(object sender,
BackRequestedEventArgs e)
    {
        if (_frame.CanGoBack) _frame.GoBack();
        e.Handled = true;
    }

    public void Dispose()
    {
        _navigationManager.BackRequested -= OnBackRequested;
    }
}
```

在所有页面中，都在 OnNavigatedTo 方法中通过传递 Frame 来实例化 BackButtonManager，并在 OnNavigatedFrom 方法中将其释放（代码文件 ApplicationLifetimeSample/MainPage.xaml.cs）：

```
private BackButtonManager _backButtonManager;
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    base.OnNavigatedTo(e);
    _backButtonManager = new BackButtonManager(Frame);
}

protected override void
OnNavigatingFrom(NavigatingCancelEventArgs e)
{
    base.OnNavigatingFrom(e);
    _backButtonManager.Dispose();
}
```

有了所有这些代码，用户就可以在三个不同页面之间来回导航。接下来需要做的是记住页面和页面堆栈，以便将应用导航到用户最近访问过的页面。

## 导航状态

为了存储和加载导航状态，NavigationSuspensionManager 类定义了 SetNavigationStateAsync 和 GetNavigationStateAsync 方法。导航的页面堆栈可以用一个字符串表示。这个字符串被写入一个本地缓存文件，文件名由常量定义。如果该文件在之前的应用运行中已经存在，则会被直接覆盖。你不需要记住多次应用运行之间的页面导航（代码文件 ApplicationLifetimeSample/Utilities/NavigationSuspensionManager。

