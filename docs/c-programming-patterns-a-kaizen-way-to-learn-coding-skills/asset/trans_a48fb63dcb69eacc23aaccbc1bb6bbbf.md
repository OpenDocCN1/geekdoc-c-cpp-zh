
## 问题 H1。

延续之前的程序（*PatternH1.c*），针对以下情况修改程序。

在程序（*PatternH1.c*）中，计数变量以值 -1 开始，如下所示：

```c
int count = -1;// counter to increment/decrement
```

需要通过以下更改，使修改后的程序（*PatternH1_2.c*）的输出与（*PatternH1*）的输出匹配：

```c
int count = 0;// counter to increment/decrement
```

这一次，程序必须将变量 count 初始化为值 0 而不是 -1，并且仍然应给出与模式程序（*PatternH1.c*）正确匹配的输出。

### PatternH1_2.C

```c
#include <stdio.h>
int main() {
        int totalRows = 7;// number of rows to display
        int count = 0;// counter to increment/decrement.

        // Row level Repetitive Action:
        // Action1: Executes Column level Repetitive Action
        // Action2: Move cursor to next row.

        // Write your logic

        return 0;
}
```

### 输出

```text
        *
      * * *
    * * * * *
  * * * * * * *
* * * * * * * * * *
* * * * * * * * * * * *
* * * * * * * * * * * * *
  * * * * * * * * * * *
    * * * * * * * *
      * * * * *
        * * *
          *
```

## 备选方案2

让我们从之前解决方案中得到的一个逻辑追踪表开始。

| 行级重复操作（变量：row） | 列级重复操作（变量：col）：打印空格字符 最小值 | 最大值 | 打印星号字符 最小值 | 最大值 | 预期输出 |
|---|---|---|---|---|---|
| 1 | 1 | 4 | 5 | 5 | * |
| 2 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 1 | 2 | 8 | * * * * * * * |
| 5 | 0 | 0 | 1 | 9 | * * * * * * * * * |
| 6 | 1 | 1 | 2 | 8 | * * * * * * * |
| 7 | 1 | 2 | 3 | 7 | * * * * * |
| 8 | 1 | 3 | 4 | 6 | * * * |
| 9 | 1 | 4 | 5 | 5 | * |

让我们重点关注星号字符的打印，并尝试找出用变量（即 row 和 totalRows=5）表示的表达式。

| 行 | 星号最小值（默认） | 星号最小值（1） | 星号最小值（2） | 星号最大值（默认） | 星号最大值（1） | 星号最大值（2） |
|---|---|---|---|---|---|---|
| 1 | 5 | 5-0 | totalRows +1 - 1 | 5 | totalRows +0 | totalRows +1 - 1 |
| 2 | 4 | 5-1 | totalRows +1 - 2 | 6 | totalRows +1 | totalRows +2 - 1 |
| 3 | 3 | 5-2 | totalRows +1 - 3 | 7 | totalRows +2 | totalRows +3 - 1 |
| 4 | 2 | 5-3 | totalRows +1 - 4 | 8 | totalRows +3 | totalRows +4 - 1 |
| 5 | 1 | 5-4 | totalRows +1 - 5 | 9 | totalRows +4 | totalRows +5 - 1 |
| 6 | 2 | 2 | 2 | 8 | totalRows +3 | totalRows +5 - 2 |
| 7 | 3 | 3 | 3 | 7 | totalRows +2 | totalRows +5 - 3 |
| 8 | 4 | 4 | 4 | 6 | totalRows +1 | totalRows +5 - 4 |
| 9 | 5 | 5 | 5 | 5 | totalRows +0 | totalRows +5 - 5 |

我们可以使用 row=1,2,3,4,5 的值来部分表示列的最小值和最大值。

