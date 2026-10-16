

```
public ICommand SaveBookCommand { get; }

private void LoadBook(object sender, BookInfoEvent bookInfo)
{
	if (bookInfo.BookId == 0)
	{
		Book = new Book();
	}
	else
	{
		Book = _booksService.GetBook(bookInfo.BookId);
	}
}

public void Dispose()
{
	EventAggregator<BookInfoEvent>.Instance.Event -= LoadBook;
}
// etc.
```

事件在 ListBox 中选择书籍时发布，因此 SelectedBook 属性会调用 set 访问器。在这里，可以通过静态 Instance 属性以类似订阅的方式访问 EventAggregator，现在通过调用 Publish 方法，该方法传递一个 BookInfoEvent 对象（代码文件 ViewModels/BooksViewModel.cs）：

```
private Book _selectedBook;
public Book SelectedBook
{
	get { return _selectedBook; }
	set
	{
		if (SetProperty(ref _selectedBook, value))
		{
			EventAggregator<BookInfoEvent>.Instance.Publish(
				this, new BookInfoEvent { BookId = _selectedBook.BookId });
		}
	}
}
```

有了消息机制后，你可以启动应用程序，选择书籍并像图 31.11 所示那样添加它们。

![](img/3d365b72b289213a91ade7eb3668f35_1188_0.png)

## IoC 容器

使用依赖注入时，你也可以使用一个控制反转（IoC）容器。在之前的代码片段中，你直接从客户端应用程序注入了一个具体类型——例如 BooksViewModel 中的 BooksService 实例（代码文件 BooksDesktopApp/Views/BooksView.xaml.cs）：

```
public BooksViewModel ViewModel { get; } =
    new BooksViewModel((App.Current as App).BooksService);
```

你可以将其更改为让 IoC 容器注入依赖项。有多个 IoC 容器以 NuGet 包形式提供，例如 Castle Windsor (http://castleproject.org/projects/Windsor)、Unity (http://unity.codeplex.com)、Autofac (http://github.com/autofac)、托管可扩展性框架（在第 26 章“组合”中介绍），以及更多。 在 .NET Core 1.0 中，微软提供了一个 IoC 容器，可通过 NuGet 包 Microsoft.Framework.DependencyInjection (http://github.com/aspnet/DependencyInjection) 获得。这是一个轻量级框架，支持构造函数注入，也是 ASP.NET Core 1.0 使用的依赖注入容器（参见第 40 章“ASP.NET Core”）。本节中的代码示例使用此 .NET Core 1.0 IoC 容器。

要使用该容器，你需要添加 NuGet 包 Microsoft.Framework.DependencyInjection。在 App 类中，你可以将服务添加到 ServiceCollection（命名空间 Microsoft.Framework.DependencyInjection）。AddTransient 方法注册的类型在每次解析该类型时都会重新实例化；AddSingleton 只实例化一次类型并在每次解析时返回同一实例。传递两个泛型参数（在 books 服务和 books 仓库中完成），可以请求第一个类型，容器会创建第二个参数的实例。BuildServiceProvider 方法返回一个实现 IServiceProvider 的对象，可在以后用于解析类型。在 WPF 中，返回的 IServiceProvider 对象在 OnStartup 方法中分配给 Container 方法（代码文件 BooksDesktopApp/App.xaml.cs）：

```
private IServiceProvider RegisterServices()
{
    var serviceCollection = new ServiceCollection();
    serviceCollection.AddTransient<BooksViewModel>();
    serviceCollection.AddTransient<BookViewModel>();
    serviceCollection.AddSingleton<IBooksService, BooksService>();
    serviceCollection.AddSingleton<IBooksRepository, BooksSampleRepository>();
    return serviceCollection.BuildServiceProvider();
}
```

```
public IServiceProvider Container { get; private set; }
```

```
protected override void OnStartup(StartupEventArgs e)
{
    base.OnStartup(e);
```

```
```csharp
Container = RegisterServices();

var mainWindow = new MainWindow();
mainWindow.Show();
}
```
```

对于 UWP 项目，`RegisterServices` 方法和 `Container` 属性在 `App` 类中相同。不同之处在于启动方法 `OnLaunched`，其中调用了 `RegisterServices` 方法（代码文件 `BooksUniversalApp/App.xaml.cs`）：

```
```csharp
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    Container = RegisterServices();

    // etc.
}
```
```

在视图的代码隐藏中，你可以通过调用 `IServiceProvider` 的 `GetService` 方法来初始化 `ViewModel` 属性。`App` 类的 `Container` 属性返回一个 `IServiceProvider`。`GetService` 方法的泛型版本是一个扩展方法，可在命名空间 `Microsoft.Framework.DependencyInjection` 中使用，需要导入该命名空间才能使用此扩展方法（代码文件 `BooksDesktopApp/Views/BooksView.xaml.cs` 和 `BooksUniversalApp/Views/BooksView.xaml.cs`）：

```
```csharp
public BooksViewModel ViewModel { get; } =
    (App.Current as App).Container.GetService<BooksViewModel>();
```
```

在 `BookView.xaml.cs` 文件中也需要进行相同的更改，否则会创建不同的 `BooksService` 实例。在可下载的示例文件中，你需要取消注释此属性的设置并注释之前的那一行，以使 IoC 容器成为活动容器。

现在运行应用程序时，`BooksViewModel` 将从容器中实例化。由于此视图模型的构造函数需要类型 `IBooksService`，因此会创建 `BooksService` 实例并传递，因为这些类型也已在容器中注册。`BooksService` 又需要在构造函数中使用 `IBooksRepository`。在这里，注入了 `BooksSampleRepository`。如果遗漏了这些依赖项的注册，将抛出类型为 `InvalidOperationException` 的异常。未能注册 `IBooksRepository` 接口会给出错误信息 `Unable to resolve service for type 'Contracts.IBooksRepository' while attempting to activate 'Services.BooksService'.`

## 使用框架

通过示例应用程序，你已经看到了在 Framework 项目中定义的类，例如 `BindableBase`、`DelegateCommand` 和

EventAggregator。这些类在所有基于 MVVM 的应用程序中都需要，你不需要自己实现它们。实现它们并不困难，但你也可以使用现有的 MVVM 框架。Laurent Bugnion 的 MVVM Light (http://mvvmlight.net) 是一个小型框架，恰好适合 MVVM 应用程序的目的，并且可用于许多不同的平台。

另一个最初由 Microsoft 模式与实践团队创建，现已移交给社区的框架是 Prism.Core (http://github.com/PrismLibrary)。尽管 Prism 框架是一个功能齐全的框架，支持插件和用于放置控件的区域，但 Prism.Core 非常轻量，仅包含少数类型，如 `BindableBase`、`DelegateCommand` 和 `ErrorsContainer`。在代码下载中，你会发现本章的示例也使用 Prism.Core 实现。

## 总结

本章为你提供了围绕 MVVM 模式创建基于 XAML 的应用程序的架构指导。你已经看到了模型、视图和视图模型之间的关注点分离。除此之外，你还看到了使用接口 `INotifyPropertyChanged` 实现更改通知、数据绑定和编译数据绑定、使用仓库模式分离数据访问代码、使用事件在视图模型之间进行消息传递（也可用于与视图通信），以及有无 IoC 容器的依赖注入。

所有这些都允许在仍使用特定平台功能的同时进行代码共享。你可以使用仓库和服务实现中的特定于平台的功能，并且所有平台都提供契约。对于代码共享，你已经看到了 UWP 的 API 契约、共享项目和便携式库。

下一章将指导你了解通用 Windows 平台应用的用户界面功能。

