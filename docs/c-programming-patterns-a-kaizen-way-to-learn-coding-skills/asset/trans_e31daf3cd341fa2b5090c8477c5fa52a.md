
让我们编写完整的编程逻辑并执行程序。

## PatternC1.c
```
#include <stdio.h>
int main() {
    int totalRows = 5; //number of rows to display

    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for( int row = 1 ; row <= totalRows ; row++ ) {

        // Column level Repetitive Action :
        for(int sp = 1 ; sp <= ( totalRows - row ) ; sp++) {
            // Action1.Move cursor in the same row
            // Action2.print space " " character
            printf(" ");
        }
        for(int col = 1 ; col <= row ; col++) {
            // Action1.Move cursor in the same row
            // Action2.print star "* " character
            printf("* ");
        }
        printf("\n");// Move cursor to the next row
    }
    return 0;
}
```

## 输出
    *
   * *
  * * *
 * * * *
* * * * *

## 替代方案2
可用的变量是 row 和 totalRows=5。

变量 col 取值为 1 到 5，即 col=1, 2, 3, 4, 5。

总体观察是，在每一行中，要么以连续的方式打印空格字符，要么打印星号 (*) 字符。

模式中的列分为两部分，要么打印空格 " " 字符，要么打印星号 ("*") 字符。

| 行级重复操作 | 预期输出 |
|---|---|
| 变量：row | 列级重复操作 | |
|  | 变量：spaces | 变量：col | 字符计数 | 总字符数 | |
| 1 | 1,2,3,4 | 5 | 4 个空格 + 1 个星号 | 5 | * |
| 2 | 1,2,3 | 4, 5 | 3 个空格 + 2 个星号 | 5 | * * |
| 3 | 1,2 | 3, 4, 5 | 2 个空格 + 3 个星号 | 5 | * * * |
| 4 | 1 | 2, 3, 4, 5 | 1 个空格 + 4 个星号 | 5 | * * * * |
| 5 | 0(无空格) | 1, 2, 3, 4, 5 | 0 个空格 + 5 个星号 | 5 | * * * * * |

打印空格首先在打印星号 ("*") 字符之前进行。当考虑到打印空格字符的条件时，其余的就是星号 ("*") 字符。如果仔细观察，可以发现它将变量 col 的值分为两半。一部分用于打印空格字符，另一部分用于打印星号字符。

| 行级重复操作 | 预期输出 |
|---|---|
| 变量：row | 列级重复操作 | |
|  | 变量：col | |
|  | 打印空格字符 | 打印星号字符 | |
|  | 最小值 | 最大值 | 最小值 | 最大值 | |
| 1 | 1 | 4 | 5 | 5 | * |
| 2 | 1 | 3 | 4 | 5 | * * |
| 3 | 1 | 2 | 3 | 5 | * * * |
| 4 | 1 | 1 | 2 | 5 | * * * * |
| 5 | 0 | 0 | 1 | 5 | * * * * * |

从之前的解决方案中，我们已经有了打印空格的通用条件，并使用该通用条件我们可以将所有内容放在下面的表中。

| 行级重复操作 |
| 变量：row | 列级重复操作 |
| | 变量：col |
| | 打印空格字符 | 打印星号字符 |
| | 最小值 | 最大值 | | 最小值 | 最大值 |
| | | 默认 | 1 | | |
| 1 | 1 | 4 | totalRows -row | 5 | 5 |
| 2 | 1 | 3 | totalRows -row | 4 | 5 |
| 3 | 1 | 2 | totalRows -row | 3 | 5 |
| 4 | 1 | 1 | totalRows -row | 2 | 5 |
| 5 | 0 | 0 | totalRows -row | 1 | 5 |

列级 for 循环在 col 变量的值 1 到 5 之间运行。

条件 (totalRows - row) 给出了从 1 开始的最大限制，在此限制内它将打印空格字符。

因此，我们可以轻松地为我们的情况使用 if-else 语句来过滤和打印空格和星号字符。

![](img/67765455776ddeb6395161cd553ecd87_136_0.png)

| 当条件为 **True** 时为每个变量 **col** 的值打印一个空格 |||||
|---|---|---|---|---|
| col=1 | col=2 | col=3 | col=4 | col=5 |
| 如果 (条件为 True)<br>    打印空格字符<br>否则<br>    打印星号字符 |||| |

使用 if-else 语句更新后的程序如下：

## PatternC2.c
```c
#include <stdio.h>
int main() {
    int totalRows = 5; //number of rows to display
    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = 1; row <= totalRows; row++) {

        // Column level Repetitive Action :
        // Action1.Move cursor in the same row.
        for (int col = 1; col <= totalRows; col++) {
            if (col <= (totalRows - row)) {
                // Action2.prints space " " character
                printf(" ");
            } else {
                // Action3.prints star "*" character
                printf("* ");
            }
        }
        printf("\n");// Move cursor to the next row
    }

    return 0;
}
```

