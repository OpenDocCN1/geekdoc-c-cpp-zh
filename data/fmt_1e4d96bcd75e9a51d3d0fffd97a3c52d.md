
正如你所见，它用红色下划线标出，当你悬停时，你会看到这里的错误，类型`T`不能用作泛型类型或方法`IRepository`中的类型参数`T`。从`T`到`IEntity`没有转换。这是因为在`IRepository`中，`T`必须是`IEntity`，所以你也必须在这里添加这个类型约束`where T`是`IEntity`。现在，你当然也可以做的是在子接口上定义其他类型参数。所以在这里，我可以例如在这个接口中创建一个`Key`属性，其类型为`TKey`。但你也可以做的是，你也可以让一个接口继承自一个泛型接口。所以让我们在这里移除类型约束，并假设你想要继承自`IRepository`。

![](img/0155736aec718cf18821e9f10a5d308d_1141_0.png)

然后接口可能命名为`IEmployeeRepository`。所以你可以看到，你可以让泛型接口继承自泛型接口，你也可以让接口继承自泛型接口。当然，你也可以让泛型接口继承自接口。当你例如查看`IEnumerable`接口时，你会看到这一点。让我们打开这个接口，并从上下文菜单中选择“转到定义”。正如你所见，这个泛型接口有一个协变类型参数，并继承自`IEnumerable`接口。现在让我们再次关闭它。

```csharp
public interface IRepository<T> : IReadRepository<T>, IWriteRepository<T>
    where T : IEntity
{
}

public interface IEmployeeRepository : IRepository<Employee>
{
}
```

相同的概念也适用于类。所以让我们在这里将接口更改为实现泛型`IRepository`接口的`EmployeeRepository`类。当你把光标放在这个`IRepository`接口上时，你可以按`Ctrl+.`，Visual Studio 会在这里建议你实现接口。让我们这样做。现在你可以看到你在这里有一个接受`Employee`的`Add`方法，一个返回`IEnumerable`的`GetAll`方法，等等。现在让我再次从这个`Employee`仓库类中移除成员。

```csharp
namespace System.Collections.Generic
{
    public interface IEnumerable<out T> : IEnumerable
    {
        IEnumerator<T> GetEnumerator();
    }
}
```

让我们删除它们，现在类又是空的。与其在类上实现接口，你也可以创建一个`GenericSuperRepository`类。让我们在这里添加一个类型参数，并继承自`IRepository`。你再次需要泛型类型约束。现在再次在这里，你可以把光标放在接口上，我按`Ctrl+.`来实现接口，你现在可以看到这里有一个带有`T`参数的`Add`方法，一个返回`IEnumerable`的`GetAll`方法，等等。

```csharp
public class EmployeeRepository : IRepository<Employee>
{
    public void Add(Employee item)
    {
        throw new System.NotImplementedException();
    }

    public IEnumerable<Employee> GetAll()
    {
        throw new System.NotImplementedException();
    }

    public Employee GetById(int id)
    {
        throw new System.NotImplementedException();
    }

    public void Remove(Employee item)
    {
        throw new System.NotImplementedException();
    }
}
```

你也可以在这里在泛型类上定义多个类型参数，如果你需要的话，然后你只需将`IRepository`接口所需的那一个传递给该接口。现在让我们再次删除这个类。

![](img/0155736aec718cf18821e9f10a5d308d_1144_0.png)

到此为止，我们已经介绍了泛型接口的继承。现在让我们总结一下本章所学的内容。在本章中，你学习了如何创建和使用泛型接口，使应用程序中的代码既能处理列表仓库，也能处理 SQL 仓库。你还学习了泛型接口的泛型类型参数默认是不变的。然后，你学习了如何在泛型接口上将泛型类型参数声明为协变。方法是在类型参数前加上 `out` 关键字。只有当 `T` 在泛型接口中仅用于方法和属性的返回值时，这才有效。协变允许你在使用泛型接口时使用更不具体的泛型类型实参。你还学习了如何将泛型类型参数声明为逆变。方法是在类型参数前加上 `in` 关键字。只有当 `T` 在接口中仅用于输入参数时，这才有效。逆变允许你在使用泛型接口时使用更具体的泛型类型实参。你还学习了如何处理接口继承。你可以从泛型接口继承其他泛型接口，也可以在泛型类和非泛型类上实现泛型接口。现在你知道了如何使用泛型接口。在下一章中，你将继续开发一个公司的 .NET 控制台应用程序，并学习如何创建泛型方法和泛型委托。

## 第 14 章 如何创建泛型方法和泛型委托

