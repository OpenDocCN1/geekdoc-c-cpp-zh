
```cs
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

### 过滤异常

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

此示例根据 `catchErrors` 布尔变量的值来捕获所有异常（`Exception` 类型）。如果该变量为 false，则不会发生异常，并将使用应用程序的默认异常处理机制。如果 `catchErrors` 为 true，则运行 catch 块中的代码来处理异常。

在接下来的练习中，你将看到当应用程序抛出未处理的异常时会发生什么，并将编写一个 try 块来捕获并处理异常。

### 观察应用程序如何报告未处理的异常

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

### 编写 try/catch 语句块

- 1. 返回到 Visual Studio 2022。
- 2. 在调试菜单上，选择“启动调试”（Start Debugging）。

> 注意
> 这一次，请确保你是在调试模式下运行应用程序。
- 3. 当表单出现时，在左侧操作数框中输入 John，在右侧操作数框中输入 2。
- 4. 选择 + 加法按钮，然后选择“计算”（Calculate）。

此输入应该导致与上一个练习中发生相同的异常，只是现在你正在调试模式下运行，所以 Visual Studio 捕获了异常并报告了它。

Visual Studio 显示了你的代码并突出显示了导致异常的语句。它还显示了一个描述异常的对话框，在这种情况下是“字符串格式不正确”。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_267_0.png)

你可以看到，`addValues` 方法内部调用 `int.Parse` 时抛出了 `FormatException`。问题是该方法无法将文本 John 解析为有效的数字。
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

不包含必要的 try/catch 处理。你很快就会修复这个问题。

+   16. 在“调试”（Debug）菜单上，选择“停止调试”。

# 传播异常

在 `addValues` 方法中添加 try/catch 块使得该方法变得非常健壮，但你还需要对其他方法应用相同的异常处理：`subtractValues`、`multiplyValues`、`divideValues` 和 `remainderValues`。这些异常处理程序的代码可能非常相似，导致你需要在每个方法中编写这些代码。

当用户选择“计算”（Calculate）按钮时，`calculateClick` 方法会调用这些方法中的每一个。因此，为了避免异常处理代码的重复，将其移动到 `calculateClick` 方法中是有意义的如果在`subtractValues`、`multiplyValues`、`divideValues` 或 `remainderValues` 方法中发生 `FormatException`，它将传播到 `calculateClick` 方法进行处理，正如本章前面的“未处理的异常”节所述。

### 将异常传回给调用者方法

+   1. 在代码和文本编辑器窗口中显示 `MainPage.xaml.cs` 文件的代码，并找到 `addValues` 方法。

+   2. 从 `addValues` 方法中移除 try 块 catch 处理器并恢复其原始状态，如下代码所示：

点击此处查看代码图像

```
private void addValues()
{
    int leftHandSide = int.Parse(lhsOperand.Text);
    int rightHandSide = int.Parse(rhsOperand.Text);
    int outcome = 0;
    outcome = lhs + rhs;
    expression.Text = lhsOperand.Text + " + " + rhsOperand.Text;
    result.Text = outcome.ToString();
}
```

+   3. 找到 `calculateClick` 方法。将此方法添加到下方示例中加粗显示的 try 块和 catch 处理器中：

点击此处查看代码图像

```
private void calculateClick(object sender, RoutedEventArgs e)
{
    try {
        if ((bool)addition.IsChecked)
        {
            addValues();
        }
        else if ((bool)subtraction.IsChecked)
        {
            subtractValues();
        }
        else if ((bool)multiplication.IsChecked)
        {
            multiplyValues();
        }
        else if ((bool)division.IsChecked)
        {
            divideValues();
        }
        else if ((bool)remainder.IsChecked)
        {
            remainderValues();
        }
    } catch (FormatException fEx)
    {
        result.Text = fEx.Message;
    }
}
```

+   4. 在**调试**(Debug）菜单上，选择**开始调试**(Start Debugging）。
5. 当表单出现时，在**左操作数**(Left Operand）框中输入**John**，在**右操作数**(Right Operand）框中输入**2**。
6. 选择**+ 加法**(+ Addition）按钮，然后选择**计算**(Calculate）。

和之前一样，`catch` 处理器成功捕获了 `FormatException`，并将消息“输入字符串不是正确的格式”写入结果（Result）框。然而，尽管异常是在 `addValues` 方法中抛出的，处理器在 `calculateClick` 方法中捕获了它。

+   7. 选择 – **减法**(Subtraction）按钮，然后选择**计算..**(Calculate..）。

这次，`subtractValues` 方法导致了异常，但它被传回 `calculateClick` 方法并以之前一样的方式进行处理。

+   8. 选择**乘法 / 除法 以及 % 余数**(Multiplication / Division , % Remainder）按钮，验证 `FormatException` 异常被正确捕获并处理。

+   9. 返回 Visual Studio 并停止调试。

> 注意
是否在方法中显式捕获未处理的异常，取决于你正在构建的应用程序的性质。在某些情况下，尽可能在异常发生的地方捕获异常是有意义的。在其他情况下，让异常传回调用抛出异常的例程的方法并处理错误更有用。

# 使用 checked 和 unchecked 整数算术

第 2 章讨论了如何使用诸如 `+` 等二进制算术运算符应用于 `int` 和 `double` 等基本数据类型。你还应该记得基本数据类型具有固定的大小。例如，C# 中的 `int` 是 32 位的。因为 `int` 有固定的大小，你确切地知道它可以容纳的值范围：2147483648 到 2147483647。

> 提示
如果你想在代码中引用 `int` 的最小值或最大值，可以使用 `int.MinValue` 或 `int.MaxValue` 属性。

`int` 的固定大小创建了一个问题。例如，如果给一个当前值为 2147483647 的 `int` 加 1 会发生什么？答案取决于应用程序是如何编译的。默认情况下，C# 编译器生成的代码允许计算静默溢出，你将得到一个错误的答案。（事实上，计算会回绕到最大的负整数值，生成的的结果为 -2147483648。） 这种行为的原因是性能考虑：整数算术是几乎每个程序中的常用操作，为每个整数表达式添加溢出检查的开销会导致性能非常糟糕。在许多情况下，这种风险是可以接受的，因为你知道（或希望！）你的 `int` 值不会达到它们的限制。如果你不喜欢这种方法，可以开启溢出检查。

> > 提示
你可以在 Visual Studio 2022 中通过设置项目属性来开启和关闭溢出检查。在解决方案管理器中，选择 YourProject（YourProject 是项目的实际名称）。在项目菜单上，选择 YourProject 属性。在项目属性对话框中，选择生成（Build）选项卡。选择页面右下角的高级（Advanced）按钮。最后，在高级设置对话框中，勾选或清除算术溢出/不足（For Arithmetic Overflow/Underflow）复选框。

### 编写 checked 语句

checked 语句是以 checked 关键字开头的块。checked 语句中的所有整数算术如果块中的整数计算溢出，始终会抛出 `OverflowException`，例所示：

点击此处查看图像

```
int number = int.MaxValue;
checked{
    int intWillThrow = number++;
    Console.WriteLine("这不会到达这里");
}
```

> > 重要
只有直接位于 checked 内部的整数算术受溢出检查的影响。例如，如果 checked 语句之一是方法调用，则检查不适用于被调用的方法。

你也可以使用 `unchecked` 关键字来创建一个 unchecked 块。unchecked 块中的所有整数算术永远不会抛出 `OverflowException`。例如：

```
int number = int.MaxValue;
unchecked
{
    int intWillThrow = number++;
    Console.WriteLine("这会到达这里");
}
```

### 编写 checked 表达式

你也可以使用 checked 和 unchecked 关键字，通过在括号表达式的前面加上 checked 或 unchecked 关键字来控制整数表达式的溢出检查，如下示例所示：

点击此处查看图像

```
int wontThrow = unchecked(int.MaxValue + 1);
int willThrow = checked(int.MaxValue + 1);
```
