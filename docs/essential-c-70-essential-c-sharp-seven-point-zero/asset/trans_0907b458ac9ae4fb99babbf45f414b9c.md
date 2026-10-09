
通常，在构造函数退出之前，所有属性都应初始化为合理的默认值。此外，通过在 setter 中使用验证逻辑，可以限制将无效数据赋值给属性。在某些情况下，一个或多个属性的值可能导致同一对象上的其他属性包含无效值。当这种情况发生时，源自无效状态的异常应推迟到相关的无效属性值变得相关时才抛出。

## 准则

- 应为所有属性提供合理的默认值，确保默认值不会导致安全漏洞或显著低效的代码。对于自动实现的属性，通过构造函数设置默认值。
- 应允许按任意顺序设置属性，即使这会导致对象处于暂时的无效状态。

## 高级主题

## 集合初始化器

使用与对象初始化器类似的语法，C# 3.0 中添加了集合初始化器。集合初始化器支持与对象初始化器类似的功能集，只不过作用于集合。具体来说，集合初始化器允许在集合实例化时分配集合内的项。借用数组所使用的相同语法，集合初始化器在创建集合时初始化集合内的每个项。例如，初始化一个员工列表涉及在构造函数调用后的大括号内指定每个项，如列表 6.30 所示。

### 列表 6.30：调用对象初始化器

```csharp
class Program
{
    static void Main()
    {
        List<Employee> employees = new List<Employee>()
        {
            new Employee("Inigo", "Montoya"),
            new Employee("Kevin", "Boost")
        };
        // ...
    }
}
```

在分配新的集合实例后，编译器生成的代码将依次实例化每个对象，并通过 Add() 方法将它们添加到集合中。

## 高级主题

## 终结器

构造函数定义了在类的实例化过程中发生什么。为了定义对象销毁时发生什么，C# 提供了终结器构造。与 C++ 中的析构函数不同，终结器并不会在对象超出作用域后立即运行。相反，终结器在对象被确定为“不可达”后的某个未指定时间执行。具体来说，垃圾回收器在垃圾回收周期中识别具有终结器的对象，并立即不释放这些对象，而是将它们添加到终结队列中。一个独立的线程遍历终结队列中的每个对象，并在将其从队列中移除并使其可供垃圾回收器再次使用之前调用该对象的终结器。第 10 章将详细讨论这个过程以及资源清理。顺便一提，C# 7.0 允许将终结器实现为表达式体成员。

## 重载构造函数

构造函数可以重载——只要参数数量或类型不同，就可以拥有多个构造函数。例如，如列表 6.31 所示，你可以提供一个包含员工 ID、名和姓的构造函数，或者甚至只包含员工 ID 的构造函数。

### 列表 6.31：重载构造函数

```csharp
class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }

    public Employee(
        int id, string firstName, string lastName )
    {
        Id = id;
        FirstName = firstName;
        LastName = lastName;
    }

    public Employee(int id) => Id = id;

    public int Id
    {
        get => Id;
        private set
        {
            // 查找员工姓名...
            // ...
        }
    }

    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Salary { get; set; } = "Not Enough";

    // ...
}
```

这种方法使得 Program.Main() 能够通过仅传入员工 ID 或同时传入姓名和 ID 的方式，从名和姓实例化员工。在系统中创建新员工时，你会使用包含姓名和 ID 的构造函数。你会使用仅包含 ID 的构造函数从文件或数据库中加载员工。

与方法重载类似，使用多个构造函数是为了支持使用少量参数的简单场景以及使用额外参数的复杂场景。考虑使用可选参数来替代重载，以便在 API 中显示“默认”属性的默认值。例如，Person(string firstName, string lastName, int? age = null) 的构造函数签名提供了签名文档，说明如果未指定 Person 的 Age，它将默认为 null。

此外，请注意，从 C# 7.0 开始，构造函数可以具有表达式体成员实现，例如：

```csharp
public Employee(int id) => Id = id;
```

## 准则

- 如果构造函数参数仅用于设置属性，则应为构造函数参数（camelCase）和属性（PascalCase）使用相同的名称。
- 应提供构造函数可选参数和/或便捷构造函数重载，以良好的默认值初始化属性。
- 应允许按任意顺序设置属性，即使这会导致对象处于暂时的无效状态。

## 构造函数链接：使用 this 调用另一个构造函数

注意在列表 6.31 中，Employee 对象的初始化代码现在在多个地方重复，因此需要在多个地方维护。代码量很小，但有一些方法可以通过使用构造函数初始化器从一个构造函数调用另一个构造函数——即构造函数链接——来消除重复。构造函数初始化器决定在执行当前构造函数的实现之前调用哪个构造函数（参见列表 6.32）。

### 列表 6.32：从一个构造函数调用另一个构造函数

```csharp
class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }

    public Employee(
        int id, string firstName, string lastName)
        : this(firstName, lastName)
    {
        Id = id;
    }

    public Employee(int id)
    {
        Id = id;

        // 查找员工姓名...
        // ...

        // 注意：成员构造函数不能显式内联调用。
        // this(id, firstName, lastName);
    }

    public int Id { get; private set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Salary { get; set; } = "Not Enough";

    // ...
}
```

要在同一类内从一个构造函数调用另一个构造函数（针对同一对象实例），C# 使用冒号后跟 **this** 关键字，再跟被调用构造函数声明中的参数列表。在这种情况下，接受所有三个参数的构造函数调用了接受两个参数的构造函数。通常，这种调用模式是相反的——也就是说，参数最少的构造函数调用参数最多的构造函数，并为未知的参数传递默认值。

## 初学者主题
### 集中初始化

注意在列表 6.32 的 `Employee(int id)` 构造函数实现中，你不能调用 `this(firstName, lastName)`，因为这个构造函数没有这样的参数。为了启用所有初始化代码都通过一个方法执行的模式，你必须创建一个单独的方法，如列表 6.33 所示。

## 列表 6.33：提供初始化方法

```csharp
class Employee
{
    public Employee(string firstName, string lastName)
    {
        int id;
        // 生成员工 ID...
        // ...
        Initialize(id, firstName, lastName);
    }

    public Employee(int id, string firstName, string lastName)
    {
        Initialize(id, firstName, lastName);
    }

    public Employee(int id)
    {
        string firstName;
        string lastName;
        Id = id;

        // 查找员工数据
        // ...
        Initialize(id, firstName, lastName);
    }

    private void Initialize(
        int id, string firstName, string lastName)
    {
        Id = id;
        FirstName = firstName;
        LastName = lastName;
    }
    // ...
}
```

在这种情况下，该方法名为 Initialize()，它接受姓名和员工 ID。请注意，你仍然可以如列表 6.32 所示，从一个构造函数调用另一个构造函数。

## 解构器

构造函数允许你接受多个参数并将它们全部封装到一个对象中。在 C# 7.0 之前，没有明确的构造用于实现相反的操作——将封装的项拆分为其组成部分。当然，你可以手动将每个属性赋值给一个变量；然而，如果存在大量这样的变量，它将需要许多单独的语句。随着 C# 7.0 对元组语法的引入，这变得容易得多。例如，你可以声明一个像列表 6.34 所示的 Deconstruct() 方法那样的方法。

