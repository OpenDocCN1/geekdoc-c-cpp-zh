
如果承诺不会失败，就使用 `Cer.Success`。否则，使用 `Cer.MayFail`。任何没有应用 `ReliabilityContractAttribute` 的方法都等同于标记为下面这样。

```csharp
[ReliabilityContract(Consistency.MayCorruptProcess, Cer.None)]
```

`Cer.None` 值表示该方法不做任何 CER 保证。换句话说，它编写时并未考虑 CER；因此，它可能会失败，并且可能会也可能不会报告失败。请记住，这些设置大多是为方法提供一种方式，向潜在的调用者记录它能提供什么，以便他们知道会出现什么情况。CLR 和 JIT 编译器不会使用此信息。

当你想要编写可靠的方法时，应使其保持短小并限制其行为。确保它不分配任何对象（例如，不装箱），不调用任何虚方法或接口方法，不使用任何委托，也不使用反射，因为 JIT 编译器无法判断实际会调用哪个方法。但是，你可以通过调用 `RuntimeHelpers` 类定义的以下方法之一来手动准备这些方法。

```csharp
public static void PrepareMethod(RuntimeMethodHandle method)
public static void PrepareMethod(RuntimeMethodHandle method,
    RuntimeTypeHandle[] instantiation)
public static void PrepareDelegate(Delegate d);
public static void PrepareContractedDelegate(Delegate d);
```

请注意，编译器和 CLR 不会做任何验证，来确认你编写的方法确实满足你通过 `ReliabilityContractAttribute` 所声明的保证。如果你做错了什么，就可能导致状态损坏。

> **注意** 即使所有方法都已预先准备，方法调用仍可能导致 `StackOverflowException`。当 CLR 未被承载时，`StackOverflowException` 会导致 CLR 内部调用 `Environment.FailFast` 来立即终止进程。当被承载时，`PrepareConstrainedRegions` 方法会检查堆栈，看是否还有大约 48 KB 的堆栈空间剩余。如果堆栈空间有限，则会在进入 try 块之前发生 `StackOverflowException`。

你还应该了解一下 `RuntimeHelpers` 的 `ExecuteCodeWithGuaranteedCleanup` 方法，这是另一种保证清理代码执行的方式。

```csharp
public static void ExecuteCodeWithGuaranteedCleanup(TryCode code, CleanupCode backoutCode,
    Object userData);
```

调用此方法时，你将 try 和 finally 块的主体作为回调方法传递，这些回调方法的原型分别与以下两个委托匹配。

```csharp
public delegate void TryCode(Object userData);
public delegate void CleanupCode(Object userData, Boolean exceptionThrown);
```

最后，另一种获得保证代码执行的方法是使用 `CriticalFinalizerObject` 类，第 21 章将对此进行详细说明。

## 代码契约

代码契约为你提供了一种方式，可以在代码本身中以声明方式记录你对代码所做的设计决策。契约采用以下形式：

- **前置条件** 通常用于验证参数
- **后置条件** 用于在方法因正常返回或因抛出异常而终止时验证状态
- **对象不变式** 用于确保对象的字段在整个对象生命周期内保持良好的状态

代码契约有助于代码的使用、理解、演进、测试、文档编写和早期错误检测。10 你可以将前置条件、后置条件和对象不变式视为方法签名的一部分。因此，你可以在新版本的代码中放宽契约，但不能在新版本中使契约更严格，否则会破坏向后兼容性。

代码契约的核心是静态的 `System.Diagnostics.Contracts.Contract` 类。

```csharp
public static class Contract {
    // Precondition methods: [Conditional("CONTRACTS_FULL")]
    public static void Requires(Boolean condition);
    public static void EndContractBlock();

    // Preconditions: Always
    public static void Requires<TException>(Boolean condition) where TException : Exception;

    // Postcondition methods: [Conditional("CONTRACTS_FULL")]
    public static void Ensures(Boolean condition);
    public static void EnsuresOnThrow<TException>(Boolean condition)
        where TException : Exception;

    // Special Postcondition methods: Always
    public static T Result<T>();
    public static T OldValue<T>(T value);
    public static T ValueAtReturn<T>(out T value);

    // Object Invariant methods: [Conditional("CONTRACTS_FULL")]
    public static void Invariant(Boolean condition);

    // Quantifier methods: Always
    public static Boolean Exists<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static Boolean Exists(Int32 fromInclusive, Int32 toExclusive,
        Predicate<Int32> predicate);
    public static Boolean ForAll<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static Boolean ForAll(Int32 fromInclusive, Int32 toExclusive,
        Predicate<Int32> predicate);

    // Helper methods: [Conditional("CONTRACTS_FULL")] or [Conditional("DEBUG")]
    public static void Assert(Boolean condition);
    public static void Assume(Boolean condition);

    // Infrastructure event: usually your code will not use this event
    public static event EventHandler<ContractFailedEventArgs> ContractFailed;
}
```

