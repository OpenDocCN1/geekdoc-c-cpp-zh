

```
printf("\nThe reversed array is : ");
for(i = n ; i >= 1 ; i--)
    printf("%2.2f", a[i]);
}
```

> 程序显示以下输出
> 输入限制：5
> 输入元素：9 7 6 3 2
> 反转后的数组是：2.00 3.00 6.00 7.00 9.00

### 程序 A3：

编写一个程序，查找数组中最小的数及其位置。

```c
/* smallpos.c */
#include<stdio.h>
void main()
{
    int a[10], i, n, s = 0, pos = 0;
    printf("Enter the limit : ");
    scanf("%d", &n);
    printf("Enter the elements : ");
    for(i = 0 ; i < n ; i++)
        scanf("%d", &a[i]);
    s = a[0];
    for(i = 0 ; i < n ; i++)
    {
        if(a[i] < s)
        {
            s = a[i];
            pos = i;
        }
    }
    printf("The smallest number is %d", s);
    printf("\nIts position is %d", pos+1);
}
```

> 程序显示以下输出
> 输入限制：4
> 输入元素：67 5 74 987
> 最小的数是 5
> 其位置是 2

### 程序 A4：

编写一个程序，仅显示数组中的负数元素。

```c
/* negative.c */
#include<stdio.h>
void main()
{
    int i, num, neg[25];
    printf("Enter the limit : ");
    scanf("%d", &num);
    printf("Enter the elements : ");
    for(i = 0 ; i < num ; i++)
        scanf("%d", &neg[i]);
    printf("The negative elements are : ");
    for (i = 0 ; i < num ; i++)
    if(neg[i] < 0)
    {
        printf( "%d", neg[i]);
        continue;
    }
    printf("\n");
}
```

> 程序显示以下输出
> 输入限制：5
> 输入元素：-5 -4 3 -2 -1
> 负数元素为：-5 -3 -1

### 程序 A5：

编写一个程序，使用数组生成斐波那契数列。

```c
/* Fiboarr.c */
#include <stdio.h>
void main()
{
    int i, n, fib[30];
    printf("Enter the limit : ");
    scanf("%d", &n);
    fib[0] = 0;
    fib[1] = 1;
    for(i = 2; i < n; i++)
    fib[i] = fib[i-1] + fib[i-2];
    printf("The fibonacci series is : ");
    for(i = 0; i < n; i++)
    printf("%d ", fib[i]);
}
```

> 程序显示以下输出
> 输入限制：8
> 斐波那契数列为：0 1 1 2 3 5 8 13

## 1.19 矩阵程序

### 程序 M1：

编写一个程序，计算矩阵中所有元素的和。

```c
/* summat.c */
#include<stdio.h>
void main()
{
int a[10][10], i, j, m, n, sum = 0;
printf("Enter the order of matrix : ");
scanf("%d %d", &m, &n);
printf("Enter the elements of matrix : ");
for(i = 0 ; i < m ; i++)
for(j = 0 ; j < n ; j++)
scanf("%d", &a[i][j]);
for(i = 0 ; i < m ; i++)
for(j = 0 ; j < n ; j++)
sum = sum + a[i][j];
printf("Sum of elements of the matrix is %d", sum);
}
```

程序显示以下输出

```
Enter the order of matrix : 2 2
Enter the elements of matrix : 1 1 1 1
Sum of elements of the matrix is 4
```

### 程序 M2：

编写一个程序，判断矩阵是否对称。对称意味着原始矩阵中的元素与其转置矩阵中的元素必须相同。

```c
/* symetric.c */
#include<stdio.h>
void main()
{
int i, j, row, column, mat[10][10], trans[10][10];
printf("Enter the order of matrix : ");
scanf("%d %d", &row, &column);
if (row != column)
{
printf("The given matrix cannot be symmetric");
exit(0);
}
printf("Enter the elements in row wise \n");
for(i = 0 ; i < row ; i++)
for(j = 0 ; j < column ; j++)
{
    scanf("%d", &mat[i][j]);
    trans[j][i] = mat[i][j];
}
for(i = 0 ; i < row ; i++)
for(j = 0 ; j < column ; j++)
if(mat[i][j] != trans[i][j])
{
    printf("The given matrix is not symmetric");
    exit(0);
}
printf("The given matrix is symmetric");
}
```

| 运行 | 输出 |
| --- | --- |
| RUN1 | 输入矩阵阶数：3 3\n按行输入元素\n1 1 1\n1 1 1\n1 1 1\n给定矩阵是对称的 |
| RUN2 | 输入矩阵阶数：3 3\n按行输入元素\n1 2 3\n1 2 3\n1 2 3\n给定矩阵不是对称的 |
| RUN3 | 输入矩阵阶数：3 4\n给定矩阵不能是对称的 |

### 程序 M3：

编写一个程序，减去两个矩阵。

