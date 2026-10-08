

## 88 使用 if 和 switch 进行分支

```csharp
Console.WriteLine("Total = " + total +);\n// 等待用户确认结果。
Console.WriteLine("Press Enter to terminate . . .");
Console.Read();
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_113_0.png)

`CalculateInterest` 程序首先通过 `WriteLine()`向用户提示其姓名，该方法向控制台写入一个字符串。准确地告诉用户你想要什么，如果可能的话，要指定格式。对于没有提供信息的提示（例如 `>`），用户的反应通常不太良好。

示例程序使用 `ReadLine()` 命令在用户输入时读取；当用户按下回车键时，程序会以字符串的形式返回该值。由于程序正在寻找小数形式的本金，因此必须使用 `Convert.ToDecimal()` 命令对输入字符串进行转换。结果存储在 `principalInput` 中。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_113_1.png)

`ReadLine()`、`WriteLine()` 和 `ToDecimal()` 命令都是方法调用的示例。方法调用将工作委托给程序的另一个部分，该部分被称为“方法”。我将在第二书中详细描述方法调用；这些特定的方法调用是直观的。你应该能够通过我那极具洞察力的解释来理解其含义的大意。如果这很有用，请忽略叙述；如果不起作用，请参阅第二本书。

示例中的下一行检查 `principal`。如果它为负数，程序将输出一条礼貌的“恶性信息（nastygram）”，指示用户出错了。程序对利率也执行相同的操作，然后简化了之前在“介绍 if 语句”中概述的利息计算，并使用一系列 `WriteLine()` 命令输出。

使用合法的本金和不寻常的利率（在大多数情况下是完全合法的），程序会生成以下输出：

```
Enter principal: 1234
Enter interest: 21%

Principal = 1234
Interest      = 21%

Interest paid = 259.14
Total         = 1493.14
Enter Enter to terminate . . .
```

使用非法输入执行程序将生成以下输出：

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative

Principal = 1234
Interest      = 0%
```

## 使用 if 和 switch 进行分支

Interest paid = 0
Total = 1234
Press Enter to terminate ..

第一本书
第 5 章

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_114_0.png)

深入
程序流程

对 `if` 子句内部的行进行缩进以增强可读性。C# 会忽略这种类型的缩进，但它对我们人类来说是有帮助的。大多数编程编辑器都支持自动缩进，即只要在你输入 `if` 命令时，编辑器会自动插入。要在 Visual Studio 中设置自动缩进，选择“工具（Tools）+选项（Options）”。展开“编辑器（Editor）”节点。从那里，展开 C#。最后，点击“制表符（Tabs）”。在此页面上，启用“智能缩进（Smart Indenting）”并根据你的喜好设置每个缩进的空格数。（我在本书中使用每次缩进两个空格）。将制表符大小也设置为相同的值。

## 检查 else 语句

有时，你的代码必须检查互斥条件。例如，以下代码段将两个数字 `a` 和 `b` 的最大值存储在变量 `max` 中：

```csharp
// 将 a 和 b 的最大值存储在变量 max 中。
int max;
// 如果 a 大于 b . . .
if (a > b)
{
    // . . 将 a 保存为最大值。
    max = a;
}
// 如果 a 小于等于 b . . .
if (a <= b)
{
    // . . 将 b 保存为最大值。
    max = b;
}
```

第二个 `if` 语句会导致不需要的处理，这两个条件是互斥的。如果 `a` 大于 `b`，它就不可能小于等于 `b`。C# 专门为这种情况定义了 `else` 子句。`else` 关键字定义了一个代码块，如果 `if` 块没有执行，则执行该代码块。

计算最大值的代码段现在看起来如下：

```csharp
// 将 a 和 b 的最大值存储在变量 max 中。
int max;
// 如果 a 大于 b . . .
if (a > b)
{
    // . . 将 a 保存为最大值；否则 . . .
    max = a;
}
else
{
    // . . 将 b 保存为最大值。
    max = b;
}
```

