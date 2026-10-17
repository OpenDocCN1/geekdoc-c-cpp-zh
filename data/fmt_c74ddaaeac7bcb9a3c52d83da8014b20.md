
```csharp
// The iterator is expanded into the following
// code by the compiler
public virtual IEnumerator<T> GetEnumerator()
{
    __ListEnumerator result = new __ListEnumerator(0);
    result._Pair = this;
    return result;
}
public virtual System.Collections.IEnumerator
    System.Collections.IEnumerable.GetEnumerator()
{
    return new GetEnumerator();
}
private sealed class __ListEnumerator<T> : IEnumerator<T>
{
    public __ListEnumerator(int itemCount)
    {
        _ItemCount = itemCount;
    }
    Pair<T> _Pair;
    T _Current;
    int _ItemCount;
    public object Current
    {
        get
        {
            return _Current;
        }
    }
    public bool MoveNext()
    {
        switch (_ItemCount)
        {
            case 0:
                _Current = _Pair.First;
                _ItemCount++;
                return true;
            case 1:
                _Current = _Pair.Second;
                _ItemCount++;
                return true;
            default:
                return false;
        }
    }
}
```

由于编译器接受 `yield return` 语句并生成对应于你通常会手动编写的类的代码，C# 中的迭代器表现出与手动实现枚举器设计模式的类相同的性能特征。虽然没有性能提升，但程序员生产力的提升是显著的。

# 高级主题

## 上下文关键字

许多 C# 关键字是“保留”的，除非在前面加上 `@` 符号，否则不能用作标识符。`yield` 关键字是一个上下文关键字，而不是保留关键字；声明名为 `yield` 的局部变量是合法的（尽管令人困惑）。事实上，C# 1.0 版本之后添加的所有关键字都是上下文关键字；这有助于防止在将现有程序升级以使用语言新版本时意外破坏代码。

如果 C# 设计者选择使用 `yield value;` 而不是 `yield return value;` 作为迭代器产出的语法，将会引入一种可能的歧义：`yield(1+2);` 现在可能是在产出一个值，也可能是在将值传递给名为 `yield` 的方法作为参数。

由于以前从未合法地允许标识符 `yield` 紧挨在 `return` 或 `break` 之前，C# 编译器知道这种 `yield` 的用法必须是作为关键字，而不是标识符。

## 在单个类中创建多个迭代器

之前的迭代器示例实现了 `IEnumerable<T>.GetEnumerator()`——这是 `foreach` 隐式寻找的方法。有时你可能希望有不同的迭代序列，例如反向迭代、过滤结果或迭代对象的其他投影（而不是默认的）。你可以通过将它们封装在返回 `IEnumerable<T>` 或 `IEnumerable` 的属性或方法中，在类中声明额外的迭代器。例如，如果你想反向迭代 `Pair<T>` 的元素，你可以提供一个 `GetReverseEnumerator()` 方法，如清单 17.20 所示。

### 列表 17.20：在返回 `IEnumerable<T>` 的方法中使用 `yield return`

```csharp
public struct Pair<T> : IEnumerable<T>
{
    // ...
    public IEnumerable<T> GetReverseEnumerator()
    {
        yield return Second;
        yield return First;
    }
    // ...
}
public void Main()
{
    var game = new Pair<string>("Redskins", "Eagles");
    foreach (string name in game.GetReverseEnumerator())
    {
        Console.WriteLine(name);
    }
}
```

请注意，你返回的是 `IEnumerable<T>`，而不是 `IEnumerator<T>`。这与 `IEnumerable<T>.GetEnumerator()` 不同，后者返回 `IEnumerator<T>`。`Main()` 中的代码演示了如何使用 `foreach` 循环调用 `GetReverseEnumerator()`。

## `yield` 语句要求

你只能在对 `IEnumerator<T>` 或 `IEnumerable<T>` 类型（或其非泛型等价物）进行返回的成员中使用 `yield return` 语句。包含 `yield return` 语句的成员体中不能有简单的 `return`。如果成员使用了 `yield return` 语句，C# 编译器会生成必要的代码来维护迭代器的状态。相反，如果成员使用的是 `return` 语句而非 `yield return`，则程序员负责维护其自身的状态机并返回迭代器接口之一的实例。此外，正如在具有 `return` 类型的方法中，所有代码路径必须包含伴随值的 `return` 语句（假设它们不抛出异常），如果迭代器要返回任何数据，其所有代码路径也必须包含 `yield return` 语句。

