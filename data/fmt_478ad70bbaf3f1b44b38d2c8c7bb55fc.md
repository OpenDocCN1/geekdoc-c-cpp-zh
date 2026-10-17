
再次，这些是第一个日期早于第二个日期时的正确结果。

- 16. 测试其他日期，并验证结果是否符合预期。完成后，返回 `Visual Studio 2017` 并停止调试。

# 在真实世界应用中比较日期

现在你已经看到了如何使用一系列相当长且复杂的 `if` 和 `else` 语句，我应该提到，这并不是你在真实世界应用中比较日期时会采用的技术。如果你查看上一个练习中的 `dateCompare` 方法，你会发现两个参数 `leftHandSide` 和 `rightHandSide` 是 `DateTime` 值。你编写的逻辑只比较这些参数的日期部分，但它们还包含你没有（或没有显示）的时间元素。要使两个 `DateTime` 值被视为相等，它们不仅应该具有相同的日期，还应该具有相同的时间。比较日期时间是非常常见的操作，因此 `DateTime` 实际上有一个内置名为 `Compare` 的方法专门执行此操作：它接受两个参数并进行比较，返回一个值，指示第一个参数是否小于第二个（在这种情况下结果为负）；第一个参数是否大于第二个（在这种情况下结果为正）；或两个参数表示相同的日期和时间（在这种情况下结果为 0）。

# 使用 switch 语句

有时当你编写级联 `if` 语句时，每个 `if` 语句看起来都很相似，因为它们都在评估相同的表达式。唯一的区别是每个 `if` 将将逻辑的结果与具有不同值的表达式进行比较。例如，考虑以下代码块，它使用 `if` 语句检查 `day` 变量并确定它是星期几：

点击此处查看代码图片

```csharp
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
}
```

在这些情况下，你可以将级联 `if` 语句重写为 `switch` 语句，以使程序更高效、更具读性。

# 理解 switch 语句语法

`switch` 语句的语法如下（`switch`、`case` 和 `default` 是关键字）：

点击此处查看代码表达式

```csharp
switch ( controllingExpression )
{
  case constantExpression :
    statements
    break;
  case constantExpression :
    statements
    break;
  default :
    statements
    break;
}
```

`controllingExpression` 必须在括号内，会被评估一次。控制跳转到由 `constantExpression` 标识的代码块，其值等于 `controllingExpression` 的结果。（`constantExpression` 标识符也称为标签）。执行到 `break` 语句为止，此时 `switch` 语句结束，程序从右大括号后的第一个语句继续执行。

注意：如果没有 `constantExpression` 匹配 `controllingExpression` 的值，且没有 `default` 标签，执行将从 `switch` 语句右大括号后的第一个语句继续。

因此，你可以将之前的 `if` 语句重写为如下 `switch` 语句：

点击此处查看代码图片

