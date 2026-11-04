
所以它有两个重复过程：一个用于打印空格，另一个用于打印数值。

这意味着我们需要 2 个内部 for 循环和 1 个外部循环来迭代行。行值与用于空格和数字的内部 for 循环的上界之间的关系。

| 行级重复操作 | 列级重复操作：lower_limit <= col_sp <= upper_limit（下限） | 列级重复操作：lower_limit <= col_sp <= upper_limit（上限） | 列级重复操作：lower_limit <= col_num <= upper_limit（下限） | 列级重复操作：lower_limit <= col_num <= upper_limit（上限） | 预期输出 |
|---|---|---|---|---|---|
| 行 | 下限 | 上限 | 下限 | 上限 | |
| 5 | 1 | 0 | 1 | 5 | 5 5 5 5 5 |
| 4 | 1 | 1 | 1 | 4 | 4 4 4 4 |
| 3 | 1 | 2 | 1 | 3 | 3 3 3 |
| 2 | 1 | 3 | 1 | 2 | 2 2 |
| 1 | 1 | 4 | 1 | 1 | 1 |

spaces & num 变量的 lower_limit 在所有行中具有相同的数值表达式。

它在所有行中都是一致的。同样，我们需要为 upper_limit 找到一个一致的表达式，使其适用于任意数量的行。

其他剩余变量是 row 和 totalRows=5。让我们尝试使用这些变量进行泛化。

| 行级重复操作 | 列级重复操作：lower_limit <= col_sp <= upper_limit（下限） | 列级重复操作：lower_limit <= col_sp <= upper_limit（上限） | 列级重复操作：lower_limit <= col_sp <= upper_limit（默认值） | 列级重复操作：lower_limit <= col_num <= upper_limit（下限） | 列级重复操作：lower_limit <= col_num <= upper_limit（上限） | 预期输出 |
|---|---|---|---|---|---|---|
| 行 | 下限 | 上限 | 默认值 | 下限 | 上限 | |
| 5 | 1 | 0 | totalRows - row | 1 | 5 | 5 5 5 5 5 |
| 4 | 1 | 1 | totalRows - row | 1 | 4 | 4 4 4 4 |
| 3 | 1 | 2 | totalRows - row | 1 | 3 | 3 3 3 |
| 2 | 1 | 3 | totalRows - row | 1 | 2 | 2 2 |
| 1 | 1 | 4 | totalRows - row | 1 | 1 | 1 |

现在 col_sp 变量相关内部 for 循环的 upper_limit 已被泛化，所有行上的表达式相同。col_num 变量相关内部 for 循环的 lower_limit 未被泛化，因为所有行上没有相同的表达式。

由于 col_num 变量的 lower_limit 值与 row 变量值匹配。因此，我们可以使用 row 变量使其保持一致，如下所示。

| 行级重复操作 | 列级重复操作：lower_limit <= col_sp <= upper_limit（下限） | 列级重复操作：lower_limit <= col_sp <= upper_limit（上限） | 列级重复操作：lower_limit <= col_sp <= upper_limit（默认值） | 列级重复操作：lower_limit <= col_num <= upper_limit（下限） | 列级重复操作：lower_limit <= col_num <= upper_limit（上限） | 列级重复操作：lower_limit <= col_num <= upper_limit（默认值） |
|---|---|---|---|---|---|---|
| 行 | 下限 | 上限 | 默认值 | 下限 | 上限 | 默认值 |
| 5 | 1 | 0 | totalRows - row | 1 | 5 | row |
| 4 | 1 | 1 | totalRows - row | 1 | 4 | row |
| 3 | 1 | 2 | totalRows - row | 1 | 3 | row |
| 2 | 1 | 3 | totalRows - row | 1 | 2 | row |
| 1 | 1 | 4 | totalRows - row | 1 | 1 | row |

col_sp 变量的 lower_limit 对所有行都相同。col_num 变量的 upper_limit 对所有行都相同。这意味着 col_sp 和 col_num 变量的 upper_limit 已针对任意数量的行进行了泛化。因此，我们用于打印空格字符的内部 for 循环条件变为；

| 循环条件 | lower_limit <= col_sp <= upper_limit |
|---|---|
| **数学表达式** | 1 <= col_sp <= (totalRows - row) |
| **语法** | `for( col_sp = 1; col_sp <= (totalRows - row); col_sp++ )` |

因此，我们用于打印数字字符的内部 for 循环条件变为；

| 循环条件 | lower_limit <= col_num <= upper_limit |
|---|---|
| **数学表达式** | 1 <= col_num <= row |
| **语法** | `for( col_num=1; col_num <= row ; col_num ++ )` |

我们的观察流程图可以如下所示。

![](img/67765455776ddeb6395161cd553ecd87_240_0.png)

让我们根据流程图编写程序。

### NumberPattern1D.c

```c
#include <stdio.h>
int main() {

    int  totalRows = 5;  //number of rows to display

    for( int row = totalRows ; row >=1 ; row -- ) {

        // spaces to be printed
        for( int col = 1; col <= ( totalRows - row ); col++ ) {
            printf("  ");
        }

        // row value to be printed
        for( int num=1; num<= row ; num++ ){
            printf("%d ", row);
        }// inner for-loop

        printf("\n");// moves control to the next line
    }// outer for-loop
    return 0;
}
```

### Output

```text
5 5 5 5 5
  4 4 4 4
    3 3 3
      2 2
        1
```

现在，测试不同数量的行；让我们将其更改为 7 并执行。它应该能正确工作。