## 90 使用 if 和 switch 进行分支

如果 `a` 大于 `b`，则执行第一个块；否则，执行第二个块。最后，`max` 包含 `a` 或 `b` 中的较大值。

## 甚至避免 else

连续的 `else` 也会导致困惑。某些程序员在这样做时会避免它们，因为这样做甚至不会引起更多困惑。你可以这样编写最大值计算：

```csharp
// 将 a 和 b 的最大值存储在变量 max 中。
int max;
// 先假设 a 大于 b。
max = a;
// 如果不是这样 ...
if (b > a)
{
    // 那么你可以改变主意。
    max = b;
}
```

某些程序员像躲避瘟疫一样避免这种风格，我对此表示同情。（这并不意味着我会改变，只是表示我同情。）你可以在常用语中看到这种风格和“else 风格”。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_115_0.png)

喜欢简洁且晦涩难懂的程序员经常使用三元运算符 `?:`，它等同于一行的 `if/else`：

```csharp
bool informal = true;
string name = informal ? "Chuck" : "Charles"; // 返回 "Chuck"
```

这段代码会评估冒号之前的表达式：如果表达式为真，它返回问号之前的内容。如果表达式为假，它返回问号后面的内容。

这一部分评估冒号之前的表达式：如果表达式为真，它返回问号之前的内容。如果表达式为假，它返回问号后面的内容。这把 `if/else` 变成了一个表达式。

很少使用三元运算符，是因为它是晦涩的。

## 嵌套 if 语句

`CalculateInterest` 程序警告用户输入非法；然而，继续利息计算，即使其中一个值是不合理的，这似乎不对。因为利息计算几乎不花时间。此外，在用户已经输入了无效值后，为什么要询问利率？（你会惊讶于这有多么令人愤怒。）

程序应该只在本金合理的情况下要求用户输入利率。要实现这一点，你需要两个 `if` 语句，一个在另一个内部。

## 使用 if 和 switch 进行分支 91

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_116_0.png)

位于另一个语句内部的 `if` 语句是嵌入或嵌套语句。

以下程序 `CalculateWithTest` 使用嵌入 `if` 语句来避免愚蠢的问题：

```csharp
// CalculateWithTest -- 计算给定本金的
// 利息金额。如果本金或利率
// 为负，则生成错误信息
// 并不继续计算。
using System;
namespace CalculateWithTest
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // 定义最大利率。
            int maximumInterest = 0;
            // 提示用户输入本金。
            Console.Write("Enter principal: ");
            string principalInput = Console.ReadLine();
            decimal principal = Convert.ToDecimal(principalInput);
// 如果本金为负数 -
            if (principal < 0)
            {
                // 生成错误信息
                Console.WriteLine("Principal cannot be negative!");
            }
            else
            {
                // 否则，输入利率。
                Console.Write("Enter interest: ");
                string interestInput = Console.ReadLine();
                decimal interest = Convert.ToDecimal(interestInput);
// 如果利率为负或太大 -
                if (interest < 0 || interest > maximumInterest)
                {
                    // 同样生成错误信息。
                    Console.WriteLine("Interest cannot be negative or greater than " + maximumInterest);
                    interest = 0;
                }
                else
                {
                    // 本金和利率看起来都是合法的；
                    // 计算本金加利息的值。
                    decimal interestPaid = principal * (interest / 100);
                    // 现在计算总额。
                    decimal total = principal + interestPaid;
                    // 输出结果。
                    Console.WriteLine();
                    Console.WriteLine("Principal = " + principal + "*");
                    Console.WriteLine("Interest = " + interest + " **%");
                    Console.WriteLine();
                    Console.WriteLine("Interest paid = " + interestPaid);
                    Console.WriteLine("Total = " + total);
                }
            }
        }
    }
}
```

