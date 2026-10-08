
```csharp
        }

        // 计算每月利息和新余额。

        public void CalculateMonthCharges(int month, int numPayments)

        {

            double payment = paymentAmount;

            int monthInterest = rate / 12 * balance;

            if (month == numPayments)

            {

                principal = balance;

                payment = balance + monthInterest;

            }

            else

            {

                principal = payment - monthInterest;

            }

            balance -= principal;

        }

        // 计算贷款存期内的总利息。

        public void DetermineTotalInterestPaid()

        {

            int totalInterestPaid = 0;

            balance = loanAmount;

            for (int month = 1; month <= numPayments; month++)

            {

                CalculateMonthCharges(month, numPayments);

                totalInterestPaid += monthInterest;

            }

        }

    }

}
```

```csharp
/* LoanApp.cs
* 用于测试 Loan 类。
* 提示用户输入贷款金额、
* 利率和贷款的
* 期限。调用方法显示
* 还款金额和摊还
* 计划表。允许进行多次
* 计算。
 */

using System;
using System.Windows.Forms;
namespace Loan
{
    class LoanApp
    {
        static void Main()
        {
            int years;
            double loanAmount;
            double interestRate;
            string inValue;
            char anotherLoan = 'N';
            do {
                GetInputValues(out loanAmount, out interestRate, out years);
                Loan ln = new Loan(loanAmount, interestRate, years);
                ln.DeterminePaymentAmount();
                Console.WriteLine();
                Console.WriteLine(ln.ReturnAmortizationSchedule());
                ln.DetermineTotalInterestPaid();
                Console.WriteLine("Payment Amount: {0:C}", ln.PaymentAmount);
                Console.WriteLine("Interest Paid over Life of Loan: {0:C}", ln.TotalInterestPaid);
                Console.Write("Do another Calculation? (Y or N)");
                inValue = Console.ReadLine();
                anotherLoan = Convert.ToChar(inValue);
            } while ((anotherLoan == 'Y') || (anotherLoan == 'y'));
        }

        // 提示用户输入贷款数据。
        static void GetInputValues(out double loanAmount, out double interestRate, out int years)
        {
            string sValue;
            Console.Write("Loan Amount: ");
            sValue = Console.ReadLine();
            loanAmount = Convert.ToDouble(sValue);
            Console.Write("Interest Rate (as a decimal value): ");
            sValue = Console.ReadLine();
            interestRate = Convert.ToDouble(sValue);
            Console.Write("Number of Years to Finance: ");
            sValue = Console.ReadLine();
            years = Convert.ToInt32(sValue);
        }
    }
}
```

使用表 6-6 最后行的输入值，输出如图 21 所示。

![](img/45e6f245af3139d967c3186f)

输出使用了固定 `F` 和货币 `C` 字符串。

## 第 6 章 重复指令

## 代码标准

为了开发可靠且可维护的应用程序，你必须遵循代码标准和最佳实践。行业内存在多种标准。标准存在差异：有些基于个人喜好，有些则基于“我们一直以来都是这样做的”的格言。语言选择也存在差异。最重要的是你选择一种方法并始终坚持。

循环语句中最重要的考虑因素之一是可读性。下文描述了最佳实践，涉及大括号的一致放置和空格的使用。

### 大括号放置的指南

大括号应该放在单独一行，而不是与循环条件表达式在同一行，如下：

```csharp
for (int i = 0; i < 10; i++)
{
```

如上所示，对齐起始大括号和结束大括号。

大括号是可选的。当循环体包含多个语句时，大括号是必须的。对于选择语句（如 `if` 语句），许多开发者会对所有循环使用大括号。在本本书中，只有当有两个或多个执行语句时才添加大括号。

### 空格规范

在比较运算符前后使用单个空格，如下：
`while (a < b)`

不要在表达式内部括号内放置额外的空格，如上所示。

在循环体内部，将每个执行语句放在单独一行。

