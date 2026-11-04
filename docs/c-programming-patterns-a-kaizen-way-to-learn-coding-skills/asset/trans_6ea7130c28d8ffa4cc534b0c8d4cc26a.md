

| 行级重复操作 | 预期输出 |
| 变量：row | 列级重复操作 | |
|  | 变量：col | |
|  | 打印空格字符(s) | 打印星号字符(s) | |
|  | min_val | max_val 默认 | min_val | max_val | |
| 1 | 0 | 0 | row | totalRows | * * * * |
| 2 | 1 | 1 | row | totalRows | * * * |
| 3 | 1 | 2 | row | totalRows | * * |
| 4 | 1 | 3 | row | totalRows | * * |
| 5 | 1 | 4 | row | totalRows | * |

条件 (col >= row) 给出了最小限制，是一个起点，从该起点开始打印星号("*")字符(s)，直到变量 col 的最大值为 totalRows。

if 条件可以用比较和逻辑运算符给出，范围在 (row) 和 totalRows 之间，如下：

If ( col >= row && col <= totalRows).

我们可以消除逻辑与条件( col <= totalRows) ，因为该条件已在列级内部 for 循环中被考虑。

因此 if 条件可以写为；

If ( col >= row )
我们可以将其总结如下：

![](img/67765455776ddeb6395161cd553ecd87_146_0.png)

程序可以写成如下：

## PatternD1.c
```
#include <stdio.h>
int main() {
    int totalRows = 5; // total number of rows to display

    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = 1; row <= totalRows; row++) {

        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        for (int col = 1; col <= totalRows; col++) {

            if (col >= row) {
                // Action2.prints star "*" character
                printf("* ");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }
        }
        printf("\n");// Move cursor to the next row

    }

    return 0;
}
```

### 输出
* * * *
  * * *
    * *
      *
        *

## 现在，测试不同行数的情况，设为 10。

## PatternD1.C
```c
#include <stdio.h>
int main() {

    int totalRows = 10; // total number of rows to display

    // Row level Repetitive Action :
    // Action1:Executes Column level Repetitive Action
    // Action2:Move cursor to next row.
    for (int row = 1; row <= totalRows; row++) {

        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        for (int col = 1; col <= totalRows; col++) {

            if (col >= row) {
                // Action2.prints star "*" character
                printf("*");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }
        }
        printf("\n");// Move cursor to the next row
    }

    return 0;

}
```

### 输出
```
* * * * * * * * * *
  * * * * * * * * *
    * * * * * * * *
      * * * * * * *
        * * * * * *
          * * * * *
            * * * *
              * *
                *
```

## 问题 D1:
编写一个程序来生成模式 **Pattern1D**，遵循打印空格字符的条件表达式。当条件表达式为 **true** 时，程序应打印空格字符，当条件为 **false** 时打印星号字符。

| 当条件为 **True** 时对变量 **col** 的每个值打印一个空格 | | | | |
|---|---|---|---|---|
| col=1 | col=2 | col=3 | col=4 | col=5 |
| 如果 ( condition=(?) 为 True) 打印空格字符 **Else** 打印星号字符 | | | | |

## 问题 D2.
编写一个程序来生成模式 **Pattern1D**，使用列中给出的信息 →变量：row，字符计数和总字符数。

变量 **totalRows = 5** 表示行数。程序也应适用于 10 行，并且通过将变量 **totalRows = 10** 修改即可输出。

| 行级重复操作 | | | | | 预期输出 |
|---|---|---|---|---|---|
| 变量：row | 列级重复操作 | | | | |
| | 变量：spaces | 变量：col | 字符计数 | 总字符数 | |
| 1 | 0(无空格) | 1, 2, 3, 4, 5 | 0 个空格 + 5 个星号 | 5 | * * * * * |
| 2 | 1 | 2, 3, 4, 5 | 1 个空格 + 4 个星号 | 5 | * * * * |
| 3 | 1,2 | 3, 4, 5 | 2 个空格 + 3 个星号 | 5 | * * * |
| 4 | 1,2,3 | 4, 5 | 3 个空格 + 2 个星号 | 5 | * * |
| 5 | 1,2,3,4 | 5 | 4 个空格 + 1 个星号 | 5 | * |

此页特意留空。

## Pattern1E

