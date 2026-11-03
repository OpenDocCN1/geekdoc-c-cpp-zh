

```c
// calculate amount on deposit for each of ten years
for (unsigned int year = 1; year <= 10; ++year) {

    // calculate new amount for specified year
    double amount = principal * pow(1.0 + rate, year);

    // output one table row
    printf("%4u%21.2f\n", year, amount);
}
```

| 年份 | 存款金额 |
|------|-------------------|
| 1 | 1050.00 |
| 2 | 1102.50 |
| 3 | 1157.63 |
| 4 | 1215.51 |
| 5 | 1276.28 |
| 6 | 1340.10 |
| 7 | 1407.10 |
| 8 | 1477.46 |
| 9 | 1551.33 |
| 10 | 1628.89 |

图 4.6 | 计算复利。（第 2 部分，共 2 部分。）

`for` 语句会将循环体执行 10 次，控制变量从 1 递增到 10，每次增量为 1。虽然 C 语言没有指数运算符，但我们可以使用标准库函数 `pow`（第 18 行）来实现这一目的。函数 `pow(x, y)` 计算 `x` 的 `y` 次方的值。它接收两个 `double` 类型的参数，并返回一个 `double` 类型的值。

> **软件工程观察 4.2**
> `double` 与 `float` 一样都是浮点类型，但通常 `double` 类型的变量能够以比 `float` 更高的精度存储数值大得多的量。`double` 类型的变量比 `float` 类型的变量占用更多内存。除极少数对内存要求非常苛刻的应用外，专业程序员通常更倾向于使用 `double` 而不是 `float`。

只要使用了 `pow` 这样的数学函数，就应该包含头文件 `<math.h>`（第 4 行）。如果没有包含 `math.h`，该程序将无法正常链接，因为链接器会找不到 `pow` 函数。`pow` 函数要求两个 `double` 参数，但变量 `year` 是整数。`math.h` 文件中的信息会告诉编译器在调用该函数之前，将 `year` 的值转换为临时的 `double` 表示。这些信息包含在 `pow` 的函数原型中。这些内容将在第 5 章中说明，那里还会介绍 `pow` 函数以及其他数学库函数的摘要。

### 关于使用 `float` 或 `double` 表示货币金额的告诫

请注意，我们将变量 `amount`、`principal` 和 `rate` 定义为 `double` 类型。这样做只是为了简化，因为我们处理的是美元的小数部分。

> **错误预防提示 4.5**
> 不要使用 `float` 或 `double` 类型的变量进行货币计算。浮点数的不精确性可能导致错误，从而产生不正确的货币值。[在练习 4.23 中，我们探讨了使用整数形式的“分”来进行精确货币计算的方法。]

下面简单说明使用 `float` 或 `double` 表示美元金额时可能出现的问题。机器中存储的两个 `float` 美元金额可能是 14.234（使用 `%.2f` 打印为 14.23）和 18.673（使用 `%.2f` 打印为 18.67）。当这两个金额相加时，得到总和 32.907，使用 `%.2f` 打印为 32.91。因此你的打印结果可能显示为

```
  14.23
+ 18.67
------
  32.91
```

显然，按打印出来的各个数字相加，结果应该为 32.90！你已经得到警告了！

### 格式化数值输出

程序中使用转换说明符 `%21.2f` 来打印变量 `amount` 的值。转换说明符中的 `21` 表示输出该值所用的字段宽度。字段宽度为 21 意味着打印的值将占据 21 个打印位置。其中的 `2` 表示精度（即小数位数）。如果显示出的字符数小于字段宽度，那么该值将自动右对齐，并在字段左侧填充空格。这对于对齐具有相同精度的浮点数值尤其有用（这样它们的小数点可以在垂直方向上对齐）。若要在字段中左对齐某个值，可在 `%` 和字段宽度之间放置一个 `-`（负号）。负号也可以用于左对齐整数（例如 `%-6d`）和字符串（例如 `%-8s`）。我们将在第 9 章详细讨论 `printf` 和 `scanf` 强大的格式化功能。

## 4.7 `switch` 多分支选择语句