```csharp
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

# 遵循 switch 规则

基本的 `switch` 语句非常有用，但遗憾的是，你并不总是可以在需要的地方它。你编写的任何 `switch` 语句必须遵守以下规则：

- 你只能对某些数据类型使用 `switch`，例如 `int`、`char` 或 `string`。对于任何其他类型（包括 `float` 和 `double`），你必须使用 `if` 语句。
- `case` 标签必须是常量表达式，例如如果 `switch` 数据类型是 `int`，则为 `42`；如果是 `char`，则为 `'42'`；如果是 `string`，则为 `"42"`。如果你需要在运行时计算你的 `case` 标签，你必须使用 `if` 语句。
- `case` 标签必须是唯一的。换句话说，两个 `case` 标签不能具有相同的值。

你可以通过提供 `case` 标签列表且中间没有插入语句，来指定要为多个值运行相同的语句，在这种情况下，列表中最后一个标签的代码将为列表中的所有情况执行。然而，如果一个标签有一个或多个关联的语句，执行将无法穿透（fall-through）到后续的标签；在这种情况下，编译器会生成错误。以下代码片段说明了这些点：

点击此处查看代码图片

```csharp
switch (trumps)
{
  case Hearts :
  case Diamonds : // 允许穿透，标签之间没有代码
    color = "Red"; // 为 Hearts 和 Diamonds 执行代码
    break;
  case Clubs :
    color = "Black";
  case Spades : // 错误 - 标签之间有代码
    color = "Black";
    break;
}
```

注意：`break` 语句是停止穿透的最常见方法，但你也可以使用 `return` 语句退出包含 `switch` 语句的方法，或者使用 `throw` 语句生成异常并终止 `switch` 语句。`throw` 语句在第6章“管理错误和异常”中描述。

# switch 穿透规则

由于在没有中间代码的情况下，你不会意外穿透到下一个 `case` 标签，你可以自由地排列 `switch` 语句各个部分而不影响其含义（包括 `default` 标签，按照惯例通常——但不必——放在最后一个标签）。

C 和 C++ 程序员应该注意，`break` 语句是

`switch` 语句中的每个 `case` 都是强制性的（即使是 `default` case 也是如此）。这一要求是一件好事——在 C 或 C++ 程序中，忘记 `break` 语句是很常见的，这会导致执行贯穿到下一个标签，从而引发难以发现的错误。

如果你确实需要，可以在 C# 中通过 `goto` 语句跳转到下一个 `case` 或 `default` 标签来模拟 C/C++ 的贯穿行为。不过，通常不建议使用 `goto`，本书也没有演示如何实现。

在接下来的练习中，你将完成一个程序，该程序读取字符串的字符并将每个字符映射到其 XML 表示。例如，左尖括号字符 `<` 在 XML 中具有特殊含义（如果你的数据包含此字符，则必须将其转换为文本实体 `&lt;`，这样 XML 处理器才知道它是数据而不是 XML 指令的一部分）。类似的规则也适用于右尖括号 `>`、和符号 `&`、单引号 (`'`) 和双引号 (`"`) 字符。你将编写一个 `switch` 语句来测试字符的值，并将特殊的 XML 字符作为 `case` 标签进行捕获。

## 编写 switch 语句

- 1. 启动 `Visual Studio 2017`（如果它尚未运行）。
- 2. 打开 `SwitchStatement` 解决方案，它位于文档文件夹下的 `\Microsoft Press\VCSBS\Chapter 4\SwitchStatement` 文件夹中。
- 3. 在“调试”菜单上，点击“开始调试”。

`Visual Studio 2017` 编译并运行应用程序。该应用程序显示一个包含两个文本框的表单，两个框之间由“复制”按钮隔开。

- 4. 在上方文本框中输入以下示例文本：

点击此处查看代码图像

```
inRange = (lo <= number) && (hi >= number);
```

- 5. 点击“复制”。

该语句被原样复制到下方的文本框中，`<`、`&` 或 `>` 字符没有发生任何转换，如下屏所示。

### SwitchStatement

```
inRange = (lo <= number) && (hi >= number);
```

复制

```
inRange = (lo <= number) && (hi >= number);
```

- 6. 返回 `Visual Studio 2017` 并停止调试。
- 7. 在“代码和文本编辑器”窗口中显示 `MainPage.xml.cs` 的代码并找到 `copyOne` 方法。它目前如下：

点击此处查看代码图像

```
private void copyOne(char current)
{
    switch (current)
    {
        default:
            target.Text += current;
            break;
    }
}
```

`copyOne` 方法将输入参数指定的字符复制到下方文本框显示的文本末尾。目前，`copyOne` 包含一个带有单一默认操作的 `switch` 语句。在接下来的几步中，你将修改此 `switch` 语句，将那些在 XML 映射中具有意义的字符转换为 XML。例如，`<` 字符将被转换为字符串 `&lt;`。

- 8. 在语句的大括号之后、`default` 标签之前，添加**加粗**显示的以下语句：

点击此处查看图像

```
switch (current)
{
  case '<':
    target.Text += "&lt;";
    break;
  default:
    target.Text += current;
    break;
}
```

如果当前复制的字符是左括号 (`<`)，则之前的字符会在输出文本中被字符串 `&lt;` 取替。

- 9. 在你刚刚添加的 `break` 语句之后、`default` 标签之前，向 `switch` 语句中添加以下 `case`：

点击此处查看图像

```
case '>':
    target.Text += "&gt;";
    break;
case '&':
    target.Text += "&amp;";
    break;
case '\'':
    target.Text += "&#34;";
    break;
case '\\':
    target.Text += "&#39;";
    break;
```

> 注意：单引号 (`'`) 和双引号 (`"`) 在 C# 中具有特殊含义——它们用于界定字符和字符串。最后两个 `case` 标签中的反斜杠 (`\`) 是转义字符，导致 C# 编译器将这些字符视为字面量而不是分隔符。

