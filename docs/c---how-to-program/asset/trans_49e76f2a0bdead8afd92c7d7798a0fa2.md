
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

        default: // catch all other characters
            printf("%s", "Incorrect letter grade entered.");
            puts("Enter a new grade.");
            break; // optional; will exit switch anyway
        }
    } // end while

    // output summary of results
    puts("\nTotals for each letter grade are:");
    printf("A: %u\n", aCount);
    printf("B: %u\n", bCount);
    printf("C: %u\n", cCount);
    printf("D: %u\n", dCount);
    printf("F: %u\n", fCount);
}
```

图 4.7 | 使用 switch 计数字母等级。 (第 1 部分，共 2 部分。)

图 4.7 | 使用 switch 计数字母等级。 (第 2 部分，共 2 部分。)

![](img/d0d3b7423c2d9e5650be79209ea1885d_157_0.png)

## 读取字符输入

在程序中，用户为一门课程输入字母等级。在 while 头部（第 18 行），

```c
while ((grade = getchar()) != EOF)
```

带括号的赋值 `(grade = getchar())` 首先执行。`getchar` 函数（来自 <stdio.h>）从键盘读取一个字符并将其存储在整数变量 grade 中。字符通常存储在类型为 char 的变量中。然而，C 的一个重要特性是字符可以存储在任何整数数据类型中，因为它们在计算机中通常表示为一字节整数。`getchar` 函数返回用户输入的作为 `int` 的字符。我们可以根据其用途将字符视为整数或字符。例如，语句

```c
printf("The character (%c) has the value %d.\n", 'a', 'a');
```

使用转换说明符 `%c` 和 `%d` 分别打印字符 `'a'` 及其整数值。结果是

The character (a) has the value 97.

### ASCII

整数 97 是计算机中字符的数值表示。今天许多计算机使用 ASCII（美国信息交换标准代码）字符集，其中 97 表示小写字母 'a'。附录 B 中列出了 ASCII 字符及其十进制值。字符可以使用转换说明符 `%c` 通过 scanf 读取。

### 赋值有值

赋值整体实际上有一个值。该值被赋给等号左侧的变量。赋值表达式 `grade = getchar()` 的值是 `getchar` 返回并赋给变量 grade 的字符。

赋值有值这一事实对于将多个变量设置为相同值很有用。例如，

```c
a = b = c = 0;
```

首先计算赋值 `c = 0`（因为 = 运算符从右到左结合）。然后变量 b 被赋值为赋值 `c = 0` 的值（即 0）。然后，变量 a 被赋值为赋值 `b = c = 0` 的值（也是 0）。在程序中，赋值 `grade = getchar()` 的值与 EOF 的值进行比较（EOF 这个符号的缩写代表“文件结束”）。我们使用 EOF（通常值为 –1）作为哨兵值。用户键入系统相关的键序列来表示“文件结束”——即“我没有更多数据要输入”。EOF 是在 `<stdio.h>` 头文件中定义的符号整数常量（我们将在第 6 章看到符号常量的定义方式）。如果赋给 grade 的值等于 EOF，程序即终止。我们选择在本程序中将字符表示为 ints，因为 EOF 有一个整数值（同样通常为 –1）。

> **可移植性提示 4.1**
>
> 输入 EOF（文件结束）的键组合是系统相关的。

> **可移植性提示 4.2**
>
> 测试符号常量 EOF（而不是 –1）使程序更具可移植性。C 标准规定 EOF 是一个负整数值（但不一定是 –1）。因此，EOF 在不同系统上可能有不同的值。

### 输入 EOF 指示符

在 Linux/UNIX/Mac OS X 系统上，EOF 指示符通过在单独一行键入

```
<Ctrl> d
```

来输入。这种记法 <Ctrl> d 表示同时按下 Ctrl 键和 d 键。在其他系统上，如 Microsoft Windows，EOF 指示符可以通过键入

```
<Ctrl> z
```

来输入。你还需要在 Windows 上按 *回车*。

用户在键盘上输入等级。当按下 *回车* 键时，字符由函数 `getchar` 一次一个地读取。如果输入的字符不等于 EOF，则进入 switch 语句（第 21–57 行）。

## switch 语句细节

关键字 *switch* 后跟放在括号中的变量名 *grade*。这称为控制表达式。该表达式的值与每个 *case* 标签进行比较。假设用户输入字母 C 作为等级。C 会自动与 *switch* 中的每个 case 进行比较。如果发生匹配（case `'C':`），则执行该 case 的语句。对于字母 C 的情况，`cCount` 增加 1（第 35 行），并且 *switch* 语句会立即通过 *break* 语句退出。

*break* 语句使程序控制继续执行 *switch* 语句之后的第一条语句。使用 *break* 语句是因为如果不使用，*switch* 语句中的 *cases* 就会连在一起。如果在 *switch* 语句中任何地方都不使用 *break*，那么每次发生匹配时，该语句中 *所有* 剩余 *cases* 的语句都将被执行。（这种特性称为贯穿， rarely 有用，尽管它非常适合编程练习 4.38——迭代歌曲“十二天的圣诞节”！）如果没有匹配发生，则执行 *default* case，并打印错误消息。

## switch 语句流程图

每个 *case* 可以有一个或多个操作。*switch* 语句与其他所有控制语句不同之处在于，在 *switch* 的一个 *case* 中，多个操作周围 *不需要* 大括号。一般的 *switch* 多选语句（在每个 *case* 中使用 *break*）在图 4.8 中进行了流程图。流程图清楚地表明，每个 *case* 末尾的 *break* 语句会立即使控制退出 *switch* 语句。

> **常见编程错误 4.4**
>
> 在 *switch* 语句中需要时忘记 *break* 语句是一个逻辑错误。

> **错误预防提示 4.6**
>
> 在 *switch* 语句中提供 *default* case。在 *switch* 中未明确测试的值通常会被忽略。*default* case 通过让你关注处理异常条件的需要来帮助防止这种情况。有时不需要 *default* 处理。

> **良好编程实践 4.4**
>
> 尽管 *switch* 语句中的 *case* 子句和 *default* case 子句可以按任何顺序出现，但通常将 *default* 子句放在最后。

> **良好编程实践 4.5**
>
> 在 *switch* 语句中，当 *default* 子句在最后时，*break* 语句不是必需的。你可能更喜欢为了清晰和与其他 case 的对称性而包含此 *break*。
