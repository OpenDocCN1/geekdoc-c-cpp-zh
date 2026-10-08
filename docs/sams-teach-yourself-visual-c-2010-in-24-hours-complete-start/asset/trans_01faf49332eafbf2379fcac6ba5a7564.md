

## 亲自试一试

### 处理异常

要了解如何通过抛出和捕获几种不同的异常来处理异常，请按照以下步骤操作。

1.  创建一个新的控制台应用程序。

2.  在 `Program.cs` 文件中，实现以下函数：
    ```csharp
    private static void ThrowsException()
    {
        Console.WriteLine("即将抛出 InvalidOperationException");
        throw new InvalidOperationException();
    }
    private static void PrintString(string message)
    {
        if (message == null)
        {
            throw new ArgumentNullException("message");
        }
        Console.WriteLine(message);
    }
    ```

3.  在 `Program.cs` 文件的 `Main` 方法中，调用 `ThrowsException` 方法。

4.  使用 Ctrl+F5 运行应用程序。你会首先看到控制台窗口，如**图 10.1** 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_255_0.png)

**图 10.1** 由缺乏类型安全导致的运行时异常

如果你运行的是 Windows Vista 或更高版本，可能会看到**图 10.2** 中所示的对话框。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_255_1.png)

**图 10.2** 检查解决方案的 Windows 应用程序故障对话框

Visual C# 2010 Express 版不支持 JIT 调试，因此在该对话框完成后，你将看到显示的异常信息，如**图 10.3** 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_256_0.png)

**图 10.3** 异常信息和堆栈跟踪详细信息

显示的信息是异常信息，表明这是一个未处理的 `System.InvalidOperationException` 类型的异常。它还显示了堆栈跟踪信息，其中包括方法调用堆栈、文件名和行号。这些堆栈跟踪信息有助于你识别代码中发生异常的位置。

如果你安装了带有 MSDN 版本的 Visual Studio，你会看到一个对话框，如**图 10.4** 所示，允许你关闭或调试应用程序。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_256_1.png)

**图 10.4** 关闭或调试应用程序对话框

5.  如果你按下“关闭程序”按钮，控制台窗口应看起来像**图 10.3**。如果你按下“调试”按钮，你会看到 Visual Studio 即时（Just-In-Time）调试器对话框。

6.  再次使用 Ctrl+F5 运行应用程序，但这次当出现**图 10.3** 所示的对话框时，按下“调试”按钮。这将显示 Visual Studio 即时调试器对话框，如**图 10.5** 所示。

如果你按下“是”按钮，控制权将返回 Visual Studio，并且包含异常的该行被设置为当前语句，如**图 10.6** 所示。

通过点击“操作”下方的“查看详细信息”链接，你可以看到异常的详细信息，如**图 10.7** 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_257_0.png)

**图 10.5** Visual Studio 即时调试器对话框

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_257_1.png)

**图 10.6** 异常助手

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_257_2.png)

**图 10.7** 异常详细信息对话框

7.  将 `ThrowsException` 的调用包裹在一个 try/catch 块中，专门捕获 `InvalidOperationException` 并将其赋值给名为 `ex` 的捕获处理程序变量。在捕获处理程序主体中，打印 `Message` 属性的值。

8.  使用 Ctrl+F5 运行应用程序。你会看到**图 10.8** 所示的控制台窗口。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_258_0.png)

**图 10.8** 已处理异常的控制台输出

请注意，这次应用程序没有终止，而是显示了与异常相关联的消息。

9.  将 Main 的主体更改为以下内容：

```csharp
try
{
    PrintString(null);
}
catch (InvalidOperationException ex)
{
    Console.WriteLine(ex.GetType().Name);
    Console.WriteLine(ex.Message);
}
catch (ArgumentNullException ex)
{
    Console.WriteLine(ex.GetType().Name);
    Console.WriteLine(ex.Message);
}
catch (Exception ex)
{
    Console.WriteLine(ex.GetType().Name);
    Console.WriteLine(ex.Message);
}
```

