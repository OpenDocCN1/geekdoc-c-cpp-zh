
type of exception that int.Parse() threw, the code inside this block will execute. If a statement within the try block throws a different exception, the second catch block would execute because all exceptions are of type System.Exception.

![](img/25683ccec0773ba5b8794b11f2b12877_244_0.png)

Figure 4.1: Exception-Handling Program Flow

如果没有 System.FormatException 的 catch 块，System.Exception 的 catch 块就会执行，即使 int.Parse 抛出的是 System.FormatException。这是因为 System.FormatException 也是 System.Exception 的一种类型。System.FormatException 是通用异常 System.Exception 的更具体实现。

处理异常的顺序很重要。catch 块必须从最具体到最不具体排列。System.Exception 数据类型是最不具体的，因此排在最后。System.FormatException 排在最前面，因为它是列表 4.21 处理的最具体的异常。

无论控制是否正常离开 try 块，还是因为 try 块中的代码抛出异常，finally 代码块在控制离开 try 保护区域后都会执行。finally 块的目的是提供一个位置来放置无论 try/catch 块如何退出——是否出现异常——都会执行的代码。finally 块对于在是否抛出异常的情况下清理资源很有用。事实上，可以有一个只有 finally 块而没有 catch 块的 try 块。finally 块无论 try 块是否抛出异常，或是否编写了 catch 块来处理异常都会执行。列表 4.22 演示了 try/finally 块，输出 4.14 显示了结果。

## LISTING 4.22: Finally Block without a Catch Block

```
using System;

class ExceptionHandling
{
    static int Main()
    {
        string firstName;
        string ageText;
        int age;
        int result = 0;

        Console.Write("Enter your first name: ");
        firstName = Console.ReadLine();

        Console.Write("Enter your age: ");
        ageText = Console.ReadLine();

        try
{
    age = int.Parse(ageText);
    Console.WriteLine(
        $"Hi { firstName }! You are { age*12 } months old.");
}
finally
{
    Console.WriteLine($"Goodbye { firstName }");
}

return result;
}
}
```

## OUTPUT 4.14

```
Enter your first name: Inigo
Enter your age: forty-two

Unhandled Exception: System.FormatException: Input string was not in a correct format.
  at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
  at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
  at ExceptionHandling.Main()
Goodbye Inigo
```

细心的读者会注意到这里有一个有趣的现象：运行时首先报告了未处理的异常，然后才运行 finally 块。这不寻常的行为如何解释？

首先，这种行为是合法的，因为当异常未被处理时，运行时的行为是实现定义的；任何行为都是合法的！运行时选择这种特定行为是因为它在决定运行 finally 块之前就知道异常将不会被处理；运行时已经检查了调用栈上的所有激活帧，并确定其中没有一个与匹配所抛异常的 catch 块相关联。

一旦运行时确定异常将不会被处理，它就会检查机器上是否安装了调试器，因为你可能是正在分析此故障的软件开发人员。如果存在调试器，它会在 finally 块运行之前提供用户将调试器附加到进程的机会。如果没有安装调试器或用户拒绝调试问题，默认行为是向控制台打印未处理的异常，然后查看是否有可以运行的 finally 块。由于情况的“实现定义”性质，运行时在此情况下不要求运行 finally 块；实现可以选择这样做也可以不做。

## Guidelines

- **AVOID** 显式地从 finally 块中抛出异常。隐式抛出异常的方法调用是可以接受的。
- **DO** 优先使用 try/finally，避免使用 try/catch 进行清理代码。
- **DO** 抛出描述发生了哪种异常情况的异常，如果可能的话，还说明如何防止它。

## ADVANCED TOPIC

## Exception Class Inheritance

从 C# 2.0 开始，所有作为异常抛出的对象都派生自 System.Exception。非派生自 System.Exception 的其他语言抛出的对象会被自动“包装”成派生自该类的对象。因此，它们可以由 catch(System.Exception exception) 块处理。然而，更可取的是包含一个针对最派生类型特定 catch 块，例如 System.FormatException，因为这样可以获得有关异常的最详细信息并以更少泛化的方式处理它。这样，使用最派生类型的 catch 语句能够专门处理异常类型，访问与所抛异常相关的数据，避免使用条件逻辑来确定发生了什么类型的异常。

这就是为什么 C# 强制要求 catch 块从最派生到最不派生排列的原因。例如，捕获 System.Exception 的 catch 语句不能出现在捕获 System.FormatException 的语句之前，因为 System.FormatException 派生自 System.Exception。

一个方法可能抛出许多异常类型。表 4.2 列出了框架中一些更常见的异常类型。

## TABLE 4.2: Common Exception Types

| Exception Type | Description |
|---|---|
| System.Exception | 所有其他异常派生的“基”异常。 |
| System.ArgumentException | 表示传递给方法的一个参数无效。 |
| System.ArgumentNullException | 表示某个参数为 null，而这对该参数而言不是有效值。 |
| System.ApplicationException | 应避免使用。最初的想法是你可能想要对“系统”异常和“应用程序”异常有一种不同的处理方式，虽然合理，但在现实世界中并不实际。 |
| System.FormatException | 表示字符串格式对于转换无效。 |
| System.IndexOutOfRangeException | 表示尝试访问不存在的数组或其他集合元素。 |
| System.InvalidCastException | 表示尝试从一种数据类型转换为另一种数据类型不是有效的转换。 |
| System.InvalidOperationException | 表示发生了意外的场景，使得应用程序不再处于有效运行状态。 |
| System.NotImplementedException | 表示尽管方法签名存在，但尚未完全实现。 |
| System.NullReferenceException | 当代码尝试查找由空引用引用的对象时抛出。 |
| System.ArithmeticException | 表示无效的数学运算，不包括除零。 |
| System.ArrayTypeMismatchException | 在尝试将错误类型的元素存储到数组中时发生。 |
| System.StackOverflowException | 表示递归深度异常。 |

## ADVANCED TOPIC

## General catch

可以指定一个不带参数的 catch 块，如列表 4.23 所示。

## LISTING 4.23: General Catch Blocks

```
...
try
{
    age = int.Parse(ageText);
    System.Console.WriteLine(
        $"Hi { firstName }!  You are { age*12 } months old.");
}
catch (System.FormatException exception)
{
    System.Console.WriteLine(
        $"The age entered ,{ ageText }, is not valid.");
    result = 1;
}
catch(System.Exception exception)
{
    System.Console.WriteLine(
        $"Unexpected error: { exception.Message }");
    result = 1;
}
catch
{
    System.Console.WriteLine("Unexpected error!");
    result = 1;
}
finally
{
    System.Console.WriteLine($"Goodbye { firstName }");
}
...
```

不带数据类型的 catch 块称为通用 catch 块，等同于指定一个接受 object 数据类型的 catch 块——例如 catch(object exception){...}。由于所有类最终都派生自 object，因此不带数据类型的 catch 块必须排在最后。

通用 catch 块很少使用，因为没有任何方式捕获有关异常的信息。此外，C# 不支持抛出 object 类型的异常的能力。仅使用 C++ 等语言编写的库允许抛出任何类型的异常。

