

从 C# 2.0 开始的行为与之前的 C# 行为略有不同。在 C# 2.0 中，如果一种语言允许抛出非 System.Exception 的异常，则被抛出的异常对象将被包装在派生自 System.Exception 的 System.Runtime.CompilerServices.RuntimeWrappedException 中。因此，无论是否派生自 System.Exception，所有异常在传播到 C# 程序集时都将表现为派生自 System.Exception。

其结果是，System.Exception 捕获块将捕获所有未被前面块捕获的异常，而在 System.Exception 捕获块之后出现的通用捕获块将永远不会被调用。因此，在 C# 2.0 或更高版本中，在 System.Exception 捕获块之后跟随通用捕获块将导致编译器警告，指出通用捕获块将永远不会执行。

## Guidelines

- AVOID 使用通用捕获块，改用对 System.Exception 的捕获。
- AVOID 捕获那些不知道如何适当处理的异常。让异常未被处理要好于错误地处理它。
- AVOID 在重新抛出异常之前捕获并记录异常。相反，应允许异常在能够适当处理之前继续传播。

## Reporting Errors Using a throw Statement

C# 允许开发人员从其代码中抛出异常，如 Listing 4.24 和 Output 4.15 所示。

### LISTING 4.24: Throwing an Exception

```
using System;
public class ThrowingExceptions
{
    public static void Main()
    {
        try
        {
            Console.WriteLine("Begin executing");
            Console.WriteLine("Throw exception");
            throw new Exception("Arbitrary exception");
            Console.WriteLine("End executing");
        }
        catch(FormatException exception)
        {
            Console.WriteLine(
            "A FormatException was thrown");
        }
        catch(Exception exception)
        {
            Console.WriteLine(
            $"Unexpected error: { exception.Message }");
        }
        catch
        {
            Console.WriteLine("Unexpected error!");
        }
        Console.WriteLine(
        "Shutting down...");
    }
}
```

### OUTPUT 4.15

```
Begin executing
Throw exception...
Unexpected error:  Arbitrary exception
Shutting down...
```

正如 Listing 4.24 中的箭头所示，抛出异常会导致执行从抛出异常的位置跳转到堆栈中与所抛异常类型兼容的第一个 catch 块内。⁵ 在本例中，第二个 catch 块处理了该异常并输出错误消息。在 Listing 4.24 中没有 finally 块，因此执行会落到 try/catch 块之后的 System.Console.WriteLine() 语句。

要抛出异常，需要有一个异常实例。Listing 4.24 使用关键字 new 后跟异常的类型来创建实例。大多数异常类型允许在抛出异常时生成消息，以便在异常发生时可以检索该消息。

5. 技术上，它也可能被兼容的 catch 过滤器捕获。

有时 catch 块会捕获异常但无法适当或完全处理它。在这种情况下，catch 块可以使用 throw 语句重新抛出异常而不指定任何异常，如 Listing 4.25 所示。

### LISTING 4.25: Rethrowing an Exception

```
catch(Exception exception)
{
    Console.WriteLine(
        $@"Rethrowing unexpected error: { exception.Message }");
    throw;
}
```

在 Listing 4.25 中，throw 语句是“空的”，而不是指定要抛出由 exception 变量引用的异常。这说明了一个细微差别：throw; 保留异常中的“调用堆栈”信息，而 throw exception; 则用当前调用堆栈信息替换该信息。出于调试目的，通常最好知道原始调用堆栈。

## Guidelines

- DO 优先使用空的 throw 在捕获并重新抛出异常时以保留调用堆栈。
- DO 通过抛出异常而不是返回错误代码来报告执行失败。
- DO NOT 拥有返回异常作为返回值或 out 参数的公共成员。抛出异常以指示错误；不要将它们用作返回值来指示错误。

## Avoid Using Exception Handling to Deal with Expected Situations

开发人员应努力避免为预期条件或正常控制流而抛出异常。例如，开发人员不应期望用户在指定年龄时输入有效文本。⁶ 因此，

> 6. 通常，开发人员应期望用户执行意外操作，因此他们应以防御性方式编码以处理“愚蠢用户技巧”。

不要依赖异常来验证用户输入的数据，开发人员应提供在尝试转换之前检查数据的方法。 （更好的是，他们应首先防止用户输入无效数据。）异常专门设计用于跟踪异常、意外和可能致命的情况。将它们用于预期情况等非预期目的会使你的代码难以阅读、理解和维护。

此外，与大多数语言一样，C# 在抛出异常时会产生轻微的性能损失——以微秒计，而大多数操作以纳秒计。这种延迟在人类时间尺度上通常不易察觉——除非异常未被处理。例如，当 Listing 4.20 执行且用户输入无效年龄时，异常未被处理，并且在运行时搜索环境以查看是否有要加载的调试器时会产生明显的延迟。幸运的是，程序关闭时的缓慢性能通常不是需要担心的问题。

**Guidelines**

DO NOT 使用异常来处理正常、预期的条件；将它们用于异常、意外的条件。

## ADVANCED TOPIC

## Numeric Conversion with TryParse()

Parse() 方法的一个问题是，判断转换是否成功唯一的方法是尝试转换然后在失败时捕获异常。由于抛出异常是相对昂贵的操作，因此最好在不使用异常处理的情况下尝试转换。在 C# 的第一个版本中，唯一启用此行为的数据类型是 double 类型的 double.TryParse() 方法。然而，CLI 在 2.0 版中将此方法添加到所有数值基元类型中。它需要使用 out 关键字，因为 TryParse() 函数的返回值为 bool 而不是转换后的值。Listing 4.26 是一个代码片段，演示了使用 int.TryParse() 进行转换。

### LISTING 4.26: Conversion Using int.TryParse()

```
if (int.TryParse(ageText, out age))
{
    Console.WriteLine(
        $"Hi { firstName }! "
        + $"You are { age*12 } months old.");
}
else
{
    Console.WriteLine(
        $"The age entered, { ageText }, is not valid.");
}
```

随着 .NET Framework 4，TryParse() 方法也被添加到枚举类型中。

有了 TryParse() 方法，就不再有必要仅为处理字符串到数值的转换而包含 try/catch 块。

## SUMMARY

本章讨论了声明和调用方法的细节，包括使用 out 和 ref 关键字传递变量而不是其值。除了方法声明之外，本章还介绍了异常处理。

方法是编写可读代码的关键基础结构。不要编写包含大量语句的大方法，而应使用方法在你的代码中创建“段落”，其长度大约为 10 条语句或更少。将大型函数分解为更小块的过程是你可以重构代码以使其更易读和可维护的方式之一。

下一章将考虑类构造并描述它如何将方法（行为）和字段（数据）封装到一个单元中。

