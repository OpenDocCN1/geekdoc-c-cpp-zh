
现在，你也已经在 `SqlRepository` 类中实现了 `IRepository<T>` 接口的这个 `GetAll` 方法。现在，让我们在应用程序中使用这个 `GetAll` 方法。让我们打开 `Program.cs` 文件。在调用 `GetEmployeeById` 方法之后，让我们调用一个新方法，名为 `WriteAllToConsole`。作为参数，让我们传入 `employeeRepository`。我按 `Ctrl+dot` 在 `Program` 类中生成这个方法。让我们将参数类型从 `SqlRepository` 改为 `IRepository`，以便它也可以与 `ListRepository<Employee>` 一起使用。现在，在这个方法中，让我们从仓库中获取所有员工。

```csharp
static void Main(string[] args)
{
    var employeeRepository = new SqlRepository<Employee>(new StorageAppDbContext());
    AddEmployees(employeeRepository);
    GetEmployeeById(employeeRepository);
    WriteAllToConsole(employeeRepository);
    var organizationRepository = new ListRepository<Organization>();
    AddOrganizations(organizationRepository);
    Console.ReadLine();
}

private static void WriteAllToConsole(SqlRepository<Employee> employeeRepository)
{
    throw new NotImplementedException();
}

private static void GetEmployeeById(IRepository<Employee> employeeRepository)
{
```

所以，让我们在这里创建一个 `items` 变量，并在 `employeeRepository` 上调用 `GetAll` 方法。你可以看到，它返回一个 `IEnumerable<Employee>`。现在，你已经在 `items` 变量中有了这个 `IEnumerable<Employee>` 实例，你可以创建一个 `foreach` 循环来遍历这些项。我按两次 `Tab` 键来插入 `foreach` 代码片段，然后写 `foreach item in items`。在 `foreach` 循环内部，让我们创建一条 `Console.WriteLine` 语句，并将该项写到控制台。

```csharp
var employeeRepository = new SqlRepository<Employee>(new StorageAppDbContext());
AddEmployees(employeeRepository);
GetEmployeeById(employeeRepository);
WriteAllToConsole(employeeRepository);
var organizationRepository = new ListRepository<Organization>();
AddOrganizations(organizationRepository);
Console.ReadLine();
}

private static void WriteAllToConsole(IRepository<Employee> employeeRepository)
{
    var items = employeeRepository.GetAll();
    foreach (var item in items)
    {
        Console.WriteLine(item);
    }
}
```

这意味着现在，在我们通过 Id 打印出一个 `Employee` 之后，你应该能在控制台看到所有员工被写入。让我们实际看看，并运行应用程序。这里，你可以看到 Id 为 2 的 `Employee`，她是 Anna，然后你会看到使用 `GetAll` 方法从 `SqlRepository` 获取到的所有员工。

```
Employee with Id 2: Anna
Id: 1, FirstName: Julia
Id: 2, FirstName: Anna
Id: 3, FirstName: Thomas
```

在下一章，让我向你展示你也可以对组织使用 `WriteAllToConsole` 方法。

## 第 11 章 协变基础

在本演示中，我会确保你理解协变，在创建泛型接口时知道这一点很重要。这里，我打开了 `StorageApp` 的 `Program.cs` 文件。之前，我们创建了这个 `WriteAllToConsole` 方法，它有一个 `Employee` 的 `IRepository` 参数。它在仓库上调用 `GetAll` 方法，并将所有项写入控制台。

```
AddEmployees(employeeRepository);
GetEmployeeById(employeeRepository);
WriteAllToConsole(employeeRepository);
var organizationRepository = new ListRepository<Organization>();
AddOrganizations(organizationRepository);
Console.ReadLine();
}
private static void WriteAllToConsole(IRepository<Employee> employeeRepository)
{
    var items = employeeRepository.GetAll();
    foreach (var item in items)
    {
        Console.WriteLine(item);
    }
}
```

