
所有异常的祖父。如果你捕获 `Exception`，处理程序将捕获所有可能发生的异常。

> 注意
> 该体系包含许多类型的异常，其中许多是为 .NET 的各个部分设计的。虽然某些异常相当晦涩，但了解如何捕获它们仍然很有用。

下一个示例展示了如何捕获所有可能的异常：

点击此处查看代码图片

```cs
try
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int answer = doCalculation(leftHandSide, rightHandSide);
    result.Text = answer.ToString();
}
catch (Exception ex) // 这是一个通用的 catch 处理器
{
    //...
}
```

> 注意
> 如果你想捕获 `Exception`，你实际上可以从 catch 处理器中省略它的名称，因为它是默认异常：

```cs
catch
{
    // ...
}
```

然而，并不建议这样做。传递给 catch 处理器的异常对象可以包含有关该异常的有用信息，而在使用这种形式的 catch 结构时，这些信息很难被访问。

此时你应该问的最后一个问题是：如果同一个异常在 try 块末尾匹配到多个 catch 处理器会发生什么？例如，如果你在两个不同的处理器中捕获了 `FormatException` 和 `Exception`，哪一个会运行？（或者两者都会执行吗？）

当异常发生时，运行时将使用匹配该异常的第一个处理器，其他处理器将被忽略。因此，如果你将 `Exception` 处理器放在 `FormatException` 处理器之前，那么 `FormatException` 处理器将永远不会运行。因此，你应该在 try 块之后，将更具体的 catch 处理器放在通用 catch 处理器上方。如果某个特定的 catch 处理器匹配了异常，则该 catch 处理器将获胜。

## 过滤异常

你可以对与 catch 处理器匹配的异常进行过滤，以确保在满足额外条件时才触发 catch 处理器。这些条件以 `when` 关键字前缀的布尔表达式形式存在。此示例说明了语法：

点击此处查看代码图片

```cs
bool catchErrors = ...;
try {
  ...
}
catch (Exception ex) when (catchErrors == true) {
  // 只有当 catchErrors 变量为 true 时才处理异常
}
```

此示例根据 `catchErrors` 布尔变量的值来捕获所有异常（Exception 类型）。如果该变量为 false，则不会发生异常，并将使用应用程序的默认异常处理机制。如果 `catchErrors` 为 true，则运行 catch 块中的代码来处理异常。

在接下来的练习中，你将看到当应用程序抛出未处理的异常时会发生什么，并将编写一个 try 块来捕获并处理异常。

## 观察应用程序如何报告未处理的异常

- 1. 启动 Visual Studio 2022（如果它尚未运行）。
- 2. 打开 MathOperators 解决方案，它位于你文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 6\MathOperators` 文件夹中。

这是第 2 章“使用变量、运算符和表达式”中的程序版本，它演示了不同的算术运算符。
- 3. 在调试菜单上，选择“无调试启动”（Start Without Debugging）。

> 注意
> 对于此练习，请确保你实际上是在没有调试的情况下运行应用程序。

表单出现。现在你将在左侧操作数（Left Operand）框中输入一些文本，这将导致异常。此操作将演示该程序当前版本缺乏健壮性。
- 4. 在左侧操作数框中选择 John，在右侧操作数框中输入 2。
- 5. 选择 - + 加法按钮，然后选择“计算”（Calculate）。

此输入触发了 Windows 默认异常处理。应用程序直接终止，你返回到桌面，而没有任何关于哪里错误的任何说明！

现在你已经看到了应用程序在发生未处理的异常时的行为，下一步是通过处理无效输入并防止未处理异常的产生来使应用程序更加健壮。

## 编写 try/catch 语句块

- 1. 返回到 Visual Studio 2022。
- 2. 在调试菜单上，选择“启动调试”（Start Debugging）。

> 注意
> 这一次，请确保你是在调试模式下运行应用程序。
- 3. 当表单出现时，在左侧操作数框中输入 John，在右侧操作数框中输入 2。
- 4. 选择 + 加法按钮，然后选择“计算”（Calculate）。

此输入应该导致与上一个练习中发生相同的异常，只是现在你正在调试模式下运行，所以 Visual Studio 捕获了异常并报告了它。

Visual Studio 显示了你的代码并突出显示了导致异常的语句。它还显示了一个描述异常的对话框，在这种情况下是“字符串格式不正确”。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_267_0.png)

你可以看到，addValues 方法内部调用 `int.Parse` 时抛出了 `FormatException`。问题是该方法无法将文本 John 解析为有效的数字。
- 5. 在异常对话框中，选择“查看详细信息”（View Details）。

打开 QuickWatch 对话框，你可以在其中查看异常的更多详细信息。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_268_0.png)

> 提示
> 异常是之前提出的其他异常的结果。Visual Studio 报告的异常只是链中的最后一个异常，但通常是早期的异常突出了问题。
> 你可以查看 `InnerException` 属性来深入这些早期的异常，直到找到 `InnerException` 属性为 null 的异常（如之前的图像所示）。此时你找到了初始异常，该异常就是你需要解决的问题。
- 6. 在 QuickWatch 对话框中选择“关闭”（Close）。
- 7. 在 Visual Studio 中，在调试菜单上选择“停止调试”（Stop Debugging）。
- 8. 在代码编辑器中显示 `MainPage.cs` 文件，并找到 `addValues` 方法。
- 9. 在方法内部添加 try 块（包括括号），以及针对 `FormatException` 异常的 catch 处理器，如下所示：

点击此处查看代码图片

```cs
try
{
  int lhs = int.Parse(lhsOperand.Text);
  int rhs = int.Parse(rhsOperand.Text);
  int outcome = 0;

  outcome = lhs + rhs;
  expression.Text = $"{lhs} + {rhs}";
  result.Text = outcome.ToString();
}
catch (FormatException fex)
{
  result.Text = fex.Message;
}
```

现在，如果发生 `FormatException` 异常，catch 处理器会将表单底部 Result 框中的异常 Message 属性显示。应用程序现在健壮了一些。

- 10. 在调试菜单上，选择“启动调试”（Start Debugging）。
- 11. 当表单出现时，在左侧操作数框中输入 John，在右侧操作数框输入 2。
- 12. 选择 + 加法按钮，然后选择“计算”（Calculate）。

catch 处理器成功捕获了 `FormatException`，并将“字符串格式不正确”写入 Result 框。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_270_0.png)
- 13. 在左侧操作数框中，将 John 替换为数字 10。在右侧操作数框中输入 Sharp。然后选择“计算”（Calculate）。
try 块阻止了解析两个框的语句，因此同一个异常处理器处理了两个框的用户输入错误。
- 14. 在右侧操作数框中，将 Sharp 替换为 20，选择 + 加法按钮，然后选择“计算”（Calculate）。
应用程序现在按预期工作，并在 Result 框中显示值 30。
- 15. 在左侧操作数框中，将 10 替换为 John，选择 – 减法按钮，然后选择“计算”（Calculate）。
Visual Studio 进入调试状态并再次报告 `FormatException` 异常。这次错误发生在 `subtractValues` 方法中，该
