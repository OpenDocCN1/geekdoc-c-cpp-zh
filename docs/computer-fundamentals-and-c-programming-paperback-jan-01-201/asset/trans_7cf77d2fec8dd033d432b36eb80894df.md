

不过，我们有时可以在控制表达式本身中更新关键变量，从而省去循环体中的一条语句。下面这段与程序 `while_intro.c` 相关的代码同样可以正常工作：

```c
short i = 0, sum = 0;
while (++i <= 10) {
    sum += i;
    printf("%hd ", sum);
}
printf("\nSum of first 10 integers = %hd\n", sum);
```

i 初始化为 0 而非 1；使用 ++i 而非 i；输出 55

关键变量 i 的更新现在已移入控制表达式，但这种移动也需要改变 i 的初始值。

> **注意：**当你在控制表达式中将关键变量改为带有前缀或后缀运算符的形式时，还需要相应修改关系运算符（例如，将 > 改为 >=）或关键变量的初始值。

## 8.3 三个使用 `while` 的程序

在继续探索 C 语言中的这个循环之前，让我们先来看三个使用了简单控制表达式的程序。这些程序都会在后续章节中被修订，以使用数组和函数。其中两个后续版本还会使用*递归*技术，而这里采用的是循环的*迭代*方法。

### 8.3.1 `factorial.c`：计算一个数的阶乘

正整数 *n* 的阶乘（记作 *n*!）是所有小于或等于 *n* 的正整数的乘积。因此，4! = 4 × 3 × 2 × 1 = 24。程序 8.2 使用 `while` 循环来计算用户提供的整数的阶乘。第 11.13.1 节展示了使用函数解决同一问题的另一种方法。

```c
/* factorial.c: Program to determine factorial of a number
                  without using a function. */
#include <stdio.h>
int main(void)
{
    short num1, num2;
    unsigned int factorial = 1;      /* unsigned doubles the maximum value */
    printf("Factorial of which number? ");
    scanf("%hd", &num1);
    num2 = num1;                     /* Saving num1 before it changes */
    while (num1 >= 1) {
        factorial *= num1;
        num1--;
    }
    printf("Factorial of %hd = %d\n", num2, factorial);
    return 0;
}
```

程序 8.2：`factorial.c`

| 求哪个数的阶乘？ | 结果 |
|---|---|
| 4 | 4 的阶乘 = 24 |
| 6 | 6 的阶乘 = 720 |
| 1 | 1 的阶乘 = 1 |

程序输出：**factorial.c**

### 8.3.2 `extract_digits.c`：反转整数各位数字的程序

程序 8.3 执行两项任务：反转一个整数的各位数字并打印它们的和。以 10 作为除数，使用 / 和 % 运算符从右侧逐个提取数字。该程序的缺点是没有保存这些数字，因此打印完成后无法对它们执行任何其他操作。

```c
/* extract_digits.c: Reverses the digits of an integer. Prints and sums
   the digits using the % and / operators. */
#include <stdio.h>
int main(void)
{
    unsigned int number;
    short last_digit, sum = 0;

    printf("Key in an integer: ");
    scanf("%d", &number);

    while (number != 0) {
        last_digit = number % 10;          /* Extracts last digit */
        number = number / 10;              /* Removes last digit */
        sum += last_digit;
        printf("%hd ", last_digit);
    }
    printf("\nSum of digits: %hd\n", sum);
    return 0;
}
```

程序 8.3：**extract_digits.c**

```
Key in an integer: 13569
9 6 5 3 1
Sum of digits: 24
```

程序输出：**extract_digits.c**

在 **while** 循环的每次迭代中，/ 操作会移除最后一位数字，% 操作会保存该数字。这就是变量 `last_digit` 和 `number` 的值在每次循环迭代中的变化方式：

| | 迭代 1 | 迭代 2 | 迭代 3 | 迭代 4 | 迭代 5 |
|---|---|---|---|---|---|
| last_digit | 9 | 6 | 5 | 3 | 1 |
| number | 1356 | 135 | 13 | 1 | 0 |