在显示错误消息时，除了告诉用户哪里错了，消息还应该告诉用户应该做什么来解决问题。

使用 `for` 语句进行计数控制循环。计数变量可以在循环结构的一部分声明并递增。

## 资源

你可能想要探索的额外网站：

- [Loops—C# Tutorial](http://csharp.net-tutorials.com/basics/loops/)
- [C# Station Tutorial—Control Statements—Loops at](http://www.csharp-station.com/Tutorials/Lesson04.aspx
- [C# and Loops at](http://www.homeandlearn.com/uk/csharp/csharp_s3p5.html
- [Dot Net Perls—C# and Loops at](http://dotnetperls.com/loops

1. 大多数编程语言中的构造结构顺序、选择和迭代。
2. 根据预定义的条件，迭代允许你识别并组合一个或多个需要重复的语句。
3. C# 中提供的循环结构包括 `while`、`do...while`、`for` 和 `foreach` 语句。`do...while` 循环是后测试的；其他是先测试结构。在先测试中，在执行循环中的任何语句之前，会先测试条件表达式。
4. 当你知道语句必须的次数时，可以使用计数控制循环。
5. 无限循环没有正常终止的机制。当循环的条件表达式永远不为假，或者循环存在某些固有特性或问题时，就会发生无限循环。
6. 使用计数控制循环时，仔细考虑测试用例并检查端点很重要，以确保它们被正确使用以避免差错（off-by-one errors）。
7. 哨兵值控制循环也称为不定循环。当在循环执行之前不知道重复次数时，它们非常有用。对于交互式输入，选择一个哨兵值并告诉用户输入该值以停止。哨兵值不应该被处理。

8. `MessageBox.Show()` 方法用于以类似于 Windows 应用程序的格式向用户显示信息。

9. 状态控制循环（也称为标志控制循环）使用一个特殊变量——而不是存储正在处理的数据变量。在状态控制循环中，当特殊变量的值改变时，循环体将停止。

10. `for` 语句被认为是 `while` 语句的特殊形式。它将初始化、测试和更新全部封装在一行中。

11. `foreach` 语句用于迭代或遍历集合（例如数组）。它不需要在处理所有数据后对循环变量进行递增和测试。

12. 在 `do...while` 后测试循环结构中，语句在测试条件表达式之前会执行一次。

13. 循环可以包含在另一个循环的体中。当这种情况发生时，内部嵌套循环在外部循环进行第二次测试之前会完全完成。

14. C# 提供了许多跳转语句，可以改变程序的控制流。它们包括 `break`、`continue`、`goto`、`throw` 和 `return` 语句。

15. 当遇到 `continue` 语句时，最近的包含它的 `while`、`do...while`、`for` 或 `foreach` 循环将开始新的迭代。

16. `break` 和 `continue` 语句在循环中使用应尽量少。

17. 关于关于使用哪种类型的循环的决策——如果你知道循环将至少会执行一次，那么 `do..while` 是一个很好的选择。当数值变量在循环每次迭代中按固定的量发生变化时，`for` 语句可能是最佳选择。`while` 语句可以编写任何类型的循环。

## 练习

1. 编程语言中需要循环：
- a. 为了便于数据的顺序处理
- b. 为了允许对变量进行分析以进行额外处理
- c. 为了处理存储在硬盘上的文件
- d. 为了允许语句重复
- e. 以上所有

2. 为了编写一个哨兵值控制循环来计算佛罗里达 7 月的平均温度，哨兵值的最佳选择是：
- a. 67
- b. 1000
- c. 100
- d. “high temperature”
- e. 以上都不是

3. 哪种循环结构只能用于集合或数组？
- a. foreach
- b. for
- c. while
- d. do...while
- e. 以上都不是

4. 如果循环体必须至少执行一次，哪种循环结构是最佳选择？
- a. foreach
- b. for
- c. while
- d. do...while
- e. 以上都不是

5. 如果循环使用一个数值，该数值在每次迭代中递增三，直到达到 1000，哪种循环结构可能是最佳选择？
- a. foreach
- b. for
- c. while
- d. do...while
- e. 以上都不是

6. 与 `while` 语句配合使用时，哪个跳转语句会导致执行在循环体内停止并立即将控制转移到条件表达式？
- a. break
- b. goto
- c. return
- d. continue
- e. 以上都不是

7. 下列哪个是有效的 C# 先测试条件表达式，允许只要计数器小于 10 就执行循环？
- a. do while (counter < 10)
- b. while (counter < 10)
- c. foreach (counter < 10)
- d. 以上不是
- e. 以上都是

8. 下列哪种 `for` 语句的执行次数与以下 `while` 语句相同？
```csharp
int num = 10;
while (...)
{
  Console.WriteLine(num);
}
```
- a. for (num = 0; num < 10; num++)
- b. for (num = 1; num < 10; num++)
- c. for (num = 10; num++)
- d. for (num = 10; num--)
- e. 以上都不是

9. 以下代码的输出是什么？
```csharp
int aValue = 1;
do
{
  aValue++;
  Console.Write(aValue);
} while (aValue < 3);
```
- a. 2
- b. 23
- c. 234
- d.

10. 如果 `aValue`、`i` 和 `n` 是变量，以下程序会产生 4 6 8 10 吗？
```csharp
int i = 0;
while (i < n)
{
  Console.Write(i);
  i++;
}
```
哪个 `for (int n = 0; ??)` 应该替换问号？

11. 下列代表先测试循环？
- a. while
- b. do...while
- c. for
- d. 以上都是

14. 如果你打算将语句块放在循环体中，你必须将块括在：
- a. 圆括号
- b. 方括号
- c. 引号
- d. 大括号
- e. 以上都不是

问题 15-17 参考以下程序段：
```csharp
int i = 0, g = 0, s = 0, t = 0, z = 0;
string inValue;
while (i < 5)
{
    inValue = Console.ReadLine();
    t = Convert.ToInt32(inValue);
    s = s + t;
    if (t > -1)
        g = g + 1;
    else
        z = z + 1;
    i = i + 1;
}
```

15. `while` 语句的体执行了多少次？
- a. 一次
- b. 从未
- c. 四次
- d. 五次
- e. 直到输入5 或更大的数字

16. 循环执行结束时存储在 `z` 中的值可以描述为：
- a. 输入的正数个数
- b. 所有正数的总和
- c. 输入的负数个数
- d. 所有负数的总和
- e. 以上都不是

17. 该循环最好被分类为：
- a. 计数控制循环
- b. 哨兵值控制循环
- c. 状态控制循环
- d. 标志控制循环
- e. 以上都不是

20. 下列条件表达式的结果是什么？

```csharp
int i = 0;
while (i < 10);
i++;
Console.Write(i);
```

- a. 123456789
- b. 012345678910
- c. 0123456789
- d. 无限循环
- e. 以上均不是

21. 将以下 `do...while` 循环转换为 `for` 循环和 `while` 循环。逻辑发生变化了吗？如果是，请解释。

```csharp
int counter = 100;
do
{
    Console.WriteLine(counter);
    counter--;
}
while (counter > 0);
```

22. 编写一个 `for` 循环，从 10 开始到 100，显示每第三个数字。

23. 编写一个哨兵控制的 `while` 循环，允许输入任意数量的温度。计算并显示平均温度。

24. 创建一个循环体，生成 25 到 75 之间的随机数。编写一个状态控制的循环，累加所有生成的随机数，直到生成大于 60 的数值为止。当循环停止时，显示生成的有效数量以及这些值的总和。

25. 手动运行（Desk run）或跟踪以下代码段，显示进入每个变量的每一个值。

```csharp
for (i = 0; i < 3; i++)
    for (j = 4; j >= 0; j--)
        Console.WriteLine("{0}\t{1}", i, j);
```
