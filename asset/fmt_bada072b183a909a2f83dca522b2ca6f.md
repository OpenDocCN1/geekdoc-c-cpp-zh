
```csharp
List<Employee> employees = new List<Employee>() {

new Employee("Inigo", "Montoya"),

new Employee("Kevin", "Bost");

};
```

![img18af4770e919568243fa73ff1469b4_335_0

在新集合赋值之后，生成的代码将顺序实例化每个对象并通过 `Add()` 方法添加到集合中。

## 终析器

构造函数定义了对象销毁时发生了什么。C# 提供了终析器结构与与 C++ 的析构构不同，析器在在作用后立即运行。终析器在对象确定为“不可到达”后的不确定时间执行。具体来说，垃圾收集器在垃圾回收期间识别带有终析器的对象，而不是立即释放这些对象，而是将它们添加到终析队列中。一个单独的线程遍历终析队列中的每个对象，并在调用对象的终析器之前将其从队列中移除，并允许垃圾收集器再次使用。第 10 章将深入讨论这一过程，以及资源清理。

## 构造函数重载

构造函数可以重载——只要参数的数量或类型不同，你就可以拥有多个构造函数。例如，如列表 6.31 所示，你可以提供一个带有员工 ID、名字和姓氏的构造函数，甚至只有一个员工 ID。

### 列表 6.31：重载构造函数

```csharp
public class Employee {
    public Employee(string firstName, string lastName)
{}
}
```

# 构造函数

```csharp
FirstName = firstName;
LastName = lastName;
}
public Employee(
    int id, string firstName, string lastName)
{
    Id = id;
    FirstName = firstName;
    LastName = lastName;
}
// FirstName & LastName 设置在 Id 属性访问器内部。
#pragma warning disable CS8618
public Employee(int id) => Id = id;
#pragma warning restore CS8618
public int Id
{
    get => Id;
    private set
        // 查找员工姓名...
        // ...
}
```

`public string FirstName { get; set; }`
`public string LastName { get; set; }`
`public string? Salary { get; set; } = "金额不足";`

这种方法允许 `Program.Main()` 通过仅传递员工 ID 或同时传递姓名和 ID，根据姓和名来实例化员工。当在系统中创建新员工时，你会使用同时包含姓名和 ID 的构造函数。当从文件或数据库加载员工数据时，你会使用仅包含 ID 的构造函数。

与方法重载一样，使用多个构造函数是为了同时支持使用少量参数的简单场景和带有额外参数的复杂场景。考虑使用可选参数来代替重载，这样“默认”属性的默认值在 API 中是可见的。例如，`Person(string firstName, string lastName, int? age = null)` 构造函数签名提供了签名文档说明：如果未指定人的年龄（Age），它将默认为 `null`。

# 第 6 章：类

请注意，从 C# 7.0 开始，可以对构造函数使用表达式体成员实现，如下所示：

```csharp
// FirstName & LastName 设置在 Id 属性访问器内部。
#pragma warning disable CS8618
public Employee(int id) => Id = id;
```

在这种情况下，我们调用 `Id` 属性来给 `FirstName` 和 `LastName` 赋值。遗憾的是，编译器没有检测到该赋值，并且从 C# 8.0 开始会发出警告，考虑将这些属性标记为可空。由于我们实际上设置了它们，因此禁用了该警告。

# 指南

- 如果构造函数参数仅用于设置属性，请对构造函数参数（驼峰命名法 camelCase）和属性（帕斯尔命名法 PascalCase）使用**相同的名称**。
- 提供构造函数可选参数和/或便利构造函数重载，用默认值初始化属性。
- 允许按任何顺序设置属性，即使这会导致对象处于暂时的无效状态。

# 构造函数链：使用 this 调用另一个构造函数

在列表 6.31 所示，`Employee` 对象的初始化代码现在于多处是重复的，因此也必须在多处进行维护。虽然代码量很小，但有方法可以通过从一个构造函数调用另一个构造函数来消除重复——这种做法被称为**构造函数链**——构造函数初始化器会在执行当前构造函数的实现之前确定要调用哪个构造函数（参见列表 6.32）。

列表 6.32：从一个构造函数调用另一个构造函数

```csharp
public class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }
public Employee(
    int id, string firstName, string lastName ) 
    : this(firstName, lastName)
    {
        Id = id;
    }
    // FirstName & LastName 设置在 Id 属性访问器内部。
    #pragma warning disable CS8618
    public Employee(int id)
    {
        Id = id;
        // 查找员工姓名...
        //
        // 注意：成员构造函数不能
        // 显式内联调用
        // this(id, firstName, lastName);
    }
    public int Id { get; private set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string? Salary { get; set; } = "金额不足";
```

要在同一类内（针对同一个对象实例）调用另一个构造函数，C# 使用冒号后跟 `this` 关键字，然后是被调用构造函数声明中的参数列表。在这种情况下，接收三个参数的构造函数调用了接收两个参数的构造函数。也就是说，参数最少的构造函数调用了参数最多的构造函数，并为未知的参数传递默认值。

## 初学者主题

# 集中初始化

注意在列表 6.32 的 `Employee(int id)` 构造函数实现中，你不能调用 `this(firstName, lastName)`，因为该构造函数上不存在此类参数。为了启用这种模式（即所有初始化代码都通过一个方法发生），你必须创建一个单独的方法，如列表 6.33 所示。

# 第 6 章：类

列表 6.33：提供初始化方法

```csharp
public class Employee
{
    // FirstName & LastName 设置在 Initialize() 方法内部。
    #pragma warning disable CS8618 
    public Employee(string firstName, string lastName)
    {
        int id;
        // 生成员工 ID...
        //...
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
        //...
        Initialize(id, firstName, lastName);
    }
    #pragma warning restore CS8618
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

在这种情况下，调用了 `Initialize()` 方法，它接收了姓名和员工 ID。注意，你可以像列表 6.32 所示，继续从一个构造函数调用另一个构造函数。

正如通过 `Id` 属性设置 `LastName` 和 `FirstName` 未被检测到一样，通过 `Initialize` 方法的赋值也没有被检测到，因此禁用了该警告。

# 带构造函数的非可空引用类型属性

在整个章节中，我们一直禁用了 C# 警告：

CS8618：非可空字段/属性未初始化。考虑将其标记为可空。

当你声明引用类型 (1) 非可空字段或 (2) 非可空自动实现属性时，显然这些字段和属性在容器对象完全实例化之前需要初始化。不要让这些字段和属性保持默认值——因此它们不应被声明为非可空。

问题在于，非可空字段和属性经常间接初始化，超出了构造函数的直接作用范围，因此超出了编译器的代码分析范围，尽管它们实际上已经过初始化，可能是通过构造函数调用的方法或属性实现的。以下是这种做法的一些示例：

- 具有验证逻辑的简单属性在赋值给编译器报告未初始化的字段之前，会检查要赋值的值是否不空（参见列表 6.20）。
- 计算属性 `Name`（如列表 6.22）设置了类中的其他非可空属性或字段。
- 集中初始化采用了列表 6.32 和 6.33 所示的方式。
- 公共属性由外部代理触发实例化并进行初始化。

大多数情况下，引用类型非可空字段或非可空自动实现属性（在本节中称为非可空字段/属性，“引用类型”是隐含的）通过构造函数调用的属性或方法间接赋值。遗憾的是，C# 编译器无法识别非可空字段/属性的间接赋值。

>.7 或者可能通过外部代理，参见第 18 章。

> 8. 示例包括 MSTest 中的 `TestContext` 属性或通过依赖注入初始的对象。

## 第6 章：类

此外，所有非可空字段/属性都需要确保它们不会被赋值为 `null` 值。对于字段，需要将它们封装在带有`setter`验证的属性中，以确保不会分配 `null` 值。（请记住，字段验证依赖于以下准则：我们不在封装字段的属性之外访问字段。）结果是，非可空的可读写完全实现引用类型属性应该具有防止 `null` 赋值的验证。

非可空自动实现属性需要限制为只读封装，在实例化期间分配的任何值在赋值之前都要验证为非空。应该避免可读可写的非可空类型自动实现属性，特别是带有公有有set器的属性，因为防止 `null` 赋值是非常困难的。虽然通过从构造函数赋值属性可以避免未初始化非空属性的编译器警告，但这还不够的：该属性是可读可写的，因此在实例化之后它可能被赋值为 `null`，从而违背了你将其设置为非空的意图。

## 可读写非可空引用类型属性

列表 6.34 展示了如何通知编译器并避免关于非可空字段/属性未初始化的虚假警告。最终目标是允许程序员通知编译器属性/字段是非可空的，以便编译器能够告知调用者这些属性/字段的（是否）可空性。

列表 6.34：对非可空属性提供验证

```csharp
public class Employee
{
    public Employee(string name)
    {
        Name = name;
    }
    public string Name
    {
        get => _Name;
        set => _Name = value ?? throw new ArgumentNullException(nameof(value));
    }
    private string? _Name;
    // ...
}
```

## 带构造函数的非可空引用类型属性

处理未由构造函数直接初始非可空属性/字段的代码段具有几个重要特性（此处列表无特定顺序）：

- 1. 属性`setter` 包含一个在设置非可空字段值之前的 `null` 检查。在列表 6.34 中，这是通过使用空合并运算符并在值值为 `null` 时抛出 `ArgumentNullException` 实现的。
- 2. 构造函数调用了一个方法或属性，间接分配了非可空字段，但未能识别出字段已初始化为 `null` 以外的值。
- 3. 后备字段被声明为可空，以避免编译器关于该字段未初始化的警告。
- 4. `getter` 使用忽略空运算符（null-forgiving operator）返回字段——即通过`setter`验证确保它不是 `null`。

对于非可空属性，将后备字段声明为可空似乎是毫无意义的。然而这是必要的，因为编译器忽略构造函数之外的非可空字段/属性赋值。坦率地说，在这种情况下，作为程序员的你之所以在返回字段时仅仅使用忽略空运算符，是因为`setter` 中的非 `null` 检查确保了字段永远不会为 `null`。

## 只读自动实现引用类型属性

正如本节前面提到的，非可空实现的引用类型属性需要是只读的，以避免无效的 `null` 赋值。然而，你仍然需要验证实例化期间可能分配的所有参数，如列表 6.35 所示。

列表 6.35：非空引用类型自动实现属性的验证

```csharp
public class Employee
{
    public Employee(string name)
    {
        Name = name?? throw new ArgumentNullException(nameof(name));
    }
    public string Name { get; }
}
```

## 第6 章：类

对于是否应该在非可空自动实现引用类型属性上允许私有`setter`可能存在争议。虽然这是可能的，但更合适的问题是，你的类是否会错误地给属性分配 `null`。如果你没有在`setter`中通过验证来封装字段，你能确定自己不会误操作分配一个 `null` 值吗？虽然编译器会验证你的实例化意图，但开发者是否总是能记得对进入类的应为非空值进行 `null` 检查是值得怀疑的——正如列表 6.35 构造函数中的所示。

> 准则
> 要实现非可空读/写引用完全实现属性，并带有可空后备字段、在从`getter`返回字段时使用忽略空运算符以及在属性`setter` 中进行非空验证。
> 要在实例化之前为非可空引用类型属性赋值。
> 要将非可空引用类型自动实现属性实现为只读。
> 对于所有在实例化完成前未初始化的引用类型属性和字段，要使用可空检查。

## 可空属性

与其禁用可空或可空警告，有时偶尔为编译器提供有关你可空意图的提示是有帮助的。这可以使用直接放在代码中的元数据来实现，这种结构称为属性（attribute）（参见第 18 章）。共有七种不同的可空属性，分别定义在`System.Diagnostics.CodeAnalysis`命名空间中，并识别为前置条件（pre-conditions）或后置条件（post-conditions）（表 6.1）。

拥有此类属性是有帮助的，因为有时数据类型的可空性是不够的。你可以使用装饰在方法上的每个输入（前置条件可空属性）或输出（后置条件可空属性）数据的属性来克服这种不足。前置条件与调用者通信该值是否意图为 `null`，而后置条件则

## 表 6.1：可空属性

| 属性 | 类别 | 说明 |
| --- | --- | --- |
| AllowNull | precondition | 非可空输入参数。 |
| DisallowNull | precondition | 可空输入参数绝不应为 `null`。 |
| MaybeNull | postcondition | 非可空返回值可能为 `null`。 |
| NotNull | postcondition | 可空返回值绝不应为 `null`。 |
| MaybeWhen | postcondition | 可空输入参数可能为 `null`。 |
| NotNullWhen | postcondition | 可空输入参数不会为 `null`。 |
| NullIfNotNull | postcondition | 如果参数不为 `null`则返回值不为 `null`。 |

考虑例如 6.36 所示的遵循 try-get 的方法。

## 列表 6.36：使用 NullWhen 和 NotNotNull 属性

```csharp
using System.Diagnostics.CodeAnalysis;
static bool TryGetDigitAsText(char number, [NotNullWhen(true)] string text) =>
    text switch {
        '1' => "one",
        '2' => "two",
        // ...
        '9' => "nine",
        => null
```
