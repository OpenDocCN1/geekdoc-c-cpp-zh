
```csharp
public TemporaryFileStream FileStream =>
    InternalFileStream.Value;

private Lazy<TemporaryFileStream> InternalFileStream { get; }
    = new Lazy<TemporaryFileStream>(() => new TemporaryFileStream());
}
```

从 C# 4.0 和 .NET Framework 4.0 开始添加到 CLR 的类。

## 总结

本章对与构建健壮类库相关的许多主题进行了快速回顾。所有主题也适用于内部开发。

命名空间和垃圾回收。这两个主题也属于可编程范畴，此外包括重写对象的虚成员、运算符重载以及用于文档的 XML 注释。

异常处理很大程度上依赖于继承，通过定义异常层次结构并强制执行自定义异常以符合该层次结构来实现的。此外，C# 编译器使用继承来验证 `catch` 块的顺序。在第 11 章中，你将看到为什么继承是异常处理的核心部分。

# 11 异常处理

第 5 章讨论了使用 `try/catch/finally` 块进行标准异常处理。在该章中，`catch` 块总是捕获类型为 `System.Exception`。本章定义了异常处理的一些额外细节——特别是关于附加异常类型的细节、自定义异常以及处理每种类型的多个 `catch` 块。本章还详细介绍了异常，因为它们对继承的依赖。

- 7. 重新抛出包装过的异常
- 6. 定义自定义异常
- 5. 异常处理指南
- 1. 多种异常类型
- 2. 捕获异常
- 3. 重新抛出现有异常
- 4. 普通 catch 块

# 多种异常类型

列表 11.1 抛出了一个 `System.ArgumentException`，而不是第 5 章演示的 `System.Exception` 类型。C# 允许抛出任何（可能间接的）继承自 `System.Exception` 的类型。要抛出异常，只需在异常实例前加上 `throw` 关键字即可。使用的异常类型显然是最能描述导致异常情况的类型。

# 第 11 章：异常处理

导致异常的错误情况。例如，考虑列表 11.1 中的 `TextNumberParser.Parse()` 方法。

# 列表 11.1：抛出异常

```csharp
public sealed class TextNumberParser
{
    public static int Parse(string textDigit)
    {
        string[] digitTexts =
            "zero", "one", "two", "three", "four",
            "five", "six", "seven", "eight", "nine";
        int result = Array.IndexOf(
            digitTexts,
            // 利用 C# 2.0 的空合并运算符
            textDigit?
            // 利用 C# 7.0 的 throw 表达式
            throw new ArgumentNullException(nameof(textDigit))
        ).ToLower();
        if (result < 0)
        {
            // 利用 C# 6.0 的 nameof 运算符
            throw new ArgumentException(
                "The argument did not represent a digit",
                nameof(textDigit));
            return result;
        }
    }
}
```

在调用 `Array.IndexOf()` 时，当 `textDigit` 参数为 null，我们利用了 `throw` 表达式¹。

与其抛出 `System.Exception`，不如抛出 `ArgumentException` 更合适，因为该类型指示了发生了什么，并包含了用于识别哪个参数出错的特殊参数。

两个类似的异常是 `ArgumentException` 和 `NullReferenceException`。对于不当传递的 null 参数，应该抛出 `ArgumentNullException`。这是无效参数参数异常异常的一种特例。

- 1. 从 C# 7.0 开始。

该异常在更通用的情况下（当它不为 null 时）会作为 `ArgumentException` 或 `ArgumentOutOfRangeException` 抛出。

`NullReferenceException` 通常是底层运行时仅在尝试解引用 null 值时才会抛出的异常——也就是说，尝试调用一个值为 null 的对象的成员。程序员不应该触发抛出 `NullReferenceException`，而应该在访问参数之前检查参数是否为 null，然后抛出 `ArgumentNullException`，这可以提供更多的上下文信息，例如参数名称。如果即使参数为 null 也有无害的方法继续执行，请务必在解引用时使用空条件运算符²，以避免运行时抛出 `NullReferenceException`。

参数异常类型（包括 `ArgumentException`、`ArgumentNullException` 和 `ArgumentOutOfException`）的一个重要特征是，每个类型都有一个构造函数，允许以字符串形式识别参数名称³。通用指南是对对于参数异常的参数名始终使用 `nameof` 运算符。第 18 章提供了对 `nameof` 运算符的完整解释。在此之前，只需理解 `typeof` 返回所识别的参数名称即可。

其他几种异常仅仅供运行时使用，并（有时是间接的）继承自 `System.SystemException`。它们包括 `System.StackOverflowException`、`System.OutOfMemoryException`、`System.Runtime.InteropServices.ComException`、`System.Runtime.ExecutionEngineException` 和 `System.Runtime.InteropServices.SEHException`。不要抛出这些类型的异常。同样地，你应该避免抛出 `System.Exception` 或 `System.ApplicationException`，因为这些异常是通用的，对于问题的原因或解决方案提供的指示很少。相反，请抛出符合场景的最派生异常。显然，开发者应该避免创建可能导致系统失败的 API。然而，如果执行代码到达某种状态

- 1. 从 C# 6.0 开始。
- 2. 在 C# 6.0 之前，这意味着硬编码一个魔法字符串来识别参数名称。

# 第 11 章：异常处理

如果继续执行是不安全或不可恢复的，它应该调用 `System.Environment.FailFast()`。这将在向标准错误写入消息后立即终止进程，在 Microsoft Windows 上，还会写入 Windows 应用程序事件日志。

## 指南

