
## 列级重复动作

让我们将二维图案的两个属性行和列作为变量来考虑；

row → 变量类型为整数，用于一次存储一个整数值，表示介于 0 和 4 之间的行号。

col → 变量类型为整数，用于一次存储一个整数值，表示介于 1 和 5 之间的列号。

spaces → 变量类型为整数，用于一次存储一个整数值，表示介于 1 和 5 之间的列号处的空格字符。

totalRows → 变量类型为整数，用于存储总行数的值。

### 逻辑追踪表

(row, col) 值对描述了显示屏上“*”字符的位置

|  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|
|  |  |  |  | row=1, col=5 |  |  |  |  |
|  |  |  | row=2, col=4 | row=2, col=5 | row=2, col=6 |  |  |  |
|  |  | row=3, col=3 | row=3, col=4 | row=3, col=5 | row=3, col=6 | row=3, col=7 |  |  |
|  | row=4, col=2 | row=4, col=3 | row=4, col=4 | row=4, col=5 | row=4, col=6 | row=4, col=7 | row=4, col=8 |  |
| row=5, col=1 | row=5, col=2 | row=5, col=3 | row=5, col=4 | row=5, col=5 | row=5, col=6 | row=5, col=7 | row=5, col=8 | row=5, col=9 |

### 行级重复动作

| 变量：row | 列级重复动作：变量：spaces | 列级重复动作：变量：col | 预期输出 |
|---|---|---|---|
| 1 | 1,2,3,4 | 5 | * |
| 2 | 1,2,3 | 4,5,6 | * * * |
| 3 | 1,2 | 3,4,5,6,7 | * * * * * |
| 4 | 1 | 2,3,4,5,6,7,8 | * * * * * * * |
| 5 | 0(no space) | 1,2,3,4,5,6,7,8,9 | * * * * * * * * * |

空格（“ ”）和星号（“*”）字符被重复多次。

因此，我们可以为每个使用 for 循环。我们可以按如下方式填充表格：

| 变量：row | 列级重复动作：变量：spaces 最小值 | 列级重复动作：变量：spaces 最大值 | 列级重复动作：变量：col 最小值 | 列级重复动作：变量：col 最大值 | 预期输出 |
|---|---|---|---|---|---|
| 1 | 1 | 4 | 5 | 5 | * |
| 2 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 1 | 2 | 8 | * * * * * * * |
| 5 | 0 | 0 | 1 | 9 | * * * * * * * * * |

我们知道 totalRows = 5（总行数）。

让我们尝试使用变量 **totalRows** 来概括变量 **col** 的列 **min_val** 和 **max_val**。

| 行级重复动作 | 变量：row | 列级重复动作 | 变量：spaces | 变量：col | 预期输出 |
|---|---|---|---|---|---|
| 1 |  |  | 最小值: 1<br>最大值: 4 | 最小值: totalRows - 0<br>最大值: totalRows + 0 | * |
| 2 |  |  | 最小值: 1<br>最大值: 3 | 最小值: totalRows - 1<br>最大值: totalRows + 1 | * * * |
| 3 |  |  | 最小值: 1<br>最大值: 2 | 最小值: totalRows - 2<br>最大值: totalRows + 2 | * * * * * |
| 4 |  |  | 最小值: 1<br>最大值: 1 | 最小值: totalRows - 3<br>最大值: totalRows + 3 | * * * * * * * |
| 5 |  |  | 最小值: 0<br>最大值: 0 | 最小值: totalRows - 4<br>最大值: totalRows + 4 | * * * * * * * * * |

让我们将 **row** 值从 0 到 4 开始，而不是从 1 到 5。这是为了使变量 **col** 的列 **min_val** 和 **max_val** 的表达式部分相匹配。

| 行级重复动作 | 变量：row | 列级重复动作 | 变量：spaces | 变量：col | 预期输出 |
|---|---|---|---|---|---|
| 0 |  |  | 最小值: 1<br>最大值: 4 | 最小值: totalRows - 0<br>最大值: totalRows + 0 | * |
| 1 |  |  | 最小值: 1<br>最大值: 3 | 最小值: totalRows - 1<br>最大值: totalRows + 1 | * * * |
| 2 |  |  | 最小值: 1<br>最大值: 2 | 最小值: totalRows - 2<br>最大值: totalRows + 2 | * * * * * |
| 3 |  |  | 最小值: 1<br>最大值: 1 | 最小值: totalRows - 3<br>最大值: totalRows + 3 | * * * * * * * |
| 4 |  |  | 最小值: 0<br>最大值: 0 | 最小值: totalRows - 4<br>最大值: totalRows + 4 | * * * * * * * * * |

使用变量 **row** 来概括变量 **col** 的列 **min_val** 和 **max_val**。