现在，假设你也想用这个方法处理组织。所以在这里，在向 `ListRepository` 添加组织之后，让我们用 `organizationRepository` 调用这个 `WriteAllToConsole` 方法。参数用红色下划线标出。当你悬停时，你可以看到错误 `cannot convert from ListRepository of Organization to IRepository of Employee`。但正如你所知，`Organization` 类和 `Employee` 类都实现了 `IEntity` 接口。所以与其在这里接收 `IRepository of Employee`，你可以接收这里一个 `IRepository of IEntity`，这样它就能同时适用于员工和组织。让我们把参数命名为 `repository`。我按 `Ctrl+点` 将其从 `employeeRepository` 重命名为 `repository`。

![](img/0155736aec718cf18821e9f10a5d308d_1125_0.png)

但现在，你会看到这个方法既不能用于 `employeeRepository`，也不能用于 `organizationRepository`。其原因是接口的参数默认是不变的。这意味着它们必须与实现接口的类上使用的类型完全相同。这到底是什么意思？这意味着，如果你有一个 `IRepository<Organization>` 变量，我们就叫它 `repo`，并为其分配 `ListRepository<Organization>`，你会看到在接口上使用的类型参数与类上完全相同。这当然是可行的，因为 `ListRepository<Organization>` 是一个 `IRepository<Organization>`。但这个泛型 `IRepository` 接口的泛型类型参数默认是不变的。

```
IRepository<Organization> repo = new ListRepository<Organization>();
Console.ReadLine();
}
```

这意味着，在接口上，你不能使用像 `IEntity` 接口这样更不具体的泛型类型参数。当你指定它时，你可以看到 `ListRepository` 类被红色下划线标出。当你悬停时，你可以看到，`Cannot implicitly convert type ListRepository of Organization to IRepository of IEntity`。但实际上，当你看这个 `repo` 变量时，让 `GetAll` 方法返回一个 `IEnumerable of IEntity` 是可以的，因为实现返回的是更具体的类型。所以你仍然可以将 `IEntities` 转换为 `organizations`。对于 `GetById` 方法，返回这种更不具体的类型也是可以的。但对于传入项的方法来说，不可以传入一个 `IEntity`，因为 `ListRepository` 实际上需要一个 `Organization`。这意味着，对于从仓库读取的方法，你可以使用更不具体的类型，而这就是协变所关心的。

```
IRepository<IEntity> repo = new ListRepository<Organization>();
repo.
Add
Equals
GetAll
GetById
GetHashCode
GetType
private
{
var i
forea
{
void IRepository<IEntity> Add(IEntity item)
WriteAllToConsole(IRepository<IEntity> repository)
ory.GetAll();
n items)
```

所以让我们暂时保留这一行，然后转到 `IRepository` 接口。如你所见，这里我们有两个返回类型 `T` 的方法，我们可以在这里使用更不具体的类型。但对于 `Add` 和 `Remove` 方法，它们接收类型 `T` 作为输入，你不能使用更不具体的类型。如我所说，默认情况下，泛型类型参数是不变的。你可以通过在泛型类型参数前使用 `out` 关键字将其定义为协变的。如你所见，使用 `out` 关键字将泛型类型参数定义为协变对于类型流出、即被返回的方法是可以的，但对于类型流入的方法是不可以的。当你悬停在这里的 `T` 时，错误提示 `Invalid variance: The type parameter 'T' must be contravariantly valid on 'IRepository.Add(T).' 'T' is covariant.`

```
public interface IRepository<T> where T : IEntity
{
    IEnumerable<T> GetAll();
    T GetById(int id);
    void Add(T item);
    void Remove(T item);
    void Save();
}
```

这意味着，换句话说，你不能在该接口上使用 `out` 关键字将泛型类型参数定义为协变，但你可以定义一个单独的接口，只包含这两个返回类型 `T` 的方法。让我们直接在这个文件中做。我在这里创建一个 `public` 接口，我称它为 `IReadRepository`，然后我把这里的两个方法 `GetAll` 和 `GetById` 剪切下来，粘贴到这个新接口中。现在，让 `IRepository` 接口继承自这个 `IReadRepository` 接口 `of T`，这样这个接口也拥有 `GetAll` 和 `GetById` 方法。现在，让我们回到 `Program.cs` 文件。到目前为止，什么都没有改变。但我可以在这里使用，例如，这个 `IReadRepository`，但我们仍然有同样的错误，因为这个接口的类型参数也是不变的。现在，让我们更改它。

