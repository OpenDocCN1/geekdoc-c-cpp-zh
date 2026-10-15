
```csharp
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)

    {

        base.OnConfiguring(optionsBuilder);

        optionsBuilder.UseInMemoryDatabase("StorageAppDb");

    }

}
```

> ▲ 1 / 2 ▼（扩展）`DbContextOptionsBuilder` `DbContextOptionsBuilder.UseInMemoryDatabase(string databaseName, [System.Action<Microsoft.EntityFrameworkCore.Infrastructure.InMemoryDbContextOptionsBuilder>] inMemoryOptionsAction = null)`
> 配置上下文以连接到有名称的内存数据库。只要 `databaseName` 相同，内存数据库就会在任何位置共享
> `databaseName`：内存数据库的名称。这样可以控制内存数据库的作用范围

接下来，让我们创建一个构造函数，该构造函数接受一个 `DbContext` 实例作为参数。我按 `Ctrl+.` 为 `Microsoft.EntityFrameworkCore` 添加 `using`。让我们把这个参数命名为 `dbContext`，然后按 `Ctrl+.` 创建并分配一个 `_dbContext` 字段。此外，我还想从 `dbContext` 中获取 `DbSet`，并将其存储到 `_dbSet` 字段中。所以在 `dbContext` 上，我使用我们已经用过的泛型 `Set<T>()` 方法，并将实体指定为 `T` 类型。现在按 `Ctrl+.` 在我们的类中创建该 `DbSet` 字段。这就是创建出来的 `_dbSet` 字段，但如你所见，它带有红色下划线。当你将鼠标悬停在它上面时，你会看到错误：类型 `T` 必须是引用类型，才能用作泛型类型或方法 `DbSet<TEntity>` 中的参数 `TEntity`。

```csharp
public class SqlRepository<T> where T : IEntity

{

    private readonly DbContext _dbContext;

    public SqlRepository(DbContext dbContext)

    {

        _dbContext = dbContext;

    }

    public T GetById(int id)

    {

        return _items.Single(item => item.Id == id);

    }

}
```

这意味着我们需要调整泛型类型约束，因为 `T` 必须是引用类型，才能与 Entity Framework Core 一起使用。为此，让我们在这里使用 `IEntity` 接口之前的 `class` 约束。现在你会看到错误消失了。接下来，你现在可以实现这些方法了。`GetById()` 非常简单。在 `dbSet` 上，你可以使用 `id` 调用 `Find()` 方法，它会按 ID 返回该对象。`Add()` 方法也很简单。在 `dbSet` 上，你可以使用 `T` 类型的项调用 `Add()` 方法。

```csharp
public class SqlRepository<T> where T : class, IEntity

{

    private readonly DbContext _dbContext;

    private readonly DbSet<T> _dbSet;

    public SqlRepository(DbContext dbContext)

    {

        _dbContext = dbContext;

        _dbSet = _dbContext.Set<T>();

    }

    public T GetById(int id)

    {

        return _items.Single(item => item.Id == id);

    }

    public void Add(T item)
```

`Remove()` 方法也很简单。在 `dbSet` 上，你可以使用该项调用 `Remove()` 方法。在 `Save()` 方法中，你不需要 `foreach` 循环。相反，你使用 `dbContext` 实例，并调用它的 `SaveChanges()` 方法。就这样。现在你已经实现了一个泛型 `SqlRepository` 类，它使用 Entity Framework `DbContext` 来存储项。现在让我们前往解决方案资源管理器，打开 `Program.cs` 文件，在这里我们使用 `SqlRepository` 而不是 `ListRepository`。

```csharp
public void Add(T item)

{

    _dbSet.Add(item);

}

public void Remove(T item)

{

    _dbSet.Remove(item);

}

public void Save()

{

    _dbContext.SaveChanges();

}
```

`SqlRepository` 的构造函数接受一个 `DbContext` 实例，所以让我们在这里创建 `StorageAppDbContext` 类的一个新实例。我按 `Ctrl+.` 为包含此类的 `Data` 命名空间添加 `using`。所以现在你有了一个 `SqlRepository` 实例，但如你所见，它在这里带有红色下划线，因为它不是这两个方法的有效参数。这是因为这些方法接受的是 `ListRepository` 类型，而不是 `SqlRepository` 类型。因此，当你将鼠标悬停在此处的 `employeeRepository` 参数上时，会看到错误：无法将 `SqlRepository` 转换为 `ListRepository`。让我们在下一章通过创建泛型接口来解决这个问题。

## 第 10 章 如何创建泛型接口

