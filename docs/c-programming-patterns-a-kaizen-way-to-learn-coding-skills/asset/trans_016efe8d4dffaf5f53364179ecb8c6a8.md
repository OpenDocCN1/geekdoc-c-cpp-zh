
让我们执行下面的程序。

## Pattern1A_2.C

```c
#include <stdio.h>

int main() {

    int totalRows = 5;  //number of rows to display

    // Row level Repetitive Action:
    // Action1,Executes Column level Repetitive Action
    // Action2,Move cursor to next row.
    for( int row = 1; row <= totalRows; row ++ ) {

        // Column level Repetitive Action :
        for( int col = 1; col <= row ; col++ ) {

            // Action1,Move cursor in the same row
            // Action2.print "★" character
            printf("★ ");

        }
        printf("\n");// Move cursor to the next row
    }

    return 0;

}
```

### 输出

```
★
★ ★
★ ★ ★
★ ★ ★ ★
★ ★ ★ ★ ★
```

现在，测试不同的行数，设为 10。它应该能正确工作，这样我们就可以确认我们的解决方案是通用且适用于任意行数的。

## Pattern1A_1.C

```c
#include <stdio.h>

int main() {

    int totalRows = 10;   //number of rows to display

    // Row level Repetitive Action:

    // Action1.Executes Column level Repetitive Action

    // Action2.Move cursor to next row.

    for( int row = 1 ; row <= totalRows ; row ++ ) {

        // Column level Repetitive Action :

        for( int col = 1 ; col <= row ; col++ ) {

            // Action1.Move cursor in the same row

            // Action2.print "*" character

            printf("* ");

        }

        printf("\n");// Move cursor to the next row

    }

    return 0;

}
```

### 输出