![](img/0155736aec718cf18821e9f10a5d308d_1128_0.png)

让我们转到 `IRepository` C# 文件，现在让我们在这个接口上为类型参数添加 `out` 关键字。这现在使类型参数变为协变，这意味着可以使用更不具体的类型。当你回到 `Program.cs` 文件时，你会看到，现在这一行不再有错误了。

![](img/0155736aec718cf18821e9f10a5d308d_1128_1.png)

将 `ListRepository of Organization` 分配给 `IReadRepository of IEntity` 是可以的。由于这个 `IReadRepository` 接口上没有泛型类型约束，你甚至可以在这里说类型是 `object`，这样也同样可行。这意味着，现在，让我们删除这一行。你可以在这个 `WriteAllToConsole` 方法中使用 `IReadRepository` 接口，现在你会看到，这里的错误消失了，你可以传入任何 `IReadRepository of IEntity` 的实现。

```
AddEmployees(employeeRepository);
GetEmployeeById(employeeRepository);
WriteAllToConsole(employeeRepository);
var organizationRepository = new ListRepository<Organization>();
AddOrganizations(organizationRepository);
WriteAllToConsole(organizationRepository);
Console.ReadLine();
}
private static void WriteAllToConsole(IReadRepository<IEntity> repository)
{
var items = repository.GetAll();
foreach (var item in items)
{
Console.WriteLine(item);
}
```

现在，让我们运行应用程序，你应该能看到所有员工被打印到控制台，以及所有组织。让我们再次停止应用程序，并调整 `ListRepository` 类。让我们打开这个类，并向下滚动到 `safe` 方法，并删除这里写入控制台的 `for each` 循环。我在这里添加一个注释，`Everything is saved already in the list of T`。好的，所以在这个 `safe` 方法中不需要做任何事情。

```csharp
public void Remove(T item)
{
    _items.Remove(item);
}
public void Save()
{
    // Everything is saved already in the List<T>
}
}
```

现在，我们只需要查看 `Program` 类的 `WriteAllToConsole` 方法的输出。你会看到所有的员工，这里你会看到所有的组织。现在你学习了协变，它允许你为泛型接口使用一个不太具体的泛型类型参数。在下一章，你将学习关于逆变。

## 第 12 章 逆变基础

在本演示中，我会确保你理解逆变。这里在 `StorageApp` 项目中，让我们打开 `Employee` 类，并从该类创建一个名为 `Manager` 的子类。所以我让它继承自 `Employee`。在这个子类中，让我们重写 `ToString` 方法。我在这里也使用表达式体，并调用基类的 `ToString` 方法，也就是这里 `Employee` 类的那个，然后我只是给这个 `ToString` 结果加上 `Manager` 后缀。

```
public class Employee : EntityBase
{
    public string? FirstName { get; set; }
    public override string ToString() => $"Id: {Id}, FirstName: {FirstName}";
}
public class Manager : Employee
{
    public override string ToString() => base.ToString() + " (Manager)";
}
```

现在，我们有一个更具体的类继承自 `Employee`。让我们把光标放在 `Manager` 类名上，我按 `Ctrl + .` 将此类型移动到 `Manager` C# 文件。让我们按 `Enter`。现在让我们回到解决方案资源管理器。这里，你可以看到新的 `Manager` C# 文件。现在让我们打开 `Program.cs` 文件。在 `Main` 方法中，在调用 `AddEmployees` 方法之后，让我们调用一个名为 `AddManagers` 的新方法。我传入 `employeeRepository` 作为参数。现在你可以再次按 `Ctrl + .` 在 `Program` 类中生成这个 `AddManagers` 方法。这里，你可以看到它。首先，让我把参数类型从 `SqlRepository` 改为 `IRepository`，这样这个方法也能与 `Employee` 的列表存储库一起工作。现在，在这个方法中，让我们向存储库添加两个经理。所以让我们调用 `Add` 方法，并在这里传入一个 `first name` 为 `Sara` 的经理。我按 `Ctrl + C` 复制这一行，然后再次粘贴。

![](img/0155736aec718cf18821e9f10a5d308d_1132_0.png)

```csharp
private static void AddManagers(SqlRepository<Employee> employeeRepository)
{
    throw new NotImplementedException();
}
```
