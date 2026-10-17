
在你的应用之间共享数据的另一种方式是使用应用服务。应用服务是 Windows 10 的一项新功能，可与调用 Web 服务相比较，但服务位于用户系统本地。多个应用可以访问同一服务，这就是你在应用之间共享信息的方式。应用服务与 Web 服务之间的一个重要区别是，用户无需通过此功能进行交互；所有操作都可以从应用中完成。

示例应用 `AppServices` 使用服务来缓存 `Book` 对象。通过调用服务，可以检索 `Book` 对象的列表，并向服务添加新的 `Book` 对象。

该应用包含多个项目。

- 一个 .NET 便携式库（`BooksCacheModel`）定义了该应用的模型——`Book` 类。为了便于数据传输，提供了扩展方法将 `Book` 对象转换为 JSON，反之亦然。该库被所有其他项目使用。

- 第二个项目（`BooksCacheService`）是一个 Windows 运行时组件，定义了图书服务本身。此类服务需要在后台运行；因此实现了一个后台任务。

- 后台任务需要向系统注册。该项目是一个 Windows 应用：`BooksCacheProvider`。

- 调用应用服务的客户端应用是一个 Windows 应用：`BooksCacheClient`。

让我们深入了解这些部分。

### Creating the Model

便携式库 `BooksCacheModel` 包含 `Book` 类、借助 NuGet 包 `Newtonsoft.Json` 的 JSON 转换器，以及一个仓库。

`Book` 类定义了 `Title` 和 `Publisher` 属性（代码文件 `AppServices/BooksCacheModel/Book.cs`）：

```
public class Book
{
    public string Title { get; set; }
    public string Publisher { get; set; }
}
```

`BooksRepository` 类保存了 `Book` 对象的内存缓存，允许用户通过 `AddBook` 方法添加图书对象，并通过 `Books` 属性返回所有缓存的图书。为了在不添加新图书的情况下就能看到一本书，初始化时已向列表中添加了一本书（代码文件 `AppServices/BooksCacheModel/BooksRepository.cs`）：

```
public class BooksRepository
{
    private readonly List<Book> _books = new List<Book>()
    {
        new Book {Title ="Professional C# 6", Publisher ="Wrox Press" }
    };
    public IEnumerable<Book> Books => _books;

    private BooksRepository()
    {
    }

    public static BooksRepository Instance = new BooksRepository();

    public void AddBook(Book book)
    {
        _books.Add(book);
    }
}
```

由于跨应用服务传输的数据需要可序列化，扩展类 `BookExtensions` 定义了一些扩展方法，将 `Book` 和 `Book` 列表转换为 JSON 字符串，反之亦然。通过 App 服务传递字符串是一项简单的任务。扩展方法使用了 NuGet 包 `Newtonsoft.Json` 提供的 `JsonConvert` 类（代码文件 `AppServices/BooksCacheModel/BookExtensions.cs`）：

```
public static class BookExtensions
{
    public static string ToJson(this Book book) =>
        JsonConvert.SerializeObject(book);

    public static string ToJson(this IEnumerable<Book> books) =>
        JsonConvert.SerializeObject(books);

    public static Book ToBook(this string json) =>
        JsonConvert.DeserializeObject<Book>(json);

    public static IEnumerable<Book> ToBooks(this string json) =>
        JsonConvert.DeserializeObject<IEnumerable<Book>>(json);
}
```

### Creating a Background Task for App Service Connections

现在让我们深入了解此示例应用的核心：应用服务。你需要将应用服务实现为 Windows 运行时组件库，并作为后台任务实现 `IBackgroundTask` 接口。Windows 后台任务可以在没有用户交互的情况下在后台运行。

有不同种类的后台任务。后台任务可以根据计时器间隔、Windows 推送通知、位置信息、蓝牙设备连接或其他事件启动。

类 `BooksCacheTask` 是应用服务的后台任务。接口 `IBackgroundTask` 定义了需要实现的 `Run` 方法。在实现中，在接收到应用服务连接时定义了一个请求处理程序（代码文件 `AppServices/BooksCacheService/BooksCacheTask.cs`）：

```
public sealed class BooksCacheTask: IBackgroundTask
{
    private BackgroundTaskDeferral _taskDeferral;

    public void Run(IBackgroundTaskInstance taskInstance)
    {
        _taskDeferral = taskInstance.GetDeferral();
        taskInstance.Canceled += OnTaskCanceled;

        var trigger = taskInstance.TriggerDetails as AppServiceTriggerDetails;
        AppServiceConnection connection = trigger.AppServiceConnection;
        connection.RequestReceived += OnRequestReceived;
    }

    private void OnTaskCanceled(IBackgroundTaskInstance sender, BackgroundTaskCancellationReason reason)
    {
        _taskDeferral?.Complete();
    }

    // etc.
```

通过实现 `OnRequestReceived` 处理程序，服务可以读取请求并需要提供答复。接收到的请求包含在 `AppServiceRequestReceivedEventArgs` 的 `Request.Message` 属性中。`Message` 属性返回一个 `ValueSet` 对象。`ValueSet` 是键及其对应值的字典。此处服务需要一个 `command` 键，其值要么为 `GET` 要么为 `POST`。`GET` 命令返回所有图书的列表，而 `POST` 命令需要额外的键 `book`，其值为 `Book` 对象表示的 JSON 字符串。根据接收到的消息，会调用 `GetBooks` 或 `AddBook` 辅助方法。这些消息的返回结果通过调用 `SendResponseAsync` 返回给调用方：

