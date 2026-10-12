
```csharp
public sealed class TextNumberParser
{
    public static int Parse(string textDigit)
    {
        string[] digitTexts =
            { "zero", "one", "two", "three", "four",
              "five", "six", "seven", "eight", "nine" };

        int result = Array.IndexOf(
            digitTexts,
            // Leveraging C# 2.0's null coalesce operator
            textDigit ??
            // Leveraging C# 7.0's throw expression
            throw new ArgumentNullException(nameof(textDigit))
            ).ToLower());
        if (result < 0)
        {
            // Leveraging C# 6.0's nameof operator
            throw new ArgumentException(
                "The argument did not represent a digit",
                nameof(textDigit));
        }

        return result;
    }
}
```

在对 `Array.IndexOf()` 的调用中，当 `textDigit` 参数为 null 时，我们利用了 C# 7.0 的 throw 表达式。在 C# 7.0 之前，不允许使用 throw 表达式；只允许使用 throw 语句。因此，需要两条独立的语句：一条用于检查 null，另一条用于抛出异常。例如，你不能将 throw 嵌入到使用空值合并运算符的同一语句中。

抛出 `System.Exception` 不如抛出 `ArgumentException` 合适，因为该类型本身指示了出了什么问题，并且包含用于识别哪个参数出错的特殊参数。

两个类似的异常是 `ArgumentNullException` 和 `NullReferenceException`。`ArgumentNullException` 应针对不当传递的 null 参数进行抛出。这是无效参数异常的一个特例，在更一般的情况下（当它不是 null 时），通常会作为 `ArgumentException` 或 `ArgumentOutOfRangeException` 抛出。`NullReferenceException` 通常是底层运行时仅在尝试取消引用 null 值时抛出的异常——也就是说，尝试访问值为 null 的对象成员。为了避免触发 `NullReferenceException` 的抛出，程序员应在访问参数之前检查其是否为 null，然后抛出 `ArgumentNullException`，后者可以提供更多的上下文信息，例如参数名称。如果即使参数为 null 也有无害的方式继续执行，请务必使用 C# 6.0 的空值传播运算符，以避免运行时抛出 `NullReferenceException`。

参数异常类型（包括 `ArgumentNullException`、`ArgumentException` 和 `ArgumentOutOfRangeException`）的一个重要特征是，每种类型都有一个构造函数参数，允许以字符串形式识别参数名称。在 C# 6.0 之前，这意味着需要硬编码一个魔法字符串（例如 `"textDigit"`）来识别参数名称。这种方法的问题在于，如果参数名称发生变化，开发人员必须记得更新魔法字符串。幸运的是，C# 6.0 及更高版本提供了 `nameof` 运算符，它接受参数名称标识符并在编译时生成参数名称（参见列表 11.1 中的 `nameof(textDigit)`）。这种方法的优势在于，现在 IDE 可以使用重构工具（如自动重命名）在所有地方更改标识符，包括将其用作 `nameof` 运算符参数的情况。此外，如果参数名称更改（未使用重构工具），如果传递给 `nameof` 运算符的标识符不再存在，编译器将生成错误。今后，对于 C# 6.0（及更高版本），一般准则是始终对参数类型异常的参数名称使用 `nameof` 运算符。第 18 章将对 `nameof` 运算符提供完整的解释。在此之前，只需理解 `nameof` 简单地返回已识别参数的名称即可。

其他一些异常仅旨在供运行时使用，并派生自（有时是间接派生自）`System.SystemException`。它们包括 `System.StackOverflowException`、`System.OutOfMemoryException`、`System.Runtime.InteropServices.COMException`、`System.ExecutionEngineException` 和 `System.Runtime.InteropServices.SEHException`。不要抛出这些类型的异常。同样，应避免抛出 `System.Exception` 或 `System.ApplicationException`，因为这些异常过于通用，以至于对问题的原因或解决方案提供的指示很少。相反，请抛出最适合该场景的最派生异常。显然，开发人员应避免创建可能导致系统故障的 API。然而，如果执行的代码达到某种状态，使得继续执行是不安全的或不可恢复的，则应调用 `System.Environment.FailFast()`。这将在向 Windows 应用程序事件日志写入消息后立即终止进程，并且如果用户选择，还将该消息作为 Windows 错误报告的一部分包含在内。

## 准则

- **应该** 在成员接收到不良参数时抛出 `ArgumentException` 或其子类型之一。如果适用，优先使用最派生的异常类型（例如 `ArgumentNullException`）。