在本章中，你将学习如何通过将方法和委托设为泛型来使它们可复用。首先，你将学习如何使用泛型方法。你会从一个普通方法开始，然后创建一个泛型方法，使其可用于不同的类型。最后，你将为泛型接口构建一个泛型扩展方法。在本章的第二部分，你将学习如何使用泛型委托。你会从一个委托开始，然后创建一个泛型委托，使其可用于不同的类型。你还将学习如何使用 .NET 中的泛型 `Action` 委托，并且会学习如何使用 .NET 中的泛型 `EventHandler` 委托来创建事件。现在让我们开始吧，为我们的 .NET 控制台应用程序添加一个方法。在本演示中，让我们为控制台应用程序添加一个提供新功能的方法。这里我打开了之前创建的 `StorageApp`。

![](img/0155736aec718cf18821e9f10a5d308d_1146_0.png)

现在让我们打开`Program.cs`文件，并向下滚动到这个文件中的`AddOrganizations`方法。在该方法中，你为每个组织调用仓库的`Add`方法。现在假设你还希望能够将组织的数组添加到仓库中。那么，我们在这里创建一个新变量，命名为`organizations`，并用一个新数组初始化它。现在让我们把这两个组织移入这个`organizations`数组，并移除这里对`Add`方法的调用。现在，为了将该数组中的组织添加到仓库中，让我们创建一个新方法，我把它命名为`AddBatch`。作为第一个参数，我们把`organizationRepository`传给这个方法；作为第二个参数，传入`organizations`数组。我按下`Ctrl+.`在`Program`类中生成`AddBatch`方法。

![](img/0155736aec718cf18821e9f10a5d308d_1147_0.png)

在该方法中，我们创建一个`foreach`循环。假设对于这个`organizations`数组中的每一项，你都想在`organizationRepository`上调用`Add`方法来添加该项。之后，你应该像我们在这里所做的那样，在仓库上调用`Save`方法。那么，让我们把这条包含`Save`方法调用的语句剪切掉。我按下`Ctrl+X`，然后把它粘贴到`AddBatch`方法中。

![](img/0155736aec718cf18821e9f10a5d308d_1147_1.png)

现在，这个`AddBatch`方法允许你将组织的数组添加到仓库中。其内部会为每个组织调用`Add`方法。现在让我们运行`StorageApp`，看看它是否仍然有效。在本演示中，你将学习如何创建泛型方法。之前，你创建了这个`AddBatch`方法，用于将组织的数组添加到组织仓库中。现在让我们也把这个方法用于员工。那么，让我们向上滚动，你会在这里看到`AddEmployees`方法。首先，让我们也创建一个`employees`变量，并用一个新数组初始化它。我把光标放在`employeeRepository`之前，然后按住`Shift`键，同时按下`Alt`键。这样可以选中包含`Add`方法的所有三行，然后你可以按删除键。现在让我们剪切这三个 employee 对象，然后粘贴到数组中。最后，我需要删除分号和括号，并添加逗号。让我们添加一个分号，并稍微缩进一下，现在看起来不错了。

```csharp
private static void AddEmployees(IRepository<Employee> employeeRepository)
{
    var employees = new[]
    {
        new Employee { FirstName = "Julia" },
        new Employee { FirstName = "Anna" },
        new Employee { FirstName = "Thomas" }
    };

    employeeRepository.Save();
}
```

现在，让我们移除这里对`Save`方法的调用。取而代之，让我们用`employeeRepository`和我们的`employees`数组来调用`AddBatch`方法。正如你所看到的，这当然不行。当你将鼠标悬停在其上时，会看到：无法从`IRepository<Employee>`转换为`IRepository<Organization>`。那么，让我们向下滚动到`AddBatch`方法。现在，你可能会想，或许可以在这里使用`IEntity`接口，因为`Organization`类和`Employee`类都实现了这个接口。但正如你所看到的，这里的`organizationRepository`带有红色下划线。当你悬停它时，会看到这个错误：无法从`IRepository<Organization>`转换为`IRepository<IEntity>`。这个`IRepository`接口上的泛型类型参数是不变的。

![](img/0155736aec718cf18821e9f10a5d308d_1149_0.png)