我们的编程任务是在计算机屏幕的某一部分输出此模式，如下所示。我们可以将计算机屏幕视为 (row, column) 数值配对框的组合，这些框遍布整个屏幕。每个框仅被视为单个字符的驻留。

![](img/67765455776ddeb6395161cd553ecd87_151_0.png)

![](img/67765455776ddeb6395161cd553ecd87_151_1.png)

### 输出分析

我们看到完整的模式可以很容易地表示为所选 (row, column) 数值对的集合。(行号，列号) 数值对的选择将基于用于设计给定模式的键盘字符。利用这种数值对编号方案，我们可以正确地定位计算机屏幕上的特定键盘字符。任何所选数值对中的第一个值表示行号，第二个值表示列号。例如；

(2, 4) 表示表格中第 2 行第 4 列的字符 "*"。

| | 列=1 | 列=2 | 列=3 | 列=4 | 列=5 | 列=6 | 列=7 | 列=8 | 列=9 |
|---|---|---|---|---|---|---|---|---|---|
| 行=1 | space | space | space | space | *(1,5) | space | space | space | space |
| 行=2 | space | space | space | *(2,4) | *(2,5) | *(2,6) | space | space | space |
| 行=3 | space | space | *(3,3) | *(3,4) | *(3,5) | *(3,6) | *(3,7) | space | space |
| 行=4 | space | *(4,2) | *(4,3) | *(4,4) | *(4,5) | *(4,6) | *(4,7) | *(4,8) | space |
| 行=5 | *(5,1) | *(5,2) | *(5,3) | *(5,4) | *(5,5) | *(5,6) | *(5,7) | *(5,8) | *(5,9) |

Space → space 也是一个字符，就像任何其他字符一样。如果在空白区域或间隙之后在屏幕上显示非空格字符或文本，则意味着在之后打印任何其他非空格字符(s) 之前必须打印许多空格字符。

| 模式生成步骤 | 计算机屏幕 |
|---|---|
| **行 = 1**<br>在同一第 1 行打印空格 " " 4 次。<br>在同一第 1 行打印星号 "*" 一次<br>然后移动到下一行编号 2。 | 网格包含列 1-9 和行 1-5；星号位于第 1 行、第 5 列；第 1 行的打印部分由实线边框包围；箭头指向第 2 行。 |
| **行 = 2**<br>在同一第 2 行打印空格 " " 3 次。<br>在同一第 2 行打印星号 "*" 3 次<br>然后移动到下一行编号 3。 | 网格包含列 1-9 和行 1-5；星号位于第 1 行第 5 列，第 2 行列 4-5；第 1-2 行的打印部分由实线边框包围；箭头指向第 3 行。 |
| **行 = 3**<br>在同一第 3 行打印空格 " " 2 次。<br>在同一第 3 行打印星号 "*" 5 次<br>然后移动到下一行编号 4。 | 网格包含列 1-9 和行 1-5；星号位于第 1 行第 5 列，第 2 行列 4-5，第 3 行列 3-7；第 1-3 行的打印部分由实线边框包围；箭头指向第 4 行。 |
| **行 = 4**<br>在同一第 4 行打印空格 " " 1 次。<br>在同一第 4 行打印星号 "*" 7 次<br>然后移动到下一行编号 5。 | 网格包含列 1-9 和行 1-5；星号位于第 1 行第 5 列，第 2 行列 4-5，第 3 行列 3-7，第 4 行列 2-8；第 1-4 行的打印部分由实线边框包围；箭头指向第 5 行。 |
| **行 = 5**<br>在同一第 5 行打印空格 " " 0 次。<br>在同一第 5 行打印星号 "*" 9 次<br>然后移动到下一行编号 6。 | 网格包含列 1-9 和行 1-5；星号位于第 1 行第 5 列，第 2 行列 4-5，第 3 行列 3-7，第 4 行列 2-8，第 5 行列 1-9；第 1-5 行的打印部分由实线边框包围；箭头指向第 6 行。 |

## 将步骤转换为 C 程序。

### 使用 C 内置方法

| 描述 | C 语句 |
|---|---|
| 移动到下一行 | `printf("\n");` |
| 移动到下一个 (row, col) 位置并在同一行打印空格 " " 字符 | `printf(" ");` |
| 移动到下一个 (row, col) 位置并在同一行打印星号 "*" 字符 | `printf("*");` |

上述三种类型的编程语句预计在程序中会重复多次。因此我们可以使用 **for-loop** 来实现。

