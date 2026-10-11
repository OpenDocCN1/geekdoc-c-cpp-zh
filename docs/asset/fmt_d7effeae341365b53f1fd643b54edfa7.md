
注意你返回的是 `IEnumerable<T>`，而不是 `IEnumerator<T>`。这与返回 `IEnumerator<T>` 的 `IEnumerable<T>.GetEnumerator()` 不同。`Main()` 中的代码演示了如何使用 `foreach` 循环调用 `GetReverseEnumerator()`。

## yield 语句要求

你只能在返回 `Enumerator<T>` 或 `IEnumerable<T>` 类型或其非泛型对应类型的成员中使用 `yield return` 语句。包含 `yield return` 语句的成员不能有简单的 `return`。如果成员使用了 `yield return` 语句，C# 编译器将生成必要的代码来维护迭代器的状态。相比之下，如果成员使用 `return` 语句而不是 `yield return`，则程序员负责维护自己的状态机并返回迭代器接口之一的实例。此外，就像方法中的所有代码路径都必须包含一个带值的 `return` 语句（假设它们没有抛出异常）一样，迭代器中的所有代码路径如果要返回任何数据，就必须包含 `yield return` 语句。

如果违反以下对 `yield` 语句的附加限制，会导致编译器错误：

- `yield` 语句只能出现在方法、用户定义的运算符、或索引器或属性的 `get` 访问器内部。该成员不能接受任何 `ref` 或 `out` 参数。
- `yield` 语句不能出现在匿名方法或 lambda 表达式任何位置（见第 13 章）。
- `yield` 语句不能出现在 `try` 语句的 `catch` 和 `finally` 子句中。此外，只有在没有 `catch` 块的情况下，yield` 语句才能出现在 `try` 块中。

## 总结

在本章中，我们回顾了关键集合类，并根据它们支持的接口考虑了分类。每个类都专注于从集合中插入和检索项目，使用了键、索引、先进先出（FIFO）或后进先行（LIFO）等机制。我们还探索了如何遍历集合。此外，本章解释了如何使用自定义迭代器定义自定义集合，以枚举集合中的项目。（迭代器涉及一个上下文关键字 `yield`，C# 使用它来生成底层 CIL 代码以实现 `foreach` 循环使用的迭代器模式。）

在第 18 章中，我们将探索反射（Reflection），这是一个之前简要提到过的话题，尽管几乎没有解释。反射允许我们在运行时检查 CIL 代码中类型的结构。

# 第 18 章 反射、特性与动态编程

特性（Attributes）是向程序集中插入额外元数据的一种手段，并将这些元数据与类、方法或属性等编程构造相关联。本章将研究框架内置特性的详细信息，并描述了如何定义自定义特性。为了利用自定义特性，需要了解定义方法。

反射允许我们在运行时检查 CIL 代码中类型的结构。本章从反射开始，这在之前简要提到过，尽管几乎没有解释。反射允许我们在运行时检查 CIL 代码中类型的结构。

## 反射

使用反射，可以实现以下操作访问元数据

### 18 第 1 章: Reflection, Attributes and Dynamic Programming

反射允许我们在运行时检查 CIL 代码中类型的结构。本章从反射开始，这在之前简要提到过，尽管几乎没有解释。反射允许我们在运行时检查 CIL 代码中类型的结构。

## 使用 System.Type 访问元数据

### 1. Reflection

### 属性

### 1. Reflection, Attributes and Dynamic Programming

### 1. Reflection

### 2. Reflection

反射允许我们在运行时检查 CIL 代码中类型的结构。

### 1. Reflection

特性

### 1. Reflection, Attributes and Dynamic Programming

### 1. Reflection

### 2. 反射

反射允许我们在运行时检查 CIL 代码中类型的结构。本章从反射开始，这在之前简要提到过，尽管几乎没有解释。反射允许我们在运行时检查 CIL 代码中类型的结构。

反射允许我们在运行时检查 CIL 代码中类型的结构。本章从反射开始，这在之前简要提到过，尽管几乎没有解释。反射允许我们在运行时检查 CIL 代码中类型的结构。

### 1. Reflection

### 2. Reflection

### 3. Reflection

### 1. Reflection

### 2. Reflection

### 3. Reflection

## 使用 System.Type 访问元数据

读取类型元元数据的关键是获取一个代表目标类型的 `System.Type` 实例。`System.Type` 提供了所有获取类型信息的方法。你可以用它来回答以下问题：

- 类型的名称是什么 (`Type.Name`)？
- 类型是公共的吗 (`Type.IsPublic`)？
- 类型的基类型是什么 (`Type.BaseType`)？
- 类型支持哪些接口 (`Type.GetInterfaces()`)？
- 类型在哪个程序集中定义 (`Type.Assembly`)？
- 属性、方法、字段等有哪些 (`Type.GetProperties()`、`Type.GetMethods()`、`Type.GetFields()` 等）？
- 哪些特性装饰了该类型 (`Type.GetCustomAttributes()`)？

还有许多此类成员，但它们都提供关于特定类型的信息。关键是获取类型 `Type` 对象的引用，其两种主要方法是通过 `object.GetType()` 和 `typeof()`。

注意 `GetMethods()` 调用不返回扩展方法。这些方法仅作为实现类型的静态成员可用。

## 第 18 章：反射、特性与动态编程

### GetType()

包含一个 `GetType()` 成员，因此所有类型都包含此函数。你调用 `GetType()` 来获取与原始对象对应的 `System.Type` 实例。示例 18.1 展示了这一过程，使用了 `DateTime` 的 `Type` 实例。输出 18.1 显示了结果。

列表 18.1：使用 `Type.GetProperties()` 获取对象的公共属性

```csharp
DateTime dateTime = new();
Type type = dateTime.GetType();
foreach(
    System.Reflection.PropertyInfo property in type.GetProperties())
{
    Console.WriteLine(property.Name);
}
```

| Date | Day | DayOfWeek | DayOfYear | Hour | Kind | Millisecond | Minute | Month | Now | UtcNow | Second | Ticks | TimeOfDay | Today | Year |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

在调用 `GetType()` 之后，你遍历 `Type.GetProperties()` 返回的每个 `System.Reflection.PropertyInfo` 实例并显示属性名称。调用 `GetType()` 的关键在于你必须有一个对象实例。然而，有时无法获得此类实例。例如，静态类无法实例化，因此没有办法对它们调用 `GetType()`。

## typeof()

获取 `Type` 对象的另一种方法是使用 `typeof` 表达式。`typeof` 在编译时绑定到特定的 `Type` 实例，并直接将类型作为参数。例外是泛型类型上的类型参数，因为它在运行时之前无法确定。列表 18.2 展示了结合 `Enum.Parse()` 使用 `typeof`。

列表 18.2：使用 `typeof()` 创建 `System.Type` 实例

```csharp
using System.Diagnostics;
// ...
    ThreadPriorityLevel priority;
    priority = (ThreadPriorityLevel)Enum.Parse(
        typeof(ThreadPriorityLevel), "Idle");
