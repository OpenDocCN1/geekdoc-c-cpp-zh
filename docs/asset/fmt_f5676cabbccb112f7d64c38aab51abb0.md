
# 异常处理与重新抛出

## 基础异常处理示例

```csharp
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
```

方法 `ThrowAnException` 是抛出第一个异常的方法。此异常在第 8002 行抛出。在开发过程中，了解此异常抛出位置很有帮助：

```csharp
#line 8000
public static void ThrowAnException(string message)
{
    throw new MyCustomException(message);  // line 8002
}
```

### Naïve Use to Rethrow the Exception

方法 `HandleAndThrowAgain` 除了将异常记录到控制台并使用 `throw ex` 再次抛出它之外什么也不做：

```csharp
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

堆栈跟踪显示了 `HandleAll` 方法中对 `m` 方法的调用，而该方法又调用了 `HandleAndThrowAgain` 方法。异常最初抛出位置的信息在最终 catch 的调用堆栈中完全丢失。这使得很难找到错误的原始原因。通常，不应该只是使用 `throw` 传递异常对象来抛出相同的异常。

### Changing the Exception

一个有用的场景是更改异常类型并向错误添加信息。这在方法 `HandleAndThrowWithInnerException` 中完成。记录错误后，会抛出类型为 `AnotherCustomException` 的新异常，并将 `ex` 作为内部异常传递：

```csharp
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

> **NOTE** 当尝试找出错误的原因时，请查看是否存在内部异常。这通常能提供有用的信息。

> **NOTE** 在捕获异常时，重新抛出时更改异常是良好的做法。例如，捕获 `SqlException` 可能导致抛出业务相关的异常，例如 `InvalidIsbnException`。

### Rethrowing the Exception

如果异常类型不应更改，则可以使用 `throw` 语句重新抛出相同的异常。使用不传递异常对象的 `throw` 会抛出 catch 块的当前异常并保留异常信息：

```csharp
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

这样，堆栈信息不会丢失。异常最初在第 8002 行抛出，并在第 2009 行重新抛出。第 114 行包含调用 `HandleAndRethrow` 的委托 `m`：

```
Log exception test 3 and rethrow
test 3
    at Program.ThrowAnException(String message) in Program.cs:line 8002
    at Program.HandleAndRethrow() in Program.cs:line 2009
    at Program.HandleAll() in Program.cs:line 114
```

### Using Filters to Add Functionality

当使用 `throw` 语句重新抛出异常时，调用堆栈包含 `throw` 的地址。当你使用异常过滤器时，可以完全不改变调用堆栈。现在添加 `when` 关键字以传递过滤器方法。此过滤器方法名为 `Filter`，它记录消息并始终返回 `false`。因此 catch 块永远不会被调用：

```csharp
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

现在当你查看堆栈跟踪时，异常源自 `HandleAll` 方法中的第 114 行，该方法又调用 `HandleWithFilter`，第 1004 行包含对 `ThrowAnException` 的调用，而第 8002 行包含异常被抛出的行：

```
just log test 4
test 4
    at Program.ThrowAnException(String message) in Program.cs:line 8002
    at Program.HandleWithFilter() in Program.cs:line 1004
    at RethrowExceptions.Program.HandleAll() in Program.cs:line 114
```

> **NOTE** 异常过滤器的主要用途是根据异常的值过滤异常。异常过滤器也可以用于其他效果，例如在不更改调用堆栈的情况下写入日志信息。然而，异常过滤器应快速运行，因此你应该只做简单的检查。

### What Happens If an Exception Isn’t Handled?

有时可能会抛出异常，但你的代码中没有 catch 块能够处理那种类型的异常。`SimpleExceptions` 示例可以说明这一点。假设，例如，你省略了 `FormatException` 和捕获所有异常的 catch 块，只提供了捕获 `IndexOutOfRangeException` 的块。在这种情况下，如果抛出 `FormatException` 会发生什么？

答案是 .NET 运行时会捕获它。本节后面你将学习如何嵌套 `try` 块；事实上，示例中背后已经有一个嵌套的 `try` 块。.NET 运行时有效地将整个程序放在另一个巨大的 `try` 块内——它对每个 .NET 程序都这样做。此 `try` 块有一个可以捕获任何类型异常的 catch 处理程序。如果发生你的代码未处理的异常，执行流程 simply 直接退出你的程序并被 .NET 中的此 catch 块捕获。

运行时。但是，这样做的结果很可能并非你所愿，因为你的代码执行会立即被终止。用户会看到一个对话框，提示你的代码未处理该异常，并显示 .NET 运行时能够检索到的有关该异常的任何详细信息。至少异常已经被捕获了！

一般而言，如果你在编写可执行程序，请尽量合理地捕获尽可能多的异常，并以合理的方式处理它们。如果你在编写类库，通常最好是捕获那些能以有用方式处理的异常，或者能够在上下文中添加附加信息并按上一节所示抛出其他异常类型。要假定调用代码会处理它遇到的任何错误。

## 用户定义的异常类

在上一节中，你已经创建了一个用户定义的异常。现在，我们来看一个更大的示例来演示异常。这个示例名为 `SolicitColdCall`，包含两个嵌套的 `try` 块，演示了定义自己的自定义异常类以及从 `try` 块内部抛出另一个异常的实践。

这个示例假设一家销售公司想扩大客户群。公司的销售团队将给一份名单上的人打电话，邀请他们成为客户，这种做法在销售术语中称为*冷呼叫*。为此，你有一个文本文件，其中包含要被冷呼叫的人员姓名。该文件应采用明确定义的格式：第一行包含文件中的人数，随后每一行包含下一个人的姓名。换句话说，一个格式正确的姓名文件可能如下所示：

```
4
George Washington
Benedict Arnold
John Adams
Thomas Jefferson
```

这个版本的冷呼叫设计为在屏幕上显示人名（也许供销售人员阅读）。因此，文件中只包含姓名，而不包含电话号码。

在这个示例中，你的程序要求用户输入文件名，然后简单地将它读入并显示人名。这听起来是一项简单的任务，但即便如此，仍可能有几处出错，需要你放弃整个过程：

- 用户可能输入了一个不存在的文件名。这会被捕获为 `FileNotFoundException`。
- 文件格式可能不正确。有两种可能

```csharp
public class Program
{
    public static void Main()
    {
        Write("Please type in the name of the file " +
            "containing the names of the people to be cold called >");
        string fileName = ReadLine();
        ColdCallFileReaderLoop(fileName);
        WriteLine();
        ReadLine();
    }

    public static void ColdCallFileReaderLoop(string fileName)
    {
        var peopleToRing = new ColdCallFileReader();
        try
        {
            peopleToRing.Open(fileName);
            for (int i = 0; i < peopleToRing.NPeopleToRing; i++)
            {
                peopleToRing.ProcessNextPerson();
            }
            WriteLine("All callers processed correctly");
        }
        catch (FileNotFoundException)
        {
            WriteLine($"The file {fileName} does not exist");
        }
        catch (ColdCallFileFormatException ex)
        {
            WriteLine($"The file {fileName} appears to have been corrupted");
            WriteLine($"Details of problem are: {ex.Message}");
            if (ex.InnerException != null)
            {
                WriteLine($"Inner exception was: {ex.InnerException.Message}");
            }
        }
        catch (Exception ex)
        {
            WriteLine($"Exception occurred:\n{ex.Message}");
        }
        finally
        {
            peopleToRing.Dispose();
        }
    }
}
```
