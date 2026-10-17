
如果表达式 `leftHandSide.Year < rightHandSide.Year` 为真，则 `leftHandSide` 中的日期必须早于 `rightHandSide` 中的日期，因此程序将 `result` 变量设为 `-1`。否则，如果表达式 `leftHandSide.Year > rightHandSide.Year` 为真，则 `leftHandSide` 中的日期必须晚于 `rightHandSide` 中的日期，程序将 `result` 变量设为 `1`。

如果表达式 `leftHandSide.Year < rightHandSide.Year` 为假且表达式 `leftHandSide.Year > rightHandSide.Year` 也为假，则两个日期的 `Year` 属性必须相同，因此程序需要比较每个日期中的月份。

## 11. 将以下以粗体显示的语句添加到 `dateCompare` 方法的主体中。在前一步输入的代码之后输入它们：

Click here to view code image

```
private int dateCompare(DateTime leftHandSide, DateTime rightHandSide)
{
    ...
    else if (leftHandSide.Month < rightHandSide.Month)
    {
        result = -1;
    }
    else if (leftHandSide.Month > rightHandSide.Month)
    {
        result = 1;
    }
}
```

这些语句比较月份，其逻辑与前一步中比较年份时使用的逻辑相似。

如果表达式 `leftHandSide.Month < rightHandSide.Month` 为假且表达式 `leftHandSide.Month > rightHandSide.Month` 也为假，则两个日期的 `Month` 属性必须相同，因此程序最终需要比较每个日期中的日。

## 12. 在前两步输入的代码之后，将以下语句添加到 `dateCompare` 方法的主体中：

Click here to view code image

```
private int dateCompare(DateTime leftHandSide, DateTime rightHandSide)
{
    ...
    else if (leftHandSide.Day < rightHandSide.Day)
    {
        result = -1;
    }
    else if (leftHandSide.Day > rightHandSide.Day)
    {
        result = 1;
    }
    else
    {
        result = 0;
    }

    return result;
}
```

到现在你应该能认识到这种逻辑的模式。

如果 `leftHandSide.Day < rightHandSide.Day` 和 `leftHandSide.Day > rightHandSide.Day` 均为假，则两个变量中 `Day` 属性的值必须相同。`Month` 值和 `Year` 值也必须分别相同，才能使程序逻辑到达此点，因此两个日期必须相同，程序将 `result` 的值设为 `0`。

最后一条语句返回 `result` 变量中存储的值。

- 13. 在 `Debug` 菜单上，单击 `Start Debugging`。

应用程序将被重建并运行。

- 14. 单击 `Compare`。

以下文本出现在文本框中：

Click here to view code image

```
firstDate == secondDate : True
firstDate != secondDate : False
firstDate <  secondDate: False
firstDate <= secondDate: True
firstDate >  secondDate: False
firstDate >= secondDate: True
```

这些是相同日期的正确结果。

- 15. 使用 `DatePicker` 控件为第二个日期选择一个更晚的日期，然后单击 `Compare`。

以下文本出现在文本框中：

Click here to view code image

```
firstDate == secondDate: False
firstDate != secondDate: True
firstDate <  secondDate: True
firstDate <= secondDate: True
firstDate >  secondDate: False
firstDate >= secondDate: False
```

同样，这些是第一个日期早于第二个日期时的正确结果。

16. 测试一些其他日期，并验证结果是否符合你的预期。完成测试后返回 `Visual Studio 2015` 并停止调试。

### 在实际应用中比较日期

现在你已经看到了如何使用相当长且复杂的 `if` 和 `else` 语句序列，我应该提到，这并不是你在实际应用中比较日期时采用的技术。如果查看前一个练习中的 `dateCompare` 方法，你会看到两个参数 `leftHandSide` 和 `rightHandSide` 都是 `DateTime` 值。你编写的逻辑仅比较这些参数的日期部分，但它们还包含你未考虑（或未显示）的 时间元素。要使两个 `DateTime` 值被视为相等，它们不仅应具有相同的日期，还应具有相同的时间。比较日期和时间是如此常见的操作，以至于 `DateTime` 类型实际上有一个内置的方法 `Compare` 来执行此操作：它接受两个 `DateTime` 参数并比较它们，返回一个值，指示第一个参数是否小于第二个参数，在这种情况下结果为负；第一个参数是否大于第二个参数，在这种情况下结果为正；或两个参数是否代表相同的日期和时间，在这种情况下结果为 `0`。

### 使用 switch 语句

