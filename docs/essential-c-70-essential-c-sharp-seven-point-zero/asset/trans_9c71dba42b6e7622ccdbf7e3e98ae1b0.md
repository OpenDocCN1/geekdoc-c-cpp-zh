

set => _FirstName = value;
}
private string _LastName;
// ...
}

在清单 6.18 中，我们对相同的属性实现使用了两种不同的语法。在实际代码中，请尽量保持语法选择的一致性。

## 自动实现的属性

在 C# 3.0 中，属性语法包含了另一个语法捷径。由于只有一个后备字段的属性通过 get 和 set 访问器进行赋值和检索非常简单且常见（参见 FirstName 和 LastName 的实现），C# 3.0（及更高版本）编译器允许声明属性时无需提供任何访问器实现或后备字段声明。清单 6.19 演示了使用 Title 和 Manager 属性的语法，输出 6.6 展示了结果。

### 清单 6.19：自动实现的属性

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 =
            new Employee();
        Employee employee2 =
            new Employee();

        // Call the FirstName property's setter
        employee1.FirstName = "Inigo";

        // Call the FirstName property's getter
        System.Console.WriteLine(employee1.FirstName);

        // Assign an auto-implemented property
        employee2.Title = "Computer Nerd";
        employee1.Manager = employee2;

        // Print employee1's manager's title
        System.Console.WriteLine(employee1.Manager.Title);
    }
}

class Employee
{
    // FirstName property
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

    // LastName property
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;

    public string Title { get; set; }

    public Employee Manager { get; set; }

    public string Salary { get; set; } = "Not Enough";
    // ...
}
```

**输出 6.6**

```
Inigo
Computer Nerd
```

自动实现的属性除了读取之外，提供了一种更简单的编写属性的方式。此外，当到了需要向 setter 添加诸如验证等功能的时候，即使属性声明已更改以包含实现，调用该属性的现有代码也不需要更改。

在本书的其余部分，我们经常使用这种 C# 3.0 或更高版本的语法，而不会特别指出这是 C# 3.0 引入的特性。

关于自动声明的属性，最后还有一点值得注意：在 C# 6.0 中，可以像清单 6.19 中对 Salary 那样初始化它们：

```
public string Salary { get; set; } = "Not Enough";
```

在 C# 6.0 之前，属性初始化仅能通过方法完成（包括构造函数，我们将在本章后面讨论）。然而，通过 C# 6.0，你可以在声明时使用类似于字段初始化的语法来初始化自动实现的属性。

## 属性和字段指南

鉴于有可能编写显式的 setter 和 getter 方法而不是属性，有时可能会出现关于使用属性还是方法更好的问题。一般指南是方法应表示操作，而属性应表示数据。属性旨在提供对简单数据及简单计算结果的简单访问。期望调用属性的开销不会显著高于访问字段。

关于命名，请注意，在清单 6.19 中，属性名为 FirstName，而字段名从之前的清单更改为 _FirstName——即带有下划线前缀的 PascalCase。支持属性的私有字段的另一种常见命名约定是 _firstName 和 m_FirstName（这是从 C++ 沿袭下来的，其中 m 代表成员变量），偶尔也会使用驼峰式命名法，就像局部变量一样。³ 然而，应避免使用驼峰式命名法。用于属性名称的驼峰式命名法与用于局部变量和参数的命名约定相同，这意味着名称重叠的可能性极高。此外，为了尊重封装原则，字段不应声明为 public 或 protected。

### 指南

- **务必** 使用属性来简单访问具有简单计算的简单数据。
- **避免** 从属性 getter 中抛出异常。
- **务必** 如果属性抛出异常，保留原始属性值。
- **务必** 在不需要额外逻辑时，优先使用自动实现的属性，而不是带有简单后备字段的属性。

> 3. 我们更喜欢 _FirstName，因为与下划线 (\_) 相比，名称前的 *m* 是不必要的。此外，通过使用与属性相同的命名法，在 Visual Studio 代码模板扩展工具中，我们只需要一个字符串，而无需分别为属性名和字段名各准备一个字符串。

无论您对私有字段使用哪种命名模式，属性的编码标准均为 PascalCase。因此，属性应使用 LastName 和 FirstName 模式，其名称应为名词、名词短语或形容词。属性名与类型名相同的情况并不少见。例如，Person 对象上类型为 Address 的 Address 属性。

![](img/ef6a8a417630b222bfb3f3b949facff0_304_0.png)

## 使用带验证的属性

注意清单 6.20 中，Employee 的 Initialize() 方法在赋值时也使用了属性而不是字段。虽然这不是必须的，但结果是，属性 setter 中的任何验证都会在类和类外被调用。例如，考虑一下如果你修改 LastName 属性，使其在将值分配给 _LastName 之前检查 value 是否为 null 或空字符串，会发生什么。

**清单 6.20：提供属性验证**

```csharp
class Employee
{
    // ...
    public void Initialize(
        string newFirstName, string newLastName)
    {
        // Use property inside the Employee
        // class as well
        FirstName = newFirstName;
        LastName = newLastName;
    }

