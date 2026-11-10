

在本例中，1 和 2 初始化了数组 x 的第一行，接下来的两行分别初始化第二行和第三行。初始化在第四行之前结束，因此第四行的成员默认值为 0 还是垃圾值取决于编译器。结果如下。

```c
x[0][0] = 1;
x[0][1] = 2;
x[1][0] = 3;
x[1][1] = 4;
x[2][0] = 5;
x[2][1] = 6;
x[3][0] = 0;
x[3][1] = 0;
```

下面的声明可以达到同样的效果。

```c
int x[4][2] = { 1, 2, 3, 4, 5, 6 };
```

在这里，编译器用可用的初始值逐行填充数组。编译器将 1 和 2 放在第一行（x[0]），将 3 和 4 放在第二行（x[1]），将 5 和 6 放在第三行（x[2]）。数组中其余成员被初始化为零或垃圾值。

### 11.4.4 不指定长度的数组初始化

如果声明了不指定长度的数组，C 编译器会自动创建一个足够大的数组来容纳所有的初始化值。这被称为不指定长度的数组（unsized array）。下面是带初始化的声明示例。

- (a) `char e1[] = "read error\n";`
- (b) `char e2[] = "write error\n";`
- (c)
  ```c
  int sgrs[][2] = {
      {1, 1},
      {2, 4},
      {3, 9},
      {4, 16},
  };
  ```

### 11.4.5 访问多维数组

多维数组的元素在计算机内存中连续存储在一块内存区域中。在从头到尾扫描这块内存时，存储的顺序是：数组的最后一个下标变化最快，而第一个下标变化最慢。例如，二维数组 x[2][2] 的元素按以下顺序存储：x[0][0]、x[0][1]、x[1][0]、x[1][1]。请看下面的代码。

```c
#include <stdio.h>
int main()
{
    int i,j;
    int a[3][2] = {{4,7},{1,0},{6,2}};
    for(i = 0; i < 3; i++)
    {
        for(j = 0; j < 2; j++)
        {
            printf("%d", a[i][j]);
        }
    }
    printf("\n");
    return 0;
}
```

由于计算机内存本质上是一维的，内存位置从 0 一直延伸到最高地址，多维数组不能以网格形式存储在内存中。相反，数组会被拆分并按行存储。考虑以下二维数组。

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_290_0.png)

请注意，方框内的数字并不是数组的实际索引——该数组是二维的，每个元素有两个索引——而只是一些任意的占位符，以便读者在下面的示例中看清哪些元素是对应的。行号对应于数组的第一个索引，因此编号从 0 到 2，而不是从 1 到 3。

在计算机中，上述数组实际上“看起来”是这样的。

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_290_1.png)

另一种表达方式是，数组按行存储，且第二个索引变化最快。二维数组总是被认为具有如下形式：

```c
array_name[row][column]
```

每一行存储的元素包含了多个列。在一维表示中，列索引在每个行内从 0 变化到 (size - 1)，其中 size 是数组的列数。因此，当遍历计算机内部数组的一维表示时，列索引的变化比行索引更快。

为了说明多维数组的用法，可以使用下面这段代码来填充或初始化数组 a2 的元素。

```c
int i, j;
for(i = 0; i < 5; i = i + 1)
{
    for(j = 0; j < 7; j = j + 1)
    {
        a2[i][j] = 10 * i + j;
    }
}
```

这对嵌套循环将 a[1][2] 设为 12，将 a[4][1] 设为 41，等等。由于 a2 的第一个维度是 5，第一个下标变量 i 从 0 运行到 4。类似地，第二个下标变量从 0 变化到 6。

可以用类似的一对嵌套循环，以二维的方式打印数组 a2，以显示其结构。

```c
for(i = 0; i < 5; i = i + 1)
{
    for(j = 0; j < 7; j = j + 1)
        printf("%d\t", a2[i][j]);
    printf("\n");
}
```

`printf()` 字符串中的字符 `\t` 是制表符，它本身就是一个转义序列或控制代码。为了更清楚地理解这一点，可以同时打印“行”和“列”下标，使它们变得明确。因此，可以使用下面的代码。

```c
for(j = 0; j < 7; j = j + 1)
    printf("%4d:", j);
printf("\n");
for(i = 0; i < 5; i = i + 1)
{
    printf("%d:", i);
    for(j = 0; j < 7; j = j + 1)
        printf("%4d", a2[i][j]);
    printf("\n");
}
```

最后这段代码会打印出

```text
     0:    1:    2:    3:    4:    5:    6:
 0:    0     1     2     3     4     5     6
 1:   10    11    12    13    14    15    16
 2:   20    21    22    23    24    25    26
 3:   30    31    32    33    34    35    36
 4:   40    41    42    43    44    45    46
```

最后，没有理由一定要先循环行再循环列；根据用户想要做的事情，这两个循环可以互换，如下所示。

```c
for(j = 0; j < 7; j = j + 1)
{
    for(i = 0; i < 5; i = i + 1)
        printf("%d\t", a2[i][j]);
    printf("\n");
}
```

请注意，`i` 仍然是第一个下标，它仍然从 0 运行到 4；`j` 仍然是第二个下标，它仍然从 0 运行到 6。

可以发现，程序仍然可以毫无问题地运行。这是因为多维数组在实现上是一个大的单维数组。当引用数组中的一个元素时，所用的两个索引会被转换为该数组的单一索引。

### 11.4.6 处理二维数组

二维数组最重要的应用是矩阵。矩阵被定义为一个有序的矩形数字阵列。它们可以用来表示线性方程组。