有时当你编写级联 `if` 语句时，每个 `if` 语句看起来相似，因为它们都评估相同的表达式。唯一的区别是每个 `if` 将表达式的结果与不同的值进行比较。例如，考虑以下使用 `if` 语句检查 `day` 变量中的值并确定它是星期几的代码块：

```
if (day == 0)
{
    dayName = "Sunday";
}
else if (day == 1)
{
    dayName = "Monday";
}
else if (day == 2)
{
    dayName = "Tuesday";
}
else if (day == 3)
{
    ...
}
else
{
    dayName = "Unknown";
}
```

在这些情况下，通常可以将级联 `if` 语句重写为 `switch` 语句，以使程序更高效、更易读。

### 理解 switch 语句语法

`switch` 语句的语法如下（`switch`、`case` 和 `default` 是关键字）：

Click here to view code image

```
switch ( controllingExpression )
{
    case constantExpression :
        statements
        break;
    case constantExpression :
        statements
        break;
    ...
    default :
        statements
        break;
}
```

`controllingExpression` 必须用括号括起来，只会被评估一次。然后控制跳转到由 `constantExpression` 标识的代码块，该 `constantExpression` 的值等于 `controllingExpression` 的结果。`constantExpression` 标识符也称为 `case` 标签。执行一直运行到 `break` 语句，在此点 `switch` 语句结束，程序继续执行 `switch` 语句闭合大括号之后的第一条语句。如果没有任何 `constantExpression` 值等于 `controllingExpression` 的值，则在可选的 `default` 标签下方的语句会运行。

# Note

每个 `constantExpression` 值必须是唯一的，这样 `controllingExpression` 将只匹配其中一个。如果 `controllingExpression` 的值与任何 `constantExpression` 值都不匹配并且没有 `default` 标签，程序执行将继续执行 `switch` 语句闭合大括号之后的第一条语句。

因此，你可以将之前的级联 `if` 语句重写为以下 `switch` 语句：

```
switch (day)
{
    case 0 :
        dayName = "Sunday";
        break;
    case 1 :
        dayName = "Monday";
        break;
    case 2 :
        dayName = "Tuesday";
        break;
    ...
    default :
        dayName = "Unknown";
        break;
}
```

### Following the *switch* statement rules

`switch` 语句非常有用，但不幸的是，你不能总是在你想使用它的时候使用它。你编写的任何 `switch` 语句都必须遵守以下规则：

- 你只能对某些数据类型使用 `switch`，例如 `int`、`char` 或 `string`。对于其他任何类型（包括 `float` 和 `double`），你必须使用 `if` 语句。

- `case` 标签必须是常量表达式，例如如果 `switch` 数据类型是 `int` 则为 `42`，如果 `switch` 数据类型是 `char` 则为 `'4'`，如果 `switch` 数据类型是 `string` 则为 `"42"`。如果需要在运行时计算 `case` 标签值，你必须使用 `if` 语句。

- `case` 标签必须是唯一的表达式。换句话说，两个 `case` 标签不能具有相同的值。

- 你可以通过提供一组 `case` 标签且中间没有介入语句来指定对多个值运行相同的语句，在这种情况下，最终标签列表的代码将为该列表中的所有情况执行。但是，如果标签有一条或多条关联语句，执行就不能落到后续标签；在此情况下，编译器会生成错误。以下代码片段说明了这些要点：

```
switch (trumps)
{
    case Hearts :
    case Diamonds :        // Fall-through allowed - no code between labels
        color = "Red";    // Code executed for Hearts and Diamonds
        break;
    case Clubs :
        color = "Black";
    case Spades :          // Error - code between labels
        color = "Black";
        break;
}
```

# Note

`break` 语句是最常见的停止落入下一条语句的方式，但你也可以使用 `return` 语句退出包含 `switch` 语句的方法，或使用 `throw` 语句生成异常并中止 `switch` 语句。`throw` 语句在第 6 章“管理错误和异常”中描述。

### *switch* fall-through rules

由于如果有任何介入代码就不能意外地从一个 `case` 标签落到下一个，因此你可以自由地重新排列 `switch` 语句的各部分而不影响其含义（包括 `default` 标签，按惯例通常——但不必——放在最后一个标签）。

C 和 C++ 程序员应注意，`break` 语句对 `switch` 语句中的每个 `case` 都是强制性的（甚至是 `default` case）。这一要求是一件好事——在 C 或 C++ 程序中，忘记 `break` 语句是很常见的，这会导致执行落到下一个标签，从而导致难以发现的错误。

如果你真的想，可以通过使用 `goto` 语句跳转到下一个 `case` 或 `default` 标签来模拟 C/C++ 中的落入行为。一般来说不推荐使用 `goto`，而且本书不会向你展示如何操作。