在第 3 章中，我们讨论了 `if` 单分支选择语句以及 `if...else` 双分支选择语句。有时，算法会包含一系列判断，这些判断会对同一个变量或表达式可能取到的各个常量整数值分别进行测试，并根据不同情况执行不同的操作。这称为多分支选择。C 语言提供了 `switch` 多分支选择语句来处理这类判断。

`switch` 语句由一系列 `case` 标签、一个可选的 `default` 分支以及每个分支要执行的语句组成。图 4.7 使用 `switch` 统计学生在一次考试中获得的各类字母等级的数量。

```c
// Fig. 4.7: fig04_07.c
// Counting letter grades with switch.
#include <stdio.h>

int main(void)
{
    unsigned int aCount = 0;
    unsigned int bCount = 0;
    unsigned int cCount = 0;
    unsigned int dCount = 0;
    unsigned int fCount = 0;

    puts("Enter the letter grades.");
    puts("Enter the EOF character to end input.");
    int grade; // one grade

    // loop until user types end-of-file key sequence
    while ((grade = getchar()) != EOF) {

        // determine which grade was input
        switch (grade) { // switch nested in while

            case 'A': // grade was uppercase A
            case 'a': // or lowercase a
                ++aCount;
                break; // necessary to exit switch

            case 'B': // grade was uppercase B
            case 'b': // or lowercase b
                ++bCount;
                break;

            case 'C': // grade was uppercase C
            case 'c': // or lowercase c
                ++cCount;
                break;

            case 'D': // grade was uppercase D
            case 'd': // or lowercase d
                ++dCount;
                break;

            case 'F': // grade was uppercase F
            case 'f': // or lowercase f
                ++fCount;
                break;

            case '\n': // ignore newlines,
            case '\t': // tabs,
            case ' ': // and spaces in input
                break;
        }
    }
}
```

图 4.7 | 使用 `switch` 统计字母等级。（第 1 部分，共 2 部分。）

它以 `int` 类型返回用户输入的字符。我们可以根据具体用途，将字符视为整数或字符。例如，语句

```
printf("The character (%c) has the value %d.\n", 'a', 'a');
```

使用转换说明符 `%c` 和 `%d` 分别打印字符 `'a'` 及其整数值。结果是

```
The character (a) has the value 97.
```

### ASCII

整数 97 是该字符在计算机中的数值表示。如今许多计算机使用 ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）字符集，在该字符集中，97 表示小写字母 `'a'`。附录 B 列出了所有 ASCII 字符及其十进制值。使用 `scanf` 时，可以通过转换说明符 `%c` 读取字符。

### 赋值表达式具有值

赋值表达式作为一个整体实际上具有一个值。这个值会被赋给 `=` 左侧的变量。赋值表达式 `grade = getchar()` 的值，就是 `getchar` 返回并赋给变量 `grade` 的字符。

赋值具有值这一事实可用于将多个变量设置为同一个值。例如，

```
a = b = c = 0;
```

首先计算赋值 `c = 0`（因为 `=` 运算符从右向左结合）。接着，变量 `b` 被赋值为赋值表达式 `c = 0` 的值（即 0）。然后，变量 `a` 被赋值为赋值表达式 `b = (c = 0)` 的值（也是 0）。在该程序中，赋值表达式 `grade = getchar()` 的值会与 `EOF`（其缩写代表“end of file”，即文件结束）的值进行比较。我们使用 `EOF`（通常值为 -1）作为哨兵值。用户按下系统相关的按键组合来表示“文件结束”——也就是说，不再输入更多数据。`EOF` 是在 `<stdio.h>` 头文件中定义的符号整型常量（我们将在第 6 章了解符号常量是如何定义的）。如果赋给 `grade` 的值等于 `EOF`，程序将终止。在本程序中，我们选择用 `int` 来表示字符，因为 `EOF` 是一个整数值（同样，通常为 -1）。

**可移植性提示 4.1**
输入 `EOF`（文件结束）的按键组合与系统相关。

**可移植性提示 4.2**
与符号常量 `EOF`（而不是 -1）进行比较可以使程序更具可移植性。C 标准规定 `EOF` 是负整数值（但不一定等于 -1）。因此，`EOF` 在不同系统上可能有不同的值。

### 输入 EOF 指示符

在 Linux/UNIX/Mac OS X 系统中，通过输入以下内容来输入 `EOF` 指示符：

```
<Ctrl> d
```

