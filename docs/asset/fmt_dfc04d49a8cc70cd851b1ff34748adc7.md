
// 等待用户确认。

`Console.WriteLine("Press Enter to terminate...");`

`Console.Read();`

}

}

```

这个“异常”版本的 `Main()` 将其几乎所有内容都包裹在 `try` 块中。`Main()` 结尾的 `catch` 块捕获 `ArgumentException` 对象，并使用其 `ToString()` 方法在一个字符串中显示异常对象包含的大部分错误信息。

我们选择使用 `ArgumentException` 是因为它最准确地描述了问题：向 `Factorial()` 传递了一个不可接受的参数。

![](img/6df7bb88e9302e98442acc219cfbd7fc_213_0.png)

## 了解为什么该示例是异常

上一节中 `Factorial()` 方法的版本包含了与之前版本相同的负数参数检查。（对整数的测试已不再相关，因为我们已经 `Factorial()` 的参数和返回类型更改为 `int`。）如果其参数为负数，`Factorial()` 将无法继续，因此它会格式化一条描述问题的错误消息，包括它发现的违规值。然后 `Factorial()` 将这些信息封装在一个新创建的 `ArgumentException` 对象中，并将其抛回给调用方法。

我们建议在调试器中运行程序，以实时观察异常的发生。（我们在第四卷中会详细介绍关于调试器的信息。）

该程序的输出如下（为了提高可读性，我们修剪了错误消息）：

```
i = 6, factorial = 720

i = 5, factorial = 120

i = 4, factorial = 24

i = 3, factorial = 6

i = 2, factorial = 2

i = 1, factorial = 1

i = 0, factorial = 0

Fatal error:

System.ArgumentException: Illegal negative argument to Factorial -1

  at Factorial(Int32 value) in c:\#programs\Factorial\Program.cs:line 21

  at FactorialException.Program.Main(String[] args) in c:\#programs\Factorial\Program.cs:line 49

Press Enter to terminate...
```

前几行显示了数字 6 到 0 的实际阶乘。尝试计算 −1 的阶乘会产生以 Fatal error 开头的消息——这听起来可不妙。

错误消息的第一行是在 `Factorial()` 内部格式化的。此行描述了问题的性质，包括违规的值 −1。

## 追溯堆栈

输出的其余部分是堆栈跟踪（stack trace）。堆栈跟踪的第一行描述了抛异常的位置。在这种情况下，异常是在 `Factorial(int)` 中抛出的——具体是在源文件 `Program.cs` 的第 21 行。`Factorial()` 在同一文件的第 49 行的 `Main(string[])` 方法中被调用。堆栈跟踪停止于 `Main()`，因为那是捕获异常的模块——堆栈跟踪结束。

你必须承认这个过程令人印象深刻——消息描述了问题并识别了违规参数。堆栈跟踪告诉你异常是在哪里抛出的，以及程序是如何到达那里的。利用这些信息，你应该像龙风卷入拖车场一样找到罪魁祸首。

如果你运行上一个示例并检查打印到控制台的堆栈跟踪，你会在列表底部看到 `Main()`，在上方看到更深的方法。跟踪是从 `Main()` 向上构建的，因此从技术上讲，展开调用堆栈是沿着跟踪向下到 `Main()`。不过，你应该反过来考虑：调用者在调用链中的位置更高（参见图 9-1）。

返回像堆栈跟踪这样的极客信息在开发期间运行得很好，但你可能更希望真实用户看到更易于理解的信息。尽管如此，你可能仍然想将堆栈跟踪写入某处的日志文件中。

我在在本章前面描述的 `Factorial()` 版本使用了非递归算法，该算法使用循环计算阶乘。对于递归版本，请参网页上的 `RecursiveFactorial` 示例。递归方法调用自己，可能会反复调用直到出现停止条件。递归的 `Factorial()` 重复调用自己（递归），当传入的值变为负数时停止。递归是实现 `Factorial()` 最常见的方法。注意：确保递归会停止。

## 分配多个 catch 块

我们在在本章早些时候提到，你可以定义自己的异常。假设你定义了一个 `CustomException` 类（我们在文章“创建你的异常”中描述了这一点）。现在考虑这里使用的 `catch` 子句：

```cs
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

