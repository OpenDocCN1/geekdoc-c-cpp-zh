
```
            Console.WriteLine("This is the finally block");

        }

    }

}

```

输出：

Exception has occurred - divide by zero
Exception has occurred - out of range
Exception has occurred - format exception
This is the finally block

在程序中，抛出的 `DivideByZeroException` 和 `IndexOutOfRangeException` 被各自的 `catch` 块捕获。`catch` 块显示“Exception has occurred - divide by zero”和“Exception has occurred - out of range”。此外，程序使用 `ToInt32` 函数尝试将字符串转换为整数，这是不可能的；抛出了 `FormatException` 异常。`FormatException` 异常被相应的 `catch` 块捕获，因此屏幕上显示“Exception has occurred - format exception”。

程序不仅可以有多个 `try` 块，单个 `try` 块也可以有多个 `catch` 块。

## 使用多个 catch 块

你可以为单个 `try` 块关联多个 `catch`。每个预期错误的代码都封装在 `try` 块中。每个 `catch` 块必须捕获不同类型的异常。当 `try` 中的任何语句抛出异常时，它会被相应的 `catch` 块捕获或持有。如果某个 `catch` 块处理了异常，则执行该 `catch` 块中的代码，程序在 `catch` 块之后继续执行。列表 13.5 所示的 `TryCatch2.cs` 文件捕获了三种异常：数组边界、除零错误和格式错误。

### 列表 13.5 TryCatch2.cs 文件中的代码

```csharp
using System;

class TryCatch2
{
    static void Main()
    {
        int x = 10,y=0,z=0,n=0;
        int[] p=new int[3];
        String str;
        try{
            z = x/y;
            Console.WriteLine("Result of dividing (0) by (1) is (2)", x,y,z);
        } catch(DivideByZeroException ex)
        {
            Console.WriteLine("Exception has occurred – divide by zero", ex);
        }
        try
        {
            p[3]=23;
            Console.WriteLine("Array element is {0}", p[0]);
        } catch(System.IndexOutOfRangeException ex)
        {
            Console.WriteLine("Exception has occurred – out of range", ex);
        }
        try
        {
            str="John";
            n=Convert.ToInt32(str);
            Console.WriteLine("Value in variable n is (0)", n);
        } catch(FormatException ex)
        {
            Console.WriteLine("Exception has occurred – format exception", ex);
        }
        finally
        {
            Console.WriteLine("This is the finally block");
        }
    }
}
```

输出：

Exception has occurred – divide by zero

变量 `x` 被除以 `y`（`y` 为 0），因此相应的 `catch` 块抛出了 `DivideByZeroException` 异常。处理异常的 `catch` 块显示了“Exception has occurred – divide by zero”消息。`try` 块中位于 `catch` 块之后的语句（即导致 `DivideByZeroException` 异常的语句）完全不执行。

要捕获所有类型的异常，你可以定义一个没有异常类型的 `catch` 块。这使得无论发生什么类型的异常，`catch` 块都会执行。以下语法处理了 `try` 块中可能发生的任何异常：

```c
try{
    // 可能导致 exception() 的代码
}
catch
{
    // 处理异常的代码
}
```

# 第 13 章 管理错误与异常

列表 13.6 显示的 `CatchAll.cs` 文件演示了一个可以处理所有类型异常的 catch 块。该程序包含三个 try 块，分别包含抛出 `DivideByZeroException`、`IndexOutOfRangeException` 和 `FormatException` 的代码。这三个异常被三个 catch 块捕获，每个 catch 块都被设置为捕获所有异常。

### 列表 13.6 CatchAll.cs 中的程序代码

```cs
using System;

class CatchAll
{
    static void Main()
    {
        int x=10,y=0,z=0,n=0;
        int[] p=new int[3];
        String str;
        try{
            z=x/y;
            Console.WriteLine("Result of dividing (0) by (1) is (2)", x,y,z);
        } catch(Exception ex)
        {
            Console.WriteLine("Exception has occurred - "+ex.ToString());
        }
        try{
            p[3]=23;
            Console.WriteLine("Array element is (0)", p[0]);
        } catch(Exception ex)
        {
            Console.WriteLine("Exception has occurred - "+ex.ToString());
        }
        try{
            str="John";
            n=Convert.ToInt32(str);
            Console.WriteLine("Value in variable n is (0)", n);
        } catch(Exception ex)
        {
            Console.WriteLine("Exception has occurred - "+ex.ToString());
        }
    }
}
```

## 输出：

Exception has occurred - System.DivideByZeroException: Attempted to divide by zero.
at CatchAll.Main()
Exception has occurred - System.IndexOutOfRangeException: Index was outside the bounds
of the array.
at CatchAll.Main()
Exception has occurred - System.FormatException: Input string was not in a correct
format.
at System.Number.ToStringNumber(String str, NumberStyles options, NumberBuffer&
number, NumberFormat info, Boolean parseDecimal)
at System.Number.ParseInt32(String s, NumberStyles style, NumberFormat info)
at CatchAll.Main()

你可以看到，无论 try 块抛出什么类型的异常，都会被 catch 块处理，并且每个 catch 块都包含一个异常类型参数。由于所有异常都继承自 `Exception` 类，因此每个 catch 块都可以处理任何异常。

## 抛出异常

