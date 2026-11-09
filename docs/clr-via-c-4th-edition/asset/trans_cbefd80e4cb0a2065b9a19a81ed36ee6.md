
你可以采取以下几项措施来*帮助*缓解状态损坏：

-   CLR 不允许在线程执行 catch 或 finally 块内的代码时中止该线程。因此，我们可以通过执行以下操作来让 Transfer 方法更加稳健。

    ```
    public static void Transfer(Account from, Account to, Decimal amount) {
       try { /* do nothing in here */ }
       finally {
          from -= amount;
          // Now, a thread abort (due to Thread.Abort/AppDomain.Unload) can't happen here
          to += amount;
       }
    }
    ```

    但是，绝对不建议你把所有代码都写在 finally 块中！你只应将此技术用于修改极其敏感的状态。

-   你可以使用 System.Diagnostics.Contracts.Contract 类将代码契约应用于方法。代码契约提供了一种方式，让你在尝试通过这些参数/变量修改状态之前，先验证参数和其他变量。如果参数/变量满足契约，那么状态损坏的*可能性*就会降到最低（但并未完全消除）。如果契约失败，则会在修改任何状态之前抛出异常。我将在本章后面讨论代码契约。

-   你可以使用受约束执行区域（CER），它提供了一种从场景中消除某些 CLR 不确定性的方法。例如，在进入 try 块之前，你可以让 CLR 加载任何关联的 catch 和 finally 块中的代码所需的所有程序集。此外，CLR 将编译 catch 和 finally 块中的所有代码，包括从这些块内部调用的所有方法。这将消除在尝试执行错误恢复代码（在 catch 块中）或清理代码（在 finally 块中）时可能发生的一批潜在异常（包括 FileLoadException、BadImageFormatException、InvalidProgramException、FieldAccessException、MethodAccessException、MissingFieldException 和 MissingMethodException）。它还会降低 OutOfMemoryException 以及一些其他异常发生的可能性。我将在本章后面讨论 CER。

-   根据状态所在的位置，你可以使用事务来确保要么修改所有状态，要么不修改任何状态。例如，如果数据位于数据库中，事务就能很好地工作。Windows 现在也支持事务性注册表和文件操作（仅在 NTFS 卷上），因此你或许可以使用这一功能；但是，.NET Framework 目前并不直接公开此功能。你必须通过 P/Invoke 调用本机代码才能利用它。有关更多详细信息，请参见 System.Transactions.TransactionScope 类。

## 准则与最佳实践

理解异常机制固然重要。同样重要的是，理解如何明智地使用异常。我常常看到库开发者捕获各种异常，导致应用程序开发者无法知道已经发生问题。在本节中，我将提供一些开发人员在使用异常时应注意的准则。

> **重要** 如果你是一名*类库开发者*，正在开发将被其他开发者使用的类型，请非常认真地对待这些准则。你肩负着重大的责任：你要在类库中设计类型，使其对各种各样的应用程序都有意义。请记住，你并不深入了解自己将要回调的代码（通过委托、虚方法或接口方法）。你也不知道是哪些代码在调用你。预判你的类型会被用于何种场景并不可行，所以不要做出任何策略性决定。你的代码绝不能决定什么条件构成错误；让调用方做出该决定。
> 
> 此外，要密切关注状态，尽量不要损坏它。使用代码契约（本章后面会讨论）验证传递给方法的参数。尽量不要修改状态。如果你确实修改了状态，就要为失败做好准备，并尝试恢复状态。如果你遵循本章中的准则，应用程序开发者在使用你的类库中的类型时就不会感到困难。
> 
> 如果你是一名*应用程序开发者*，请定义你认为合适的任何策略。遵循本章中的设计准则将帮助你在代码发布之前发现问题，从而修复问题并使应用程序更加稳健。不过，在仔细考虑之后，你也可以自由地偏离这些准则。策略由你设定。例如，应用程序代码在捕获异常方面可以比类库代码更激进。

### 大方地使用 finally 块

我认为 finally 块非常棒！它们允许你指定一个代码块，无论线程抛出何种异常，该代码块都保证会执行。你应该使用 finally 块来清理任何已成功启动的操作，然后再返回到调用方，或允许 finally 块之后的代码执行。你也经常使用 finally 块来显式释放对象，以避免资源泄漏。下面是一个示例，它将所有清理代码（关闭文件）都放在 finally 块中。

