
```
while(year <= duration)
{
    // Calculate the value of the principal plus interest.
    decimal interestPaid;
    interestPaid = principal * (interest / 100);
    // Now calculate the new principal by adding
    // the interest to the previous principal.
    principal = principal + interestPaid;
    // Round off the principal to the nearest cent.
    principal = decimal.Round(principal, 2);
    // Output the result.
    Console.WriteLine(year + " - " + principal);
    // Skip over to next year.
    year = year + 1;
}
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate . . .");
Console.Read();
}
```

本程序的工作方式在很大程度上与本章前几节中的示例相同，只是用户输入方面有所不同。这次，用 while 循环取代了早期示例中用于检测无效输入的 if 语句：

```
decimal principal;
while(true)
{
    Console.Write("Enter principal: ");
    string principalInput = Console.ReadLine();
    principal = Convert.ToDecimal(principalInput);
    // Exit when the value entered is correct.
    if (principal >= 0)
    {
        break;
    }
    // Generate an error on incorrect input.
    Console.WriteLine("Principal cannot be negative");
    Console.WriteLine("Try again");
    Console.WriteLine();
}
```

这段代码在循环中从用户输入一个值。如果文本的值正确，程序将退出输入循环并继续；然而，如果输入有错误，用户会看到错误信息，控制权会返回到程序流程以重新开始。

![](img/80ff26f06fc9ab951e1cd4257b867366_125_0.png)

程序会一直循环，直到用户输入正确的值。（在最坏的情况下，程序可能会一直循环，直到一个迟钝的用户因年老而去世。）

请注意条件判断已被反转，因为问题不再是非法输入是否应生成错误信息，而是正确的输入是否应退出循环。例如在利率部分，考虑以下测试：

```
principal < 0 || principal > maximumInterest
```

该测试改为如下：

```
interest >= 0 && interest <= maximumInterest
```

显然，interest >= 0 与 interest < 0 相反。可能不太明显的是，OR（| |）运算符被 AND（&&）运算符取代了。它表示：“如果利率大于零且小于最大值（换句话说，如果正确），则退出循环。”

顺便问一下，你如何修改 CalculateInterestTableMoreForgiving，让用户一次又一次地运行计算，并在每次想要退出之前输入新的本金和利率数字？提示：使用另一个带有自身退出条件的 while(true) 循环。

请注意，由于作用域规则，principal 变量必须在循环外部声明，我将在下一节中解释这一点。

![](img/80ff26f06fc9ab951e1cd4257b867366_126_0.png)

这听起来可能很明显，但表达式 true 的求值结果为 true。因此，while(true) 是典型的无限循环。嵌入的 break 命令使循环退出。因此，如果你使用 while(true) 循环，请确保你的 break 条件可以发生。

该程序示例运行的输出（显示了作者的无知）如下所示：

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

Principal      = 1000
Interest       = 10%
Duration       = 5 years

1-1100.00
2-1210.00
3-1331.00
4-1464.10
5-1610.51
Press Enter to terminate . . .
```

程序拒绝接受负的本金或利率，并耐心地在每次循环中解释错误。

![](img/80ff26f06fc9ab951e1cd4257b867366_127_0.png)

在循环返回以进行进一步输入之前，准确解释用户做错了什么，否则那个人会变得极度困惑。举例也可能有帮助，尤其是在格式问题上。一点外交手腕也不会有坏处，正如奶奶可能指出的那样。

## 聚焦作用域规则

在循环体内声明的变量仅在该循环内定义。请考虑以下代码片段：

```
int days = 1;
while(days < duration)
{
    int average = value / days;
    // . . . some series of commands . . .
    days = days + 1;
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_127_1.png)

变量 average 在 while 循环外部未定义。存在各种原因，但请考虑以下原因：循环第一次执行时，程序遇到声明 int average，变量被定义。在第二次循环时，程序再次遇到 average 的声明，如果没有作用域规则，这将是一个错误，因为变量已经被定义了。

我可以提供其他更有说服力的理由，但目前这个理由就足够了。

简而言之，就 C# 而言，变量 average 在程序到达闭合大括号时就会消失——并且在每次循环中都会重新定义。