如果 `SomeOtherMethod()` 抛出了 `Exception` 会怎样？它会跳过 `catch(CustomException)`，因为 `Exception` 不是 `CustomException` 的类型。它会被下一个 `catch` 子句捕获：`catch(Exception)`。

不要对我使用“许多”这个词感到惊讶。在实践中，你不会使用许多 `catch` 块。

![](img/6df7bb88e9302e98442acc219cfbd7fc_216_0.png)

不同类型的多个 `catch` 子句必须在 `try` 块之后尾尾相齐。C# 按顺序检查每个 `catch` 块，将抛出的对象与 `catch` 子句的参数进行比较，如这段代码所示：

![](img/6df7bb88e9302e98442acc219cfbd7fc_216_1.png)

```cs
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(CustomException ce)  // 最具体的异常类型
    {
        // 所有的 CustomException 对象在这里被捕获。
    } // 你可以在这里插入其他异常类型。
    catch(Exception e)          // 最通用的异常类型
    {
        // 所有其他未捕获的异常在这里被捕获。
        // 并不是说你总是这样做——但在合理的情况下。
    }
}
```

如果 `SomeOtherMethod()` 抛出一个 `Exception` 对象，它会跳过 `catch(CustomException)`，因为 `Exception` 不是 `CustomException` 的类型。它会被下一个 `catch` 子句捕获：`catch(Exception)`。

![](img/6df7bb88e9302e98442acc219cfbd7fc_216_2.png)

始终按 `catch` 子句从最具体的到最通用的排列。永远将更通用的 `catch` 子句放在前面，就像这段相当糟糕的代码：

```cs
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(Exception e)  // 最通用的在前——不妙！
    {
        // 所有异常在这里被捕获。
        // 澳洲袋鼠吃了一切。
    }
    catch(CustomException ce)
}
```

```cs
{
    // No exception ever gets this far, because it's
    // caught and consumed by the more general catch clause.
}
```

更通用的 catch 子句会通过拦截任何 throw 导致紧随其后的 catch 子句无法执行（饥饿）。编译器会提示你这个错误。

任何继承自 `CustomException` 的类都是一个 `CustomException`：

```cs
class MySpecialException : CustomException
{
    // . . . whatever . . .
}
```

如果有机会，`CustomException` 的 catch 捕获 `MySpecialException` 对象就像就像青蛙捕食苍蝇一样。

# 规划你的异常处理策略

为程序如何处理错误制定一个计划是有意义的。选择异常而不是错误代码只是你所需要做出的选择之一。

由于空间限制，我无法完全探讨你在响应异常时所拥的所有选项。这个概述——一套指南和一些关键技术——应该让你有一个良好的方向。请参考 http://csharp102.info 上的文章，以深入探讨“当代码抛出异常时我能做什么？”这一基础问题。

# 引导你规划的一些问题

在开发程序时，脑海中应该有几个问题：

