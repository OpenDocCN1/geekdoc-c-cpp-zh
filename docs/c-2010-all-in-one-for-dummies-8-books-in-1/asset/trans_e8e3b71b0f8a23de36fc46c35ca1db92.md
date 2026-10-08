

## 让我们开始循环循环 101

```csharp
// 提示用户输入本金；持续提示
// 直到输入正确的值。
decimal principal;
while(true) {
    Console.Write("Enter principal: ");
    string principalInput = Console.ReadLine();
    principal = Convert.ToDecimal(principalInput);
    // 如果值正确，则退出
    if (principal >= 0) {
        break;
    }
    // 如果输入错误，生成错误。
    Console.WriteLine("Principal cannot be negative");
    Console.WriteLine("Try again");
    Console.WriteLine();
}
// 现在输入利率。
while(true) {
    Console.Write("Enter interest: ");
    string interestInput = Console.ReadLine();
    decimal interest = Convert.ToDecimal(interestInput);
    // 如果利率为负数或太大，则不接受
    if (interest >= 0 && interest <= maximumInterest) {
        break;
    }
    // 同样生成一条错误消息。
    Console.WriteLine("* cannot be negative or greater than " + maximumInterest);
    Console.WriteLine("Try again");
    Console.WriteLine();
}
// 本金和利率似乎都是
// 最终的；输入年份。
Console.Write("Enter number of years: ");
string durationInput = Console.ReadLine();
int duration = Convert.ToInt32(durationInput);
// 验证输入。
Console.WriteLine("Skip a line.");
Console.WriteLine("Principal = " + principal);
Console.WriteLine("Interest = " + interest + "%");
Console.WriteLine("Duration = " + duration + " years");
Console.WriteLine();
// 现在按照指定的年份循环。
int year = 1;
while(year <= duration) {
    // 计算本金加利息的值。
    decimal interestPaid = principal * (interest / 100);
    // 现在通过加上利息计算新的本金
    principal = principal + interestPaid;
    // 将本金四舍五入到分分。
    principal = decimal.Round(principal, 2);
    // 输出结果。
    Console.WriteLine(year + " - " + principal);
    // 跳到下一年。
    year = year + 1;
}
```

第一部分 阶段程序流

## 102 让我们开始循环循环

```csharp
year = year * 1;
}
// 等待用户确认结果。
Console.WriteLine("Press Enter to terminate . . ");
Console.Read();

```

此程序的工作方式与本章之前节中的示例基本相同，仅在用户输入部分不同。这次，我们使用一个 `while` 循环替换了早期示例中用于检测无效输入的 `if` 语句：

```csharp
decimal principal;
while(true)
{
    Console.WriteLine("Enter principal: ");
    string principalInput = Console.ReadLine();
    principal = Convert.ToDecimal(principalInput);
    // 当输入的值正确时退出。
    if (principal >= 0)
    {
        break;
    }
    // 如果输入错误，生成错误。
    Console.WriteLine("Principal cannot be negative");
    Console.WriteLine("Try again");
    Console.WriteLine();
}
```

这段代码在循环内从用户处输入一个值。如果文本的值没问题，程序将退出输入循环并继续。然而，如果输入有误，用户将看到错误消息，控制权将传回程序重新开始。

程序将一直循环，直到用户输入正确的输入。（在最坏的情况下，程序可能会一直循环到某个迟钝的用户老死为止。）

注意，条件判断已经反转了，因为现在的问题不再是非法输入是否应该生成错误消息，而是正确输入是否应该退出循环。在利率部分，例如，考虑这段：

```csharp
principal < 0 || principal > maximumInterest
```

该测试变为：

```csharp
interest >= 0 && interest <= maximumInterest
```

显然，`interest >= 0` 是 `interest < 0` 的反面。可能没那么明显的是，逻辑或 (`|`) 运算符被替换成了逻辑与 (`&&`) 运算符。“如果利率大于零且小于小于最大值，则退出循环（换句话说，如果它是正确的）”

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_127_0.png)

## 让我们开始循环循环 103

顺问一下，你如何修改 `CalculateInterestTableMoreForgiving` 以让用户在计算后再次计算，并输入新的本金和利率数字，直到她想退出为止？**提示：** 使用另一个带有自身退出条件的 `while (true)` 循环。

注意，根据作用域规则，变量必须在循环外部声明，我将在下一节中解释。

听起来可能显而易见，但表达式 `true` 的结果是 `true`。因此，`while(true)` 是你典型的无限循环。退出循环的是嵌入的 `break` 命令。因此，如果你使用 `while(true)` 循环，确保你的 `break` 条件能够发生。

该程序示例执行的输出（显示了作者的一个无知）如下：

```
Enter principal: -1000
Principal cannot be negative
Try again

Enter principal: 1000
Enter interest: -10
Interest cannot be negative or greater than 50
Try again

Enter interest: 10
Enter number of years: 5

Principal = 1000
Interest = 10%
Duration = 5 years

1-1100.00
2-1210.00
3-1331.00
4-1464.10
5-1610.51
Press Enter to terminate . . .
```

程序拒绝接受负本金或利息金额，并在每次循环中痛苦地解释错误。

在返回循环进行进一步输入之前，要准确地解释用户做了什么，否则那个人将变得极其困惑。展示示例也可能有帮助，特别是对于格式问题。一点点外交手段并无害，正如奶奶可能指出的那样样。

在循环体内声明的变量*仅定义在*该循环内。考虑这段代码片段：

```csharp
int days = 1;
while(days < duration)
{
    int average = value / days;
    // ... 一系列命令
    days = days + 1;
}
```

变量 `average` 在 `while` 循环之外没有定义。

## 105 按指定次数循环

```csharp
year = year * 1;
}
```

第一部分
第 5 章

## 一个示例

你可以从这个示例中看到 `for` 循环是如何工作的：

```csharp
a = 1;
// 现在进行循环。
for(int year = 1; year < duration; year + 1)
{
    // . . 代码体 .
}
// 程序在此继续。
a = 2;
```
