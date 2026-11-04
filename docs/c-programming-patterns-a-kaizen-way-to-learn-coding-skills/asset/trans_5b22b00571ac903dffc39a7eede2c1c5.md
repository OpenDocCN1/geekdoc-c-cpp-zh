
## 替代方案2

从之前的解法，当 if 条件为真时我们将打印一个星号("*")字符，而在 if 语句的 else 部分我们将打印空格。让我们从之前解法中得到的观察表开始。

| 行 | 空格最小值 | 空格最大值 | 列最小值 | 列最大值 | 预期输出 |
|---|---|---|---|---|---|
| 1 | 1 | 4 | 5 | 5 | * |
| 2 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 1 | 2 | 8 | * * * * * * * |
| 5 | 0 | 0 | 1 | 9 | * * * * * * * * * |

反转变量 row 的计数器值，即 row = 5, 4, 3, 2, 1，以便使其与变量 col 的列最小值匹配。

| 行 | 空格最小值 | 空格最大值 | 列最小值 | 列最大值 | 预期输出 |
|---|---|---|---|---|---|
| 5 | 1 | 4 | 5 | 5 | * |
| 4 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 2 | 1 | 1 | 2 | 8 | * * * * * * * |
| 1 | 0 | 0 | 1 | 9 | * * * * * * * * * |

我们可以使用变量 totalRows 来概括用于打印星号字符的列最大值。

| 行 | 空格最小值 | 空格最大值 | 列最小值 | 列最大值 | 预期输出 |
|---|---|---|---|---|---|
| 5 | 1 | 4 | row | 5 + 0 / totalRows + 0 | * |
| 4 | 1 | 3 | row | 5 + 1 / totalRows + 1 | * * * |
| 3 | 1 | 2 | row | 5 + 2 / totalRows + 2 | * * * * * |
| 2 | 1 | 1 | row | 5 + 3 / totalRows + 3 | * * * * * * * |
| 1 | 0 | 0 | row | 5 + 4 / totalRows + 4 | * * * * * * * * * |

变量 col 的列最大值的表达式的一部分在每一行仍具有不同的数值。

| 变量：行 | 变量：列（最小值） | 最大值 | 1 | 2 | 3 | 预期输出 |
|---|---|---|---|---|---|---|
| 5 | row | 5 | 5+0 | totalRows+0 | totalRows+0 | * |
| 4 | row | 6 | 5+1 | totalRows+1 | totalRows+5-4 | * * * |
| 3 | row | 7 | 5+2 | totalRows+2 | totalRows+5-3 | * * * * * |
| 2 | row | 8 | 5+3 | totalRows+3 | totalRows+5-2 | * * * * * * * |
| 1 | row | 9 | 5+4 | totalRows+4 | totalRows+5-1 | * * * * * * * * * |

变量 col 的列最大值的表达式的一部分与行值匹配。

| 变量：行 | 变量：列（最小值） | 最大值 | 4 | 5 | 预期输出 |
|---|---|---|---|---|---|
| 5 | row | 5 | totalRows + 5 - 5 | totalRows + totalRows - 5 | * |
| 4 | row | 6 | totalRows + 5 - 4 | totalRows + totalRows - 4 | * * * |
| 3 | row | 7 | totalRows + 5 - 3 | totalRows + totalRows - 3 | * * * * * |
| 2 | row | 8 | totalRows + 5 - 2 | totalRows + totalRows - 2 | * * * * * * * |
| 1 | row | 9 | totalRows + 5 - 1 | totalRows + totalRows - 1 | * * * * * * * * * |

条件 (col >= row) 给出了 for 循环开始打印星号("*")字符的起点，直到变量 col 的最大值，该最大值对 row 的每个值都是 (2 * totalRows - row)。if 条件可以使用比较和逻辑运算符给出，范围在 (row) 和 (2 * totalRows - row) 之间，如下所示：

```text
If ( col >= ( row ) && col <= (2 * totalRows - row ) ) ← Same expression
```

我们已经知道；

```text
variable col = 1,2,3,4,5 or 1,2,3,4, ...,(2 * totalRows - row)
variable row = 5,4,3,2,1 or totalRows,4,3,2,1
```

