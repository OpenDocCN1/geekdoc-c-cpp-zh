
注意，内层循环的 **printf** 不包含任何换行符（`\n`）。这使得所有行值可以在一行中打印。外层循环中的空 **printf** 会启动一个新行，以打印下一行。

## 8.4 for 语句

**LO 8.3**

### 简单的“for”循环

**for** 循环是另一种*入口控制*循环，它提供了更简洁的循环控制结构。**for** 循环的一般形式为

```
for ( initialization ; test-condition ; increment)
{
    body of the loop
}
```

**for** 语句的执行过程如下：

- 1. *控制变量的初始化*首先完成，使用诸如 `i = 1` 和 `count = 0` 的赋值语句。变量 `i` 和 `count` 称为循环控制变量。
- 2. 使用测试条件检验控制变量的值。*测试条件*是一个关系表达式，例如 `i < 10`，它决定循环何时退出。如果条件为*真*，则执行循环体；否则循环终止，并继续执行紧跟在循环之后的语句。
- 3. 当循环体执行时，在计算循环中的最后一条语句后，控制权转回 **for** 语句。现在，使用诸如 `i = i+1` 的赋值语句对控制变量进行*递增*，并再次检验控制变量的新值，看它是否满足循环条件。如果满足条件，则再次执行循环体。此过程持续进行，直到控制变量的值不满足测试条件为止。

> **注意** *C99 增强了 **for** 循环，允许在初始化部分声明变量。参见附录“C99 特性”。*

考虑以下程序段：

```
for ( x = 0 ; x <= 9 ; x = x+1)
{
    printf("%d", x);
}
printf("\n");
```

这个 **for** 循环执行 10 次，并在一行中打印数字 0 到 9。括号内的三个部分必须用分号分隔。注意，*增量部分 x = x+1* 末尾没有分号。

**for** 语句允许*负增量*。例如，上面讨论的循环可以写成如下形式：

## 例题 8.3

图 8.4 中的程序使用 for 循环打印幂次为 0 到 20 的“2 的幂”表，包括正幂和负幂。

程序

```c
main()
{
    long int p;
    int n;
    double q;
    printf("--------------------------------------\n");
    printf("2 to power n       n       2 to power -n\n");
    printf("--------------------------------------\n");
    p = 1;
    for (n = 0; n < 21 ; ++n) /* LOOP BEGINS */
    {
        if (n == 0)
            p = 1;
        else
            p = p * 2;
        q = 1.0/(double)p ;
        printf("%10d %10d %20.12lf\n", p, n, q);
    }                     /* LOOP ENDS */
    printf("--------------------------------------\n");
}
```

输出

| 2 的 n 次幂 | n | 2 的 -n 次幂 |
| :---: | :---: | :---: |
| 1 | 0 | 1.000000000000 |
| 2 | 1 | 0.500000000000 |
| 4 | 2 | 0.250000000000 |
| 8 | 3 | 0.125000000000 |
| 16 | 4 | 0.062500000000 |
| 32 | 5 | 0.031250000000 |
| 64 | 6 | 0.015625000000 |
| 128 | 7 | 0.007812500000 |
| 256 | 8 | 0.003906250000 |
| 512 | 9 | 0.001953125000 |
| 1024 | 10 | 0.000976562500 |
| 2048 | 11 | 0.000488281250 |
| 4096 | 12 | 0.000244140625 |
| 8192 | 13 | 0.000122070313 |
| 16384 | 14 | 0.000061035156 |
| 32768 | 15 | 0.000030517578 |
| 65536 | 16 | 0.000015258789 |
| 131072 | 17 | 0.000007629395 |
| 262144 | 18 | 0.000003814697 |
| 524288 | 19 | 0.000001907349 |
| 1048576 | 20 | 0.000000953674 |

*图 8.4 使用 for 循环打印 2 的幂表的程序*

该程序计算以下值

p = 2^n

其方法是依次将 2 自身相乘 n 次。

q = 2^-n = 1/p

注意，我们将 p 声明为 long int，将 q 声明为 double。

## 例题 8.4 [L]