![](img/80ff26f06fc9ab951e1cd4257b867366_127_2.png)

有经验的程序员说变量 average 的作用域仅限于 while 循环。

## 使用 for 循环指定次数

while 循环是 C# 中最简单且第二常用的循环结构。然而，与 for 循环相比，while 循环的使用频率大约相当于美国机加工车间中的公制工具。

for 循环具有以下结构：

```
for(initExpression; condition; incrementExpression)
{
    // . . . body of code . . .
}
```

当遇到 for 循环时，程序首先执行 initExpression 表达式，然后执行条件。如果条件表达式为真，程序执行循环体，该循环体由紧跟在 for 命令后的大括号包围。当程序到达闭合大括号时，控制权传递给 incrementExpression，然后返回到 condition，在那里开始下一次循环。

实际上，for 循环的定义可以转换为以下 while 循环：

```
initExpression;
while(condition)
{
    // . . . body of code . . .
    incrementExpression;
}
```

## 一个示例

你可以在以下示例中更好地了解 for 循环的工作方式：

```
// Here is one C# expression or another.
a = 1;
// Now loop for awhile.
for(int year = 1; year < duration; year = year + 1)
{
    // . . . body of code . . .
}
// The program continues here.
a = 2;
```

假设程序刚刚执行了 a = 1; 表达式。接下来，程序声明变量 year 并将其初始化为 1。然后程序将 year 与 duration 进行比较。如果 year 小于 duration，则大括号内的代码体被执行。遇到闭合大括号后，程序跳回顶部并执行 year = year + 1 子句，然后再回到 year < duration 比较。

![](img/80ff26f06fc9ab951e1cd4257b867366_128_0.png)

year 变量在 for 循环的作用域之外未定义。循环的作用域包括循环的标题及其主体。

## 为什么还需要另一个循环？

如果 C# 已有等效的 while 循环，为什么还需要 for 循环？简短的回答是：不需要——for 循环没有带来 while 循环无法实现的东西。

然而，for 循环的各部分是为了方便而存在的——并且为了明确建立每个循环应有的三个部分：设置、退出条件和递增。不仅这种安排更易于阅读，而且也更容易正确实现。（请记住，while 循环中最常见的错误是忘记递增计数变量以及未能提供适当的退出条件。）

除了我可能做的任何歌舞式的解释之外，理解 for 循环最重要的原因是：这是每个人都使用的循环——它（连同其表亲 foreach）是你阅读他人代码时 90% 的时间看到的循环。

for 循环的设计使第一个表达式初始化计数变量，最后一个部分递增它；然而，C# 语言并不强制执行此类规则。你可以在这两个部分中做任何你想做的事情——然而，除了初始化和递增计数变量之外做任何事情都是不明智的。

![](img/80ff26f06fc9ab951e1cd4257b867366_129_0.png)

在编写 for 循环时，自增运算符特别受欢迎。（我在本书迷你版的第 4 章中描述了自增运算符以及其他运算符。）之前的 for 循环通常这样写：

```
for(int year = 1; year < nDuration; year++)
{
    // . . . body of code . . .
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_129_1.png)

你几乎总是看到在 for 循环中使用后置自增运算符而不是前置自增运算符，尽管在这种情况下效果相同。除了习惯和它看起来更酷之外，没有其他原因。（下次你想打破僵局时，只要拿出满是后置自增运算符的 C# 代码清单来展示你有多酷就行了。它几乎从不奏效，但值得一试。）

for 循环有一个我无法声称理解的变化。如果逻辑条件表达式缺失，则假定为真。因此 for( ; ; ) 是一个无限循环。

![](img/80ff26f06fc9ab951e1cd4257b867366_129_2.png)

你看到 for( ; ; ) 用作无限循环的频率比 while(true) 更常见。我不知道为什么会这样。

## 嵌套循环

内层循环可以出现在外层循环内，如下所示：

```
for( . . .some condition . . .)
{
    for( . . .some other condition . . .)
    {
        // . . . do whatever . . .
    }
}
```

内层循环在外层循环的每次遍历后执行完毕。内层 for 循环中使用的循环变量（如 year）在内层循环的作用域之外未定义。
