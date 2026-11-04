
该程序的输出如下（为了更易读，我们删减了错误消息）：

```
i = 6, factorial = 720
i = 5, factorial = 120
i = 4, factorial = 24
i = 3, factorial = 6
i = 2, factorial = 2
i = 1, factorial = 1
i = 0, factorial = 0
Fatal error: System.ArgumentException: Illegal negative argument to Factorial -1
   at Factorial(Int32 value) in c:\programs\Factorial\Program.cs:line 21
   at FactorialException.Program.Main(String[] args) in c:\programs\Factorial\Program.cs:line 49
Press Enter to terminate...
```

前几行显示数字 6 到 0 的实际阶乘。尝试计算 –1 的阶乘会生成以 Fatal error 开头的消息——这听起来可不妙。

错误消息的第一行是在 Factorial() 内部格式化出来的。这一行描述了问题的性质，包括出错的 –1 值。

## 跟踪堆栈

输出的其余部分是堆栈跟踪。堆栈跟踪的第一行描述了异常是在哪里抛出的。在本例中，异常是在 Factorial(int) 中抛出的——更具体地说，是在源文件 Program.cs 的第 21 行。Factorial() 是在同一文件的第 49 行的 Main(string[] args) 方法中被调用的。堆栈跟踪止于 Main()，因为那正是捕获异常的模块——堆栈跟踪到此结束。

你不得不承认，这个过程令人印象深刻——消息描述了问题并指出了出错的参数。堆栈跟踪告诉你异常是在哪里抛出的，以及程序是如何到达那里的。利用这些信息，你应该会像龙卷风被拖车停车场吸引一样，被吸引到问题所在。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_220_0.png)

如果你运行前面的示例并检查它打印到控制台的堆栈跟踪，你会看到 Main() 位于列表的*底部*，而更深层的方法在它上面。跟踪从 Main() 向上构建，所以从技术上说，展开调用堆栈是沿着跟踪向*下*走向 Main()。不过，你应该反过来想：调用者在调用链中位置更高（参见图 9-1）。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_220_1.png)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_221_0.png)

我在本章前面描述的 Factorial() 版本使用非递归算法，该算法用循环来计算阶乘。关于递归版本，请参见 Web 上的 RecursiveFactorial 示例。递归方法会调用自身，可能反复调用，直到出现停止条件。递归的 Factorial() 会反复调用自身（递归），当传入的值变为负数时停止。递归是实现 Factorial() 最常见的方式。注意：确保递归会停止。你可以将 RecursiveFactorial 的结果与不那么奇特的 NonrecursiveFactorial 示例的结果进行比较，而 DeadlyRecursion 示例展示了递归不停止时会发生什么——它会导致相当令人不快的 StackOverflowException。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_221_1.png)

当程序在调试器中运行时，堆栈跟踪可在某个 Visual Studio 调试器窗口中获得。

## 使用多个 catch 块

我在本章前面提到，你可以定义自己的自定义异常类型。假设你定义了一个 CustomException 类。（我在文章“Creating Your Own Exception Class”中描述了这个过程，你可以在 csharp102.info 上找到它。）现在考虑这里使用的 catch 子句：

```
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(CustomException ce)
    {
    }
}
```

如果 SomeOtherMethod() 抛出了一个简单的 Exception 或另一种非 CustomException 类型的异常，会怎么样？那就像试图用棒球手套接橄榄球一样——捕获与抛出不相匹配。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_221_2.png)

幸运的是，C# 使程序能够定义多个 catch 子句，每个子句针对不同类型的异常。假设这里是处理其他异常的正确位置，你可以一个接一个地加上去。

不要因为我用了“多个”这个词就感到惊慌。在实践中，你不会在一个地方使用很多 catch 块。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_221_3.png)

针对不同异常类型的多个 catch 子句必须在 try 块之后首尾相接地排列。C# 会依次检查每个 catch 块，将抛出的对象与 catch 子句的参数类型进行比较，如下面这段代码所示：

```
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(CustomException ce) // Most specific exception type
    {
        // All CustomException objects are caught here.
        // You could insert other exception types between these two.
    }
    catch(Exception e) // Most general exception type
    {
        // All otherwise uncaught exceptions are caught here.
        // Not that you should always do so -- but when it makes sense ...
    }
}
```

如果 SomeOtherMethod() 抛出一个 Exception 对象，它会跳过 catch(CustomException)，因为 Exception 不是 CustomException 类型。它会被下一个 catch 子句捕获：catch(Exception)。

始终按从最具体到最一般的顺序排列 catch 子句。永远不要把更一般的 catch 子句放在前面，如下面这段相当糟糕的代码所示：

```
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(Exception e) // Most general first -- not good!
    {
        // All exceptions are caught here.
        // The dingo ate everything.
    }
    catch(CustomException ce)
    {
        // No exception ever gets this far, because it's
        // caught and consumed by the more general catch clause.
    }
}
```

更一般的 catch 子句会拦截任何抛出，从而使后面的 catch 子句得不到异常。编译器会提醒你这个错误。

任何继承 CustomException 的类都是 CustomException：

```
class MySpecialException : CustomException
{
    // . . . whatever . . .
}
```

只要有机会，CustomException 的 catch 就会抓住 MySpecialException 对象，就像青蛙捕捉苍蝇一样。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_222_0.png)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_222_1.png)

- **在大多数情况下，不要在特定方法中捕获异常，除非你能以有用的方式处理它们，最好是能从错误中恢复。** 捕获一个你无法处理的异常就像徒手抓黄蜂。然后呢？大多数方法不包含异常处理程序。

- **彻底测试你的代码**，尤其是你能想到的任何一类错误输入。你的方法能处理负输入吗？零？非常大的值？空字符串？null 值？用户可能做什么来导致异常？你的代码使用了哪些可能出错的资源，比如文件、数据库或 URL？参见前面两个项目符号段落。了解如何为你的代码编写单元测试。这相当容易，而且很有趣。

- **捕获你能捕获的最具体的异常。** 不要为 Exception 或 ApplicationException 这类高级异常类编写很多 catch 块。你可能会使调用链上更高层的处理程序得不到异常。

- **始终在 Main() 中放一个最后机会异常处理程序块**——或者放在你程序的“顶层”所在之处（可重用类库除外）。你可以在此块中捕获 Exception 类型。捕获并处理你能处理的异常，让最后机会异常处理程序收拾任何漏网之鱼。（我们在后面的“抓住捕获异常的最后机会”一节中解释最后机会处理程序。）

- **不要把异常作为正常执行流程的一部分。** 例如，不要用抛出异常的方式跳出循环或退出方法。

- **如果自定义异常类能带来好处，就考虑编写自己的自定义异常类**——比如提供更多有助于调试的信息，或为用户提供更有意义的错误消息。我们在 csharp102.info 上的一篇文章中介绍自定义异常。

本章其余部分（以及 csharp102.info 上的文章）为你提供了遵循这些准则所需的工具。有关更多信息，请在帮助系统中查找异常处理、设计准则，但要做好阅读一些技术内容的准备。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_225_0.png)

如果一个公共方法抛出了调用方可能需要捕获的任何异常，这些异常就是你类公共接口的一部分。你需要记录它们，最好使用第 IV 部分中讨论的 XML 文档注释。

## 如何分析一个方法可能抛出的异常

在下面的方法中——这是设置异常处理程序的第一步——考虑它能抛出哪些异常：
