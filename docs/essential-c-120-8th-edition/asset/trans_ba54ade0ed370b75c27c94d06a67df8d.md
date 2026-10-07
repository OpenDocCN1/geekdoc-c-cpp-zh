

# 带有构造函数的非可空引用类型属性

- 后备字段被声明为可空，以避免编译器产生该字段未初始化的警告。
- 访问器器使用 null 忽略运算符（null-forgiveness operator）返回字段——声明由于设置器的验证，该字段不为 null。

对于非可空属性，将后备字段声明为 null 似乎是不合逻辑的。然而，这是必要的，因为编译器对构造函数之外的非空字段/属性赋值是不感知的。幸运的是，在这种情况下，你作为程序员，在返回字段时使用 null 忽略运算符是合理的，因为设置器中的非空检查确保了字段（在赋值前）为空。

# 只读自动实现的引用类型属性

正如本节早些指出的，非空自动实现的引用类型属性需要是只读的，以避免无效的 null 赋值。然而，你仍然需要验证实例化期间可能赋值的任何参数，如列表 6.37 所示。

> 列表 6.37：非空引用类型自动实现属性的验证

```csharp
public class Employee {
    public Employee(string name) {
        Name = name ?? throw new ArgumentNullException(nameof(name));
    }
    public string Name { get; }
}
```

人们可能会争论是否允许非空自动实现的引用类型属性具有私有设置器。虽然这是可能的，但更合适的问题是你的类是否会误将 null 赋值给属性。如果你不在设置器中使用验证来封装字段，你能够确定自己不会错误地赋值 null 值吗？虽然编译器会在实例化期间验证你的意图，但开发者是否总是记得对进入类的本应为非空的值进行 null 检查是怀疑的——正如列表 6.37 所示的构造函数那样。

### 指南

- **必须**实现带有可空后备字段的非空读/写完全实现属性，在从访问器返回字段时使用 null 忽略运算符，并在属性设置器中进行非空验证。
- **必须**在实例化完成之前为非空引用类型属性赋值。
- **必须**将非空引用类型自动实现属性实现为只读。
- **必须**对所有在实例化完成前未定义的引用类型属性和字段使用可空检查。

# required 修饰符

在 C# 11 中，设计人员增加了将字段或属性标记为 `required` 的能力。这将其指定为“要求的”，以便它们必须在构造期间在对象初始化器内部赋值（见列表 6.38）。

列表 6.38：使用 Required 修饰符

```csharp
public class Book
{
    string? _Title;
    public required string Title
    {
        get
            return _Title!;
        set
        {
            _Title = value ?? throw new ArgumentNullException(nameof(value));
        }
    }

    string? _Isbn;

    public required string Isbn
    {
        get {
            return _Isbn!;
        }
        set {
            _Isbn = value ?? throw new ArgumentNullException(nameof(value));
        }
    }

    public string? Subtitle { get; set; }
    //...
}

public class Program
{
    public static void Main() {
        //...
        Book book = new() {
            Isbn = "978-01335972267",
            Title = "Harold and the Purple Crayon"
        };
    }
}
```

通过添加 `required` 修饰符，我们无法在不提供一个为 Isbn 码和 Title 提供值的对象初始化器的情况下实例化书籍（见列表 6.39）。

列表 6.30：在对象初始化器中指定要求的成员

```csharp
// 错误 CS9835:
// 要求的成员 'Book.Isbn' 必须在对象初始化器
// 或属性构造函数中设置
Book book = new() { Title="Essential C#" };
//...
```

# 第 6 章：类

注意，由于我们没有为 Book 包含显式构造函数，我们依赖于自动生成的默认构造函数来实例化 Book。这是理想的，因为要求的成员定义了如何构造对象以代替任何构造函数。为要求的成员提供带参数的构造函数将导致既需要在构造函数参数中指定值，又需要在对象初始化器中冗余指定值。例如，带有 Title 参数的构造函数将导致如下实例化：

