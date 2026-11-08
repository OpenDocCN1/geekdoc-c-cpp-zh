
### 5.7.2 两个矩阵的乘法

```c
#include<stdio.h>
int main()
{
    int a[5][5],b[5][5],c[5][5],m,n,p,q,i,j,k;
    printf("Enter rows and columns of first matrix:");
    scanf("%d%d",&m,&n);
    printf("Enter rows and columns of second matrix:");
    scanf("%d%d",&p,&q);
    if(n==p)
    {
        printf("\nEnter first matrix:\n");
        for(i=0;i<m;++i)
            for(j=0;j<n;++j)
                scanf("%d",&a[i][j]);
        printf("\nEnter second matrix:\n");
        for(i=0;i<p;++i)
            for(j=0;j<q;++j)
                scanf("%d",&b[i][j]);
        printf("\nThe new matrix is:\n");
        for(i=0;i<m;++i)
        {
            for(j=0;j<q;++j)
            {
                c[i][j]=0;
                for(k=0;k<n;++k)
                    c[i][j]=c[i][j]+(a[i][k]*b[k][j]);
                printf("%d ",c[i][j]);
            }
            printf("\n");
        }
    }
    else
    printf("\nSorry!!!! Matrix multiplication can't be done");
    return 0;
}
```

**输出：**

```
Enter rows and columns of first matrix:3
3
Enter rows and columns of second matrix:3
3
Enter first matrix:
1 2 3
4 5 6
7 8 9
Enter second matrix:
9 8 7
6 5 4
3 2 1
The new matrix is:
30 24 18
84 69 54
138 114 90
```

### 5.7.3 打印矩阵的转置

```c
#include<stdio.h>
int main()
{
        int a[5][5],i,j,m,n;
        printf("How many rows?");
        scanf("%d",&n);
        printf("How many columns?");
        scanf("%d",&m);
        printf("\nEnter the matrix:\n");
        for(i=0;i<m;++i)
                for(j=0;j<n;++j)
                        scanf("%d",&a[i][j]);
        printf("\nTranspose of given matrix:\n");
        for(i=0;i<m;++i)
        {
                for(j=0;j<n;++j)
                        printf("%d ",a[j][i]);
                printf("\n");
        }
        return 0;
}
```

**输出：**

```
How many rows?3
How many columns?3
Enter the matrix:
1 2 3
4 5 6
7 8 9
Transpose of given matrix:
1 4 7
2 5 8
3 6 9
```

### 5.7.4 检查矩阵的对称性

用于检查矩阵是否对称的 C 程序：我们先求矩阵的转置，然后将其与原矩阵比较。对于对称矩阵，A^T = A。

```c
#include<stdio.h>
int main()
{
    int m, n, c, d, matrix[10][10], transpose[10][10];
    printf("Enter the number of rows and columns of matrix\n");
    scanf("%d%d", &m, &n);
    printf("Enter elements of the matrix\n");
    for (c = 0; c < m; c++)
        for (d = 0; d < n; d++)
            scanf("%d", &matrix[c][d]);
    for (c = 0; c < m; c++)
        for (d = 0; d < n; d++)
            transpose[d][c] = matrix[c][d];
    if (m == n) /* check if order is same */
    {
        for (c = 0; c < m; c++)
        {
            for (d = 0; d < m; d++)
            {
                if (matrix[c][d] != transpose[c][d])
                    break;
            }
            if (d != m)
                break;
        }
        if (c == m)
            printf("The matrix is symmetric.\n");
        else
            printf("The matrix isn't symmetric.\n");
    }
    else
        printf("The matrix isn't symmetric.\n");
    return 0;
}
```

### 5.7.5 检查上三角矩阵

```c
#include <stdio.h>
int main()
{
        int i,n,flag = 0, mat[n][n];
        printf("Enter the value of n");
        scanf("%d",&n);
        int j;
        for(i = 0; i < n; i++)
        {
                for(j = 0; j < n; j++)
                        scanf("%d",&mat[i][j]);
        }
        for (i = 1; i < n; i++)
                for (j = 0; j < i; j++)
                        if (mat[i][j] != 0)
                                flag = 0;
                        else
                                flag = 1;
        if (flag == 1)
                printf("Upper Triangular Matrix");
        else
                printf("Not an Upper Triangular Matrix");
        return 0;
}
```

### 5.7.6 检查下三角矩阵