在下面的练习中，你将完成一个程序，该程序读取字符串的字符并将每个字符映射到其 XML 表示。例如，左尖括号字符 (`<`) 在 XML 中有特殊含义（用于形成元素）。如果你的数据包含此字符，它必须被翻译成文本实体 `&lt;`，以便 XML 处理器知道它是数据而不是 XML 指令的一部分。类似的规则适用于右尖括号 (`>`)、与号 (`&`)、单引号 (`'`) 和双引号 (`"`) 字符。你将编写一个 `switch` 语句来测试字符的值并将特殊 XML 字符作为 `case` 标签捕获。

### Write switch statements

- 1. 如果尚未运行，请启动 `Visual Studio 2015`。

- 2. 打开 `SwitchStatement` 项目，该项目位于你的文档文件夹中的 `\Microsoft Press\VCSBS\Chapter 4\SwitchStatement` 文件夹中。

- 3. 在 `Debug` 菜单上，单击 `Start Debugging`。

`Visual Studio 2015` 构建并运行应用程序。应用程序显示一个包含两个文本框并由 `Copy` 按钮分隔的表单。

- 4. 在上方的文本框中输入以下示例文本：

`inRange = (lo <= number) && (hi >= number);`

- 5. 单击 `Copy`。

语句原样复制到下方的文本框中，且 `<`、`&` 或 `>` 字符不会发生翻译，如以下屏幕截图所示。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_149_0.png)

6. 返回 `Visual Studio 2015` 并停止调试。

7. 在代码和文本编辑器窗口中显示 `MainPage.xaml.cs` 的代码并找到 `copyOne` 方法。

`copyOne` 方法将作为其输入参数指定的字符复制到下方的文本框中显示的文本末尾。目前，`copyOne` 包含一个只有一个默认操作的 `switch` 语句。在接下来的几个步骤中，你将修改此 `switch` 语句以将 XML 中重要的字符转换为其 XML 映射。例如，`<` 字符将被转换为字符串 `&lt;`。

8. 在 `switch` 语句的开始大括号之后并直接在 `default` 标签之前，将以下以粗体显示的语句添加到 `switch` 语句中：

```
switch (current)
{
    case '<' :
        target.Text += "&lt;";
        break;
    default:
        target.Text += current;
        break;
```

如果当前正在复制的字符是左尖括号 (`<`)，则前面的代码会在其位置将字符串 `"&lt;"` 附加到输出文本中。

9. 在你刚刚添加的 `break` 语句之后并在 `default` 标签之上，将以下语句添加到 `switch` 语句中：

```
case '>' :
    target.Text += "&gt;";
    break;
case '&' :
    target.Text += "&amp;";
    break;
case '"' :
    target.Text += "&#34;";
    break;
case '\'' :
    target.Text += "&#39;";
    break;
```

# Note

单引号 (`'`) 和双引号 (`"`) 在 C# 中有特殊含义——它们用于分隔字符和字符串常量。最后两个 `case` 标签中的反斜杠 (`\`) 是一个转义字符，会导致 C# 编译器将这些字符视为文字而不是分隔符。

10. 在 `Debug` 菜单上，单击 `Start Debugging`。

11. 在上方的文本框中输入以下文本：

`inRange = (lo <= number) && (hi >= number);`

12. 单击 `Copy`。

语句被复制到下方的文本框中。这一次，每个字符都经过 `switch` 语句中实现的 XML 映射。目标文本框显示以下文本：

`inRange = (lo &lt;= number) &amp;&amp; (hi &gt;= number);`

13. 尝试其他字符串，并验证所有特殊字符（`<`、`>`、`&`、`"` 和 `'`）是否都得到正确处理。

14. 返回 `Visual Studio` 并停止调试。

### Summary

在本章中，你学习了布尔表达式和变量。你看到了

如何使用布尔表达式与 `if` 和 `switch` 语句在程序中做出决策，以及如何使用布尔运算符组合布尔表达式。

- 如果你想继续下一章，请保持 `Visual Studio 2015` 运行并转到第 5 章“使用复合赋值和迭代语句”。

- 如果你现在想退出 `Visual Studio 2015`，请在 `File` 菜单上单击 `Exit`。如果出现 `Save` 对话框，请单击 `Yes` 并保存项目。

### Quick reference

| To | Do this | Example |
|---|---|---|
| Determine whether two values are equivalent | Use the `==` operator or the `!=` operator. | `answer == 42` |
| Compare the value of two expressions | Use the `<`, `<=`, `>`, or `>=` operator. | `age >= 21` |
