

**表 7.1** 用于决策的运算符（按优先级顺序）

| 运算符 | 含义 | 结合性 |
|---|---|---|
| `!` | 逻辑非 | 从右到左 |
| `%` | 取模 | 从左到右 |
| `<, <=, >, >=` | 关系 | 从左到右 |
| `==, !=` | 关系（相等） | 从左到右 |
| `&&` | 逻辑与 | 从左到右 |
| \|\| | 逻辑或 | 从左到右 |
| `?:`（三元运算符） | 条件 | 从右到左 |

### 7.2.2 复合语句或块

当使用 **if** 和 **while** 等结构时，你需要将一组语句作为一个整体来处理。这个整体两侧由一对匹配的花括号括起，被称为*复合语句*。它也被称为*控制块*，或简称为*块*。下面是取自第 6.5 节的一个复合语句：

```c
if ((last_number % 2) == 1) {
    printf("Not an even number\n");
    return 0;
}
```

控制块开始  
控制块结束

**printf** 和 **return** 语句构成一个复合语句，**if** 将它当作单条语句来处理。当控制表达式影响两条或更多条语句时，它们*必须*被括在花括号中以构成复合语句。在允许使用单条语句的任何地方，也可以使用复合语句。这样做有时是为了使代码更清晰。

记住这一点会很有帮助：块会改变在其中声明的变量的*作用域*（即可见性）。这样的变量在块外或其他块中是不可见的。这些可见性问题将在第 11 章讨论。

## 7.3 if 语句

**if** 语句是任何编程语言中最常用的选择结构。它基本上有两种形式——带 **else** 关键字和不带 **else** 关键字。后面讨论的其他形式都是由这两种形式派生出来的。第一种形式（图 7.1）指定当*表达式*求值为真时要执行的操作。该语法展示了简单语句和复合语句的用法。

![](img/d75612dcf3ab36327142238ab5bb21d8_234_0.png)

**图 7.1** if 语句（形式 1）

执行该语句时，首先对*表达式*求值。如果该值为真，则执行一条或多条语句。对于单条语句，花括号不是必需的；但对于复合语句，它们是必需的。下面是一个简单的示例：

```c
if (hours_left > 6)
    rate = 25;
printf("Refund amount = %f\n", rate * amount);
```

*if 语法要求使用圆括号*  
*下一条语句应缩进*

这里，如果 `hours_left` 大于 6，则将 25 赋给 `rate`。请注意，`printf` 语句是无条件执行的，与控制表达式的结果无关。缩进上的差异反映了我们的真实意图，并且与编译器看到的情况一致。

复合语句需要在两端使用花括号。下面的复合语句由三条简单语句组成：

```c
if (amount > 10000) {
    printf("You can't withdraw more than 10000 with this debit card\n");
    printf("Key in an amount not exceeding 10000\n");
    scanf("%d", &amount);
}
```

*if 到此处的 ; 结束*

注意，`}` 符号后面没有分号。如果没有花括号，则只有第一个 `printf` 会被条件执行。

> **注意：** 当 `if` 与单条语句一起使用时，它以作为语句终止符的分号结束。对于复合语句，`if` 在最后一条语句的终止 `;` 处结束。

> **警告：** 用于决策和循环结构的所有控制表达式都必须用圆括号括起来。如果你使用 `if count > 0` 或 `while count++ <= MAX_COUNT`，编译器将生成错误。

## 7.4 `average_integers.c`：平均值计算程序

我们的第一个程序（程序 7.1）计算用户输入的两个非零整数的平均值，但在验证后只考虑它们的绝对值。这意味着负整数的符号会被去掉。该任务通过使用一个关系运算符（`<`）和一个逻辑运算符（`||`）完成。该程序运行了三次。

程序首先从键盘输入为两个整型变量 `inta` 和 `intb` 赋值。然后它使用一个逻辑表达式作为 `if` 的控制表达式，以判断两个整数中是否有一个为零。首先处理那些会导致错误的情况是一种良好的编程实践。如果程序流越过了第一个 `if` 语句，就说明我们手中已经有两个有效的整数。

