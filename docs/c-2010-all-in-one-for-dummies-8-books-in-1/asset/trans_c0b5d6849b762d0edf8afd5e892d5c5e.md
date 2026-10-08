

这种异常机制无疑比使用错误代码要复杂且难以处理。你需要在增加的难度与这些考虑因素之间取得平衡，如图 9-1 所示：

- 异常提供了一个更具“表现力”的模型——它允许你表达各种错误处理策略。
- 异常对象携带的信息多得多，因此有助于调试——远超错误代码所能提供的。
- 异常使代码更具可读性——代码更少。
- 异常是 C# 的不可或缺的一部分，而不是像错误代码方案那样随意的、附加的补救（后者没有两个方案是相似的）。一致的模型有助于理解。

## 自己自己抛出异常

如果 .NET 类库中的类可以抛出异常，那么你也可以。

当你检测到足以抛出异常的错误时，使用 `throw` 关键字：

```csharp
throw new ArgumentException("Don't argue with me!");
```

你和任何人一样有权抛出任何东西。因为 .NET 类库并不感知你自定义的 `BadHairDayException`，谁会帮你抛出它呢？

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_217_0.png)

如果 .NET 预定义的异常有一个适用于你的情况，但如果没有合适的，你可以创建自己的自定义异常类。

.NET 有一些你不应该永远抛出或捕获的异常：`StackOverflowException`、`OutOfMemoryException`、`ExecutionEngineException` 以及其他一些与非 .NET 代码交互相关的高级项目。它们属于系统。

## 了解异常的用途

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_217_1.png)

如果没有异常，软件将无法完成其设定的目标。例如，如果一个方法应该处理整个数组或读取整个文件——但由于某些原因无法完成工作——它应该抛出一个适当的异常。

方法可能因为各种原因任务失败：例如，输入值错误或意外情况（如文件比预期的要小或大）。任务不完整或甚至无法执行。如果你的方法中发生了任何这些情况，你都应该抛出一个异常。

## 记住

这里的核心点是，任何调用该方法的人都需要知道其任务未完成。抛出异常几乎比使用任何错误返回代码都要好。

第一卷
第 9 章

调用者如何处理异常取决于问题的性质和严重性。有些问题比其他问题糟糕。我们将使用本章的剩余部分——加上 csharp102.info 上的文章“响应异常”——来探索调用者在使用你的方法 `throws` 方法时的各种选择。

一些特殊的异常

## 我能得到一个异常的示例吗？

下面的 `FactorialException` 程序演示了异常的关键要素：

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_218_0.png)

```csharp
// FactorialException -- 创建一个使用 Exception 报告非法
// Factorial() 参数的阶乘数计算程序。
namespace FactorialException
{
    // MyMathFunctions -- 我们创建的一组数学函数
    // （目前看起来内容并不多）
    public class MyMathFunctions
    {
        // 返回所提供值的阶乘。
        public static int Factorial(int value)
        {
            // 不允许负数。
            if (value < 0)
            {
                // 报告负参数。
                string s = String.Format("Illegal negative argument to Factorial ({0})", value);
                throw new ArgumentException(s);
            }

            // 从 1 开始作为“累加器”。
            int factorial = 1;

            // 从 value 循环到 1，每次将
            // 之前的累加器值乘以结果。
            while (--value > 1)
            {
                factorial *= value;
            }

            // 返回累加值。
            return factorial;
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            // 这里是异常处理器。
            try
            {
                // 在从 6 到 -6 的循环中调用 factorial。
                for (int i = 6; i > -6; i--)
                {
                    // 计算数字的阶乘
                    int factorial = MyMathFunctions.Factorial(i);
                }
                // 显示每次运行的结果。
                Console.WriteLine("i = {}, factorial = {}", i, factorial);
            }
            catch (ArgumentException e)
            {
                // 这是一个“最后尝试”的异常处理器——责任在 Main 处终结。
                // 可能你在这里唯一能做的就是在退出前提醒用户。
                Console.WriteLine("Fatal error:");
                // 当你准备发布程序时，将此输出
                // 改为纯英文描述，最好带有如何处理问题的指南。
                Console.WriteLine(e.ToString());
            }
            // 等待用户确认。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

这个“异常”版本的 `Main()` 方法将其几乎所有的内容封装在 `try` 块中。`Main()` 结尾的 `catch` 块捕获了 `ArgumentException` 对象并使用其 `ToString()` 将异常对象中包含的大部分错误信息在一个字符串中显示。

我在这里选择使用 `ArgumentException` 是因为它最准确地描述了问题：给 `Factorial()` 传递了一个不可接受的参数。

## 了解是什么使示例变得异常的

上一节中的 `Factorial()` 方法版本包含了与之前版本相同的负参数检查。（对整数的测试不再相关，因为我们更改了 `Factorial()` 的参数和返回值为 `int`。）如果参数是负数，`Factorial()` 将无法继续，它会格式化描述问题的错误消息，包括发现的违规值。然后 `Factorial()` 将这些信息封装进新创建 `ArgumentException` 对象中，并将其抛回调用方法。

我建议在调试器中运行程序，以实时观察异常的发生。（我将在第四卷中告诉你更多关于调试器的信息。）

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_219_0.png)

## 我能得到一个异常的示例吗？

程序的输出如下（我们精简了错误信息以便于读）：

```
i = 6, factorial = 720
i = 5, factorial = 120
i = 4, factorial = 24
i = 3, factorial = 6
i = 2, factorial = 2
i = 1, factorial = 1
Fatal error:
System.ArgumentException: Illegal negative argument to Factorial -1
   at FactorialException.MyMathFunctions.Factorial(Int32) in c:\programs\Program.cs:21
   at FactorialException.Program.Main(String[] args) in c:\programs\Program.cs:49
Press Enter to terminate...
```

该程序的输出几行显示了通过 0 的实际阶乘。尝试计算 -1 的阶乘产生了以 Fatal error 开头的消息。

错误消息的第一行是在 `Factorial()` 内部格式化的。该行描述了问题的性质，包括违规的值。

## 追踪堆栈

输出的其余部分是堆栈跟踪。堆栈的第一行描述了异常抛出的位置。在这种情况下，异常发生在 `Factorial(int)` 中——具体位于 `c:\programs\Program.cs:21`。`Factorial()`是在 `Main(string())` 中调用的。堆栈在 `Main()` 处停止，因为那是捕获异常的模块——堆栈结束。

你不得不承认这个过程是令人深刻的——消息描述了问题并识别了错误的参数。堆栈告诉你异常是在哪里抛出的，以及程序是如何到达那里的。有了这些信息，你应该像龙风吸引拖车公园一样被问题。

如果你再次运行程序并检查打印在控制台上的堆栈，你会看到 `Main()` 在列表底部，深度的方法在其上方。堆栈从 `Main()` 开始构建，因此从技术上说，回溯调用栈是向 `Main()` 的。但你应该相反思考：调用者在链中更高。

返回堆栈跟踪之类的极客信息在开发期间运行良好，但你可能希望看到更智能的信息。尽管如此，你可能希望堆栈跟踪写入某个日志文件。

