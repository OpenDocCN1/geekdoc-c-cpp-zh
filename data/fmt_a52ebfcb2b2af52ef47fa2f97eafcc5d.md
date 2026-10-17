
图 20-8 性能监视器显示了 .NET CLR 异常计数器

# 第四部分 核心设施

偶尔，你会遇到一个频繁调用但失败率很高的方法。在这种情况下，抛出异常带来的性能影响可能是无法忍受的。例如，微软收到了几位客户的反馈，他们调用了 `Int32` 的 `Parse` 方法，经常传递从端用户输入的无法解析的数据。由于 `Parse` 被频繁调用，抛出和捕获异常的性能影响对应用程序的整体性能产生了巨大影响。

为了解决客户的顾虑并满足本章描述的所有准则，微软在 `Int32` 类中添加了一个新方法。该方法称为 `TryParse`，它具有如下重载：

```csharp
public static Boolean TryParse(String s, out Int32 result);
public static Boolean TryParse(String s, NumberStyles styles,
FormatException provider, out Int32 result);
```

你会注意到，这些方法返回一个布尔值，指示传入的字符是否可以解析为 `Int32`。这些方法还返回一个名为 `result` 的输出参数。如果方法返回 `true`，`result` 将包含将字符串解析为 32 位整数的结果。如果方法返回 `false`，`result` 将包含 0，但你真的不应该执行任何像那样的代码。

我想绝对明确一点：`TryXXX` 的布尔返回值返回 `false` 仅表示且仅一种类型的失败。对于任何其他类型的失败，方法仍然应该抛出异常。例如，如果 `style` 参数无效，`Int32` 的 `TryParse` 会抛出 `ArgumentException`，而且在调用 `Parse` 时，仍然完全可能抛出 `OutMemoryException`。

我还想明确，面向对象的编程允许程序员提高生产率。需要注意的是，它并不是通过在类型的成员中暴露错误代码来实现的。换句话说，构造函数、方法、属性等的定义，都是基于调用它们不会失败的假设。而且，如果定义正确，对于大多数成员的使用者来说，它不会失败，而且因为不会抛出异常，所以没有性能影响。

在定义类型及其成员时，你应该定义这些成员，使其在你预期的类型被使用的常见场景下，它们不太可能失败。如果你以后从用户那里听到他们对由于抛出异常导致的性能表示满意，那么再只考虑添加 `TryXXX` 方法。换句话说，你应该先产生最好的对象模型，如果用户有异议，再为你的类型添加一些 `TryXXX` 方法，以便遇到性能问题的用户从中受益。没有遇到性能问题的用户应该继续使用方法的非 `TryXXX` 版本，因为这是更好的对象模型。

## 受限制执行区域 (CERs)

许多应用程序并不需要健壮到能从各种失败中恢复。对于 `Notepad.exe` 和 `Calc.exe` 等许多客户端应用程序确实如此。当然，我们许多人见过 Microsoft Office 如 `WinWord.exe`、`Excel.exe` 和 `Outlook.exe` 因未处理的异常而终止。此外，许多服务器端应用程序（如 Web 服务器）是无的，如果它们由于未处理的异常而失败，会自动重启。而某些服务器（如 SQL Server）完全关于状态管理，由于未处理的异常导致数据丢失要灾难得多。

在 CLR 中，我们有 `AppDomains`（第 22 章讨论），它们包含状态。当 `AppDomain` 被卸载时，它的所有状态都会被卸载。因此，如果 `AppDomain` 中的一个线程遇到未处理的异常，卸载该 `AppDomain`（这会销毁其所有状态）而不终止整个进程是可以的。⁸

根据定义，CER 是一块必须对失败具有韧性的代码。由于 `AppDomains` 可以被卸载并销毁其状态，CER 通常用于操作由多个 `AppDomains` 或进程共享的任何状态。在面对意外发生的异常时，CER 对于维护状态是很有用的。我们将此类异常称为*异步异常*。例如，在调用方法时，CLR 必须加载程序集、在 `AppDomain` 的加载器堆中创建类型对象、调用类型的构造函数、将 IL JIT 编译为本地代码等。在这些操作中的任何一个都可能失败，CLR 都会通过抛出异常来报告失败。

如果这些操作中的任何一个在 **catch** 或 **finally** 块中失败，那么你的错误恢复清理代码将无法完整执行。这里有一个显示潜在问题的代码示例：