如果对 `yield` 语句的以下额外限制被违反，将导致编译器错误：

- `yield` 语句只能出现在方法、用户定义运算符或索引器或属性的 get 访问器内部。该成员不能接受任何 ref 或 out 参数。
- `yield` 语句不能出现在匿名方法或 lambda 表达式（见第 13 章）内部的任何位置。
- `yield` 语句不能出现在 `try` 语句的 catch 和 finally 子句中。此外，只有当没有 catch 块时，`yield` 语句才能出现在 try 块中。

## 总结

在本章中，我们回顾了主要的集合类，以及它们如何根据所支持的接口归入不同类别。每个类都专注于向集合中插入项目以及从集合中检索项目，使用的机制包括按键、按索引，或者按 FIFO（先进先出）或 LIFO（后进先出）等。我们还探讨了如何迭代集合。此外，本章还解释了如何定义带有自定义迭代器的自定义集合，以便枚举集合内的项目。（迭代器涉及一个上下文关键字 `yield`，C# 用它来生成实现 `foreach` 循环所使用的迭代器模式的底层 CIL 代码。）

在第 18 章中，我们将探讨反射（Reflection），这是一个在前面简要提及但几乎没有解释的话题。反射允许我们在运行时检查 CIL 代码中类型的结构。

# 18 反射、特性与动态编程

特性（Attributes）是一种向程序集插入额外元数据并将该元数据与诸如类、方法或属性等编程构造关联起来的手段。本章将调查内置于框架中的特性的细节，并描述如何定义自定义特性。为了利用自定义特性，必须识别它们。这通过反射来实现。本章从介绍反射开始，包括如何使用它在执行时基于成员调用的名称（或元数据）在编译时进行动态绑定。反射经常在代码生成器等工具中被利用。此外，当调用目标未知时，会在执行时使用反射。

![](img/ef6a8a417630b222bfb3f3b949facff0_757_0.png)

本章以对动态编程的讨论结束，这是 C# 4.0 中新增的一项功能，极大地简化了处理动态数据以及需要执行时而非编译时绑定的情况。

## 反射

使用反射，可以做到以下几点。

- 访问程序集内类型的元数据。这包括诸如完整类型名称、成员名称以及装饰该构造的任何特性等构造。
- 使用元数据在运行时动态调用类型的成员，而不是使用编译时定义的绑定。

反射是检查程序集内元数据的过程。传统上，当代码编译成机器语言时，关于代码的所有元数据（如类型和方法名称）都会被丢弃。相比之下，当 C# 编译成公共中间语言（CIL）时，它会保留关于代码的大部分元数据。此外，使用反射，可以枚举程序集内的所有类型，并搜索符合某些条件的类型。你通过 `System.Type` 的实例访问类型的元数据，该对象包含用于枚举类型实例成员的方法。此外，可以在属于被检查类型的对象上调用这些成员。

反射设施使许多否则无法使用的新范式成为可能。例如，反射允许你枚举程序集内的所有类型及其成员，并在此过程中创建存根以记录程序集 API。然后，你可以将从反射获取的元数据与从 XML 注释生成的 XML 文档（使用 `/doc` 开关）结合，创建 API 文档。类似地，程序员使用反射元数据来生成将业务对象持久化（序列化）到数据库的代码。它还可以用于显示对象集合的列表控件。给定一个集合，列表控件可以使用反射迭代集合中对象的所有属性，为每个属性定义列表中的一列。此外，通过在每个对象上调用每个属性，即使对象的数据类型在编译时未知，列表控件也可以将每个行和列填充为对象中包含的数据。

`XmlSerializer`、`ValueType` 和 Microsoft .NET Framework 的 `DataBinder` 也是框架中几个使用反射作为其实现部分的类。

## 使用 System.Type 访问元数据

读取类型元数据的关键是获取代表目标类型实例的 `System.Type` 实例。`System.Type` 提供了检索类型信息的所有方法。你可以用它来回答如下的问题：

- 类型的名称是什么 (`Type.Name`)？
- 类型是否是公共的 (`Type.IsPublic`)？
- 类型的基础类型是什么 (`Type.BaseType`)？
- 类型是否支持任何接口 (`Type.GetInterfaces()`)？
- 类型定义在哪个程序集中 (`Type.Assembly`)？
- 类型的属性、方法、字段等是什么 (`Type.GetProperties()`, `Type.GetMethods()`, `Type.GetFields()`, 等等)？
- 哪些特性装饰该类型 (`Type.GetCustomAttributes()`)？

