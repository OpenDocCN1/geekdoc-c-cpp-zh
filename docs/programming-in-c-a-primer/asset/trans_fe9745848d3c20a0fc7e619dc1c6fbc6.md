

# 复习题

6.1 判断以下说法是否正确：

- (a) 当 if 语句嵌套时，最后一个 else 会与最近的没有 else 的 if 关联。
- (b) 一个 if 可以有多个 else 子句。
- (c) switch 语句总可以用一系列 if....else 语句替换。
- (d) switch 表达式可以是任意类型。
- (e) 遇到 break 语句时程序会停止执行。
- (f) if 语句中的表达式必须始终解析为整数值。
- (g) 一组嵌套的 if....else 语句可以用 else if 阶梯替换。
- (h) switch () 中的每个 case 标签都应有一个关联的 break 语句。
- (i) 当 default 是最后一个时，break 语句在 default case 中是可选的。
- (j) 条件运算符 ?: 可以用 if else 构造替换。
- (k) switch 中的 default 必须是 case 列表中的最后一条语句。
- (l) default 是 switch 语句中的可选 case。

6.2 switch 语句的执行顺序是什么？

6.3 if 语句有哪些形式及其具体用途？

6.4 switch 语句与 if 语句有何不同？

6.5 找出以下每个 if 段中的错误，如有的话：

- (a) if(x+y = z && y>0)
- (b) if(p<0) || (q<0)

6.6 以下是一段程序：
x = 1;
y = 1;
if(n>0)
x = x+1;
y = y-1;
如果 n 假设为 (a)1 和 (b) 0 的值，x 和 y 的值会是多少。

6.7 不使用复合关系重写以下每个：

- (a) if(grade<=59 && grade>=50)
  second = second + 1;
- (b) if(number>100 || number<0)
  System.Console.Write("Out of range");
  else
  sum = sum + number;
- (c) if ((M1>60 && M2>60) || T>200)
  y=1;
  else
  y=0;

6.8 switch 语句中的“fallthrough”是什么？在 C# 中是如何实现的？

6.9 你在什么情况下认为使用 goto 语句是必要的？

6.10 为以下每个编写伪代码：

- (a) 从键盘读取两个数字并显示这两个数字中较大的一个
- (b) 从键盘读取三个数字并显示这三个数字中最小的一个。

6.11 与 if...else 语句相比，你会在什么情况下使用条件运算符 ?:？

6.12 识别以下语句中的错误。

(a) if (code = = 1)
    Console.WriteLine("Pass");
else;
Console.WriteLine("Fail");

(b) if (code > 1);
    a = b + c
else
    a = 0

# 调试练习

6.1 找出以下程序中的错误。

```
using System;
class TernaryExample
{
    static void Main()
    {
        int num = 3;
        string result = (num < 2) ? "True" : "False";
        Console.WriteLine(result);
    }
}
```

6.2 调试下面给出的程序。

```
using System;
class StudentRecord
{
    static void Main(string[] args)
    {
        Console.WriteLine("Enter the name of the student: ");
        string name = Console.ReadLine();

        Console.WriteLine("Enter the grade for the student: ");
        string grade = Console.ReadLine();
        if (grade == "a")
            Console.WriteLine("{0} is an Outstanding student.",name);
            Console.WriteLine("You have received a scholarship.");
        else if (grade == "b")
            Console.WriteLine("{0} is a Good student.",name);
        else if (grade == "c")
            Console.WriteLine("{0} is an Average student.",name);
        else if (grade == "d")
            Console.WriteLine("{0} Needs more practice.",name);
        else
            Console.WriteLine("{0} Need a lot of practice.",name);
    }
}
```

# 编程练习

6.1 编写一个程序，将 0 到 20 之间所有的奇数相加。使用简单的 if 和 goto 语句形成操作循环

6.2 修改上述程序，使其也将 0 到 20 之间的所有偶数相加

6.3 编写一个程序，找出大于 100 且小于 200 的所有能被 7 整除的整数的个数和总和。

6.4 给出两个未知数 x₁ 和 x₂ 的两个线性方程组如下：
ax₁ + bx₂ = m
cx₁ + dx₂ = n
该组有唯一解
x₁ = (md + bn)/(ad - cb)
x₂ = (na + mc)/(ad - cb)
前提是分母 ad - cb 不等于零。
编写一个程序读取常数 a、b、c、d、m 和 n 的值并计算 x₁ 和 x₂ 的值。如果 ad – cb = 0，则应打印适当的提示信息。