```csharp
private static void Demo() {
    try {
        Console.WriteLine("In try");
    } finally {
        // 这是一个潜在问题：如果在这里发生异常，
        // 下面的行可能不会执行。
        Type1.M(); 
    }
}

private sealed class Type1 {
    static Type1() {
        Console.WriteLine("Type1's static constructor");
    }

    public static void M() {}
}
```

请注意，编译器和 CLR 并不会验证你编写的方法是否真实符合你通过 `ReliabilityContractAttribute` 记录的保证。如果你执行了错误的操作，可能会导致状态损坏。

> 即使所有方法都已预先准备，方法仍然可能导致 `StackOverflowException`。当 CLR 未被托管时，`StackOverflowException` 会导致 CLR 调用 `Environment.FailFast` 从而立即终止进程。在托管时，`PreparedConstrainedRegions` 方法会检查栈以查看是否剩余约 48KB 的栈空间。如果栈空间有限，`StackOverflowException` 将入口块之前发生。

你还应该查看 `RuntimeHelper` 的 `ExecuteWithGuaranteedCleanup` 方法，这是另一种执行具有保证清理操作的代码的方法：

```
public static void ExecuteWithGuaranteedCleanup(TypeCode code, CleanupCode backout, Object userData);
```

调用时，你将 `try` 和 `finally` 块的主体作为回调方法传递，这两个委托的原型分别是：

```c
public delegate void TryCode(Object userData);
public delegate void CleanupCode(Object userData, Boolean exceptionThrown);
```

最后，另一种保证代码执行的方法是使用 `CriticalFinalizerObject` 类，该类在第 21 章中有详细的解释。

## 代码约 (Code Contracts)

代码约提供了一种方法，让你能够在代码内部声明式地记录对代码所做的设计决策。这些约的形式如下：

- **前置条件 (Preconditions)**：通常用于验证参数。
- **后置条件 (Postconditions)**：用于在方法因正常返回或抛出异常而终止时验证状态。
- **对象不变性 (Object Invariants)**：用于确保对象的字段在对象的整个生命周期内保持处于良好状态。

代码约有助于代码的使用、理解、演进、测试、文档编写和早期错误检测。你可以将前置条件、后置条件和对象不变性视为方法签名的一部分。因此，你可以通过新版本的代码放宽约，但在不破坏向后兼容性的情况下，你不能通过新版本使约变得更严格。

# 第 20 章 异常与状态管理

代码约的核心是静态的 `System.Diagnostics.Contracts.Contract` 类：

```
public static class Contract {
    // 前置条件方法: [Conditional("SS_FULL")]
    public static void Requires(Boolean condition);
    public static void EndContractBlock();

    // 前置条件: Always
    public static void Requires<T>(Boolean condition) where TException : Exception;

    // 后置条件方法: [Conditional("CONTRACTS_FULL")]
    public static void Ensures(Boolean condition);
    public static void EnsuresOnThrow<T>(Boolean condition) where TException : Exception;

    // 特殊后置条件方法: Always
    public static T Result<T>();
    public static T ValueAtReturn<T>(out T value);
    public static T ValueReturn<T>(out T value);

    // 不变性方法: [Conditional("CONTRACTS_FULL")]
    public static void Invariant(Boolean condition);

    // 量化方法: Always
    public static bool Exists<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static bool Exists(Int32 fromInclusive, Int32 toExclusive, Predicate<T> predicate);
    public static bool ForAll(IEnumerable<T> collection, Predicate<T> predicate);
    public static bool ForAll(Int32 fromInclusive, Int32 toExclusive, Predicate<T> predicate);

    // 辅助方法: [Conditional("CONTRACTS_FULL")] 或 [Conditional("DEBUG")]
    public static void Assert(Boolean condition);
    public static void Assume(Boolean condition);

    // 基础设施事件: 通常你的代码不会使用此事件
    public static event EventHandler<ContractFailedEventArgs> ContractFailed;
}
```

如上所示，这些静态方法中的许多带有 `[Conditional("CONTRACTS_FULL")]`。某些辅助方法也应用了该属性。这意味着编译器将忽略这些方法调用的任何代码。此外，标记为 "Always" 的方法编译器总是生成调用。`Requires`、`Requires<T>`、`Ensures`、`EnsuresOnThrow`、`Invariant` 和 `Assume` 都有一个接收字符串 消息的重载（未显示），你可以显式地指定在违反约时应该出现的消息。

