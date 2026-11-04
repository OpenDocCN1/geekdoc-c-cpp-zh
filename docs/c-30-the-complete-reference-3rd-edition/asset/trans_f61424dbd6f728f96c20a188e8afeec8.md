
关于使用 catch-all catch 有一点需要记住：它必须是 catch 序列中的最后一个 catch 子句。

> 注意 在绝大多数情况下，你不应使用“catch all”处理器来处理异常。通常最好单独处理代码可能产生的异常。不当使用“catch all”处理器可能导致本应在测试期间被捕获的错误被掩盖。并且用单个处理器正确处理所有类型的异常也很困难。话虽如此，在某些特定情况下，“catch all”处理器可能是合适的，例如在运行时代码分析工具中。

## 嵌套 try 块

一个 try 块可以嵌套在另一个 try 块内。内层 try 块中产生的异常如果未被与该 try 关联的 catch 捕获，则会传播到外层 try 块。例如，这里 IndexOutOfRangeException 未被内层 try 块捕获，而是由外层 try 捕获：

```csharp
// Use a nested try block.

using System;

class NestTrys {
    static void Main() {
        // Here, numer is longer than denom.
        int[] numer = { 4, 8, 16, 32, 64, 128, 256, 512 };
        int[] denom = { 2, 0, 4, 4, 0, 8 };

        try { // outer try
            for(int i=0; i < numer.Length; i++) {
                try { // nested try
                    Console.WriteLine(numer[i] + " / " +
                        denom[i] + " is " +
                        numer[i]/denom[i]);
                }
                catch (DivideByZeroException) {
                    Console.WriteLine("Can't divide by Zero!");
                }
            }
        }
        catch (IndexOutOfRangeException) {
            Console.WriteLine("No matching element found.");
            Console.WriteLine("Fatal error -- program terminated.");
        }
    }
}
```

程序的输出如下所示：

```
4 / 2 is 2
Can't divide by Zero!
16 / 4 is 4
32 / 4 is 8
Can't divide by Zero!
128 / 8 is 16
No matching element found.
Fatal error -- program terminated.
```

在此示例中，内层 try 可以处理的异常——在此情况下为除零错误——允许程序继续运行。然而，数组边界错误被外层 try 捕获，这导致程序终止。

虽然嵌套 try 语句的原因绝不仅仅于此，但前面的程序提出了一个可以推广的重要观点。通常，嵌套 try 块用于以不同方式处理不同类别的错误。某些类型的错误是灾难性的，无法修复。有些则是轻微的，可以立即处理。许多程序员使用外层 try 块捕获最严重的错误，让内层 try 块处理较不严重的问题。你也可以将外层 try 块用作“catch all”块，用于处理内层块未处理的错误。

## 抛出异常

前面的示例一直在捕获由运行时系统自动生成的异常。然而，使用 throw 语句手动抛出异常也是可能的。其一般形式如下所示：

```
throw exceptOb;
```

exceptOb 必须是派生自 Exception 的异常类的对象。

这里有一个示例，通过手动抛出 DivideByZeroException 来说明 throw 语句：

// Manually throw an exception.

using System;

class ThrowDemo {
 static void Main() {
   try {
     Console.WriteLine("Before throw.");
     throw new DivideByZeroException();
   }
   catch (DivideByZeroException) {
     Console.WriteLine("Exception caught.");
   }
   Console.WriteLine("After try/catch statement.");
 }
}
```

程序的输出如下所示：

```
Before throw.
Exception caught.
After try/catch statement.
```

注意 **DivideByZeroException** 是如何在 **throw** 语句中使用 **new** 创建的。记住，**throw** 抛出的是一个对象。因此，你必须为其创建对象来抛出。也就是说，你不能只抛出一个类型。在此情况下，使用默认构造函数创建 **DivideByZeroException** 对象，但异常也提供了其他构造函数。

最常见的情况是，你抛出的异常将是你自己创建的异常类的实例。正如本章后面将看到的，创建自己的异常类允许你将代码中的错误处理作为程序整体异常处理策略的一部分。

## 重新抛出异常

一个 **catch** 捕获的异常可以被重新抛出，以便由外层的 **catch** 捕获。重新抛出异常最可能的原因是允许多个处理器访问该异常。例如，也许一个异常处理器管理异常的一个方面，而第二个处理器应对另一个方面。要重新抛出异常，只需指定 **throw**，而不指定表达式。也就是说，你使用 **throw** 的这种形式：

```csharp
throw;
```

记住，当你重新抛出异常时，它不会被同一个 **catch** 子句再次捕获。相反，它会传播到外层的 **catch**。

以下程序说明了重新抛出异常。在此情况下，它重新抛出 **IndexOutOfRangeException**。

```csharp
// Rethrow an exception.