    // LastName property
    public string LastName
    {
        get => _LastName;
        set
        {
            // Validate LastName assignment
            if (value == null)
            {
                // Report error
                // In C# 6.0 replace "value" with nameof(value)
                throw new ArgumentNullException("value");
            }
            else
            {
                // Remove any whitespace around
                // the new last name
                value = value.Trim();
                if (value == "")
                {
                    // Report error
                    // In C# 6.0 replace "value" with nameof(value)
                    throw new ArgumentException(
                          "LastName cannot be blank.", "value");
                }
                else
                {
                    _LastName = value;
                }
            }
        }
    }

    private string _LastName;
    // ...
}
```

通过这种新的实现，如果 LastName 被分配了无效值，无论是来自同一类的其他成员，还是通过 Program.Main() 内部对 LastName 的直接赋值，代码都会抛出异常。通过提供类似字段的 API 来拦截赋值并验证参数的能力，是属性的一大优势。

- 1. 向 Teller、Cher、Sting、Madonna、Bono、Prince、Liberace 等人道歉。

良好的实践是仅在属性实现内部访问属性的后备字段。换句话说，你应该始终使用属性，而不是直接调用字段。在许多情况下，即使是在与该属性相同的类内的代码中，这一原则也适用。如果你遵循这种做法，当你添加诸如验证代码之类的代码时，整个类立即就能从中受益。⁵

虽然罕见，但可以在 setter 内部对 value 进行赋值，如清单 6.20 所示。在这种情况下，对 `value.Trim()` 的调用会移除新姓氏值周围的空白字符。

## 指南

- **避免** 在属性外部（即使是在包含类内部）访问属性的后备字段。
- **务必** 在创建 `ArgumentException()` 或 `ArgumentNullException()` 类型的异常时，使用 "value" 作为 paramName 参数（"value" 是属性 setter 中参数的隐式名称）。

## 高级主题

### nameof 操作符

如果在属性验证过程中确定新值的赋值无效，则有必要抛出异常——通常为 `ArgumentException()` 或 `ArgumentNullException()` 类型。这两种异常都接受一个名为 `paramName` 的字符串参数，用于标识无效参数的名称。在清单 6.20 中，我们将 "value" 作为此参数的参数传递，但 C# 6.0 提供了使用 `nameof` 操作符的改进。`nameof` 操作符接受一个标识符，如 `value` 变量，并返回该名称的字符串表示——在本例中为 "value"。

5. 如本章后面所述，存在一个例外情况，即当字段被标记为只读时，因为那时值只能在构造函数中设置。在 C# 6.0 中，可以直接赋值只读属性的值，从而完全消除对只读字段的需求。

