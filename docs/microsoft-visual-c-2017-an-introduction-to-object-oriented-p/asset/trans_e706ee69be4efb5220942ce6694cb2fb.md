

```csharp
class Employee
{
    private int idNumber;
    private string name;
    public Employee()
    {
        PayRate = 9.99;
    }
    public double PayRate{get; set;}
    // Other classes can go here
}
```

**图 9-22** 带有无参数构造函数的 Employee 类

图 9-22 中的构造函数是一个**无参数构造函数**——一个不接受任何参数的函数。也就是说，你可能选择为每个 *Employee* 创建不同的初始薪率。为了完成这项任务，你可以将薪率传递给构造函数。图 9-23 显示了接收参数的 Employee 构造函数。可以使用如下语句将值传递给构造函数：
*Employee partTimeWorker = new Employee(12.50);*

当构造函数执行时，方法调用用实际参数的 double 类型被传递给 *Employee()* 并赋值给 *Employee* 的 *PayRate*。

```csharp
public Employee(double PayRate)
{
    PayRate = PayRate;
}
```

**图 9-23** 带有参数的 Employee 构造函数

# 重载构造函数

C# 会自动为你的类创建一个默认构造函数。一旦你创建了自己的构造函数（无论它是否带有参数），你就再无法访问自动创建的版本了。然而，如果你想让一个类同时拥有带参数和无参数的构造函数版本，你可以创建它们。像任何其他 C# 方法一样，构造函数也可以被重载。你可以根据需要为一个类编写任意数量的构造函数，只要它们的参数列表不会引起歧义即可。一个类只能包含一个无参数构造函数：即默认构造函数，它可以是自动提供的，也可以是你编写的。如果你创建了任意数量的构造函数但没有创建无参数版本，它们将是歧义的；那么该类就不具有默认构造函数了。

例如，图 9-24 中的 Employee 类包含四个构造函数。图 9-25 中 CreateSomeEmployees 类中的 Main() 方法显示了如何实例化不同类型的 Employee。注意，即使是 Employee 构造函数中的一个——即一个支持字符参数的构造函数——也没有被使用；有时你可能创建一个带有特定参数类型的构造函数，仅仅是为了强制该构造函数成为执行的那个一个。CreateSomeEmployees 程序的输出如图 9-26 所示。

```csharp
class Employee
{
    public int IdNumber {get; set;}

    public double Salary {get; set;}
    public Employee()
    {
        IdNumber = 999;
        Salary = 0;
    }
    public Employee(int empId)
    {
        IdNumber = empId;
        Salary = 0;
    }
    public Employee(int empId, double sal)
    {
        IdNumber = empId;
        Salary = sal;
    }
    public Employee(char code)
    {
        IdNumber = 111;
        Salary = 100000;
    }
}
```

图 9-24 带有四个构造函数的 Employee 类

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_407_0.png)

```csharp
using static System.Console;
class CreateSomeEmployees
{
    static void Main()
    {
        Employee aWorker = new Employee();
        Employee anotherWorker = new Employee(234);
        Employee theBoss = new Employee('A');
        WriteLine("{0, 4}{1, 14}", aWorker.IdNumber,
            aWorker.Salary.ToString("C"));
        WriteLine("{0, 4}{1, 14}", anotherWorker.IdNumber,
            anotherWorker.Salary.ToString("C"));
        WriteLine("{0, 4}{1, 14}", theBoss.IdNumber,
            theBoss.Salary.ToString("C"));
    }
}
```

图 9-25 CreateSomeEmployees 程序

| | $0.00 |
|---|---|
| 234 | $0.00 |
| 111 | $100,000.00 |

图 9-26 CreateSomeEmployees 程序的输出

很有可能，单个应用程序不会使用 Employee 类的全部四个构造函数。更有可能，每个使用该类的应用程序只会使用一个或两个构造函数。我们创建一个带有多个构造函数的类是为了为客户提供灵活性。例如，某些客户可能选择仅用 ID 数字来构造 Employee 对象，而另一些客户可能倾向于用 ID 数字和薪水来构造。

# 使用构造函数初始化器

图 9-24 中的 Employee 类包含四个构造函数，每个构造函数都初始化相同的字段。在公司使用的完整代码中，会有更多的字段被初始化，产生大量的重复代码。在这些构造函数中编写重复语句是一项额外工作，当将来修改类时将需要更多工作。例如，如果你的组织实施了需要特定位数的新员工 ID 编号格式，那么每个构造函数都必须修改，并且可能会漏掉一个或多个必须修改的构造版本，从而给类的类的程序引入错误。

作为重复构造函数的替代方案，你可以使用构造函数初始化器。构造函数初始化器是一个语句，表示在执行当前构造函数体中的任何语句之前，应该执行类构造函数的另一个实例。图 9-27 显示了新版本的 Employee 类，在四个重载构造函数中的三个使用了构造函数初始化器。

```csharp
class Employee {
    public int IdNumber {get; set;}
    public double Salary {get; set;}
    public Employee() : this(999, 0) {}

    public Employee(int empId) : this(empId, 0) {}

    public Employee(int empId, double sal) {
        IdNumber = empId;
        Salary = sal;
    }

    public Employee(char code) : this(111, 100000) {}
}
```

**9-27** 带有构造函数初始化器的 Employee 类

图 9-27 中的三个阴影子句中，此引用被用来表示“正在构造的对象的构造函数”。例如，当客户调用无参数的 Employee 时，999 和 0 被传递给带有两个参数的构造函数。在那里，它们变成了 empId 和 sal，这些被赋值给 IdNumber 和 Salary 属性的参数。如果在无参数构造函数内部编写了语句，它们将被执行；但在该类中，没有必要的额外的语句。同样，如果客户使用只接受一个参数的构造函数版本，该参数和薪水的 0 将被传递给两个参数的构造函数。只有当客户将 ID 数字和薪水作为构造函数参数时，该参数版本的构造函数才会执行。将来，如果需要对类添加额外的语句（例如，确保 ID 编号至少五位数），该决策将只需添加到两个参数的构造函数中，其他所有版本可以使用它。

# 在构造函数中使用 readonly 修饰符

你已经学习过当你对变量使用 const 修饰符时，必须在声明处赋值且该值无法更改。readonly 修饰符与 const 相似，它们都用于分配不可更改的常量值，但当你对字段使用 readonly 时，你可以在声明处或构造函数内部赋值。这意味着不同的构造函数可以为 readonly 字段分配不同的值。const 字段必须在程序编译时赋值，而 readonly 字段可以在初始化时或运行时赋值。例如，readonly 字段的值可以从用户输入或操作系统获取。

图 9-28 显示了一个带有 Employee 类的程序，其中 idNumber 被声明为 readonly。（参见第一个阴影语句。）Main() 程序可以向构造函数发送不同的值来赋值给 idNumber，但在构造之后，idNumber 不能再更改。第二个阴影语句会导致编译器错误。

```csharp
class EmployeesReadOnlyDemo {
    static void Main() {
        Employee myAssistant = new Employee(1234);
        Employee myDriver = new Employee(2345);
        myAssistant.IdNumber = 3456;
    }
}
class Employee {
    private readonly int idNumber;
    public Employee(int id) {
        idNumber = id;
    }
    public int IdNumber {
        get {
            return idNumber;
        }
        set {
            idNumber = value;
        }
    }
}
```

图 9-28 带有 readonly 字段的 Employee 类

