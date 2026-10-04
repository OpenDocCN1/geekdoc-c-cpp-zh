

# 代码契约 (Code Contracts)

代码契约提供了一种方法，允许你在代码内部声明式地记录对代码所做的设计决策。契约采用以下形式：

- **前置条件 (Preconditions)**：通常用于验证参数。
- **后置条件 (Postconditions)**：用于在方法因正常返回或抛出异常而终止时验证状态。
- **对象不变性 (Object Invariants)**：用于确保对象的字段在整个对象的生命周期内始终保持良好状态。

代码契约有助于代码的使用、理解、演进、测试、文档编写以及早期错误检测.¹¹⁰。你可以将前置条件、后置条件和对象不变性视为方法签名的一部分。因此，你可以通过新版本的代码来放宽契约，也可以在新版本中使契约更严格，而不破坏兼容性。

代码契约的核心是静态的 `System.Diagnostics.Contracts.Contract` 类。

```cs
public static class Contract {
    public Precondition methods: [Conditional("CONTRACTS_FULL")];
    public static void Requires(Boolean condition);
    public static void EndContractBlock();

    // Postconditions: 始终执行
    public static void Requires<TException>(Boolean condition) where TException : Exception;

    // Postcondition methods: [Conditional("CONTRACTS_FULL")];
    public static void Ensures(Boolean condition);
    public static void EnsuresOnThrow<TException>(Boolean condition)
    where TException : Exception;

    // Special Postmethods: 始终执行
    public static T Result<T>();
    public static T 0OldValue<T>(out T value);
    public static T ValueAtReturn<T>(out T value);

    // Object Invariant methods: [Conditional("CONTRACTS_FULL")];
    public static void Invariant(Boolean condition);

    // Quantifier methods: 始终执行
    public static bool Exists<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static bool Exists(Int32 inclusive, Int32 toExclusive,
    Predicate<Int32> predicate);
    public static bool ForAll<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static bool ForAll(Int32 inclusive, Int32 toExclusive,
    Predicate<Int32> predicate);
    // Helper methods: [Conditional("CONTRACTS_FULL")] or [Conditional("DEBUG")];
    public static void Assert(Boolean condition);
```

> ¹⁰ 为了帮助自动化测试，请参见由微软研究院创建的 Pex 工具：http://research.microsoft.com/en-us/projects/pex/。

```cs
public static void Assume(Boolean condition);
```

```cs
// Infrastructure 事件：通常你的代码不会使用此事件
public static event EventHandler<ContractFailedEventArgs> ContractFailed;
}
```

如前所述，这些静态方法中的许多一个都应用了 `[Conditional(CONTRACTS_FULL)]` 特性。其他一些方法还应用了 `[Conditional(DEBUG)]` 特性。这意味着除非在编译代码时定义了相应的符号，否则编译器将忽略你编写的任何调用这些方法的代码。任何标记为“Always”的方法意味着编译器始终会它们以调用该方法。任何标记为 `Requires`、`Requires-Exception`、`Ensures`、`EnsuresOnThrow`、`Invariant`、`Assert` 和 `Assume` 的方法都有一个不接受 String 参数的重载版本，这样你可以在违反契约时显式指定字符串消息。

默认情况下，契约仅作为文档使用，因为你在构建项目时不会定义 `CONTRACTS_FULL` 符号。为了使用契约获取额外价值，你必须从 https://msdn.microsoft.com/en-us/devblogs/dd49192.aspx 下载工具和 Visual Studio 属性面板。代码契约没有包含在 Visual Studio 中是因为这项技术正在验证中。Microsoft DevLabs 网站可以比 Visual Studio 更快提供新版本和改进。下载并安装工具后，你将拥有一个新的属性面板，如图 20-9 所示。

![](img/0ce3b788d061e3d3095fa554b1a34adf_524_0.png)

图 20-9 - Visual Studio 项目的契约面板。

要开启代码契约功能，请选择 `Perform Runtime Checking`（执行运行时检查）复选框，并在旁边的组合框中选择 `From`。这会在你构建项目时定义 `CONTRACTS_FULL` 符号，并在构建项目后调用相应的工具（稍后描述）。现在，在运行时，当契约被违反时，会触发 `Contract.Failed` 事件。通常，开发者不会向此事件注册任何方法，但如果你注册了，你注册的任何方法都会接收一个所示的 `ContractFailedEventArgs` 对象。

```cs
public sealed class ContractFailedEventArgs : EventArgs {
    public ContractFailedEventArgs(ContractFailureKind kind,
                                    String message, String condition, Exception originalException) {

    public ContractFailureKind Kind { get; }
    public String Message { get; }
    public String Condition { get; }
    public Exception OriginalException { get; }

    public bool SetHandled { get; set; } // 如果任何处理器调用了 SetHandled，则为 true
    public void SetHandled(); // 调用以忽略违反；将 Handled 设置为 true

    public bool Unwind { get; set; } // 如果任何处理器调用了 SetUnwind，则为 true
    public void SetUnwind(); // 调用强制触发 Contractexception；将 Unwind 设置为 true
}
```

此事件可以注册多个处理器。每个方法都可以以其选择的任何方式处理契约违反。例如，处理器可以忽略违反（通过调用 `SetHandled`）或终止进程。如果任何方法调用了 `SetHandled`，则该违反将被视为已处理。