- **应该** 在抛出 `ArgumentException` 或其子类之一时设置 `ParamName` 属性。

- **应该** 抛出最有意义（最派生）的最具体异常。

- **不应该** 抛出 `NullReferenceException`。相反，当值意外为 null 时，请抛出 `ArgumentNullException`。

- **不应该** 抛出 `System.SystemException` 或派生自它的异常类型。

- **不应该** 抛出 `System.Exception` 或 `System.ApplicationException`。

- **可以考虑** 如果程序遇到进一步执行不安全的场景，通过调用 `System.Environment.FailFast()` 来终止进程。

- **应该** 对接受此类参数的参数异常类型传入的 `paramName` 参数使用 `nameof`。此类异常的示例包括 `ArgumentException`、`ArgumentOutOfRangeException` 和 `ArgumentNullException`。

## 捕获异常

抛出特定的异常类型使得捕获者能够使用异常类型本身来识别问题。换句话说，没有必要捕获异常并使用 switch 语句对异常消息进行操作来确定在异常情况下应采取哪些操作。相反，C# 允许多个 catch 块，每个针对特定的异常类型，如列表 11.2 所示。

### 列表 11.2：捕获不同的异常类型

```csharp
using System;

public sealed class Program
{
    public static void Main(string[] args)
    {
        try
        {
            // ...
            throw new InvalidOperationException(
                "Arbitrary exception");
            // ...
        }
        catch (Win32Exception exception)
            when (exception.NativeErrorCode == 42)
        {
            // Handle Win32Exception where
            // ErrorCode is 42
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
            bool exceptionHandled = false;
            // Handle InvalidOperationException
            // ...
            if (exceptionHandled)
            {
                throw;
            }
        }
    }
}
```

```csharp
catch (Exception exception)
{
      // 处理异常
}
finally
{
      // 在此处处理任何清理代码，因为它无论如何都会执行
      // 不管是否发生异常
}
```

清单 11.2 包含五个 catch 块，每个块处理不同类型的异常。当发生异常时，执行流程将跳转到异常类型与当前异常最匹配的 catch 块。匹配程度由继承链决定。例如，虽然抛出的异常类型是 `System.Exception`，但由于 `System.InvalidOperationException` 最终继承自 `System.Exception`，因此通过这种“是一种”的继承关系产生了联系。由于异常类型 `InvalidOperationException` 与抛出的异常匹配度最高，因此 `catch(InvalidOperationException...)` 块将捕获该异常，而不是 `catch(Exception...)` 块。

从 C# 6.0 开始，catch 块提供了额外的条件表达式。不再仅限于基于异常类型匹配来决定是否执行 catch 块，C# 6.0 及更高版本支持使用条件子句。`when` 子句允许你提供一个布尔表达式；只有当条件为真时，catch 块才会处理该异常。在清单 11.2 中，这是一个相等性比较运算符。尽管如此，例如，你可以调用方法来验证某个条件。

当然，你也可以简单地将条件检查作为一个 if 块放在 catch 主体内部。然而，这样做会导致 catch 块在检查条件之前成为该异常的处理程序。很难编写代码，使得在条件不满足的情况下让不同的 catch 块来处理异常。然而，通过异常条件，现在可以在无需捕获并重新抛出异常的情况下检查程序状态（包括异常）。

谨慎使用条件子句；如果条件表达式本身抛出异常，那么该新异常将被忽略，并且该条件被视为假。因此，应避免在异常条件表达式中抛出异常。

Catch 块必须按顺序排列，从最具体到最通用，以避免编译时错误。例如，将 `catch(Exception...)` 块移动到任何其他异常之前会导致编译错误，因为所有先前的异常在其继承链的某个点上都继承自 `System.Exception`。

如 `catch (SystemException){ }` 块所示，catch 块不需要命中的参数。事实上，甚至没有类型参数的最终 catch 也是允许的，如下一节所示。

## 重新抛出已有异常

在 `InvalidOperationException` 的 catch 块中，出现了一个没有指定要抛出哪个异常的 `throw` 语句（`throw` 是独立存在的），即使在 catch 块的作用域中出现了异常实例（`exception`）可以重新抛出。抛出特定异常会更新所有堆栈信息以匹配新的抛出位置。结果是，指示异常最初发生位置的调用站点的所有堆栈信息都会丢失，这使得诊断问题变得更加困难。因此，C# 支持在 catch 块内使用没有显式异常引用的 `throw` 语句或表达式（C# 7.0 或更高版本）。这样，代码可以检查异常以确定是否可能完全处理它，如果不能，则重新抛出异常（即使没有明确指定），就好像它从未被捕获过，并且不替换任何堆栈信息。

