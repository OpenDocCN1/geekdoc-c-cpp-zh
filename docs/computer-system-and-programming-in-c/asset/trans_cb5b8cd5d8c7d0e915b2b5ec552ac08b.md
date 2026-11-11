
这个二维数组也可以看作是由多个一维数组组成的一维数组。该数组的另一种视图如下：

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_214_0.png)

这个二维数组可以看作一个有40个元素的一维数组，其中每个元素是一个包含14个值的数组。

## 访问二维数组元素

在 labScores 示例中，假设我们希望表示第二个学生（对应第 1 行）在第 10 次实验（对应第 9 列）中得了 90 分。我们可以使用如下语句：

`labScores[1][9] = 90;`

数组下标可以是整数常量（如上述示例）、变量或表达式。它们应在数组的边界范围内。

## 二维数组初始化

我们可以按如下方式声明并初始化一个数组 A：

```c
//declaration
int A[3][4] = {{8, 2, 6, 5}, //row 0
               {6, 3, 1, 0}, //row 1
               {8, 7, 9, 6}}; //row 2
```

该数组的内存布局可以如下所示：

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_214_1.png)

## 编程问题

### 问题 1

编写一个程序，输入一个 3*3 矩阵，并以矩阵形式打印其中的元素。

**解答**

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a[3][3],i,j;
    clrscr();
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            printf("\n enter the element");
            scanf("%d",&a[i][j]);
        }
    }
    printf("\n the matrix is");
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            printf("\t%d",a[i][j]);
        }
        printf("\n");
    }
    getch();
}
```

### 问题 2

编写一个程序，输入两个 3*3 矩阵，并打印两个矩阵的和。

**解答**

通常的矩阵加法定义在两个维度相同的矩阵上。两个 *m* 行 *n* 列矩阵 A 和 B 的和，记为 A + B，仍是一个 *m* 行 *n* 列矩阵，通过将对应元素相加得到。例如：如果我们要将以下矩阵相加：

$$
\begin{bmatrix}0 & 1 & 2\\9 & 8 & 7\end{bmatrix}
+
\begin{bmatrix}6 & 5 & 4\\3 & 4 & 5\end{bmatrix}
$$

将对应的元素逐对相加，并化简得到最终结果：

$$
\begin{bmatrix}0+6 & 1+5 & 2+4\\9+3 & 8+4 & 7+5\end{bmatrix}
=
\begin{bmatrix}6 & 6 & 6\\12 & 12 & 12\end{bmatrix}
$$

## 课程核心

本课程旨在帮助学员掌握人工智能的基本概念、核心技术及实际应用场景，通过理论与实践相结合的方式，培养学员解决实际问题的能力。

- 第一章：人工智能导论
- 第二章：机器学习基础
- 第三章：深度学习与神经网络
- 第四章：自然语言处理
- 第五章：计算机视觉
- 第六章：强化学习

| 章节 | 课时 | 难度 |
|------|------|------|
| 第一章 | 4 | 低 |
| 第二章 | 6 | 中 |
| 第三章 | 8 | 高 |
| 第四章 | 6 | 中 |
| 第五章 | 6 | 中 |
| 第六章 | 4 | 高 |

> 人工智能不仅是一种技术，更是一种改变世界的思维方式。

```c
scanf("%d",&a[i][j]);
}
printf("\n enter elements of the second Matrix:\n");
for(i=0;i< p;i++)
{
    for(j=0;j< q;j++)
        scanf("%d",&b[i][j]);
}
printf("The first matrix is:\n");
for(i=0;i< m;i++)
{
    for(j=0;j< n;j++)
        printf("%d ",a[i][j]); //print the first matrix
    printf("\n");
}
printf("The second matrix is:\n");
for(i=0;i< p;i++)
{
    for(j=0;j< q;j++)
        printf("%d ",b[i][j]);
    printf("\n");
}
if(n!=p)
{
    printf("Aborting!!!!!!\n multiplication of the above matrices not feasible.");
    exit(0);
}
else
{
    for(i=0;i< m;i++)
    {
        for(j=0;j< q;j++)
        {
            c[i][j] = 0;
            for(k=0;k< n;k++)
            {
                c[i][j] = c[i][j] + a[i][k] * b[k][j];
            }
        }
    }
    printf("\n multiplication of the above two matrices are:\n\n");
    for(i=0;i< m;i++)
    {
        for(j=0;j< q;j++)
            printf("\t%d ",c[i][j]);
    }
    printf("\n");
}
getch();
}
```

### 问题 4

编写一个程序，输入一个矩阵，并打印该矩阵的转置。

**解答**

转置矩阵是将给定矩阵的所有行变为列、所有列变为行所得到的矩阵。矩阵 A 的转置记作 Aᵀ。

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_216_0.png)

用 C 语言编写的程序如下：

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a[3][3],i,j;
    clrscr();
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            printf("\n enter the element");
            scanf("%d",&a[i][j]);
        }
    }
    printf("\n the transpose of the matrix is");
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            printf("\t%d",a[j][i]);
            printf("\n");
        }
    }
    getch();
}
```

