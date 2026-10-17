
```c
do {
    printf("%d\n", x);
} while (x++ < 10);
```

由于测试条件是在循环的底部执行的，如果从第一次尝试时就不满足条件，循环体可能完全不会执行。例如：

```c
do {
    printf("%d\n", x);
} while (x++ > 0);
```

如果 `x` 一开始就不大于 0，则循环体将不会执行。再次考虑 6.1 节讨论的整数平方和。这个问题可以编码如下：

```c
sum = 0;
for (n = 1; n <= 10; n++) {
    sum += n * n;
}
printf("sum = %d\n", sum);
```

关于 `for` 循环的一个重要点是，所有的操作（即初始化、测试和增量）都放在 `for` 语句中，使得它们是可见的。

### 6.1 三种循环比较

| `for` | `while` | `do` |
|---|---|---|
| `for (n=1; n<=10; ++n)` | `n = 1; while (n<=10)` | `do { ... } while (n<=10); n++` |

## 6.3 程序

图 6.4 中的程序使用 `for` 循环打印“2 的幂”表，包括正负指数。

```c
main() {
    long p;
    int n;
    double q;
    printf("----------\n");
    printf("2 to power %n\t2 to power -n\n");
    printf("----------\n");
    p = 1;
    for (n = 0; n < 21; ++n) /* LOOP BEGINS */
        if (n == 0)
            p = 1;
        else
            p = p * 2;
        q = 1.0/(double)p;
        printf("%010d %010d\t%20.12f\n", p, n, q);
    /* LOOP ENDS */
    printf("----------\n\n");
}
```

# 麦格希尔公司

决策与循环 161

| Value | n | 概率 |
| :--- | :--- | :--- |
| 8192 | 13 | 0.000122070313 |
| 16384 | 14 | 0.000061035156 |
| 32768 | 15 | 0.000030517578 |
| 65536 | 16 | 0.000015258789 |
| 131072 | 17 | 0.000007629399 |
| 262144 | 18 | 0.00000381469 |
| 524288 | 19 | 0.000001907349 |
| 1048576 | 20 | 0.000000953674 |

图 6.4 使用循环打印 2 的幂表的程序

该程序通过连续将 2 相乘 `n` 次来计算值

`p = 2^`

`q = 2^n / p`

注意我们已经将 `p` 声明为 `long int`，将 `q` 声明为 `double`。

程序 6.4 图 6.5 所示的程序展示了如何编写一个 C 程序来打印 1 到 `n` 之间的所有质数，其中 'n' 是用户提供的值。

```c
Program
#include <stdio.h>
#include <conio.h>

void main()
{
  int prime (int num);
  int n,i;
  int temp;

  printf("Enter the value of n: ");
  scanf("%d", &n);

  printf("Prime numbers between 1 and %d are:\n", n);
  for (i=2; i<n; i++) {
    temp=prime(i);
    if(temp== -99)
      continue;
    printf("%d\t", i);
  }
  getch();
}
```

## ANSI C 编程

```c
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
    }
    if (j==num)
        return(num);
}
```

输出 输入 `n` 的值: 20

1 到 20 之间的质数有:

2 3 5 7 11 13 17 19

> 图 6.5 打印 1 到 `n` 之间所有质数的程序

# 程序 6.5

图 6.6 所示的程序展示了如何编写一个 C 程序来打印第 `n` 个斐波那契契数。

## 程序

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int num1=0, num2=1, n, i, fib;
    clrscr();

    printf("\n\nEnter the value of n: ");
    scanf("%d", &n);