6.5 给定一个从 0 到 100 的分数列表，编写一个程序计算并打印获得分数的学生人数
(a) 在 81 到 100 范围内，          (b) 在 61 到 80 范围内，
(c) 在 41 到 60 范围内，和      (d) 在 0 到 40 范围内。
程序应使用最少的 if 语句。

6.6 报考专业课程需满足以下条件：
(a) 数学成绩 >= 60
(b) 物理成绩 >= 50
(c) 化学成绩 >= 40
(d) 三科总分 >= 200
（或）
数学和物理总分 >= 150
给定三科成绩，编写一个程序处理申请，列出符合条件的考生。

6.7 编写一个程序打印如下所示的二维平方根表，以提供从 0 到 9.9 的任意数字的平方根。例如，值 x 给出 3.2 的平方根，y 给出 3.9 的平方根。

# 平方根表

| NUMBER | 0.0 | 0.1 | 0.2 | ...... | 0.9 |
| 0.0 |  |  |  |  |  |
| 1.0 |  |  |  |  |  |
| 2.0 |  |  |  |  |  |
| 3.0 |  |  | x |  | y |
| . |  |  |  |  |  |
| . |  |  |  |  |  |
| 9.0 |  |  |  |  |  |

6.8 下面是 Floyd 的三角形

1
2 3
4 5 6
7 8 9 10
11 ...........15
.
.
79 ........... 91

- (a) 编写一个程序打印此三角形。
- (b) 修改程序以产生以下形式的 Floyd 三角形：
  1
  0 1
  1 0 1
  0 1 0 1
  1 0 1 0 1

6.9 一家布料商店宣布了以下购买商品的季节性折扣：

| PURCHASE AMOUNT | DISCOUNT |  |
|  | MILL CLOTH | HANDLOOM ITEMS |
| 0 – 100 |  | 5.0% |
| 101 – 200 | 5.0% | 7.5% |
| 201 – 300 | 7.5% | 10.0% |
| Above 300 | 10.0% | 15.0% |

编写一个使用 switch 和 if 语句计算客户需支付的净金额的程序。

6.10 编写一个程序读取 x 的值并计算以下函数

y = { 1 for x > 0
      0 for x = 0
     -1 for x < 0 }

- 使用
- (a) 嵌套 if 语句
- (b) else if 语句，和
- (c) 条件运算符?

# 7

# 决策与循环

# 7.1 引言

计算机非常适合执行重复操作。它可以做十次、百次甚至一万次。每种计算机语言都必须具有指示计算机执行此类重复任务的功能。反复执行一段语句的过程称为循环。块中的语句可能被执行任意次数，从零次到无限次。如果循环永远持续下去，则称为无限循环。C# 支持此类循环功能，使我们能够开发包含重复过程的简洁程序，而无需使用 goto 语句等无条件分支语句。

在循环中，一系列语句会一直执行，直到满足循环终止的某些条件。程序循环因此由两个段组成，一个称为循环体，另一个称为控制语句。控制语句测试某些条件，然后指示重复执行循环体中包含的语句。

根据循环中控制语句的位置，控制结构可分为入口控制循环或出口控制循环。图 7.1 中的流程图说明了这些结构。在入口控制循环中，控制条件在循环执行开始前进行测试。如果条件不满足，则循环体将不会执行。在出口控制循环的情况下，测试在循环体末尾进行，因此循环体无条件地第一次执行。

测试条件应仔细说明，以便执行所需次数的循环。假设测试条件最终会将控制转移出循环。如果由于某种原因没有这样做，控制会设置一个无限循环，循环体会被一次又一次地执行。

一般来说，循环过程包括以下四个步骤：

- 1. 设置和初始化计数器。
- 2. 执行循环中的语句。
- 3. 测试循环执行的指定条件。
- 4. 增加计数器。

测试可以是确定循环是否已执行指定次数，或者确定是否满足特定条件。

C# 语言提供了四种执行循环操作的构造。它们是：

- 1. while 语句
- 2. do 语句
- 3. for 语句
- 4. foreach 语句

