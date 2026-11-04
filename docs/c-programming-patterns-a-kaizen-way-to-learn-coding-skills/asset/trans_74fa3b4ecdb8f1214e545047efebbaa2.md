
```
        1
      2   2   2
    3   3   3   3   3
  4   4   4   4   4   4   4
5   5   5   5   5   5   5   5   5
```

NumberPattern1E

## 表格表示

|  | 列=1 | 列=2 | 列=3 | 列=4 | 列=5 | 列=6 | 列=7 | 列=8 | 列=9 |
|---|---|---|---|---|---|---|---|---|---|
| 行=1 | 空格 | 空格 | 空格 | 空格 | 1 | 空格 | 空格 | 空格 | 空格 |
| 行=2 | 空格 | 空格 | 空格 | 2 | 2 | 2 | 空格 | 空格 | 空格 |
| 行=3 | 空格 | 空格 | 3 | 3 | 3 | 3 | 3 | 空格 | 空格 |
| 行=4 | 空格 | 4 | 4 | 4 | 4 | 4 | 4 | 4 | 空格 |
| 行=5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |

## （行，列）值对表示

|  | 列=1 | 列=2 | 列=3 | 列=4 | 列=5 | 列=6 | 列=7 | 列=8 | 列=9 |
|---|---|---|---|---|---|---|---|---|---|
| 行=1 |  |  |  |  | 1, 5 |  |  |  |  |
| 行=2 |  |  |  | 2, 4 | 2, 5 | 2,6 |  |  |  |
| 行=3 |  |  | 3, 3 | 3, 4 | 3, 5 | 3,6 | 3,7 |  |  |
| 行=4 |  | 4, 2 | 4, 3 | 4, 4 | 4, 5 | 4,6 | 4,7 | 4,8 |  |
| 行=5 | 5, 1 | 5, 2 | 5, 3 | 5, 4 | 5,5 | 5,6 | 5,7 | 5,8 | 5,9 |

## 输出分析

| 行 | 1 | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 列 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 输出 | | | | | 1 | | | | |

对于行 = 1，5 <= 列 <= 5，（打印行的值）

| 行 | 2 | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 列 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 输出 | | | | 2 | 2 | 2 | | | |

对于行 = 2，4 <= 列 <= 6，（打印行的值）

| 行 | 3 | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 列 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 输出 | | | 3 | 3 | 3 | 3 | 3 | | |

对于行 = 3，3 <= 列 <= 7，（打印行的值）

| 行 | 4 | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 列 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 输出 | | 4 | 4 | 4 | 4 | 4 | 4 | 4 | |

对于行 = 4，2 <= 列 <= 8，（打印行的值）

| 行 | 5 | | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 列 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| 输出 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |

对于行 = 5，1 <= 列 <= 9，（打印行的值）

## 列级重复操作

打印图案底部最多总共需要 9 列。

| 行级重复操作 | | | 预期输出 |
| :--- | :--- | :--- | :--- |
| 行 | 列级重复操作 | | |
| | （lower_limit <= col <= upper_limit） | | |
| | lower_limit | upper_limit | |
| 1 | 5 | 5 | 1 |
| 2 | 4 | 6 | 2 2 2 |
| 3 | 3 | 7 | 3 3 3 3 3 |
| 4 | 2 | 8 | 4 4 4 4 4 4 4 |
| 5 | 1 | 9 | 5 5 5 5 5 5 5 5 5 |

lower_limit 和 upper_limit 并非对所有行都一致。我们需要为 upper_limit 和 lower_limit 都给出适用于 n 行的统一表达式。

其余变量是 row、totalRows=5。

让我们尝试使用这些变量进行泛化。

## 列级重复操作

| 行 | lower_limit 值 | lower_limit 表达式 | lower_limit 公式 | upper_limit 值 | upper_limit 表达式 | upper_limit 公式 |
|---|---|---|---|---|---|---|
| 1 | 5 | totalRows | totalRows +1 - 1 | 5 | totalRows | totalRows +1 - 1 |
| 2 | 4 | totalRows -1 | totalRows +1 - 2 | 6 | totalRows + 1 | totalRows + 2 - 1 |
| 3 | 3 | totalRows -2 | totalRows +1 - 3 | 7 | totalRows + 2 | totalRows + 3 - 1 |
| 4 | 2 | totalRows -3 | totalRows +1 - 4 | 8 | totalRows + 3 | totalRows + 4 - 1 |
| 5 | 1 | totalRows -4 | totalRows +1 - 5 | 9 | totalRows + 4 | totalRows + 5 - 1 |

## 列级重复操作

