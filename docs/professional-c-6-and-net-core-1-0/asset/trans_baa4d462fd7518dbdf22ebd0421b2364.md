

当你捕获异常时，重新抛出异常也很常见。你可以在再次抛出异常时更改异常类型。这样可以向调用方提供有关发生了什么的更多信息。原始异常可能没有足够的信息来说明当时发生的上下文。你也可以记录异常信息并向调用方提供不同的信息。例如，对于运行应用程序的用户来说，异常信息并没有什么帮助。阅读日志文件的系统管理员可以根据情况做出相应的反应。

重新抛出异常的一个问题是，调用方通常需要找出早期异常发生的原因，以及它发生在哪里。根据异常的抛出方式，堆栈跟踪信息可能会丢失。为了让你了解重新抛出异常的不同选项，示例程序 `RethrowExceptions` 展示了不同的选项。

重新抛出异常的代码示例使用了以下依赖项和命名空间：

## Dependencies

```
NETStandard.Library
```

## Namespaces

```
System

static System.Console
```

对于本示例，创建了两种自定义异常类型。第一个 `MyCustomException` 在基类 `Exception` 的成员之外定义了属性 `ErrorCode`；第二个 `AnotherCustomException` 支持传递内部异常（代码文件 `RethrowExceptions/MyCustomException.cs`）：

```
public class MyCustomException : Exception
{
    public MyCustomException(string message)
        : base(message)
    {
    }
    public int ErrorCode { get; set; }
}
public class AnotherCustomException : Exception
{
    public AnotherCustomException(string message, Exception innerException)
        : base(message, innerException)
    {
    }
}
```

方法 `HandleAll` 调用方法 `HandleAndThrowAgain`、`HandleAndThrowWithInnerException`、`HandleAndRethrow` 和 `HandleWithFilter`。抛出的异常会被捕获以将异常消息以及堆栈跟踪写入控制台。为了更好地找到堆栈跟踪中引用的行号，使用了 `#line` 预处理器指令来重新开始行号计数。这样，使用委托 m 调用方法位于第 114 行（代码文件 RethrowExceptions/Program.cs）：

```
#line 100
public static void HandleAll()
{
    var methods = new Action[]
    {
        HandleAndThrowAgain,
        HandleAndThrowWithInnerException,
        HandleAndRethrow,
        HandleWithFilter
    };

    foreach (var m in methods)
    {
        try
        {
            m();  // line 114
        }
        catch (Exception ex)
        {
            WriteLine(ex.Message);
            WriteLine(ex.StackTrace);
            if (ex.InnerException != null)
            {
                WriteLine($"\tInner Exception: {ex.Message}");
                WriteLine(ex.InnerException.StackTrace);
            }
            WriteLine();
        }
    }
}
```

方法 ThrowAnException 是抛出第一个异常的方法。此异常在第 8002 行抛出。在开发过程中，了解此异常抛出位置很有帮助：

```
#line 8000
public static void ThrowAnException(string message)
{
    throw new MyCustomException(message);  // line 8002
}
```

## Naïve Use to Rethrow the Exception

方法 HandleAndThrowAgain 除了将异常记录到控制台并使用 throw ex 再次抛出它之外什么也不做：

```
#line 4000
public static void HandleAndThrowAgain()
{
    try
    {
        ThrowAnException("test 1");
    }
    catch (Exception ex)
    {
        WriteLine($"Log exception {ex.Message} and throw again");
        throw ex;  // you shouldn't do that - line 4009
    }
}
```

运行应用程序后，显示堆栈跟踪的简化输出（不包含命名空间和代码文件的完整路径）如下所示：

```
Log exception test 1 and throw again
test 1
at Program.HandleAndThrowAgain() in Program.cs:line 4009
at Program.HandleAll() in Program.cs:line 114
```

堆栈跟踪显示了 HandleAll 方法中对 m 方法的调用，而该方法又调用了 HandleAndThrowAgain 方法。异常最初抛出位置的信息在最终 catch 的调用堆栈中完全丢失。这使得很难找到错误的原始原因。通常，不应该只是使用 throw 传递异常对象来抛出相同的异常。

## Changing the Exception

一个有用的场景是更改异常类型并向错误添加信息。这在方法 HandleAndThrowWithInnerException 中完成。记录错误后，会抛出类型为 AnotherCustomException 的新异常，并将 ex 作为内部异常传递：

