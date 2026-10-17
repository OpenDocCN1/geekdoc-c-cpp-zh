
- `Services`—包含视图模型使用的服务的可移植库

- `Models`—包含共享模型的可移植库

- `Repositories`—返回和更新项目的可移植库

- `Contracts`—用于依赖注入的合约接口的可移植库

可移植库配置的目标为 .NET Framework 4.6 和 Windows Universal 10.0。

图 31.8 显示了项目及其依赖关系。Framework 和 Contracts 需要所有其他项目。查看 ViewModels 项目；它会调用服务，但它并不依赖于服务——只是由服务实现的合约。

![](img/3d365b72b289213a91ade7eb366b8f35_1170_0.png)

#### 图 31.8

应用程序的用户界面将有两个视图：一个用于以书籍列表形式显示，另一个用于显示书籍详细信息。当你从列表中选择一本书时，会显示其详细信息。也可以添加和编辑书籍。

#### 模型

让我们从 Models 库开始定义 `Book` 类型。这是将在 UI 中显示和编辑的类型。为了支持数据绑定，从用户界面更新值的属性需要更改通知实现。`BookId` 属性仅显示但不更改，因此该属性不需要更改通知。方法 `SetProperty` 由基类 `BindableBase` 定义（代码文件 `Models/Book.cs`）：

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

#### 实现更改通知

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

> **注意** `依赖属性在第 29 章“Core XAML”中进行了说明。`

#### 使用存储库模式

接下来你需要一种检索、更新和删除 `Book` 对象的方法。你可以使用 ADO.NET Entity Framework 从数据库中读取和写入书籍。尽管 Entity Framework 7 可以从通用 Windows 平台访问，但通常这是后端任务，因此本章不涵盖。要使后端可从客户端应用访问，ASP.NET Web API 是服务器端的首选技术。这些主题在第 38 章“Entity Framework Core”和第 42 章“ASP.NET Web API”中进行了介绍。对于客户端应用程序，最好与数据存储无关。为此，定义了 Repository 设计模式。`Repository` 模式是模型和数据访问层之间的中介；它可以充当对象的内存集合。它提供了数据访问层的抽象，并允许更轻松的单元测试。

通用接口 `IQueryRepository` 定义了按 ID 检索一个项目或项目列表的方法（代码文件 `Contracts/IQueryRepository.cs`）：

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
                Publisher ="AWL"
            }
        };
    }

    public Task<bool> DeleteAsync(int id)
    {
        Book bookToDelete = _books.Find(b => b.BookId == id);
        if (bookToDelete != null)
        {
            return Task.FromResult<bool>(_books.Remove(bookToDelete));
        }
        return Task.FromResult<bool>(false);
    }

    public Task<Book> GetItemAsync(int id)
    {
        return Task.FromResult(_books.Find(b => b.BookId == id));
    }

    public Task<IEnumerable<Book>> GetItemsAsync() =>
        Task.FromResult<IEnumerable<Book>>(_books);

    public Task<Book> UpdateAsync(Book item)
    {
        Book bookToUpdate = _books.Find(b => b.BookId ==
item.BookId);
        int ix = _books.IndexOf(bookToUpdate);
        _books[ix] = item;
        return Task.FromResult(_books[ix]);
    }

    public Task<Book> AddAsync(Book item)
    {
        item.BookId = _books.Select(b => b.BookId).Max() + 1;
        _books.Add(item);
        return Task.FromResult(item);
    }
}
```

> 注意：仓库定义了异步方法，尽管在目前情况下并不需要，因为书籍仅通过内存进行检索和更新。之所以定义异步方法，是因为用于访问 ASP.NET Web API 或实体框架的仓库本质上是异步的。

#### 视图模型

让我们创建包含视图模型的库。每个视图都有一个视图模型。在示例应用中，`BooksView` 关联了 `BooksViewModel`，`BookView` 关联了 `BookViewModel`。视图和视图模型之间存在一一对应的关系。实际上，视图和视图模型之间存在多对一的映射，因为同一个视图可以用于不同的技术——WPF 和 UWP。这使得视图模型不能了解视图的任何信息，而视图却需要了解视图模型，这一点非常重要。视图模型通过可移植库实现，从而可以在 WPF 和 UWP 中使用。

可移植库 `ViewModels` 引用了 `Contracts`、`Models` 和 `Framework` 库，这些库也都是可移植库。

视图模型包含用于显示项的属性和用于操作的命令。`BooksViewModel` 类定义了属性 `Books`（用于显示书籍列表）和 `SelectedBook`（当前选中的书籍）。`BooksViewModel` 还定义了命令 `GetBooksCommand` 和 `AddBookCommand`（代码文件 `ViewModels/BooksViewModel.cs`）：

```
public class BooksViewModel: ViewModelBase
{
    private IBooksService _booksService;

    public BooksViewModel(IBooksService booksService)
    {
        // etc.
    }

    private Book _selectedBook;
    public Book SelectedBook
    {
        get { return _selectedBook; }
        set
        {
            if (SetProperty(ref _selectedBook, value))
            {
                // etc.
            }
        }
    }

    public IEnumerable<Book> Books => _booksService.Books;
    public ICommand GetBooksCommand { get; }

    public async void OnGetBooks()
    {
        // etc.
    }

    private bool _canGetBooks = true;

    public bool CanGetBooks() => _canGetBooks;

    private void OnAddBook()
    {
        // etc.
    }

    public ICommand AddBookCommand { get; }
}
```

`BookViewModel` 类定义了属性 `Book` 来显示选中的书籍，以及命令 `SaveBookCommand`（代码文件 `ViewModels/BookViewModel.cs`）：

```
public class BookViewModel: ViewModelBase
{
    private IBooksService _booksService;
    public BookViewModel(IBooksService booksService)
    { // etc. }

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

    private Book _book;
    public Book Book
    {
        get { return _book; }
        set { SetProperty(ref _book, value); }
    }

    private async void OnSaveBook()
    {
        Book book = await _booksService.AddOrUpdateBookAsync(Book);
        Book = book;
    }
}
```

视图模型的属性需要更改通知以更新 UI。接口 `INotifyPropertyChanged` 通过基类 `BindableBase` 实现。视图模型类从 `ViewModelBase` 派生以获得此实现。您可以使用 `ViewModelBase` 类来支持视图模型的其他功能，例如提供进度信息和输入验证（代码文件 `Frameworks/ViewModelBase.cs`）：

```
public abstract class ViewModelBase: BindableBase
{
}
```

### 命令

视图模型提供实现了 `ICommand` 接口的命令。命令通过数据绑定实现了视图与命令处理程序方法之间的分离。命令还提供启用或禁用命令的功能。`ICommand` 接口定义了 `Execute` 和 `CanExecute` 方法以及 `CanExecuteChanged` 事件。

为了将命令映射到方法，在 Framework 程序集中定义了 `DelegateCommand` 类。

`DelegateCommand` 定义了两个构造函数，其中可以传递一个委托给应通过命令调用的方法，另一个委托定义该命令是否可用（代码文件 `Framework/DelegateCommand.cs`）：
