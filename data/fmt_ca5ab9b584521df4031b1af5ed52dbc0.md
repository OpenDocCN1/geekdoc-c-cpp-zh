
到此为止是关于 `class` 约束的内容。在下一章，你将学习关于允许你调用无参构造函数的新的约束。

## 第 8 章 如何使用 `new()` 约束

在本演示中，你将学习如何使用 `new()` 约束来调用你的泛型类型参数的无参构造函数。这里，我打开了 `GenericRepository` 类。让我们在这个 `GenericRepository` 类中创建一个我称之为 `CreateItem` 的方法，并从该方法返回类型 `T` 的新实例。正如你所见，这行代码被红色下划线标出。当你悬停其上时，你可以看到这里的错误，无法创建变量类型 `"T"` 的实例，因为它没有 `new()` 约束。

![](img/0155736aec718cf18821e9f10a5d308d_1098_0.png)

要调用构造函数，你必须确保类型 `T` 实际上有一个无参构造函数。为了确保这一点，你将添加 `new()` 约束。此约束必须是最后定义的约束。顺序与 C# 中的正常继承方式相同。你在这里定义类名如 `EntityBase`，或者使用关键字 `class` 或 `struct`。然后你定义泛型类型参数所需的所有接口，最后，如果你需要通过调用无参构造函数来创建类型 `T` 的实例，你可以定义 `new()` 约束。现在有了这个 `new()` 约束和这个 `CreateItem` 方法，这意味着现在在 `Program.cs` 文件中那个 `GenericRepository` 你现在有了这个 `CreateItem` 方法，它返回新的 employee 实例。

![](img/0155736aec718cf18821e9f10a5d308d_1099_0.png)

现在让我们看看当你为 `Employee` 类添加一个带参数的构造函数时会发生什么。所以让我们打开这里的 `Employee` 类，并在这里使用 `ctor` 片段创建一个构造函数。我按两次 Tab 键，并为该构造函数添加 `firstName` 参数。现在让我们回到 `Program.cs` 文件。正如你所见，`Employee` 被红色下划线标出。当你悬停其上时，你可以看到错误，employee 必须是一个具有公共无参构造函数的类型，才能将其用作泛型类型或方法 `GenericRepository` 中的参数 `"T"`。

```csharp
static void Main(string[] args)
{
    var employeeRepository = new GenericRepository<Employee>();
    AddEmployees(employeeRepository);
    GetEmployeeById(employeeRepository);
    var organizationRepository = new GenericRepository<Organization>();
    AddOrganizations(organizationRepository);
    Console.ReadLine();
}

private static void GetEmployeeById(GenericRepository<Employee> employeeRepository)
{
    var employee = employeeRepository.GetById(2);
    Console.WriteLine($"Employee with Id 2: {employee.FirstName}");
}
```

当你回到 `GenericRepository` 类，并移除这里的 `new()` 约束时，这意味着你无法实现这里的 `CreateItem` 方法，因为不存在无参构造函数，所以让我们移除它，现在让我们回到 `Program.cs` 文件，现在你可以看到一切又正常了，即使 `Employee` 类中有那个构造函数。让我们在这里移除这个空行，并再次从 `Employee` 类中移除构造函数；我们不需要它。现在让我们回到 `GenericRepository` 类，让我再展示你一件事。当你有多个类型参数时，让我们在这里添加另一个名为 `TKey` 的参数，然后你可以为不同的类型参数定义多个 `where`。

```csharp
public class Employee : EntityBase
{
    public string? FirstName { get; set; }
    public override string ToString() => $"Id: {Id}, FirstName: {FirstName}";
}
```

所以在这里，我可以例如说 `TKey` 需要是一个 `struct`。你甚至可以做更高级的事情。你可以例如说 `TKey` 需要是 `T` 的子类型。你看，你可以围绕这些泛型类型约束进行操作，以确保传递给你的类的泛型类型参数具有你需要的形状。

```csharp
public class GenericRepository<T, TKey>
    where T : class, IEntity
    where TKey : T
{
    private readonly List<T> _items = new();
    public T GetById(int id)
    {
        return _items.Single(item => item.Id == id);
    }
    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }
    public void Remove(T item)
    {
```

