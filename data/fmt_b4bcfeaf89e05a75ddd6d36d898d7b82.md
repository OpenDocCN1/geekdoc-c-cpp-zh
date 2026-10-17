
| 学号 1 | 75.00 | 90.00 | 40.00 | 40.00 | 245.00 |
| 学号 2 | 50.00 | 60.00 | 70.00 | 85.00 | 265.00 |
| 学号 3 | 80.00 | 85.00 | 55.00 | 60.00 | 280.00 |

在程序 6 中，我们可以观察到我们定义了两个符号常量，即 `ROLLNO` 和 `SUBJECT`。这两个符号常量定义了数组的最大行数和列数。然后使用嵌套的 `for` 循环从用户那里读取不同科目的成绩。在同一个循环中，我们计算每个学生的总分数。最后，输出以表格形式呈现。

让我们再举一个例子，以便更好地理解多维数组的概念。矩阵是数学中常见的对象。可以对矩阵执行许多操作。其中一种执行的操作是两个矩阵的乘法。程序 7 说明了如何计算两个矩阵的乘积：

#### 程序 7

```c
/* Program to multiply two matrices */

#include <stdio.h>
#define ROW 25
#define COL 25

/* Global variable */
int i_Amatrix[ROW][COL];
int i_Bmatrix[ROW][COL];
int i_ResultMatrix[ROW][COL];
int i_ROW[2], i_COL[2];

/* Function to read values in matrix */
void InputValues(int i_matrix[ROW][COL], int i_row, int i_col)
{
    int i_octr, i_ict;

    printf("\nEnter elements of matrix\n");
    printf("-------------------------------------\n");
    for (i_octr = 0; i_octr < i_row; i_octr++)
    {
        for (i_ict = 0; i_ict < i_col; i_ict++)
        {
            printf("\nEnter element[%d][%d]: ", i_ict, i_ict);
            scanf("%d", &i_matrix[i_octr][i_ict]);
        }
    }
}
/* End of InputValues function */

/* Function to print values of matrix */
void PrintValues(int i_matrix[ROW][COL], int i_row, int i_col)
{
    int i_octr, i_ict;

    for (i_octr = 0; i_octr < i_row; i_octr++)
    {
        for (i_ict = 0; i_ict < i_col; i_ict++)
        {
            printf("%4d ", i_matrix[i_octr][i_ict]);
        }
        printf("\n");
    }
} /* End of PrintValues function */

/* Function to multiply values of matrix */
void MultiplyMatrix()
{
    int i_ict r, i_jct r, i_kct r;
    for (i_ict r = 0; i_ict r < i_ROW[0]; i_ict r++)
    {
        for (i_jct r = 0; i_jct r < i_COL[1]; i_jct r++)
        {
            i_ResultMatrix[i_ict r][i_jct r] = 0;
            for (i_kct r = 0; i_kct r < i_ROW[0]; i_kct r++)
                i_ResultMatrix[i_ict r][i_jct r] +=
                    i_Amatrix[i_ict r][i_kct r] * i_Bmatrix[i_kct r][i_jct r];
        }
    }
} /* End of MultiplyMatrix function */

/* Beginning of main function */
main()
{
    printf("\nNumber of rows in Matrix A: ");
    scanf("%d", &i_ROW[0]);
    printf("\nNumber of columns in Matrix A: ");
    scanf("%d", &i_COL[0]);
    printf("\nNumber of rows in Matrix B: ");
    scanf("%d", &i_ROW[1]);
    printf("\nNumber of columns in Matrix B: ");
    scanf("%d", &i_COL[1]);
    if (i_COL[0] != i_ROW[1])
    {
        printf("Columns in first matrix must be equal Rows in second matrix.\n");
        printf("Matrix Multiplication not possible\n");
        exit(1);
    }
    /* Read values in both Matrix */
    InputValues(i_Amatrix, i_ROW[0], i_COL[0]);
    InputValues(i_Bmatrix, i_ROW[1], i_COL[1]);
    /* Multiply the matrix */
    MultiplyMatrix();
    /* Print Result */
    printf("\nMatrix A\n");
    PrintValues(i_Amatrix, i_ROW[0], i_COL[0]);
    printf("\nMatrix B\n");
    PrintValues(i_Bmatrix, i_ROW[1], i_COL[1]);
    printf("\nResult Matrix\n");
    PrintValues(i_ResultMatrix, i_ROW[0], i_COL[1]);
    return;
} /* End of function main */
```

**输出 1：**

矩阵 A 的行数: 2

矩阵 A 的列数: 2

矩阵 B 的行数: 2

矩阵 B 的列数: 2

输入矩阵元素

----------------------------------

输入元素 [0][0]: 1

输入元素 [0][1]: 2

输入元素 [1][0]: 3

输入元素 [1][1]: 4

