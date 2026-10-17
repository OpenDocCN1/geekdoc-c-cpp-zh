
```csharp
public class DataManager: INotifyPropertyChanged
{
    private const string SessionStateFile = "TempSessionState.json";
    private Dictionary<string, string> _state = new Dictionary<string, string>()
    {
        [nameof(Session1)] = string.Empty,
        [nameof(Session2)] = string.Empty
    };

    private DataManager()
    {
    }

    public event PropertyChangedEventHandler PropertyChanged;

    protected void OnPropertyChanged(
        [CallerMemberName] string propertyName = null)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }

    public static DataManager Instance { get; } = new DataManager();

    public string Session1
    {
        get { return _state[nameof(Session1)]; }
        set
        {
            _state[nameof(Session1)] = value;
            OnPropertyChanged();
        }
    }

    public string Session2
    {
        get { return _state[nameof(Session2)]; }
        set
        {
            _state[nameof(Session2)] = value;
            OnPropertyChanged();
        }
    }
}
```

对于加载和存储会话状态，定义了`SaveTempSessionAsync()`和`LoadTempSessionAsync()`方法。实现使用了 Json.Net 将字典序列化为 JSON 格式。当然，你也可以使用任何你喜欢的序列化方式（代码文件 `ApplicationLifetimeSample/Services/DataManager.cs`）：

```csharp
public async Task SaveTempSessionAsync()
{
    StorageFile file =
        await ApplicationData.Current.LocalCacheFolder.CreateFileAsync(
            SessionStateFile,
            CreationCollisionOption.ReplaceExisting);
    Stream stream = await file.OpenStreamForWriteAsync();

    var serializer = new JsonSerializer();
    using (var writer = new StreamWriter(stream))
    {
        serializer.Serialize(writer, _state);
    }
}

public async Task LoadTempSessionAsync()
{
    Stream stream = await
        ApplicationData.Current.LocalCacheFolder.OpenStreamForReadAsync(
            SessionStateFile);

    var serializer = new JsonSerializer();
    using (var reader = new StreamReader(stream))
    {
        string json = await reader.ReadLineAsync();
        Dictionary<string, string> state =
            JsonConvert.DeserializeObject<Dictionary<string, string>>(json);
        _state = state;

        foreach (var item in state)
        {
            OnPropertyChanged(item.Key);
        }
    }
}
```

> 注意 XML 和 JSON 的序列化在第 27 章“XML 和 JSON”中讨论。

剩下的就是在应用挂起和激活时调用`SaveTempSessionAsync()`和`LoadTempSessionAsync()`方法。这些方法被添加到与页面栈写入和读取相同的位置，即`OnSuspending()`和`OnLaunched()`方法中（代码文件 `ApplicationLifetimeSample/App.xaml.cs`）：

```csharp
private async void OnSuspending(object sender, SuspendingEventArgs e)
{
    var deferral = e.SuspendingOperation.GetDeferral();
    //...

    await DataManager.Instance.SaveTempSessionAsync();

    deferral.Complete();
}

protected override async void OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;

    if (rootFrame == null)
    {
        rootFrame = new Frame();
        rootFrame.NavigationFailed += OnNavigationFailed;

        if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
        {
            //...
            await DataManager.Instance.LoadTempSessionAsync();
        }
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

现在你可以运行应用，在`Page2`中输入状态，挂起并终止应用，再次启动后状态会再次显示出来。

通过应用生命周期，你已经看到为了考虑 UWP 应用的电池消耗，需要特殊的编程。下一个主题讨论在应用之间共享数据，这在手机平台上也可用。

## 共享数据

当应用能够与其他应用交互时，其实用性会大大提高。在 Windows 10 中，应用可以使用拖放与桌面应用程序共享数据，甚至在 Windows 应用之间，也可以使用共享契约共享数据。

当你使用共享契约时，一个应用（共享源）可以以多种不同格式共享数据——例如文本、HTML、图像或自定义数据——用户可以选择接受该数据格式的应用作为共享目标。Windows 通过在安装时与应用注册的契约，找到支持相应数据格式的应用。

### 共享源

关于共享，首先要考虑的是确定应以何种格式共享什么数据。可以共享简单文本、富文本、HTML 和图像，甚至是自定义类型。当然，这些类型必须为其他应用程序所知并使用——共享目标。共享自定义类型只能与知道该类型并且是该类型的共享目标的其他应用程序一起使用。示例应用程序以文本格式提供共享数据，并以 HTML 格式提供图书列表。

为了以 HTML 格式提供图书信息，你定义一个简单的`Book`类（代码文件 `SharingSource\Models\Book.cs`）：

```csharp
public class Book
{
    public string Title { get; set; }
    public string Publisher { get; set; }
}
```

`Book`对象的列表由`BooksRepository`类的`GetSampleBooks()`方法返回（代码文件 `SharingSource\Models\BooksRepository.cs`）：

```csharp
public class BooksRepository
{
    public IEnumerable<Book> GetSampleBooks() =>
        new List<Book>()
        {
            new Book
            {
                Title = "Professional C# 6 and .NET 5 Core",
                Publisher = "Wrox Press"
            },
            new Book
            {
                Title = "Professional C# 5.0 and .NET 4.5.1",
                Publisher = "Wrox Press"
            }
        };
```

为了将`Book`对象的列表转换为 HTML，扩展方法`ToHtml()`在 LINQ to XML 的帮助下返回一个 HTML 表格（代码文件 `SharingSource\Utilities\BooksExtensions.cs`）：

```csharp
public static class BookExtensions
{
    public static string ToHtml(this IEnumerable<Book> books) =>
        new XElement("table",
            new XElement("thead",
                new XElement("tr",
                    new XElement("td", "Title"),
                    new XElement("td", "Publisher"))),
            books.Select(b =>
                new XElement("tr",
                    new XElement("td", b.Title),
                    new XElement("td", b.Publisher))).ToString();
}
```

> 注意 LINQ to XML 在第 27 章中介绍。

使用`MainPage`，你定义一个`Button`，用户可以发起共享，以及一个`TextBox`控件供用户输入要共享的文本数据（代码文件 `SharingSource\MainPage.xaml`）：

```xml
<RelativePanel Margin="24">
    <Button x:Name="shareDataButton" Content="Share Data"
        Click="{x:Bind DataSharing.ShowShareUI, Mode=OneTime}"
        Margin="12" />
    <TextBox RelativePanel.RightOf="shareDataButton"
        Text="{x:Bind DataSharing.SimpleText, Mode=TwoWay}"
        Margin="12" />
</RelativePanel>
```

在代码隐藏文件中，`DataSharing`属性返回`ShareDataViewModel`，其中实现了所有重要的共享功能（代码文件 `SharingSource\MainPage.xaml.cs`）：

```csharp
public ShareDataViewModel DataSharing { get; set; } = new ShareDataViewModel();
```

`ShareDataViewModel`定义了`SimpleText`属性，该属性由 XAML 文件绑定以输入要共享的简单文本。对于共享，事件处理方法`ShareDataRequested()`被分配给`DataTransferManager`的`DataRequested`事件。当用户请求共享数据时触发此事件（代码文件 `SharingSource\ViewModels\ShareDataViewModel.cs`）：

```csharp
public class ShareDataViewModel
{
    public ShareDataViewModel()
    {
        DataTransferManager.GetForCurrentView().DataRequested +=
            ShareDataRequested;
    }

