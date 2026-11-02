
| 头文件 | 说明 |
|---|---|
| `<math.h>` | 包含数学库函数的函数原型。 |
| `<setjmp.h>` | 包含允许绕过通常的函数调用和返回序列的函数的函数原型。 |
| `<signal.h>` | 包含处理程序执行期间可能出现的各种条件的函数原型和宏。 |
| `<stdarg.h>` | 定义用于处理参数数量和类型未知函数的参数列表的宏。 |
| `<stddef.h>` | 包含 C 用于执行计算的常用类型定义。 |
| `<stdio.h>` | 包含标准输入/输出库函数的函数原型，以及它们使用到的信息。 |
| `<stdlib.h>` | 包含数字到文本和文本到数字的转换、内存分配、随机数和其他实用函数的函数原型。 |
| `<string.h>` | 包含字符串处理函数的函数原型。 |
| `<time.h>` | 包含用于操作时间和日期的函数原型和类型。 |

**图 5.10** | 一些标准库头文件。 (第 2 部分，共 2 部分。)

你可以创建自定义头文件。程序员定义的头文件也应使用 `.h` 文件扩展名。可以通过使用 `#include` 预处理指令来包含程序员定义的头文件。例如，如果我们的 square 函数的原型位于头文件 `square.h` 中，我们就可以通过在程序顶部使用以下指令来包含该头文件：

```c
#include "square.h"
```

第 13.2 节介绍了有关包含头文件的额外信息，例如为什么程序员定义的头文件用引号 (`" "`) 而不是尖括号 (`<>`) 括起来。

## 5.9 按值传递参数和按引用传递参数

在许多编程语言中，传递参数有两种方式——按值传递和按引用传递。当参数*按值传递*时，会复制参数的值并将其传递给被调用函数。对副本的更改不会影响调用方中原始变量的值。当参数*按引用传递*时，调用方允许被调用函数*修改*原始变量的值。

只要被调用函数不需要修改调用方原始变量的值，就应使用按值传递。这可以防止意外的副作用（变量修改），而这些副作用极大地阻碍了正确可靠的软件系统的开发。仅应在需要修改原始变量的*受信任*的被调用函数中使用按引用传递。

在 C 语言中，所有参数都是按值传递的。正如我们在第 7 章《C 指针》中将看到的那样，可以通过使用*地址运算符*和*间接运算符*来实现按引用传递。在第 6 章中，我们将看到出于性能原因，数组参数会自动按引用传递。我们将在第 7 章看到，这*不是*矛盾。目前，我们集中讨论按值传递。

## 5.10 随机数生成

我们现在进行一次简短的、希望是有趣的关于*模拟*和*游戏*的插曲。在本节和下一节中，我们将开发一个结构良好的游戏程序，其中包含多个函数。该程序使用了函数和我们已经学习过的几种控制语句。*随机性*可以通过使用来自 `<stdlib.h>` 头文件的 C 标准库函数 `rand` 引入到计算机应用中。

### 获取随机整数值

考虑以下语句：

```c
i = rand();
```

`rand` 函数生成 0 到 `RAND_MAX` 之间的整数（在 `<stdlib.h>` 头文件中定义的符号常量）。标准 C 规定 `RAND_MAX` 的值必须至少为 32767，这是两字节（即 16 位）整数的最大值。本节中的程序在 Microsoft Visual C++ 上进行了测试，最大 `RAND_MAX` 值为 32767，并在 GNU gcc 和 Xcode LLVM 上进行了测试，最大 `RAND_MAX` 值为 2147483647。如果 `rand` 真正*随机*产生整数，则 0 到 `RAND_MAX` 之间的每个数字在每次调用 `rand` 时都有相同的机会（或概率）被选中。

`rand` 直接产生的数字范围通常与特定应用程序的需求不同。例如，模拟抛硬币的程序可能只需要 0 表示“正面”和 1 表示“反面”。模拟六面骰子的掷骰程序需要 1 到 6 的随机整数。

### 掷六面骰子

为了演示 `rand`，让我们开发一个程序（图 5.11）来模拟六面骰子掷 20 次并打印每次掷出的值。

