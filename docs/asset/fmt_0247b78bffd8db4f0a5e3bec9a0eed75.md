
```csharp
using System;

public sealed class Program
{
    public static void Main()
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
        catch (Exception exception)
        {
            // Handle Exception
        }
        catch
        {
            // Any unhandled exception
        }
        finally
        {
            // Handle any cleanup code here as it runs
            // regardless of whether there is an exception
        }
    }
}
```

通用 `catch` 块将捕获所有异常，无论它们是否派生自 `System.Exception`，前提是前面的 `catch` 块没有捕获它们。这种块的缺点仅仅是没有异常实例可供访问，因此没有方法来知道适当的应对措施。甚至不可能识别出这种异常是无害的罕见情况。最好的应对方式是在关闭应用程序之前，通过一些清理代码来处理异常。例如，`catch` 块可以在关闭应用程序或重新抛出异常之前保存任何易失性数据。

## 高级主题

### 通用 Catch 块内部机制

通用 `catch` 块对应的公共中间语言 `CIL` 代码实际上是一个 `catch(object)` 块。因此，无论抛出的是什么类型，通用 `catch` 块都会捕获它。有趣的是，在 C# 代码中无法显式声明一个 `catch(object)` 异常块。因此，没有办法捕获非 `System.Exception` 派生的异常并拥有一个异常实例来审查。

事实上，来自 C++ 等语言的未托管异常通常会导致 `System.Runtime.InteropServices.SEHException` 类型的异常，这些异常派生自 `System.Exception` 类型。因此，不仅可以使用通用 `catch` 块捕获未托管类型的异常，还可以捕获抛出的非 `System.Exception` 托管类型——例如，诸如 `string` 这样的类型。

## 异常处理指南

异常处理为之前错误处理机制提供了急需的结构。然而，如果随意使用，它仍然可能导致一些笨拙的结果。以下指南提供了一些异常处理的最佳实践。

- *仅捕获你可以处理的异常。*

通常，可以处理某些类型的异常，但不能处理其他类型。例如，以独占读写方式打开文件可能会抛出 `System.IO.IOException`，因为文件已在使用中。在捕获此类型的异常时，代码可以报告给用户该文件已在使用，并允许用户选择取消操作或重试。仅应捕获已知有应对措施的其他异常类型。其他异常类型应留给调用栈中更高层级的调用者。

- *不要隐藏（*埋葬*）你未完全处理的异常。*

新程序员常常倾向于捕获所有异常，然后继续执行，而不是向用户报告未处理的异常。然而，这种做法可能导致严重的系统问题未被检测到。除非代码采取明确措施来处理异常，或明确确定某些异常是无害的，否则 `catch` 块应重新抛出异常，而不是捕获它们并将它们从调用者那里隐藏起来。在大多数情况下，捕获 `System.Exception` 和通用 `catch` 块应位于调用栈中的较高层级，除非该块以重新抛出异常结束。

- *很少使用 `System.Exception` 和通用 `catch` 块。*

几乎所有异常都派生自 `System.Exception`。然而，处理某些 `System.Exception` 的最佳方式是让它们未被处理，或尽早优雅地关闭应用程序。这些异常包括诸如 `System.OutOfMemoryException` 和 `System.StackOverflowException` 等。在公共语言运行时 `CLR` 4 中，这些异常默认设为不可恢复，这意味着如果不重新抛出就捕获它们，`CLR` 仍然会重新抛出它们。这些异常是运行时异常，开发人员无法编写代码来从中恢复。因此，最佳措施是关闭应用程序——这是在 `CLR` 4 及更高版本中运行时强制执行的操作。`CLR` 4 之前的代码仅在关闭应用程序或重新抛出异常之前运行清理或紧急代码（例如保存任何易失性数据）时才应捕获此类异常，并使用 `throw;` 重新抛出异常。

- *避免在调用栈较低层级进行异常报告或记录。*

通常，程序员倾向于在调用栈中尽可能早的位置记录异常或向用户报告异常。然而，这些位置很少能够完全处理异常；相反，它们诉诸于重新抛出异常。此类 `catch` 块在调用栈内部时不应记录异常或向用户报告。如果异常被记录并重新抛出，调用栈中较高层级的调用者可能会执行相同的操作，导致异常的日志条目重复。更糟糕的是，向用户显示异常可能不适合应用程序类型。例如，在 Windows 应用程序中使用 `System.Console.WriteLine()` 永远不会被用户看到，而在无人值守的命令行进程中显示对话框可能不会被注意到并冻结应用程序。日志记录和与异常相关的用户界面应保留用于调用栈中的较高位置。

- *在 *catch 块* 内部使用 *throw* 而不是 *throw* <i><异常对象></i>。*

