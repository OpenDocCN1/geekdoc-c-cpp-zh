
**程序**

```c
#include <stdio.h>
#include <conio.h>
void main()
{
    int num,i,y,x=40;
    clrscr();
    printf("\nEnter a number for \ngenerating the\npyramid:\n");
    scanf("%d",&num);
    for(y=0;y<=num;y++)
    {
        gotoxy(x,y+1);
        for(i=0-y;i<=y;i++)
        printf("%3d",abs(i));
        x=x-3;
    }
    getch();
}
```

**输出**

```text
Enter a number for
generating the pyramid:

7

          0
        1 0 1
      2 1 0 1 2
    3 2 1 0 1 2 3
  4 3 2 1 0 1 2 3 4
5 4 3 2 1 0 1 2 3 4 5
6 5 4 3 2 1 0 1 2 3 4 5 6
7 6 5 4 3 2 1 0 1 2 3 4 5 6 7
```

**图 8.8** *构建金字塔的程序*

## 选择循环

给定一个问题，程序员首先关心的是决定要使用哪种循环结构。要在 C 支持的三种循环中选择一种，我们可以使用以下策略：

- 分析问题，看它需要前测试循环还是后测试循环。
- 如果它需要后测试循环，那么我们只能使用一种循环，即 **do while**。
- 如果它需要前测试循环，那么我们有两种选择：**for** 和 **while**。
- 决定循环终止需要基于计数器的控制还是基于哨兵值的控制。
- 如果基于计数器的控制是必要的，则使用 **for** 循环。
- 如果需要基于哨兵值的控制，则使用 **while** 循环。
- 请注意，计数器控制循环和哨兵控制循环都可以由所有三种控制结构实现。

由于 **goto** 语句可以将控制转移到程序中的任何位置，因此它在循环内提供分支很有用。**goto** 的另一个重要用途是在发生错误时从深度嵌套的循环中退出。简单的 **break** 语句在这里无法做到。

![](img/11b034a94fc590add0a7808250a38792_282_0.png)

### 已解答问题 8.8

图 8.11 中的程序演示了 break 语句在 C 程序中的使用。

该程序读取一系列正值并计算它们的平均值。**for** 循环被编写为读取 1000 个值。然而，如果我们希望程序计算任意少于 1000 个值的数据集的平均值，那么必须在列表最后一个值之后输入一个“负数”，以标记输入结束。

**程序**

```c
main()
{
    int m;
    float x, sum, average;
    printf("This program computes the average of a\n           set of numbers\n");
    printf("Enter values one after another\n");
    printf("Enter a NEGATIVE number at the end.\n\n");
    sum = 0;
    for (m = 1 ; m <= 1000 ; ++m)
    {
        scanf("%f", &x);
```

**程序**

```c
#define LOOP 100
#define ACCURACY 0.0001
main()
{
    int n;
    float x, term, sum;
    printf("Input value of x : ");
    scanf("%f", &x);
    sum = 0 ;
    for (term = 1, n = 1 ; n <= LOOP ; ++n)
    {
        sum += term ;
        if (term <= ACCURACY)
            goto output; /* EXIT FROM THE LOOP */
        term *= x ;
    }
    printf("\nFINAL VALUE OF N IS NOT SUFFICIENT\n");
    printf("TO ACHIEVE DESIRED ACCURACY\n");
    goto end;
output:
    printf("\nEXIT FROM LOOP\n");
    printf("Sum = %f; No. of terms = %d\n", sum, n);
end:
    ;    /* Null Statement */
}
```

**输出**

```text
Input value of x : .21
EXIT FROM LOOP
Sum = 1.265800; No. of terms = 7
Input value of x : .75
EXIT FROM LOOP
Sum = 3.999774; No. of terms = 34
Input value of x : .99
FINAL VALUE OF N IS NOT SUFFICIENT
TO ACHIEVE DESIRED ACCURACY
```

**图 8.12** *使用 goto 退出循环*

```c
while (count <= 100)
{
    printf("Enter a number : ");
    scanf("%lf", &number);
    if (number == 9999)
        break;        /* EXIT FROM THE LOOP */
    if (number < 0)
    {
        printf("Number is negative\n\n");
        negative++ ;
        continue; /* SKIP REST OF THE LOOP */
    }
    sqroot = sqrt(number);
    printf("Number    = %lf\n Square root = %lf\n\n",
            number, sqroot);
    count++ ;
}
printf("Number of items done = %d\n", count);
printf("\n\nNegative items = %d\n", negative);
printf("END OF DATA\n");
}
```