```
#line 3000
public static void HandleAndThrowWithInnerException()
{
    try
    {
        ThrowAnException("test 2"); // line 3004
    }
    catch (Exception ex)
    {
        WriteLine($"Log exception {ex.Message} and throw again");
        throw new AnotherCustomException("throw with inner exception", ex); // 3009
    }
}
```

检查外部异常的堆栈跟踪，你会看到与之前类似的行号 3009 和 114。然而，内部异常给出了错误的原始原因。它给出了调用出错方法的行（3004）以及原始（内部）异常被抛出的行（8002）：

```
Log exception test 2 and throw again
throw with inner exception
at Program.HandleAndThrowWithInnerException() in Program.cs:line 3009
at Program.HandleAll() in Program.cs:line 114
Inner Exception: throw with inner exception
at Program.ThrowAnException(String message) in Program.cs:line 8002
at Program.HandleAndThrowWithInnerException() in Program.cs:line 3004
```

这样不会丢失任何信息。

> **NOTE** 当尝试找出错误的<|message|>原因时，请查看是否存在内部异常。这通常能提供有用的信息。

> **NOTE** 在捕获异常时，重新抛出时更改异常是良好的做法。例如，捕获 SqlException 可能导致抛出业务相关的异常，例如 InvalidIsbnException。

## Rethrowing the Exception

如果异常类型不应更改，则可以使用 throw 语句重新抛出相同的异常。使用不传递异常对象的 throw 会抛出 catch 块的当前异常并保留异常信息：

```
#line 2000
public static void HandleAndRethrow()
{
    try
    {
        ThrowAnException("test 3");
    }
    catch (Exception ex)
    {
        WriteLine($"Log exception {ex.Message} and rethrow");
        throw;  // line 2009
    }
}
```

这样，堆栈信息不会丢失。异常最初在第 8002 行抛出，并在第 2009 行重新抛出。第 114 行包含调用 HandleAndRethrow 的委托 m：

```
Log exception test 3 and rethrow
test 3
    at Program.ThrowAnException(String message) in Program.cs:line 8002
    at Program.HandleAndRethrow() in Program.cs:line 2009
    at Program.HandleAll() in Program.cs:line 114
```

## Using Filters to Add Functionality

当使用 throw 语句重新抛出异常时，调用堆栈包含 throw 的地址。当你使用异常过滤器时，可以完全不改变调用堆栈。现在添加 `when` 关键字以传递过滤器方法。此过滤器方法名为 `Filter`，它记录消息并始终返回 false。因此 catch 块永远不会被调用：

```
#line 1000
public static void HandleWithFilter()
{
    try
    {
        ThrowAnException("test 4");  // line 1004
    }
    catch (Exception ex) when (Filter(ex))
    {
        WriteLine("block never invoked");
    }
}

#line 1500
public static bool Filter(Exception ex)
{
    WriteLine($"just log {ex.Message}");
    return false;
}
```

现在当你查看堆栈跟踪时，异常源自 HandleAll 方法中的第 114 行，该方法又调用 HandleWithFilter，第 1004 行包含对 ThrowAnException 的调用，而第 8002 行包含异常被抛出的行：

```
just log test 4
test 4
    at Program.ThrowAnException(String message) in Program.cs:line 8002
    at Program.HandleWithFilter() in Program.cs:line 1004
    at RethrowExceptions.Program.HandleAll() in Program.cs:line 114
```

> **NOTE** 异常过滤器的主要用途是根据异常的值过滤异常。异常过滤器也可以用于其他效果，例如在不更改调用堆栈的情况下写入日志信息。然而，异常过滤器应快速运行，因此你应该只做简单的检查。

## What Happens If an Exception Isn’t Handled?

有时可能会抛出异常，但你的代码中没有 catch 块能够处理那种类型的异常。SimpleExceptions 示例可以说明这一点。假设，例如，你省略了 FormatException 和捕获所有异常的 catch 块，只提供了捕获 IndexOutOfRangeException 的块。在这种情况下，如果抛出 FormatException 会发生什么？

答案是 .NET 运行时会捕获它。本节后面你将学习如何嵌套 try 块；事实上，示例中背后已经有一个嵌套的 try 块。.NET 运行时有效地将整个程序放在另一个巨大的 try 块内——它对每个 .NET 程序都这样做。此 try 块有一个可以捕获任何类型异常的 catch 处理程序。如果发生你的代码未处理的异常，执行流程 simply 直接退出你的程序并被 .NET 中的此 catch 块捕获