```c
/* sub_mat.c */
#include<stdio.h>
void main()
{
    int a[3][3], b[3][3], c[3][3];
    int i, j;
    printf("Enter the elements of matrix 1 \n");
    for(i = 0 ; i < 3 ; i++)
    for(j = 0 ; j < 3 ; j++)
    scanf("%d", &a[i][j]);
    printf("Enter the elements of matrix 2 \n");
    for(i = 0 ; i < 3 ; i++)
    for(j = 0 ; j < 3 ; j++)
    scanf("%d", &b[i][j]);
    for(i = 0 ; i < 3 ; i++)
    for(j = 0 ; j < 3 ; j++)
        c[i][j] = a[i][j] - b[i][j];
    printf("\n Result of matrix subtraction is \n");
    for(i = 0 ; i < 3 ; i++)
    {
        for(j = 0 ; j < 3 ; j++)
            printf("\n%d ", c[i][j]);
        printf("\n");
    }
}
```

> 程序显示以下输出
>
> 输入矩阵 1 的元素
> 11  13  15  17  19      21  23  25  27
>
> 输入矩阵 2 的元素
> 1   3   5   7   9       21  23  25  27
>
> 矩阵减法结果为
> 10  10  10  10
> 10  10  10  0
> 0   0   0   0

### 程序 M4：

编写一个程序，计算两个矩阵的乘积。

```c
/* mulmat.c */
#include<stdio.h>
void main()
{
    int a[5][5], b[5][5], c[5][5], i, j, k, m, n, p, q;
    printf("%d %d", &m, &n);
    printf("Enter the order of matrix 1 : ");
    scanf("%d %d", &m, &n);
    printf("Enter the order of matrix 2 : ");
    scanf("%d %d", &p, &q);
    if(n == p)
    /* if column of matrix 1 is equal to the row of matrix 2 */
    {
    printf("Enter the elements of matrix 1 \n");
    for(i = 0 ; i < m ; i++)
    for(j = 0 ; j < n ; j++)
    scanf("%d", &a[i][j]);
    printf("Enter the elements of matrix 2 \n");
    for(i = 0 ; i < p ; i++)
    for(j = 0 ; j < q ; j++)
    scanf("%d", &b[i][j]);
    for(i = 0 ; i < m ; i++)
    for(j = 0 ; j < q ; j++)
    {
        c[i][j] = 0;
        for(k = 0 ; k < p ; k++)
            c[i][j] = c[i][j] + a[i][k] * b[k][j];
    }
    }
    else
        printf("Matrix multiplication is invalid");
        printf("Result of matrix multiplication is \n");
        for(i = 0 ; i < m ; i++)
        {
            for(j = 0 ; j < q ; j++)
                printf("%d \t", c[i][j]);
            printf("\n");
        }
}
```

> 程序显示以下输出
> 运行 1 输入矩阵 1 的阶数：3 3
> 输入矩阵 2 的阶数：3 3
> 输入矩阵 1 的元素
> 1 3 5 7 9 11 21 23 25
> 输入矩阵 2 的元素
> 25 23 21 11 9 7 5 3 1
> 矩阵乘法结果为
> 83 65 47
> 329 275 221
> 903 765 627
> 运行 2 输入矩阵 1 的阶数：1 2
> 输入矩阵 2 的阶数：3 4
> 矩阵乘法无效

### 程序 M5：

编写一个程序，计算矩阵的行列式。

```c
/* determinant.c */
#include<stdio.h>
void main()
{
float a[10][10], det, ratio;
int i, j, k, n;
printf("Enter the order of matrix : ");
scanf("%d", &n);
printf("Enter the elements of matrix \n");
for(i = 1 ; i <= n ; i++)
for(j = 1 ; j <= n ; j++)
scanf("%f", &a[i][j]);
for(k = 1 ; k <= n-1 ; k++)
{
    for(i = k+1 ; i <= n ; i++)
    {
        ratio = a[i][k]/a[k][k];
        for(j = 1 ; j <= n ; j++)
            a[i][j] = a[i][j] - ratio * a[k][j];
    }
}
det = 1.0;
for(i = 1 ; i <= n ; i++)
    det = det * a[i][i];
printf("The determinant of the matrix is %.3f", det);
}
```

程序显示以下输出
运行 1 输入矩阵阶数：3
输入矩阵元素
9 8 7
6 5 4
3 2 1
矩阵的行列式是 0.000
运行 2 输入矩阵阶数：3
输入矩阵元素
9 9 9
6 5 4
12 36 4
矩阵的行列式是 504.000

## 1.20 总结

C 是由丹尼斯·里奇开发的一种通用结构化编程语言。

标识符是由字母数字字符组成的字符串，以字母字符或下划线字符开头，用于标识或命名各种编程元素，如变量、函数、数组、结构体、联合体等。

关键字是 C 编译器中已定义具有固定含义的单词。它们只能用于其预定义的目的，不能用作用户定义的变量。

语言支持的数据类型决定了该语言可以处理的值的类型。基本数据类型为 char、int、float 和 double。

类型定义允许用户定义与现有数据类型等效的新数据类型。

