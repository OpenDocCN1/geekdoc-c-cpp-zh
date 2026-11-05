
```csharp
Report report = new Report();
Printer<Report> printer = new Printer<Report>();
printer.PrintItem(report);
}
}
```

### [执行结果]

Printing report...

此示例定义了一个泛型类 `Printer<T>`，并带有 `where T : IPrintable` 约束。这意味着不能将 `Printer<T>` 与任何未实现 `IPrintable` 的类型一起使用。

这样做的好处是类型安全——编译器知道 `T` 始终会有 `Print()` 方法，因此可以避免运行时错误。

也可以使用多个约束：

```csharp
where T : class, new(), IPrintable
```

这意味着：

- `T` 必须是类（而不是结构体），
- 必须具有无参构造函数（`new()`），
- 并且必须实现 `IPrintable`。

约束是编写可复用且安全代码的强大工具。

### [补充]

可以将泛型参数约束为基类、接口，或约束为 `struct`、`class` 或 `new()`。

`where` 子句有助于 IDE 中的智能感知建议，因为编译器对该类型了解得更多。

泛型方法可以具有与其所在类不同的约束。

约束仅在编译时强制执行，这提高了可靠性，而无需运行时检查。

`dynamic` 关键字会禁用编译时检查。编译器相信你尝试执行的操作在运行时能够正常工作。

这在以下情况下很有用：

- 使用 COM 对象，或与 Python 或 JavaScript 等动态语言交互时。
- 读取编译时类型未知的 JSON 或 XML 时。

但它很危险：

如果调用一个不存在的方法，程序会成功编译，但会在运行时因 `RuntimeBinderException` 而崩溃。

使用 `dynamic` 是以安全性换取灵活性。仅在绝对必要时，并且你对运行时行为有信心时才使用它。

### [补充]

`dynamic` 是在 C# 4.0 中引入的。

它是 DLR（动态语言运行时）的一部分。

对动态变量的任何操作都在运行时解析，而 `var` 则在编译时解析。

IDE 通常不会为动态对象提供智能感知。

## 31. 使用反射在运行时检查和使用类型

反射让你可以在 C# 运行时检查类型（类、方法、属性等）并与它们交互。

下面是一个使用反射检查类并动态调用方法的简单示例。

### [代码示例]

```csharp
using System;
using System.Reflection;

public class HelloWorld
{
    public void SayHello()
    {
        Console.WriteLine("Hello from reflection!");
    }
}

class Program
{
    static void Main()
    {
        // Get the type info of the HelloWorld class
        Type type = typeof(HelloWorld);

        // Create an instance of HelloWorld dynamically
        object instance = Activator.CreateInstance(type);

        // Get the method info for SayHello
        MethodInfo method = type.GetMethod("SayHello");

        // Invoke the SayHello method on the instance
        method.Invoke(instance, null);
    }
}
```

### [执行结果]

Hello from reflection!

### 逐步解释：

- `typeof(HelloWorld)` 获取 `HelloWorld` 类的 `Type` 对象。该对象包含有关该类的元数据。
- `Activator.CreateInstance(type)` 动态创建 `HelloWorld` 的实例。无需直接使用 `new HelloWorld()`。
- `type.GetMethod("SayHello")` 检索名为 `"SayHello"` 的方法的元数据。
- `method.Invoke(instance, null)` 实际在创建的实例上调用该方法。

### 为什么这很强大？

- 可以构建灵活的系统，例如插件加载器、对象映射器或测试框架。
- 当你在编译时不知道确切类型时很有用。

### 常见陷阱：

- 反射比直接调用慢。
- 会失去编译时检查——拼错的方法名直到运行时才会被发现。

### [补充]

- 反射是 `System.Reflection` 命名空间的一部分。
- 可以检查字段、属性、构造函数、接口等，而不仅仅是方法。
- ASP.NET Core 在内部使用反射进行依赖注入和路由。
- 可以将反射与自定义特性结合使用，以实现强大的行为。

## 32. 将特性用作元数据标记

特性就像添加到代码中的特殊标记。它们添加了工具或基于反射的代码可以读取的额外信息（元数据）。

下面是一个使用反射定义和读取自定义特性的示例。

### [代码示例]

```csharp
using System;
using System.Reflection;

// Define a custom attribute
[AttributeUsage(AttributeTargets.Class)]
public class InfoAttribute : Attribute
{
    public string Message { get; }
    public InfoAttribute(string message)
    {
        Message = message;
    }
}

// Apply the custom attribute to a class
[Info("This class does something important.")]
public class ImportantClass
{
}

class Program
{
    static void Main()
    {
        // Get type information
        Type type = typeof(ImportantClass);
        // Check if the attribute is applied
        if (Attribute.IsDefined(type, typeof(InfoAttribute)))
        {
            // Get the attribute instance
            InfoAttribute attr = (InfoAttribute)Attribute.GetCustomAttribute(type, typeof(InfoAttribute));
            Console.WriteLine("Attribute message: " + attr.Message);
        }
    }
}
```

### [执行结果]

Attribute message: This class does something important.

### 逐步解释：

- `[AttributeUsage(AttributeTargets.Class)]` 指定特性的使用位置（例如，可用于类）。
- `InfoAttribute` 是一个存储消息的自定义特性类。
- `[Info("...")]` 将该特性应用于 `ImportantClass`。
- `Attribute.IsDefined(...)` 检查该特性是否存在。
- `Attribute.GetCustomAttribute(...)` 检索实际实例，以便你可以读取 `Message` 属性。

### 为什么使用特性？

- 它们添加结构化、可检索的元数据。
- 在框架中很常见——例如，`[Serializable]`、`[Obsolete]` 或 `[HttpGet]`。

### 实际应用：

- 在 ASP.NET 中，特性定义路由：`[HttpPost("login")]`
- 在单元测试中：`[TestMethod]`
- 在 Unity 游戏开发中：`[SerializeField]`

### [补充]

- 特性必须继承自 `System.Attribute`。
- 内置特性包括 `[Obsolete]`、`[Serializable]`、`[DllImport]` 等。
- 可以在特性构造函数中定义位置参数和命名参数。
- 反射用于在运行时访问这些特性，使它们对于框架级决策非常强大。

## 33. 匿名类型是不可变的，并在编译时定义

匿名类型是没有显式定义类名的对象。它们用于快速对数据进行分组，尤其在 LINQ 查询中很有用。创建后，其属性是只读的，无法更改。

下面是一个创建和使用匿名类型的简短示例。

### [代码示例]

```csharp
using System;

class Program
{
    static void Main()
    {
        // Creating an anonymous type with two properties
        var person = new { Name = "Alice", Age = 30 };
        // Accessing the properties
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
        // person.Age = 31; // This line would cause a compile-time error because properties are read-only
    }
}
```

### [执行结果]

Name: Alice, Age: 30

匿名类型使用 `new { }` 语法定义。它们主要用于以下情况：

- 需要一个用于临时用途的简单数据结构。
- 不想为仅保存少量数据而创建完整类。

编译器会自动推断类型并生成具有只读属性的类。只能在方法内部定义它们（不能作为类成员）。

### 重要说明：

- 不能向匿名类型添加方法。
- 创建后，不能修改或添加新属性。
- 不能从方法返回匿名类型，除非使用 `dynamic`，或者返回到创建它的同一作用域。

### [补充]

- 匿名类型是引用类型。
- 它们的属性名称和类型决定其类型标识——如果两个匿名类型具有相同的属性和顺序，则仅在同一程序集内被视为相同类型。
- 它们通常与 LINQ 一起使用，将数据投影为新形状而无需定义新类型。