| 行 | lower_limit 值 | lower_limit 公式 | upper_limit 值 | upper_limit 公式 |
|---|---|---|---|---|
| 1 | 5 | totalRows +1 - row | 5 | totalRows + row - 1 |
| 2 | 4 | totalRows +1 - row | 6 | totalRows + row - 1 |
| 3 | 3 | totalRows +1 - row | 7 | totalRows + row - 1 |
| 4 | 2 | totalRows +1 - row | 8 | totalRows + row - 1 |
| 5 | 1 | totalRows +1 - row | 9 | totalRows + row - 1 |

lower_limit 和 upper_limit 对所有行都一致。现在它已泛化到可用于任意行数来打印数值。因此我们的 if 条件变为

| if 条件 | lower_limit <=col<= upper_limit |
|---|---|
| 数学表达式 | (totalRows +1 - row) <= col <= (totalRows + row - 1) |
| 语法 | if( col >= ( ( totalRows - row ) + 1 ) && col <= ( ( totalRows + row ) - 1 ) ) |

当 if 条件满足时，它会在特定行的该位置打印行值，否则打印空格字符。由于我们知道打印图案底部最多需要 9 列。for 循环条件如下：

| 循环条件 | lower_limit <=col<= upper_limit |
|---|---|
| 数学表达式 | 1<= col <= 9 |
| 语法 | for( col = 1 ; col <= 9 ; col++ ) |

内层 for 循环的 col 变量的*upper_limit*（即**值 9**）需要泛化。

逻辑条件中的硬编码值会使程序在不同输入值下失败。必须通过程序中考虑的变量以某种方式对其进行泛化。

| 循环条件 | lower_limit <=col<= upper_limit |
|---|---|
| 数学表达式 | 1<= col <= totalRows + 4 |
|  | 1<= col <= totalRows + ( totalRows - 1 ) |
|  | 1<= col <= ( 2*totalRows - 1 ) |
| 语法 | for( col = 1 ; col <= ( 2* totalRows - 1 ) ; col++ ) |

现在我们可以使用变量 totalRows 进行泛化。

让我们尝试验证每行要显示的总列数的上限

对于 totalRows = 5，col <= 9（2*5 - 1）

对于 totalRows = 4，col <= 7（2*4 - 1）

对于 totalRows = 3，col <= 5（2*3 - 1）

对于 totalRows = 2，col <= 3（2*2 - 1）

对于 totalRows = 1，col <= 1（2*1 - 1）

因此，根据给定行数对总列数的这种泛化是成立的。

所有这些观察结果都可以轻松地记录在如下流程图中。

![](img/67765455776ddeb6395161cd553ecd87_251_0.png)

让我们根据流程图中记录的观察结果编写程序。

## NumberPattern1E.C

```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display

    for ( int row = 1; row <= totalRows; row++) {

        // repetition happens ( 2 * totalRows - 1 ) times for columns

        for ( int col = 1; col <= ( 2 * totalRows - 1 ); col++ ) {

            if ( col >= ( ( totalRows - row ) + 1 ) &&
                col <= ( ( totalRows + row ) - 1 ) ) {

                // row value to be printed
                printf( "%d ", row );

            } else {

                // spaces to be printed
                printf( "  " );

            }

        }// end  inner for - loop

        printf( "\n" );// moves control to the next line

    } // end  outer for - loop

    return 0;

}
```

## 输出

```text
        1
      2 2 2
    3 3 3 3 3
  4 4 4 4 4 4 4
5 5 5 5 5 5 5 5 5
```

现在，测试不同的行数，设为 8。它应该能正确工作。

## NumberPattern1E.c

```
#include <stdio.h>
int main() {
    int totalRows = 8; //number of rows to display
    for ( int row = 1; row <= totalRows; row++ ) {
        // repetition happens ( 2* totalRows - 1) times for columns
        for ( int col = 1; col <= ( 2 * totalRows - 1 ); col++ ) {
            if ( col >= ( ( totalRows - row ) + 1 ) &&
                col <= ( ( totalRows + row ) - 1 ) ) {
                // row value to be printed
                printf( "%d ", row );
            } else {
                // spaces to be printed
                printf( "  " );
            }
        }// end inner for-loop
        printf( "\n" );// moves control to the next line
    } // end outer for-loop
    return 0;
}
```

## 输出

1
  2 2 2
  3 3 3 3 3
  4 4 4 4 4 4 4
  5 5 5 5 5 5 5 5 5
  6 6 6 6 6 6 6 6 6 6 6 6
  7 7 7 7 7 7 7 7 7 7 7 7 7 7 7
  8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8 8
