
和任何变量一样，数组在使用之前必须声明。声明的一般形式为：

`type name[size];`

类型指定数组中包含的元素类型（例如 `int` 或 `float`），`size` 表示数组内可以存储的最大元素个数。例如：

`float height[50];` 声明 `height` 为包含 50 个元素的数组。任何从 0 到 49 的下标都是有效的。在 C 中，数组索引从零开始。因此 `height[0]` 指向数组的第一个元素。单个数组元素可以使用普通变量语句使用，例如：

`g = height[i];` 将数组第 `i` 索引的值赋值给变量 `g`。如果 `i` 被声明为整数变量，当执行上述语句时，如果 `i` 等于 7，则 `height[7]` 的值将被赋值给 `g`。通过表达式 `(low + high)`。如果 `low` 等于 1 且 `high` 等于 9，则 `data[5]` 的值将被赋值。如果 `low` 等于 1 且 `high` 等于 10，则 `data[5]` 的值将被引用。

通过单个数组表示相关数据集合使我们能够编写简洁高效的程序。例如，通过改变作为下标的变量值，我们可以轻松遍历数组中的元素。如下循环：

```c
for (i = 0; i < 100; i++)
    sum = sum + grades[i];
```

遍历数组的前 100 个元素（0 到 99），并将每个的值加到 `sum` 中。循环完成后，变量 `sum` 将包含 `grades` 数组的前 100 个值。除了整数常量，整数表达式也可以放在括号内引用数组的特定元素。

正如变量在使用之前必须声明一样，数组的声明涉及指定数组中包含的元素类型及其个数。系统需要这些信息来确定为特定数组预留多少内存空间。`int values[10];` 为名为 `values` 的数组预留足够的空间，可以容纳 10 个整数。参考下图进行概念化：

![](img/42571661744bb1de66abc4519753_120_0.png)

| | |
| :--- | :--- |
| | `values[0]` |
| | `values[1]` |
| | `values[2]` |
| | `values[3]` |
| | `values[4]` |
| | `values[5]` |
| | `values[6]` |
| | `values[7]` |
| | `values[8]` |
| | `values[9]` |

存储在内存中的数组 `values`。

### 9.2.1 数组声明的一些变体

```c
int numbers[10] = { 34, 27, 16 };
static int numbers[] = { 2, -3, 45, 79, -5, 9, 28, -1, 0 };
static char text[] = "Welcome to New Zealand.";
static float radix[12] = { 134.362, 193.248 };
```

程序：

```c
#include <stdio.h>
main() {
    int numbers[100];
    float averages[20];
    numbers[2] = 10;
    --numbers[2];
    printf("The 3rd element of array numbers is %d\n", numbers[2]);
}
```

程序输出

`numbers` 数组的第 3 个元素是 9

## 9.3 数组初始化

我们可以在声明普通变量的同时，初始化数组元素。数组初始化的一般形式为：

`type array_name[size] = {list of values};`

列表中的值用逗号分隔，例如语句：`int number[3] = {0, 0, 0};` 将数组大小声明为 3，并为每个元素赋值 0。如果列表中的值个数少于元素个数，则只初始化相应数量元素。剩余元素将自动设置为 0。在数组声明中，可以省略大小，在这种情况下，编译器为所有初始化元素分配足够的空间。对于示例语句：

```c
int counter[] = {1, 2, 3};
```

将声明数组包含三个初始值为 1、2、3 的元素。只要我们初始化了数组中的每个元素，这种方法就能正常工作。C 语言中数组初始化有两个缺点：

1. 没有方便的方法可以只初始化选定的元素。
2. 没有简捷方法来初始化大量元素。

# 114 C语言编程 – 实用视角

```c
printf("Enter the elements of the array\n");
for (i = 0; i < n; i++)
    scanf("%d", &a[i]);
for (i = 0; i < n; i++) {
    if (a[i] < 0)
        count_neg++;
    else
        count_pos++;
}
printf("There are %d negative numbers in the array\n", count_neg);
printf("There are %d positive numbers in the array\n", count_pos);
```

