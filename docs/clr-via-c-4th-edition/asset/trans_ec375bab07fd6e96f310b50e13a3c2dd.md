
或 ARM 处理器。另外，与其他 CLR 实现（例如 Microsoft 的 .NET Compact Framework 或开源 Mono 项目）关联的 JIT 编译器很可能生成不同的代码。

实际上，我已经能够用 Microsoft 内部的一些不同 JIT 编译器测试我自己的一些代码，而我观察到的性能差异相当显著且令人惊讶。关键在于，你必须在用户预期会运行的各种平台上测试代码，并据此进行修改。同样，我不会担心使用异常处理的性能；其好处通常远远超过任何负面的性能影响。

如果你有兴趣了解异常处理如何影响代码性能，可以使用 Windows 自带的性能监视器工具。图 20-8 中的屏幕显示了随 .NET Framework 一起安装的与异常相关的计数器。

![](img/857bdf6cef9e242b53a37f88df9a1287_518_0.png)

图 20-8 显示 .NET CLR Exceptions 计数器的性能监视器。

有时你会遇到一个频繁调用且失败率很高的方法。在这种情况下，抛出异常带来的性能损失可能无法忍受。例如，Microsoft 收到多家客户的反馈，他们频繁调用 Int32 的 Parse 方法，并经常传入无法解析的最终用户输入数据。由于 Parse 被频繁调用，抛出和捕获异常带来的性能损失对应用程序的整体性能造成了很大损害。

为了解决客户的顾虑并满足本章所述的所有准则，Microsoft 向 Int32 类添加了一个新方法。这个新方法称为 TryParse，它有两个重载，如下所示。

```csharp
public static Boolean TryParse(String s, out Int32 result);
public static Boolean TryParse(String s, NumberStyles styles,
    IFormatProvider provider, out Int32 result);
```

你会注意到，这些方法返回一个 Boolean，指示传入的 String 是否包含可解析为 Int32 的字符。这些方法还返回一个名为 result 的输出参数。如果方法返回 true，result 将包含将该字符串解析为 32 位整数的结果。如果方法返回 false，result 将包含 0，但无论如何你都不应执行任何查看它的代码。

有一点我想绝对明确：TryXxx 方法的 Boolean 返回值返回 false，仅表示唯一一种失败类型。对于任何其他类型的失败，该方法仍应抛出异常。例如，如果 style 参数无效，Int32 的 TryParse 会抛出 ArgumentException；而且调用 TryParse 时当然仍可能抛出 OutOfMemoryException。

我还想明确说明，面向对象编程让程序员能够高效工作。其实现方式之一是不在类型的成员中暴露错误代码。换句话说，构造函数、方法、属性等全都基于调用它们不会失败这一理念来定义。而且，如果定义正确，对于成员的大多数使用情况，它不会失败，也不会产生性能损失，因为不会抛出异常。

在定义类型及其成员时，你应当这样定义成员：在你预期使用这些类型的常见场景中，它们不太可能失败。如果之后你听到用户因为抛出异常而导致的性能不满意，那么只有到那时，你才应考虑添加 TryXxx 方法。换句话说，你应当先产出最佳的对象模型，然后，如果用户提出异议，再向你的类型添加一些 TryXxx 方法，以便遇到性能问题的用户能够受益。没有遇到性能问题的用户应继续使用方法的非 TryXxx 版本，因为这是更好的对象模型。

### 受约束的执行区域 (CER)

许多应用程序不需要具备健壮性并从任何及所有类型的失败中恢复。许多客户端应用程序都是如此，例如 Notepad.exe 和 Calc.exe。当然，我们中的许多人都见过 Microsoft Office 应用程序（如 WinWord.exe、Excel.exe 和 Outlook.exe）因未处理异常而终止。此外，许多服务器端应用程序（如 Web 服务器）是无状态的，如果因未处理异常而失败，会自动重新启动。当然，有些服务器（如 SQL Server）完全围绕状态管理，因未处理异常而丢失数据可能更具灾难性。

在 CLR 中，我们有 AppDomain（第 22 章讨论），其中包含状态。卸载 AppDomain 时，其所有状态都会被卸载。因此，如果 AppDomain 中的某个线程遇到未处理异常，可以卸载该 AppDomain（这会销毁其所有状态），而无需终止整个进程。8