```csharp
Book book = new("A People's History of the United States")
{
    Title = "A People's History of the United States",
    Isbn = "978-0062397348";
};
```

为了避免这种冗余，你可以用 `SetsRequiredMembers` 特性修饰构造函数，指示编译器在调用关联构造函数时禁用所有对象初始化器要求。有效来说，`SetsRequiredMembers` 属性告诉编译器开发者将负责设置所有要求的成员，因此编译器可以忽略对初始化赋值的检查。遗憾的是，几乎没有验证这种初始化是否发生过——编译器并不检查。请查看列表 6.40 的如何使用 `SetsRequiredMembers` 属性的示例。

列表 6.40：禁用要求的对象初始化

```csharp
[SetsRequiredMembers]
public Book(int id)
{
    Id = id;

    // 查找书籍数据
    //...
//...
}
```

并且，鉴于这样的构造函数，我们可以实例化书籍：

```csharp
Book book = new(42) {
    Subtitle = "The Comprehensive Guide"
};
```

# 带有构造函数的非可空引用类型属性

对于非可空属性，将后备字段声明为 null 似乎是不合逻辑的。然而，这是必要的，因为编译器对构造函数之外的非空字段/属性赋值是不感知的。幸运的是，在这种情况下，你作为程序员，在返回字段时使用 null 忽略运算符是合理的，因为设置器中的非空检查确保了字段（在赋值前）为空。

# 只读自动实现的引用类型属性

正如本节早些指出的，非空自动实现的引用类型属性需要是只读的，以避免无效的 null 赋值。然而，你仍然需要验证实例化期间可能赋值的任何参数，如列表 6.37 所示。

# required 修饰符

在 C# 11 中，设计人员增加了将字段或属性标记为 `required` 的能力。这将其指定为“要求的”，以便它们必须在构造期间在对象初始化器内部赋值（见列表 6.38）。

通过添加 `required` 修饰符，我们无法在不提供一个为 Isbn 码和 Title 提供值的对象初始化器的情况下实例化书籍（见列表 6.39）。

# 第 6 章：类

注意，由于我们没有为 Book 包含显式构造函数，我们依赖于自动生成的默认构造函数来实例化 Book。这是理想的，因为要求的成员定义了如何构造对象以代替任何构造函数。为要求的成员提供带参数的构造函数将导致既需要在构造函数参数中指定值，又需要在对象初始化器中冗余指定值。例如，带有 Title 参数的构造函数将导致如下实例化：

为了避免这种冗余，你可以用 `SetsRequiredMembers` 特性修饰构造函数，指示编译器在调用关联构造函数时禁用所有对象初始化器要求。有效来说，`SetsRequiredMembers` 属性告诉编译器开发者将负责设置所有要求的成员，因此编译器可以忽略对初始化赋值的检查。遗憾的是，几乎没有验证这种初始化是否发生过——编译器并不检查。请查看列表 6.40 的如何使用 `SetsRequiredMembers` 属性的示例。

# 可空属性

与其禁用可空类型或可空警告，有时为编译器提供关于可空意图的提示是有帮助的。这可以通过直接放入代码中的元数据——属性来实现（见第 18 章）。共有七种不同的可空属性，每个都定义在 `System.Diagnostics.CodeAnalysis` 命名空间中，并识别为前置条件或后置条件（表 6.1）。

| 特性 | 类别 |  |
|---|---|---|
| AllowNull | 前置条件 | 非空输入参数可能为 null。 |
| DisallowNull | 前置条件 | 可空输入参数不应为 null。 |
| MaybeNull | 后置条件 | 非空返回值可能为 null。 |
| NotNull | 后置条件 | 可空返回值永远不为 null。 |
| MaybeNullWhen | 后置条件 | 方法返回指定的 bool 值时，非空输入参数可能为 null。 |
| NotNullWhen | 后置条件 | 方法返回指定的 bool 值时，可空输入参数不会为 null。 |
| NullIfNotNull | 后置条件 | 如果指定参数的值不为 null，则返回值不为 null。 |