在我们的情况下，你只需要确保 `T` 是 `IEntity` 类型，因为我们在类中需要 `Id` 属性。所以让我们在这里移除其余部分，并同时移除第二个泛型类型参数。现在让我们运行应用程序并看看一切是否仍然正常工作。我们这里有三个员工，我们这里是否有 `Id` 为 2 的员工，然后我们这里有两家组织。现在让我们总结一下你在本章中学到的内容。你在本章中学到如何实现泛型类。我向你展示了如何从泛型类继承一个类，你还学习了如何从泛型类继承一个泛型类。你还学习了如何在泛型类上使用多个类型参数。之后，我向你展示了如何为泛型类添加泛型类型约束。类型约束允许你确保泛型类型参数具有特定的形状。你学习了如何确保类型参数具有具体类的类型，在本章中就是具有 `Id` 属性的 `EntityBase` 类。你还学习了如何使用 `class` 和 `struct` 约束来确保类型参数是引用类型或值类型。我还向你展示了如何使用 `new` 约束调用泛型类型参数的构造函数。除此之外，你还了解了 `default` 关键字，它允许你用默认值初始化 `T` 类型的变量。对于引用类型，默认值是 `null`；对于数值类型，默认值例如是 0。现在你知道如何实现泛型类了。在下一章中，你将继续处理一个公司的控制台应用程序。你将实现另一个泛型仓库，它不是将员工和组织放在列表中，而是放在数据库中。为了使我们的控制台应用程序的现有代码也能与该新的泛型仓库类一起使用，你将学习如何使用泛型接口。

## 第 9 章 如何使用泛型接口

在本章中，你将学习如何通过使用泛型接口来编写松散耦合的代码。首先，我会确保你理解为什么要使用泛型接口。在你知道这一点之后，你将学习如何创建泛型接口，以及如何使用泛型接口。在本章中，我还会确保你理解什么是协变，以及在使用泛型接口时它如何帮助你。我也会确保你理解什么是逆变。最后，你将学习在使用泛型接口时如何处理接口继承。现在，让我们确保你理解为什么要使用泛型接口。之前，你创建了 `StorageApp`，这是一个 .NET 控制台应用程序。在此应用程序中，你创建了 `GenericRepository` 类，它将员工和组织存储在 `List` 中。在本章中，你将继续处理这个 .NET 应用程序。你要做的第一件事是将 `GenericRepository` 类重命名为 `ListRepository`，以使它的作用更明显。然后，你将实现另一个泛型类，名为 `SqlRepository`。在这个类中，你将使用 Entity Framework Core 将项目存储在数据库中。但我不希望你在本书中必须设置数据库。这就是为什么你将使用带内存提供程序的 Entity Framework Core 数据库。该数据提供程序仅用于测试，因为它缺乏真实的数据库功能，例如引用完整性。但因为它设置非常简单，并且也足以满足我们的需求，所以我们将使用它。需要知道的重要一点是，你在 `SqlRepository` 类中编写的代码与你在访问真实数据库（如 SQLite 或 SQL Server）时编写的代码完全相同。所以现在你会看到我们有两个不同的仓库实现，但是当你查看我们的 .NET 控制台应用程序的 `Program` 类时，你会看到像 `AddEmployees` 和 `GetEmployeeById` 这样的方法。这些方法有一个 `ListRepository` 参数。这意味着你不能将 `SqlRepository` 实例传递给这些方法。但是作为开发人员，公司希望你让 `Program` 类中的这些方法同时适用于列表仓库和 SQL 仓库。为了实现这一点，你将引入泛型 `IRepository` 接口，该接口将由 `ListRepository` 类和 `SqlRepository` 类实现。引入此接口后，你可以将 `Program` 类中方法的参数类型从 `ListRepository` 改为 `IRepository`。这意味着这些方法将适用于任何 `IRepository` 实现，例如 `ListRepository` 或 `SqlRepository`。因此，这些方法现在依赖于泛型 `IRepository` 接口，这是一种抽象，而不依赖于具体实现。这实际上是我们在软件开发中使用的一个原则，称为依赖倒置原则。它指出，像 `Program` 类中的静态方法这样的组件必须依赖抽象，而不是依赖实现。而这正是我们所做的。`Program` 类中的方法依赖于 `IRepository` 接口，这是一种抽象。现在让我们来实现它。在你创建这个 `IRepository` 接口之前，你将构建泛型 `SqlRepository` 类。在此演示中，你将学习如何构建泛型 `SqlRepository` 类。在这个类中，你将使用 Entity Framework Core，并将数据存储在数据库中。这里，我已经打开了你之前创建的 `StorageApp` 项目。让我们在这里选择 `GenericRepository.cs` 文件，并将该文件重命名为 `ListRepository`。我按下 Enter，Visual Studio 在这里询问我是否还要重命名代码元素 `GenericRepository`。是的，我要这样做。

```csharp
namespace WiredBrainCoffee.StorageApp.Repositories
{
    public class ListRepository<T> where T : IEntity
    {
        private readonly List<T> _items = new();
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

现在你可以在这里看到，该类也已更名为 `ListRepository`。现在在 C# 文件中，让我们折叠这个类。让我们选中它。我按下 Ctrl+C 复制它，然后再次粘贴到这个文件中。现在让我们向上滚动，并将新类命名为 `SqlRepository` 而不是 `ListRepository`。现在，我按下 Ctrl+.，你会看到 Visual Studio 建议在此处将类型移动到 `SqlRepository.cs` 文件。让我们按 Enter 执行此操作。让我们回到解决方案资源管理器，现在你会看到这个新的 `SqlRepository.cs` 文件，其中包含 `SqlRepository` 类。

```csharp
public class ListRepository<T> ...

