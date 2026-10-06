

## 两个真一假

## 创建你自己的异常类

- 1. 要创建可以可以抛出其对象的异常类型，你可以扩展 `ApplicationException` 类或 `Exception` 类。
- 2. 在 C# 中，如果某个对象对应用程序是合适的，你可以抛出你创建的任何对象。
- 3. 你可以在任何时间抛出任何类型的异常——包括那些作为 C# 部分已创建的异常以及你创建的异常。

`Exception` 或 `Exception` 类的派生类。
错误的陈述是 #2。在 C# 中，除非对象是 `Exception`，否则你无法抛出现。

## 重新抛出异常

当你编写一个捕获异常的方法时，你的方法并不需要处理它。相反，你可能选择**重新抛出异常**给调用你方法的方法。然后，你可以让调用方法来处理该问题。

在 **catch** 块中，你可以使用关键字 **throw** 且后不跟任何对象，来重新抛出一个被捕获的未命名异常。例如，图 11-37 显示了一个包含方法的类。在该程序中，发生了以下事件序列：

- 1. `Main()` 方法调用 `MethodA()`。
- 2. `MethodA()` 调用 `MethodB()`。
- 3. `MethodB()` 调用 `MethodC()`。
- 4. `MethodC()` 抛出一个 `Exception`。
- 5. 当 `MethodB()` 捕获到 `Exception` 时，它没有处理该 `Exception`；而是将 `Exception` 抛回给 `MethodA()`。
- 6. `MethodA()` 捕获了 `Exception` 但也没有处理。相反，`MethodA()` 将 `Exception` 抛回给 `Main()` 方法。
- 7. `Exception` 在 `Main()` 方法中被捕获，在 `MethodC()` 中创建的消息最终显示出来。

图 11-38 显示了程序的执行情况。

## 第11 章 异常处理

```csharp
using System;
using static System.Console;
class ReThrowDemo{
    static void Main()
    {
        try {
            WriteLine("Trying in Main() method");
            MethodA();
        } catch (Exception ae)
        {
            WriteLine("Caught in Main() method --\n {0}",
                ae.Message);
        }
        WriteLine("Main() is done");
    }
    private static void MethodA()
    {
        try {
            WriteLine("Trying in method A");
            MethodB();
        } catch (Exception)
        {
            WriteLine("Caught in method A");
            throw();
        }
    }
    private static void MethodB()
    {
        try {
            WriteLine("Trying in method B");
            MethodC();
        } catch (Exception)
        {
            WriteLine("Caught in method B");
            throw();
        }
    }
    private static void MethodC()
    {
        WriteLine("In method C");
        throw(new Exception("This came from method C"));
    }
}
```

**图 11-37** ReThrowDemo 程序

## 章总结

```
Trying in Main() method
Trying in method A
Trying in method B
in method C
Caught in method B
Caught in method A
Caught in Main() method --
  This came from method C
Main() method is done
```

**图 11-38** ReRewDemo 程序的执行

如果你在 catch 块中为异常参数命名（例如，`catch (Exception e)`），那么在块块中使用 `throw` 语句时，应该使用该标识符（例如，`throw e`）；

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_551_0.png)

## 章总结

- 异常是执行中的程序中的任何错误状况或意外行为。在 C# 中，所有异常都是 `Exception` 类或其一个派生类的实例对象。你大多数异常派生自三个类：`SystemException`、`ApplicationException` 以及它们的父类 `Exception`。你可以通过强制程序包含错误来故意生成 `SystemException`。虽然你不是要求处理异常，但可以使用面向对象的技术提供优雅的错误处理解决方案。

## 第11 章 异常处理

- 当你认为错误会频繁发生时，最有效的方法是使用传统方式（即 `if` 语句）处理错误。如果错误发生频率较低，在需要时实例化 `Exception` 对象会更有效。在面向对象的术语中，你“尝试”（try）一个可能无法正常完成的过程。检测错误状况的方法“抛出”（throws）异常，而检测错误的代码块“捕获”（catch）异常。你必须包含至少一个 `catch` 块，或者在 `try` 块之后立即结束。

- 每个 `Exception` 对象都包含一个 `ToString()` 方法和一个 `Message` 属性，该属性包含关于异常的有用信息。

- 你可以在 `try` 块中放置任意数量的语句，并可以捕获任意数量不同的异常。如果错误发生频率较低，在需要时实例化 `Exception` 对象会更有效。在面向对象的术语中，你“尝试”（try）一个可能无法正常完成的过程。检测错误状况的方法“抛出”（throws）异常，而检测错误的代码块“捕获”（catch）异常。你必须包含至少一个 `catch` 块，或者在 `try` 块之后立即结束。

- 每个 `Exception` 对象都包含一个 `ToString()` 方法和一个 `Message` 属性，该属性包含关于异常的有用信息。

- 你可以在 `try` 块中放置任意数量的语句，并可以捕获任意数量不同的异常。如果错误发生频率较低，在需要时实例化 `Exception` 对象会更有效。在面向对象的术语中，你“尝试”（try）一个可能无法正常完成的过程。检测错误状况的方法“抛出”（throws）异常，而检测错误的代码块“捕获”（catch）异常。你必须包含至少一个 `catch` 块，或者在 `try` 块之后立即结束。

- 你可以在 `try` 块中放置任意数量的语句，并可以捕获任意数量不同的异常。如果错误发生频率较低，在需要时实例化 `Exception` 对象会更有效。在面向对象的术语中，你“尝试”（try）一个可能无法正常完成的过程。检测错误状况的方法“抛出”（throws）异常，而检测错误的代码块“捕获”（catch）异常。你必须包含至少一个 `catch` 块，或者在 `try` 块之后立即结束。

- 你可以在 `try` 块中放置任意数量的语句，并可以捕获任意数量不同的异常。如果错误发生频率较低，在需要时实例化 `Exception` 对象会更有效。在面向对象的术语中，你“尝试”（try）一个可能无法正常完成的过程。检测错误状况的方法“抛出”（throws）异常，而检测错误的代码块“捕获”（catch）异常。你必须包含至少一个 `catch` 块，或者在 `try` 块之后立即结束。

## 关键术语

异常是执行程序中的任何错误状况或意外行为。

异常处理是管理执行程序中意外错误的面向对象技术集。

## 复习题

1. 程序中的任何错误代码或意外行为被称为
2. 下列哪项被视为 C# 异常？
   a. 你的程序要求用户输入数字，但用户输入了字符。
   b. 你计算了一个对于答案变量类型过大的值。
   c. 你尝试使用大下标访问数组。
   d. 你尝试执行一个 C# 程序，但 C# 编译器尚未编译它。
3. 大多数异常派生自三个类：
   a. Object, ObjectException, 和 ObjectApplicationException
   b. Exception, SystemException, 和 ApplicationException
   c. FormatException, ApplicationException, 和 IOExceptionException
   d. SystemException, IOException, 和 FormatException

