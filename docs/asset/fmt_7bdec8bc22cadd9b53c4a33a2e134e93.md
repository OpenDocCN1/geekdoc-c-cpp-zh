
与 `MainPage` 类似，`Page1` 的导航代码为通过导航传递的数据定义了一个自动实现的属性，并实现了一个用于导航到 `Page2` 的事件处理程序（代码文件 `ApplicationLifetimeSample/Page1.xaml.cs`）：

```
public void GotoPage2()
{
    Frame.Navigate(typeof(Page2), Parameter1);
}

public string Parameter1 { get; set; }
```

在代码隐藏文件中，导航参数在 `OnNavigatedTo()` 方法的重写中接收。接收到的参数被赋值给自动实现的属性 `ReceivedContent`（代码文件 `ApplicationLifetimeSample/Page1.xaml.cs`）：

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

在导航实现方面，`Page2` 与 `Page1` 非常相似，因此这里不再重复其实现。

使用系统后退按钮将在第 32 章“Windows 应用：用户界面”中介绍。在这里，后退按钮的可见性和处理程序在 `BackButtonManager` 类中定义。如果 `Frame` 实例的 `CanGoBack` 属性返回 `true`，构造函数实现会使后退按钮可见。`OnBackRequested()` 方法用于在页面堆栈可用时返回上一页（代码文件 `ApplicationLifetimeSample/Utilities/BackButtonManager.cs`）：

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

在所有页面中，都在 `OnNavigatedTo()` 方法中通过传递 `Frame` 来实例化 `BackButtonManager`，并在 `OnNavigatedFrom()` 方法中将其释放（代码文件 `ApplicationLifetimeSample/MainPage.xaml.cs`）：

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

为了存储和加载导航状态，`NavigationSuspensionManager` 类定义了 `SetNavigationStateAsync()` 和 `GetNavigationStateAsync()` 方法。导航的页面堆栈可以用一个字符串表示。这个字符串被写入一个本地缓存文件，文件名由常量定义。如果该文件在之前的应用运行中已经存在，则会被直接覆盖。你不需要记住多次应用运行之间的页面导航（代码文件 `ApplicationLifetimeSample/Utilities/NavigationSuspensionManager.cs`）：

```csharp
public class NavigationSuspensionManager
{
	private const string NavigationStateFile = "NavigationState.txt";

	public async Task SetNavigationStateAsync(string navigationState)
	{
		StorageFile file = await
		ApplicationData.Current.LocalCacheFolder.CreateFileAsync(
		NavigationStateFile,
		CreationCollisionOption.ReplaceExisting);
		Stream stream = await file.OpenStreamForWriteAsync();
		using (var writer = new StreamWriter(stream))
		{
			await writer.WriteLineAsync(navigationState);
		}
	}
	public async Task<string> GetNavigationStateAsync()
	{
		Stream stream = await
		ApplicationData.Current.LocalCacheFolder.OpenStreamForReadAsync(
		NavigationStateFile);
		using (var reader = new StreamReader(stream))
		{
			return await reader.ReadLineAsync();
		}
	}
}
```

> 注意：`NavigationSuspensionManager` 类利用 Windows 运行时 API 与 .NET `Stream` 类来读写文件内容。这两个特性将在第23章“文件和流”中详细说明。

## 挂起应用

为了在应用程序挂起时保存状态，`App` 类的 `Suspending` 事件在 `OnSuspending()` 事件处理程序中进行设置。当应用程序进入挂起模式时，该事件被触发（代码文件 `ApplicationLifetimeSample/App.xaml.cs`）：

```csharp
public App()
{
	this.InitializeComponent();
	this.Suspending += OnSuspending;
}
```

`OnSuspending()` 方法是一个事件处理程序方法，因此被声明为返回 `void`。这里有一个问题。一旦该方法执行完毕，应用程序就可能被终止。然而，由于该方法被声明为 `void`，无法等待该方法完成。为此，收到的 `SuspendingEventArgs` 参数定义了一个 `SuspendingDeferral`，可以通过调用 `GetDeferral()` 方法获取。一旦代码中的异步功能完成，你需要调用延迟对象的 `Complete()` 方法。这样，调用方就知道方法已完成，应用程序可以被终止（代码文件 `ApplicationLifetimeSample/App.xaml.cs`）：

```csharp
private async void OnSuspending(object sender,
SuspendingEventArgs e)
{
    var deferral = e.SuspendingOperation.GetDeferral();

    //...

    deferral.Complete();
}
```

> 注意：你可以在第15章“异步编程”中阅读有关异步方法的详细信息。

在 `OnSuspending()` 方法的实现中，页面堆栈被写入临时缓存。你可以使用 `Frame` 的 `BackStack` 属性检索页面堆栈上的页面。该属性返回一个 `PageStackEntry` 对象列表，其中每个实例表示类型、导航参数和导航转换信息。为了使用 `SetNavigationStateAsync()` 方法存储页面轨迹，只需要一个包含完整页面堆栈信息的字符串。可以通过调用 `Frame` 的 `GetNavigationState()` 方法获取该字符串（代码文件 `ApplicationLifetimeSample/App.xaml.cs`）：

