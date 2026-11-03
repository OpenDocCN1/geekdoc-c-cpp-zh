
```
printf("\nFINAL VALUE OF N IS NOT SUFFICIENT\n");
printf("TO ACHIEVE DESIRED ACCURACY\n");
goto end;
output:
printf("\nEXIT FROM LOOP\n");
printf("Sum = %f; No. of terms = %d\n", sum, n);
end:
;
}
```
输出
输入 x 值 : 21
退出循环
和 = 1.265800; 项数 = 7
输入 x 值 : 75
退出循环
和 = 3.999774; 项数 = 34
输入 x 值 : 99
N 的最终值不足
以达到期望的精度

## 图 7.9 使用 goto 从循环退出

精度测试使用 if 语句进行，goto 语句在精度条件满足后立即退出循环。如果循环重复次数不足以产生期望的精度，程序将打印相应的消息。

请注意，在这里 break 语句并不太方便使用。正常退出和 break 退出都会将控制转移到循环后出现的同一条语句。但是，在当前问题中，正常退出会打印消息 "FINAL VALUE OF N IS NOT SUFFICIENT TO ACHIEVE DESIRED ACCURACY"，而强制退出会打印求值结果。注意末尾使用了空语句。这是必要的，因为程序不应以标签结尾。

## 跳过循环的一部分——continue 语句

在循环操作期间，在某些条件下可能需要跳过循环体的一部分。例如，在处理某些工作的申请时，我们可能希望排除属于某一类别的申请人的数据处理。在读取申请人的类别代码时，会进行测试以查看其申请是否应被考虑。如果不予考虑，则跳过处理申请详细信息的程序循环部分，并继续执行下一个循环操作。

与 break 语句类似，C 支持另一种类似的语句，称为 continue 语句。然而，与会导致循环终止的 break 不同，continue 正如其名称所示，会在跳过中间的任何语句后继续下一次迭代。continue 语句告诉编译器，“SKIP THE FOLLOWING STATEMENTS AND CONTINUE WITH THE NEXT ITERATION”。continue 语句的格式很简单

## continue;

在循环中使用 **continue** 语句的示例见图 7.10。在 **while** 和 **do** 循环中，**continue** 会使控制直接转到 *test-condition*，然后继续迭代过程。在 **for** 循环的情况下，*increment* 部分将在 *test-condition* 评估之前执行。

![](img/65953ea584e494f3d396b2252cb5ea53_185_0.png)

图 7.10 在循环中绕过并继续

## 示例 7.7

图 7.11 中的程序说明了 **continue** 语句的使用。

该程序计算一系列数字的平方根并打印结果。当输入数字 9999 时，过程停止。

如果序列中包含负数，则应绕过此类数字的平方根求值过程，因为负数的平方根未定义。**continue** 语句用于实现这一点。程序还打印一条消息，说明该数字为负数，并对负数进行计数。

最终输出包括已求值的正数值数量和遇到的负项数量。

```
Program
/***************************************************************/
/*              USE OF continue STATEMENT                     */
/***************************************************************/

#include <math.h>
main()
{
    int count, negative;
    double number, sqroot;
    printf("Enter 9999 to STOP\n");
    count = 0;
    negative = 0;
    while (count <= 100)
{
    printf("Enter a number : ");
    scanf("%lf", &number);
    if (number == 9999)
        break;    /* EXIT FROM THE LOOP */
    if (number <0)
    {
        printf("number is negative\n\n");
        negative++;
        continue;    /* SKIP REST OF THE LOOP */
    }
    sqroot = sqrt(number);
    printf("\nNumber    = %lf\nSquare root = %lf\n", number, sqroot);
    count++;
}
printf("Number of items done    = %d\n", count);
printf("\nNegative items          = %d\n", negative);
printf("END OF DATA\n");
```
输出
输入 9999 停止
输入一个数字 : 25.0
数字        = 25.000000
平方根   = 5.000000
输入一个数字 : 40.5
数字        = 40.500000
平方根   = 6.363961
输入一个数字 : -9
数字为负数
输入一个数字 : 16
数字        = 16.000000
平方根   = 4.000000
输入一个数字 : -14.75
数字为负数
输入一个数字 : 80
数字        = 80.000000
平方根   = 8.944272
输入一个数字 : 9999
已处理的项目数    = 4
负项          = 2
数据结束

图 7.11 continue 语句的使用

## 避免使用 goto

如前所述，避免使用 goto 是一个良好的实践。有很多原因。当使用 goto 时，许多编译器会生成效率较低的代码。此外，使用过多会使程序逻辑复杂化并使程序难以阅读。通过仔细的程序设计可以避免使用 goto。如果绝对需要使用任何 goto，则应进行文档记录。以下 goto 跳转会导致问题，因此必须避免：

![](img/65953ea584e494f3d396b2252cb5ea53_187_0.png)

## 简洁的测试表达式

我们经常在 if、for、while 和 do 语句中使用测试表达式，这些表达式会被求值并与零进行比较以做出分支决策。由于每个整数表达式都有真/假值，因此我们无需显式与零进行比较。例如，表达式 x 在 x 不为零时为真，在 x 为零时为假。应用 ! 运算符，我们可以在不使用任何关系运算符的情况下编写简洁的测试表达式。

```
if (expression == 0)
```

等价于

```
if (! expression)
```

同样，

```
if (expression != 0)
```

等价于

```
if (expression)
```

## 示例

If (m%5 == 0 && n%5 == 0) 与 if (!(m%5) && !(n%5)) 相同

## 7.6 结构化编程

结构化编程是对程序设计和开发的一种方法。它是使程序的逻辑易于理解的学科，仅使用三种基本控制结构：

- Sequence (straight line) structure
- Selection (branching) structure
- Repetition (looping) structure

虽然序列和循环结构足以满足编程的所有要求，但在某些情况下选择结构更方便。

## 决策与循环 7.21

使用结构化编程技术有助于确保设计良好的程序，与非结构化程序相比，更易于编写、阅读、调试和维护。结构化编程不鼓励使用 goto、break 和 continue 等跳转语句实现无条件分支。在其最纯粹的形式中，结构化编程与“goto-less 编程”同义。不要使用 goto 语句！

## 案例研究

## 1. 二项式系数表

问题：二项式系数用于二项分布和多组件冗余系统可靠性的研究。它由 B(m, x) = (m choose x) = m! / (x! (m-x)!) 给出，m >= x

需要一个二项式系数表来确定任意 m 和 x 的二项式系数。

问题分析：二项式系数可以递归计算如下：B(m, x) = B(m, x - 1) * [(m - x + 1) / x] ，x = 1, 2, 3, ..., m

此外，B(m, 0) = 1 B(0, x) = 1

也就是说，当 x 为零或 m 为零时，二项式系数为一。图 7.12 中的程序打印 m = 10 的二项式系数表。程序采用一个 do 循环和一个 while 循环。

```
#include <stdio.h>
/* EVALUATION OF BINOMIAL COEFFICIENTS */
#define MAX 10
{
int m, x, binom;
printf("m x\n");
for (m=0; m<=10; ++m)
printf("%4d", m);
printf("\n");
m=0;
do {
printf("%4d ", m);
x=0; binom=1;
while (x <= m) {
printf("%4d", binom);
binom = binom * (m - x +1) / x;
x++;
}
printf("\n");
m++;
} while (m <=10);
}
```
