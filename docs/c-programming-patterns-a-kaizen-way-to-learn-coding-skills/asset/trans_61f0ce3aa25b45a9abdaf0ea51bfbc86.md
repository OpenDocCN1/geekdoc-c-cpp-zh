
*练习。* 完成此逻辑模式的生成步骤，并在计算机屏幕示意图上显示输出，对每一行 1 到 5。

| 生成模式的步骤（row = 1 到 5） | 计算机屏幕 |
|---|---|
| 对于 row = 1 | 计算机屏幕示意图：列 1–9 和行 1–5；箭头指向第 2 行。 |
| 对于 row = 2 | 计算机屏幕示意图：列 1–9 和行 1–5；箭头指向第 3 行。 |
| 对于 row = 3 | 计算机屏幕示意图：列 1–9 和行 1–5；箭头指向第 4 行。 |
| 对于 row = 4 | 计算机屏幕示意图：列 1–9 和行 1–5；箭头指向第 5 行。 |
| 对于 row = 5 | 计算机屏幕示意图：列 1–9 和行 1–6；箭头指向第 6 行。 |

## **让我们将步骤转换为 C 程序。**

| C 内置方法的使用 | |
|---|---|
| 移至下一行 | `printf("\n");` |
| 移至下一个 (row, col) 位置并在同一行打印空格 " " 字符 | `printf(" ");` |
| 移至下一个 (row, col) 位置并在同一行打印星号 "*" 字符 | `printf("*");` |

提到的这些方法在程序中必然会被重复多次使用，以便反复输出这些字符。因此我们将在 *for 循环* 中使用它们来处理程序中的此类重复任务。

## 列级重复操作

让我们将二维模式的两个属性 rows 和 columns 视为变量；

row → 变量类型为整数，用于一次存储一个整数值，表示介于 0 和 4 之间的行号

col → 变量类型为整数，用于一次存储一个整数值，表示介于 1 和 5 之间的列号

spaces → 变量类型为整数，用于一次存储一个整数值，表示介于 1 和 5 之间的列号处的空格字符

totalRows → 变量类型为整数，用于存储总行数的值。

## 逻辑追踪表

| (row, col) 值对表示显示屏上“*”字符的位置 |
| row=1, col1 | row=1, col2 | row=1, col3 | row=1, col4 | row=1, col5 | row=1, col6 | row=1, col7 | row=1, col8 | row=1, col9 |
|  | row=2, col2 | row=2, col3 | row=2, col4 | row=2, col5 | row=2, col6 | row=2, col7 | row=2, col8 |  |
|  |  | row=3, col3 | row=3, col4 | row=3, col5 | row=3, col6 | row=3, col7 |  |  |
|  |  |  | row=4, col4 | row=4, col5 | row=4, col6 |  |  |  |
|  |  |  |  | row=5, col5 |  |  |  |  |

空格（“ ”）和星号（“*”）字符被重复多次。

因此，我们可以对空格（“ ”）和星号（“*”）字符使用 for 循环。

| 行级重复操作 | 预期输出 |
| 变量：row | 列级重复操作 | |
|  | 变量：spaces | 变量：col | |
| 1 | 0(no space) | 1,2,3,4,5,6,7,8,9 | * * * * * * * * * |
| 2 | 1 | 2,3,4,5,6,7,8 | * * * * * * * |
| 3 | 1,2 | 3,4,5,6,7 | * * * * * |
| 4 | 1,2,3 | 4,5,6 | * * * |
| 5 | 1,2,3,4 | 5 | * |

我们也可以按如下方式填充上表，以便探索 for 循环的各个组成部分。

| 行级重复操作 | 预期输出 |
| 变量：row | 列级重复操作 | |
|  | 变量：spaces | 变量：col | |
|  | min_val | max_val | min_val | max_val | |
| 1 | 0 | 0 | 1 | 9 | * * * * * * * * * |
| 2 | 1 | 1 | 2 | 8 | * * * * * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 3 | 4 | 6 | * * * |
| 5 | 1 | 4 | 5 | 5 | * |

我们知道 totalRows=5（总行数）。

让我们尝试使用变量 totalRows 来概括变量 col 的列的 min_val 和 max_val。

| 行级重复操作 | 预期输出 |
| 变量：row | 列级重复操作 | |
| 变量：spaces | 变量：col | |
| min_val | max_val | min_val | max_val | |
| 1 | 0 | 0 | totalRows -4 | totalRows +4 | * * * * * * * * * |
| 2 | 1 | 1 | totalRows -3 | totalRows +3 | * * * * * * * |
| 3 | 1 | 2 | totalRows -2 | totalRows +2 | * * * * * |
| 4 | 1 | 3 | totalRows -1 | totalRows +1 | * * * |
| 5 | 1 | 4 | totalRows -0 | totalRows +0 | * |