| 行级重复动作 | 变量：row | 列级重复动作 | 预期输出 |
|---|---|---|---|
| 0 |  | 变量：spaces<br>最小值: 1<br>最大值: 4 | 变量：col<br>最小值: totalRows - row<br>最大值: totalRows + row<br>* |
| 1 |  | 变量：spaces<br>最小值: 1<br>最大值: 3 | 变量：col<br>最小值: totalRows - row<br>最大值: totalRows + row<br>* * * |
| 2 |  | 变量：spaces<br>最小值: 1<br>最大值: 2 | 变量：col<br>最小值: totalRows - row<br>最大值: totalRows + row<br>* * * * * |
| 3 |  | 变量：spaces<br>最小值: 1<br>最大值: 1 | 变量：col<br>最小值: totalRows - row<br>最大值: totalRows + row<br>* * * * * * * |
| 4 |  | 变量：spaces<br>最小值: 0<br>最大值: 0 | 变量：col<br>最小值: totalRows - row<br>最大值: totalRows + row<br>* * * * * * * * * |

条件 (col >= (**totalRows - row**)) 给出了最小限制，即从该点开始打印星号（“*”）字符，直到变量 col 的最大值 (**totalRows + row**) 为止的起点。

使用 **比较和逻辑运算符**，if 条件可以表示为 (**totalRows - row**) 和 (**totalRows + row**) 之间的值范围：

If ( col >= ( **totalRows - row** ) && col <= ( **totalRows + row** ) )

我们已经知道：

变量 row = 0,1,2,3,4 或

row = 0,1,2,3,4, **totalRows - 1**

变量 col = 1,2,3,4,...,9 或

col=1,2,3,4,..., ( **totalRows + row** )

## 为什么变量 col 的最大值保持动态？

我们知道打印星号("*")字符将持续到变量 col 的最大值，即 (totalRows + row)。

当一行中所有星号("*")字符的打印完成后，我们不担心空格。

将列级循环限制在星号("*")字符的最大打印次数达到的点是有意义的。

## 为什么变量 col 的最小值保持为 1？

从值 1 开始 col=1,2...是有意义的，因为在列级循环开始时，我们需要在实际打印星号("*")字符之前打印空格字符。

我们可以消除用于打印星号("*")字符的 if 条件中的逻辑 AND(&&) 条件，即 ( col <= ( totalRows + row ) )。

已经计划将此逻辑 AND(&&) 条件作为循环条件考虑，因为它已包含在列级内部 for 循环中。

因此，if 条件现在简化为以下内容：

```
If ( col >= (totalRows - row ) )
```

我们可以将其总结如下：

| 当条件对变量 col 的每个值都为 True 时打印星号字符 |  |  |  |  |  |
|---|---|---|---|---|---|
| col=1 | col=2 | col=3 | col=4 | ................... | col=(totalRows + row) |
| If ( condition( col >= (totalRows - row) ) is True )<br>打印星号字符<br><br>Else<br><br>打印空格字符 |  |  |  |  |  |

我们将列 max_val 的非重复数字模式概括为一个表达式。

现在我们可以定义列级 for 循环，该循环对每个行值都相同。

| 列级 for 循环的元素 |  |
|---|---|
| 最小值 | 1 |
| 最大值 | totalRows + row |
| 变量名 | col |
| 语句 | printf("*"); |

## 行级重复动作

以下语句已重复 5 次（总行数）。

**打印星号字符的列级 for 循环** // *内部 for 循环*

```
printf("\n" );// Move cursor to the next row
```

我们已为每一行分配从 0 到 4 的唯一值。

让我们考虑：

row → 变量类型为整数，用于一次存储一个整数值，表示介于 0 和 4 之间的行号（totalRows - 1）。totalRows 最初被赋值为 5。

| 行级 for 循环的元素 |  |
|---|---|
| 最小值 | 0 |
| 最大值 | totalRows - 1 |
| 变量名 | row |
| 语句 | 列级 for 循环用于打印星号字符<br>printf("\n" );// Move cursor to the next row |

我们已经获得了与行级重复相关的 for 循环的所有内容，相关的流程图可以显示。

![](img/67765455776ddeb6395161cd553ecd87_156_0.png)

让我们执行以下程序。

## PatternE1.c

```c
#include <stdio.h>
int main() {
    int totalRows = 5; // total number of rows to display
    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = 0; row < totalRows; row++) {
        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        for (int col = 1; col <= (totalRows + row); col++) {
            if (col >= (totalRows - row)) {
                // Action2.prints star "*" character
                printf("* ");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }
        }// inner for-loop
        printf("\n");// Move cursor to the next row
    }// outer for-loop
    return 0;
}
```

## 输出

```
*
* * *
* * * * *
* * * * * * *
* * * * * * * * *
```
