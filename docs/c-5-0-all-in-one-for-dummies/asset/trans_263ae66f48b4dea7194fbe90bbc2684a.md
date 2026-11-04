
```
}
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate . . .");
Console.Read();
}
}
```

程序首先从用户那里读取本金。如果本金为负数，程序会输出错误信息并退出。如果本金不是负数，控制权会转到 else 子句，程序继续执行。

本例改进了利率测试。在这里，程序要求利率为非负数（数学定律）且小于某个最大利率（司法法律——我只希望信用卡有利率上限）。这个 if 语句使用了以下复合测试：

```
if (interest < 0 || interest > maximumInterest)
```

如果 interest 小于 0 或大于 maximumInterest，该语句为真。注意，我在程序顶部声明了 maximumInterest，而不是在这里将其硬编码为常量数字。硬编码是指在代码中直接使用值，而不是创建常量来保存它们。

![](img/80ff26f06fc9ab951e1cd4257b867366_115_0.png)

在程序顶部定义重要常量。给常量一个描述性名称（而不只是一个数字）便于查找，也更容易修改。如果该常量在代码中出现十次，要更改所有引用，你仍然只需做一次修改。

输入正确的本金但利率为负数时，会生成以下输出：

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative or greater than 50.
Press Enter to terminate . . .
```

只有当用户输入合法的本金和合法的利率时，程序才会生成正确的计算结果：

```
Enter principal: 1234
Enter interest: 12.5

Principal = 1234
Interest = 12.5%

