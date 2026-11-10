
外层 **while** 循环反复提示输入两个整数。完成必要的验证后，程序将有效数字传递给内层循环。对于该循环的每次迭代，`total` 会被依次赋值为 `base`、`base * base`、`base * base * base` 等，直到关键变量 `num` 等于用户输入设定的幂次。

**注意：** 数学库支持 **pow** 函数，其作用与本程序相同。第 12 章介绍了一个使用该函数的程序。对于包含 **pow** 的程序，编译过程有所不同：必须*显式*调用链接器，以便将 **pow** 的代码包含到可执行文件中。

## 8.6 将 **while** 与 **break** 和 **continue** 一起使用

到目前为止看到的 **while** 循环都使用控制表达式来决定应当迭代还是终止。然而，有些情况需要立即暂停当前迭代，以便跳出循环或重新开始一次新的迭代。C 支持两个关键字——**break** 和 **continue**——它们可以完成这两项任务（图 8.4）。

当程序遇到 **break** 时，控制流会跳出循环，从紧挨着循环结束之后的语句继续执行。另一方面，**continue** 不会终止循环，而是暂停循环执行，以继续下一次迭代。这两种情况通常发生在循环中使用的变量或表达式取得了某个值，使得继续执行语句不再合适时。

![](img/d75612dcf3ab36327142238ab5bb21d8_273_0.png)

**图 8.4** continue 和 break 在 while 循环中的行为

下一个程序（程序 8.8）使用一个无限 **while** 循环，以便重复输入三个正数。如果发现其中至少一个数为负数，它就使用 **continue** 请求输入一组新的数字。如果所有数字都是正数，那么 **break** 语句会终止循环。随后，**while** 的右花括号下方的 **printf** 语句会打印这些数字的和。当三个数都输入为零时，程序也会终止。

```c
/* break_continue.c: Uses break and continue in a loop. */
#include <stdio.h>
int main(void)
{
    short a, b, c;
    while (1) {
        printf("Enter three integers a b c: ");
        scanf("%hd %hd %hd", &a, &b, &c);

        if (a == 0 && b == 0 && c == 0) {
            printf("All values zero. Quitting ...\n");
            return 1;
        }
        else if (a < 0 || b < 0 || c < 0) {
            printf("Negative integer not allowed\n");
            continue;            /* Goes to while (1) */
        }
        else
            break;               /* Goes to next printf statement */

        printf("Sum of %d %d %d: %d\n", a, b, c, a + b + c);
    }
    return 0;
}
```

| **程序 8.8：break_continue.c** |
| --- |
| 输入三个整数 a b c：3 4 -5 |
| 不允许负整数 |
| 输入三个整数 a b c：3 4 5 |
| 3 4 5 的和：12 |
| 输入三个整数 a b c：0 0 0 |
| 所有值均为零。正在退出…… |

程序输出：**break_continue.c**

结构化编程理论家不赞成使用 **break** 和 **continue**。他们认为循环应当提供单一出口点（即测试控制表达式的位置）。但这种安排是有代价的；需要在循环中的多个位置设置并测试若干变量。在你使用过 **break** 和 **continue** 之后，可能就不愿意付出这种代价了。

## 8.7 prime_number_check.c：更多 **break** 和 **continue** 的用法

我们以程序 8.9 结束关于 *while* 循环的讨论，该程序检查一个数是否为素数。*素数*是指除自身和 1 之外不能被任何其他数整除的数。程序从键盘接受多个数字，并在输入零时终止。该练习在一个使用 **break** 和 **continue** 的嵌套 *while* 循环结构中完成。程序分为四个部分。

```c
/* prime_number_check.c: Determines whether a variable is prime or not.
   Uses a nested loop with break and continue. */
#include<stdio.h>
int main(void)
{
    int num, divisor;
    char is_prime;

    /* (A) Number input and validation */
    printf("Enter numbers for prime test (0 to quit): ");
    while (scanf("%d", &num) == 1) {
        if (num < 0) {
            printf("Invalid input\n");
            continue;
        }
        else if (num == 0)
            break;                  /* Go to (D) */

        /* (B) Check for prime */
        divisor = 2;
        is_prime = 'y';             /* Assume number is prime */
        while (divisor < num) {
            if (num % divisor == 0) {
                is_prime = 'n';     /* Number is not prime */
                break;              /* Go to (C) */
            }
            divisor++;
        }

        /* (C) After break in (B) */
        is_prime == 'y' ? printf("%d is prime\n", num) :
            printf("%d is not prime, divisible by %d\n", num, divisor);
    } /* End of outer loop */

    /* (D) After break in (A) */
    printf("Quitting ...\n");
    return 0;
}
```