```

# 麦格希尔公司

决策与循环 163

```c
for (i = 1; i <= n-2; i++)
{
  fib=num1 + num2;
  num1=num2;
  num2=fib;
  printf("\n%nth fibonacci number (for n=%d) = %d\n", n, fib);
  getch();
}
```

图 6.6 打印第 `n` 个斐波那契数的程序

# for 循环的附加功能

C 语言中的循环具有其他循环结构中没有的功能。例如，在 `for` 语句中可以初始化多个变量。语句

```c
p = 1;
for (n=0; n<17; ++n)
```

可以重写为：

```c
for (p=1, n=0; n<17; ++n)
```

注意初始化部分包含两个部分 `p=1` 和 `n=0`，由逗号隔开。

与初始化部分一样，递增部分也可以包含多个部分。例如，

```c
for (n=1, m=50; n<m; n=n++, m=m-1)
{
  p = m/n;
  printf("\n%d = %d\n", n, p);
}
```

完全有效。递增部分中的多个参数用逗号隔开。

第三个特性是，测试条件可以包含任何复合关系，且测试不需要仅限于循环控制变量。考虑这个用例：

```c
sum = 0;
for (i = 1; i < 20 && sum < 100; ++i)
{
  sum = sum+i;
  printf("\n%d = %d\n", i, sum);
}
```

循环使用了带有计数器 `i` 和哨兵变量 `sum` 的复合条件。只要条件 `i < 20` 和 `sum < 100` 同时为真，循环就会执行。`sum` 在循环内部进行求值。

在初始化和递增语句中使用表达式也是允许的。例如，这种类型的

```c
for (x = n/2; x > 0; x = x/2)
```

完全有效。

# 麦格希尔公司

164 ANSI C 编程

`for` 循环的另一个独特方面是必要时可以省略一个或多个部分。考虑以下语句：

```c
m = 5;
for ( )
{
    printf("%d\n", m);
    m = m+5;
```

`for` 语句中的初始化和递增部分都被省略了。初始化在 `for` 语句之前完成，控制变量在循环内部递增。在这种情况下，不存在测试条件，形成无限循环。这种循环可以使用 `break` 或 `goto` 语句跳出。

我们可以使用空语句设置延迟循环，如下：

```c
for ( j = 1000; j > 0; j-1);
```

该循环执行 1000 次而不产生任何输出；注意 `for` 语句的主体只包含一个分号，被称为空语句。这也可以写成

```c
for (j=1000; j>0; j-1);
```

这意味着如果我们错误地在 `for` 语句结束放置分号，C 编译器将报错。分号将被视为空语句，程序将产生无意义的内容。

# 循环嵌套

C 语言允许循环嵌套，即在一个 `for` 语句中嵌套另一个 `for` 语句。两个循环可以嵌套如下：

```c
for ( i = 1; i < 10; ++i )
{
    for ( j = 1; j < 5; ++j )
    {
```

# 决策与循环 165

嵌套可以持续到任何深度。循环应该正确缩进，以便读者轻松确定包含哪些语句（ANSI C 允许 15 层嵌套，但某些编译器允许更多）。程序 6.2 中讨论的乘法表可以使用嵌套的 `for` 语句更简洁地编写：

```c
for (row = 1; row <= ROWMAX; ++row)
  for (column = 1; column <= COLMAX; ++column)
    y = row * column;
    printf("%4d", y);
  printf("\n");
```

外部循环控制行，内层循环控制列。6.6 学生参加 `m` 门科的年度考试。读取每个学生各科目的成绩并计算总分的程序如图 6.7 所示。该程序使用了 `for` 循环，一个控制学生人数，另一个控制科目数。由于程序要求学生人数和科目数，该程序可用于任何规模的课程和任何数量的科目。外部循环包括三个部分：

1. 读取学号；
2. 内层循环，读取并累加每个学生的成绩；
3. 打印总分并划分等级。

```c
#define FIRST 360
#define SECOND 240
main()
{
  int n, m, i, j;
  roll_number, marks, total;
  printf("Enter number of students and subjects\n");
  scanf("%d %d", &n, &m);
  printf("\n");
  for (i = 1; i <= n; ++i) {
    printf("Enter roll_number : %d");
    scanf("%d", &roll_number);
    total = 0;
    printf("\nEnter marks of %d subjects for ROLL NO %d\n", m,roll_number);
    for (j = 1; j <= m; j++) {
        scanf("%d", &marks);
        total = total + marks;
    }
    printf("TOTAL MARKS = %d\n", total);
    if (total >= FIRST) {
        printf("* First Division\n\n");
    } else if (total >= SECOND) {
        printf("* Second Division\n\n");
    } else {
        printf("* *** FAIL ***\n\n");
    }
  }
}
```

输出 输入人数和科目数

6

输入学号：8701

输入学号 8701 的 6 门科目成绩:

81 75 83 45 61 59

总分 = 404 ( 一等 )

输入学号：8702

输入学号 8702 的 6 门科目成绩:

51 49 55 47 65 41

总分 = 308 ( 不及格 )

图 6.7 嵌套循环示意图

# 程序 6.7

图 6.8 所示的程序展示了如何编写一个显示金字塔的程序。

算法

步骤1 - 开始

步骤2 - 读取用于生成金字塔的值 (`num`)

步骤3 - 设置 `x = 40`

步骤4 - 初始化循环计数器 `y=0`

步骤5 - 当 `y <= num` 时重复步骤 6-12

步骤6 - 移动到坐标位置 (`x`, `y+1`)

步骤7 - 初始化循环计数器 `i=0-y`

8 - 当 `i < x` 时重复步骤 9-10

步骤9 - 显示 `i` 的绝对值，`abs(i)`

步骤10 - `i = i + 1`

步骤11 - `x = x - 3`

步骤12 - `y = y + 1`

步骤13 - 停止

流程图

```c
Program
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
void main() {
    int num,i,y,x=40;
    printf("nEnter a number for \nenerating the pyramid:\n");
    scanf("%d",&num);
    for(y=0;y<=num;y++) {
        gotoxy(x,y+1);
        for(i=0-y;i<x;i++) {
            printf("%3d",abs(i));
        }
        x=x-3;
    }
    getch();
}
```

输出 输入一个生成金字塔的数字:

7

![](img/177eacb192165f90062789304b5da281_178_0.png)

# McGraw-Hill 公司

168 ANSI C 编程

```
0
1 0
2 1 0 2
3 2 1 0 2 3
4 3 2 1 0 2 3 4
5 4 3 2 1 0 2 3 4 5
6 5 4 3 2 1 0 2 3 4 5 6
7 6 5 4 3 2 1 0 2 3 4 5 6 7
```

图 6.8 构建金字塔的程序

# 选择循环

给定一个问题后，程序员首要考虑的问题是决定使用哪种循环。为了在 C 语言支持的三种循环中选择一种，我们可以采用以下策略：

- 分析问题，并查看它需要的是前测试循环还是后测试循环。
- 如果需要后测试循环，那么我们只能使用一种循环：`do-while`。
- 如果需要前测试循环，那么我们有两个选择：`for` 和 `while`。
- 决定循环的终止是需要计数控制还是哨兵控制。
- 如果需要计数控制，则使用 `for`。
- 如果需要哨兵控制，则使用 `while`。
- 注意，计数控制循环和哨兵控制循环都可以通过这三种控制结构来实现。

## 6.5 循环中的跳转

循环重复执行一组操作，直到控制变量不再满足测试条件。循环重复的次数是预先决定的，并通过编写测试条件来实现这一点。有时，执行循环时，跳过部分循环或在某个特定条件发生时立即退出循环会变得困难。例如，考虑在包含 100 个名称的列表中搜索特定名称的情况。一个用于编写和测试 100 次名称的程序循环在找到所需名称时必须终止。C 语言允许从循环内部的一个语句跳转到另一个语句，也允许跳出循环。

# 跳出循环

可以通过 `break` 语句或 `goto` 语句实现循环的提前退出。我们已经见过在 `switch` 语句中使用 `break` 以及在 `if...else` 结构中使用 `goto`。这些语句也可以用于 `while` 或 `for` 循环中。它们在图 6.9 和图 6.10 中所示。

- 当循环内部遇到 `break` 时，循环将立即退出，程序继续执行紧随循环之后的语句。当存在嵌套循环时，`break` 只会退出包含它的那个循环。也就是说，`break` 只会退出单个循环。

由于 `goto` 语句可以将控制权转移到程序的任何位置，因此在循环内部提供分支是非常有用的。`goto` 的另一个用途是在发生错误时从深层嵌套循环中退出。在这种情况下，简单的 `break` 语句无法生效。

```c
while (----)
{
  do
  {
    if (condition)
      break;
    Exit from loop
  } while (----);
}
(a)
(b)
for (----)
{
  if (error)
    break;
  Exit from loop
  Exit from inner loop
  if (condition)
    break;
}
(c)
(d)
```

图 6.9 使用 `break` 语句退出循环

```c
while (----)
{
  for (----)
  {
    if (error)
      goto stop;
    for (----)
    {
      if (error)
        goto error;
    }
    Jump within loop
    if (condition)
      goto abc;
    Exit from two loops
}
abc:
stop: (----);
error:
(a)
(b)
```

图 6.10 使用 `goto` 语句在循环内跳转并退出循环

# 程序 6.8

图 6.11 中的程序阐述了 `break` 语句在 C 程序中的用法。

该程序读取一个正值列表并计算它们的平均值。`for` 循环被编写为读取 1000 个值。然而，如果我们想让程序计算任何少于 1000 个值的平均值，那么我们必须在列表最后一个值之后输入一个“负”数，以标记输入的的结束。