图 8.5 中的程序展示了如何编写一个 C 程序来打印第 n 个斐波那契数。

程序

```c
#include <stdio.h>
#include <conio.h>

void main()
{
int num1=0, num2=1, n, i, fib;
clrscr();

printf("\n\nEnter the value of n: ");
scanf ("%d", &n);

for (i = 1; i <= n-2; i++)
{
fib=num1 + num2;
num1=num2;
num2=fib;
}
printf("\n\n fibonacci number (for n = %d) = %d", n, fib);
getch();
}
```

*图 8.5 打印第 n 个斐波那契数的程序*

## 例题 8.5

图 8.6 中的程序展示了如何编写一个 C 程序来打印 1 到 n 之间的所有素数，其中“n”是用户提供的值。

程序

```
#include <stdio.h>
#include <conio.h>

void main()
{
    int prime (int num);
    int n,i;
    int temp;

    printf("Enter the value of n: ");
    scanf ("%d", &n);

    printf("Prime numbers between 1 and %d are:\n", n);
    for (i=2; i<=n;i++)
    {
        temp=prime(i);
        if(temp==-99)
            continue;
        else
            printf("%d\t", i);
    }

    getch();
}

int prime (int num)
{
    int j;
    for (j=2;j<num; j++)
    {
        if(num%j==0)
            return (-99);
        else
            ;
    }
    if (j==num)
```

**for** 循环的另一个独特之处在于，必要时可以省略一个或多个部分。考虑以下语句：

```
--------
m = 5;
for ( ; m != 100 ; )
{
    printf("%d\n", m);
    m = m+5;
}
--------
```

在 **for** 语句中，初始化和增量部分都被省略。初始化已在 **for** 语句之前完成，控制变量在循环内部递增。在这种情况下，这些部分留“空”。但是，分隔各部分的分号必须保留。如果不存在测试条件，**for** 语句会建立一个“无限”循环。此类循环可以使用循环中的 **break** 或 **goto** 语句来中断。

我们可以使用空语句建立时间延迟循环，如下所示：

```
for ( j = 1000; j > 0; j = j-1)
    ;
```

该循环执行 1000 次而不产生任何输出；它只是造成时间延迟。注意，循环体只包含一个分号，称为**空语句**。这也可以写成如下形式：

```
for (j=1000; j > 0; j = j-1);
```

这意味着，如果我们误在 **for** 语句末尾放置分号，C 编译器不会给出错误消息。该分号将被视为**空语句**，程序可能产生一些无意义的结果。

### 8.4.2 for 循环的嵌套

循环嵌套，即一个 **for** 语句位于另一个 **for** 语句内部，在 C 中是允许的。例如，两个循环可以按如下方式嵌套：

![](img/11b034a94fc590add0a7808250a38792_277_0.png)

```c
for (i = 1; i <= n ; ++i)
{
    printf("Enter roll_number : ");
    scanf("%d", &roll_number);
    total = 0 ;
    printf("\nEnter marks of %d subjects for ROLL NO %d\n",
            m, roll_number);
    for (j = 1; j <= m; j++)
    {
        scanf("%d", &marks);
        total = total + marks;
    }
    printf("TOTAL MARKS = %d ", total);
    if (total >= FIRST)
        printf("( First Division )\n\n");
    else if (total >= SECOND)
        printf("( Second Division )\n\n");
    else
        printf("( *** F A I L *** )\n\n");
}
}
```

**输出**

```
Enter number of students and subjects
3  6
Enter roll_number : 8701
Enter marks of 6 subjects for ROLL NO 8701
81 75 83 45 61 59
TOTAL MARKS = 404 ( First Division )
Enter roll_number : 8702
Enter marks of 6 subjects for ROLL NO 8702
51 49 55 47 65 41
TOTAL MARKS = 308 ( Second Division )
Enter roll_number : 8704
Enter marks of 6 subjects for ROLL NO 8704
40 19 31 47 39 25
TOTAL MARKS = 201 ( *** F A I L *** )
```

*图 8.7 嵌套 for 循环的示例*

## 例题 8.7

图 8.8 中的程序展示了如何编写一个程序来显示金字塔。