**输出**

```text
Enter 9999 to STOP
Enter a number : 25.0
Number        = 25.000000
Square root   = 5.000000
Enter a number : 40.5
Number        = 40.500000
Square root   = 6.363961
Enter a number : -9
Number is negative
Enter a number : 16
Number        = 16.000000
Square root   = 4.000000
Enter a number : -14.75
Number is negative
Enter a number : 80
Number        = 80.000000
Square root   = 8.944272
Enter a number : 9999
Number of items done = 4
Negative items      = 2
END OF DATA
```

**图 8.14** *continue 语句的使用*

### 学习成果

- 在测试表达式中使用错误的关系运算符是一个常见错误。确保循环恰好执行所需次数。LO 8.3.1
- 避免使用 = 代替 == 运算符这一常见错误。LO 8.3.1
- 不要对浮点值进行相等比较。LO 8.3.1
- 在循环体中对变量重复执行操作时，请确保在进入循环之前已正确初始化该变量。LO 8.3.1
- 正确缩进循环体中的语句，以增强可读性和可理解性。LO 8.3.1
- 强烈建议在循环前后以及终止注释处使用空白。LO 8.3.1
- 不要忘记在 do ...while 语句末尾放置分号。LO 8.3.2
- 不要忘记将递增语句放在 while 或 do...while 循环的循环体中。LO 8.3.2
- 避免使用 while 和 for 语句实现出口控制（后测试）循环。应使用 do... while 语句。同样，不要将 do...while 用于前测试循环。LO 8.3.2
- 在 while 或 for 语句的控制表达式后放置分号不是语法错误，但很可能是逻辑错误。LO 8.3.3
- 在 for 语句的头部使用逗号而不是分号是错误的。LO 8.3.3
- 不要在 for 语句和循环体中同时更改控制变量。这是逻辑错误。LO 8.3.3
- 尽管允许将初始化、测试和递增部分放在 for 语句头部之外，但应尽可能避免这样做。LO 8.3.3
- 尽管允许在初始化和递增部分使用算术表达式，但要注意求值过程中的舍入误差和截断误差。LO 8.3.3
- 尽管 for 之前的语句和循环体中的语句可以放在 for 头部，但应避免这样做，因为这会使程序更难阅读。LO 8.3.3
- 在任何循环中使用 break 和 continue 语句都被视为非结构化编程。尽可能消除这些跳转语句的使用。LO 8.3.4
- 避免在程序中的任何地方使用 goto。LO 8.3.4
- 仅在必须退出程序时才使用函数 exit()。LO 8.3.4

### 需要记住的关键术语

- **控制语句：** 测试某些条件并指导循环体的重复执行。LO 8.3.1
- **程序循环：** 重复执行一系列语句，直到满足循环终止的某些条件。LO 8.3.1
- **while 语句：** 是一种入口控制循环，先计算测试条件，如果条件为真，则执行循环体。LO 8.3.1
- **do 语句：** 先执行循环体，然后在随后的 while 语句中计算测试条件。LO 8.3.2
- **break 语句：** 终止循环，并将程序控制转移到紧跟在循环之后的语句。LO 8.3.4

**程序**

```c
#define N 5
main()
{
    int value[N];
    int i, j, n, x;
    for (n=0; n < N; ++n)
    {
        printf("Enter employees in Group - %d : ",n+1);
        scanf("%d", &x);
        value[n] = x;
        printf("%d\n", value[n]);
    }
    printf("\n");
    printf("\n");
    for (n = 0 ; n < N ; ++n)
    {
        for (i = 1 ; i <= 3 ; i++)
        {
            if ( i == 2)
                printf("Group-%ld |",n+1);
            else
                printf("|");
            for (j = 1 ; j <= value[n]; ++j)
                printf("*");
            if (i == 2)
                printf("(%d)\n", value[n]);
            else
                printf("\n");
        }
        printf("\n");
    }
}
```

**输出**

```text
Enter employees in Group - 1 : 12
12
Enter employees in Group - 2 : 23
23
Enter employees in Group - 3 : 35
35
Enter employees in Group - 4 : 20
```

