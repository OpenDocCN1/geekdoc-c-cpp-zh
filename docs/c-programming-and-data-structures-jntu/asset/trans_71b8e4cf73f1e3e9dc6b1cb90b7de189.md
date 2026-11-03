
这个循环执行 1000 次而不产生任何输出；它只是造成时间延迟。注意，循环体只包含一个分号，称为空语句。这也可以写成

```
for (j=1000; j > 0; j = j-1);
```

这意味着，如果我们错误地在 for 语句末尾放置一个分号，C 编译器不会给出错误消息。该分号将被视为空语句，程序可能会产生一些无意义的结果。

## for 循环的嵌套

循环的嵌套，即一个 for 语句位于另一个 for 语句内部，在 C 中是允许的。例如，两个循环可以如下嵌套：

![](img/65953ea584e494f3d396b2252cb5ea53_179_0.png)

在 ANSI C 中，嵌套最多可达到 15 层；许多编译器允许更多层。循环应正确缩进，以便读者能轻松确定每个 for 语句中包含哪些语句。

示例 7.2 中讨论的打印乘法表的程序，可以使用嵌套 for 语句写得更简洁，如下所示：

```
for (row = 1; row <= ROWMAX; ++row)
{
    for (column = 1; column <= COLMAX; ++column)
    {
        y = row * column;
        printf("%4d", y);
    }
    printf("\n");
}
```

外层循环控制行，而内层循环控制列。

## 示例 7.4

一个班有 n 名学生参加 m 门科目的年度考试。图 7.5 给出了一个程序，用于读取每名学生在各科目中获得的分数，并计算和打印每名学生获得的总分。

```
Program
/ ************************************************************/
/ * ILLUSTRATION ON NESTED LOOPS */
/ ************************************************************/
#define FIRST  360
#define SECOND 240
main()
{
 int n, m, i, j;
 roll-number, marks, total;
 printf("Enter number of students and subjects\n");
 scanf("%d %d", &n, &m);
 printf("\n");
 for (i = 1; i <= n; ++i)
 {
 printf("Enter roll-number: ");
 scanf("%d", &roll-number);
 total = 0 ;
 printf("Enter marks of %d subjects for ROLL NO %d\n",m,roll-number);
 for (j = 1; j <= m; j++)
 {
 scanf("%d", &marks);
 total = total + marks;
 }
 printf("TOTAL MARKS = %d", total);
 if (total >= FIRST)
 printf("(First Division) \n\n");
 else if (total >= SECOND)
 printf("(Second Division) \n\n");
 else
 printf("*** F A I L *** \n\n");
 }
}
```

输出
Enter number of students and subjects
3 6
Enter roll-number : 8701
Enter marks of 6 subjects for ROLL NO 8701
81 75 83 45 61 59
TOTAL MARKS = 404 ( First Division )
Enter roll-number : 8702
Enter marks of 6 subjects for ROLL NO 8702
51 49 55 47 65 41
TOTAL MARKS = 308 ( Second Division )
Enter roll-number : 8704
Enter marks of 6 subjects for ROLL NO 8704
40 19 31 47 39 25
TOTAL MARKS = 201 ( *** F A I L ***)

图 7.5 嵌套 for 循环的示例

## 7.5 循环中的跳转

该程序使用两个 for 循环，一个用于控制学生人数，另一个用于控制科目数。由于学生人数和科目数都由程序请求，因此该程序可用于任意规模的班级和任意数量的科目。

外层循环包括三个部分：(1) 依次读取学生的学号；(2) 内层循环，在其中读取并累加每名学生的分数；(3) 打印总分并公布等级。

循环会反复执行一组操作，直到控制变量不再满足测试条件。循环重复的次数是预先确定的，并编写测试条件来实现这一点。有时，在执行循环时，可能希望跳过循环的一部分，或者在某个条件出现时立即离开循环。例如，考虑在一个包含比如 100 个名字的列表中搜索某个特定名字的情况。为读取并测试名字 100 次而编写的程序循环，必须在找到所需名字时立即终止。C 允许在循环内从一条语句跳转到另一条语句，也允许跳出循环。

