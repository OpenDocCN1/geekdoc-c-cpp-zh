
当代码以这种方式呈现时，将 **if** 与其 **else** 配对应该没有问题。前三个 **if** 语句表示 AND 条件（a > 0 && b > 0 && c > 0），因此第一个 **printf** 表示当三个表达式的值都为真时要执行的操作。其他 **printf** 语句与 **else** 子句相关联，它们告诉我们当各个变量小于或等于零时会发生什么。

在某些情况下，我们需要省略一些 **else** 关键字，甚至全部省略。后者容易处理，但我们必须谨慎处理其他情况。在此之前，让我们看一个包含语义嵌套 **if** 结构的程序。

## 7.11 `right_angle_check.c`：检查勾股定理的程序

我们的几何知识告诉我们，直角三角形斜边的平方等于另外两条边的平方和。这意味着给定三个数 a、b 和 c，如果 a * a + b * b 等于 c * c，那么可以用这三条边构成一个直角三角形，其中最长边表示斜边。

程序 7.5 运行一个无限 **while** 循环，从键盘接受三个整数（a、b 和 c）。它允许用户多次输入非零值，然后尝试 a、b 和 c 的所有可能组合，以判断其中是否有组合符合该公式。了解嵌套 **if** 结构如何工作是有益的，尽管更好、更直观的方法是使用 **if-else-if** 阶梯。

程序首先验证这些整数是否为非零值；当它们全为零时，程序终止。验证成功后，控制流转移到由四个 **if** 语句组成的嵌套结构。第一个 **if**（最外层）只允许正整数通过。如果该测试失败，底部匹配的 **else** 会使用 **printf** 显示一条不具体的错误消息。由于整个结构在循环中运行，控制流随后回到 **while** 的开头，以接受下一组整数。

一旦这三个整数通过第二次验证测试，程序会尝试三种可能*不*符合该定理的组合（a-b-c、a-c-b 和 b-c-a）。换句话说，如果三个关系表达式的值都为真，那么用这些整数的任何组合都*不能*构成直角三角形。如果其中一个表达式失败，其对应的 **else** 部分会使用 **printf** 告诉我们*可以*构成直角三角形，并且还会告诉我们斜边是哪条。

## 7.12 **if-if-else** 嵌套结构的配对问题

在上一个程序（程序 7.5）中，我们没有遇到任何配对问题，因为嵌套 **if** 结构中的 **if** 和 **else** 子句数量相等。很容易看出哪个 **else** 与哪个 **if** 配对。有时，程序逻辑可能不需要一个或多个 **else** 子句。图 7.5 展示了一个缺少 **else** 的小代码片段，并同时给出了具有误导性的缩进和正确的缩进。

左侧形式中 **else** 部分的缩进具有欺骗性。它给人的印象是 **else** 与第一个 **if** 配对，但事实并非如此。右侧形式正确显示了 **else** 与内层 **if** 配对。尽管编译器并不关注缩进，但我们不能忽视它。

```c
/* right_angle_check.c: Uses nested if statements. Doesn't catch
   exact cause of failure. Formula used: a*a + b*b = c*c */
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

        /* RAT represents right-angled triangle */
        if (a > 0 && b > 0 && c > 0)
            if (a * a + b * b != c * c)       /* Whether RAT can't be formed */
                if (a * a + c * c != b * b)   /* Ditto */
                    if (b * b + c * c != a * a)   /* Ditto */
                        printf("RAT not possible.\n");
                    else
                        printf("RAT with %hd as hypotenuse.\n", a);
                else
                    printf("RAT with %hd as hypotenuse.\n", b);
            else
                printf("RAT with %hd as hypotenuse.\n", c);
        else
            printf("At least one input is invalid.\n");
    }
}
```

### 程序 7.5：**right_angle_check.c**

```text
Enter three integers a b c: 5 0 9
At least one input is invalid.
Enter three integers a b c: 3 5 4
RAT with 5 as hypotenuse.
Enter three integers a b c: 5 2 6
RAT not possible.
Enter three integers a b c: 6 10 8
RAT with 10 as hypotenuse.
Enter three integers a b c: 0 0 0
All values zero. Quitting ...
```

