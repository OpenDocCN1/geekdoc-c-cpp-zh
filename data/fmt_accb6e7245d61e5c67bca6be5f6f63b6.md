
```csharp
public class Program
{
    public static void Main()
    {
        Employee employee = new();

        // 调用 FirstName 属性的 setter
        employee.FirstName = "Inigo";

        // 调用 FirstName 属性的 getter
        System.Console.WriteLine(employee.FirstName);

        // 调用 Title 属性的 setter
        employee.Title = "Manager";

        // 调用 Title 属性的 getter
        System.Console.WriteLine(employee.Title);

        // 调用 Manager 属性的 setter
        employee.Manager = "Computer Nerd";

        // 调用 Manager 属性的 getter
        System.Console.WriteLine(employee.Manager);
    }
}

public class Employee
{
    // FirstName 属性
    public string FirstName
    {
        get
        {
            return _FirstName;
        }
        set
        {
            _FirstName = value;
        }
    }
    private string _FirstName;

    // LastName 属性
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;

    // Title 属性
    public string Title
    {
        get => _Title;
        set => _Title = value;
    }
    private string _Title;

    // Manager 属性
    public string Manager
    {
        get => _Manager;
        set => _Manager = value;
    }
    private string _Manager;
    // ...
}
```

- 2. 从 `C# 3.0` 开始。

由于一个由 `get` 和 `set` 访问器进行分配和检索的单字段属性是如此简单且常见的，编译器允许在没有任何访问器实现或后台字段声明的情况下声明属性。输出 6.6 显示了 `Title` 和 `Manager` 属性的结果。

- 3. 从 `C# 6.0` 开始。

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee = new();

        // 调用 FirstName 属性的 setter
        employee.FirstName = "Inigo";

        // 调用 FirstName 属性的 getter
        System.Console.WriteLine(employee.FirstName);

        // 调用 Title 属性的 setter
        employee.Title = "Manager";

        // 调用 Title 属性的 getter
        System.Console.WriteLine(employee.Title);

        // 调用 Manager 属性的 setter
        employee.Manager = "Computer Nerd";

        // 调用 Manager 属性的 getter
        System.Console.WriteLine(employee.Manager);
    }
}

public class Employee
{
    // FirstName 属性
    public string FirstName
    {
        get
        {
            return _FirstName;
        }
        set
        {
            _FirstName = value;
        }
    }
    private string _FirstName;

    // LastName 属性
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;

    // Title 属性
    public string Title
    {
        get => _Title;
        set => _Title = value;
    }
    private string _Title;

    // Manager 属性
    public string Manager
    {
        get => _Manager;
        set => _Manager = value;
    }
    private string _Manager;
    // ...
}
```

输出 6.6

```
Inigo
Manager
Computer Nerd
```

# 第 6 章：类

输出 6.6

```
Inigo
```

自动实现属性属性提供了一种更简单的属性编写方式。此外，当对属性添加诸如验证逻辑时，任何调用该属性的代码将不再需要更改。

关于自动实现属性的最后一点注意是，可以像列表 19 所示对其进行初始化³：

```csharp
public string Salary { get; set; } = "Not Enough";
```

# 属性和字段指南

由于可以使用显式的 setter 方法而不是属性，有时会产生关于使用属性还是方法更好的问题。一般指南是：方法代表操作，而属性代表数据。预计调用属性的开销不会比访问字段大得多。

关于命名，注意在列表 19 中属性名是 `FirstName`，而字段名是 `_FirstName`——即带有下划线前缀的 PascalCase。属性的私有字段的其他命名约定包括 `_firstName` 以及有时使用的像局部变量一样的 camelCase⁴。然而，应该避免 camelCase 约定。这是因为用于属性名的 camelCase 与用于局部变量和参数的命名约定相同，这意味着名称重叠非常可能。此外，为了尊重封装原则，字段不应声明为公共。

无论你对私有字段使用何种命名模式，属性的代码标准都是 PascalCase。因此，属性应该使用名词、名词短语或形容词。例如，`Person` 对象上类型为 `Address` 的 `Address` 属性。事实上，属性名称与其类型相同的情况并不罕见。

我们倾向于使用 `_FirstName`，因为相比之下，名字前面的 `m` 是必要的。此外，通过使用与属性相同的大小写，在 Visual Studio 代码模板扩展工具中只需要一个字符串，而不需要为属性名和字段名都提供一个。

³ 从 `C# 6.0` 开始。

⁴ 参见 Microsoft 命名规范。

# 第 6 章：类

- 将所有实例字段声明为私有（并通过属性暴露它们）。
- 使用帕斯卡命名命名法（PascalCase）为属性命名。
- 优先使用自动实现属性而不是字段。
- 如果没有额外的实现逻辑，优先使用自动实现属性，而不是使用完全展开的属性。

## 使用带有验证的属性

请注意列表 6.20，`Employee` 类的 `Initialize()` 方法在赋值时也使用了属性而不是字段。虽然这不是强制要求的，但结果是属性设置器（setter）中的任何验证逻辑在类内部外部都会被调用。例如，考虑一下如果你更改 `LastName` 属性，使其在赋值给 `_LastName` 之前检查是否为空或空字符串，会发生什么。（记住，即使数据是非可空字符串，检查空值也是必要的，因为调用者可能禁用了可空引用类型，或者方法可能从 `C# 7.0` 或更早版本调用——即可空引用类型出现之前。）

