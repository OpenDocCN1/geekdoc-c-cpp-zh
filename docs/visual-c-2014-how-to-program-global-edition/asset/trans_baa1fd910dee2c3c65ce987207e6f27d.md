
[content]

# 异常处理：深入探讨

## 13 目标

## 目标

在本章中，你将：

- 理解什么是异常以及如何处理它们。
- 学习何时使用异常处理。
- 使用 `try` 来界定可能抛出异常的代码。
- 使用 `throw` 指明运行时的问题。
- 使用 `catch` 指定异常处理程序。
- 理解未捕获异常会发生什么。
- 理解终止处理的机制。
- 使用 `finally` 块释放资源。
- 了解 `using` 语句如何自动释放资源。
- 理解 .NET 异常层次。
- 使用 `Exception` 属性。
- 创建新的异常类型。
- 使用 C# 6 的空条件运算符（`?.`）在调用引用类型方法或访问属性之前，判断其是否为 `null`。
- 使用可空值类型（nullable value types）指定变量可能包含值或 `null`。
- 使用 C# 6 异常过滤器指定捕获异常的条件。

![](img/57baed2319be0bb1b5f98674846f2711_547_0.png)

## 第 13 章异常处理：深入探讨

## 13.1 引言

## 13.2 示例：没有异常处理的除以零

## 13.3 处理：DivideByZeroExceptions 和 FormatExceptions

## 13.4 .NET 异常层次

## 13.5 Finally 块

## 13.6 using 语句

## 13.7 异常属性

## 13.8 自定义异常类

## 13.9 检查空引用：C# 6 及更高版本

### 13.2.1 除以零
### 13.2.2 输入非数字分母
### 13.2.3 未处理的异常会终止应用程序

### 13.3.1 在 try 块中编码代码
### 13.3.2 捕获异常
### 13.3.3 未捕获的异常
### 13.3.4 异常处理的终止模型
### 13.3.5 异常发生时的控制流

### 13.4.1 类 SystemException
### 13.4.2 哪些方法可能会抛出异常？

### 13.5.1 将代码移动到 Finally 块
### 13.5.2 演示 Finally 块
### 13.5.3 使用语句抛出异常
### 13.5.4 重新抛出异常
### 13.5.5 在 finally 块后返回

### 13.7.1 属性 InnerException
### 13.7.2 其他异常属性
### 13.7.3 演示异常属性和栈回溯
### 13.7.4 带有 InnerException 抛出异常
### 13.7.5 显示异常信息

### 13.9.1 空条件运算符 (?. )
### 13.9.2 复习运算符 is 和 as 运算符
### 13.9.3 可空类型
### 13.9.4 合并运算符 (??)

## 13.10 异常过滤器和 C# 6 子句

## 13.11 总结

### 13.1 引言

在本章中，我们将深入探讨异常处理。正如你从第 8.5 节所了解的，异常表示执行过程中发生了问题。“异常”（exception）一词源于：尽管问题可能会意外发生，但异常处理允许你创建在许多情况下处理异常的应用程序。更严重可能会阻止程序继续执行，除非要求使用异常处理程序以受控的方式处理问题。

在回顾了异常处理概念和基本异常处理技术后，我们概述了 .NET 的异常处理层次。这些资源是有限的，一次只能由一个程序使用。我们演示了异常处理机制的一项功能，该功能允许程序在发生异常时仍使用其他程序的资源。我们展示了 System.Exception（所有异常类的基类）的几个属性，并讨论了如何创建和使用自定义异常类，包括：

- C# 6 的空条件运算符（`?.`），它在用引用调用方法或访问属性之前判断该引用是否为 `null`。
- 合并运算符（`??`），如果左操作数为 `null`，则返回其左操作数的值，否则返回其右操作数的值。
- 可空类型，指定值类型变量可能包含一个值或 `null`。

最后，我们将介绍 C# 6 的异常过滤器，它用于指定捕获异常的条件。“异常处理最佳实践。” .NET Framework Developer's Guide, Visual Studio Online. 可访问：https://learn.microsoft.com/dotnet/

## 13.2 示例：没有异常处理的除以零

让我们重新回顾当不使用异常处理的控制台程序出现错误时会发生什么。图 13.1 从用户输入两个整数，然后使用整数除法将第一个除以第二个，以获得一个 `int` 结果。在这个示例中，当方法检测到问题且无法处理时，就会抛出异常（即发生异常）。

```csharp
// Fig. 13.1: DivideByExceptionHandling.cs
// 没有异常处理的整数除法。
class DivideByZeroExceptionHandling
{
    // 分子
    Console.Write("Please enter an integer numerator:");
    var numerator = int.Parse(Console.ReadLine());

    // 分母
    Console.Write("Please enter an integer denominator:");
    var denominator = int.Parse(Console.ReadLine());

    // 将两个整数相除，然后显示结果
    var result = numerator / denominator;
    Console.WriteLine($"\nResult: {numerator} / {denominator} = {result}");
}
```

![](img/57baed2319be0bb1b5f98674846f2711_549_0.png)

| 输出 1 | 输出 2 |
| :--- | :--- |
| Please enter an integer numerator: 100<br>Please enter an integer denominator: 7<br><br>Result: 100 / 7 = 14 | Please enter an integer numerator: 100<br>Please enter an integer denominator: 0<br><br>Unhandled Exception: System.DivideByZeroException:<br>Attempted to divide by zero.<br>At DivideByZeroExceptionHandler.Main()<br>At C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_01_DivideByZeroNoExceptionHandler.DivideByZeroExceptionHandler()<br>DivideByZeroNoExceptionHandler.cs:line: 18 |
| Please enter an integer numerator: 100<br>Please enter an integer denominator: hello<br><br>Unhandled Exception: System.FormatException:<br>Input string was not in a correct format.<br>At System.Number.ToNumber(String str, NumberStyles options, NumberBuffer&, NumberFormat info, Boolean parseDecimal)<br>At System.Number.Parse32(String s, NumberStyles style, NumberFormat info)<br>At Int32.Parse(String s)<br>At DivideByZeroExceptionHandler.Main()<br>At C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_01_DivideByZeroNoExceptionHandler.DivideByZeroExceptionHandler()<br>DivideByZeroNoExceptionHandler.cs:line: 15 |

**Fig. 13.1** | 没有异常处理的整数除法。（第 2 部分，共 2 部分。）

[/content]
