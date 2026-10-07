

# 异常处理指南 611

新程序员往往倾向于捕获所有异常并继续执行，而不是向用户报告未处理的异常。然而，这种做法可能导致关键问题无法被发现。除非代码采取显式操作处理异常，或明确确定某些异常是无害的，否则 catch 块应该重新考虑异常，而不是捕获它们并对调用者隐藏。在大多数情况下，`catch(System.Exception)` 和通用的 catch 块应该出现在调用堆栈的更高位置，除非该块最后通过重新抛出异常来结束。

- 极少使用 System.Exception 和通用的 catch 块。
所有异常都派生自 System.Exception。但是，处理某些 System.Exceptions 的最佳方法是让它们保持未处理状态或优雅地关闭应用程序，而不是稍后。这些异常包括 `System.OutOfMemoryException` 和 `System.OverflowException` 等情况。幸运的是，此类异常默认处于不可恢复状态，因此捕获它们而不重新抛出会导致 CLR 无论如何都会重新抛出它们。这些异常是开发者无法编写代码来恢复的运行时异常。因此，最佳行动方案是关闭应用程序——这是运行时强制要求的。

- 避免在调用堆栈中进行异常报告或记录。
程序员通常会在调用堆栈中尽可能早的位置报告异常。然而，这些位置能够完全处理异常；相反，它们会诉诸重新抛出异常。catch 块不应该在调用堆栈深处记录异常或向用户报告异常。如果异常被记录并重新抛出，调用堆栈中更高处的调用者可能也会这样做，导致异常的重复日志条目。糟糕糟糕，向用户显示可能不适用于该类型的应用程序。（例如，在 Windows 应用程序中使用 `System.Console.WriteLine()` 用户永远是看不到的，而在无人值守的命令行进程中显示对话框可能不会被注意到并冻结应用程序。）与日志和异常相关的用户界面应该预留给调用堆栈的更高处使用。

> 4 从通用语言运行时 (CLR) 4 开始。在 CLR 4 之前，代码应该捕获此类异常仅是为了在关闭应用程序之前运行清理代码或紧急代码（如保存任何易失数据），或使用 `throw` 重新抛出异常；

# 第 11 章：异常处理

- 在 catch 块内部使用 `throw;` 而不是 `throw <exception object>`。

在 catch 块内部重新抛出异常是可能的。例如，`catch(ArgumentNullException exception)` 的实现可能包含对 `throw exception` 的调用。然而，重新抛出异常会将堆栈跟踪重置为重新抛出调用的位置，而不是重用原始点的位置。因此，除非你使用不同的异常类型重新抛出异常，或者刻意隐藏原始调用堆栈，否则应使用 `throw;` 以允许相同的异常传播到调用堆栈上方。

- 优先使用异常条件以避免在 catch 块内部重新抛出异常。

当你发现自己捕获了一个实际上无法妥善处理且因此需要重新抛出的异常时，请优先使用异常条件来避免从一开始就捕获该异常。

- 避免从异常过滤器中抛出异常。

在提供异常过滤器（exception filter）时，避免使用会抛出异常的代码。从异常过滤器中抛出异常将导致假条件，异常的发生将被忽略。由于此原因，你应该考虑将复杂的条件检查放在单独的方法中，并将该方法封装在 try/catch 块中，以显式处理该异常。

- 避免可能随时间变化的异常条件。

如果异常过滤器评估的条件（如异常消息）可能随本地化或消息的更改而变化，则预期的异常将无法被捕获，从而意外地改变业务逻辑。由于此原因，你应该确保异常条件随时间保持有效。

- 重新抛出不同异常时要小心。

在 catch 块内部重新抛出不同的异常不仅会重置调用堆栈，还会隐藏原始异常。为了保留原始异常，请设置新异常的 `InnerException` 属性，通常可以通过构造函数赋值。重新抛出不同的异常应保留用于以下情况：

# 异常处理指南 613

1. 更改异常类型可以阐明问题。
例如，调用 `Logon(User user)` 时，如果用户列表文件不可访问，重新抛出不同的异常类型可能比传播 `System.IO.IOException` 更合适。

2. 私有数据是原始异常的一部分。
在上述场景中，如果原始的 `System.IO.IOException` 包含了文件路径，从而暴露了系统的私有安全信息，则应该对异常进行封装。当然，这假设了异常是被封装的。

3. 异常类型对于调用者来说太具体。
在某些情况下，抛出的异常对于调用者处理来说太具体。在这种情况下，将异常封装在更通用的异常中可能更好。

## 异常处理指南

- 避免在调用堆栈中进行异常报告或记录。
- 在 catch 块内部使用 `throw;` 而不是 `throw <exception object>`。
- 优先使用异常条件以避免在 catch 块内部重新抛出异常。
- 避免从异常过滤器中抛出异常。
- 避免可能随时间变化的异常条件。
- 重新抛出不同异常时要小心。

# 定义自定义异常

一旦抛出异常成为最佳行动方案，最好是使用框架异常，因为它们已经非常完善。例如，与其抛出自定义异常，不如说是使用 `System.Exception`。然而，关键在于调用者是否可能编写特定的 catch 块而不是通用的 catch 块。

定义自定义异常仅涉及派生自 `System.Exception` 或其他异常类型。列表 11.4 提供了一个示例。

列表 11.4：创建自定义异常

```csharp
class DatabaseException : Exception
{
    public DatabaseException(
        string? message,
        System.Data.SqlClient.SqlLException exception)
        : base(message, exception)
    {
    }
}
```

# 定义自定义异常 615

```csharp
class DatabaseException : Exception
{
    public DatabaseException(
        string? message,
        System.Data.OracleClient.OracleException? exception)
        : base(message, exception)
    {
    }

    public DatabaseException()
    {
    }

    public DatabaseException(string? message)
      : base(message)
    {
    }

    public DatabaseException(
      string? message,
      Exception? exception)
      : base(message, exception)
    {
    }
}
```

此自定义异常可能用于封装特定的数据库异常。由于 Oracle 和 SQL Server（例如）对类似错误抛出不同的异常，应用程序可以定义自定义异常，将数据库异常标准化为应用程序可以处理的通用封装。这样，无论应用程序使用的是 Oracle 还是 SQL Server 后端数据库，都可以在堆栈更高处使用相同的 catch 块来处理错误。

自定义异常的唯一要求是它派生自 System .Exception 或其后代。自定义异常的其他良好实践如下：

- 所有异常都应该使用“Exception”后缀。这样，从名称就可以很容易确立其目的。
- 通常，所有异常都应该包含无参数、字符串参数、以及一个由字符串和内部异常组成的参数set的构造函数。