在本演示中，你将学习如何创建泛型接口。这里，我已经打开了 `StorageApp` 的 `Program.cs` 文件。此前，你已经创建了 `SqlRepository` 类，但它无法与这些方法一起使用，因为这些方法的参数是 `ListRepository`。现在，让我们引入一个泛型 `IRepository` 接口，使这些方法不仅能处理列表仓库，还能处理 SQL 仓库。为此，让我们打开 `SqlRepository` 类。首先，让我把光标放在 `using` 语句上，然后按 `Ctrl+.` 删除不必要的 `using`。现在，把光标放在 `SqlRepository` 类名上，按 `Ctrl+.`，你可以看到 Visual Studio 建议在这里提取接口。

![](img/0155736aec718cf18821e9f10a5d308d_1114_0.png)

按 Enter 选择此选项。在这个对话框中，我们将新接口命名为 `IRepository`，并希望将其创建在新的文件 `IRepository.cs` 中。接下来，你可以在这里选择用于构成接口的公共成员。我让所有成员保持选中状态，然后点击“确定”按钮。现在你可以看到 `SqlRepository` 类实现了这个泛型 `IRepository` 接口。让我们前往解决方案资源管理器，你可以在这里看到 `IRepository.cs` 文件。让我们打开这个 `.cs` 文件，直到你看到泛型 `IRepository` 接口。与泛型类一样，它在这里有一个泛型类型参数，并且还有一个针对该类型参数的类型约束。然后，该类型参数被用于这个接口中定义的方法。当你像这样定义类型约束时，意味着实现此接口的泛型类也必须为其泛型类型参数定义这些类型约束。让我在 `ListRepository` 类上实现该接口，以向你说明这一点。让我们展开这个类，然后在这里实现新的 `IRepository` 接口。

![](img/0155736aec718cf18821e9f10a5d308d_1115_0.png)

```csharp
public interface IRepository<T> where T : class, IEntity

{

    void Add(T item);

    T GetById(int id);

    void Remove(T item);

    void Save();

}
```

如你所见，`ListRepository` 类带有红色下划线。当我把鼠标悬停在它上面时，你会看到类型 `T` 必须是引用类型，才能用作泛型类型或方法 `IRepository` 中的参数 `T`。这意味着，在这个类中，我们现在也需要这个 `class` 类型约束，但这也许不太合理，因为这是 `ListRepository` 类的一个实现细节，而这个实现细节是不需要的。所以我们就保持这样。回到 `IRepository` 接口，让我们从这个接口中移除类约束。

```csharp
public class ListRepository<T> : IRepository<T> where T : IEntity
```

现在，当你回到 `ListRepository`，你可以看到这个类现在只需要 `IEntity` 约束就一切正常了。好的，现在这个接口已经在 `ListRepository` 和 `SqlRepository` 类上实现。接下来，让我们回到 `IRepository` 接口，因为我还想提一点。这里的接口上的 `IEntity` 类型约束也不是必须的，因为这个接口中没有任何实现需要该类型约束。所以，你可能会问，为什么接口上要有类型约束呢？接口通常是没有实现的。在 `IRepository` 接口上保留这个 `IEntity` 类型约束意味着，如果你将 `IRepository` 接口与一个不是 `IEntity` 类型的泛型类型参数一起使用，就会收到编译错误。我认为这对这个 `IRepository` 接口是有意义的，尤其是在我们有这个 `GetById()` 方法的情况下。这个方法只有对具有 `Id` 属性的 `IEntity` 实例才有意义。

```csharp
{

  public interface IRepository<T> where T : IEntity

  {

    void Add(T item);

    T GetById(int id);

    void Remove(T item);

    void Save();

  }

}
```

所以，让我们在这里保留这个 `IEntity` 约束，这使得 `IRepository` 接口只能用于实现了 `IEntity` 接口的类型。既然这个 `IRepository` 接口已经被 `ListRepository` 和 `SqlRepository` 类实现，你就可以在 `Program` 类中使用它了。让我们导航到 `Program.cs` 文件。在下面这里，我们有 `GetEmployeeById()` 方法，现在让我们把参数类型改为 `IRepository`。如你所见，这里的错误消失了。我们再把 `AddEmployees()` 方法的参数类型改为 `IRepository`，你会看到这里的错误也消失了。让我们向下滚动，也把 `AddOrganizations()` 方法的参数类型改为 `IRepository`。

![](img/0155736aec718cf18821e9f10a5d308d_1117_0.png)

现在我们引入了这个泛型接口，这意味着 `Program` 类中所有的静态方法都可以用于 SQL 仓库、列表仓库或任何其他 `IRepository` 实现。让我们运行应用程序，看看代码是否仍然正常工作。

```
Employee with Id 2: Anna
```

是的，你可以在这里看到 `Id` 为 2 的员工，也就是 Anna。这个员工是从 `SqlRepository`，也就是从数据库中读取的。

![](img/0155736aec718cf18821e9f10a5d308d_1118_0.png)