| 操作 | 描述 |
| :--- | :--- |
| 抛出 | 如果向成员传递了错误的参数，请抛出 `ArgumentException` 或其子类型。如果适用，优先使用最派生的异常类型（例如 `ArgumentNullException`）。 |
| 不要抛出 | 不要抛出 `System.Exception` 或继承自非的异常类型。 |
| 不要抛出 | 不要抛出 `System.Exception`、`System.NullReferenceException` 或 `System.ApplicationException`。 |
| 考虑 | 如果程序遇到不安全继续执行的情况，调用 `System.Environment.FailFast()` 终止进程。 |
| 使用 | 对于传入此类异常类型的参数使用 `nameof`。此类异常的示例包括 `ArgumentException`、`ArgumentOutOfRangeException` 和 `ArgumentNullException`。 |

# 捕获异常

抛出特定的异常使捕获者能够异常类型本身来识别问题。换句话说，没有必要捕获异常并对消息使用 `switch` 语句来根据异常情况采取行动。相反，C# 允许使用多个 `catch` 块，每个块针对特定的异常类型，如列表 11.2 所示。

# 列表 11.2：捕获不同异常类型

```csharp
using System;
public sealed class Program
{}
```

# 捕获异常

```csharp
public static void Main(string[] args)
{
    try {
        // ...
        throw new InvalidOperationException(
            "Arbitrary exception");
        // ...
    }
    catch(Win32Exception exception)
        when(exception.NativeErrorCode == 42) {
        // 处理 ErrorCode 为 42 的 Win32Exception
    }
    catch(ArgumentException exception) {
        // 处理 ArgumentException
    }
    catch(InvalidOperationException exception) {
        bool exceptionHandled = false;
        // 处理 InvalidOperationException
        // ...
        if(!exceptionHandled) {
            throw;
        }
    }
    catch(Exception exception) {
        // 处理 Exception
    }
    finally {
        // 在此处处理任何清理代码，无论是否有异常，
        // 该代码都会运行
    }
}
```

列表 11.2 包含了五个 `catch` 块，每个块处理不同类型的异常。当发生异常时，执行将跳转到异常类型最匹配异常的 `catch` 块。匹配的接近程度由继承链决定。例如，即使该异常

抛出的类型为 `System.Exception`。这种“是一个”关系通过继承实现，因为 `System.InvalidOperationException` 最终派自 `System.Exception`。由于异常类型 `InvalidOperationException` 与该异常最匹配，因此 `catch(InvalidOperationException...)` 块会捕获该异常，而不是 `catch(Exception...)` 块。

catch 块还可以使用额外的条件表达式。与其限制 `catch` 块仅根据异常类型匹配，还存在一个条件子句。在列表 11.2 中，这是一个等值运算符。对于更复杂的逻辑，你可以简单地将条件检查放在 `catch` 体内部。然而，这样做会导致 `catch` 块在检查条件之前就成为该异常的处理程序。但是，有了异常条件，现在可以检查程序状态（包括异常），而无需捕获并重新抛出异常。

请谨慎使用条件子句：如果条件表达式本身抛出异常，则该新异常将被忽略，且条件将被视为视为 `false`。由于此原因，你应该避免使用条件表达式。

catch 块必须按照从具体到通用的顺序出现，以避免编译错误。例如，将 `catch(Exception...)` 块移动到任何其他异常之前会导致编译错误，因为之前的所有异常在它们的继承链的某个地方都派自 `System.Exception`。正如 `catch(System) {}` 块所示，`catch` 块不需要命名参数。事实上，允许使用空 `throw`，正如你将在下一节中看到的那样。

1. 从 C# 6.0 开始。

## 重新抛出现有异常

在 `InvalidOperation` catch 块中，出现了一个没有指定要抛出的异常标识的 `throw` 语句（单独使用 `throw`），尽管在 catch 作用域内出现了一个可以重新抛出的异常实例。抛出特定异常将更新栈信息以匹配 `throw` 位置。结果是，指示异常源调用处的栈信息将会丢失，这使得诊断问题变得困难得多。因此，只要发生在 `catch` 块内部，C# 就支持不带显式异常引用的 `throw` 语句或表达式。这样，代码可以检查异常以确定是否可能完全处理它，如果不能，则重新抛出异常（即使没有显式指定），就像它从未被捕获一样，且不会替换任何栈信息。

## 在不替换栈信息的情况下抛出现有异常

有一种机制可以抛出之前抛出的异常，而不丢失原始异常中的堆栈跟踪信息。这允许你重新抛出异常，例如即使从 `catch` 块外部，因此不需要使用 `throw`。虽然这样做相当罕见，但有时会被封装或保存直到程序执行移动到 `catch` 块之外。例如，多线程代码可能会用 `AggregateException` 封装异常。`System.Runtime.ExceptionServices.ExceptionInfo` 类专门设计通过其静态 `Capture()` 方法和实例 `Throw()` 方法来处理这种场景。列表 11.3 展示了在不重置堆栈跟踪信息或使用空 `throw` 语句的情况下重新抛出异常。

5. C# 7.0 或更高版本。
6. 从 C# 5.0 开始。

### 列表 11.3：使用 ExceptionInfo 重新抛出异常

```csharp
using System;
using System.Runtime.ExceptionServices;
using System.Threading.Tasks;
using System.Net;
using System.Linq;
using System.IO;
// ...
Task task = WriteWebRequestAsync(url);
try {
  while (!task.Wait(100)) {
    Console.Write(".");
  }
}
catch (AggregateException exception) {
  exception = exception.Flatten();
  ExceptionInfo.Capture(exception.InnerException ?? exception).Throw();
}
```