一旦成功通过验证测试，下一步就是使用两个 `if` 语句来计算这两个整数的绝对值。最简单的方法是使用一元 `-` 运算符，它只是将操作数乘以 -1。我们使用 `(float)` 强制转换来计算这两个整数的平均值，因为如果没有它，除法将导致小数部分被截断。

```c
/* average_integers.c: Calculates average of the absolute values of two
   integers. Quits program if one integer is zero. */
#include <stdio.h>
int main(void)
{
    int inta, intb;
    printf("Enter two non-zero integers: ");
    scanf("%d %d", &inta, &intb);

    if (inta == 0 || intb == 0) {
        printf("At least one integer is zero\n");
        return 1;            /* Good to return nonzero for invalid entry */
    }

    /* Assigning absolute values to inta and intb */
    if (inta < 0)
        inta = -inta;        /* Using the - unary operator */
    if (intb < 0)
        intb = -intb;
    /* If we have come here, both inta and intb must be positive */
    printf("Average of absolute value of the integers = %.2f\n",
           (float) (inta + intb) / 2);
    return 0;
}
```

| 程序 7.1：**average_integers.c** | |
|---|---|
| Enter two non-zero integers: **7 0**<br>At least one integer is zero | *第一次调用* |
| Enter two non-zero integers: **5 10**<br>Average of absolute value of the integers = 7.50 | *第二次调用* |
| Enter two non-zero integers: **-13 8**<br>Average of absolute value of the integers = 10.50 | *第三次调用* |
| 程序输出：**average_integers.c** | |

该程序包含两条 **return** 语句，有趣的是，第一条返回的是 1 而不是 0。返回 1 而不是 0 会有什么不同吗？是的，有，但前提是*下一个*程序会利用这个值。你需要过一段时间才会接触到协作程序，但了解一下这就是 **return** 的设计用法是件好事（见插文——*它是如何工作的*）。请注意，我们没有为 `inta` 和 `intb` 这两个整数使用单独的验证例程。相反，我们使用了下面的逻辑表达式：

```c
if (inta == 0 || intb == 0)
```

对于这个入门程序来说，这是可以接受的，因为我们不需要在失败时知道是哪个变量出了问题。有时，我们需要查明失败的原因，在这种情况下，你需要使用两个带有单独 `if` 语句的关系表达式（如 `if (inta == 0)` 和 `if (intb == 0)`），并为它们分别指定独立的处理路径。

```c
/* leap_year_check.c: Checks for leap year using the if-else structure.
   Doesn't make the check for century. */
#include <stdio.h>
int main(void)
{
    short year, years_left;

    printf("Enter year for leap year check: ");
    scanf("%hd", &year);
    if (year < 0) {
        printf("Invalid year\n");
        return 1;
    }
    if (year % 4 == 0)              /* No parentheses required */
        printf("Year %hd is a leap year.\n"
               "Next leap year is after 4 years.\n", year);
    else {
        years_left = 4 - year % 4;   /* No parentheses required */
        printf("Year %hd is not a leap year.\n"
               "Next leap year is %hd.\n", year, year + years_left);
    }
    return 0;
}
```

**程序 7.2：leap_year_check.c**

| 程序输出 | 调用 |
|---|---|
| Enter year for leap year check: **2009**<br>Year 2009 is not a leap year.<br>Next leap year is 2012. | *第一次调用* |
| Enter year for leap year check: **2012**<br>Year 2012 is a leap year.<br>Next leap year is after 4 years. | *第二次调用* |
| Enter year for leap year check: **1900**<br>Year 1900 is a leap year.<br>Next leap year is after 4 years. | *第三次调用*<br>*这是错误的* |

程序输出：**leap_year_check.c**

在表达式 `year % 4 == 0` 中，我们没有使用圆括号，因为 `%` 的优先级高于 `==`（表 7.1）。因此先执行取模运算。`else` 部分包含处理非闰年的代码。表达式 `4 - year % 4` 中也省略了圆括号，因为 `%` 的优先级高于 `-`。

在最后两个 `printf` 语句中，第一个实参实际上由两个拼接在一起的字符串组成。C 语言允许这种拼接（9.12.2），但请注意，即使这些字符串位于两个物理行上，拼接后的字符串实际上也只是一个实参。

