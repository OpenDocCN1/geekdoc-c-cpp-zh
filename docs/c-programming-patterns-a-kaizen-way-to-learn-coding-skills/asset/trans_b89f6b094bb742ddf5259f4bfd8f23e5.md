
让我们尝试使用行变量来概括 upper_limit 的一部分，可以表示为；

| 列级重复操作 | 预期输出 |
|---|---|
| **行** | **循环条件**( _下限_ <=col<= _上限_) |
| _下限_ | _上限_ |
| 3 | 4 | 5 |
| 1 | totalRows +1 - row | 2* totalRows - row | 2* totalRows - row -1 +1 | 5 6 7 8 9 |
| 2 | totalRows +1 - row | 2* totalRows - row - 1 | 2* totalRows - row -2+1 | 4 5 6 7 |
| 3 | totalRows +1 - row | 2* totalRows - row - 2 | 2* totalRows - row - 3+1 | 3 4 5 |
| 4 | totalRows +1 - row | 2* totalRows - row - 3 | 2* totalRows - row - 4+1 | 2 3 |
| 5 | totalRows +1 - row | 2* totalRows - row - 4 | 2* totalRows - row - 5+1 | 1 |

再次，我们可以在 upper_limit 中使用行变量来消除硬编码的数值。

| 列级重复操作 | 预期输出 |
|---|---|
| **行** | **循环条件**( _下限_ <=col<= _上限_) |
| _下限_ | _上限_ |
| 3 | 6 | 7 |
| 1 | totalRows +1 - row | 2* totalRows - row -row +1 | 2* (totalRows – row) + 1 | 5 6 7 8 9 |
| 2 | totalRows +1 - row | 2* totalRows - row -row +1 | 2* (totalRows – row) + 1 | 4 5 6 7 |
| 3 | totalRows +1 - row | 2* totalRows - row -row +1 | 2* (totalRows – row) + 1 | 3 4 5 |
| 4 | totalRows +1 - row | 2* totalRows - row -row +1 | 2* (totalRows – row) + 1 | 2 3 |
| 5 | totalRows +1 - row | 2* totalRows - row -row +1 | 2* (totalRows – row) + 1 | 1 |

lower_limit 和 upper_limit 表达式都包含 +1。此外，如果我们将循环设为 [1 <=row<= totalRows] 或 [0 <=row< totalRows]，在任何一种情况下都是相同的。通过从 row 中减去 1 来使 lower_limit 和 upper_limit 表达式更简单。

| 列级重复操作 | 预期输出 |
|---|---|
| **行** | **循环 -条件**( _下限_ <=col< _上限_) |
| _下限_ | _上限_ |
| **表达式** | **表达式** |
| 1 -1 | totalRows +1 – row - 1 | 2* (totalRows – row) + 1 - 1 | 5 6 7 8 9 |
| 2 -1 | totalRows +1 – row - 1 | 2* (totalRows – row) + 1 - 1 | 4 5 6 7 |
| 3 -1 | totalRows +1 – row - 1 | 2* (totalRows – row) + 1 - 1 | 3 4 5 |
| 4 -1 | totalRows +1 – row - 1 | 2* (totalRows – row) + 1 - 1 | 2 3 |
| 5 -1 | totalRows +1 – row - 1 | 2* (totalRows – row) + 1 - 1 | 1 |

| 列级重复操作 | 预期输出 |
|---|---|
| **行** | **循环 -条件**( _下限_ <=col< _上限_) |
| _下限_ | _上限_ |
| **表达式** | **表达式** |
| 0 | totalRows – row | 2* (totalRows – row) | 5 6 7 8 9 |
| 1 | totalRows – row | 2* (totalRows – row) | 4 5 6 7 |
| 2 | totalRows – row | 2* (totalRows – row) | 3 4 5 |
| 3 | totalRows – row | 2* (totalRows – row) | 2 3 |
| 4 | totalRows – row | 2* (totalRows – row) | 1 |

因此我们的外层 for 循环条件变为；

| 循环条件 | 下限 <=row< 上限 |
| 数学表达式 | 0 <= row < totalRows |
| 语法 | for( row = 0; row < totalRows; row++) |

因此我们的内层 for 循环条件变为；

| 循环条件 | 下限 <=col< 上限 |
| 数学表达式 | (totalRows - row) <=col< 2* (totalRows - row) |
| 语法 | for(col=(totalRows - row);col<2*(totalRows - row);col++ ) |

流程图可以如下给出。

![](img/67765455776ddeb6395161cd553ecd87_328_0.png)

## NumberPatternCCC2.c

```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display

    // Row level Repetitive Action :
    for ( int row = 0; row < totalRows; row++ ) {

        // Column level Repetitive Action :
        // 1)Move cursor in the same row. 2)print character
        int lower_limit = ( totalRows - row );
        int upper_limit = 2 * ( totalRows - row );
        for ( int col = lower_limit ; col < upper_limit ; col++ ) {
            printf( "%d ", col );
        }// inner loop

        printf( "\n" );// Move cursor to the next row

    }// outer loop

    return 0;
}
```

## 输出

```text
5 6 7 8 9
4 5 6 7
3 4 5
2 3
1
```

```
9 8 7 6 5
  7 6 5 4
    5 4 3
      3 2
        1
```

## NumberPatternDDD

## 表格表示