### NumberPattern1D.c

```c
#include <stdio.h>
int main() {

    int  totalRows = 7;  //number of rows to display

    for( int row = totalRows ; row >=1 ; row -- ) {

        // spaces to be printed
        for( int col = 1; col <= ( totalRows - row ); col++ ) {
            printf( "  " );
        }

        // row value to be printed
        for( int num=1; num<= row ; num++ ){
            printf("%d ", row);
        }// inner for-loop

        printf("\n");// moves control to the next line
    }// outer for-loop
    return 0;
}
```

### Output

```text
7 7 7 7 7 7 7
  6 6 6 6 6 6
    5 5 5 5 5
      4 4 4 4
        3 3 3
          2 2
            1
```

## 替代方案

由于列值需要在打印空格和数字之间明确区分。我们可以尝试使用 if-else 条件结构来实现。

### NumberPattern2D.c

```c
#include <stdio.h>
int main() {

    int totalRows = 5; //number of rows to display

    for ( int row = totalRows; row >= 1; row-- ) {

        for ( int col = 1; col <= ( totalRows ); col++ ) {

            if ( col <= ( totalRows - row ) ) {

                // spaces to be printed
                printf("  " );

            } else {

                // row value to be printed
                printf("%d ", row );

            }

        }// inner for-loop

        printf("\n" );// moves control to the next line

    }// outer for-loop

    return 0;
}
```

### Output

```text
5 5 5 5 5
  4 4 4 4
    3 3 3
      2 2
        1
```

## 替代方案

让我们设计一个解决方案，通过递减 col 变量的 for 循环（从 5 到 1），使数字输出与 row 变量的值匹配。

| 变量 | 值1 | 值2 | 值3 | 值4 | 值5 |
|---|---|---|---|---|---|
| row | 5 |  |  |  |  |
| col | 5 | 4 | 3 | 2 | 1 |
| output | 5 | 5 | 5 | 5 | 5 |

row = 5，5 >= col >= 1（打印 row 值）或 row >= col >= 1（打印 row 值）

| 变量 | 值1 | 值2 | 值3 | 值4 | 值5 |
|---|---|---|---|---|---|
| row | 4 |  |  |  |  |
| col | 5 | 4 | 3 | 2 | 1 |
| output | space | 4 | 4 | 4 | 4 |

row = 4，4 >= col >= 1（打印 row 值）或 row >= col >= 1（打印 row 值）

| 变量 | 值1 | 值2 | 值3 | 值4 | 值5 |
|---|---|---|---|---|---|
| row | 3 |  |  |  |  |
| col | 5 | 4 | 3 | 2 | 1 |
| output | space | space | 3 | 3 | 3 |

row = 3，3 >= col >= 1（打印 row 值）或 row >= col >= 1（打印 row 值）

| 变量 | 值1 | 值2 | 值3 | 值4 | 值5 |
|---|---|---|---|---|---|
| row | 2 |  |  |  |  |
| col | 5 | 4 | 3 | 2 | 1 |
| output | space | space | space | 2 | 2 |

row = 2，2 >= col >= 1（打印 row 值）或 row >= col >= 1（打印 row 值）

| 变量 | 值1 | 值2 | 值3 | 值4 | 值5 |
|---|---|---|---|---|---|
| row | 1 |  |  |  |  |
| col | 5 | 4 | 3 | 2 | 1 |
| output | space | space | space | space | 1 |

row = 1，1 >= col >= 1（打印 row 值）或 row >= col >= 1（打印 row 值）

| 行级重复操作 | 列级重复操作：upper_limit >= col >= lower_limit（上限） | 列级重复操作：upper_limit >= col >= lower_limit（默认值） | 列级重复操作：upper_limit >= col >= lower_limit（下限） | 预期输出 |
|---|---|---|---|---|
| 行 | 上限 | 默认值 | 下限 | |
| 5 | 5 | row | 1 | 5 5 5 5 5 |
| 4 | 4 | row | 1 | 4 4 4 4 |
| 3 | 3 | row | 1 | 3 3 3 |
| 2 | 2 | row | 1 | 2 2 |
| 1 | 1 | row | 1 | 1 |

让我们尝试执行以下程序。

### NumberPattern3D.c

```c
#include <stdio.h>
int main() {
    int totalRows = 5; //number of rows to display

    for( int row = totalRows ; row >=1 ; row-- ) {

        for( int col = totalRows; col >= 1 ; col-- ) {

            if( col <= row ) {
                // row value to be printed
                printf( "%d ", row );
            }else {
                // spaces to be printed
                printf( "  " );
            }

        }
        printf("\n");// move control to the next line
    }

    return 0;
}
```

### Output

```text
5 5 5 5 5
  4 4 4 4
    3 3 3
      2 2
        1
```

现在，测试不同数量的行，让它为 7。它应该能正确工作。

### NumberPattern3D.c

```c
#include <stdio.h>
int main() {

    int totalRows = 7;  //number of rows to display

    for( int row = totalRows ; row >=1 ; row -- ) {

        for( int col = totalRows; col >= 1; col-- ) {

            if( col <= row ) {
                // row value to be printed
                printf("%d ", row );
            }else {
                // spaces to be printed
                printf( "  " );
            }

        }

        printf("\n");// moves control to the next line
    }

    return 0;

}
```

### Output

```text
7 7 7 7 7 7 7
  6 6 6 6 6 6
    5 5 5 5 5
      4 4 4 4
        3 3 3
          2 2
            1
```