## 列表 6.20：提供属性验证

```csharp
public class Employee
{
    // ...
    public void Initialize(
        string firstName, string lastName)
    {
        // 在 Employee 类内部 
        // 也使用属性
        FirstName = firstName;
        LastName = lastName;
    }
}

// LastName 属性
public string LastName
{
    get => _LastName;
    set
    {
        // ...
        // 验证 LastName 赋值
        ArgumentException.ThrowIfNullOrEmpty(value = value?.Trim()!);
        // ...
        _LastName = value;
    }
    private string _LastName;
}
```

通过这种新实现，如果为 `LastName` 分配了无效值，代码将抛出异常，无论来自同一类的其他成员，还是通过 `Program.Main()` 内部直接赋值给 `LastName`。拦截赋值并通过提供类似字段的 API 来验证参数的能力是属性的优势之一。

在属性实现内部访问备字段（backing field）是一个良好的做法。换句话说，你应该始终使用属性而不是直接调用字段。在许多情况下，这一原则即使对于属性所在类中的代码也适用。如果你遵循这一做法，你就可以添加诸如验证之类的代码，整个类将立即受益.^5

虽然罕见，但在设置器内部进行赋值是可能的，列表 6.20 所示。在这种情况下，对 `value.Trim()` 的调用删除了新姓值周围的任何空格。

![](img/ffe0f34eac7523830420733690014d17_359_0.png)

## 指南

- 避免在属性外部访问属性的备字段，即使是在包含类的内部也是如此。

> ^5. 如章节后文所述，这种例外发生在字段被标记为 `readonly` 时，因为此时值只能在构造函数中设置。在 `C# 6.0` 中，你可以直接为只读属性赋值，从而完全消除了对只读字段的需求。

## 只读和只写属性

通过移除属性的获取访问器（getter）或设置器（setter）部分，你可以更改属性的访问权限。仅包含设置器的属性是只写的，这相对罕见。同样，只提供获取访问器将导致属性变为只读；任何尝试赋值的尝试都会导致编译错误。例如，要使 `Id` 变为只读，你将使用列表 6.21 所示的代码。

## 列表 6.21：在 C# 6.0 之前定义只读属性

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee1 = new();
        employee1.Initialize(42);

        // 错误：属性或索引器 'Employee.Id'
        // 不能赋值；它是只读的
        employee1.Id = "498";
    }
}
```

```csharp
public class Employee
{
    public void Initialize(int id)
    {
        // 使用字段，因为 Id 属性没有设置器；
        // 它是只读的
        _Id = id.ToString();
    }

    // ...
    // Id 属性声明
    public string Id
    {
        get => _Id;
        // 未提供设置器
    }
    private string _Id;
}
```

列表 6.21 在 `Employee.Initialize()` 方法内部为字段赋值而不是属性（`_Id = id`）。通过属性赋值会导致编译错误，正如 `Program.Main()` 中发生的情况。

同时也支持只读的自动实现属性，^6 如下：

```csharp
public bool[] Cells { get; } = new bool[9];
```

关于只读自动实现属性的一个重要说明是，与只读字段一样，编译器要求此类属性通过自动属性初始化器（或在构造函数中）进行初始化。在前面的代码段中，我们使用了初始化器，但也允许从构造函数内部为 `Cells` 赋值，正如我们很快看到的。

根据字段不应从其封装属性外部访问的指南，程序员应该改用只读的、自动实现的属性。唯一的例外可能是只读可修改字段的数据类型与属性的数据类型不匹配——例如，如果字段是 `int` 类型，而只读属性是 `double` 类型。

> 指南

> **如果属性值不应更改，请创建只读属性。**

> **请创建只读的自动实现属性，而不是备字段。**

## 计算属性

在在某些情况下，你完全不需要备字段。相反，获取访问器返回一个计算值，而设置器则解析该值并将其持久化到其他字段中。例如，考虑列表 6.22 所示的 `Name` 属性。

## 列表 6.22：定义计算属性

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee1 = new();
        employee1.Name = "Inigo Montoya";
        Console.WriteLine(employee1.Name);
    }
}

public class Employee
{
    // ...
    public string Name
    {
        get => $"{FirstName} {LastName}";
        set 
        {
            // 将赋值的值拆分为姓和名
            string[] names;
            names = value.Split(new char[] { ' ' });
            if (names.Length == 2)
            {
                FirstName = names[0];
                LastName = names[1];
            }
            else
            {
                // 如果未分配全名，则抛出异常
                throw new ArgumentException("赋值的值 '{value}' 无效", nameof(value));
            }
        }
    }

    // FirstName 属性
    public string FirstName
    {
        get => _FirstName;
        set => _FirstName = value;
    }
    private string _FirstName;

    // LastName 属性
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;
}
```

## 输出 6.7

| Inigo Montoya |

## 获取访问器和设置器上的访问修饰符

如前所述，从属性外部访问字段不是良好的做法，因为这样做会绕过可能插入的验证或额外逻辑。

访问修饰符可以出现在属性实现的 get 或 set 部分（不能同时出现），从而覆盖属性声明中指定的访问修饰符。列表 6.23 展示了如何这样做。

## 列表 6.23：在设置器上放置访问修饰符

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee1 = new();
        employee1.Initialize(42);
        // 错误：属性或索引器 'Employee.Id'
        // 在在此文中中使用，因为设置访问器
        // 是不可用的
        employee1.Id = "496";
    }
}
```