public class SqlRepository<T> where T : IEntity
{
    private readonly List<T> _items = new();
    public T GetById(int id)
    {
        return _items.Single(item => item.Id == id);
    }
    public void Add(T item)
    {
        item.Id = _items.Count + 1;
        _items.Add(item);
    }
    public void Remove(T item)
    {
```

这里找不到 `Single` 方法，因为缺少 `System.Linq` 命名空间。让我们将光标放在此方法上，然后按 Ctrl+. 为 `System.Linq` 添加 `using`。与将项目存储在此处的 `List` 中不同，你应该使用 Entity Framework Core 将它们存储到数据库中。这意味着你必须设置一个 Entity Framework `DbContext`。让我们在我们的项目中执行此操作。我右键单击项目，然后从上下文菜单中选择“添加”->“新建文件夹”。让我们将新文件夹命名为 `Data`。现在我右键单击此文件夹，然后从上下文菜单中选择“添加”->“类”。让我们将这个类命名为 `StorageAppDbContext`。这将是我们 Entity Framework Core 的 `DbContext`。让我们将它添加到 `Data` 文件夹中。现在我们需要 Entity Framework Core，所以让我们右键单击“依赖项”，然后在这里选择“管理 NuGet 包”。

![](img/0155736aec718cf18821e9f10a5d308d_1107_0.png)

正如你所看到的，我已经在这里选择了“浏览”，所以让我们在这里搜索 `EntityFrameworkCore.InMemory`，并在这里选择 `Microsoft.EntityFrameworkCore.InMemory` NuGet 包，然后点击“安装”按钮。包含更改的预览会出现，我在此对话框中点击“确定”，并且我也在此处接受许可。这个 `EntityFrameworkCore.InMemory` NuGet 包已安装，所以让我们关闭此选项卡。你也可以通过在解决方案资源管理器中右键单击项目来打开 `cs.proj` 文件，然后你会看到包引用，你也可以手动在 `cs.proj` 文件中添加。现在让我们关闭 `cs.proj` 文件。

![](img/0155736aec718cf18821e9f10a5d308d_1107_1.png)

让 `StorageAppDbContext` 类继承自 `DbContext`。我按 Esc 关闭 IntelliSense，并按 Ctrl+. 为 `Microsoft.EntityFrameworkCore` 添加 `using`。现在，我们还要把这个类设为公共类，并让光标停留在这里的 `using` 语句上，然后按 Ctrl+. 删除不必要的 `using`。现在，在这个类中，我们需要一个 `Employees` 属性。在 Entity Framework Core 中，这是一个 `DbSet`。如你所见，这是一个泛型类，它接受实体类型作为泛型类型参数。所以让我们在这里创建一个 `DbSet`。我按 Ctrl+. 为包含 `Employee` 类的 `Entities` 命名空间添加 `using`。现在，让我们把这个属性命名为 `Employees`。如你所见，它带有绿色下划线，因为我们在 `.csproj` 文件中启用了可空引用类型。当你将鼠标悬停在它上面时，你会看到警告：属性 `Employees` 在退出构造函数时必须包含一个值。请考虑将该属性声明为可空。所以你可以在这里用问号将该属性声明为可空，然后警告就会消失。但在 `DbContext` 上，`DbSet` 属性通常不为 `null`，因为它是在 `DbContext` 基类的构造函数中初始化的。

![](img/0155736aec718cf18821e9f10a5d308d_1108_0.png)

与其在这里使用问号，你可以换一种做法。你可以在这里使用表达式主体，并使用 `DbContext` 基类中定义的泛型 `Set` 方法；你会看到这个方法返回一个 `TEntity` 的 `DbSet`。要使用这个泛型 `Set` 方法，你必须传入一个泛型类型参数。在这种情况下，让我们传入 `Employee` 类型，然后这个 `Set` 方法就会返回一个 `DbSet`，正是这个属性所需要的。

![](img/0155736aec718cf18821e9f10a5d308d_1109_0.png)

我复制这个 `DbSet` 属性，并为 organizations 也创建一个。所以这里我们把属性命名为 `Organizations`，并让这个泛型 `Set` 方法使用 `Organization` 类型。除了这两个属性之外，我们还要在这里重写 `OnConfiguring` 方法。在 `optionsBuilder` 上，你会找到一个名为 `UseInMemoryDatabase` 的扩展方法。你必须用这个方法指定数据库名称。我们把这个数据库命名为 `StorageAppDb`。现在，这个 Entity Framework `DbContext` 已经设置好了，你可以实现 `SqlRepository` 类了，所以让我们打开这个类。首先，让我移除这里的 `_items` 字段，因为我们不需要那个列表。

```csharp
public class StorageAppDbContext : DbContext
{
    public DbSet<Employee> Employees => Set<Employee>();
    public DbSet<Organization> Organizations => Set<Organization>();
```