让我们在行级重复中使用范围为 4 到 的递减 for 循环。

这是为了匹配变量 col 列 min_val 和 max_val 表达式的一部分。

使用变量 row 来概括变量 col 的列 min_val 和 max_val。

| 行级重复操作 | 预期输出 |
| 变量：row | 列级重复操作 | |
| 变量：spaces | 变量：col | |
| min_val | max_val | min_val | max_val | |
| 4 | 0 | 0 | totalRows - row | totalRows + row | * * * * * * * * |
| 3 | 1 | 1 | totalRows - row | totalRows + row | * * * * * * |
| 2 | 1 | 2 | totalRows - row | totalRows + row | * * * * * |
| 1 | 1 | 3 | totalRows - row | totalRows + row | * * * |
| 0 | 1 | 4 | totalRows - row | totalRows + row | * |

条件 (col >= (totalRows – row)) 给出了最小限制，从该点开始它将开始打印星号(*) 字符，直到变量 col 的最大值 (totalRows + row)。

if 条件可以为值范围

(totalRows - row ) 和 (totalRows + row) 使用比较和逻辑运算符给出为：

```
If ( col >= ( totalRows - row ) && col <= ( totalRows + row ) )
```

我们已经知道；

变量 col = 1,2,3,4,...,9 或 1,2,3,4,..., ( totalRows + row )

变量 row = 4,3,2,1,0 或 (totalRows – 1),3,2,1,0

我们可以消除 if 条件中打印星号(*) 字符的逻辑 AND(&&) 条件( col <= ( totalRows + row ) )。该逻辑 AND(&&) 条件已作为列级内层 for 循环的循环条件中的 upper_limit 考虑。因此 if 条件现在将简化为以下内容。

If ( col >= (totalRows - row ) ) 它将允许在 if 条件表达式结果为真时打印星号(*) 字符，否则将打印空格字符。我们将列 max_val 的非重复数字模式概括为表达式。我们现在可以定义列级 for 循环。

| 列级 for 循环的元素 |
|---|---|
| min_val | 1 |
| max_val | totalRows + row |
| variable_name | col |
| statement(s) | printf("*"); |

## 行级重复操作

以下语句被重复了 5 次（总行数）。

打印星号字符的列级 for 循环 // 内层 for 循环

```
printf("\n "); // Move cursor to the next row
```

row → 变量类型为整数，用于一次存储一个整数值，表示

行号介于 4 或 (totalRows - 1) 和 0 之间。totalRows 已初始分配值为 5。

我们已经获得了行级重复 for 循环相关的所有内容。

| 行级递减 for 循环的元素 |
|---|---|
| min_val | 0 |
| max_val | totalRows - 1 |
| variable_name | row |
| statement(s) | 打印星号字符的列级 for 循环
printf("\n"); // Move to the next row |

流程图可以如下给出：

![](img/67765455776ddeb6395161cd553ecd87_166_0.png)

让我们执行以下程序。

## PatternF1.c

```
#include <stdio.h>
int main() {
    int totalRows = 5; // total number of rows to display
    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = (totalRows - 1); row >= 0; row--) {
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

* * * * * * * *
  * * * * * *
    * * * * *
      * * *
        *

## 替代方案2

通过在行级重复中使用递增 for 循环，我们可以给出替代方案。

## 问题 F1. 找到不同的逻辑并编写程序打印以下 5 行的模式。

测试该逻辑是否适用于 12 行。一些细节以表格形式列出作为开始。

| 行级重复操作 | 预期输出 |
| 变量：row | 列级重复操作 | |
| | 变量：spaces | 变量：col | |
| | min_val | max_val | min_val | max_val | |
| 1 | 0 | 0 | 1 | 9 | * * * * * * * * * |
| 2 | 1 | 1 | 2 | 8 | * * * * * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 3 | 4 | 6 | * * * |
| 5 | 1 | 4 | 5 | 5 | * |

当 if 条件为真时程序应打印星号('*') 字符，而在 if-else 语句的 else 部分程序应打印空格字符。

## 问题 F2. 在前一个问题（问题 F1）的基础上，编写程序实现以下情况。

当 if 条件为真时，程序应打印空格(' ') 字符，而在 if-else 语句的 else 部分程序应打印星号('*') 字符。