Interest paid = 154.250
Total = 1388.250
Press Enter to terminate . . .
```

## 运行 switch 控制板

你经常需要针对许多不同的值测试同一个变量。例如，maritalStatus 可能为 0 表示未婚、1 表示已婚、2 表示离婚、3 表示丧偶（我肯定涵盖了所有选项——哦，等等），或者 4 表示“不关你的事”。要区分这些值，可以使用以下一系列 if 语句：

```
if (maritalStatus == 0)
{
    // Must be unmarried . . .
    // . . . do something . . .
}
else
{
    if (maritalStatus == 1)
    {
        // Must be married . . .
        // . . . do something else . . .
    }
```

以此类推。

你可以看到，这些重复的 if 语句很快就会让人厌烦。针对多种情况测试非常常见，因此 C# 提供了一种特殊构造，用于在一组互斥条件之间做出选择。这种控制结构就是 switch，其工作方式如下：

```
switch (maritalStatus)
{
    case 0:
        // . . . do the unmarried stuff . . .
        break;
    case 1:
        // . . . do the married stuff . . .
        break;
    case 2:
        // . . . do the divorced stuff . . .
        break;
    case 3:
        // . . . do the widowed stuff . . .
        break;
    case 4:
        // . . . get out of my face . . .
        break;
    default:
        // Goes here if it fails to pass a case;
        // this is probably an error condition.
        break;
}
```

switch 语句顶部的表达式会被求值。在本例中，表达式就是变量 maritalStatus。然后将该表达式的值与每个 case 的值进行比较。如果找不到匹配项，控制权会转到 default 子句。

switch 语句的参数也可以是字符串：

```
string s = "Davis";
switch(s)
{
case "Davis":
    // . . . control will actually pass here . . .
    break;
case "Smith":
    // . . . do Smith stuff . . .
    break;
case "Jones":
    // . . . do Jones stuff . . .
    break;
case "Hvidsten":
    // . . . do Hvidsten stuff . . .
    break;
default:
    // Goes here if it doesn't pass any cases.
    break;
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_117_0.png)

使用 switch 语句涉及以下严格限制：

- switch() 的参数必须是计数类型之一（包括 char）或字符串。浮点值被排除在外。
- 各个 case 值必须引用与 switch 表达式相同类型的值。
- case 值必须是常量，即其值必须在编译时已知。（诸如 case x 这样的语句不合法，除非 x 是某种常量。）
- 每个子句都必须以 break 语句（或其他退出命令，例如 return）结束。break 语句将控制权转出 switch。

如果两个 case 导致相同的操作，可以省略 break 语句：单个 case 子句可以有多个 case 标签，如下例所示：

```
string s = "Davis";
switch(s)
{
case "Davis":
case "Hvidsten":
    // Do the same thing whether s is Davis or Hvidsten
    // since they're related.
    break;
case "Smith":
    // . . . do Smith stuff . . .
    break;
default:
    // Goes here if it doesn't pass any cases.
    break;
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_118_0.png)

这种方法使程序无论输入是 Davis 还是 Hvidsten，都能执行相同的操作。网站上的 SwitchSyntaxTest 示例展示了关于使用 switch 的各种建议。本章最后一节为 switch 的故事提供了一个小补充。你可以在 csharp102.info 找到代码。

## 开始循环吧

if 语句使程序能够根据 bool 表达式的结果，在执行的代码中走不同的路径。与没有决策能力的程序相比，这种语句使程序有趣得多。而增加重复执行一组指令的能力，则是在能力上的又一次量子跃迁。

考虑本章前面“介绍 if 语句”一节中的 CalculateInterest 程序。使用计算器（或手工用纸笔）完成这个简单利息计算，会比编写和执行程序容易得多。

如果你能计算随后几年的本金金额，那会更有用。Microsoft Excel 电子表格中的简单宏仍然更容易处理，但至少你更接近目标了。

你需要的是一种让计算机多次执行同一小段指令的方法——这称为循环。

### while 循环

C# 关键字 while 引入最基本的执行循环形式：

```
while(bool-expression)
{
    // ... repeatedly executed as long as the expression is true.
}
```

第一次遇到 while 循环时，会求值 bool 表达式。如果表达式为真，则执行块内的代码。当代码块到达右花括号时，控制权返回顶部，整个过程重新开始。（这有点像我遛狗时的感觉。我和狗在院子里一圈又一圈地转，直到狗……嗯，直到它完事。）第一次求值 bool 表达式且结果为假时，控制权会越过右花括号。

![](img/80ff26f06fc9ab951e1cd4257b867366_118_1.png)

如果第一次遇到 while 循环时条件不为真，则花括号内的那组命令永远不会执行。

![](img/80ff26f06fc9ab951e1cd4257b867366_119_0.png)

程序员说话时常常变得不严谨。（程序员大多数时候都不严谨。）如果程序员说一个循环会执行到某个条件为假为止，那暗示只要条件变为假，控制权就会立即传到循环之外——无论程序当时正在执行到哪里。事实绝对不是这样。程序不会检查条件是否仍然为真，直到控制权特别返回到循环顶部。

你可以使用 while 循环创建 CalculateInterestTable 程序，这是 CalculateInterest 程序的循环版本。CalculateInterestTable 计算一张显示累计年度付款的本金表：

![](img/80ff26f06fc9ab951e1cd4257b867366_119_1.png)

```
// CalculateInterestTable -- Calculate the interest paid on a given
//              principal over a period of years.
using System;
namespace CalculateInterestTable
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // Define a maximum interest rate.
            int maximumInterest = 50;
            // Prompt user to enter source principal.
            Console.Write("Enter principal: ");
            string principalInput = Console.ReadLine();
            decimal principal = Convert.ToDecimal(principalInput);
            // If the principal is negative . . .
            if (principal < 0)
            {
                // . . . generate an error message . . .
                Console.WriteLine("Principal cannot be negative");
            }
            else  // Go here only if principal > 0; thus valid.
            {
                // . . . otherwise, enter the interest rate.
                Console.Write("Enter interest: ");
                string interestInput = Console.ReadLine();
                decimal interest = Convert.ToDecimal(interestInput);
                // If the interest is negative or too large . . .
                if (interest < 0 || interest > maximumInterest)
                {
                    // . . . generate an error message as well.
                    Console.WriteLine("Interest cannot be negative " +
                                      "or greater than " + maximumInterest);
                    interest = 0;
                }
                else  // Reach this point only if all is well.
                {
                    // Both the principal and the interest appear to be
                    // legal; finally, input the number of years.
                    Console.Write("Enter number of years: ");
                    string durationInput = Console.ReadLine();
                    int duration = Convert.ToInt32(durationInput);
                    // Verify the input.
                    Console.WriteLine();  // Skip a line.
                    Console.WriteLine("Principal = " + principal);
```