## 9.4 多维数组

通常需要存储和操作二维数据结构，例如矩阵和表格。在这里，数组有两个下标。其中一个下标表示行，另一个表示列。

二维数组的声明如下：

```c
data_type array_name[row_size][column_size];
int m[10][20];
```

这里，`m` 被声明为一个具有 10 行（编号从 0 到 9）和 20 列（编号从 0 到 19）的矩阵。矩阵的第一个元素是 `m[0][0]`，最后一列是 `m[9][19]`。

## 9.5 下标变量规则

下标变量可以是双精度型、整型或字符型。最大下标数量由编译器决定。算术表达式可以用于下标。下标必须是整数值。你的程序中必须包含一条语句来为你的数组留出空间（维度）。在 C 语言中，二维数组被视为一个一维数组，其元素是一维数组（即行）。

例如，

一个 4x3 的 T 类型数组（其中 "T" 是某种数据类型）可以如下方式声明：`T mat[4][3]`，其描述如下方的方案所示：

```
mat = mat[0] -> a00 | a01 | a02 |
mat[1] -> a10 | a11 | a12 |
mat[2] -> a20 | a21 | a22 |
mat[3] -> a30 | a31 | a32 |
```

数组元素按行存储在内存中，因此类型为 T 的元素 `mat[m][n]` 的数组方程为：

```c
address(mat[i][j]) = address(mat[0][0]) + (i * n + j) * size(T)
address(mat[i][j]) = address(mat[0][0]) + i * size(T) + j * size(T)
address(mat[i][j]) = address(mat[0][0]) + i * size(row of T) + j * size(T)
```

## 9.6 多维数组的元素

下面所示了一个二维数组 `marks[4][3]`。第一个元素由 `marks[0][0]` 给出，包含 35.5，第二个元素是 `marks[0][1]` 包含 40.5，以此类推。

| Marks[0][0] | Marks[0][1] | Marks[0][2] |
| :--- | :--- | :--- |
| 35.5 | 40.5 | 45.5 |
| Marks[1][0] | Marks[1][1] | Marks[1][2] |
| 50.5 | 55.5 | 60.5 |
| Marks[2][0] | Marks[2][1] | Marks[2][2] |
| Marks[3][0] | Marks[3][1] | |

### 9.6.1 多维数组的初始化

与一维数组一样，二维数组可以通过在声明后紧跟大括号括起来的初始值列表来初始化。

示例：

```c
int table[2][3] = {1, 2, 3, 4, 5, 6};
```

将第一行从第一列初始化为 1，第二列初始化为 2。初始化是按行完成的。上述语句等价地写为：

```c
int table[2][3] = {{1, 2, 3}, {4, 5, 6}};
```

通过大括号包围每行的元素。C 允许三维或更多维的数组。编译器决定最大维数。多维数组声明的一般形式为：

```c
date_type array_name[s1][s2][s3]...[sn];
```

其中 `s` 是第 `i` 维的大小。

`float table[5][4];`

/* 两个矩阵矩阵并将结果存储在矩阵中的示例程序 */

```cpp
#include <stdio.h>
#include <conio.h>
int main() {
    int a[10][10][10], c[10][10], i, j, m, p, q;
    clrscr();
    printf("enter the order of the matrix\n");
    scanf("%d%d", &m, &n);
    if (m == p && n == q) {
        printf("enter the elements of the matrix a\n");
        for (i = 0; i < m; i++)
            for (j = 0; j < n; j++)
                scanf("%d", &a[i][j]);
        printf("enter the elements of the matrix b\n");
        for (i = 0; i < p; i++)
            for (j = 0; j < q; j++)
                scanf("%d", &a[i][j]);
        printf("There are %d negative numbers in the array\n", count_neg);
        printf("There are %d positive numbers in the array\n", count_pos);
    }
}
```