可以在 `catch` 块内部重新抛出异常。例如，`catch (ArgumentNullException *exception*)` 的实现可以包含对 *throw exception* 的调用。然而，像这样重新抛出异常会将堆栈跟踪重置到重新抛出调用的位置，而不是重用原始抛出点位置。因此，除非你要使用不同的异常类型重新抛出或有意隐藏原始调用堆栈，否则使用 *throw* 让相同的异常沿调用栈向上传播。

- *优先使用 *异常条件* 以避免在 *catch 块* 内部重新抛出 *异常*。*

当你发现自己捕获了一个实际上无法适当处理的异常，因此需要重新抛出时，优先考虑使用异常条件来避免一开始就捕获该异常。

- *避免从 *异常条件* 中 *抛出异常*。*

在提供异常条件时，避免抛出异常的代码。从异常条件中抛出异常会导致错误的条件，并且异常发生将被忽略。因此，考虑将复杂的条件检查放入一个单独的方法中，该方法被包裹在一个明确处理异常的 `try/catch` 块中。

- *避免可能随时间变化的异常条件。*

如果异常条件评估诸如异常消息等可能会随本地化或消息更改而变化的条件，预期的异常条件将不会被捕获，从而意外地改变业务逻辑。因此，确保异常条件在时间上是有效的。

- *重新抛出不同异常时需谨慎。*

从 `catch` 块内部重新抛出不同的异常不仅会重置抛出点，还会隐藏原始异常。为了保留原始异常，设置新异常的 `InnerException` 属性，通常可以通过构造函数赋值。重新抛出不同的异常应保留用于以下情况：

1. *更改异常类型使问题更清晰。*

    例如，在对 `Logon(User user)` 的调用中，当用户列表文件不可访问时，重新抛出不同的异常类型可能比传播 `System.IO.IOException` 更合适。

2. *私有数据是原始异常的一部分。*

    在前面的场景中，如果原始 `System.IO.IOException` 中包含了文件路径，从而暴露了关于系统的私有安全信息，则应包装异常。当然，这假设 `InnerException` 未设置为原始异常。（有趣的是，`CLR` v1 的一个非常早期的版本 [即使是预发布版] 有一个异常，其中写着类似“安全异常：您没有权限确定 `c:\temp\foo.txt` 的路径”的内容）

3. *异常类型对于调用者来说太具体，无法适当处理。*

    例如，而不是抛出特定于特定数据库系统的异常，使用更通用的异常，以便避免调用栈中较高层级的数据库特定代码。

## 指南

避免在调用堆栈的下层进行异常报告或日志记录。

不要过度捕获异常。除非明确了解如何在堆栈下层通过编程方式处理这些错误，否则应允许异常沿调用堆栈向上传播。

当你了解在特定上下文中抛出异常的原因，并且能够通过编程方式对失败做出响应时，考虑捕获特定的异常。

避免捕获 `System.Exception` 或 `System.SystemException`，除非是在执行最终清理操作后再重新抛出异常的最高层异常处理程序中。

在 `catch` 块中，请使用 `throw` 而不是 `throw <异常对象>`。

使用异常条件来避免从 `catch` 块内部重新抛出异常。

重新抛出不同的异常时要谨慎。

不要抛出 `NullReferenceException`，当值意外为空时，优先使用 `ArgumentNullException`。

避免在异常条件判断中抛出异常。

避免使用可能会随时间变化的异常条件判断。

## 定义自定义异常

一旦确定抛出异常是最佳方案，最好使用框架异常，因为它们已经过充分验证且广为人知。例如，不要抛出自定义的无效参数异常，而是优先使用 `System.ArgumentException` 类型。然而，如果使用特定 API 的开发者需要采取特殊行动——例如，异常处理逻辑会因处理自定义异常类型而有所不同——那么定义自定义异常是合适的。例如，如果映射 API 接收到邮政编码无效的地址，与其抛出 `System.ArgumentException`，不如抛出自定义的 `InvalidAddressException` 可能更好。关键在于调用方是否更有可能编写针对特定 `InvalidAddressException` 的 `catch` 块并进行特殊处理，而不是仅仅使用通用的 `System.ArgumentException` `catch` 块。

定义自定义异常通常涉及从 `System.Exception` 或其他异常类型派生。代码清单 11.5 提供了一个示例。

### 代码清单 11.5：创建自定义异常

```csharp
class DatabaseException : System.Exception
{
    public DatabaseException(
        System.Data.SqlClient.SQLException exception)
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

    public DatabaseException(
        string message, Exception innerException)
    {
        InnerException = innerException;
        // ...
    }
}
```

