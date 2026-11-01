
```
Exception: Number should be between 0 and 5. You typed in 10
Thank you
Input a number between 0 and 5 (or just hit return to exit)>hello
An exception was thrown. Message was: input string was not in a correct format.
Thank you
Input a number between 0 and 5 (or just hit return to exit)>
Thank you
```

## 从其他代码捕获异常

前面的示例演示了两种异常的处理。其中一种 IndexOutOfRangeException 是由你自己的代码抛出的。另一种 FormatException 是从某个基类内部抛出的。

如果库代码检测到出现问题，或某个方法因传入了错误的参数而被不恰当地调用，则库代码抛出异常是很常见的。然而，库代码很少尝试捕获异常；这被视为客户端代码的责任。

在调试时，你会经常发现异常是从基类库中抛出的。调试过程在某种程度上涉及确定异常为何被抛出并消除原因。你的目标应该是确保在代码实际发布时，异常只在非常特殊的情况下才会发生，并且如果可能的话，在你的代码中以适当的方式得到处理。

## System.Exception 属性

示例仅说明了异常对象的 Message 属性的使用。然而，System.Exception 中还有许多其他属性，如下表所示。

| 属性 | 描述 |
|---|---|
| Data | 这提供了向异常添加键/值语句的能力，可用于提供有关异常的额外信息。 |
| HelpLink | 这是提供有关异常更多信息的帮助文件的链接。 |
| InnerException | 如果此异常是在 catch 块内部抛出的，则 InnerException 包含导致代码进入该 catch 块的异常对象。 |
| Message | 这是描述错误条件的文本。 |
| Source | 这是导致异常的应用程序或对象的名称。 |
| StackTrace | 这提供了堆栈上的方法调用的详细信息（有助于追踪抛出异常的方法）。 |
| TargetSite | 这是一个 .NET 反射对象，描述抛出异常的方法。 |

这些属性中，如果有堆栈跟踪可用，StackTrace 和 TargetSite 会由 .NET 运行时自动提供。Source 总是由 .NET 运行时填充为引发异常的程序集的名称（尽管你可能希望在代码中修改该属性以提供更具体的信息），而 Data、Message、HelpLink 和 InnerException 必须由抛出异常的代码填充，通过在抛出异常之前立即设置这些属性。例如，抛出异常的代码可能看起来像这样：

```
if (ErrorCondition == true)
{
    Exception myException = new ClassMyException("Help!!!!");
    myException.Source = "My Application Name";
    myException.HelpLink = "MyHelpFile.txt";
    myException.Data["ErrorDate"] = DateTime.Now;
    myException.Data.Add("AdditionalInfo", "Contact Bill from the Blue Team");
    throw myException;
}
```

这里，ClassMyException 是你要抛出的特定异常类的名称。请注意，将所有异常类名称以 Exception 结尾是常见做法。另外，请注意 Data 属性有两种可能的赋值方式。

## 如果异常未被处理会怎样？

有时可能会抛出异常，但你的代码中可能没有能够处理那种异常的 catch 块。SimpleExceptions 示例可以说明这一点。假设，例如，你省略了 FormatException 和捕获所有异常的 catch 块，只提供了捕获 IndexOutOfRangeException 的块。在这种情况下，如果抛出 FormatException 会怎样？

答案是 .NET 运行时会捕获它。本节后面你将学习如何嵌套 try 块，实际上示例背后已经有一个嵌套的 try 块。.NET 运行时实际上已将整个程序放在另一个巨大的 try 块内——它对每个 .NET 程序都这样做。该 try 块有一个可以捕获任何类型异常的 catch 处理程序。如果发生你的代码未处理的异常，执行流程将直接退出你的程序，并被 .NET 运行时中的该 catch 块捕获。然而，这样的结果可能不是你想要的。发生的情况是你的代码执行会立即终止；用户会看到一个对话框，抱怨你的代码未处理异常，并提供 .NET 运行时能够获取的有关异常的任何详细信息。至少异常已被捕获！这就是在第 2 章“Core C#”中 Vector 示例中程序抛出异常时发生的情况。

总的来说，如果你正在编写可执行文件，尽量捕获你合理能够捕获的尽可能多的异常并以合理的方式处理它们。如果你在编写库，通常最好不要处理异常（除非特定异常代表你可以在代码中处理的问题），而是假设调用代码会处理它遇到的任何错误。然而，你可能仍然希望捕获任何 Microsoft 定义的异常，以便你可以抛出自己的异常对象，向客户端代码提供更具体的信息。

## 嵌套 try 块

异常的一个不错特性是你可以将 try 块嵌套在彼此内部，像这样：

```
try
{
    // Point A
    try
    {
        // Point B
    }
    catch
    {
        // Point C
    }
    finally
    {
        // clean up
    }
    // Point D
}
catch
```

## 修改异常类型

当抛出的原始异常不能充分描述问题时，修改异常类型可能很有用。通常发生的情况是某些东西——可能是 .NET 运行时——抛出一个相当低级的异常，说明例如发生了溢出（OverflowException）或传递给方法参数不正确（派生自 ArgumentException 的类）。然而，由于异常发生的上下文，你会知道这揭示了其他一些潜在问题（例如，在代码的该点只能发生溢出，因为你刚刚读取的文件包含不正确的数据）。在这种情况下，你对第一个异常的处理程序最合适的做法是抛出另一个更准确描述问题的异常，以便稍后的另一个 catch 块可以更恰当地处理它。在这种情况下，它还可以通过 System.Exception 实现的属性 InnerException 转发原始异常。InnerException 仅包含对抛出的任何其他相关异常的引用——以防最终的处理程序例程需要此信息。

当然，也存在异常发生在 catch 块内部的情况。例如，你通常会读取包含处理错误详细说明的配置文件，而该文件可能并不存在。

## 在不同位置处理不同的异常

拥有嵌套 try 块的第二个原因是可以在代码的不同位置处理不同类型的异常。一个很好的例子是如果你有一个循环，其中可能发生各种异常条件。其中一些可能严重到需要放弃整个循环，而另一些可能不那么严重，只需要放弃该次迭代并继续下一次循环迭代。你可以通过在循环内部设置一个 try 块来处理较不严重的错误条件，并在循环外部设置一个外部 try 块来处理更严重的错误条件来实现这一点。你将在下一个异常示例中看到其工作原理。

## 用户定义异常类

你现在准备好查看第二个说明异常的示例。这个名为 SolicitColdCall 的示例包含两个嵌套的 try 块，并说明了定义自己的自定义异常类并从 try 块内部抛出另一个异常的做法。

本示例假设一家销售公司希望在销售名单上增加更多客户。公司的销售团队将致电一批人邀请他们成为客户，这在销售术语中称为冷电话。为此，你有一个文本文件可用，其中包含要进行冷电话的人员姓名。该文件应采用格式良好的格式，其中第一行包含文件中的人数，每一行后续行包含下一个人的姓名。换句话说，一个格式正确的人员姓名文件可能看起来像这样：

```
4
George Washington
Benedict Arnold
John Adams
Thomas Jefferson
```

这个版本的冷电话旨在在屏幕上显示人员的姓名（也许供销售人员阅读）。这就是为什么文件中只包含姓名而不包含个人的电话号码。

对于本示例，你的程序将要求用户输入文件名，然后简单地读取它并显示人员的姓名。这听起来像是一项简单的任务，但即便如此，也可能出现一些问题需要你放弃整个过程：

- 用户可能输入一个不存在的文件名。这将被捕获为 FileNotFound 异常。
