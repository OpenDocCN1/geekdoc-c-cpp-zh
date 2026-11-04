
![](img/a16f85e62ce9bdc527f4b09dbfe26092_46_0.png)

FIGURE 1.4 从代码到指令。

## 通用类型系统详解

类型是 CLR 世界中的核心。它们定义了库和程序的组织方式，以及组件之间交互的实现方式。程序集是此类类型的容器。

让我们更详细地探讨类型的优点，并了解运行时支持的各种类型种类。暂时不用担心 C# 语法；我们在后续内容中会详细介绍。

### 什么是类型安全？

为了强制代码以正确的方式处理类型，CLR 保证类型安全。这确保对象只能以与对象类型契约一致的方式访问。类型包含两部分：类型对象所包含的数据（例如，客户的姓名和信用额度）以及可以对该数据执行的操作（例如，对 Product 的 DiscountPrice）。

为了说明类型不安全的操作，假设你可以将 Customer 类型的对象当作 Product 类型来处理。那么，对客户对象执行 DiscountPrice 操作意味着什么呢？也许你会更改客户的信用额度。这显然是不安全的做法。同样，任意内存访问也是不安全的，因为你可能会进入某个类型的中间位置，而不知道那里驻留的数据类型。

像 C 和 C++ 这样的非托管语言允许这种情况发生，这为难以调试的问题和安全漏洞打开了大门。最理想的情况是，在执行无效操作时进程会崩溃（例如，因尝试覆盖受保护的内存），但类型不安全操作很可能在一段时间内未被察觉，使得在损害已经发生时追踪问题根源变得非常困难。

为了消除这类错误，CLR 强制执行类型安全。这通过多种方式实现，包括在 JIT 编译期间进行代码验证以及监控类型的使用，以确保不会进行与对象运行时类型不兼容的操作。我们示例中将 Customer 类型的对象“强制转换”为 Product 类型的漏洞将导致运行时异常，从而完全阻止无效操作的发生。

### 关于类型安全与静态和动态语言的几点说明

不要将类型安全与静态类型编程语言（主要是 C# 和 F#）混为一谈。虽然动态语言（如 Ruby 和 Python）在编写动态类型代码时不需要用户指定类型，但在代码运行时对象仍然具有明确定义的类型。这足以让运行时——在此情况下是与 CLR 协同工作的 DLR——检测到对类型安全的违反。

静态类型语言与其动态类型对应物之间的区别在于，它们通过强制执行各种规则，有潜力在编译时及早捕获大量违规。能够在静态情况下被证明是类型安全的代码称为可验证类型安全代码。.NET Framework 随带一个名为 PEVerify 的工具，用于确定代码是否可验证类型安全。

表 1.1 符合 CLS 的原始类型

| 类型 | C# | VB | C++/CLI | F# |
|---|---|---|---|---|
| System.Byte | byte | Byte | unsigned char | byte |
| System.Int16 | short | Short | short | int16 |
| System.Int32 | int | Integer | int/long | int/int32 |
| System.Int64 | long | Long | __int64 | int64 |
| System.Single | float | Single | Float | single/float32 |
| System.Double | double | Double | Double | double/float |
| System.Boolean | bool | Boolean | Bool | bool |
| System.Char | char | Char | wchar_t | char |
| System.Decimal | decimal | Decimal | Decimal | decimal |
| System.String | string | String | String^ | string |

### 原始类型

用户定义的类型通常包含数据，而这些数据的每个部分本身都应具有类型。这些类型也可以再次是用户定义的，但显然，在某个时刻需要使用预定义的类型。CTS 的角色之一是提供此类原始数据类型。.NET Framework 上的各种语言为这些数据类型定义了不同的“友好名称”，但最终它们都使用其底层类型表示，该类型在 BCL 的一部分 mscorlib.dll 程序集中定义。各种语言使用相同的内置类型这一事实是实现真正跨语言集成的基石之一。

表 1.1 显示了符合 CLS 的语言应支持的原始类型。各种语言中对应的关键字也显示在其中。除了这些类型之外，还存在各种其他非 CLS 原始类型，例如数值数据类型的无符号变体。

### 类、结构和枚举

由于 CLI 受 OO 编程原则的启发，类是 CLI 支持的一种类型，这不足为奇。本质上，类是数据的容器以及可以对该数据执行的操作的容器。通过将类的内部数据表示保持为私有，可以实现封装的优点，即只要公共契约保持不变，实现细节就可以更改。

```csharp
static class Calculator
{
    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```

遵循真正的 OO 风格，CLI 支持创建类层次结构，其中一个类型派生自另一个类型。例如，Apple 类型可以派生自 Fruit 基类。当我们介绍使用 C# 进行 OO 编程时，将会详细解释这些细节。

类正式被称为 *引用类型*，因为它们驻留在堆上并通过引用使用。String 类型是内置引用类型的示例。然而，轻量级且在栈上分配的类型有时会很有用，因此 CLI 也支持值类型的概念。值类型的示例包括数值数据类型（如 Int32 和 Double）、DateTime 类型等。在 C# 世界中，值类型被声明为 struct：

```csharp
struct Point
{
    private readonly int _x;
    private readonly int _y;
    private readonly int _z;

    public Point(int x, int y, int z)
    {
        _x = x;
        _y = y;
        _z = z;
    }

    public int X { get { return _x; } }
    public int Y { get { return _y; } }
    public int Z { get { return _z; } }
}
```

枚举是一种特殊的值类型，用于表示有限的可能值集合（例如，颜色）。这与命名常量数值值有很大不同，因为枚举强制执行强类型。虽然 Color.Red 可能与 Weekday.Monday 具有相同的数值表示，但不能将 Color 值分配给 Weekday 变量：

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

### 接口

接口提供了定义可由类或结构实现契约的能力。这样，契约与特定功能的实现就可以彼此解耦。例如，给定以下接口，可以定义对“某物”进行枚举的含义，无论它是集合类型还是从网络套接字接收的数据：

```csharp
interface IEnumerable
{
    IEnumerator GetEnumerator();
}
```

```csharp
interface IEnumerator
{
    bool MoveNext();
    object Current { get; }
    void Reset();
}
```

现在可以编写代码来处理遵守此契约的任何事物——例如，将枚举结果打印到屏幕上。这样，接口允许编写多态代码，我们将在后面更详细地讨论这一点。

### 委托

在另一处使用代码块的能力非常强大。需要这种设置的典型任务是创建新的后台线程，这需要线程应开始执行的代码。某些平台通过提供像 Runnable 这样的单方法接口来解决这个问题。仅仅为了传递一段代码就需要相当多的样板。另一种可能性是使用函数指针，但在这种方法中类型安全会受损。

委托结合了函数指针的简洁性，同时保留了单方法接口的类型安全特性，但无需处理其繁琐之处。下面展示了一个与线程相关的示例：

```csharp
var t = new Thread(delegate(object data)
{
    // Process customer object in the background
});
Customer customer = new Customer();
t.Start(customer);
```

这仅展示了委托的使用位置，我们在其中将用于客户数据处理的代码块传递给新线程。CTS 对代码声明自己的委托类型提供了第一类支持，你可以将其视为静态类型的方法签名，描述预期代码块的输入和输出类型：

```csharp
/* declaration of a delegate for binary mathematical operations on two integer values */
delegate int BinaryOperation(int a, int b);
```

```csharp
class WorkingWithDelegates
{
    public int Calculate(BinaryOperation op, int a, int b)
    {
        // calling through the delegate
        return op(a, b);
    }
}
```
