
## try 块

`try` 块包含需要执行常见清理操作、异常恢复操作或同时需要这两种操作的代码。清理代码应放在单个 `finally` 块中。try 块还可以包含可能引发异常的代码。异常恢复代码应放在一个或多个 catch 块中。对于应用程序能够安全恢复的每一种异常，都应创建一个 catch 块。try 块必须至少与一个 catch 或 finally 块关联；单独存在的 try 块没有意义，C# 会阻止你这样做。

> **重要** 有时开发人员会问，他们应该把多少代码放进单个 `try` 块中。答案取决于状态管理。如果在 `try` 块中执行多个操作，而这些操作都可能抛出同一种异常类型，并且你恢复这种异常类型的方式因操作而异，那么就应该把每个操作分别放进各自的 `try` 块中，以便正确恢复状态。

## catch 块

`catch` 块包含为响应异常而执行的代码。try 块可以关联零个或多个 catch 块。如果 try 块中的代码没有导致抛出异常，CLR 将绝不会执行其任何 catch 块中包含的代码。线程将直接跳过所有 catch 块，并执行 `finally` 块中的代码（如果存在）。`finally` 块中的代码执行完毕后，执行将继续进行到 `finally` 块之后的语句。

出现在 `catch` 关键字后的括号表达式称为 *catch 类型*。在 C# 中，必须指定 `System.Exception` 或派生自 `System.Exception` 的 catch 类型。例如，前面的代码包含用于处理 `InvalidOperationException`（或派生自它的任何异常）和 `IOException`（或派生自它的任何异常）的 catch 块。最后一个 catch 块（未指定 catch 类型）会处理除前面 catch 块所指定的异常类型之外的任何异常；这等效于有一个指定 `System.Exception` 作为 catch 类型的 catch 块，不同之处在于你无法通过 catch 块大括号内的代码访问异常信息。

**注意** 使用 Microsoft Visual Studio 调试经过 `catch` 块时，可以通过将特殊的 `$exception` 变量名添加到监视窗口来查看当前抛出的异常对象。

CLR 会从上到下搜索匹配的 catch 类型，因此应将更具体的异常类型放在顶部。最派生的异常类型应最先出现，随后是其基类型（如果有），一直到 `System.Exception`（或不指定 catch 类型的异常块）。事实上，如果更具体的 catch 块出现在更靠近底部的位置，C# 编译器会生成错误，因为该 catch 块将不可达。

如果 `try` 块内执行的代码（或从 try 块内调用的任何方法）抛出异常，CLR 会开始搜索 catch 类型与被抛出异常的类型相同或是其基类型的 catch 块。如果没有任何 catch 类型与该异常匹配，CLR 会继续沿调用堆栈向上搜索与该异常匹配的 catch 类型。如果到达调用堆栈顶部后仍未找到具有匹配 catch 类型的 catch 块，则会发生未处理异常。本章稍后会更详细地讨论未处理异常。

一旦 CLR 找到具有匹配 catch 类型的 catch 块，它就会执行所有内部 *finally* 块中的代码，从代码抛出异常的那个 *try* 块开始，到与该异常匹配的 catch 块为止。注意，与该匹配异常的 catch 块关联的任何 *finally* 块尚未执行。这个 *finally* 块中的代码要等到处理该异常的 catch 块中的代码执行完毕后才会执行。

所有内部 *finally* 块中的代码执行完毕后，处理异常的 catch 块中的代码开始执行。这段代码通常执行一些操作来处理该异常。在 catch 块末尾，你有三种选择：

- 重新抛出同一异常，通知调用堆栈中更高层的代码发生了该异常。
- 抛出不同的异常，向调用堆栈中更高层的代码提供更丰富的异常信息。
- 让线程从 catch 块底部退出。

本章稍后，我将提供一些关于何时应使用每种技术的指导原则。如果你选择前两种技术中的任意一种，你就是在抛出异常，CLR 的行为与之前一样。它会沿调用堆栈向上查找类型与被抛出异常类型匹配的 catch 块。

如果选择最后一种技术，当线程从 catch 块底部退出时，它会立即开始执行 *finally* 块（如果存在）中包含的代码。*finally* 块中的所有代码执行完毕后，线程会离开 *finally* 块，并开始执行紧跟在 *finally* 块之后的语句。如果不存在 *finally* 块，线程将在最后一个 catch 块之后的语句处继续执行。

在 C# 中，可以在 catch 类型之后指定变量名。捕获异常时，该变量引用被抛出的、派生自 System.Exception 的对象。catch 块的代码可以引用该变量来访问特定于该异常的信息（例如导致该异常的堆栈跟踪）。尽管可以修改此对象，但你不应该这样做；应将该对象视为只读。本章稍后我将解释 Exception 类型以及可以用它做什么。

**注意** 你的代码可以向 AppDomain 的 FirstChanceException 事件注册，以便在 AppDomain 内发生异常时立即收到通知。此通知发生在 CLR 搜索任何 catch 块之前。有关此事件的更多信息，请参见第 22 章“CLR 托管与 AppDomain”。

## *finally* 块

*finally* 块包含保证会执行的代码。<sup>12</sup> 通常，*finally* 块中的代码执行 *try* 块中所执行操作需要的清理操作。例如，如果你在 *try* 块中打开文件，就应把关闭文件的代码放在 *finally* 块中：

```csharp
private void ReadData(string pathname) {

    FileStream fs = null;
    try {
        fs = new FileStream(pathname, FileMode.Open);
        // Process the data in the file...
    }
    catch (IOException) {
        // Put code that recovers from an IOException here...
    }
    finally {
        // Make sure that the file gets closed.
        if (fs != null) fs.Close();
    }
}
```

如果 *try* 块中的代码执行时没有抛出异常，则文件保证会被关闭。如果 *try* 块中的代码确实抛出了异常，*finally* 块中的代码仍会执行，并且无论异常是否被捕获，文件都保证会被关闭。把关闭文件的语句放在 *finally* 块之后是不恰当的；如果抛出异常且未被捕获，该语句将不会执行，这会导致文件保持打开状态（直到下一次垃圾回收）。

*try* 块不要求关联 *finally* 块；有时 *try* 块中的代码根本不需要任何清理代码。但是，如果你确实有 *finally* 块，它必须出现在所有 *catch* 块之后。一个 *try* 块最多只能关联一个 *finally* 块。

当线程到达 *finally* 块中包含的代码末尾时，线程会直接开始执行紧跟在 *finally* 块之后的语句。请记住，*finally* 块中的代码是清理代码。这段代码应只执行清理 *try* 块中所启动操作所需的内容。*catch* 和 *finally* 块内的代码应该非常短，并且应很可能成功执行而自身不抛出异常。通常，这些块中的代码只有一两行。

异常恢复代码或清理代码始终有可能失败并抛出一个

12 中止线程或卸载 AppDomain 会导致 CLR 抛出 `ThreadAbortException`，从而允许 *finally* 块执行。如果只是通过 `Win32 TerminateThread` 函数终止线程，或者通过 `Win32 TerminateProcess` 函数或 `System.Environment's FailFast` 方法终止进程，那么 *finally* 块将不会执行。当然，进程终止时，Windows 会清理该进程使用的所有资源。