```csharp
using System;
using System.IO;

public sealed class SomeType {
    private void SomeMethod() {
        FileStream fs = new FileStream(@"C:\Data.bin ", FileMode.Open);
        try {
            // Display 100 divided by the first byte in the file.
            Console.WriteLine(100 / fs.ReadByte());
        }
        finally {
            // Put cleanup code in a finally block to ensure that the file gets closed regardless
            // of whether or not an exception occurs (for example, the first byte was 0).
            if (fs != null) fs.Dispose();
        }
    }
}
```

确保清理代码始终执行非常重要，因此许多编程语言提供了让编写清理代码更容易的构造。例如，每当你使用 lock、using 和 foreach 语句时，C# 语言都会自动生成 try/finally 块。每当你重写类的析构函数（Finalize 方法）时，C# 编译器也会生成 try/finally 块。使用这些构造时，编译器会将你编写的代码放入 try 块，并自动将清理代码放入 finally 块。具体来说：

-   当你使用 lock 语句时，锁会在 finally 块内释放。
-   当你使用 using 语句时，对象的 Dispose 方法会在 finally 块内被调用。
-   当你使用 foreach 语句时，IEnumerator 对象的 Dispose 方法会在 finally 块内被调用。
-   当你定义析构函数方法时，基类的 Finalize 方法会在 finally 块内被调用。

例如，下面的 C# 代码利用了 using 语句。这段代码比上一个示例中显示的代码更短，但编译器生成的代码与上一个示例中生成的代码完全相同。

```csharp
using System;
using System.IO;

internal sealed class SomeType {
    private void SomeMethod() {
        using (FileStream fs = new FileStream(@"C:\Data.bin", FileMode.Open)) {
            // Display 100 divided by the first byte in the file.
            Console.WriteLine(100 / fs.ReadByte());
        }
    }
}
```

有关 using 语句的更多信息，请参见第 21 章；有关 lock 语句的更多信息，请参见第 30 章。

### 不要捕获所有异常

那些未接受过正确使用异常培训的开发者普遍会犯的一个错误，就是过于频繁且不恰当地使用 catch 块。当你捕获异常时，你是在声明你预料到了这个异常，你理解它为何发生，并且你知道如何处理它。换句话说，你是在为应用程序定义策略。这一切都要回到本章前面的“用可靠性换取生产力”一节。

我常常看到像这样的代码。

```csharp
try {
    // try to execute code that the programmer knows might fail...
}
catch (Exception) {
    ...
}
```

这段代码表明它预期任何及所有异常，并且知道如何从任何及所有情况中恢复。这怎么可能呢？作为类库一部分的类型，在任何情况下都绝对不应该捕获并吞掉所有异常，因为该类型无法确切知道应用程序打算如何响应异常。此外，该类型会经常通过委托、虚方法或接口方法调用应用程序代码。如果应用程序代码抛出异常，应用程序的另一部分很可能期望捕获这个异常。应该允许异常沿着调用栈向上传递，并让应用程序代码自行决定如何处理该异常。

如果异常未被处理，CLR 将终止进程。我将在本章后面讨论未处理异常。大多数未处理异常都会在代码测试期间被发现。要修复这些未处理异常，你要么修改代码以查找特定异常，要么重写代码以消除导致异常被抛出的条件。最终将在生产环境中运行的代码版本应该很少遇到未处理异常，并且会极其稳健。

> **注意** 在某些情况下，无法完成其任务的方法会检测到某个对象的状态已损坏且无法恢复。允许应用程序继续运行可能会导致不可预测的行为或安全漏洞。检测到这种情况时，该方法不应抛出异常；相反，它应通过调用 System.Environment 的 FailFast 方法强制进程立即终止。

顺便说一下，捕获 System.Exception 并在 catch 块的大括号内执行一些代码是可以的，只要你在该代码的末尾重新抛出异常。绝不应该捕获 System.Exception 并吞掉异常（不重新抛出它），因为这会隐藏失败，使应用程序在不可预测的结果和潜在安全漏洞下继续运行。Visual Studio 的代码分析工具（FxCopCmd.exe）会标记任何包含 catch (Exception) 块的代码，除非该块的代码中包含 throw 语句。关于“从部分完成的状态中退出”