```c
// Fig. 5.11: fig05_11.c
// Shifted, scaled random integers produced by 1 + rand() % 6.
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
   // loop 20 times
   for (unsigned int i = 1; i <= 20; ++i) {

      // pick random number from 1 to 6 and output it
      printf("%10d", 1 + (rand() % 6));

      // if counter is divisible by 5, begin new line of output
      if (i % 5 == 0) {
         puts("");
      }
   }
}
```

**图 5.11** | 由 `1 + rand() % 6` 产生的平移、缩放随机整数。 (第 1 部分，共 2 部分。)

![](img/d0d3b7423c2d9e5650be79209ea1885d_207_0.png)

**图 5.11** | 由 1 + rand() % 6 产生的平移、缩放随机整数。 (第 2 部分，共 2 部分。)

函数 `rand` 的函数原型在 `<stdlib.h>` 中。我们将取余运算符 (%) 与 `rand` 结合使用，如下所示

```c
rand() % 6
```

以产生 0 到 5 范围内的整数。这称为缩放。数字 6 称为缩放因子。然后我们通过在之前的结果上加 1 来平移产生的数字范围。输出确认结果在 1 到 6 的范围内——实际选择的随机值可能会因编译器而异。

### 掷六面骰子 60,000,000 次

为了显示每个数字出现的可能性大致相等，让我们用图 5.12 的程序模拟掷骰子 60,000,000 次。1 到 6 的每个整数应大约出现 10,000,000 次。

```c
// Fig. 5.12: fig05_12.c
// Rolling a six-sided die 60,000,000 times.
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    unsigned int frequency1 = 0; // rolled 1 counter
    unsigned int frequency2 = 0; // rolled 2 counter
    unsigned int frequency3 = 0; // rolled 3 counter
    unsigned int frequency4 = 0; // rolled 4 counter
    unsigned int frequency5 = 0; // rolled 5 counter
    unsigned int frequency6 = 0; // rolled 6 counter

    // loop 60000000 times and summarize results
    for (unsigned int roll = 1; roll <= 60000000; ++roll) {
        int face = 1 + rand() % 6; // random number from 1 to 6

        // determine face value and increment appropriate counter
        switch (face) {

            case 1: // rolled 1
                ++frequency1;
                break;

            case 2: // rolled 2
                ++frequency2;
                break;

29
30            case 3:  // rolled 3
31                ++frequency3;
32                break;
33
34            case 4:  // rolled 4
35                ++frequency4;
36                break;
37
38            case 5:  // rolled 5
39                ++frequency5;
40                break;
41
42            case 6:  // rolled 6
43                ++frequency6;
44                break;  // optional
45        }
46
47
48        // display results in tabular format
49        printf("%s%13s\n", "Face", "Frequency");
50        printf("%13u\n", frequency1);
51        printf("%13u\n", frequency2);
52        printf("%13u\n", frequency3);
53        printf("%13u\n", frequency4);
54        printf("%13u\n", frequency5);
55        printf("%13u\n", frequency6);
56    }
}
```

**图 5.12** | 掷六面骰子 60,000,000 次。 (第 1 部分，共 2 部分。)

| 点数 | 频率 |
| --- | --- |
| 1 | 9999294 |
| 2 | 10002929 |
| 3 | 9995360 |
| 4 | 10000409 |
| 5 | 10005206 |
| 6 | 9996802 |

**图 5.12** | 掷六面骰子 60,000,000 次。 (第 2 部分，共 2 部分。)

正如程序输出所示，通过缩放和平移，我们已使用 rand 函数真实地模拟了六面骰子的掷骰。注意使用 %s 转换说明符将字符字符串 "Face" 和 "Frequency" 打印为列标题（第 49 行）。在第 6 章学习数组后，我们将展示如何优雅地用单行语句替换这 26 行 switch 语句。

### 随机化随机数生成器

再次执行图 5.11 的程序会产生

| | | | | |
|---|---|---|---|---|
| 6 | 6 | 5 | 5 | 6 |
| 5 | 1 | 1 | 5 | 3 |
| 6 | 6 | 2 | 4 | 2 |
| 6 | 2 | 3 | 4 | 1 |