在`IReadRepository`上，我们将其定义为协变，所以这里本来是可以工作的，但`IReadRepository`没有`Add`方法，也没有`Save`方法。在`IWriteRepository`接口上，你有`Add`和`Save`方法，但泛型类型参数被定义为逆变。这意味着，这里的泛型类型实参可以更具体，但不能更不具体。但在这里，`IEntity`接口比`Organization`更不具体。这意味着，当你尝试像这样将一个`IWriteRepository<Organization>`传递给`IWriteRepository<IEntity>`时，会得到一个编译错误。所以，你会看到所有这些方案在这里都行不通。让我按`Ctrl+set`重新获取`Organization`的`IRepository`接口。但你在这里要对`employee`做的是，把这里的`Organization`类型以及另一处的类型都替换掉。实际上，你可以通过将`AddBatch`方法定义为泛型方法来实现这一点。

要做到这一点，你需要在方法名后面创建一个泛型类型参数。

```csharp
private static void AddBatch<T>(IRepository<Organization> organizationRepository,
    Organization[] organizations)
{
    foreach (var item in organizations)
    {
        organizationRepository.Add(item);
    }

    organizationRepository.Save();
}
```

现在你可以将这个类型参数用于方法参数，如果愿意，也可以用于方法的返回类型。那么，让我们把这里的`Organization`替换为`T`，并把`Organization`数组替换为`T`数组。现在让我也把这里的`organizationRepository`重命名为`repository`。我按下`Ctrl+RR`，输入`repository`，然后按`Enter`。让我们再把参数`organizations`重命名为`items`。我再次按下`Ctrl+RR`，在这里输入`items`。现在，我们还可以删除这里的换行，因为这个参数很短。但正如你现在所看到的，`repository`带有红色下划线。当你悬停它时，会看到这个错误：类型`T`不能作为类型参数`T`用于泛型类型或泛型方法`IRepository`。

```csharp
private static void AddBatch<T>(IRepository<T> repository, T[] items)
    where T : IEntity
{
    foreach (var item in items)
    {
        repository.Add(item);
    }

    repository.Save();
}
```

不存在从`T`到`IEntity`的转换。在`IRepository`接口上，我们有一个类型约束，要求`T`必须是`IEntity`。因此，你也必须为这个类型参数添加类型约束。你也可以在方法上使用`where`关键字来做到这一点。在这里你可以写`where T implements IEntity`。现在你会看到错误消失了。不过，与其在这里使用`IRepository`接口，你可以使用更不具体的`IWriteRepository`接口，因为这个接口有`Add`和`Save`方法。这个接口没有类型约束，这意味着你也可以从泛型方法中移除类型约束。

现在，当我向上滚动时，你会看到你可以将`AddBatch`方法用于员工，也可以用于组织。实际上，让我再次删除这一行。当你调用`AddBatch`方法时，你可以看到它是一个泛型方法，因为这里有这些尖括号。IntelliSense 还会显示它有一个泛型类型参数，并且它接收一个`IWriteRepository<T>`和一个`T`数组。

```cs
};

AddBatch<Employee>(employeeRepository, employees);

}

private static void AddOrganizations(IRepository<Organization> organizationRepository)
{

var organizations = new[]
{

```

现在你可以说，在这种情况下，你想以`Employee`类型来使用它。然后你会看到它接收一个`IWriteRepository<Employee>`以及一个`Employee`数组。这意味着你可以传入`employeeRepository`和`employees`数组。现在，C# 编译器足够聪明，能够根据方法参数检测出你想以`Employee`类型调用`AddBatch`方法，因为这里比如传入的就是一个`IWriteRepository<Employee>`。这意味着，在这种情况下，泛型类型实参是可选的，你可以将其移除。当你悬停在`AddBatch`方法上时，你会看到编译器使用的是`AddBatch<Employee>`。

在下一个演示中，你将学习如何构建泛型扩展方法。之前你已经创建了一个泛型`AddBatch`方法，它可以将一个`T`数组添加到`IWriteRepository`中。如果这个方法能用在所有`IWriteRepository`实例上，那不是很好吗？实际上，你可以通过将这个方法实现为`IWriteRepository`接口的扩展方法来做到这一点。现在让我们在本次演示中这样做。首先，我选中这个方法，并将它剪切出来。接下来，我们打开解决方案资源管理器，右键单击`Repositories`，然后从上下文菜单中选择“添加”->“类”。让我们在此创建一个新类，我称之为`RepositoryExtensions`，并将这个类添加到`Repositories`文件夹中。首先，按`Ctrl+.`删除不必要的`using`指令。接下来，我将这个类设置为`public static`类。`static`意味着它只能包含静态成员。

```cs
public static class RepositoryExtensions
{
    private static void AddBatch<T>(IWriteRepository<T> repository, T[] items)
    {
        foreach (var item in items)
        {
            repository.Add(item);
        }

        repository.Save();
    }
}
```