还有更多这样的成员，但它们都提供关于特定类型的信息。关键是获取对该类型的 `Type` 对象的引用，主要方法是通过 `object.GetType()` 和 `typeof()`。

请注意，`GetMethods()` 调用不返回扩展方法。这些方法只能作为实现类型上的静态成员可用。

### GetType()

`object` 包含一个 `GetType()` 成员，因此，所有类型都包含此函数。你调用 `GetType()` 以检索对应于原始对象的 `System.Type` 实例。列表 18.1 演示了这一过程，使用了来自 `DateTime` 的 `Type` 实例。输出 18.1 显示了结果。

**列表 18.1：** 使用 `Type.GetProperties()` 获取对象的公共属性

```csharp
DateTime dateTime = new DateTime();
Type type = dateTime.GetType();
foreach (
    System.Reflection.PropertyInfo property in
    type.GetProperties() )
{
    Console.WriteLine(property.Name);
}
```

**输出 18.1**

![](img/ef6a8a417630b222bfb3f3b949facff0_760_0.png)

调用 `GetType()` 后，你遍历从 `Type.GetProperties()` 返回的每个 `System.Reflection.PropertyInfo` 实例并显示属性名称。调用 `GetType()` 的关键是你必须有一个对象实例。然而，有时并没有这样的实例可用。例如，静态类不能被实例化，因此没有方法调用 `GetType()`。

### typeof()

获取 `Type` 对象的另一种方式是使用 `typeof` 表达式。`typeof` 在编译时绑定到特定的 `Type` 实例，并直接接受一个类型作为参数。列表 18.2 演示了将 `typeof` 与 `Enum.Parse()` 一起使用。

**列表 18.2：** 使用 `typeof()` 创建 `System.Type` 实例

```csharp
using System.Diagnostics;
// ...
ThreadPriorityLevel priority;
priority = (ThreadPriorityLevel)Enum.Parse(
            typeof(ThreadPriorityLevel), "Idle");
// ...
```

在此列表中，`Enum.Parse()` 接收一个标识枚举的 `Type` 对象，然后将字符串转换为特定的枚举值。在这种情况下，它将 `"Idle"` 转换为 `System.Diagnostics.ThreadPriorityLevel.Idle`。

类似地，下一节的列表 18.3 使用 `CompareTo(object obj)` 方法内的 `typeof` 表达式来验证 `obj` 参数的类型确实符合预期：

```csharp
if(obj.GetType() != typeof(Contact)) { ... }
```

`typeof` 表达式在编译时解析，以便类型比较——例如比较对 `GetType()` 调用的返回类型——可以确定对象是否为特定类型。

## 成员调用

反射的可能性不仅仅限于检索元数据。下一步是获取元数据并动态调用其引用的成员。考虑定义一个类来表示应用程序的命令行这一可能性。¹ 像这样的 `CommandLineInfo` 类的难点在于用启动应用程序的实际命令行数据来填充该类。然而，使用反射，你可以将命令行选项映射到属性名称，然后在运行时动态设置这些属性。列表 18.3 演示了这一过程。

### 列表 18.3：动态调用成员

```csharp
using System;
using System.Diagnostics;
public partial class Program
{
    public static void Main(string[] args)
    {
        string errorMessage;
        CommandLineInfo commandLine = new CommandLineInfo();
        if (!CommandLineHandler.TryParse(
    args, commandLine, out errorMessage))
{
    Console.WriteLine(errorMessage);
    DisplayHelp();
}
if (commandLine.Help)
{
    DisplayHelp();
}
else
{
    if (commandLine.Priority !=
        ProcessPriorityClass.Normal)
    {
        // Change thread priority
    }
}
// ...
    }
    private static void DisplayHelp()
    {
        // Display the command-line help
        Console.WriteLine(
        "Compress.exe / Out:< file name > / Help \n"
        + " / Priority:RealTime | High | "
        + " AboveNormal | Normal | BelowNormal | Idle");
    }
    public partial class CommandLineInfo
    {
        public bool Help { get; set; }
        public string Out { get; set; }
        public ProcessPriorityClass Priority { get; set; }
            = ProcessPriorityClass.Normal;
    }
}
```