## 输出
```
        *
      * *
    * * *
  * * * *
* * * * *
```

现在，测试不同数量的行，设为 10。

## PatternC2.c
```c
#include <stdio.h>
int main() {

        int totalRows = 10; //number of rows to display
        // Row level Repetitive Action :
        // Action1.Executes Column level Repetitive Action
        // Action2.Move cursor to next row.
        for (int row = 1; row <= totalRows; row++) {

                // Column level Repetitive Action :
                // Action1.Move cursor in the same row
                for (int col = 1; col <= totalRows; col++) {
                        if (col <= (totalRows - row)) {
                                // Action2.prints space “ ” character
                                printf(" ");
                        } else {
                                // Action3.prints star “* ” character
                                printf("* ");
                        }
                }
                printf("\n");// Move cursor to the next row
        }

        return 0;
}
```

## 输出
```text
                  *
                * *
              * * *
            * * * *
          * * * * *
        * * * * * *
      * * * * * * *
    * * * * * * * *
  * * * * * * * * *
* * * * * * * * * *
```

## 替代方案3
从之前的解决方案中，我们已检查 **if-condition** 为 **true** 以打印空格，并在 **if-statement** 的 else 部分打印了星号（“*”）字符。这被如下捕获：

<table><tr><td colspan='5'>当条件为 True 时为变量 col 的每个值打印一个空格</td></tr><tr><td>col=1</td><td>col=2</td><td>col=3</td><td>col=4</td><td>col=5</td></tr><tr><td colspan='5'><pre>如果 (条件为 True)
    打印空格字符
否则
    打印星号字符</pre></td></tr></table>

在此解决方案中，我们将反转情况。当 **if-condition** 变为 **true** 时，我们将打印星号（“*”）字符，并在 **if-statement** 的 else 部分打印空格。

让我们从之前的解决方案中得到的观察表开始。

<table><tr><td colspan='6'>行级重复操作</td></tr><tr><td rowspan='4'>变量：row</td><td colspan='5'>列级重复操作</td></tr><tr><td colspan='5'>变量：col</td></tr><tr><td colspan='2'>打印空格字符</td><td colspan='3'>打印星号字符</td></tr><tr><td>最小值</td><td>最大值</td><td>默认</td><td>最小值</td><td>最大值</td></tr><tr><td>1</td><td>1</td><td>4</td><td>5</td><td>5</td><td>5</td></tr><tr><td>2</td><td>1</td><td>3</td><td>4</td><td>5</td><td>5</td></tr><tr><td>3</td><td>1</td><td>2</td><td>3</td><td>5</td><td>5</td></tr><tr><td>4</td><td>1</td><td>1</td><td>2</td><td>5</td><td>5</td></tr><tr><td>5</td><td>0</td><td>0</td><td>1</td><td>5</td><td>5</td></tr></table>

我们知道 totalRows = 5。

用于打印星号字符的列 **min_val** 可以表示为；

| 行级重复操作（变量：row） | 列级重复操作（变量：col） | 打印空格字符 最小值 | 打印空格字符 最大值（默认） | 打印星号字符 最小值 | 打印星号字符 最大值 |
|---|---|---|---|---|---|
| 1 | | 1 | 4 | 5 - 0 | totalRows |
| 2 | | 1 | 3 | 5 - 1 | totalRows |
| 3 | | 1 | 2 | 5 - 2 | totalRows |
| 4 | | 1 | 1 | 5 - 3 | totalRows |
| 5 | | 0 | 0 | 5 - 4 | totalRows |

如果我们尝试使用变量 totalRows 来概括列 **min_val** 的数字模式。

那么它将是 totalRows – 0 , totalRows – 1,...等等。该表达式的一部分几乎遵循变量 row = 1,2,...5 的数字模式。前者具有从零(0)开始的数字模式，而 row 变量的数字模式从一(1)开始。让它，开始 row 变量的数字模式也从零(0)开始。

让我们利用变量 <u>totalRows</u> 和 <u>row</u> 来推导出打印星号字符的广义表达式。

| 行级重复操作（变量：row） | 列级重复操作（变量：col） | 打印空格字符 最小值 | 打印空格字符 最大值（默认） | 打印星号字符 最小值 | 打印星号字符 最大值 |
|---|---|---|---|---|---|
| 0 | | 1 | 4 | totalRows - 0 | totalRows |
| 1 | | 1 | 3 | totalRows - 1 | totalRows |
| 2 | | 1 | 2 | totalRows - 2 | totalRows |
| 3 | | 1 | 1 | totalRows - 3 | totalRows |
| 4 | | 0 | 0 | totalRows - 4 | totalRows |

我们可以使用变量 **row** 来概括打印星号字符的列 **min_val**。
