

{
    try
    {
        // ...
        throw new InvalidOperationException (
            "Arbitrary exception");
        // ...
    }
    catch (NullReferenceException exception)
    {
        // Handle NullReferenceException
    }
    catch (ArgumentException exception)
    {
        // Handle ArgumentException
    }
    catch (InvalidOperationException exception)
    {
        // Handle ApplicationException
    }
    catch (SystemException exception)
    {
        // Handle SystemException
    }
    catch (Exception exception)
    {
        // Handle Exception
    }
    catch
    {
        // Any unhandled exception
    }
}

通用 catch 块会捕获所有异常，无论它们是否派生自 System.Exception，前提是较早的 catch 块未捕获它们。此类块的缺点仅在于无法访问异常实例，因此也无法知道应采取的适当措施。甚至无法识别这种异常无害的罕见情况。最佳做法是在关闭应用程序之前，使用一些清理代码来处理异常。例如，catch 块可以在关闭应用程序或重新抛出异常之前保存任何易失性数据。

## 高级主题

### 空 catch 块内部

与空 catch 块对应的 CIL 代码实际上是一个 catch(object) 块。这意味着无论抛出的类型是什么，空 catch 块都会捕获它。有趣的是，在 C# 代码中无法显式声明 catch(object) 异常块。因此，无法捕获非 System.Exception 派生的异常并拥有可供审查的异常实例。

具有讽刺意味的是，来自 C++ 等语言的非托管异常通常会导致 System.Runtime.InteropServices.SEHException 类型的异常，这些异常派生自 System.Exception 类型。因此，不仅可以使用通用 catch 块捕获非托管类型异常，还可以捕获抛出的非 System.Exception 托管类型——例如 string 等类型。

### 异常处理准则

异常处理为先前的错误处理机制提供了急需的结构。但是，如果使用不当，它仍可能产生一些笨拙的结果。以下准则提供了一些异常处理的最佳实践。

- 仅捕获你能处理的异常。
  通常可以处理某些类型的异常，但不能处理其他类型。例如，以独占读写方式打开文件可能会因为文件正在使用而抛出 System.IO.IOException。在捕获此类异常时，代码可以向用户报告文件正在使用，并允许用户选择取消操作或重试。只有有已知措施可采的异常才应被捕获。其他异常类型应留给调用栈中更高层的调用者处理。

- 不要隐藏（掩盖）你未完全处理的异常。
  新程序员常常想捕获所有异常，然后继续执行，而不是向用户报告未处理的异常。然而，这可能导致关键系统问题未被发现。除非代码采取显式操作来处理异常，或明确判定某些异常无害，否则 catch 块应重新抛出异常，而不是捕获并向调用者隐藏它们。绝大多数情况下，catch (System.Exception) 和通用 catch 块应出现在调用栈中较高的位置，除非该块以重新抛出异常结束。

- 很少使用 System.Exception 和通用 catch 块。
  几乎所有异常都派生自 System.Exception。但是，处理某些 System.Exception 的最佳方式是允许它们未被处理，或尽早优雅地关闭应用程序，而不是拖延。这些异常包括 System.OutOfMemoryException 和 System.StackOverflowException 等。在 CLR 4 中，此类异常默认为不可恢复，因此在不重新抛出的情况下捕获它们会导致 CLR 无论如何都会重新抛出。这些异常是运行时异常，开发人员无法编写代码来从中恢复。因此，最佳做法是关闭应用程序——CLR 4 中运行时会强制执行此操作。CLR 4 之前的代码应仅在关闭应用程序或使用 throw; 重新抛出异常之前，捕获此类异常以运行清理或紧急代码（例如保存任何易失性数据）。

- 避免在调用栈较低位置报告或记录异常。
  程序员常常想在调用栈中尽早的位置记录异常或向用户报告异常。然而，这些位置很少能完全处理异常，因此会采取重新抛出异常的方式。此类 catch 块不应在调用栈深处记录异常或向用户报告。如果异常被记录并重新抛出，调用栈中较高位置的调用者可能会做同样的事情，导致重复的异常日志条目。更糟的是，向用户显示异常可能不适合该类型的应用程序。（例如，在 Windows 应用程序中使用 System.Console.WriteLine() 用户永远看不到，在无人值守的命令行进程中显示对话框可能被忽略并导致应用程序冻结。）与日志记录和异常相关的用户界面应保留给调用栈中较高的位置。

- 在 catch 块中使用 throw; 而不是 throw <exception object>。

  可以在 catch 块内重新抛出异常。例如，catch(ArgumentNullException exception) 的实现可以包含对 throw exception 的调用。但是，这样重新抛出异常会将堆栈跟踪重置为重新抛出调用的位置，而不是重用原始抛出点位置。因此，除非你使用不同的异常类型重新抛出或故意隐藏原始调用堆栈，否则请使用 throw; 以允许相同的异常沿调用栈向上传播。

- 重新抛出不同异常时需谨慎。

  在 catch 块内部，重新抛出不同的异常不仅会重置抛出点，还会隐藏原始异常。要保留原始异常，请设置新异常的 InnerException 属性，通常可通过构造函数赋值。重新抛出不同的异常应仅限于以下情况。

  - 1. 更改异常类型能澄清问题。

    例如，在调用 Logon(User user) 时，当用户列表文件不可访问时，重新抛出不同的异常类型可能比传播 System.IO.IOException 更合适。

  - 2. 私有数据是原始异常的一部分。

    在前述场景中，如果文件路径包含在原始 System.IO.IOException 中，从而暴露了系统的私有安全信息，则应包装异常。当然，这假设 InnerException 未设置为原始异常。（有趣的是，CLR v1 的一个非常早期版本（甚至是 pre-alpha）曾有一个异常，内容类似于“安全异常：您无权确定 c:\temp\foo.txt 的路径”。）

  - 3. 异常类型过于特定，调用者无法适当处理。

    例如，与其抛出特定于特定数据库系统的异常，不如使用更通用的异常，以避免调用栈中更高位置的数据库特定代码。

### 定义自定义异常

一旦抛出异常成为最佳做法，最好使用框架异常，因为它们已得到充分确立和理解。例如，与其抛出自定义无效参数异常，不如使用 System.ArgumentException 类型。但是，如果使用特定 API 的开发人员会采取特殊操作——例如，异常处理逻辑会因处理自定义异常类型而有所不同——那么定义自定义异常是合适的。例如，如果映射 API 接收到一个邮政编码无效的地址，与其抛出 System.ArgumentException，不如抛出自定义 InvalidAddressException。关键在于调用者是否可能编写特定的 ValidAddressException catch 块并进行特殊处理，而不仅仅是编写通用的 System.ArgumentException catch 块。定义自定义异常只需从 System.Exception 或其他异常类型派生即可。清单 10.4 提供了一个示例。

```
LISTING 10.4: Creating a Custom Exception

class DatabaseException : System.Exception
{
    public DatabaseException(
        System.Data.SqlClient.SqlException exception)
    {
        InnerException = exception;
        // ...
    }

    public DatabaseException(
        System.Data.OracleClient.OracleException exception)
    {
        InnerException = exception;
        // ...
    }

    public DatabaseException()
    {
        // ...
    }

    public DatabaseException(string message)
    {
        // ...
    }
}
```