## 高级主题

### 重新抛出已有异常而不替换堆栈信息

在 C# 5.0 中，增加了一种机制，允许在不丢失原始异常中的堆栈跟踪信息的情况下，抛出之前已抛出的异常。这允许你重新抛出异常，例如，即使在 catch 块外部，因此无需使用 `throw;`。虽然很少需要这样做，但在某些情况下，异常会被包装或保存，直到程序执行移动到 catch 块之外。例如，多线程代码可能会用 `AggregateException` 包装异常。Microsoft .NET Framework 4.5 提供了一个专门的 `System.Runtime.ExceptionServices.ExceptionDispatchInfo` 类，通过其静态 `Catch()` 和实例 `Throw()` 方法来处理这种场景。（不幸的是，截至 2.0 版本，该类在 .NET Core 中不可用。）清单 11.3 展示了如何重新抛出异常，而无需重置堆栈跟踪信息或使用空的 `throw` 语句。

### 清单 11.3：使用 ExceptionDispatchInfo 重新抛出异常

```csharp
using System
using System.Runtime.ExceptionServices;
using System.Threading.Tasks;
Task task = WriteWebRequestSizeAsync(url);
try
{
    while (!task.Wait(100))
    {
        Console.Write(".");
    }
}
catch (AggregateException exception)
{
    exception = exception.Flatten();
    ExceptionDispatchInfo.Capture(
        exception.InnerException).Throw();
}
```

使用 `ExceptionDispatchInfo.Throw()` 方法时，编译器不会像对待普通 `throw` 语句那样将其视为返回语句。例如，如果方法签名返回一个值，但代码路径在使用 `ExceptionDispatchInfo.Throw()` 时没有返回值，编译器将发出错误，指示没有返回值。因此，在某些情况下，开发人员可能被迫在 `ExceptionDispatchInfo.Throw()` 之后跟一个 `return` 语句，即使这样的语句在运行时永远不会执行——取而代之的是会抛出异常。

## 语言对比：Java——异常说明符

C# 没有相当于 Java 异常说明符的功能。利用异常说明符，Java 编译器能够验证函数（或函数的调用层级）中抛出的所有可能异常要么被捕获，要么被声明为可能重新抛出。C# 团队考虑过这个选项，并认为其所带来的维护负担不值得预期的好处。因此，没有必要在整个特定调用栈中维护所有可能异常的列表，但也无法轻松地确定可能的异常。（事实证明，这在 Java 中也是不可能的。调用虚方法或使用延迟绑定，例如反射，使得在编译时完全解析方法可能抛出的异常变得不可能。）

## 通用 Catch 块

C# 要求代码抛出的任何对象都必须继承自 `System.Exception`。然而，这一要求并非所有语言通用。例如，C 和 C++ 允许抛出任何对象类型，包括未从 `System.Exception` 继承的托管异常。从 C# 2.0 开始，无论是否继承自 `System.Exception`，所有异常都将作为 `System.Exception` 的派生类传播到 C# 程序集中。结果是，`System.Exception` 的 catch 块将捕获未被先前块捕获的所有异常。

C# 还支持**通用 catch 块**（`catch{ }`），其行为与 `catch(System.Exception exception)` 块完全相同，只是没有类型或变量名。此外，通用 catch 块必须出现在 catch 块列表的最后。由于通用 catch 块与 `catch(System.Exception exception)` 块相同，且通用 catch 块必须最后出现，如果两者存在于同一个 try/catch 语句中，编译器会发出警告，因为通用 catch 块永远不会被调用（有关通用 catch 块的更多信息，请参见标题为“C# 1.0 中的通用 Catch 块”的高级主题）。

## 高级主题

### C# 1.0 中的通用 Catch 块

在 C# 1.0 中，如果从方法调用中抛出了一个非 `System.Exception` 派生的异常（该方法调用所在的程序集并非用 C# 编写），该异常

不会被 `catch(System.Exception)` 块捕获。如果另一种语言抛出字符串，例如，异常可能未被处理。为避免这种情况，C# 包含一个不取参数的 catch 块。这种 catch 块的术语是 *通用 catch 块*，且清单 11.4 中包含了这样一个块。

## 清单 11.4：捕获任何异常