## 三维数组

C 语言允许使用超过二维的数组，其维数上限取决于编译器。

多维数组的一般形式为

**type array_name[s1][s2][s3]...[sm];**

任何数组的元素总数都是声明中包含的所有大小（维度）的乘积。因此，它等于 `s1*s2*s3*...*sm`。

对于大多数应用，二维数组就足够了。在一般应用中，三维是你可以预见的最高维度。在科学计算、天气预报、时空分析等领域，还需要更高维的数组。

## 数组的动态分配，或未知/可变大小数组

如果我们想要动态分配内存，就必须使用数组动态分配的概念。

### 固定大小数组的问题

声明一个固定大小的数组（如 `int a[10000];`）存在两个典型问题：

- **超出上限。** 选择一个真正的上限通常是不可行的，因为程序员无法控制用户感兴趣的数据集大小。错误地假设最大值永远不会被超出，是许多编程错误的根源。声明非常大的数组会极度浪费内存，而且如果这样的数组很多，可能导致程序在某些系统中无法运行。
- **无法扩展。** 对于典型的数据集，使用较小的尺寸可能更高效，但会阻止程序处理更大的数据集。如果不检查数组边界，大数据集将越过数组末尾，造成灾难性后果。固定大小的数组无法按需扩展。

通过动态分配合适大小的数组，或在数组需要扩展时重新分配内存，可以避免这些问题。这两种操作都是通过将数组声明为指针，并使用 malloc/calloc 函数分配内存，再用 `free` 函数释放不再需要的内存来实现的。

该主题的详细信息将在指针章节中讨论。

## 向函数传递数组

我们可以将一维数组和多维数组传递给函数。我们将逐一讨论这些概念。

### 一维数组

有时，调用一个需要很长的参数列表的函数很不方便。

一种解决方法是将变量收集到一个数组中，然后向函数传递一个指向该数组的**指针**。这种方法将在指针部分非常详细地描述，但现在你需要知道，实际上传递给函数的并不是数组本身，而只是数组在内存中的位置。这被称为**按引用传递**。数组名引用的是数组在内存中的位置，即其**地址**。

如果我们写 `int max(int *)` 或 `int max(int[])`，这两行的含义是：`max` 是一个函数，我们在其中传递整型指针，即整个数组，并根据该数组返回一个整型变量。

### 编程问题

### 问题 1

编写一个程序，输入 5 个数字，并借助函数打印这 5 个数字的和。

**解答**

```c
#include <stdio.h>
int addNumbers(int fiveNumbers[]); /* declare function */
void main()
{
    int array[5];
    int i;
    printf("Enter 5 integers separated by spaces: ");
    for(i=0; i<5; i++)
    {
        scanf("%d", &array[i]);
    }
    printf("\n their sum is: %d\n", addNumbers(array));
    return 0;
}
int addNumbers(int fiveNumbers[])
/* define function */
{
    int sum = 0;
    int i;
    for(i=0 ; i<5 ; i++) {
        sum+=fiveNumbers[i]; /* work out the total */
    }
    return sum; /* return the total */
}
```

请注意，我在函数声明和定义中都留空了数组的大小——编译器会为你计算出来。另外，当我在 C 语言中调用该函数时，我传递的是数组名。这相当于传递 `&array[0]`——第一个元素的地址。稍后你将学习取地址运算符。

### 问题 2

编写一个程序，输入 10 个数字，并借助函数打印其中的最大数。

**解答**

```c
#include<stdio.h>
#include<conio.h>
int max(int []);
void main()
{
    int a[10],i,m;
    clrscr();
    for(i=0;i<10;i++)
    {
        printf("\n enter the value of a[%d]",i);
        scanf("%d",&a[i]);
    }
    m=max(a);
    printf("\n The maximum number is %d",m);
    getch();
}
int max(int p[])
{
    int m,i;
    m=p[0];
    for(i=1;i<10;i++)
    {
        if(m<p[i])
            m=p[i];
    }
    return(m);
}
```

## 多维数组

这与传递一维数组类似，但在函数声明中，你必须指定所有维度的大小（但最左边的一个是可选的）。下面的程序演示了如何将多维数组传递给函数。

```c
#include <stdio.h>
void printArray(int array[][4]); /* declare function */
void main()
{
    int array[3][4] = {0,1,2,3,4,5,6,7,8,9,10,11};
    printArray(array);
}

void printArray(int array[][4])
/* define function */
{
    int i, j;
    for(i=0 ; i<3 ; i++) {
        for(j=0 ; j<4 ; j++)
            printf("%2d ", array[i][j]);
    }
    printf("\n");
}
```

## 小结

- 数组是相同数据类型元素的集合，并拥有一个共同的名字。
- 数组可分为以下类别：（a）一维数组 （b）多维数组。
- 如果我们要以矩阵形式存储数据，就必须使用二维数组的概念。
- 数组在计算机编程中起着非常重要的作用。
- 我们可以借助指针将数组传递给函数。