默认情况下，约仅作为文档，并在构建项目时不会定义 `CONTRACTS_FULL` 符号。为了从约中获得价值，你必须从 mdn.microsoft.com 下载额外的文档和 Visual Studio 属性。所有代码工具没有在 Visual Studio 中使用的原因是该技术相对较新并且正在快速改进。微软的 DevLabs 站点比 Visual Studio 本身更快提供新版本和改进。下载并安装额外工具后，你将看到项目有一个新的属性可用，如图 20-9 所示。

![](img/bd052960dc8576a0e401f7f03c458.png)

图 20-9 代码窗口为 Visual Studio 项目提供了运行时约检查 (Runtime Contract Checking) 复选框

要使用代码约功能，选择 Runtime Contract Checking 复选框，并从旁边的组合框中选择 `Full`。这在构建项目时定义了 `CONTRACTS_FULL` 符号，并在构建项目后调用相应的工具（稍后描述）。现在，在运行时，当违反约时，会引发一个 `ContractFailed` 事件。通常，开发者不会注册此事件，但如果你注册了，那么你注册的任何方法将接收一个类似于下面的 `ContractFailedEventArgs` 对象：

```
public class ContractFailedEventArgs : EventArgs {
    public ContractFailedEventArgs(ContractFailureKind failureKind,
        String message, Exception originalException);

    public ContractFailureKind FailureKind { get; }
    public String Message { get; }
    public String Condition { get; }
    public Exception OriginalException { get; }

    public Boolean Handled { get; set; }
    public void Handled(bool value); // 调用以忽略违反；设置 handled

    public Boolean Unwind { get; set; }
    public void SetUnwind(bool value); // 调用以强制 ContractException；设置 unwind
```

可以可以注册多个事件处理器。每个处理器可以用自己选择的方式处理违反。例如，处理器可以记录违反、忽略违反（通过调用 `SetHandler`）或终止进程。如果任何方法调用 `SetHandler`，违反将被视为已处理，并在所有处理器方法返回后，应用程序代码允许继续，除非任何处理器调用了 `SetUnwind`。如果处理器调用 `SetUnwind`，则在所有处理器方法完成后，将抛出 `System.Diagnostics.Contracts.ContractException`。注意该类型是 MSCorLib.dll 内部的，因此你无法捕获。此外注意，如果任何处理器抛出未处理的异常，将调用剩余的处理器，然后抛出 `ContractException`。

如果没有事件处理器，或者它们一个都没有调用 `SetHandler`、`SetUnwind` 或抛出未处理的异常，接下来将对违反进行默认处理。如果 CLR 正在托管，则会通知主机失败。如果 CLR 运行在非交互窗口上（Windows 应用程序），将调用 `Environment.FailFast` 来终止进程。如果你在编译时选择了 Assert On Failure，将弹出一个对话框，允许你为应用程序连接调试器。如果没有勾选此选项，将抛出 `ContractException`。

让我们看看使用这些代码约的示例类：

```
public sealed class Item { /* ... */ }

public sealed class ShoppingCart {
    private List<Item> m_cart = new List<Item>();
    private Decimal m_totalCost = 0;

    public ShoppingCart() {
    }

    public void AddItem(Item item) {
        AddItemHelper(m_cart, item, ref m_totalCost);
    }

    private static void AddItemHelper(List<Item> m_cart, Item newItem,
        ref Decimal totalCost) {
        // 前置条件:
        Contract.Requires(newItem != null);
        Contract.Requires(Contract.ForAll(m_cart, s => s != newItem));

        // 后置条件:
        Contract.Ensures(Exists(m_cart, s => s == newItem));
        Contract.Ensures(totalCost == Contract.OldValue(totalCost));
        Contract.EnsuresOnThrowIOException(totalCost == Contract.OldValue(totalCost));

        // 执行一些操作（可能会抛出 IOException）...
        m_cart.Add(newItem);
        totalCost += 1.00M;
    }
}
```

```cs
// 对象不变性
[ContractInvariantMethod]
private void ObjectInvariant() {
    Contract.Invariant(m_totalCost >= 0);
}
```