10. 使用 Ctrl+F5 运行应用程序。你会看到**图 10.9** 所示的控制台窗口。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_258_1.png)

**图 10.9** `ArgumentNullException` 的控制台输出

11. 现在更改 catch 处理程序的顺序，使 `catch(Exception)` 处理程序位于最前。你应该注意到立即出现两个编译器错误，表明额外的两个 catch 处理程序将不会执行，因为之前的处理程序捕获了基类异常类型，如**图 10.10** 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_259_0.png)

**图 10.10** 顺序错误的多个 catch 处理程序

通常，你应避免在代码中捕获非具体的异常，例如 `Exception`、`SystemException` 和 `ExternalException`。你也应避免捕获关键的系统异常，例如 `StackOverflowException` 或 `OutOfMemoryException`。对于这些类型的异常，通常无法做出有意义的响应来加以处理，而捕获它们可能会掩盖运行时问题，并使调试和故障排除过程复杂化。

## 损坏状态异常

损坏状态异常是指在你的应用程序之外（例如操作系统内核中）发生的异常，表明正在运行的进程完整性可能存在问题。大约有 12 种损坏状态异常，它们与常规异常不同。

常规异常和损坏状态异常之间的区别不在于异常的类型，而在于其抛出的上下文。默认情况下，即使你捕获 `Exception`，也无法使用 catch 块捕获损坏状态异常。

### 顺便说一下

### 重新抛出捕获的异常

如果你捕获异常的目的仅仅是用于日志记录或其他实际上并未处理异常条件的活动，你应该重新抛出该异常。重新抛出异常使其能够继续沿着调用堆栈向上寻找合适的 catch 处理程序。

正如 `throw` 关键字允许你指定要抛出的新异常（如前一小节所见），它也用于重新抛出异常。

为了保留堆栈跟踪信息，即使你的 catch 处理程序包含一个捕获处理程序变量，你也应该仅使用 `throw` 关键字来重新抛出异常。清单 10.3 中显示的两种重新抛出方法之间存在一个细微差别，直到你尝试调试问题前不会明显显现。这个差别在于随异常发送的堆栈跟踪信息。

## 清单 10.3 重新抛出异常

```csharp
try
{
    // 导致 InvalidOperationException 的某个操作
}
catch (InvalidOperationException ex)
{
    Console.WriteLine("发生了无效操作");
    throw ex;
}
catch (Exception)
{
    Console.WriteLine("通用 catch 处理程序");
    throw;
}
```

在第一种方法中，针对 `InvalidOperationException` 的 catch 处理程序使用 `throw ex` 重新抛出异常，这导致堆栈跟踪在失败的方法以下被截断。这意味着当你查看堆栈跟踪时，看起来异常似乎源自你的代码。但这并不总是事实，特别是当你正在向上冒泡一个由 CLR 生成的异常（例如 `SqlException`）时。

这是一个被称为“破坏堆栈”的问题，因为你不再拥有完整的堆栈跟踪信息。这之所以发生，本质上是因为你正在创建一个新的异常来抛出。

通过使用单独的 `throw`（如针对 `Exception` 的 catch 处理程序所做的那样），你可以保留堆栈跟踪信息。你可以通过查看为这两个代码块生成的 IL（中间语言）来确认这一点。这使得区别显而易见，因为在第一个示例中，调用的 IL 指令是 `throw`，而在第二个中，调用的指令是 `rethrow`。

## 包装异常

你还可以将捕获的异常包装在另一种异常中，然后抛出该新异常。这通常用于实际异常没有提供有意义的信息或在上层上下文中没有意义的情况。

当你包装异常时，你从 catch 处理程序中抛出一个新异常，并且应始终将原始异常包含为内部异常。由于堆栈跟踪信息重置到新异常发生的点，包含内部异常是查看原始堆栈跟踪和异常详情的唯一方法。清单 10.4 展示了抛出包装异常的正确方式。

