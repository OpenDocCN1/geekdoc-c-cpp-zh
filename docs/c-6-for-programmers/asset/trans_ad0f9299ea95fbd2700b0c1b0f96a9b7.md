
### 13.7.2 其他异常属性

Exception 类提供了其他属性，包括 HelpLink、Source 和 TargetSite：

- 属性 HelpLink 指定一个指向帮助文件的链接，该帮助文件描述发生的问题。如果不存在此类文件，此属性为 null。
- 属性 Source 指定导致该异常的程序集（即应用或库）的名称。
- 属性 TargetSite 指定异常最初发生的方法。

### 13.7.3 演示异常属性和堆栈展开

我们的下一个示例（图 13.5）演示 Exception 类的 Message、StackTrace 和 InnerException 属性。此外，该示例正式介绍堆栈展开——当异常被抛出但在特定作用域中未被捕获时，方法调用堆栈会被“展开”，并尝试在下一个外层 try 块中捕获该异常。在讨论 StackTrace 属性和堆栈展开机制时，我们会跟踪调用堆栈上的方法。要查看正确的堆栈跟踪，应使用与 13.2 节所示步骤类似的方式执行此程序。

```csharp
// Fig. 13.5: Properties.cs
// Stack unwinding and Exception class properties.
// Demonstrates using properties Message, StackTrace and InnerException.
using System;

class Properties
{
    static void Main()
    {
        // call Method1; any Exception generated is caught
        // in the catch block that follows
        try
        {
            Method1();
        }
        catch (Exception exceptionParameter)
        {
            // output the string representation of the Exception, then output
            // properties Message, StackTrace and InnerException
            Console.WriteLine("exceptionParameter.ToString: \n" +
                exceptionParameter);
            Console.WriteLine("exceptionParameter.Message: \n" +
                exceptionParameter.Message);
            Console.WriteLine("exceptionParameter.StackTrace: \n" +
                exceptionParameter.StackTrace);
            Console.WriteLine("exceptionParameter.InnerException: \n" +
                exceptionParameter.InnerException);
        }
    }

    // calls Method2
    static void Method1()
    {
        Method2();
    }

    // calls Method3
    static void Method2()
    {
        Method3();
    }

    // throws an Exception containing an InnerException
    static void Method3()
    {
        // attempt to convert string to int
        try
        {
            int.Parse("Not an integer");
        }
        catch (FormatException formatExceptionParameter)
        {
            // wrap FormatException in new Exception
            throw new Exception("Exception occurred in Method3", formatExceptionParameter);
        }
    }
}
```

**图 13.5** | 堆栈展开和 Exception 类属性。（第 1 部分，共 3 部分。）

```text
exceptionParameter.ToString:
System.Exception: Exception occurred in Method3 ---> System.FormatException: Input string was not in a correct format.
at System.Number.StringToNumber(String str, NumberStyles options, NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
at System.Number.ParseInt32(String s, NumberStyles style, NumberFormatInfo info)
at System.Int32.Parse(String s)
at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 49
--- End of inner exception stack trace ---
at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 54
at Properties.Method2() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 40
at Properties.Method1() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 34
at Properties.Main() in C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_05\Properties\Properties\Properties.cs:line 14

exceptionParameter.Message:
Exception occurred in Method3

exceptionParameter.StackTrace:
  at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\
    ch13\Fig13_05\Properties\Properties.cs:line 54
  at Properties.Method2() in C:\Users\PaulDeitel\Documents\examples\
    ch13\Fig13_05\Properties\Properties.cs:line 40
  at Properties.Method1() in C:\Users\PaulDeitel\Documents\examples\
    ch13\Fig13_05\Properties\Properties.cs:line 34
  at Properties.Main() in C:\Users\PaulDeitel\Documents\examples\
    ch13\Fig13_05\Properties\Properties.cs:line 14

exceptionParameter.InnerException:
System.FormatException: Input string was not in a correct format.
  at System.Number.StringToNumber(String str, NumberStyles options,
    NumberBuffer& number, NumberFormatInfo info, Boolean parseDecimal)
  at System.Number.ParseInt32(String s, NumberStyles style,
    NumberFormatInfo info)
  at System.Int32.Parse(String s)
  at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\
    ch13\Fig13_05\Properties\Properties.cs:line 49
```

**图 13.5** | 堆栈展开和 Exception 类属性。（第 2 部分，共 3 部分。）

**图 13.5** | 堆栈展开和 Exception 类属性。（第 3 部分，共 3 部分。）

