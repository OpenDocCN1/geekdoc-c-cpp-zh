
```
if (expression)
{
    Block of statements;
}
else
{
    Block of statements;
}
```

如果我们希望在 `if` 或 `else` 后面跟多条语句，就应该将它们在大括号中分组。这种分组被称为复合语句或块。有时，我们希望根据几个条件进行多路决策。实现此点的最通用方法是在 `if` 语句上使用 `if` 变体（即 `else if`）。这是通过级联多次比较来工作的。只要其中任何一个比较给出真结果，就会执行后续的语句或块，不再进行后续的比较。

```
if (expression)
{
    Block of statements;
}
else if (expression)
{
    Block of statements;
}
else
{
    Block of statements;
}
```

## 5.4 switch 语句

`switch` 语句提供了一种根据表达式的值在一组备选项之间选择的方法。`switch` 语句的通用形式为：

```
switch (expression)
{
    case constant1:
        statements;
        ...
    case constant:
        statements;
    default:
        statements;
}
```

首先求值表达式（称为 switch 标签），并将结果按照它们出现的顺序与每个数值常量（称为 case 标签）进行比较，直到找到匹配项。然后执行匹配的 `case` 之后的语句。复数形式：每个 `case` 后面可以跟零条或多条语句（而不仅仅是一条语句）。执行一直持续，直到遇到 `break` 语句或者直到 `switch` 语句结束的所有中间语句都已执行完毕。最后的 `default case` 是可选的，如果前面的任何 `case` 都没有提供匹配项，则执行它。

## 5.5 循环

另一种主要的控制语句是循环。循环允许语句或语句块重复执行。计算机非常擅长多次重复简单任务，循环是实现这一点的 C 工具，为你提供了三种循环类型：`while`、`do` 和 `for`。

### 5.5.1 while 循环

`while` 循环不断重复某个动作，直到关联的测试返回假。这对于程序员预先不知道循环将遍历多少次的情况非常有用。

通用语法如下：

```
while (Condition)
{
    Block of statements
}
```

### 示例：

```c
int string_length(char string[])
{
    int i = 0;
    while (string[i] != '\0')
        i++;
    return (i);
}
```

字符串作为参数传递给函数。未指定数组的大小，该函数适用于任何大小的字符串。`while` 循环用于逐个查看字符串中的字符，直到找到空字符。随后退出循环并返回空字符的索引。只要字符不为空，索引就会加 1 并重复测试。

### 5.5.2 do while 循环

`do` 循环与 `while` 循环类似，但测试是在循环体执行之后进行的。这确保了在继续执行之前，循环体至少执行一次。这种设置经常用于读取数据的情况。然后测试验证数据，如果数据不可接受，则跳回重新读取。

通用语法如下：

```
do
{
    Block of statements
}
while (Condition);
```

### 示例：

```c
do
{
    printf("Enter 1 for yes, 0 for no :");
    scanf("%d", &input_value);
} while (input_value != 1 && input_value != 0);
```

### 5.5.3 for 循环

循环通常用于需要固定次数遍历循环的情况。它非常灵活，初级程序员应该注意不要滥用它提供的功能。

通用语法如下：

```
for (Declaration/Initialization; Condition; Increment/Decrement)
{
    Block of statements
}
```

循环头由分号分隔的三部分组成。第一部分在进入循环之前执行。第二部分是测试，第三部分在循环体之后执行。

## 5.6 break 语句

`break` 语句用于提前退出循环。当你想根据循环条件之外的条件停止循环时，它非常有用。它也可以用于 `switch` 语句。

## 5.7 continue 语句

`continue` 语句用于跳过当前迭代的剩余部分并进入下一次。与 `break` 不同，它不会退出循环。它只是跳转到下一次测试。

## 5.8 goto 语句

`goto` 语句用于跳转到程序中带有标签的部分。它通常不被推荐，因为它可能会导致代码难以阅读和维护。

```
label:
    // code
goto label;
```

```c
for (i = 0; i < 10; i++) {
    if (i == 5)
        goto out;
    printf("%d", i);
}
out:
    printf("Jump out of loop");
```

(20) 编写一个 C 程序来打印以下模式：

```
1
1 2 1
1 2 3 2 1
1 2 3 4 3 2 1
1 2 3 4 5 4 3 2 1
```

(21) 编写一个 C 程序来显示以下格式：

```
a b
1 5
2 4
3 3
4 2
5 1
```

(22) 编写一个 C 程序来显示以下格式：

```
no. sum
1 1
2 3
3 6
4 10
5 15
```

# 程序 5.1

Computing powers of 2.c — 打印 2 的幂：1, 2, 4, 8, 直到 2^N

```c
#include <stdio.h>
#define N 10
int main(void)
{
    int n;
    /* The current exponent */
    int val = 1; /* The current power of 2 */
    printf("\n\t 2^n\n");
    printf("====================\n");
    for (n = 0; n <= N; n++) {
        printf("\t%3d \t %6d\n", n, val);
        val = 2 * val;
    }
    return 0;
}
```