8 如果线程整个生命周期都位于单个 AppDomain 内（例如在 ASP.NET 和托管 SQL Server 存储过程场景中），这绝对是正确的。但是，如果线程在其生命周期内跨越 AppDomain 边界，你可能必须终止整个进程。

根据定义，CER 是一块必须能够从失败中恢复的代码。由于 AppDomain 可以被卸载并销毁其状态，CER 通常用于操作由多个 AppDomain 或进程共享的任何状态。CER 在面临意外抛出的异常时尝试维护状态很有用。有时我们将这类异常称为*异步异常*。例如，在调用方法时，CLR 必须加载程序集、在 AppDomain 的加载器堆中创建类型对象、调用类型的静态构造函数、将 IL JIT 编译为本机代码，等等。这些操作中的任何一个都可能失败，而 CLR 通过抛出异常来报告失败。

如果这些操作中的任何一个在 `catch` 或 `finally` 块内失败，那么你的错误恢复或清理代码将无法完整执行。下面是一个展示潜在问题的代码示例。

```csharp
private static void Demo1() {
    try {
        Console.WriteLine("In try");
    }
    finally {
        // Type1's static constructor is implicitly called in here
        Type1.M();
    }
}

private sealed class Type1 {
    static Type1() {
        // if this throws an exception, M won't get called
        Console.WriteLine("Type1's static ctor called");
    }

    public static void M() { }
}
```

运行上述代码时，我得到以下输出。

```text
In try
Type1's static ctor called
```

我们想要的是，除非我们知道关联的 `catch` 和 `finally` 块中的代码保证（或尽可能接近保证）会执行，否则甚至不要开始执行前面 `try` 块中的代码。我们可以通过如下修改代码来实现这一点。

```csharp
private static void Demo2() {
    // Force the code in the finally to be eagerly prepared
    RuntimeHelpers.PrepareConstrainedRegions(); // System.Runtime.CompilerServices namespace
    try {
        Console.WriteLine("In try");
    }
    finally {
        // Type2's static constructor is implicitly called in here
        Type2.M();
    }
}

public class Type2 {
    static Type2() {
        Console.WriteLine("Type2's static ctor called");
    }

    // Use this attribute defined in the System.Runtime.ConstrainedExecution namespace
    [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
    public static void M() { }
}
```

现在，当我运行这个版本的代码时，我得到以下输出。

```text
Type2's static ctor called
In try
```

`PrepareConstrainedRegions` 方法是一个非常特殊的方法。当 JIT 编译器看到该方法在 `try` 块之前被立即调用时，它会立即编译 `try` 的 `catch` 和 `finally` 块中的代码。JIT 编译器将加载任何程序集、创建任何类型对象、调用任何静态构造函数，并对任何方法进行 JIT 编译。如果这些操作中的任何一个导致异常，那么异常会在*线程进入 `try` 块之前*发生。

当 JIT 编译器立即准备方法时，它还会遍历整个调用图，立即准备被调用的方法。然而，JIT 编译器只准备那些应用了 `ReliabilityContractAttribute` 且指定了 `Consistency.WillNotCorruptState` 或 `Consistency.MayCorruptInstance` 的方法，因为 CLR 无法对可能损坏 `AppDomain` 或进程状态的方法做出任何保证。在通过调用 `PrepareConstrainedRegions` 加以保护的 `catch` 或 `finally` 块内，你要确保只调用按我刚才所述设置了 `ReliabilityContractAttribute` 的方法。

`ReliabilityContractAttribute` 如下所示。

```csharp
public sealed class ReliabilityContractAttribute : Attribute {
    public ReliabilityContractAttribute(Consistency consistencyGuarantee, Cer cer);
    public Cer Cer { get; }
    public Consistency ConsistencyGuarantee { get; }
}
```

这个特性让开发者能够向该方法的潜在调用方记录特定方法的可靠性契约。`Cer` 和 `Consistency` 类型都是枚举类型，定义如下。⁹

```csharp
enum Consistency {
    MayCorruptProcess, MayCorruptAppDomain, MayCorruptInstance, WillNotCorruptState
}

enum Cer { None, MayFail, Success }
```

如果你正在编写的方法承诺不损坏任何状态，请使用 `Consistency.WillNotCorruptState`。否则，请使用其他三个可能值之一来记录你的方法的行为，这些值应与你方法可能损坏的状态相匹配。如果你正在编写的方法

⁹ 你还可以将此特性应用于接口、构造函数、结构、类或程序集，以影响其中的成员。
