
用于执行链的栈的工作方式与食堂托盘栈完全一样。最上面的先取下。第一个添加到栈中的在底部。你在第11章创建了一个栈，当时你被介绍到泛型类。

StringToNumber() 方法将异常抛给了 ParseInt32() 方法。ParseInt32() 是 C# int.Parse() 方法在 .NET 中的等价物。那里没有找到异常处理方法，因此异常随后冒泡到了父方法 Calculate_Click()。CLR 再次在此 Calculate_Click() 方法中查找异常处理程序。由于未找到，它继续将异常冒泡通过 Windows.Forms.Control.OnClick() 方法，等等。堆栈跟踪包括在引发异常时仍处于活动状态的所有方法。由于堆栈跟踪中列出的方法中没有包含处理该类型异常的代码，因此会显示未处理的异常消息。那么，你如何处理异常呢？

## 异常处理技术

首先请记住有 bug、错误和异常。如果导致问题的事件经常发生，最好编写程序语句，使用条件表达式来检查潜在错误并提供当遇到该问题时要做什么的程序指令。这就是你在示例 12-1 中看到列出的内容。如果 CLR 必须暂停一个方法并找到合适的异常处理程序，执行速度会变慢。因此，如果可能导致程序崩溃的情况经常发生，请编写使用条件表达式来处理该情况的程序语句。

异常处理技术用于偶尔发生的严重错误。如前所述，异常是指程序无法从中恢复的事件，例如尝试读取不存在的数据文件。.NET 中包含了一些类，可与你的应用程序一起使用，使其不易崩溃。这些异常类是 .NET 原始设计的一部分，因此集成在框架类库 (FCL) 中。它们以一致、高效的方式促进异常管理。它们与 `try...catch...finally` 程序结构一起使用来处理意外的条件类型。

![](img/e33ae760e23d89eac66541252ad65de8_770_1.png)

认识到使用面向对象方法处理异常的重要性，C# 的开发人员在 FCL 的原始设计中包含了处理异常的规定。类并不是像某些语言中那样事后才添加的。

## Try...Catch...Finally 块

C# 如同 C++、Java 和其他语言一样，通过 `try...catch...finally` 块处理异常。可能导致问题的代码放在 `try` 块中。处理问题（异常处理程序）的代码放在 `catch` 块中，也称为 **catch 子句**。你希望无论是否抛出异常都执行的代码放在 `finally` 块中。`try...catch...finally` 块的语法如下：

```text
try
{
        // Statements
}
catch ([ExceptionClassName exceptionIdentifier])
{
        // Exception handler statements
}
:    // [additional catch clauses]
[finally]
{
        // Statements
}]
```

![](img/e33ae760e23d89eac66541252ad65de8_771_0.png)

`:` 在本书的示例中用于表示可以在程序列表中添加额外的语句。这里，冒号必须被额外的 `catch` 子句替换。

可以包含一个以上的 `catch` 子句。`try` 块必须至少包含一个 `catch` 子句。请注意，关键字 `catch` 后面跟着一个方括号，表示括号和参数列表是可选的。省略参数列表会使 `catch` **通用**——意味着任何抛出的异常都将通过执行该 `catch` 块内的代码来处理。如果你将异常类型作为参数列表的一部分包含在内，只有与所列类型匹配的异常才会被该 `catch` 子句处理。你将在本章后面看到使用多个 `catch` 子句的示例。

`finally` 子句也是可选的。如果有一段无论如何都需要执行的代码，可以包含它。例如，如果你有一个打开的文件或数据库连接，你可以将关闭语句放在 `finally` 块中，以确保文件或连接被正确关闭。当 `try...catch...finally` 结构中的三个块都包含代码时，`try` 块内的语句会首先尝试。如果没有问题且 `try` 块代码已完成，则会跳过 `catch` 子句，并将控制转移到 `finally` 块，在那里执行该代码。

如果在 `try` 块中发生抛出异常的意外错误，`try` 块中的代码会在导致问题的行处停止。CLR 尝试在当前方法内找到匹配的异常处理程序。如果找到一个，控制就会转移到第一个可以处理所抛异常类型的 `catch` 子句。`catch` 子句语句被执行，然后控制转移到 `finally` 块，在那里执行其代码。请注意，在这两种情况（抛出异常和未抛出异常）下，如果包含 `finally` 块，其中的语句都会被执行。

另一个需要确保你理解的重要点是，抛出异常后控制永远不会返回到 *try* 块。*try* 块中导致问题的语句是 *try* 子句中最后尝试的语句。在控制从 *try* 块转移出去后，*try* 块内部的任何其他语句都永远不会被执行。

示例 12-2 使用一个 *try...catch* 块来防止程序异常终止。该示例包含一个通用 *catch* 子句——未列出特定异常类型。

### 示例 12-2

```csharp
// ExceptionApp.cs
// Uses a generic catch block to catch any
// type of exception that is thrown.
using System;
namespace ExceptionsExample
{
    class ExceptionApp
    {
        static void Main(string[] args)
        {
            int[] examScore;
            int totalScores = 0;
            int countOfScores = 0;
            string inValue;
            double averageTestScore;
            try
            {
                Console.Write("How many scores will you enter? ");
                inValue = Console.ReadLine();
                countOfScores = int.Parse(inValue);
                examScore = new int[countOfScores];

                for (int i = 0; i < countOfScores; i++)
                {
                    Console.Write("Enter score {0}: ", i+1);
                    inValue = Console.ReadLine();
                    examScore[i] = int.Parse(inValue);
                    totalScores += examScore[i];
                }

                averageTestScore = totalScores /
                                   countOfScores;
                Console.WriteLine("Average is {0}",
                                   averageTestScore);
            }
catch
{
    Console.WriteLine("Problem with scores - " +
    "Cannot compute average");
}
}
```

如果运行应用程序并且用户输入非数字字符，例如值 9U（在图 12-14 中显示为分数 3 输入），程序不会崩溃。相反，catch 块中发现的异常处理程序代码会被执行并提醒用户错误。

![](img/e33ae760e23d89eac66541252ad65de8_773_0.png)

图 12-14 通用 catch 块处理异常

## 通用捕获

使用通用 catch 来避免异常终止的问题在于，由于任何类型的异常都会被 catch 代码处理，你永远无法完全确定是什么导致了异常被抛出。例如，图 12-15 中显示的两个输出列表。

![](img/e33ae760e23d89eac66541252ad65de8_773_1.png)

图 12-15 因除零和程序员错误而抛出的异常