### 程序输出：**right_angle_check.c**

| 具有误导性的缩进 | 正确的缩进 |
|---|---|
| `if (a > 0)`<br>　`if (b > 0)`<br>　　`valid_int = 'y';`<br>`else`<br>　`valid_int = 'n';` | `if (a > 0)`<br>　`if (b > 0)`<br>　　`valid_int = 'y';`<br>　`else`<br>　　`valid_int = 'n';` |

### 图 7.5：缺少 else 的代码

但如果你实际上想为第一个 `if` 保留 `else` 部分，而不为第二个 `if` 保留，那该怎么办？这个问题有两种解决方案。一种是使用花括号来消除歧义。另一种是使用一个包含单独分号的虚拟 `else`。单独放在一行上的 ; 表示空语句——一条什么都不做的语句。图 7.6 并排列出了这两种解决方案，供你选择更喜欢的一种。花括号方案是大多数人偏好的方案。

| 空命令方案 | 花括号方案 |
|---|---|
| `if (a > 0)`<br>　`if (b > 0)`<br>　　`valid_int = 'y';`<br>　`else`<br>　　`;`<br>`else`<br>　`printf("a is <= 0\n");` | `if (a > 0) {`<br>　`if (b > 0)`<br>　　`valid_int = 'y';`<br>`}`<br>`else`<br>　`printf("a is <= 0\n");` |

### 图 7.6：缺少 else 的两种解决方案

## 7.13 `leap_year_check2.c`：使用 if-if-else 结构的程序

让我们通过改进之前的一个闰年检查程序来结束关于 `if` 语句的讨论。修订版（程序 7.6）包含对“世纪”年份（如 1900、2000 等）的特殊检查。我们使用一个对称的嵌套 `if-if-else` 结构，其中没有遗漏任何 `else`。变量 `is_leap_year` 的使用应该会让人大开眼界，因为它的使用方式非常巧妙。

你知道，并非所有标志世纪更替的年份都是闰年，尽管它们都能被 4 整除。像 1900 和 2000 这样的年份必须能被 400 整除，这意味着 2000 年是闰年，而 1900 年不是。要判断一个年份是否为闰年，我们必须遵循以下步骤：

- 1. 检查该数字是否能被 4 整除。如果不能，则该数字不是闰年，程序终止。
- 2. 如果前一项检查成功，则将该数字除以 100，以判断该年份是否代表世纪更替。如果它不能被 100 整除，则该数字表示闰年，程序终止。
- 3. 如果执行到这里，说明我们处理的是世纪年。现在检查该数字是否能被 400 整除。如果能，则该数字是闰年，程序终止。
- 4. 如果执行到这里，则该数字不表示闰年。

```c
/* leap_year_check2.c: Checks for leap year using nested ifs.
                       This one makes the check for century. */
#include <stdio.h>
int main(void)
{
    short year, years_left;
    char is_leap_year = 'n';

    printf("Enter year for leap year check: ");
    scanf("%hd", &year);

    if (year % 4 == 0)                 /* Includes 1900, 2000, 2008 */
        if (year % 100 == 0)           /* Example year 1900 */
            if (year % 400 == 0)        /* Example year 2000 */
                is_leap_year = 'y';
            else                       /* Example year 1900 */
                years_left = 4;
        else                           /* Example year 2008 */
            is_leap_year = 'y';
    else                               /* Not a leap year */
        years_left = 4 - year % 4;

    /* We now know whether it is a leap year or not */
    if (is_leap_year == 'y')
        printf("%d is a leap year.\n", year);
    else
        printf("%d is not a leap year. Next leap year: %d.\n",
               year, year + years_left);

    return 0;
}
```

### 程序 7.6：**leap_year_check2.c**

| 程序输出 |
| --- |
| 输入要检查的年份：**2016**<br>2016 年是闰年。 |
| 输入要检查的年份：**2013**<br>2013 年不是闰年。下一个闰年：2016。 |
| 输入要检查的年份：**1900**<br>1900 年不是闰年。下一个闰年：1904。 |
| 输入要检查的年份：**2000**<br>2000 年是闰年。 |

### 程序输出：**leap_year_check2.c**