```csharp
private async void OnSuspending(object sender,
SuspendingEventArgs e)
{
    var deferral = e.SuspendingOperation.GetDeferral();

    var frame = Window.Current.Content as Frame;
    if (frame?.BackStackDepth >= 1)
    {
        var suspensionManager = new NavigationSuspensionManager();
        string navigationState = frame.GetNavigationState();
        if (navigationState != null)
        {
            await
suspensionManager.SetNavigationStateAsync(navigationState);
        }
    }

    //...

    deferral.Complete();
}
```

在 Windows 8 中，在应用程序可能被终止之前，你只有几秒钟的时间来挂起应用程序。在 Windows 10 中，你可以延长这段时间，用于进行网络调用、从服务检索数据、向服务上传数据或进行位置跟踪。为此，你只需在 `OnSuspending()` 方法中创建一个 `ExtendedExecutionSession`，设置一个原因（如 `ExtendedExecutionReason.SavingData`），并通过调用 `RequestExecutionAsync()` 请求延长。只要扩展执行未被拒绝，你就可以继续执行扩展任务。

## 从挂起状态激活应用

`GetNavigationState()` 返回的字符串以逗号分隔，列出页面堆栈的完整信息，包括类型信息和参数。你不应该解析该字符串来获取不同部分，因为这可能会随着 Windows 运行时的新实现而改变。直接使用该字符串在以后通过 `SetNavigationState()` 恢复页面堆栈是可以的。如果字符串格式在未来版本中发生变化，这两个方法也会随之改变。

要在应用程序启动时设置页面堆栈，你需要修改 `OnLaunched()` 方法。此方法是从 `Application` 基类重写的，并在应用程序启动时被调用。参数 `LaunchActivatedEventArgs` 提供了应用程序如何启动的信息。`Kind` 属性返回一个 `ActivationKind` 枚举值，你可以从中读取应用程序是由用户点击磁贴（发出语音命令）启动的，还是由 Windows 启动的（例如作为共享目标启动）。`PreviousExecutionState`（此场景中需要）返回一个 `ApplicationExecutionState` 枚举值，提供应用程序之前如何结束的信息。如果应用程序以 `ClosedByUser` 值结束，则无需特殊操作；应用程序应全新启动。但是，如果应用程序先前被终止，则 `PreviousExecutionState` 包含值 `Terminated`。有了此状态，将应用程序安排到用户之前离开的状态是有用的。在这里，页面堆栈从 `NavigationSuspensionManager` 中检索，并通过将先前保存的字符串传递给 `SetNavigationState()` 方法设置到根框架（代码文件 `ApplicationLifetimeSample/App.xaml.cs`）：

```csharp
protected override async void
OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;

    if (rootFrame == null)
    {
        rootFrame = new Frame();

        rootFrame.NavigationFailed += OnNavigationFailed;

        if (e.PreviousExecutionState ==
ApplicationExecutionState.Terminated)
        {
            var suspensionManager = new NavigationSuspensionManager();
            string navigationState =
                await suspensionManager.GetNavigationStateAsync();
            rootFrame.SetNavigationState(navigationState);

            // etc.
        }
    }
```

```
// Place the frame in the current Window
Window.Current.Content = rootFrame;
}

if (rootFrame.Content == null)
{
    rootFrame.Navigate(typeof(MainPage), e.Arguments);
}
Window.Current.Activate();
}
```

## 测试挂起

现在你可以启动应用程序（见图33.1），导航到另一个页面，然后打开其他应用程序，等待应用程序被终止。使用任务管理器，如果将“状态值”选项设置为“显示挂起状态”，你可以在“详细信息”视图中看到挂起的应用程序。然而，这不是一种简单的测试挂起的方法（因为可能需要很长时间才会发生终止），而且能够调试不同状态会更好。

![](img/3d365b72b289213a91ade7eb366b8f35_1248_0.png)

图33.1

使用调试器时，一切工作方式都不同。如果应用程序在失去焦点时立即被挂起，那么每次到达断点时它都会被挂起。这就是为什么在调试器下运行时挂起被禁用的原因。所以正常的挂起机制不适用。然而，模拟起来很容易。如果打开“调试位置”工具栏，会有三个按钮：挂起、恢复、挂起并关闭（见图33.2）。如果单击“挂起并关闭”，然后再次启动应用程序，应用程序会从 `ApplicationExecutionState.Terminated` 的先前状态继续，从而打开用户之前打开的页面。

![](img/3d365b72b289213a91ade7eb366b8f35_1249_0.png)

图33.2

## 页面状态

用户输入的任何数据也应该被恢复。在本演示中，在 `Page1` 上创建了两个输入字段（代码文件 `ApplicationLifetimeSample/Page1.xaml`）：

```xml
<TextBox Header="Session State 1" Grid.Row="4"
    Text="{x:Bind Data.Session1, Mode=TwoWay}" />
<TextBox Header="Session State 2" Grid.Row="5"
    Text="{x:Bind Data.Session2, Mode=TwoWay}" />
```

此输入字段的数据表示由从 `Data` 属性返回的 `DataManager` 类定义，如以下代码片段所示（代码文件 `ApplicationLifetimeSample/Page1.xaml.cs`）：

```csharp
public DataManager Data { get; } = DataManager.Instance;
```

`DataManager` 类定义了属性 `Session1` 和 `Session2`，其值存储在一个 `Dictionary` 中（代码文件 `ApplicationLifetimeSample/Services/DataManager.cs`）：