输入矩阵元素

----------------------------------

输入元素 [0][0]: 5

输入元素 [0][1]: 6

输入元素 [1][0]: 7

输入元素 [1][1]: 8

矩阵 A

   1    2

   3    4

矩阵 B

   5    6

   7    8

结果矩阵

  19   22

  43   50

**输出 2：**

矩阵 A 的行数: 2

矩阵 A 的列数: 2

矩阵 B 的行数: 3

矩阵 B 的列数: 3

第一个矩阵的列数必须等于第二个矩阵的行数。

矩阵乘法不可能执行

在程序 7 中，我们观察到程序变得更加复杂。许多实际问题无法仅使用二维数组来解决。考虑一家公司需要分析其产品在若干年期间内总销售额的情况。由于公司拥有许多产品和许多销售员，我们需要记录哪个销售员在哪一年销售了哪种产品。为了存储此类信息，二维数组将会失效。因此，我们需要三维数组。下一节将简要讨论三维数组。

#### 三维数组

前面提到的销售分析数据可以存储在下述数组中：

```c
int i_sales[year][product][salesman];
```

其中 `year` 指要考虑的年份数量，`product` 指公司拥有的产品数量，`salesman` 指在公司工作的销售员数量。则数组元素中的值将指代某个销售员在特定年份销售某种产品所完成的销售额。上述结构的示意图如图 5 所示：

![图 5](img/5d422ba7108ffdf64376be51eaf0c459_212_0.png)

从图 5 中可以看出，我们得到了三维的数据视图。程序 8 说明了在销售分析中使用三维数组的案例：

#### 程序 8

```c
/* Program illustrates the use of three-dimensional array */
#include <stdio.h>
#define YEAR 2
#define PROD 3
#define SMAN 3

/* Beginning of main function */
main()
{
    int i_sales[YEAR][PROD][SMAN], i_tot_sales[YEAR][PROD] = {0};
    int i_yctr, i_pctr, i_sctr;

    /* Read Data of Sales */
    for (i_yctr = 0; i_yctr < YEAR; i_yctr++)
    {
        for (i_pctr = 0; i_pctr < PROD; i_pctr++)
        {
            for (i_sctr = 0; i_sctr < SMAN; i_sctr++)
            {
                printf("Sale of product %d for salesman %d in year %d : ", i_pctr + 1, i_sctr + 1, i_yctr + 1);
                scanf("%d", &i_sales[i_yctr][i_pctr][i_sctr]);
            }
            printf("\n");
        }
    }

    /* Calculate total sales of a product in a year */
    for (i_yctr = 0; i_yctr < YEAR; i_yctr++)
    {
        for (i_pctr = 0; i_pctr < PROD; i_pctr++)
        {
            for (i_sctr = 0; i_sctr < SMAN; i_sctr++)
            {
                i_tot_sales[i_yctr][i_pctr] = i_tot_sales[i_yctr][i_pctr] + i_sales[i_yctr][i_pctr][i_sctr];
            }
        }
    }

    /* Print total sales of a product */
    for (i_yctr = 0; i_yctr < YEAR; i_yctr++)
    {
        for (i_pctr = 0; i_pctr < PROD; i_pctr++)
        {
            printf("\nTotal sales of product %d in year %d is %d", i_pctr + 1, i_yctr + 1, i_tot_sales[i_yctr][i_pctr]);
        }
        printf("\n");
    }

    return;
} /* End of function main */
```

##### 输出

```
第 1 年销售员 1 的产品 1 销售额：50
第 1 年销售员 2 的产品 1 销售额：75
第 1 年销售员 3 的产品 1 销售额：85

第 1 年销售员 1 的产品 2 销售额：90
第 1 年销售员 2 的产品 2 销售额：25
第 1 年销售员 3 的产品 2 销售额：80

第 1 年销售员 1 的产品 3 销售额：95
第 1 年销售员 2 的产品 3 销售额：55
第 1 年销售员 3 的产品 3 销售额：50

第 2 年销售员 1 的产品 1 销售额：45
第 2 年销售员 2 的产品 1 销售额：90
第 2 年销售员 3 的产品 1 销售额：54

第 2 年销售员 1 的产品 2 销售额：75
第 2 年销售员 2 的产品 2 销售额：80
第 2 年销售员 3 的产品 2 销售额：95

第 2 年销售员 1 的产品 3 销售额：35
第 2 年销售员 2 的产品 3 销售额：67
第 2 年销售员 3 的产品 3 销售额：78

第 1 年产品 1 的总销售额为 210
第 1 年产品 2 的总销售额为 195
第 1 年产品 3 的总销售额为 200

第 2 年产品 1 的总销售额为 189
第 2 年产品 2 的总销售额为 250
第 2 年产品 3 的总销售额为 180
```