我们可以消除 if 条件中的逻辑 AND(&&) 条件( col <= (2 * totalRows - row) )。此逻辑 AND(&&) 条件已作为列级内部 for 循环中的循环条件得到处理。

因此 if 条件现在简化为 If ( col >= row )。我们可以将其总结如下；

**当条件对变量 col 的每个值都为真时打印星号**

| col=1 | col=2 | col=3 | col=4 | ....................................... | col= (2 * totalRows - row) |
|---|---|---|---|---|---|
| **如果 ( 条件=( col >= row ) 为真)**<br>**打印星号字符**<br>**否则**<br>**打印空格字符** |  |  |  |  |  |

我们将列最大值中的非重复数字模式概括为一个表达式。

我们现在可以定义列级 *for 循环*。

| *列级 for 循环的元素* |  |
|---|---|
| 最小值 | 1 |
| 最大值 | (2 * totalRows - row) |
| 变量名 | col |
| 语句 | `printf("* ");` |

### 行级重复操作

以下语句重复了 5 次（总行数）。

**列级 for 循环** for printing **星号字符** // *内部 for 循环*

```c
printf("\n");// Move cursor to the next row
```

我们已为**每一行**分配了**唯一值**，从 5 开始到 1。

让我们考虑；

**row →** 变量 **整数类型** 用于一次存储一个整数值并表示 5 到 1 之间的行号。**totalRows** 最初被赋值为 5。

我们已经获得了与行级重复相关的 **for 循环** 的所有内容。

| *行级递减 for 循环的元素* |  |
|---|---|
| 最小值 | 1 |
| 最大值 | totalRows |
| 变量名 | **row** |
| 语句 | **列级 for 循环** for printing **星号字符**<br>`printf("\n"); //Moves cursor to the next row` |

让我们执行以下程序。

## PatternE.C

```c
#include <stdio.h>
int main() {

    int totalRows = 5; // total number of rows to display

    // Row level Repetitive Action:
    // Action1. Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = totalRows; row >= 1; row--) {

        // Column level Repetitive Action :

        // Action1.Move cursor in the same row
        for (int col = 1; col <= (2 * totalRows - row); col++) {

            if (col >= row) {
                // Action2.prints star "*" character
                printf("* ");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }

        }// inner for-loop

        printf("\n\n");// Move cursor to the next row

    }// outer for-loop

    return 0;

}
```

### 输出

```text
        *
      * *
    * * *
  * * * * *
* * * * * * *
```

## Pattern1F

我们的编程工作是输出此模式在计算机屏幕的一部分上，如下所示。我们可以将计算机屏幕视为 (row, column) 数字值配对框的组合，这些框遍布整个屏幕。每个框被视为仅驻留一个字符。

![](img/67765455776ddeb6395161cd553ecd87_162_0.png)

![](img/67765455776ddeb6395161cd553ecd87_162_1.png)

### 输出分析

我们看到完整的模式可以很容易地表示为所选 (row, column) 数字值对的集合。 (行号，列号) 数字对的选择将基于用于设计给定模式的键盘字符。凭借此数字对编号方案，我们可以正确地在计算机屏幕上定位特定键盘字符。任何所选数字对中的第一个值表示行号，第二个值表示列号。例如：

(2, 4) 表示字符“*”在表格中位于**第二行**和**第四列**。

|  | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 | Col=6 | Col=7 | Col=8 | Col=9 |
|---|---|---|---|---|---|---|---|---|---|
| **Row=1** | *(1,1) | *(1,2) | *(1,3) | *(1,4) | *(1,5) | *(1,6) | *(1,7) | *(1,8) | *(1,9) |
| **Row=2** | space | *(2,2) | *(2,3) | *(2,4) | *(2,5) | *(2,6) | *(2,7) | *(2,8) | space |
| **Row=3** | space | space | *(3,3) | *(3,4) | *(3,5) | *(3,6) | *(3,7) | space | space |
| **Row=4** | space | space | space | *(4,4) | *(4,5) | *(4,6) | space | space | space |
| **Row=5** | space | space | space | space | *(5,5) | space | space | space | space |

***实际挑战是通过编写程序找到计算机屏幕上正确的 (row, col) 位置。这将通过应用 for 循环以及适当的逻辑条件来完成。这促进了算法思维的成长，这是自信程序员的基本要求。***