    public string SimpleText { get; set; } = string.Empty;

    //...
```

当事件触发时，会调用`OnShareDataRequested()`方法。此方法接收`DataTransferManager`作为第一个参数，`DataRequestedEventArgs`作为第二个参数。在共享数据时，需要填充`args.Request.Data`引用的`DataPackage`。你可以使用`Title`、`Description`和`Thumbnail`属性为用户界面提供信息。应共享的数据必须通过其中一个`SetXXX`方法传递。示例代码共享简单文本和 HTML 代码，因此使用了`SetText()`和`SetHtmlFormat()`方法。`HtmlFormatHelper`类有助于创建共享所需的周围 HTML 代码。图书的 HTML 代码使用前面显示的扩展方法`ToHtml()`创建（代码文件 `SharingSource\ViewModels\ShareDataViewModel.cs`）：

```csharp
private void ShareDataRequested(DataTransferManager sender,
    DataRequestedEventArgs args)
{
    var books = new BooksRepository().GetSampleBooks();

    Uri baseUri = new Uri("ms-appx:///");
    DataPackage package = args.Request.Data;
    package.Properties.Title = "Sharing Sample";
    package.Properties.Description = "Sample for sharing data";
    package.Properties.Thumbnail =
        RandomAccessStreamReference.CreateFromUri(
            new Uri(baseUri, "Assets/Square44x44Logo.png"));
    package.SetText(SimpleText);

    package.SetHtmlFormat(HtmlFormatHelper.CreateHtmlFormat(books.To
```

如果需要在共享操作完成后获取信息——例如从源应用程序中删除数据——`DataPackage`类会触发`OperationCompleted`和`Destroyed`事件。

注意 除了提供文本或 HTML 代码外，其他方法如`SetBitmap()`、`SetRtf()`和`SetUri()`也可用于提供其他数据格式。

注意 如果需要在`ShareDataRequested()`方法内使用异步方法构建共享数据，则需要使用延期在数据可用时提供信息。这与本章前面显示的页面挂起机制类似。使用`DataRequestedEventArgs`类型的`Request`属性，你可以调用`GetDeferral()`方法。此方法返回类型为`DataRequestedDeferral`的延期。通过此对象，你可以在数据准备就绪时调用`Complete()`方法。

最后，需要显示用于共享的用户界面。这使用户能够选择目标应用：

```csharp
public void ShowShareUI()
{
    DataTransferManager.ShowShareUI();
}
```

图33.3展示了调用`DataTransferManager`的`ShowShareUI()`方法后的用户界面。根据所提供的数据格式以及已安装的应用，会显示相应的应用供用户选择。

![](img/3d365b72b289213a91ade7eb366b8f35_1255_0.png)

#### 图33.3

如果选择邮件应用，则会传递HTML信息。图33.4显示了该应用内接收到的数据。

| 标题 | 发布者 |
| --- | --- |
| Professional C# 6 and .NET 5 Core | Wrox Press |