```
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

## Pattern1B

我们的编程任务是在计算机屏幕的一部分上输出如下所示的这种简单的基于图片的模式。我们的方法将把计算机屏幕视为由包含小方框的行和列组成的组合。我们可以将计算机屏幕视为由遍布整个屏幕的 (row, column) 数值配对方框组成的组合。每个方框仅被视为一个字符的驻留。我们还知道，完整的模式可以很容易地表示为所选 (row, column) 数值配对的集合。

![](img/67765455776ddeb6395161cd553ecd87_115_0.png)

![](img/67765455776ddeb6395161cd553ecd87_115_1.png)

### 输出分析

我们可以通过知道其在计算机屏幕上的唯一 (row, column) 数值组合来确定每个 “*” 字符的确切位置。

| | 列=1 | 列=2 | 列=3 | 列=4 | 列=5 |
|---|---|---|---|---|---|
| 行=1 | \* (1,1) | \* (1,2) | \* (1,3) | \* (1,4) | \* (1,5) |
| **行=2** | **\* (2,1)** | \* (2,2) | \* (2,3) | \* (2,4) |  |
| 行=3 | \* (3,1) | \* (3,2) | \* (3,3) |  |  |
| 行=4 | \* (4,1) | \* (4,2) |  |  |  |
| 行=5 | \* (5,1) |  |  |  |  |

(2, 1) 表示字符 “*” 在表格中的 **第二行** 和 **第一列**。

例如，对于数值对(2,1)，值 2 表示行号，值 1 表示列号。这是我们能够在计算机屏幕上的特定位置清晰识别 “*” 字符的实际度量。

| 模式生成步骤 ( 总行数 = 5) | 计算机屏幕 |
|---|---|
| 对于行 = 1<br>在同一第 1 行打印 “*” 五次<br>然后移动到第 2 行 | 1 2 3 4 5 6 7 8 9<br>行 1: * * * * *<br>→ (箭头指向第 2 行) |
| 对于行 = 2<br>在同一第 2 行打印 “*” 四次<br>然后移动到第 3 行 | * * * * *<br>* * * *<br>→ (箭头指向第 3 行) |
| 对于行 = 3<br>在同一第 3 行打印 “*” 三次<br>然后移动到第 4 行 | * * * * *<br>* * * *<br>* * *<br>→ (箭头指向第 4 行) |
| 对于行 = 4<br>在同一第 4 行打印 “*” 两次<br>然后移动到第 5 行 | * * * * *<br>* * * *<br>* * *<br>* *<br>→ (箭头指向第 5 行) |
| 对于行 = 5<br>在第 5 行打印 “*” 一次<br>然后移动到第 6 行 | * * * * *<br>* * * *<br>* * *<br>* *<br>*<br>→ (箭头指向第 6 行) |

## 将步骤转换为 C 程序。

| C 内置方法的使用 | |
|---|---|
| 为了将光标移动到下一行 | printf("\n") ; |
| 为了将光标移动并在同一行打印 “*” 字符 | printf("*"); |

这些是两种将在程序中重复多次的语句。

printf("\n") ; & printf("*");

因此我们可以使用 for 循环来实现。

## 列级重复操作

让我们将二维模式的两个属性行和列视为变量；

**row** → 变量 _type of integer_ 用于一次存储一个整数值并表示 1 到 5 之间的行号。

**col** → 变量 _type of integer_ 用于一次存储一个整数值并表示 1 到 5 之间的列号。

**totalRows** → 变量 _type of integer_ 用于存储总行数的整数值。

## 追踪表

| (row, col) 值对描述了 “*” 字符在显示屏上的位置 | | | | |
|---|---|---|---|---|
| 行=1, 列=1 | 行=1, 列=2 | 行=1, 列=3 | 行=1, 列=4 | 行=1, 列=5 |
| 行=2, 列=1 | 行=2, 列=2 | 行=2, 列=3 | 行=2, 列=4 | |
| 行=3, 列=1 | 行=3, 列=2 | 行=3, 列=3 | | |
| 行=4, 列=1 | 行=4, 列=2 | | | |
| 行=5, 列=1 | | | | |

每个行 = 1 到 5 的 col 变量的值。

| 行级重复操作 | 列级重复操作 | 预期输出 |
|---|---|---|
| 变量: row | 变量: col | |
| 1 | 1,2,3,4,5 | * * * * * |
| 2 | 1,2,3,4 | * * * * |
| 3 | 1,2,3 | * * * |
| 4 | 1,2 | * * |
| 5 | 1 | * |

为了定义具有计数器更新增量值 1 的 for 循环控制结构，我们需要一组 **min_val** 和 **max_val**，因为循环需要在某处开始和结束。

| 行级重复操作 | 列级重复操作 | 预期输出 |
|---|---|---|
| 变量 : row | 变量 : col | |
| | 最小值 | 最大值 | |
| 1 | 1 | 5 | * * * * * |
| 2 | 1 | 4 | * * * * |
| 3 | 1 | 3 | * * * |
| 4 | 1 | 2 | * * |
| 5 | 1 | 1 | * |

对于每个不同的行值，我们都有一个不同的 **max_val**。

| 目标 |
|---|
| 我们需要为列 **max_val** 找到一个 _唯一表达式_，这样如果增加行数，它应该生成相应 _行大小_ 的模式。 |

## 解决方案方法

我们需要使用可用变量来概括列 max_val 的非重复数字模式。我们可以使用变量 totalRows。变量 totalRows 已被赋值为 5 作为总行数。

| 列级重复操作 |
|---|
| 变量 : row | 循环条件( 变量 : col ) |
| | 最小值 | 最大值 |
| | | 默认 | 1 |
| 1 | 1 | 5 | totalRows |
| 2 | 1 | 4 | totalRows - 1 |
| 3 | 1 | 3 | totalRows - 2 |
| 4 | 1 | 2 | totalRows - 3 |
| 5 | 1 | 1 | totalRows - 4 |

再次存在非重复的数值。我们可以按如下方式第二次表达 max_val。

| 列级重复操作 |
|---|
| 变量 : row | 循环条件( 变量 : col ) |
| | 最小值 | 最大值 |
| | | 默认 | 1 | 2 |
| 1 | 1 | 5 | totalRows | (totalRows +1) - 1 |
| 2 | 1 | 4 | totalRows -1 | (totalRows +1) - 2 |
| 3 | 1 | 3 | totalRows - 2 | (totalRows +1) - 3 |
| 4 | 1 | 2 | totalRows - 3 | (totalRows +1) - 4 |
| 5 | 1 | 1 | totalRows - 4 | (totalRows +1) - 5 |

列 max_val 表达式的一部分遵循与行相同的数值模式。

| 列级重复操作 |
|---|
| 变量 : row | 循环条件( 变量 : col ) |
| | 最小值 | 最大值 |
| | | 默认 | 1 | 2 | 3 |
| 1 | 1 | 5 | totalRows | (totalRows +1) - 1 | (totalRows +1) - row |
| 2 | 1 | 4 | totalRows -1 | (totalRows +1) - 2 | (totalRows +1) - row |
| 3 | 1 | 3 | totalRows - 2 | (totalRows +1) - 3 | (totalRows +1) - row |
| 4 | 1 | 2 | totalRows - 3 | (totalRows +1) - 4 | (totalRows +1) - row |
| 5 | 1 | 1 | totalRows - 4 | (totalRows +1) - 5 | (totalRows +1) - row |

进一步我们可以用 totalRows 和 row 变量来表达它。

现在，max_val 具有相同的表达式，并且对于每个 row 值都是一致的。

我们现在可以为每个行值定义列级 for 循环。

| 列级 for 循环的元素 |
|---|
| 最小值 | 1 |
| 最大值 | (totalRows +1) - row |
| 变量名 | col |
| 语句 | printf("%s"); |