```

在此列表中，`Enum.Parse()` 接收一个标识枚举的 `Type` 对象，然后将字符串转换为特定的枚举值。在这种情况下，它将 "Idle" 转换为 `System.Diagnostics.ThreadPriorityLevel.Idle`。

同样，下一节中的列表 18.3 在 `CompareTo(object obj)` 方法内部使用了 `typeof` 表达式，以验证 `obj` 参数的类型确实是预期的类型。

```csharp
if(obj.GetType() != typeof(Contact)) { ... }
```

`typeof` 表达式在编译时解析，因此类型比较——例如比较调用 `GetType()` 返回的类型——可以判断一个对象是否属于特定类型。

## 成员调用

反射的可能性不仅限于检索元数据。你还可以利用元数据并动态地调用它所标识的成员。考虑定义一个类来表示应用程序的命令行。`CommandLineInfo` 类困难之处在于如何向该类填充启动应用程序的实际命令行数据。然而，使用反射，你可以将命令行选项映射到属性名称，然后在运行时动态设置这些属性。列表 18.3 展示了这一过程。

### 列表 18.3：动态调用成员

```csharp
using System.Diagnostics;
using System.IO;
using System.Reflection;
public partial class Program
{
    public static void Main(string[] args)
    {
        CommandLine commandLine = new CommandLineHandler();
        if(!commandLine.TryParse(args, out string errorMessage))
        {
            Console.WriteLine(errorMessage);
        }
        else
        {
            commandLine.DisplayHelp();
        }
    }
    private static void DisplayHelp()
    {
        // ...
    }
}
public partial class CommandLineInfo
{
    public bool Help { get; set; }
    public string Out { get; set; }
    public ThreadPriorityLevel Priority { get; set; }
}
public class CommandLineHandler
{
    public static bool TryParse(string[] args, out string errorMessage)
    {
        errorMessage = null;
        string[] optionParts = args.Split(' ');
        foreach (string arg in args)
        {
            if (arg.StartsWith("/"))
            {
                string option = arg.Substring(1);
                if (option == "Help")
                {
                    // ...
                }
            }
        }
        return true;
    }
}
```

![](img/ffe0f34eac7523830420733690014d17_925_0.png)

图 18.1：MemberInfo 派类

# 第 18 章：反射、属性与动态编程

```cs
public void Add(T i)
{
    //...
    Type t = typeof(T);
    //...
}
```

一旦你获得了类型参数的 Type 对象的实例，就可以对该类型参数本身进行反射，以确定其行为并针对特定类型定制 `Add` 方法，或者更有效地定制。

# 判断类或方法是否支持泛型

在 CLR 2.0 版本的 `System.Type` 类中，添加了一些方法用于判断给定类型是否支持泛型参数和泛型参数。泛型参数是在实例化泛型类时提供的类型参数。你可以通过查询 `ContainsGenericParameters` 属性来确定类或方法是否包含尚未设置的泛型参数，如列表 18.5 的输出 18.3 所示。

# 列表 18.5：泛型的反射

```cs
public class Program
{
    Type type;
    type = typeof(System.Nullable<null>);
    Console.WriteLine(type.ContainsGenericParameters);
    Console.WriteLine(type.IsGenericType);
    type = typeof(System.Nullable<DateTime>);
    Console.WriteLine(type.ContainsGenericParameters);
    Console.WriteLine(type.IsGenericType);
}
```

# 输出 18.3

```
True
True
False
True
```

`Type.IsGenericType` 是一个布尔属性，用于评估一个类型是否为泛型。

# 获取泛型类或方法的类型参数

你可以通过调用 `GetGenericArguments()` 方法从泛型类获取泛型参数（或类型参数）列表。结果是一个 `System.Type` 实例数组，对应于它们作为泛型类类型参数声明的顺序。列表 18.6 反射了一个泛型类型并获取了每个类型参数；输出 18.4 显示了结果。

# 列表 18.6：对泛型类型使用反射

```cs
public class Program
{
    public static void Main()
    {
        Stack<int> s = new();
        Type t = s.GetType();
        foreach(Type type in t.GetGenericArguments())
        {
            System.Console.WriteLine(
```