创建此自定义异常可能是为了包装专有数据库异常。例如，由于 Oracle 和 SQL Server 在类似错误中抛出不同的异常，应用程序可以定义一个自定义异常，将数据库特有的异常标准化为一个常见的异常包装器，以便应用程序以标准方式进行处理。这样，无论应用程序使用的是 Oracle 还是 SQL Server 后端数据库，都可以使用相同的 `catch` 块在堆栈的上层处理错误。

自定义异常的唯一要求是必须从 `System.Exception` 或其子类派生。但是，自定义异常还有几项最佳实践：

- 所有异常都应使用“Exception”后缀。这样，可以通过名称轻松明确其用途。

- 通常，所有异常都应包含接受无参数、字符串参数以及由字符串和内部异常组成的参数集的构造函数。此外，由于异常通常在抛出的同一语句中构造，因此额外的异常数据也应允许作为构造函数的一部分。（创建所有这些构造函数的明显例外是，当某些数据是必需的，而某个构造函数绕过了这些要求时。）

- 继承链应保持相对较浅（大约少于五个层级）。

在重新抛出与捕获到的异常不同的异常时，内部异常起着重要作用。例如，如果数据库调用抛出了 `System.Data.SqlClient.SqlException`，但在数据访问层被捕获并作为 `DatabaseException` 重新抛出，那么接受 `SqlException`（或内部异常）的 `DatabaseException` 构造函数会将原始 `SqlException` 保存在 `InnerException` 属性中。这样，当需要有关原始异常的更多详细信息时，开发人员可以从 `InnerException` 属性中检索该异常（例如，`exception.InnerException`）。

## 指南

- 如果异常的处理方式与现有 `CLR` 异常没有不同，则不要创建新的异常类型。改为抛出现有的框架异常。

- 创建新的异常类型以传达无法使用现有 `CLR` 异常传达的独特程序错误，并且可以以不同于任何其他现有 `CLR` 异常类型的方式进行编程处理。

- 在所有自定义异常类型上提供无参数构造函数。同时提供接受消息和内部异常的构造函数。

- 异常类名应以“Exception”后缀结尾。

- 使异常支持运行时序列化。

- 考虑为异常提供属性，以便对与异常相关的额外信息进行编程访问。

- 避免过深的异常层次结构。

## 高级主题

### 可序列化异常

可序列化对象是运行时可以持久化到流中（例如文件流）然后从流中重新实例化的对象。对于异常而言，这种行为在某些分布式通信技术中可能是必要的。为了支持序列化，异常声明应包含 `System.SerializableAttribute` 特性或实现 `ISerializable`。此外，它们必须包含一个接受 `System.Runtime.Serialization.SerializationInfo` 和 `System.Runtime.Serialization.StreamingContext` 的构造函数。代码清单 11.6 展示了使用 `System.SerializableAttribute` 的示例。

#### 代码清单 11.6：定义可序列化异常

```csharp
// Supporting serialization via an attribute
[Serializable]
class DatabaseException : System.Exception
{
    // ...

    // Used for deserialization of exceptions
    public DatabaseException(
        SerializationInfo serializationInfo,
        StreamingContext context)
    {
        // ...
    }
}
```

上述 `DatabaseException` 示例展示了使异常可序列化的特性和构造函数要求。

请注意，对于 .NET Core，`System.SerializableAttribute` 直到支持 .NET Standard 2.0 之前都不可用。如果你编写的代码将在包括 .NET Standard 2.0 以下版本的多个框架中编译，请考虑定义你自己的 `System.SerializableAttribute` 作为**填充实现（polyfill）**。填充实现是一种代码，用于填补特定版本技术中的空白，从而添加功能或至少提供缺失功能的垫片。

## 重新抛出包装后的异常

有时，在堆栈下层抛出的异常在被上层捕获时不再有意义。例如，考虑由于服务器磁盘空间不足而发生的 `System.IO.IOException`。捕获此类异常的客户端未必能够理解为什么会有 I/O 活动的上下文。同样，考虑一个抛出 `System.UnauthorizedAccessException`（与所调用的 API 完全无关的异常）的地理坐标请求 API。在第二个示例中，调用者没有上下文来理解 API 调用与安全有什么关系。从调用 API 的代码角度来看，这些异常带来的困惑多于诊断帮助。而不是向客户端暴露此类异常，最好先捕获该异常，然后抛出不同的异常，例如 `InvalidOperationException`（甚至可能是自定义异常），作为传达系统处于无效状态的一种方式。在此类场景中，请确保设置包装异常的 `InnerException` 属性（通常通过构造函数调用，如 `new InvalidOperationException(String, Exception)`），以便在更接近被调用框架的地方，有人可以利用额外的上下文信息进行诊断。
