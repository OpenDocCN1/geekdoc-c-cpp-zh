
并且已授予相应的权限。从远程位置运行的程序需要显式授予此类权限。

![](img/ef6a8a417630b222bfb3f3b949facff0_766_0.png)

**图 18.1：MemberInfo 派生类**

![](img/ef6a8a417630b222bfb3f3b949facff0_767_0.png)

## 泛型类型的反射

公共语言运行时（CLR）2.0 版本引入了泛型类型，这使得需要增加额外的反射特性。对泛型的运行时反射用于确定类或方法是否包含泛型类型以及它可能包含的任何类型参数或实参。

### 确定类型参数的类型

就像你可以使用 *typeof* 运算符配合非泛型类型来获取 `System.Type` 的实例一样，你也可以在泛型类型或泛型方法的类型参数上使用 *typeof* 运算符。列表 18.4 展示了在 *Stack* 类的 *Add* 方法中对类型参数应用 *typeof* 运算符的例子。

**列表 18.4：声明 Stack<> 类**

```
public class Stack<T>
{
 // ...
 public void Add(T i)
 {
 // ...
 Type t = typeof(T);
 // ...
 }
 // ...
}
```

一旦你获得了类型参数 *Type* 对象的实例，你就可以对该类型参数本身使用反射来确定其行为，并更有效地将 *Add* 方法定制到特定类型。

### 确定类或方法是否支持泛型

在 CLR 2.0 版本的 `System.Type` 类中，添加了几个方法来确定给定的类型是否支持泛型参数和实参。泛型实参是在实例化泛型类时提供的类型参数。你可以通过查询 `Type.ContainsGenericParameters` 属性来确定类或方法是否包含尚未设置的泛型参数，如列表 18.5 所示。

**列表 18.5：使用泛型进行反射**

```csharp
using System;

public class Program
{
    static void Main()
    {
        Type type;
        type = typeof(System.Nullable<>);
        Console.WriteLine(type.ContainsGenericParameters);
        Console.WriteLine(type.IsGenericType);

        type = typeof(System.Nullable<DateTime>);
        Console.WriteLine(!type.ContainsGenericParameters);
        Console.WriteLine(type.IsGenericType);
    }
}
```

输出 18.3 展示了列表 18.5 的结果。

**输出 18.3**

```
True
True
True
True
```

Type.IsGenericType 是一个布尔属性，用于评估类型是否为泛型。

### 获取泛型类或方法的类型参数

你可以通过调用 GetGenericArguments( ) 方法从泛型类中获取泛型实参（或类型参数）的列表。结果是一个 System.Type 实例数组，其顺序对应于它们作为泛型类的类型参数声明的顺序。列表 18.6 对泛型类型进行反射并获取每个类型参数；输出 18.4 展示了结果。

**列表 18.6：使用泛型类型进行反射**

```csharp
using System;
using System.Collections.Generic;

public partial class Program
{
    public static void Main()
    {
        Stack<int> s = new Stack<int>();

        Type t = s.GetType();

        foreach (Type type in t.GetGenericArguments())
        {
            System.Console.WriteLine(
                "Type parameter: " + type.FullName);
        } // ...
    }
}
```

**输出 18.4**

```
Type parameter: System.Int32
```

## nameof 运算符

我们在第 11 章中简要提到了 nameof 运算符，其中它被用于提供参数异常中参数的名称：

```
throw new ArgumentException(
    "The argument did not represent a digit", nameof(textDigit));
```

该上下文关键字在 C# 6.0 中引入，它生成一个包含指定为参数的程序元素非限定名称的常量字符串。在这种情况下，textDigit 是方法的参数，因此 nameof(textDigit) 返回“textDigit”。（鉴于此活动发生在编译时，nameof 从技术上讲不是反射。我们将它包含在此处，因为它最终会接收有关程序集及其结构的数据。）

你可能会问，与简单地使用 "textDigit" 相比，使用 nameof(textDigit) 有什么优势（特别是对于某些程序员来说，后者甚至可能看起来更容易使用）。优势有两个方面：

- C# 编译器确保 nameof 运算符的参数实际上是一个有效的程序元素。这有助于在程序元素名称更改时防止错误，帮助防止拼写错误等等。
- IDE 工具在处理 nameof 运算符时比处理字面字符串表现得更好。例如，“查找所有引用”工具可以找到 nameof 表达式中提到的程序元素，但找不到字面字符串中提到的。自动重命名重构也表现得更佳，等等。

在之前给出的片段中，nameof(textDigit) 生成了参数的名称。然而，nameof 运算符可以与任何程序元素一起工作。例如，列表 18.7 使用 nameof 将属性名称传递给 INotifyPropertyChanged.PropertyChanged。

**列表 18.7：动态调用成员**

```csharp
using System.ComponentModel;

public class Person : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
    public Person(string name)
    {
        Name = name;
    }
    private string _Name;
    public string Name
    {
        get { return _Name; }
        set
        {
            if (_Name != value)
            {
                _Name = value;
                // 使用 C# 6.0 条件空引用
                PropertyChanged?.Invoke(
                    this,
                    new PropertyChangedEventArgs(
                        nameof(Name)));
            }
        }
    }
    // ...
}
```

请注意，无论提供的是非限定的“Name”（因为它在作用域内）还是完全（或部分）限定名称（如 Person.Name），结果都只是最终的标识符（点号名称中的最后一个元素）。你仍然可以使用 C# 5.0 的 CallerMemberName 参数特性来获取属性的名称；参见 http://itl.tc/CallerMemberName 查看示例。

## 特性

在深入了解如何编程特性之前，我们应该考虑一个用例来展示它们的实用性。在列表 18.3 的 `CommandLineHandler` 示例中，你根据与属性名称匹配的命令行选项动态设置类的属性。然而，当命令行选项是无效的属性名称时，这种方法是不够的。例如，`/?` 无法得到支持。此外，这种机制没有提供区分哪些选项是必需的，哪些是可选的方法。

与其依赖于选项名称和属性名称之间的精确匹配，你可以使用特性来标识被修饰构造的额外元数据——在这种情况下，是特性所修饰的选项。使用特性，你可以将一个属性标记为 `Required` 并提供一个 `/ ?` 选项别名。换句话说，特性是一种将额外数据与属性（以及其他构造）关联起来的手段。

特性出现在方括号内，位于它们修饰的构造之前。例如，你可以修改 `CommandLineInfo` 类以包含特性，如列表 18.8 所示。

**列表 18.8：使用特性修饰属性**

```csharp
class CommandLineInfo
{
    [CommandLineSwitchAlias("?")]
    public bool Help { get; set; }
    [CommandLineSwitchRequired]
    public string Out { get; set; }
    public System.Diagnostics.ProcessPriorityClass Priority { get; set; } =
    System.Diagnostics.ProcessPriorityClass.Normal;
}
```

在列表 18.8 中，`Help` 和 `Out` 属性被特性修饰。这些特性的目的是允许 `/Help` 的别名 `/?`，并指示 `/Out` 是必需参数。其思想是在 `CommandLineHandler.TryParse()` 方法内部，你启用对选项别名的支持，并且在假设解析成功的情况下，检查是否指定了所有必需的开关。

