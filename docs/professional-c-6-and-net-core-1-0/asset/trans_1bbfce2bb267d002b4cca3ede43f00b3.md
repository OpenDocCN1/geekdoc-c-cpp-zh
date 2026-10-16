

> **注意** 创建 NuGet 包在第 17 章“Visual Studio 2015”中进行了讨论。

使用可移植库，Microsoft 维护着一个庞大的列表，说明哪些 API 由哪个平台支持。当你创建可移植库时，会看到配置需要支持的目标平台的对话框。图 31.7 显示了对 .NET Framework 4.6、Windows Universal 10.0、Xamarin.Android 和 Xamarin.iOS 的选择。通过此选择，你只能使用所有所选目标平台都可用的 API。通过当前选择，你可以在对话框中看到说明 .NET Framework 4.5、Windows 8 和 Xamarin.iOS（Classic）也会自动被定位，因为这些平台没有任何 API 是不在所选组合交集中的。

![](img/3d365b72b289213a91ade7eb366b8f35_1168_0.png)

## 图 31.7

可移植库的巨大缺点是，你不能拥有仅在特定平台上可用的代码。你只能使用在所有所选目标平台上都可用的内容。作为一种变通方法，你可以使用可移植库来定义合约的代码，并在需要时用特定于平台的库来实现这些合约。要将来自特定于平台的库的代码与非特定于平台的库一起使用，可以使用依赖注入。如何做到这一点是本章更大示例的一部分，在“View Models”部分中进行了介绍。

## 示例解决方案

示例解决方案由一个用于显示和编辑书籍列表的 WPF 应用程序和一个通用 Windows 平台应用程序组成。为此，解决方案使用了以下项目：

- **BooksDesktopApp**—用于 .NET Framework 4.6 桌面应用程序 UI 的 WPF 项目
- **BooksUniversalApp**—用于现代应用 UI 的 UWP 应用项目
- **Framework**—包含对所有基于 XAML 的应用程序有用的类的可移植库
- **ViewModels**—包含 WPF 和 UWP 共用的视图模型的可移植库
- **Services**—包含视图模型使用的服务的可移植库
- **Models**—包含共享模型的可移植库
- **Repositories**—返回和更新项目的可移植库
- **Contracts**—用于依赖注入的合约接口的可移植库

可移植库配置的目标为 .NET Framework 4.6 和 Windows Universal 10.0。

图 31.8 显示了项目及其依赖关系。Framework 和 Contracts 需要所有其他项目。查看 ViewModels 项目；它会调用服务，但它并不依赖于服务——只是由服务实现的合约。

![](img/3d365b72b289213a91ade7eb366b8f35_1170_0.png)

## 图 31.8

应用程序的用户界面将有两个视图：一个用于以书籍列表形式显示，另一个用于显示书籍详细信息。当你从列表中选择一本书时，会显示其详细信息。也可以添加和编辑书籍。

## 模型

让我们从 Models 库开始定义 Book 类型。这是将在 UI 中显示和编辑的类型。为了支持数据绑定，从用户界面更新值的属性需要更改通知实现。BookId 属性仅显示但不更改，因此该属性不需要更改通知。方法 SetProperty 由基类 BindableBase 定义（代码文件 Models/Book.cs）：

```
public class Book: BindableBase
{
    public int BookId { get; set; }

    private string _title;
    public string Title
    {
        get { return _title; }
        set { SetProperty(ref _title, value); }
    }

    private string _publisher;
    public string Publisher
    {
        get { return _publisher; }
        set { SetProperty(ref _publisher, value); }
    }

    public override string ToString() => Title;
}
```

## 实现更改通知

XAML 元素的对象源需要依赖属性或 `INotifyPropertyChanged` 以允许数据绑定时的更改通知。对于模型类型，实现 `INotifyPropertyChanged` 是有意义的。为了在不同项目中提供实现，实现在 Framework 库项目中的类 `BindableBase` 中完成。`INotifyPropertyChanged` 接口定义了事件 `PropertyChanged`。为了触发更改通知，方法 `SetProperty` 被实现为通用函数以支持任何属性类型。在触发通知之前，会检查新值是否与当前值不同（代码文件 `Framework/BindableBase.cs`）：

```
public abstract class BindableBase: INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    protected virtual void OnPropertyChanged(
        [CallerMemberName] string propertyName = null)
    {
        PropertyChanged?.Invoke(this, new
        PropertyChangedEventArgs(propertyName));
    }

    protected virtual bool SetProperty<T>(ref T item, T value,
        [CallerMemberName] string propertyName = null)
    {
        if (EqualityComparer<T>.Default.Equals(item, value)) return
        false;
        item = value;
        OnPropertyChanged(propertyName);
        return true;
    }
}
```

> **注意** *依赖属性在第 29 章“Core XAML”中进行了说明。*

## 使用存储库模式

接下来你需要一种检索、更新和删除 Book 对象的方法。你可以使用 ADO.NET Entity Framework 从数据库中读取和写入书籍。尽管 Entity Framework 7 可以从通用 Windows 平台访问，但通常这是后端任务，因此本章不涵盖。要使后端可从客户端应用访问，ASP.NET Web API 是服务器端的首选技术。这些主题在第 38 章“Entity Framework Core”和第 42 章“ASP.NET Web API”中进行了介绍。对于客户端应用程序，最好与数据存储无关。为此，定义了 Repository 设计模式。*Repository* 模式是模型和数据访问层之间的中介；它可以充当对象的内存集合。它提供了数据访问层的抽象，并允许更轻松的单元测试。

通用接口 `IQueryRepository` 定义了按 ID 检索一个项目或项目列表的方法（代码文件 Contracts/IQueryRepository.cs）：

```
public interface IQueryRepository<T, in TKey>
    where T: class
{
    Task<T> GetItemAsync(TKey id);
    Task<IEnumerable<T>> GetItemsAsync();
}
```

通用接口 `IUpdateRepository` 定义了添加、更新和删除项目的方法（代码文件 `Contracts/IUpdateRepository.cs`）：

```
public interface IUpdateRepository<T, in TKey>
    where T: class
{
    Task<T> AddAsync(T item);
    Task<T> UpdateAsync(T item);
    Task<bool> DeleteAsync(TKey id);
}
```

`IBooksRepository` 接口通过为通用类型 `T` 定义类型 `Book` 使前两个通用接口具体化（代码文件 `Contracts/IBooksRepository.cs`）：

```
public interface IBooksRepository: IQueryRepository<Book, int>,
    IUpdateRepository<Book, int>
{
}
```

通过使用这些接口，可以更改存储库。创建一个示例存储库 `BooksSampleRepository`，它实现接口 `IBooksRepository` 的成员并包含初始书籍列表（代码文件 `Repositories/BooksSampleRepository.cs`）：

```
public class BooksSampleRepository: IBooksRepository
{
    private List<Book> _books;
    public BooksRepository()
    {
        InitSampleBooks();
    }

    private void InitSampleBooks()
    {
        _books = new List<Book>()
        {
            new Book
            {
                BookId = 1,
                Title = "Professional C# 6 and .NET Core 1.0",
                Publisher = "Wrox Press"
            },
            new Book
            {
                BookId = 2,
                Title = "Professional C# 5.0 and .NET 4.5.1",
                Publisher = "Wrox Press"
            },
            new Book
            {
                BookId = 3,
                Title = "Enterprise Services with the .NET Framework",
```