**矩阵的转置**

矩阵的转置是通过将行与列互换得到的，即对于

矩阵 A = (a_{ij})

A 的转置是 A^T = (a_{ji})，其中 i 是行号，j 是列号。

例如，矩阵 A 的转置如下所示。

**A =**

| 5 | 2 | 3 |
|---|---|---|
| 4 | 7 | 1 |
| 8 | 9 | 9 |

**A^T =**

| 5 | 4 | 8 |
|---|---|---|
| 2 | 7 | 9 |
| 3 | 1 | 9 |

对于方阵（m = n），可以用转置来检查矩阵是否对称。对于对称矩阵，A = A^T。

**A =**

| 1 | 2 |
|---|---|
| 2 | 3 |

**A^T =**

| 1 | 2 |
|---|---|
| 2 | 3 |

**A^T = A**

下面的程序求一个矩阵的转置。

```c
#include <stdio.h>
int main()
{
    int row, col;
    int i, j, value;
    int mat[10][10], transp[10][10];
    printf("\n Input the number of rows:");
    scanf("%d", &row);
    printf("Input number of cols:");
    scanf("%d", &col);
    for(i = 0 ; i < row ; i++)
        for(j = 0 ; j < col ; j++)
        {
            printf("Input Value for : %d: %d:", i+1, j+1);
            scanf("%d", &value);
            mat[i][j] = value;
        }
    printf("\n Entered Matrix is as follows:\n");
    for(i = 0 ; i < row ; i++)
    {
        for(j = 0 ; j < col ; j++)
            printf("%d", mat[i][j]);
        printf("\n");
    }
    for(i = 0 ; i < row ; i++)
    {
        for(j = 0 ; j < col ; j++)
        {
            transp[i][j] = mat[j][i];
        }
    }
    printf("\n Transpose of the matrix is as follows:\n");
    for(i = 0; i < col; i++)
    {
        for(j = 0; j < row; j++)
        {
            printf("%d", transp[i][j]);
        }
        printf("\n\n");
    }
    return 0;
}
```

在上面的例子中，需要记住的是，行数和列数都必须小于或等于 10。

**矩阵的加法和减法**

两个矩阵 *A* 和 *B* 可以相加或相减，当且仅当它们的维度相同，即两个矩阵具有相同的行数和列数。以矩阵为例，

\[A=\begin{pmatrix}1&2&3\\1&0&2\end{pmatrix}\qquad B=\begin{pmatrix}2&1&2\\1&0&3\end{pmatrix}\]

**加法** 如果上面的 *A* 和 *B* 是同类型的矩阵，那么它们的和是通过将对应元素相加得到的，即 \(a_{ij}+b_{ij}\)。

下面是将 *A* 和 *B* 相加的示例。

\[A+B=\begin{pmatrix}1&2&3\\1&0&2\end{pmatrix}+\begin{pmatrix}2&1&2\\1&0&3\end{pmatrix}=\begin{pmatrix}3&3&5\\2&0&5\end{pmatrix}\]

**减法** 如果 *A* 和 *B* 是同类型的矩阵，那么它们的差是通过将对应元素相减得到的，即 \(a_{ij}-b_{ij}\)。

下面是矩阵相减的示例。

\[A-B=\begin{pmatrix}1&2&3\\1&0&2\end{pmatrix}-\begin{pmatrix}2&1&2\\1&0&3\end{pmatrix}=\begin{pmatrix}-1&1&1\\0&0&-1\end{pmatrix}\]

下面的程序是关于矩阵加法的。

```c
#include <stdio.h>
#include <stdlib.h>
#define row 10
#define col 10
int main()
{
    int row1, col1;
    int row2, col2;
    int i,j;
    float mat1[row][col];
    float mat2[row][col];
    float mat_res[row][col];

    printf("\n Input the row of the matrix-1:");
    scanf("%d", &row1);
    printf("\n Input the col of the matrix-1:");
    scanf("%d", &col1);
    printf("\n Input data for matrix-> 1\n");
    for(i = 0; i< row1; i++)
    {
        for(j = 0; j<col1; j++)
        {
            printf("Input Value for: %d: %d:", i+1, j+1);
            scanf("%f", &mat1[i][j]);
        }
    }
    printf("\n Input the row of the matrix ->2:");
    scanf("%d", &row2);
    printf("\n Input the col of the matrix->2:");
    scanf("%d", &col2);
    printf("\n Input data for matrix-> 2\n");
    for(i = 0; i< row2; i++)
    {
        for(j = 0; j<col2; j++)
        {
            printf("Input Value for: %d: %d:", i+1, j+1);
            scanf("%f", &mat2[i][j]);
        }
    }
    printf("\n Entered Matrix First is:\n");
    for(i = 0; i < row1; i++)
    {
        for(j = 0; j < col1; j++)
        {
            printf("%f", mat1[i][j]);
        }
        printf("\n");
    }
    printf("\n Entered Matrix Two is:\n");
    for(i = 0; i < row2; i++)
    {
        for(j = 0; j < col2; j++)
        {
            printf("%f", mat2[i][j]);
        }
        printf("\n\n");
    }
    if((row1 == row2) && (col1 == col2))
    {
        printf("\n Addition is possible and");
        printf("the result is: \n");
        for(i = 0; i<row1; i++)
        for(j = 0; j<col1; j++)
            mat_res[i][j] = mat1[i][j]+mat2[i][j];
        for(i = 0; i < row1; i++)
        {
            for(j = 0; j < col1; j++)
                printf("%f", mat_res[i][j]);
```

