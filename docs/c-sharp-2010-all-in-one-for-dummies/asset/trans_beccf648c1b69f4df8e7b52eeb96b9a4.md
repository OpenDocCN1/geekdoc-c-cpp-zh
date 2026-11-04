

```
// Calculate the value of the principal plus interest.
decimal interestPaid;
interestPaid = principal * (interest / 100);
// Now calculate the total.
decimal total = principal + interestPaid;
```

第一个等式将本金乘以利率，得到应支付的利息——interestPaid。（除以 100 是因为利息通常以百分比金额输入来计算。）然后，应支付的利息被加回本金，得到新的本金，并存储在变量 total 中。

处理用户输入时，程序几乎必须预见任何情况。例如，你不希望程序接受负数的本金或利息金额（好吧，也许负利息除外）。下面的 CalculateInterest 程序包含检查，以确保这两种输入都不会发生：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_112_0.png)

```
// CalculateInterest -- Calculate the interest amount paid
// on a given principal. If either the principal or the
// interest rate is negative, generate an error message.
using System;
namespace CalculateInterest
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Prompt user to enter source principal.
            Console.Write("Enter principal: ");
            string principalInput = Console.ReadLine();
            decimal principal = Convert.ToDecimal(principalInput);

            // Make sure that the principal is not negative.
            if (principal < 0)
            {
                Console.WriteLine("Principal cannot be negative");
                principal = 0;
            }

            // Enter the interest rate.
            Console.Write("Enter interest: ");
            string interestInput = Console.ReadLine();
            decimal interest = Convert.ToDecimal(interestInput);

            // Make sure that the interest is not negative either.
            if (interest < 0)
            {
                Console.WriteLine("Interest cannot be negative");
                interest = 0;
            }

            // Calculate the value of the principal plus interest.
            decimal interestPaid;
            interestPaid = principal * (interest / 100);

            // Now calculate the total.
            decimal total = principal + interestPaid;

            // Output the result.
            Console.WriteLine(); // Skip a line.
            Console.WriteLine("Principal   = " + principal);
            Console.WriteLine("Interest    = " + interest + "%");
            Console.WriteLine();
            Console.WriteLine("Interest paid = " + interestPaid);
            Console.WriteLine("Total      = " + total);
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate . . .");
            Console.Read();
        }
    }
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_113_0.png)

CalculateInterest 程序首先提示用户输入他的姓名，使用 `WriteLine()` 向控制台写入一个字符串。要确切告诉用户你想要什么，并且如果可能的话，指定格式。用户对没有提供有用信息的提示（例如 `>`）反应不佳。

示例程序使用 `ReadLine()` 命令读取用户输入的任何内容；当用户按 Enter 键时，程序会以字符串形式返回输入的值。由于程序要查找的是 decimal 形式的本金，因此必须使用 `Convert.ToDecimal()` 命令转换输入字符串。结果存储在 `principalInput` 中。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_113_1.png)

`ReadLine()`、`WriteLine()` 和 `ToDecimal()` 命令都是方法调用的示例。*方法调用*将一些工作委托给程序的另一部分，称为*方法*。我在第 II 册中详细描述方法调用；这些特定的方法调用很直接。你应该能够通过我极具洞察力的解释性叙述理解其含义。如果那不管用，就忽略这段叙述。如果*那*还是不管用，请看第 II 册。

示例中的下一行检查 `principal`。如果它为负数，程序会输出一条礼貌的“nastygram”（令人不快的消息），表明用户弄错了。程序对利率也做同样的处理，然后执行前面在“介绍 if 语句”中概述的简单利息计算，并使用一系列 `WriteLine()` 命令输出结果。

程序使用合法的本金金额和高利贷般的利率（这在大多数州完全合法）生成以下输出：

```
Enter principal: 1234
Enter interest: 21

Principal      = 1234
Interest       = 21%

Interest paid = 259.14
Total          = 1493.14
Press Enter to terminate . . .
```

使用非法输入执行该程序会生成以下输出：

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative

Principal      = 1234
Interest       = 0%
Interest paid = 0
Total = 1234
Press Enter to terminate . . .
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_114_0.png)

缩进 if 子句中的行以增强可读性。C# 会忽略这种缩进，但对我们人类有帮助。大多数编程编辑器支持自动缩进，即只要你输入 if 命令，编辑器就会自动缩进。要在 Visual Studio 中设置自动缩进，请选择“工具”→“选项”。然后展开“文本编辑器”节点。接着展开 C#。最后单击“制表符”。在此页上，启用“智能缩进”，并根据偏好设置每级缩进的空格数。（本书中我使用每级缩进两个空格。）将制表符大小设置为相同的值。

## 检查 else 语句

有时，代码必须检查互斥的条件。例如，以下代码段将两个数字 a 和 b 中的最大值存储到变量 max 中：

```
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
  // . . . save a as the maximum.
  max = a;
}
// If a is less than or equal to b . . .
if (a <= b)
{
  // . . . save b as the maximum.
  max = b;
}
```

第二个 if 语句会导致不必要的处理，因为这两个条件是互斥的。如果 a 大于 b，它不可能小于或等于 b。C# 正是为这种情况定义了 else 子句。else 关键字定义了一个代码块，当 if 块未执行时，该代码块会被执行。

现在，用于计算最大值的代码段如下所示：

```
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
  // . . . save a as the maximum; otherwise . . .
  max = a;
}
else
{
  // . . . save b as the maximum.
  max = b;
}
```

```
}
    // Wait for user to acknowledge the results
    Console.WriteLine("Press Enter to terminate . . .");
    Console.Read();
}
}
```

程序首先从用户那里读取本金。如果本金为负数，程序会输出一条错误消息并退出。如果本金不是负数，控制权会传递到 else 子句，程序在那里继续执行。

在此示例中，利率测试得到了改进。在这里，程序要求利率为非负数（数学定律）且小于最大利率（司法定律——我只希望信用卡有利率上限）。这个 if 语句使用以下复合测试：

```
if (interest < 0 || interest > maximumInterest)
```

如果 interest 小于 0 或大于 maximumInterest，则此语句为真。注意，我在程序顶部声明 maximumInterest，而不是在这里将其硬编码为常量数字。硬编码是指在代码中直接使用值，而不是创建一个常量来保存它们。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_117_0.png)

在程序顶部定义重要的常量。给常量起一个描述性名称（而不仅仅是一个数字）使它易于查找，也更易于更改。如果该常量在代码中出现十次，你仍然只需做一处更改即可更改所有引用。

输入正确的本金但负的利率会生成以下输出：

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative or greater than 50.
Press Enter to terminate . . .
```

只有当用户同时输入合法的本金和合法的利率时，程序才会生成正确的计算：

```
Enter principal: 1234
Enter interest: 12.5

Principal   = 1234
Interest    = 12.5%
Interest paid = 154.250
Total       = 1388.250
Press Enter to terminate . . .
```

## 运行开关板

你经常希望针对许多不同的值测试一个变量。例如，maritalStatus 可能为 0 表示未婚，1 表示已婚，2 表示离异，3 表示