| | 列=1 | 列=2 | 列=3 | 列=4 | 列=5 |
| --- | --- | --- | --- | --- | --- |
| 行=1 | 9 | 8 | 7 | 6 | 5 |
| 行=2 |   | 7 | 6 | 5 | 4 |
| 行=3 |   |   | 5 | 4 | 3 |
| 行=4 |   |   |   | 3 | 2 |
| 行=5 |   |   |   |   | 1 |

## (行, 列) 值对表示。

| | 列=1 | 列=2 | 列=3 | 列=4 | 列=5 |
| --- | --- | --- | --- | --- | --- |
| 行=1 | 1,1 | 1,2 | 1,3 | 1,4 | 1,5 |
| 行=2 |   | 2,2 | 2,3 | 2,4 | 2,5 |
| 行=3 |   |   | 3,3 | 3,4 | 3,5 |
| 行=4 |   |   |   | 4,4 | 4,5 |
| 行=5 |   |   |   |   | 5,5 |

## 输出分析

在这种情况下，我们需要在特定行中的特定列打印两种不同类型的字符：

- 1) Space character
- 2) Numeric character

| 行 | 5 | | | | |
| 列 | 1 | 2 | 3 | 4 | 5 |
| 输出 | 9 | 8 | 7 | 6 | 5 |

对于 行 = 1，0<=spaces<=0，9>=num>5

| 行 | 4 | | | | |
| 列 | 1 | 2 | 3 | 4 | 5 |
| 输出 | space | 7 | 6 | 5 | 4 |

对于 行 = 2，1<=spaces<=1，9>=num>5

| 行 | 3 | | | | |
| 列 | 1 | 2 | 3 | 4 | 5 |
| 输出 | space | space | 5 | 4 | 3 |

对于 行 = 3，1<=spaces<=2，5>=num>3

| 行 | 2 | | | | |
| 列 | 1 | 2 | 3 | 4 | 5 |
| 输出 | space | space | space | 3 | 2 |

对于 行 = 4，1<=spaces<=3，3>=num>2

| 行 | 1 | | | | |
| 列 | 1 | 2 | 3 | 4 | 5 |
| 输出 | space | space | space | space | 1 |

对于 行 = 5，1<=spaces<=4，1>=num>1

## 观察

- 1) 在行级垂直方向上存在重复，即 行 = 1 到 5。
- 2) 在列级水平方向上存在重复，即 列 = 1 到 5。这被分为两个部分。一个用于重复打印空格，剩余列用于打印数字字符。

| For 循环 | 下限 | 上限 |
|---|---|---|
| 外层循环(递减) | row=1 | Row>=5 |
| 内层循环 - 空格 | col=1 | col<= ?(Unknown) |
| 内层循环 – 数字(递减) | num= row | num =?(Unknown) |

## 列级重复操作

| 行级重复操作 | 预期输出 |
|---|---|
| 行 | 列级重复操作 | |
|  | 下限 <=col<= 上限 | 上限 >=num >= 下限 | |
|  | 下限 | 上限 | 上限 | 下限 | |
| 5 | 1 | 0 | 9 | 5 | 9 8 7 6 5 |
| 4 | 1 | 1 | 7 | 4 | 7 6 5 4 |
| 3 | 1 | 2 | 5 | 3 | 5 4 3 |
| 2 | 1 | 3 | 3 | 2 | 3 2 |
| 1 | 1 | 4 | 1 | 1 | 1 |

空格和 num 变量的 lower_limit 具有相同的数值表达式，对所有行都一致。

它对所有行都是一致的。同样，我们需要为 upper_limit 找到这样一个一致的表达式，以便适用于任意行数。

其余变量为 row 和 totalRows=5。让我们尝试使用这些变量来概括。

| 列级重复操作 | |
| 行 | 下限 <=spaces<= 上限 | 上限 >=num >= 下限 |
|  | 下限 | 上限 | 上限 | 下限 |
|  |  | 默认 | 1 | 默认 | 1 |
| 5 | 1 | 0 | totalRows - row | 9 | 5 | row |
| 4 | 1 | 1 | totalRows - row | 7 | 4 | row |
| 3 | 1 | 2 | totalRows - row | 5 | 3 | row |
| 2 | 1 | 3 | totalRows - row | 3 | 2 | row |
| 1 | 1 | 4 | totalRows - row | 1 | 1 | row |

行变量相关内层 for 循环的 upper_limit 已被概括，在所有行上具有一致的表达式。

num 变量相关内层 for 循环的 upper_limit 未被概括，因为在所有行上没有表达式。根据之前的情况，我们知道它可以遵循广义表达式 2*row - 1。

| 列级重复操作 | |
| 行 | 下限 <=spaces<= 上限 | 上限 >=num >= 下限 |
|  | 下限 | 上限 | 上限 | 下限 |
|  |  | 默认 | 1 | 2*row - 1 | 1 |
| 5 | 1 | 0 | totalRows - row | 2*row - 1 | row |
| 4 | 1 | 1 | totalRows - row | 2*row - 1 | row |
| 3 | 1 | 2 | totalRows - row | 2*row - 1 | row |
| 2 | 1 | 3 | totalRows - row | 2*row - 1 | row |
| 1 | 1 | 4 | totalRows - row | 2*row - 1 | row |

因此 col 和 num 变量的 upper_limit 已被概括。

lower_limit 和 upper_limit 对所有行都是一致的。它现在已针对任意行数进行了概括。

因此它有两个重复过程，一个用于打印空格，第二个用于打印数值。

这意味着需要 2 个内层 for 循环和 1 个外层循环来迭代行。