程序 8.9：prime_number_check.c

```text
Enter numbers for prime test (0 to quit): 19 49 -5 137 1234567 0
19 is prime
49 is not prime, divisible by 7
Invalid input
137 is prime
1234567 is not prime, divisible by 127
Quitting ...
```

程序输出：prime_number_check.c

```c
short i = 1, sum = 0;
do {
    sum += i;
    i++;
} while (i <= 10);
printf("Sum of first 10 integers = %hd\n", sum);
```

注意控制表达式 (i <= 10) 末尾的 ;。关键变量 i 的自增可以移到控制表达式中（这还要求把 <= 替换为 <）。由于这一移动使循环体中只剩一条语句，你也可以去掉花括号。许多程序员即使花括号内只有一条语句，也倾向于使用花括号。下面是两种形式：

```c
do                         do {
    sum += i;                  sum += i;
while (i++ < 100);         } while (i++ < 100);
```

选择你觉得使用起来舒服的形式，并且如果你确实必须使用 do-while 循环，就始终一致地使用它。现在我们将使用该循环开发一个有用的应用程序。

## 8.9 decimal2binary.c：从重复除法中收集余数

程序 8.10 使用 do-while 循环将十进制数转换为二进制，但不反转各位。回想一下，反转后的位模式实际上表示等价的二进制数 (3,2,2)。程序还会显示存储该二进制数所需的位数。

```c
/* decimal2binary.c: Uses a do-while loop to convert a decimal number
                     to binary but without reversing the digits. */
#include <stdio.h>

int main(void)
{
    long quot;
    short count = 0, rem = 0;

    printf("Enter a decimal integer: ");
    scanf("%ld", &quot);

    do {
        rem = quot % 2;             /* Either 0 or 1 */
        quot /= 2;                  /* Quotient progressively decreases */
        printf("%hd ", rem);
        count++;
    } while (quot > 0);

    printf("\nNumber of iterations = %hd\n", count);

    return 0;
}
```

程序 8.10：**decimal2binary.c**

```text
    Enter a decimal integer: 35
    1 1 0 0 0 1                      Binary of 35 is 100011
    Number of iterations = 6
    ────────────────────────────────
    Enter a decimal integer: 128
    0 0 0 0 0 0 1
    Number of iterations = 8
```

**程序输出：** `decimal2binary.c`

从用户输入得到的数会在 `do-while` 循环中反复进行除法和取模运算。当 `quot`（它随着每次迭代逐渐减小）最终降为零时，循环终止。由于生成的位没有被保存，程序无法将它们反转。为了正确表示该数等价的二进制形式，我们需要使用数组来存储这些位，然后反向读取数组。我们将在 8.12 节改进这个程序。

## 8.10 for 循环

与 `while` 和 `do-while` 一样，`for` 循环也使用关键变量/控制表达式范式来决定循环的进入和延续。它是一种紧凑的结构，将三个表达式集中在一个地方（图 8.6）。任何 `while` 循环都可以替换为 `for` 循环，并且对许多人来说，后者是首选的循环。

```c
for (exp1; exp2; exp3)
    statement;

for (exp1; exp2; exp3) {
    statement1;
    statement2;
    ...
}
```

**图 8.6** for 语句

`while` 循环的工作原理是在循环之前初始化关键变量，在控制表达式中测试它，并在循环体中更新关键变量。`for` 中的三个表达式完成同样的工作，但集中在一个地方。初始化由 `exp1` 完成，关键变量检查由 `exp2` 完成，关键变量的更新由 `exp3` 完成。这些由分号分隔的表达式决定循环是否运行，以及如果运行，运行多少次。

图 8.7 的左侧展示了使用 `for` 循环打印大写字母 ASCII 值的用法。右侧展示了使用 `while` 的等价代码。`for` 中的三个表达式并非在每次循环迭代中都会被求值，因此让我们理解该程序中 `for` 所使用的操作顺序：

1. 第一个表达式（`chr = 65`，在语法中为 `exp1`）初始化关键变量（`chr`）。
2. 第二个表达式（`chr < 91`，在语法中为 `exp2`）是此循环的控制表达式，它会被求值。如果求值为真，则进入循环。