输出如下：

| n | 2^n |
|---|---|
| 0 | 1 |
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |
| 5 | 32 |
| 6 | 64 |
| 7 | 128 |
| 8 | 256 |
| 9 | 512 |
| 10 | 1024 |

# 程序 5.2

Adding n integers.c — 读取一个正数。然后读取 N 个整数并将它们与其和一起输出。

```c
#include <stdio.h>
int main(void)
{
    int n; /* 要读取的数字个数 */
    int sum; /* 已经读取的数字的和 */
    int current; /* 最近读取的数字 */
    int lcv; /* 循环控制变量，计算已读取的数字个数 */
    printf("Enter a positive n > ");
    scanf("%d", &n); /* 我们应该检查 n 是否真的是正整数 */
    sum = 0;
    for (lcv = 0; lcv < n; lcv++) {
        printf("\nEnter an integer > ");
        scanf("%d", &current);
        sum = sum + current;
    }
    printf("The sum is %d\n", sum);
    return 0;
}
```

# 程序 5.3

Adding a sequence of positive integers.c — 读取一个正整数序列并将它们与其和一起输出。使用哨兵值（例如 0）来确定序列何时结束。

# 程序 5.4

Determining if a number is a prime.c — 提示用户输入一个整数 N。输出它是否为质数。如果不是，则输出 N 的一个因数。

```c
#include <stdio.h>
int main(void)
{
    int n;
    /* i 的值大于 n 的平方根吗？ */
    if ((n % i) == 0) /* 如果为真则 n 可被 i 整除 */
        flag = 0;
    else
        i++;
    if (flag)
        printf("%d is prime\n", n);
    else
        printf("%d has %d as a factor\n", n, i);
    return 0;
}
```

# 程序 5.5

Finding all the proper factors of a number.c — 提示用户输入一个整数 N。输出它是否为质数。如果不是，则输出它所有的真因数。

```c
#include <stdio.h>
int main(void)
{
    int n,
    lcv,
    flag; /* flag 初始为 1，当我们确定 n 不是质数时则设为 0 */
    printf("Enter value of N > ");
    scanf("%d", &n);
    for (lcv = 2, flag = 1; lcv <= (n / 2); lcv++)
    {
        if ((n % lcv) == 0)
        {
            if (flag)
                printf("The non-trivial factors of %d are: \n", n);
            flag = 0;
            printf("%d\n", lcv);
        }
    }
    if (flag)
        printf("%d is prime\n", n);
}
```

# 程序 5.6

Computing Fibonacci numbers.c — 打印斐波那契数列。

该输出为：

```
1
2
3
4
5
6
7
8
9
```

# 程序 5.7

```c
#include <stdio.h>
#define N 100
#define FALSE 0
#define TRUE 1
int main(void)
{
    int n;
    int i;
}
```

## 第二部分

## 6. 引言

在本章中，你将学习预处理器，这是一个在代码通过编译器之前对其进行处理的过程。C 预处理器支持许多以符号 `#` 开头的指令。这些指令用于使代码变得易于编写、可移植且高效。常用的指令如下所示：

## 6.2 预处理器指令

| 指令 | 功能 |
|---|---|
| `#define` | 定义宏 |
| `#undef` | 取消宏定义 |
| `#include` | 指定要包含的文件 |
| `#ifdef` | 测试宏是否已定义 |
| `#ifndef` | 测试宏是否未被定义 |
| `#endif` | 指定 `#if` 的结束 |
| `#else` | 当 `#if` 失败时指定的替代方案 |
| `#if` | 测试编译时条件 |

预处理器指令可以分为三类：

- 宏替换
- 文件包含
- 编译器控制

## 6.3 宏

宏替换是将程序中的标识符替换为字符串的过程。它采用以下形式：`#define 标识符 字符串`。有不同形式的宏替换：

- 简单宏替换
- 参数宏替换
- 嵌套宏替换

### 简单宏替换

字符串替换通常用于定义常量。宏定义可以包含不仅仅是一个值。它也可以包含表达式。以下是一个有效示例：

```c
#define AREA 12.3
```

用大写字母写定义是一种约定而非规则。

### 带参数宏

预处理器允许我们定义更复杂、更有用的替换形式。它采用以下形式：

```c
#define 标识符(f1, f2, f3....fn) 字符串
```

注意标识符与左括号之间没有空格，标识符 `f1, f2, f3...fn` 类似于函数定义中的形式参数。

带参数宏的简单示例如下：

```c
#define CUBE(x) (x*x*x)
```

`volume = CUBE(side);`

预处理器会将语句展开为：

`volume = (side*side*side)`

### 宏嵌套

可以在另一个宏的定义中使用一个宏。宏定义可以是嵌套的。考虑以下宏定义：