从程序 8 中可以看出，使用更多维度的数组有助于我们更好地分析数据。

### 摘要

在本章中，我们讨论了一种称为数组的派生数据类型。我们了解到，数组是与单个名称关联的一组值，并且数组中的所有元素都具有相同的数据类型。我们还学习了如何使用索引来访问数组中的单个元素。在 C 语言中，索引的值从 0 开始。因此，用户需要记住数组的大小。数组的最大索引值总是比数组的大小少 1。最后，我们了解到数组可以是单维的，也可以是多维的。

### 复习问题

- Q1. 数组在 C 语言中的重要性是什么？
- Q2. 数组中索引值的重要性是什么？
- Q3. 请解释初始化一维数组的不同方法。
- Q4. 请论证“数组名称在右侧使用时充当指针”这一说法。
- Q5. 请论证“编译器在执行 C 程序时不检查数组边界”这一说法。
- Q6. 计算 `float` 类型数组中第 25 个元素的地址。假设数组的基地址为 65500，存储 `float` 值所需的内存大小为 8 字节。
- Q7. 区分一维数组和二维数组。
- Q8. 解释如何在 C 中创建 `ROW × COLUMN` 矩阵。它在内存中将如何表示？
- Q9. 请解释初始化二维数组的不同方法。

### 实践练习

- Q1. 编写一个程序，从用户处获取 `n` 个元素并将其存储在数组中。将这些元素全部增加一个整数值 `m`，并按其位置的降序存储在另一个数组中。例如，如果有 10 个元素，`A[1]` 应存储在 `B[10]` 中。显示这两个数组。
- Q2. 编写一个程序，从用户处获取 `n` 个元素并将其存储在数组中。找出数组中所有奇数和所有偶数的总和。
- Q3. 编写一个程序，从用户处获取 `n` 个元素并将其存储在数组中。找出其中是回文数的元素，并将它们存储在另一个数组中。
- Q4. 编写一个程序，使用函数 `INPUT` 读取 `N` 个数字。将这些数字传递给函数 `sort`，根据用户的选择按升序或降序对这些数字进行排序。
- Q5. 编写一个程序，使用函数 `REMOVE(arr, N)` 从数组 `arr` 中删除数字 `N` 的所有出现。如果没有重复的数字，则打印适当的输出消息；否则，打印不含重复数字的列表。
- Q6. 编写一个程序，使用函数 `square(arr)` 对数组的每个元素进行平方运算。
- Q7. 编写一个程序，使用函数 `Count(arr, N)` 统计数字 `N` 在数组 `arr` 中出现的所有次数。如果列表中不存在该数字，则打印适当的输出消息；否则，打印不含重复数字的列表。
- Q8. 编写一个程序，交换两个矩阵 `A` 和 `B` 的内容。
- Q9. 编写一个程序，在矩阵中插入值；将此矩阵传递给一个函数，该函数返回矩阵的范数。范数定义为矩阵中所有元素的平方和的平方根。
- Q10. 编写一个程序，输入一个 `M × N` 数组。将此数组的内容按升序排序，并将其存储在另一个数组中。
- Q11. 编写一个程序，输入一个 `M × N` 数组。找出所有输入数字的平均值。

## 10 C 语言中的字符串

### 目标

- 描述字符串
- 作为字符串的字符数组
- 初始化字符串
- 显示字符串
- 操作字符串
- 实现字符串数组

我们在第 9 章中已经提到，数组是一种用于存储具有相同数据类型元素的

数据结构。数组的元素按顺序存储，一个接一个。这种排列方式被称为连续内存分配。

到目前为止，数组一直用于存储数字数据，如年龄、分数和身高。

在实际场景中，我们需要存储诸如人名或城市名等数据。数字数组

在这种情况下不起作用，因此需要字符数组。在本章中，我们将学习什么是字符串，

如何定义字符数组，以及如何从字符数组中存储和检索数据。

我们还将学习如何对字符数组执行各种操作。

### 10.1 字符串

一般意义上，字符串一词指的是一系列代表某个实体（如名称）的字符。

大多数编程语言提供了字符串的逻辑实现。

提供逻辑实现而非物理实现的原因在于字符串的特性。

几乎所有在程序中使用的字符串都是可变长度的字符；

因此，将字符串存储在固定长度的数据类型中很困难。

例如，如果我们想存储城市名称，如 Ahmedabad 或 Mumbai，

那么这两个字符串使用的字符数量是不同的。

由于字符串的这一可变属性，大多数语言允许不同格式的字符串。

图 1 展示了不同格式的字符串及其示例：

![图 1：字符串格式](img/5d422ba7108ffdf64376be51eaf0c459_217_0.png)

从图 1 中可以看出，在所有字符串格式中，都需要一个额外的字符。

对于固定长度的字符串，我们需要指定一个定界符来标识字符串的结尾。