### 跳出循环

可以使用 break 语句或 goto 语句实现提前退出循环。我们已经看到 break 在 switch 语句中的使用，以及 goto 在 if … else 结构中的使用。这些语句也可以在 while、do 或 for 循环中使用。图 7.6 和图 7.7 对它们进行了说明。

![](img/65953ea584e494f3d396b2252cb5ea53_181_0.png)

图 7.6 使用 break 语句退出循环

![](img/65953ea584e494f3d396b2252cb5ea53_182_0.png)

图 7.7 使用 goto 语句在循环内跳转并退出循环

当在循环内部遇到 break 语句时，会立即退出该循环，程序继续执行紧跟在循环之后的语句。当循环嵌套时，break 只会退出包含它的那个循环。也就是说，break 只会退出单个循环。

由于 goto 语句可以将控制转移到程序中的任何位置，因此它有助于在循环内提供分支。goto 的另一个重要用途是在发生错误时从深度嵌套的循环中退出。简单的 break 语句在这里无法起作用。

## 示例 7.5

图 7.8 中的程序说明了 break 语句在 C 程序中的使用。

该程序读取一组正值并计算它们的平均值。for 循环被编写为读取 1000 个值。然而，如果我们希望程序计算任意一组少于 1000 个值的平均值，那么必须在列表中最后一个值之后输入一个负数，以标记输入的结束。

每个值在被读取时都会进行测试，以判断它是否为正数。如果为正数，则将该值加到总和中；否则，循环终止。退出时，计算已读取值的平均值并打印结果。

```
Program
/* *************************************************************** */
/* USE OF break IN A PROGRAM */
/* *************************************************************** */
main()
{
 int m;
 float x, sum, average;
 printf("This program computes the average of a
 set of numbers\n");
 printf("Enter values one after another\n");
 printf("Enter a NEGATIVE number at the end.\n\n");
 sum = 0;
 for (m = 1; m <= 1000; ++m)
 {
 scanf("%f", &x);
 if (x < 0)
 break;
 sum += x;
 }
 average = sum/(float)(m-1);
 printf("\n");
 printf("Number of values = %d\n", m-1);
 printf("Sum = %f\n", sum);
 printf("Average = %f\n", average);
}
```

输出
This program computes the average of a set of numbers
Enter values one after another
Enter a NEGATIVE number at the end.
21 23 24 22 26 22 -1
Number of values = 6
Sum = 138.000000
Average = 23.000000

This program computes the average of a set of numbers
Enter values one after another
Enter a NEGATIVE number at the end.

21 23 24 22 26 22 -1
Number of values = 6
Sum = 138.000000
Average = 23.000000

图 7.8 在程序中使用 break

## 示例 7.6

图 7.9 给出了一个程序，用于在 -1 < x < 1 时计算级数 1/(1-x) = 1 + x + x^2 + x^3 + ..... + x^n，以达到 0.01% 的精度。goto 语句用于在达到所需精度时退出循环。

我们使用 for 语句来重复累加级数中的每一项。由于这是一个无穷级数，当项 x^n 达到所需精度时，函数的计算就会终止。决定循环操作次数的 n 值未知，因此我们任意取了一个值 100，这可能会也可能不会达到所需的精度水平。

```
/*
************** EXAMPLE OF EXIT WITH goto STATEMENT **************/
#define LOOP 100
#define ACCURACY 0.0001
main()
{
int n, term, sum;
printf("Input value of x: ");
scanf("%f", &x);
sum = 0;
for(term = 1, n = 1; n <= LOOP; ++n)
{
term *= x;
if(term <= ACCURACY)
goto EXIT;
sum += term;
}
term *= x;
/* EXIT FROM THE LOOP */
}
```