- +♦ 可能会出现什么问题？针对你编写的每一段代码都问这个问题。
- +♦ 如果真的出问题了，我可以修复它吗？如果是，你可能可以从问题中恢复，程序也可以继续运行。如果不能，你可能需要收拾行李离开这个城市了。
- +♦ 问题是否会给用户数据带来风险？如果是，你必须竭尽全力防止这些数据丢失或损坏。明知发布会毁坏用户数据的代码等同于软件执业事故。
- +♦ 我应该把针对此问题的异常处理程序放在哪里？在异常发生的方法中尝试处理可能不是最佳方法。通常，方法调用链中更高处的另一个方法拥有更好的信息，并可能对异常进行更智能、更有用的处理。将 `try/catch` 放在那里，使 `try` 块包围通往可能发生异常处的调用。
- +♦ **我应该处理哪些异常？** 捕获任何你可以通过某种方式恢复的异常。努力找到恢复的方法，正如 http://csharp102.info 上的“响应异常”文章中所讨论的那样。然后，在开发和测试期间，未处理的异常将到达程序的顶端。在将程序发布给真实用户之前，修复任何未处理异常的根本原因——如果可以的话。但有时，某些异常*应该*要求提前终止程序，因为情况已经变得无无可挽回了。
- +♦ **那些溜过缝隙并避开我处理程序的异常怎么办？** 本章稍后的“抓住捕获异常的最后机会”部分描述了提供一个“最后机会”异常处理程序来捕获遗漏的异常。
- +♦ **我的代码需要多健壮（不可破坏）？** 如果你的代码运行的是航空交通控制系统，它确实应该非常健壮。如果它只是一个小型一次性工具，你可以稍微放宽。

# 良好处理错误的代码指南

在工作时，你应该记住上一节中的问题。这些指南也可能有所帮助：

- +♦ **不惜代价保护用户数据。** 这是最重要的准则。参见本章末尾的“更多信息”侧栏。另参见下一个项目符号。
- +♦ **不要崩溃。** 如果可以，请恢复，但要准备好尽可能优雅地退出。不要让你的程序只发出一个晦涩的、极客的消息就完蛋了。*优雅地*意味着在关闭之前提供包含尽可能有用信息的清晰消息。用户真的很恨崩溃。但你可能已经知道了。
- +♦ **如果你无法从问题中恢复，就不要让程序继续运行。** 程序可能会变得不稳定，或者用户数据可能处于不一致的状态。当大局已定时时，你可以显示一条消息并调用 `System.Environment.FailFast()` 来立即终止程序，而不是抛出异常。这不是崩溃——而是故意为之。
- +♦ **区别对待类库和应用程序。** 在*类库*中，让异常传递给调用者，调用者最适合决定如何处理问题。不要让调用者对问题一无知。但在*应用程序*中，处理任何你可以处理的异常。

整个程序读取 .CS 文件。然后它会逐行处理这些文件，将每一行传递给 `FixNamespaceLine()` 方法。给定一行代码，该方法调用 `String.IndexOf()` 来查找命名空间名称的索引（通常为 10）。然后它调用 `GetNameStartAfterNamespaceKeyword()` 来定位命名空间名称的起始位置。最后，它调用另一个方法 `PlugInNamespaceCompanyQualifier()`，将公司名称插入到行中的正确位置，然后返回该行。大部分工作是由子方法完成的。

首先，即使不知道这段代码的用途或那两个被调用的方法是什么，也请考虑输入内容。对于 `line` 参数，调用 `String.IndexOf()` 时至少存在一个问题。如果 `line` 为 `null`，`IndexOf()` 调用将导致 `ArgumentNullException`。你不能在 `null` 对象上调用方法。此外，乍一看，在空字符串上调用 `IndexOf()` 会有效吗？结果证明是有效的，因此那里不会发生异常，但如果你将一个空行传递给那些名称很长的方法，会发生什么呢？我们建议在必要的情况下，在 `FixNamespaceLine()` 的第一行代码之前添加一个守卫语句（guard clause）——至少检查是否为 `null`：

```
if(String.IsNullOrEmpty(name))  // 一个方便的字符串方法
{
    return name; // 你可以返回一个合理的返回值
                // 而不是抛出异常。
}
```

其次，在你安全地通过了 `IndexOf()` 调用后，两个方法调用之一仍然可能抛出异常，即使 `line` 经过了仔细检查。如果 `spaceIndex` Result为 -1（未找到）——这可能是因为传递的行通常不包含命名空间关键字——将其传递给第一个方法可能会有问题。你可以对这种结果进行防护，如下：

```
if(spaceIndex > -1) ...
```