```c
#include <stdio.h>
int main()
{
        int i,n,flag = 0, mat[n][n];
        printf("Enter the value of n");
        scanf("%d",&n);
        int j;
        for(i = 0; i < n; i++)
        {
                for(j = 0; j < n; j++)
                scanf("%d",&mat[i][j]);
        }
        for (i = 1; i < n; i++)
        for (j = i+1; j < i; j++)
                if (mat[i][j] != 0)
                        flag = 0;
                else
                        flag = 1;
        if (flag == 1)
                printf("Upper Triangular Matrix");
        else
                printf("Not an Upper Triangular Matrix");
        return 0;
}
```

## 5.8 字符串简介

### 5.8.1 定义

在 C 编程中，字符数组称为字符串。字符串以空字符 '\0' 结尾。字符串实际上是一维字符数组。字符串总是用双引号括起来。而在 C 中，字符用单引号括起来。

### C 字符串示例

```c
char string[15] = {'s', 'h', 'r', 'u', 't', 'k', 'i', 'r', 't', 'i', '\0'};
char string[15] = "shrutikrti";
char string []   = "shrutikrti";
```

上述声明之间的区别在于：当我们将 char 声明为 "string[20]" 时，会分配 20 字节的内存空间来保存字符串值。当我们将 char 声明为 "string[]" 时，内存空间将在程序执行期间根据需求分配。

C 语言中的字符串简单来说就是字符数组。字符串必须在最后一个字符之后有一个 NULL 或 \0 字符，以表明字符串结束的位置。字符串可以声明为字符数组，也可以使用字符串指针声明。首先我们来看一个字符数组示例：

```c
char mystr[15];
```

如你所见，字符数组的声明方式与普通数组相同。这个数组只能容纳 14 个字符，因为我们必须为 NULL 字符留出空间。

```c
#include <stdio.h>
int main()
{
    char name[15];
    printf("Enter name: ");
    scanf("%s", name);
    printf("Your name is %s.", name);
    return 0;
}
```

**输出：**

```
Enter name
Shrutkirti
Your name is Shrutkirti
```

### 5.8.2 声明

声明字符串就像声明一维数组一样简单。下面是声明字符串的基本语法。

```c
char str_name[size];
```

在上述语法中，str_name 是为字符串变量指定的任意名称，size 用于定义字符串的长度，即字符串将存储的字符数。请记住，还有一个额外的终止字符，即空字符（'\0'），用于表示字符串的终止，这正是字符串与普通字符数组的不同之处。

### 5.8.3 初始化

考虑下面的声明和初始化，它创建一个由单词 "Program" 组成的字符串。为了在数组末尾保存空字符，包含该字符串的字符数组的大小比单词 "Program" 中的字符数多一。

```c
char word[8] = {'P', 'r', 'o', 'g', 'r', 'a', 'm', '\0'};
```

上述数组也可以按如下方式初始化

```c
char word[] = "Program";
```

### 内存中会发生什么？

| 索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| 数组 | P | r | o | g | r | a | m | \0 |
| 内存地址 | 7890 | 7891 | 7892 | 7893 | 7894 | 7895 | 7896 | 7897 |

图 5.6：字符数组的内容

当在数组中初始化字符串时，空字符会自动将 \0 字符放在字符串末尾。

示例：

```c
void main()
{
    char word[8] = {'P', 'r', 'o', 'g', 'r', 'a', 'm', '\0'};
    printf("Message = %s", word );
}
```

**输出：**

Message = Program

## 5.9 标准库函数

C 语言本身不提供对字符串的显式支持。字符串处理函数在库中实现。字符串 I/O 操作在 `<stdio.h>`（puts、gets 等）中实现。一组简单的字符串操作函数在 `<string.h>` 中实现，或在某些系统上在 `<strings.h>` 中实现。

在 C 编程中，有一个单独的头文件用于处理字符串，名为 "string.h"。它提供了大量操作以空字符结尾的字符串的函数。

### strcpy() 函数

这个库函数用于复制字符串，可以这样使用：strcpy(destination, source)。（在 C 中不能这样做：string1 = string2）。请看下面的示例：

```c
str_one = "shruit";
str_two = "kirti";
strcpy(str_one, str_two); // str_one becomes "kirti"
```

**注意：** strcpy() 不会执行任何边界检查，因此存在越界访问字符串的风险。

### strcmp() 函数

这个库函数用于比较两个字符串，可以这样使用：strcmp(str1, str2)。

- 如果第一个字符串大于第二个字符串，则返回一个大于 null 的数。
- 如果第一个字符串小于第二个字符串，则返回一个小于 null 的数。
- 如果第一个字符串和第二个字符串相等，则返回 null。