using System;

class Rethrow {
  public static void GenException() {
    // Here, num is longer than denom.
    int[] numer = { 4, 8, 16, 32, 64, 128, 256, 512 };
    int[] denom = { 2, 0, 4, 4, 0, 8 };

    for(int i=0; i<numer.Length; i++) {
      try {
        Console.WriteLine(numer[i] + " / " +
                          denom[i] + " is " +
                          numer[i]/denom[i]);
      }
      catch (DivideByZeroException) {
        Console.WriteLine("Can't divide by Zero!");
      }
      catch (IndexOutOfRangeException) {
        Console.WriteLine("No matching element found.");
        throw; // rethrow the exception
      }
    }
  }
}

class RethrowDemo {
  static void Main() {
    try {
Rethrow.GenException();
}
catch(IndexOutOfRangeException) {
    // recatch exception
    Console.WriteLine("Fatal error -- " + "program terminated.");
}
}
```

在此程序中，除零错误由 GenException() 本地处理，但数组边界错误被重新抛出。在此情况下，IndexOutOfRangeException 由 Main() 处理。

## 使用 finally

有时你会想要定义一个代码块，在离开 try/catch 块时执行。例如，异常可能导致错误而终止当前方法，导致其过早返回。然而，该方法可能已打开需要关闭的文件或网络连接。这类情况在编程中很常见，而 C# 提供了便捷的处理方式：finally。

要指定在退出 try/catch 块时执行的代码块，请在 try/catch 序列末尾包含一个 finally 块。包含 finally 的 try/catch 的一般形式如下所示：

```
try {
    // block of code to monitor for errors
}
catch (ExceptType1 exOb) {
    // handler for ExceptType1
}
catch (ExceptType2 exOb) {
    // handler for ExceptType2
}
:
finally {
    // finally code
}
```

finally 块将在执行离开 try/catch 块时执行，无论导致其离开的条件是什么。也就是说，无论 try 块是正常结束还是因异常结束，最后执行的代码都是 finally 定义的代码。如果 try 块或其任何 catch 块中的代码从方法返回，finally 块也会被执行。

这里有一个 finally 的示例：

// Use finally.
using System;
class UseFinally {
public static void GenException(int what) {
```

还有一点：从语法上讲，当 finally 块跟随 try 块时，技术上不需要 catch 子句。因此，你可以有 try 后跟 finally 而没有 catch 子句。在这种情况下，finally 块在 try 退出时执行，但不会处理任何异常。

## 更深入地了解 Exception 类

到目前为止，我们一直在捕获异常，但尚未对异常对象本身做任何操作。如前所述，catch 子句允许你指定异常类型和变量。变量接收对异常对象的引用。由于所有异常都派生自 Exception，所有异常都支持 Exception 定义的成员。在这里，我们将检查其中几个最有用的成员和构造函数，并使用异常变量。

Exception 定义了多个属性。其中最有趣的三个是 Message、StackTrace 和 TargetSite。它们都是只读的。Message 包含描述错误性质的字符串。StackTrace 包含导致异常的调用堆栈的字符串。TargetSite 获取指定生成异常的方法的对象。

Exception 还定义了多个方法。其中你经常会使用的是 ToString()，它返回描述异常的字符串。例如，当通过 WriteLine() 显示异常时，ToString() 会自动被调用。

以下程序演示了这些属性和该方法：

```csharp
// Using Exception members.

using System;

class ExcTest {
    public static void GenException() {
        int[] nums = new int[4];

        Console.WriteLine("Before exception is generated.");

        // Generate an index out-of-bounds exception.
        for(int i=0; i < 10; i++) {
            nums[i] = i;
            Console.WriteLine("nums[{0}]: {1}", i, nums[i]);
        }

        Console.WriteLine("this won't be displayed");
    }
}

class UseExcept {
    static void Main() {
        try {
            ExcTest.GenException();
        }
        catch (IndexOutOfRangeException exc) {
```
