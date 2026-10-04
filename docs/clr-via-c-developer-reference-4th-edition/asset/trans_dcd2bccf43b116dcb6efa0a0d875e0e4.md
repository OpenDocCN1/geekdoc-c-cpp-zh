
你可以采取以下几件事来帮助缓解损坏：

- CL（公共语言运行时）不允许在执行 catch 或 finally 块内部的代码时中止线程。因此，我们可以通过以下方式使 `Transfer` 方法更加健壮。

```
public static void Transfer(Account from, Account to, Decimal amount) {
    try { /* do nothing in here */ }
    finally {
        from = amount;
        // 现在无法发生中止（由于 Thread.Abort/AppDomain.Unload）
        to += amount;
    }
}
```

然而，绝对不建议你将所有代码都写在 finally 块中！你只应该将此技术用于修改极其敏感的状态。

- 你可以使用 `System.Diagnostics.Contracts` 为你的方法应用代码合约。代码合约为你提供了一种方法在尝试使用这些参数/变量修改状态之前，验证参数和其他变量的方法。如果参数/变量符合合约，则状态损坏的可能性将降到最低（但并非完全消除）。如果合约失败，则在任何状态被修改之前抛出异常。我将在本章的稍后部分讨论代码合约。

- 你可以使用受限制执行区域（CERs），它为你提供了一种消除 CLR 不确定性的方法。例如，在进入 try 块之前，你可以让 CLR 加载任何关联 catch 和 finally 块中的代码所需的所有程序集。此外，CLR 将编译 catch 和 finally 块中的所有代码，包括从这些块内部调用的方法。这将消除大量的异常（包括 `FileLoadException`、`FormatException`、`InvalidProgramException`、`FieldAccessException`、`MissingFieldException`、`MethodException`）在尝试执行恢复代码（catch 块）或清理代码（finally块）时发生。它还会减少 `OutOfMemoryException` 等异常的可能性。我将在本章稍后部分讨论 CER。

根据你所在的环境，可以使用事务来确保所有状态都被修改或所有状态都不被修改。例如，如果数据在数据库中，事务的效果很好。Windows 也支持事务注册表和文件操作（仅限 NTFS 卷），所以你可能可以使用这些；但目前 .NET Framework 尚未暴露此功能。你必须通过 P/Invoke 调用原生代码来利用它。有关此的更多信息，请参阅 `System.Transactions.Scope` 类。

- 你可以设计你的方法更加显式。例如，`Monitor` 类通常用于如下获取/释放线程锁。

```
public static class SomeType {
    private static Object s_myLockObject = new Object();
```

```
public static void someMethod () {
    Monitor.Enter(s_myLockObject); // 如果这里抛出异常，锁是否被获取了
    // 没有？如果获取了，它将不会被释放！

    try {
        // 在此处执行线程安全操作...
    }
    finally {
        Monitor.Exit(s_myLockObject);
    }
}
// ...
}
```

由于刚才显示的问题，之前使用的 `Monitor.Enter` 方法的重载现在不再被推荐，建议按照如下方式重写代码。

```
public static class SomeType {
    private static Object s_myLockObject = new Object();
```

```code
public static void someMethod () {
    Boolean lockTaken = false; // 假设锁未被获取
    try {
        // 无论是否抛出异常，这都是有效的
        Monitor.Enter(s_myLockObject, ref lockTaken);

// 在此处执行线程安全操作...
    }
    finally {
        // 如果锁被获取，则释放它
        if (lockTaken) Monitor.Exit(s_myLockObject);
    }
}
// ...
}
```

这段代码中的显式化是一种改进。在线程同步锁的情况下，现在的建议是完全不要将它们与异常处理一起使用。更多信息请参阅第 30 节“混合线程同步构造”。

如果在你的代码中，你已经确定状态已经损坏到无法修复，你应该销毁任何损坏的状态，使其不会产生额外的危害。重启你的应用程序，使你的状态初始化到良好状态，并希望状态损坏不会再次发生。因为托管状态不会泄漏到 AppDomain 之外，你可以通过调用 `AppDomain.Unload` 方法卸载整个 AppDomain 来销毁其内部任何损坏的状态（详情请见第 22 节）。