到目前为止，你捕获的是运行时系统自动生成的异常。你也可以使用 `throw` 语句手动抛出异常。

语法：

```
throw exceptionObj;
```

在这里，`exceptionObj` 必须是派自 `Exception` 类的实例。列表 13.7 显示的 `ThrowException.cs` 文件演示了如何手动抛出 `DivideByZeroException` 异常。

### 13.7 ThrowException.cs 中的程序代码

```cs
using System;

class ThrowException
{
    static void Main()
    {
        int x=10,y=5,z=0;
        try{
            z=x/y;
            Console.WriteLine("Result of dividing (0) by (1) is (2)", x,y,z);
            throw new DivideByZeroException();
        }
catch(DivideByZeroException ex)
{
    Console.WriteLine("Exception has occurred", ex);
}
```

输出：

Result of dividing 10 by 5 is 2
Exception has occurred

你可以看到 `DivideByZeroException` 是在 `throw` 语句中使用 `new` 运算符捕获的。`new` 运算符创建了一个新对象。但为什么要创建一个对象呢？很简单。`throw` 块抛出的是对象，所以你必须创建一个对象供其抛出。

一个 catch 块捕获的异常可以被重新抛出，以便被另一个 catch 块捕获。其目的是检查相应的异常处理程序是否正确处理了异常。要重新抛出同一个异常，只需在 catch 块中编写一个不指定异常名称的 `throw`。

列表 13.8 显示的 `Exception.cs` 文件演示了手动抛出的异常如何被 catch 块捕获，以及 catch 块如何重新抛出另一个异常，该异常又被另一个 catch 块捕获。`DivideByZeroException` 被 catch 块捕获。

### 列表 13.8 Exception.cs 中的程序代码

```cs
using System;

class Throw
{
    static void disp(string str)
    {
        int x=10,y=5,z=0;
        try
        {
            z=x/y;
            Console.WriteLine("Result of dividing (0) by (1) is (2)", x,y,z);
            throw new DivideByZeroException();
        }
        catch(DivideByZeroException ex)
        {
            Console.WriteLine("Exception has occurred", ex);
        }
    }
    static void Main()
    {
        try
        {
            int[] p=new int[3];
            p[3]=23;
            disp("");
        }
        catch (IndexOutOfRangeException ex)
        {
            Console.WriteLine("Exception has occurred - "+ex.ToString());
            disp("John");
        }
    }
}
```

输出：

Exception has occurred - System.DivideByZeroException: Attempted to divide by zero.
Exception has occurred - System.IndexOutOfRangeException: Index was outside the bounds of the array.
Exception has occurred - System.DivideByZeroException: Attempted to divide by zero.

（注：第438-440 页的 OCR 文本非常碎片化且混乱。上述内容根据提供的代码片段和文中标准的异常处理模式进行的逻辑还原。）

## 嵌套 try 块

你可以将一个 try 块嵌套在另一个内部。嵌套 try 块的语法：

```
try // 外部 try 块
{
    try // 内部 try 块
    {
        // 可能引发异常的代码
    }
    catch(ExceptionType) // 内部 catch 块
    {
        // 处理异常的代码
    }
    finally // 内部 finally 块
    {
        // 任何清理代码
    }
}
catch(ExceptionType) // 外部 catch 块
{
    // 处理异常的代码
}
finally // 外部 finally 块
{
    // 任何清理代码
}
```

在使用嵌套 try 块时可能会发生的情况：

- 如果在外部 try 块但在内部 try 块之外抛出异常，异常将由外部 catch 块捕获，如果存在外部 finally 块也将执行。
- 如果在内部 try 块中抛出异常，它将由内部 catch 块捕获，并执行 finally 块（如果存在）。程序将从 catch 块后的语句继续在外部块执行。
- 如果在内部 try 块中抛出异常且没有相应的 catch 块来处理它，将执行内部 finally 块（如果存在）。同时，将搜索外部 catch 块查看它们是否可以处理此异常。如果可用，外部 catch 块将处理该异常，并执行外部 finally 块（如果存在）。

# 第 13 章 管理错误与异常

输出：

```
Exception has occurred, index out of range - System.IndexOutOfRangeException: Index was outside the bounds of the array.
at NestedTry.Main()
This is the inner finally block
Exception has occurred - divide by zero
This is the outer finally block
```

当内部 `catch` 块处理由内部 `try` 块抛出的 `IndexOutOfRangeException` 时，会显示 `Exception has occurred, index out of range`。随后在执行内部 `finally` 块时，会显示 `This is the inner finally block`。当外部 `try` 块抛出 `DivideByZeroException` 时，外部 `catch` 块会显示 `Exception has occurred - divide by zero` 信息。在执行外部 `finally` 块时，会显示 `This is the outer finally block` 信息。

# 创建你自己的异常

尽管 .NET Framework 包含了各种异常类型，足以处理大多数错误，但它还提供了一个创建你自定义异常的机制。自定义异常有助于简化代码并改进错误处理。自定义异常必须继承自 `System.Exception` 类或其标准派生类之一，如 `SystemException` 或 `ApplicationException`。`SystemException` 用于由 CLR 定义的异常，而 `ApplicationException` 是由用户程序抛出的。建议你从 `Exception` 类派生新的异常类。在最简单的形式中，自定义异常类只需要一个名称，如下所示：

```
