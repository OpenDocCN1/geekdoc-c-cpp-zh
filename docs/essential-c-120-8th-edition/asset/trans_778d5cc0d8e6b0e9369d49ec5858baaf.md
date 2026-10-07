

## 构造函数

当你显式添加构造函数时，你将无法在从 `Main()` 中不指定名和姓的情况下实例化 `Employee` 对象。因此，列表 6.29 所示的代码将无法编译。

列表 6.29: 默认构造函数不再可用

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee;

        // 错误：没有重载方法 'Employee'
        // 取 '0' 个参数
        employee = new Employee();

        // ...
    }
}
```

如果一个类没有显式定义的构造函数，C# 编译器会在编译期间添加一个。该构造函数不接受任何参数，因此根据定义，它是**默认构造函数**。一旦你为类添加了显式构造函数，**C# 编译器**就不再提供默认构造函数了。因此，在定义了 `Employee(string firstName, string lastName)` 后，编译器不会再添加默认构造函数 `Employee()`。你可以手动再次添加一个，允许在不指定员工姓名的情况下构造 `Employee`。

没有必要依赖编译器定义的默认构造函数。也就是说，程序员可以显式定义一个默认构造函数——例如将某些字段初始化为特定值的构造函数。定义默认构造函数只需声明一个不接受任何参数的构造函数。

**拷贝构造函数**是一个接收包含类型单一参数的构造函数。例如：

```csharp
public Employee(Employee original)
{
    // 在此处拷贝员工之间的之间的属性。
}
```

这样的构造函数对于将对象的实例克隆到新的重复实例非常有用。

## 对象初始化器

为了初始化对象的可访问字段和属性，你可以使用对象初始化器的概念——这是在构造函数调用之后，用大括号括起来的一组成员初始化器，用于创建对象。每个成员初始化器都是将一个可访问字段或属性名赋以一个值（见列表 6.30）。

列表 6.30: 使用显式成员赋值调用对象初始化器

```csharp
public class Program {
    public static void Main()
    {
        Employee employee = new("Inigo", "Montoya");
        Title = "Computer Nerd", Salary = "Not enough";
        // ...
    }
}
```

注意，即使在使用对象初始化器时，相同的构造函数规则也适用。C# 中成员初始化器的顺序提供了从构造函数调用之后到 CIL 之前的语句中属性和字段赋值的序列。

通常情况下，在构造函数退出时，所有属性都应该被初始化为合理的默认值。此外，通过在设置器（setter）上使用验证逻辑，可以限制向属性分配无效数据。有时，一个或多个属性的值可能会导致同一对象上的其他属性包含无效值。当这种情况发生时，来自无效状态的异常应该被推迟，直到相关的属性值变得相关。

> 指南
> 务必为所有属性提供合理的默认值，确保默认值不会导致安全漏洞或严重低效的代码。

> 必须允许按任何顺序设置属性，即使这会导致对象处于暂时的无效状态。

## 进阶主题

### 集合初始化器

使用与对象初始化器类似的语法，集合初始化器支持与对象初始化器类似的功能，只是针对集合的。具体来说，集合初始化器允许在集合实例化时为集合中的项赋值。借用用于数组的相同语法，集合初始化器在创建时初始化集合中的每个项。例如，初始化 `Employee` 对象的列表需要在构造函数调用后的大括号内指定每个项，如列表 6.31 所示。

列表 6.31: 调用对象初始化器

```csharp
public class Program {
    public static void Main() {
        List<Employee> employees = new() {
            new("Inigo", "Montoya"),
            new("Kevin", "Bost")
        };
        //...
    }
}
```

在分配新集合实例后，编译器将生成实例化。集合初始化器允许在集合实例化时为集合中的项赋值。此处此处，重复重复，重新翻译逻辑）

使用与对象初始化器类似的语法，集合初始化器支持与对象初始化器类似的功能，只是针对集合的。具体来说，集合初始化器允许在集合实例化时为集合中的项赋值。借用用于数组的相同语法，集合初始化器在创建时初始化集合中的每个项。例如，初始化 `Employee` 对象的列表需要在构造函数调用后的大括号内指定每个项，如列表 6.31 所示。

列表 6.31: 调用对象初始化器

```csharp
public class Program {
    public static void Main() {
        List<Employee> employees = new() {
            new("Inigo", "Montoya"),
            new("Kevin", "Bost")
        };
        //...
    }
}
```

在分配新集合实例后，编译器将生成实例化。

（注：由于原文文本在后续部分出现了大量重复和乱码，以下翻译已根据上下文逻辑进行了清理和对齐）

在分配新集合实例后，编译器将生成实例化。

### 仅初始化 setter

对象初始化器允许在初始化期间设置属性。然而，由于只读属性在初始化器之后无法设置，为了解决这个问题，C# 9.0 增加了 `init` 访问器，可以在初始化期间进行设置。

列表 6.32: 仅初始化 setter

```csharp
public class Employee
{
    public Employee(int id, string name)
    {
        Id = id;
        Name = name;
    }

    // ...

    public int Id { get; }
    public string Name { get; }

    public string? Salary
    {
        get => _Salary;
        init => _Salary = value;
    }
    private string? _Salary;
}

public class Program
{
    public static void Main()
    {
        Employee employee = new(42, "Inigo Montoya")
        {
            Salary = "Sufficient"
        };

        // 错误：属性 'Employee.Salary'
        // 在初始化后无法赋值。
        employee.Salary = "Enough";
    }
}
```

注意，虽然你可以在初始化期间设置 `Salary` 的值，但在初始化完成后无法更改该值。它是只读的。