而且，如果你觉得你的状态糟糕到应该终止整个进程，那么就调用 `Environment` 的静态方法 `FailFast`。

```
public static void FailFast(String message);
public static void FailFast(String message, Exception exception);
```

该方法会终止进程，而不运行任何活跃的 try/finally 块或 Finalize 方法。这样做是好的，因为在状态损坏时执行更多代码很容易让情况变得更糟。然而，`FailFast` 会允许任何 `CriticalFinalizer` 派生对象（在第 21 节“托管堆和垃圾收集”中讨论）有机会进行清理。这是可以，因为它们倾向于关闭原生资源，即使 CLR 状态或你的应用程序状态损坏，Windows 状态可能仍然良好。`FailFast` 将消息字符串和任何可选异常（通常是 catch 块中捕获的异常）写入应用程序事件日志，产生 Windows 错误报告，创建应用程序内存转储并终止当前进程。

> 重要 如果你的代码捕捉了通过 FCL 代码的异常并继续使用 FCL 对象，这些对象可能会变得不可预测。遗憾的是，更多的 FCL 对象在遇到意外异常时无法更好地维护其状态，或者在状态无法恢复时调用 `FailFast`。

本讨论的目的是让人们意识到与使用 CLR 异常处理机制相关的潜在问题。大多数应用程序无法容忍在损坏的状态下运行，这会导致错误数据和安全漏洞。如果你正在编写一个无法容忍的应用程序（如操作系统或数据库引擎），那么托管代码并不是一个很好的技术。尽管 Microsoft Exchange Server 大程度上是用托管代码编写的，但它使用原生数据库来存储电子邮件消息。该原生数据库称为 Extensible Storage Engine（扩展存储引擎）；它随 Windows 发布，可以在 `C:\Windows\System32\Esent.dll` 找到。如果你愿意，你的应用程序可以使用此引擎：在微软网站上搜索“Extensible Storage Engine”。

对于可以容忍状态可能损坏时应用程序应用程序托管应用程序是一个良好的代码。有很多应用程序属于这一类。此外，编写健壮的原生类库或应用程序需要更多的资源和技能；对于许多应用程序，托管代码是更好的选择，因为它极大地提高了程序员的生产力。

# 指南与最佳实践

理解异常机制确实很重要。理解如何明智地使用异常同样重要。我经常看到库开发者捕捉各种异常，阻止了应用程序开发者知道发生了问题。在这一节中，我为开发者提供了一些在使用异常时需要注意的指南。

> 重要 如果你是类库开发者，正在开发将供其他开发者使用的类型，请认真对待这些指南。你肩负着巨大的责任：你正尝试设计类库中的类型，使其对各种应用程序都有意义。因为你对你回调的代码（通过委托、虚或接口方法）没有深入了解。你不知道是哪个代码在调用你。预判你的类型可能出现的每一种是不可能的，所以不要做任何策略决策。你的代码不能决定什么条件限制了错误；让调用者做出该决定。

此外，密切观察并不要损坏它。使用代码合约（本章将讨论）验证传递给你方法的参数。尽量不要在执行中途修改状态。做好失败的准备，然后尝试恢复状态。如果你遵循本章中的指南，应用程序开发者在使用你类库中的类型时将不会遇到困难。

如果你是应用程序开发者，请定义你认为合适的任何策略。遵循本章的指南将帮助你在发布之前发现代码中的问题，从而修复它们并使你的应用程序更加健壮。然而，在仔细考虑后，可以偏离这些指南。由你设定策略。例如，应用程序代码可以比类库代码更激进地捕捉异常。

# 字面意思使用 finally 块

我认为 finally 块太棒了！它们允许你指定一个无论线程抛出何种异常都能保证执行的代码块。你应该使用 finally 块来清理任何在返回调用者之前或调用 finally 块之前成功启动的操作。你还经常使用 finally 块来显式释放任何对象以避免资源泄漏。这里有一个将所有清理代码（关闭文件）放在 finally 块中的示例。

```cs
using System;
using System.IO;

public sealed class SomeType {
    private void SomeMethod() {
        FileStream fs = new FileStream("C:\Data.bin", FileMode.Open);
        try {
```

478 第四 部分 核心设施