程序执行从 Main 开始，Main 成为方法调用堆栈上的第一个方法。Main 中 try 块的第 14 行（图 13.5）调用 Method1（声明于第 32–55 行），Method1 成为堆栈上的第二个方法。如果 Method1 抛出异常，第 16–28 行的 catch 块会处理该异常，并输出关于所发生异常的信息。Method1 的第 34 行调用 Method2（第 38–41 行），Method2 成为堆栈上的第三个方法。然后 Method2 的第 40 行调用 Method3（第 44–57 行），Method3 成为堆栈上的第四个方法。

此时，程序的方法调用堆栈（从上到下）为

```text
Method3
Method2
Method1
Main
```

最近被调用的方法（Method3）位于堆栈顶部；最先被调用的方法（Main）位于底部。Method3 中的 try 语句（第 47–56 行）调用方法 int.Parse（第 49 行），它尝试将字符串转换为 int。此时，int.Parse 成为调用堆栈上的第五个也是最后一个方法。

### 13.7.4 抛出带有 InnerException 的异常

由于 int.Parse 的参数不是 int 格式，第 49 行抛出一个 FormatException，并在 Method3 的第 51 行被捕获。该异常终止对 int.Parse 的调用，因此该方法从方法调用堆栈中展开（即移除）。然后 Method3 中的 catch 块创建并抛出一个 Exception 对象。Exception 构造函数的第一个参数是本示例的自定义错误消息：“Exception occurred in Method3.” 第二个参数是 InnerException——即被捕获的 FormatException。这个新异常对象的 StackTrace 反映异常抛出的位置（第 54–55 行）。现在 Method3 终止，因为 catch 块中抛出的异常未在方法体内被捕获。因此，控制权返回到调用堆栈中前一个方法（Method2）中调用 Method3 的语句。这会将 Method3 从方法调用堆栈中*展开*。

当控制权返回到 Method2 的第 40 行时，CLR 判定第 40 行不在 try 块中。因此异常无法在 Method2 中捕获，Method2 终止。这会将 Method2 从调用堆栈中*展开*，并将控制权返回到 Method1 的第 34 行。

这里同样，第 34 行不在 try 块中，因此 Method1 无法捕获该异常。该方法终止并从调用堆栈中*展开*，将控制权返回到 Main 中的第 14 行，该行位于 try 块中。Main 中的 try 块退出，catch 块（第 16–28 行）捕获该异常。catch 块使用 Message、StackTrace 和 InnerException 属性生成输出。堆栈展开会一直持续，直到某个 catch 块捕获异常或程序终止。

### 13.7.5 显示异常相关信息

图 13.5 中的第一块输出（为便于阅读，我们重新格式化了它）包含异常的字符串表示形式，该表示形式由对方法 ToString 的*隐式*调用返回。该字符串以异常类的名称开头，后跟 Message 属性值。接下来的四项显示 InnerException 对象的堆栈跟踪。该输出块的其余部分显示 Method3 第 54–55 行抛出的异常的 StackTrace。StackTrace 表示异常抛出点处的方法调用堆栈状态，而不是异常最终被捕获点处的状态。每个以“at”开头的 StackTrace 行表示调用堆栈上的一个方法。这些行指出异常所在的方法、该方法所在的文件以及文件中抛出点的行号。内部异常信息包括*内部异常*堆栈跟踪。

> **错误预防提示 13.5**
> 
> *在捕获并重新抛出异常时，请在重新抛出的异常中提供额外的调试信息。为此，请创建一个包含更具体调试信息的 Exception 子类对象，然后将原始捕获的异常传递给新异常对象的构造函数，以初始化 InnerException 属性。*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_421_0.png)

下一块输出（两行）仅显示 Method3 中抛出的异常的 Message 属性值（Exception occurred in Method3）。

第三块输出显示 Method3 中抛出的异常的 StackTrace 属性。此 StackTrace 属性包含从 Method3 第 54 行开始的堆栈跟踪，因为这是 Exception 对象被创建并抛出的位置。堆栈跟踪总是从异常的抛出点开始。

最后，最后一块输出显示 InnerException 属性的字符串表示形式，其中包括异常对象的命名空间和类名，以及其 Message 和 StackTrace 属性。

## 13.8 用户定义的异常类

在许多情况下，你可以使用 .NET Framework 类库中的现有异常类来表示程序中发生的异常。然而，在某些情况下，你可能希望针对程序中发生的问题创建新的异常类。用户定义的异常类应直接或间接派生自 Ex-