- 10. 在“调试”菜单上，点击“开始调试”。
- 11. 在上方文本框中输入以下文本：

点击此处查看代码图像

```
inRange = (lo <= number) && (hi >= number);
```

- 12. 点击“复制”。

该语句被复制到下方的文本框中。这次，每个字符都经历了 `switch` 语句中实现的 XML 映射。目标框显示以下文本：

点击此处查看代码图像

```
inRange = (lo &lt;= number) &amp;&amp; (hi &gt;= number);
```

- 13. 尝试其他字符串并验证所有特殊字符 (`<`, `>`, `&`, `\`, 和 `'`) 是否均被正确处理。
- 14. 返回 `Visual Studio` 并停止调试。

# 总结

在本章中，你学习了布尔表达式和变量。你了解了如何在 `if` 和 `switch` 语句中使用布尔表达式在程序中做出决策，并学会了使用布尔运算符组合布尔表达式。

- 如果你想继续下一章，请保持 `Visual Studio 2017` 运行并转到第 5 章“使用复合赋值和迭代语句”。
- 如果你想现在退出 `Visual Studio 2017`，请在“文件”菜单上点击“退出”。你会看到一个保存对话框。

> **提示** 复合赋值运算符的优先级和右结合性与简单赋值运算符 (`=`) 相同。

`+=` 运算符适用于字符串；它将一个字符串附加另一个字符串的末尾。例如，以下代码会在控制台上显示 "Hello John"：

[单击此处代码图片]

```
string name = "John";
string greeting = "Hello ";
greeting += name;
Console.WriteLine(greeting);
```

你不能在字符串上使用任何其他复合赋值运算符。

> **提示** 当将变量增加或减少 1 时，请使用递增 (`++`) 和 递减 (`--`) 运算符，而不是复合赋值运算符。例如，将

[单击此处代码图片]

```
count += 1;
```

替换为

```
count++;
```

## 编写 while 语句

你使用 `while` 语句在条件为真时重复运行某个语句。`while` 语句的语法如下：

[单击此处代码图片]

```
while ( booleanExpression )
statement
```

布尔表达式（必须包含在括号内）会被求值，如果为真，则执行该语句，然后再次对布尔表达式进行求值。如果表达式仍然为真，则重复语句，然后再次对布尔表达式进行求值。此过程一直持续到布尔表达式求值为假，此时 `while` 语句退出。执行将继续 `while` 语句之后的第一个语句。`while` 语句与 `if` 语句具有以下语法相似性（实际上，除了关键字完全相同）：

- 表达式必须是一个布尔表达式。
- 布尔表达式必须写在括号内。
- 如果表达式在第一次求值时为假，则语句不执行。
- 如果你想在 `while` 语句的控制下执行两个或多个语句，必须使用大括号将这些语句分组在一个块中。

以下是一个向控制台写入 0 到 9 的 `while` 语句。注意，一旦值达到 10，`while` 就会结束，语句块中的代码就不会执行：

[单击此处代码图片]

```
int i = 0;
while (i < 10)
{
  Console.WriteLine(i);
  i++;
}
```

所有的 `while` 语句都应该在某处终止。初学者常见的错误是忘记包含一个语句使布尔表达式最终求值为假并终止循环（`i++;`），这会导致程序无限运行。在示例中，语句 `i++;` 承担了这一角色。

> 注意 `while` 循环中的变量 `i` 控制循环执行的迭代次数。这是一种常见的惯用法，承担此角色的变量有时被称为哨兵变量（sentinel variable）。你还可以创建嵌套循环（一个循环内部另一个循环），在这种情况下，通常会将此命名模式扩展，使用 `j`、`k` 甚至 `i` 作为控制这些循环迭代的哨兵变量名。

提示：与 `if` 语句一样，建议在使用 `while` 语句时始终使用块，即使该块只包含一个语句。这样，如果你决定在 `while` 结构体中添加更多语句，就能很清楚你应该将它们添加到块中。如果不这样做，只有紧跟在 `while` 结构布尔表达式后面的第一个语句将作为循环的一部分执行，从而导致难以察觉的错误，如下：

[单击此处代码图片]

```
int i = 0;
while (i < 10)
Console.WriteLine(i);
i++;
```
