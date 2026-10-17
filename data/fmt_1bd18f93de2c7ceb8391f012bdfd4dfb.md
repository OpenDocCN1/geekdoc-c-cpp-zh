
| 从变量中减去一个金额 | 使用复合减法运算符。例如：`variable -= amount;` |

| 在条件为 true 时零次或多次运行一个或多个语句 | 使用 `while` 语句。例如：``` int i = 0; while (i < 10) { Console.WriteLine(i); i++; } ``` 或者，使用 `for` 语句。例如：``` for (int i = 0; i < 10; i++) { Console.WriteLine(i); } ``` |
| 重复执行语句一次或多次 | 使用 `do` 语句。例如：``` int i = 0; do { Console.WriteLine(i); i++; } while (i < 10); ``` |

## 第 6 章. 管理错误和异常

完成本章后，你将能够：

- 使用 `try`、`catch` 和 `finally` 语句处理异常。
- 使用 `checked` 和 `unchecked` 关键字控制整数溢出。
- 使用 `throw` 关键字从自己的方法中引发异常。
- 使用 `finally` 块确保代码始终运行，即使在发生异常后也是如此。

你现在已经看到了执行常见任务所需了解的核心 C# 语句，例如编写方法、声明变量、使用运算符创建值、编写 `if` 和 `switch` 语句以有选择地运行代码，以及编写 `while`、`for` 和 `do` 语句以重复运行代码。然而，前面的章节并未考虑事情出错的可能性（或概率）。

很难确保一段代码始终按预期工作。故障可能由于大量原因而发生，其中许多原因超出了程序员的控制范围。你编写的任何应用程序都必须能够检测故障并以优雅的方式处理它们，要么采取适当的纠正措施，要么，如果不可能，则以最清晰的方式向用户报告故障原因。在第一部分本章的最后，你将学习 C# 如何使用异常来发出错误已发生的信号，以及如何使用 `try`、`catch` 和 `finally` 语句来捕获和处理这些异常所代表的错误。

到本章结束时，你将对 C# 的所有基本要素有一个坚实的基础，并在第二部分中在此基础上构建。

### 应对错误

生活就是这样，有时坏事会发生。轮胎被扎破，电池耗尽，螺丝刀永远不在你放的地方，你的应用程序的用户行为不可预测。在计算机世界中，硬盘损坏，与你的程序在同一台计算机上运行的其他应用程序失控并使用完所有可用内存，无线网络连接在最不合适的时候消失，甚至附近的雷击如果导致停电或网络故障也会产生影响。错误可能在程序运行的几乎任何阶段发生，而且许多错误可能根本不是你自己应用程序的过错，那么你如何检测它们并尝试恢复呢？

多年来，已经演化出许多机制。旧系统如 UNIX 采用的一种典型方法涉及安排操作系统

system to set a special global variable whenever a method failed. Then, after each call to a method, you checked the global variable to see whether the method succeeded. C# and most other modern object-oriented languages don’t handle errors in this manner; it’s just too painful. Instead, they use `exceptions`. If you want to write robust C# programs, you need to know about exceptions.

### Trying code and catching exceptions

Errors can happen at any time, and using traditional techniques to manually add error-detecting code around every statement is cumbersome, time-consuming, and error prone in its own right. You can also lose sight of the main flow of an application if each statement requires contorted error-handling logic to manage each possible error that can occur at every stage. Fortunately, C# makes it easy to separate the error-handling code from the code that implements the primary logic of a program by using exceptions and exception handlers. To write exception-aware programs, you need to do two things:

- Write your code within a `try` block (`try` is a C# keyword). When the code runs, it attempts to execute all the statements in the `try` block, and if none of the statements generates an exception, they all run, one after the other, to completion. However, if an error condition occurs, execution jumps out of the `try` block and into another piece of code designed to catch and handle the exception—a `catch` handler.

- Write one or more `catch` handlers (`catch` is another C# keyword) immediately after the `try` block to handle any possible error conditions. A `catch` handler is intended to capture and handle a specific type of exception, and you can have multiple `catch` handlers after a `try` block, each one designed to trap and process a specific exception. This enables you to provide different handlers for the different errors that could arise in the `try` block. If any one of the statements within the `try` block causes an error, the runtime throws an exception. The runtime then examines the `catch` handlers after the `try` block and transfers control directly to the first matching handler.

Here’s an example of a `try` block that contains code that attempts to convert strings that a user has typed in some text boxes on a form to integer values. The code then calls a method to calculate a value and writes the result to another text box. Converting a string to an integer requires that the string contain a valid set of digits and not some arbitrary sequence of characters. If the string contains invalid characters, the `int.Parse` method throws a `FormatException`, and execution transfers to the corresponding `catch` handler. When the `catch` handler finishes, the program continues with the first statement that follows the handler. Note that if there is no handler that corresponds to the exception, the exception is said to be unhandled (this situation will be described shortly).

```
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (FormatException fEx)
{
    // Handle the exception
    ...
}
```

A catch handler employs syntax similar to that used by a method parameter to specify the exception to be caught. In the preceding example, when a FormatException is thrown, the fEx variable is populated with an object containing the details of the exception.

The FormatException type has a number of properties that you can examine to determine the exact cause of the exception. Many of these properties are common to all exceptions. For example, the Message property contains a text description of the error that caused the exception. You can use this information when handling the exception, perhaps recording the details in a log file or displaying a meaningful message to the user and then asking the user to try again.

### Unhandled exceptions

What happens if a try block throws an exception and there is no corresponding catch handler? In the previous example, it is possible that the lhsOperand text box could contain the string representation of a valid integer but the integer it represents is outside the range of valid integers supported by C# (for example, “2147483648”). In this case, the int.Parse statement would throw an OverflowException, which will not be caught by the FormatException catch handler. If this occurs and the try block is part of a method, the method immediately exits and execution returns to the calling method. If the calling method uses a try block, the runtime attempts to locate a matching catch handler for this try block and execute it. If the calling method does not use a try block or there is no matching catch handler, the calling method immediately exits and execution returns to its caller, where the process is repeated. If a matching catch handler is eventually found, the handler runs and execution continues with the first statement that follows the catch handler in the catching method.

## Important

Notice that after catching an exception, execution continues in the method containing the catch block that caught the exception. If the exception occurred in a method other than the one containing the catch handler, control does not return to the method that caused the exception.

If, after cascading back through the list of calling methods, the runtime is unable to find a matching catch handler, the program will terminate with an unhandled exception.

You can easily examine exceptions generated by your application. If you are running the application in Microsoft Visual Studio 2015 in debug mode (that is, on the Debug menu you selected Start Debugging to run the application) and an exception occurs, a dialog box similar to the one shown in the following image appears and the application pauses, helping you to determine the cause of the exception:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_177_0.png)

The application stops at the statement that caused the exception, and you drop into the debugger. You can examine the values of variables, you can change the values of variables, and you can step through your code from the point at which the exception occurred by using the Debug toolbar and the various debug windows.

### Using multiple catch handlers

The previous discussion highlighted how different errors throw different kinds of exceptions to represent different kinds of failures. To cope with these situations, you can supply multiple `catch` handlers, one after the other, such as in the following:
