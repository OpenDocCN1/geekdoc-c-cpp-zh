

to be available on your entities. All the entities in our project implement the IEntity interface.

![](img/0155736aec718cf18821e9f10a5d308d_1157_0.png)

这意味着你可以前往 EntityExtensions 类，在这里的 copy 方法上添加一个泛型类型约束，说明 T 是 IEntity。现在让我们回到 Program.cs 文件。现在，当你尝试在这个对象上调用扩展方法时，你会发现它不再出现在 IntelliSense 中，但它仍然出现在你的实体上，例如在 Manager 上。这里，由于 Manager 是一个 IEntity 实例，你可以使用该扩展方法。

![](img/0155736aec718cf18821e9f10a5d308d_1157_1.png)

到目前为止关于泛型方法。你只需在方法名之后定义泛型类型参数，然后你就可以将这些类型用于方法参数以及方法的返回类型。
接下来，你将开始学习委托。在下一个演示中，你将学习如何添加和使用一个委托。这里在 Program 类的 Main 方法中，我们使用了 Employee 的 SqlRepository。
现在假设你希望能够向 SqlRepository 构造函数传递一个方法，每当添加一个员工时就会调用该方法。为此，你需要一个委托。所以现在让我们前往 SqlRepository C# 文件，并在其中实现此功能。首先，让我们在此文件中创建一个返回 void 的公共委托，并将其命名为 ItemAdded。让我们添加一个类型为 object 的参数，并将其命名为 item。

```
{
    public delegate void ItemAdded(object item);

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
            return _dbSet.OrderBy(item => item.Id).ToList();
        }
    }
```

委托就像一个方法指针。此委托可以指向一个返回 void 且具有 object 参数的方法。现在在 SqlRepository 构造函数上，让我们添加一个 ItemAdded 参数，并将其命名为 ItemAddedCallback。我将其初始化为 null。因此，让我们也为此参数添加一个问号以将其标记为可空。现在，

让我们按 Ctrl+点来创建并将此参数分配给字段 _itemAddedCallback。你可以在这里看到创建的字段，并在构造函数中进行赋值。现在让我们向下滚动到 Add 方法。这里在 Add 方法中，你使用 _itemAddedCallback。你可以用问号检查它是否不为 null，然后你可以调用该回调并传入 item。所以让我们在这里传入已添加的 item。这意味着委托将调用它所指向的方法。

![](img/0155736aec718cf18821e9f10a5d308d_1159_0.png)

现在让我们回到 Program.cs 文件并使用该功能。这里在 SqlRepository 之前，让我们创建一个 ItemAdded 委托实例。让我们将其指向名为 EmployeeAdded 的方法。你可以按 Ctrl+点，Visual Studio 会建议你创建此 EmployeeAdded 方法。

![](img/0155736aec718cf18821e9f10a5d308d_1159_1.png)

现在你可以将此 itemAdded 委托传递给 SqlRepository 类的构造函数。这意味着现在每当向 SqlRepository 添加一个员工时，EmployeeAdded 方法将被调用。现在让我们向下，并实现此方法。假设你想将员工的 first name 写入控制台。所以首先，让我们在这里创建一个 employee 变量，并将这里类型为 object 的 item 强制转换为 Employee。然后，让我们创建 Console.WriteLine 语句，并在其中写入 Employee added，并打印出员工的 FirstName。但现在，如果你能在这里直接获得 employee 类型就好了，因为该类型已在此 SqlRepository 上定义。你将在接下来通过泛型委托学习如何做到这一点。在下一个演示中，你将学习如何创建一个泛型委托。之前，你创建了此 itemAdded 委托，它指向此 EmployeeAdded 方法。如果这里能得到 employee 而不是 object 就好了。那么你就不需要将 object 强制转换为 employee 才能使用其 first name。所以让我们将参数类型从 object 改为 Employee。

```
var itemAdded = new ItemAdded(EmployeeAdded);
var employeeRepository = new SqlRepository(itemAdded);
AddEmployees(employeeRepository);
AddManagers(employeeRepository);
GetEmployeeById(employeeRepository);
WriteAllToConsole(employeeRepository);

var organizationRepository = new ListRepository<Organization>();
AddOrganizations(organizationRepository);
WriteAllToConsole(organizationRepository);

Console.ReadLine();
}

private static void EmployeeAdded(Employee employee)
{
    Console.WriteLine($"Employee added => {employee.FirstName}");
}

// Error tooltip: CS0123: No overload for 'EmployeeAdded' matches delegate 'ItemAdded'
// Signature shown: void Program.EmployeeAdded(Employee employee)
```

让我们删除这一行，并直接从该 Employee 中取出 FirstName 属性。让我们也通过按 Ctrl+R+R 重命名该参数，并将其命名为 employee。但现在你可以看到，委托在这里被红色下划线标记。当你悬停其上时，你会看到这里的错误，No overload for 'EmployeeAdded' matches delegate 'ItemAdded'。该方法与委托签名不匹配，因为我们在这里定义了一个 employee 参数。但当你查看 SqlRepository C# 文件中的委托时，你可以看到委托接受一个 object。但现在，就像泛型方法一样，你也可以通过在委托名后使用泛型类型参数来定义泛型委托。所以在这里，你可以定义类型参数，然后用类型 T 的 item 代替 object。

![](img/0155736aec718cf18821e9f10a5d308d_1161_0.png)

这意味着在 SqlRepository 中，你可以创建这里的 ItemAdded 委托，并将其作为构造函数参数接收。当你向下滚动到使用委托的 Add 方法时，你会看到一切正常，因为 Invoke 方法接受类型 T 的 item，而我们这里也有类型 T 的 item。所以让我们传入该 item。现在让我们回到 Program.cs 文件。如你所见，ItemAdded 委托仍然被红色下划线标记，但现在当你悬停其上时，你会看到不同的错误。错误说，Using the generic type ItemAdded requires 1 type arguments。

![](img/0155736aec718cf18821e9f10a5d308d_1162_0.png)

所以在这种情况下，类型是 Employee。让我们将其指定为类型参数。当你实际悬停在 SqlRepository 类的构造函数上时，你会看到它接受一个 ItemAdded 委托。这意味着现在我们可以将 employee 作为参数传入，这将正常工作。

![](img/0155736aec718cf18821e9f10a5d308d_1162_1.png)

使用泛型接口，你可以在泛型委托上将类型参数定义为协变或逆变。所以，让我们前往解决方案资源管理器，并打开包含 ItemAdded 委托的 SqlRepository.cs 文件。你可以在这里使用 in 关键字将此类型参数指定为逆变。这意味着现在当你回到 Program.cs 文件时，将此 ItemAdded 委托分配给 ItemAdded 变量是完全可以的。

![](img/0155736aec718cf18821e9f10a5d308d_1164_0.png)

所以，当你现在调用此 managerAdded 委托时，你必须传入一个 Manager。而由于 Manager 实际上是一个 Employee，将 Manager 传递给由委托包装的 EmployeeAdded 方法是可行的。现在让我们回到 SqlRepository.cs 文件。你也可以将泛型类型参数作为返回值。所以，如果你在这里返回类型 T 而不是 void，它会被红色下划线标记。当你悬停时，你会得到错误，Invalid variance: The type parameter 'T' must be covariantly valid on 'ItemAdded'.Invoke(T).'T' is contravariant。是的，我们在这里使用 in 关键字将其定义为逆变。你只能在类型参数未用作返回类型时将其定义为逆变。如果它用作输入和输出，你必须将类型参数定义为不变。