| 行 | 星号最小值（默认） | 星号最小值表达式 | 星号最大值（默认） | 星号最大值表达式（1） | 星号最大值表达式（2） |
|---|---|---|---|---|---|
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 | totalRows + row - 1 |
| 6 | 2 | 2 | 8 | totalRows +5 - 2 | 2*totalRows - 2 |
| 7 | 3 | 3 | 7 | totalRows +5 - 3 | 2*totalRows - 3 |
| 8 | 4 | 4 | 6 | totalRows +5 - 4 | 2*totalRows - 4 |
| 9 | 5 | 5 | 5 | totalRows +5 - 5 | 2*totalRows - 5 |

| 变量 row | 星号最小值（默认） | 星号最小值表达式 | 星号最大值（默认） | 星号最大值表达式（1） | 星号最大值表达式（2） |
|---|---|---|---|---|---|
| 0 | 0 | 3 | 0 | 4 | 5 |
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 | totalRows + row - 1 |
| 6 | 2 | (6 - 4) | 8 | 2*totalRows - (6 - 4) | 2*totalRows - 6 + 4 |
| 7 | 3 | (7 - 4) | 7 | 2*totalRows - (7 - 4) | 2*totalRows - 7 + 4 |
| 8 | 4 | (8 - 4) | 6 | 2*totalRows - (8 - 4) | 2*totalRows - 8 + 4 |
| 9 | 5 | (9 - 4) | 5 | 2*totalRows - (9 - 4) | 2*totalRows - 9 + 4 |

| 行 | 星号最小值（默认） | 星号最小值表达式 | 星号最大值（默认） | 星号最大值表达式 |
|---|---|---|---|---|
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 |
| 6 | 2 | (row - 4) | 8 | 2*totalRows - row + 4 |
| 7 | 3 | (row - 4) | 7 | 2*totalRows - row + 4 |
| 8 | 4 | (row - 4) | 6 | 2*totalRows - row + 4 |
| 9 | 5 | (row - 4) | 5 | 2*totalRows - row + 4 |

如果我们将值 4 表示为（totalRows - 1），那么它将更具通用性。

| 行 | 星号最小值（默认） | 星号最小值表达式 | 星号最大值（默认） | 星号最大值表达式 |
|---|---|---|---|---|
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 |
| 6 | 2 | row - (totalRows - 1) | 8 | 2*totalRows - row + totalRows - 1 |
| 7 | 3 | row - (totalRows - 1) | 7 | 2*totalRows - row + totalRows - 1 |
| 8 | 4 | row - (totalRows - 1) | 6 | 2*totalRows - row + totalRows - 1 |
| 9 | 5 | row - (totalRows - 1) | 5 | 2*totalRows - row + totalRows - 1 |

| 行 | 星号最小值（默认） | 星号最小值表达式 | 星号最大值（默认） | 星号最大值表达式 |
|---|---|---|---|---|
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 |
| 6 | 2 | row - (totalRows - 1) | 8 | 2*totalRows - row + totalRows - 1 |
| 7 | 3 | row - (totalRows - 1) | 7 | 2*totalRows - row + totalRows - 1 |
| 8 | 4 | row - (totalRows - 1) | 6 | 2*totalRows - row + totalRows - 1 |
| 9 | 5 | row - (totalRows - 1) | 5 | 2*totalRows - row + totalRows - 1 |

| 行 | 星号最小值（默认） | 星号最小值表达式 | 星号最大值（默认） | 星号最大值表达式 |
|---|---|---|---|---|
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 |
| 6 | 2 | row - totalRows + 1 | 8 | 3*totalRows - row - 1 |
| 7 | 3 | row - totalRows + 1 | 7 | 3*totalRows - row - 1 |
| 8 | 4 | row - totalRows + 1 | 6 | 3*totalRows - row - 1 |
| 9 | 5 | row - totalRows + 1 | 5 | 3*totalRows - row - 1 |

通常可以观察到，在递增循环中，我们通常会得到一个一致的最小值和一个用于最大值的逻辑表达式。

在这种情况下，我们得到了两组用于最小值和最大值的逻辑表达式。最小值是列级 for 循环开始打印 * 字符的位置，并在逻辑表达式给出的最大值处结束。