该程序不够灵活；我们无法用这种技术按数字在数中出现的顺序打印它们。我们需要保存每一位数字，不是用五个变量，而是用一个包含五个元素的*数组*。我们将在第 10.7.1 节重新讨论这个程序。

### 8.3.3 `fibonacci_ite.c`：打印并求和斐波那契数

每个计算机科学专业的学生在学习过程中都会在某一点遇到斐波那契数列。在这个以 0 和 1 开头的数列中，每个后续项都是前两项之和。这种关系可以从该数列的前 12 项中看出：

0 1 1 2 3 5 8 13 21 34 55 89

这里，55 是它的两个前项 34 和 21 之和，而 21 是 13 和 8 之和。程序 8.4 打印并求和该数列的 *n* 项，其中 *n* 由用户提供。该程序使用一个运行 *n* 次的 **while** 循环。在每次迭代中，变量 prev1 和 prev2 的和被保存在 sum 中并打印。注意，前两项是由逻辑生成的，并没有对它们进行特殊处理。这是通过仔细选择四个变量的初始值而实现的。

```c
/* fibonacci_ite.c: Uses the iterative technique to generate terms of
   the Fibonacci series and compute the sum of terms. */

#include <stdio.h>
int main(void)
{
    short num;
    unsigned long prev1 = 0, prev2 = 0, sum = 1, sum_terms = 0;
    short i = 0;

    printf("Enter last term of series: ");
    scanf("%hd", &num);

    while (i++ < num) {
        printf("%ld ", sum);          /* Prints each term */
        sum_terms += sum;             /* Sums all terms */
        prev1 = prev2;
        prev2 = sum;
        sum = prev1 + prev2;          /* Sums previous two terms */
    }
    printf("\nSum of first %hd terms = %ld\n", num, sum_terms);
    return 0;
}
```

**程序 8.4：** `fibonacci_ite.c`

```
Enter last term of series: 15
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610
Sum of first 15 terms = 1596
```

程序输出：**fibonacci_ite.c**

斐波那契数列也可以使用*递归*函数生成，即一个不断调用自身的函数。第 11.4.3 节将考察这个函数及其与这里使用的迭代方法相比的缺点。

## 8.4 加载控制表达式

重复性为使用函数作为控制表达式创造了机会。例如，**getchar** 函数是 I/O 函数家族的一员，它从键盘获取一个字符并返回其 ASCII 值。**putchar** 函数使用该值来显示字符。考虑以下代码片段：

```
int c;
c = getchar();                 Gets the first character
while (c != EOF) {             EOF is end-of-file
    putchar(c);                Displays the character
    c = getchar();             Fetches the next character
}
```

这看起来是一种从键盘输入中检索文本字符串的简单方法。但由于 **getchar** 返回所获取字符的 ASCII 值，你可以将 **getchar** 语句本身移入控制表达式：

```c
while ((c = getchar()) != EOF)
    putchar(c);
```

这样既能完美工作，看起来也很简洁，因为只使用了一个 **getchar**。!= 的优先级高于 =，因此必须在赋值语句 (c = getchar()) 周围加上括号。这确保了在将 c 与 EOF（文件结束符）比较之前，**getchar** 的返回值已赋给 c。

许多函数会返回一个值。**scanf** 返回成功读取的项目数，**printf** 返回写入的字符数，因此这些函数也可以用作控制表达式：

```c
while (scanf("%d", &num) == 1)
while (printf("Enter the amount: "))
```

**getchar** 和 **putchar** 都将在第 9 章中讨论，该章会考察主要的 I/O 函数。**scanf** 和 **printf** 函数也会在同一章中讨论。

### 8.4.1 将整个循环体合并到控制表达式中

前面的示例将两次调用 **getchar** 合并为控制表达式中的一次调用。但 **putchar** 也返回一个值（即所写入字符的值），那么为什么不也把它移入控制表达式呢？是的，我们也可以这样做：