接下来，你会在这里看到来自 `ListRepository` 的两个组织。如你所见，所有员工都没有被打印到控制台，因为 `SqlRepository` 在其 `Save()` 方法中不会这么做。接下来，你将在 `IRepository` 接口中添加一个 `GetAll()` 方法，并在 `Program` 类中使用它来读取所有员工和所有组织，以便将它们写到控制台。之前，你已经创建了泛型 `IRepository` 接口。你可以调用它的 `GetById()` 方法来通过 `Id` 获取单个项。现在，你将在 `IRepository` 接口中添加一个返回所有项的 `GetAll()` 方法。如你所见，返回类型是 `IEnumerable`。`IEnumerable` 是 .NET 中来自 `System.Collections.Generic` 命名空间的一个现有泛型接口。你可以使用 `foreach` 循环遍历 `IEnumerable` 实例中的项。该接口由诸如 `List` 或 `Stack` 之类的泛型集合以及所有 C# 数组实现。所以你看，它是一个表示项序列的核心接口。此外，所有 LINQ 方法都是这个泛型接口的扩展方法，这意味着你可以对 `IEnumerable` 实例运行 C# 查询。

现在，在本演示中，你将学习如何在我们的项目的 `Repository` 类中添加和实现 `GetAll()` 方法，并学习如何使用 .NET 现有的 `IEnumerable` 接口。这里，在 `.StorageApp` 项目中，让我们打开 `IRepository` 接口。首先，让我选中 `Add()` 方法，剪切它，然后粘贴到 `GetById()` 方法下面。方法的顺序并不重要，但我喜欢这样排列，因为 `GetById()` 是从仓库读取数据的方法，而 `Add()` 和 `Remove()` 是向仓库写入数据的方法。

```csharp
{

    public interface IRepository<T> where T : IEntity

    {

        IEnumerable< GetAll();

        T GetById(int id);

        void Add(T item);

        void Remove(T item);

        void Save();

    }

}
```

现在，让我们在这里添加一个 `GetAll()` 方法，并设置返回类型为 `IEnumerable`。我按 `Ctrl+dot` 来为包含该 `IEnumerable` 接口的 `System.Collections.Generic` 命名空间添加 `using` 指令。现在，我们有了这个新的 `GetAll()` 方法，可以用来从仓库获取所有项。因为你在 `ListRepository` 和 `SqlRepository` 中都实现了这个接口，所以你现在需要在所有这些实现中添加这个 `GetAll()` 方法。让我们从 `ListRepository` 开始。如你所见，这里的接口被标红了。当你将鼠标悬停在它上面时，你会看到“`ListRepository`”未实现接口成员“`IRepository.GetAll()`”。让我们将光标放在接口上，按 `Ctrl+dot`，然后在这里你可以选择“实现接口”选项。这个选项会将缺失的 `GetAll()` 方法添加到 `ListRepository` 类中。你可以在底部看到它。

```csharp
{

    public class ListRepository<T> : IRepository<T> where T : IEntity

    {

        private readonly List<T> _items = new();

        public IEnumerable<T> GetAll()

        {

            return _items;

        }

        public T GetById(int id)

        {

            return _items.Single(item => item.Id == id);

        }

        public void Add(T item)

        {

            item.Id = _items.Count + 1;

            _items.Add(item);

        }

    }

}
```

我把它从这里剪切出来，然后粘贴到这个类的顶部。现在，从这个方法中，你可以返回存储在 `items` 字段中的列表，因为这个列表实现了 `IEnumerable` 接口。但是直接返回列表意味着仓库的使用者可以访问这个内部存储。与其直接返回列表，不如返回一个副本。你可以通过调用 `ToList()` 方法来实现这一点，这是来自 `System.Linq` 命名空间的一个扩展方法，我已经在这里包含了它。现在，让我们只复制这个 `GetAll()` 方法，然后转到解决方案资源管理器，打开 `SqlRepository` 类。在这个类中，我直接粘贴这个方法。在这种情况下，你没有 `items` 字段。相反，你会在这里使用 `dbSet`。我将光标放在 `ToList()` 方法上，按 `Ctrl+dot` 为 `System.Linq` 添加 `using` 指令。我还将光标放在 `IEnumerable` 接口上，按 `Ctrl+dot` 为 `System.Collections.Generic` 命名空间添加 `using` 指令。

```csharp
public class SqlRepository<T> : IRepository<T> where T : class, IEntity

{

    private readonly DbContext _dbContext;

    private readonly DbSet<T> _dbSet;

    public SqlRepository(DbContext dbContext)

    {

        _dbContext = dbContext;

        _dbSet = _dbContext.Set<T>();

    }

    public IEnumerable<T> GetAll()

    {

        return _dbSet.ToList();

    }

    public T GetById(int id)

    {

        return _dbSet.Find(id);

    }
```