如前所述，这些静态方法中有许多都应用了 `[Conditional("CONTRACTS_FULL")]` 特性。一些辅助方法也应用了 `[Conditional("DEBUG")]` 特性。这意味着，除非在编译代码时定义了适当的符号，否则编译器将忽略你编写的调用这些方法的任何代码。任何标记为“Always”的方法都意味着编译器总是会发出调用该方法的代码。此外，`Requires`、`Requires<TException>`、`Ensures`、`EnsuresOnThrow`、`Invariant`、`Assert` 和 `Assume` 方法还有另一个重载（未显示），它接受一个 `String` 消息参数，这样你就可以显式指定在违反契约时应显示的 `String` 消息。

默认情况下，契约仅仅作为文档使用，因为在构建项目时你不会定义 `CONTRACTS_FULL` 符号。为了从使用契约中获得更多价值，你必须从 *http://msdn.microsoft.com/en-us/devlabs/dd491992.aspx* 下载额外的工具和 Visual Studio 属性窗格。没有将所有代码契约工具都包含在 Visual Studio 中的原因是，这项技术正在快速发展。Microsoft DevLabs 网站能够比 Visual Studio 本身更快地提供新版本和改进。下载并安装额外工具后，你会看到你的项目获得了一个新的属性窗格，如图 20-9 所示。

![](img/857bdf6cef9e242b53a37f88df9a1287_524_0.png)

**图 20-9** Visual Studio 项目的代码契约窗格。

要启用代码契约功能，请选中“执行运行时契约检查”复选框，并从其旁边的组合框中选择“Full”。这会在构建项目时定义 `CONTRACTS_FULL` 符号，并在构建项目后调用适当的工具（稍后介绍）。现在，在运行时，当契约被违反时，会引发 `Contract` 的 `ContractFailed` 事件。通常，开发人员不会在此事件上注册任何方法，但如果你注册了，那么你注册的任何方法都会收到一个如下所示的 `ContractFailedEventArgs` 对象。

```csharp
public sealed class ContractFailedEventArgs : EventArgs {
    public ContractFailedEventArgs(ContractFailureKind failureKind,
        String message, String condition, Exception originalException);

    public ContractFailureKind FailureKind      { get; }
    public String                Message        { get; }
    public String                Condition      { get; }
    public Exception             OriginalException { get; }

    public Boolean Handled { get; }   // true if any handler called SetHandled
    public void SetHandled();         // Call to ignore the violation; sets Handled to true

    public Boolean Unwind { get; }    // true if any handler called SetUnwind or threw
    public void SetUnwind();          // Call to force ContractException; set Unwind to true
}
```

可以在此事件上注册多个事件处理方法。每个方法都可以选择任何方式来处理契约违规。例如，处理程序可以记录违规、忽略违规（通过调用 `SetHandled`）或终止进程。如果有任何方法调用 `SetHandled`，那么该违规将被视为已处理，并且在所有处理程序方法返回后，允许应用程序代码继续运行，除非有任何处理程序调用 `SetUnwind`。如果处理程序调用了 `SetUnwind`，那么在所有处理程序方法运行完毕后，将抛出 `System.Diagnostics.Contracts.ContractException`。请注意，此类型是 `MSCorLib.dll` 内部的，因此你无法编写 catch 块来显式捕获它。另请注意，如果任何处理程序方法抛出了未处理的异常，那么其余的处理程序方法将被调用，然后抛出 `ContractException`。

如果没有事件处理程序，或者没有处理程序调用 `SetHandled`、`SetUnwind` 或抛出未处理的异常，那么接下来将执行契约违规的默认处理。如果 CLR 被承载，则宿主会收到契约失败的通知。如果 CLR 在非交互式窗口站上运行应用程序（对于 Windows 服务应用程序来说就是这种情况），则会调用 `Environment.FailFast` 来立即终止进程。如果你在编译时选中了“契约失败时断言”复选框，则会出现一个断言对话框，允许你将调试器连接到你的应用程序。如果未选择此选项，则会抛出 `ContractException`。

让我们看一个使用代码契约的示例类。

```csharp
public sealed class Item { /* ... */ }

public sealed class ShoppingCart {
    private List<Item> m_cart     = new List<Item>();
    private Decimal    m_totalCost = 0;
}
```