```
private async void OnRequestReceived(AppServiceConnection sender,
    AppServiceRequestReceivedEventArgs args)
{
    AppServiceDeferral deferral = args.GetDeferral();
    try
    {
        ValueSet message = args.Request.Message;
        ValueSet result = null;

        switch (message["command"].ToString())
        {
            case"GET":
                result = GetBooks();
                break;
            case"POST":
                result = AddBook(message["book"].ToString());
                break;
            default:
                break;
        }
        await args.Request.SendResponseAsync(result);
    }
    finally
    {
        deferral.Complete();
    }
}
```

`GetBooks` 方法使用 `BooksRepository` 以 JSON 格式获取所有书籍，并创建一个带有 `result` 键的 `ValueSet`：

```
private ValueSet GetBooks()
{
    var result = new ValueSet();
    result.Add("result",
BooksRepository.Instance.Books.ToJson());
    return result;
}
```

`AddBook` 方法使用存储库添加一本书，并返回一个带有 `result` 键且值为 `ok` 的 `ValueSet`：

```
private ValueSet AddBook(string book)
{
    BooksRepository.Instance.AddBook(book.ToBook());
    var result = new ValueSet();
    result.Add("result","ok");
    return result;
}
```

### 注册 App 服务

现在你需要将应用服务注册到操作系统。这是通过创建一个引用 `BooksCacheService` 的普通 UWP 应用来完成的。借助此应用，你必须在 `package.appxmanifest` 中定义声明（参见图 33.8）。在应用声明列表中添加一个应用服务并为其命名。你需要将入口点设置为后台任务，包括命名空间和类名。

![](img/3d365b72b289213a91ade7eb366b8f35_1267_0.png)

#### 图 33.8

对于客户端应用，你需要使用 `package.appxmanifest` 定义的应用名称以及包名称。要查看包名称，可以调用 `Package.Current.Id.FamilyName`。为了便于查看此名称，它被写入到在用户界面中绑定的属性 `PackageFamilyName`（代码文件 `AppServices/BooksCacheProvider/MainPage.xaml.cs`）：

```
public sealed partial class MainPage: Page
{
    public MainPage()
    {
        this.InitializeComponent();
        PackageFamilyName = Package.Current.Id.FamilyName;
    }

    public string PackageFamilyName
    {
        get { return (string)GetValue(PackageFamilyNameProperty); }
        set { SetValue(PackageFamilyNameProperty, value); }
    }

    public static readonly DependencyProperty
PackageFamilyNameProperty =
        DependencyProperty.Register("PackageFamilyName",
typeof(string),
            typeof(MainPage), new PropertyMetadata(string.Empty));
}
```

运行此应用时，它会注册后台任务并显示客户端应用所需的包名称。

### 调用 App 服务

借助客户端应用，现在可以调用应用服务。客户端应用 `BooksCacheClient` 的主要部分使用视图模型实现。`Books` 属性在 UI 中绑定以显示从服务返回的所有书籍。此集合由 `GetBooksAsync` 方法填充。`GetBooksAsync` 创建一个带有 `GET` 命令的 `ValueSet`，该命令通过辅助方法 `SendMessageAsync` 发送到应用服务。此辅助方法返回一个 JSON 字符串，随后将其转换为 `Book` 集合，用于填充 `Books` 属性的 `ObservableCollection`（代码文件 `AppServices/BooksCacheClient/ViewModels/BooksViewModel.cs`）：

```
public class BooksViewModel
{
    private const string BookServiceName
="com.CNinnovation.BooksCache";
    private const string BooksPackageName =
        "CNinnovation.Samples.BookCache_p2wxv0ry6mv8g";

    public ObservableCollection<Book> Books { get; } =
        new ObservableCollection<Book>();

    public async void GetBooksAsync()
    {
        var message = new ValueSet();
        message.Add("command","GET");
        string json = await SendMessageAsync(message);
        IEnumerable<Book> books = json.ToBooks();
        foreach (var book in books)
        {
            Books.Add(book);
        }
    }
}
```

`PostBookAsync` 方法创建一个 `Book` 对象，将其序列化为 JSON，并通过 `ValueSet` 发送到 `SendMessageAsync` 方法：

```
public string NewBookTitle { get; set; }
    public string NewBookPublisher { get; set; }

    public async void PostBookAsync()
    {
        var message = new ValueSet();
        message.Add("command","POST");
        string json = new Book
        {
            Title = NewBookTitle,
            Publisher = NewBookPublisher
        }.ToJson();
        message.Add("book", json);
        string result = await SendMessageAsync(message);
    }
```

与应用服务相关的客户端代码包含在 `SendMessageAsync` 方法中。在这里，创建了一个 `AppServiceConnection`。使用 `using` 语句在用完后通过释放它来关闭连接。为了将连接映射到正确的服务，需要提供 `AppServiceName` 和 `PackageFamilyName` 属性。设置这些属性后，通过调用 `OpenAsync` 方法打开连接。只有在成功打开连接时，才会使用来自调用方法的 `ValueSet` 发送请求。`AppServiceConnection` 方法 `SendMessageAsync` 向服务发出请求并返回一个 `AppServiceResponse` 对象。响应包含来自服务的結果，并据此进行处理：
