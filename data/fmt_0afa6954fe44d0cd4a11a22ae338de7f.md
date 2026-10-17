
```c
#define MAXGIRLS 4
#define MAXITEMS 3
main() {
    int value[MAXGIRLS][MAXITEMS];
    int girl_total[MAXGIRLS],  item_total[MAXITEMS];
    int i, j, grand_total;
    /*READING OF VALUES AND COMPUTING girl_total ...*/
    printf("Enter data:\n");
    printf("Enter values, one at a time, row-wise\n\n");
    for (i = 0; i < MAXGIRLS; i++) {
        girl_total[i] = 0;
        for (j = 0; j < MAXITEMS; j++) {
            scanf("%d", &value[i][j]);
            girl_total[i] = girl_total[i] + value[i][j];
        }
    }
    /*COMPUTING item_total .......*/
    for (j = 0; j < MAXITEMS; j++) {
        item_total[j] = 0;
        for (i = 0; i < MAXGIRLS; i++) {
            item_total[j] = item_total[j] + value[i][j];
        }
    }
    /*COMPUTING grand_total.......*/
    grand_total = 0;
    for (i = 0; i < MAXGIRLS; i++) {
        grand_total = grand_total + girl_total[i];
    }
    /*PRINTING RESULTS.......*/
    printf("\nGLS TOTALS\n");
    for (i = 0; i < MAXGIRLS; i++) {
        printf("Sales[%d] = %d\n", i+1, girl_total[i]);
    }
    printf("\nITEMS TOTALS\n");
    for (j = 0; j < MAXITEMS; j++) {
        printf("Item[%d] = %d\n", j+1, item_total[j]);
    }
    printf("\nGrand Total = %d\n", grand_total);
}
```

## 数组 207

## 程序输出

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | 5 |
| 2 | 2 | 4 | 6 | 8 | 10 |
| 3 | 3 | 6 | 9 | 12 | 15 |
| 4 | 4 | 8 | 12 | 16 | 20 |
| 5 | 5 | 10 | 15 | 20 | 25 |

**图 7.6** 使用二维数组打印乘法相表的程序

## 7.6 初始化二维数组

与一维数组一样，二维数组可以通过在声明后紧跟一个大括号括起来的值列表来初始化。例如

```c
int table[2][3] = {0,0,0, {1,1,1}};
```

这会将第一行的元素初始化为零，第二行初始化为一。上面的语句可以等效地写为

```c
int table[2][3] = {{0,0,0}, {1,1,1}};
```

也可以按照如下所示矩阵的形式初始化二维数组：

注意上述语句的语法。在每个关闭行的的大括号后面，都需要一个逗号，但最后一行除外。当数组用所有值完全初始化时，我们不需要指定第一维。即该语句：

```c
int table[][] = {{0,0,0}, {1,1,1}};
```

如果初始化列表中缺少值，它们将被自动设置为零。例如，该语句将第一行的第一个元素初始化为零，第二行的第一个元素初始化为一，而所有其他元素都初始化为零。当所有元素都要初始化为零时，可以使用以下简捷方法

```c
int m[3][5] = {(0,0), (0,0), {0}};
```

每行的第一个元素被显式初始化为零，而所有其他元素自动初始化为零。以下语句将实现相同的结果：

```c
int m[3][5] = {0,0};
```

对四种汽车（大使号 Ambassador、菲特 Fiat、海豚 Dolphin 和马鲁蒂 Maruti）的受欢迎程度在四个城市（孟买 Bombay、加尔各答 Calcutta、德里 Delhi 和马德拉斯 Madras）进行了调查。每个受访者都被要求提供所在的城市和使用的汽车类型。使用这些结果，制表所示：

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| M | 1 | 2 | 1 | 2 | 4 |
| C | 1 | 3 | 4 | 2 | 3 |
| D | 4 | 4 | 1 | 1 | 3 |
| C | 1 | 1 | 2 | 4 | 4 |
| D | 1 | 2 | 3 | 1 | 1 |
| D | 3 | 4 | 1 | 2 | 3 |

代码代表以下信息：

![](img/177eacb192165f90062789304bda281_219_0.png)

- M - Madras (马德拉斯) 1 - Ambassador (大使号)
- D - Delhi (德里) 2 - Fiat (菲特)
- C - Calcutta (加尔各答) 3 - Dolphin (海豚)
- B - Bombay (孟买) 4 - Maruti (马鲁蒂)

编写一个程序生成显示四个城市汽车受欢迎程度的表格。使用二维数组 `frequency` 作为累加器，存储每个城市各种类别下的汽车数量。例如，`frequency[][]` 表示在城市 `i` 使用的 `j` 类型汽车的数量。频率被声明为大小为 5x5 的数组，所有元素初始化为零。

图 7.7 所示的程序从终端逐一组读取城市代码和汽车代码。当读取到字母 X 代替城市代码时，制表结束。

```c
main()
{
    int i, j, car;
    int frequency[5] = { (0),(0),(0),(0),(0) };
    char city;
    printf("对于每一个人，输入城市代码 \n");
    printf("随后输入汽车代码。\n");
    printf("输入字母 X 表示结束。\n");
    /* . . 制表开始 . . . . . */
    for (i = 1; i < 100; i++) {
        scanf(" %c", &city);
        if (city == 'X')
            break;
        scanf("%d", &car);
        switch(city) {
            case 'B': frequency[1][car]++;
                break;
            case 'C': frequency[2][car]++;
                break;
            case 'D': frequency[3][car]++;
                break;
            case 'M': frequency[4][car]++;
                break;
        }
    }
    /* . . 制表完成并开始打印. . . . . */
    printf("\n");
    printf("受欢迎程度表\n");
    printf("----------------\n");
    printf("City | Ambassador | Fiat | Dolphin | Maruti \n");
    for (i = 1; i < 4; i++) {
        printf("%d | %d | %d | %d | %d\n", i, frequency[i][1], frequency[i][2], frequency[i][3], frequency[i][4]);
    }
}
```

输出：

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| M | 1 | 2 | 1 | 2 | 4 |
| C | 1 | 3 | 4 | 2 | 3 |
| D | 4 | 4 | 1 | 1 | 3 |
| C | 1 | 1 | 2 | 4 | 4 |
| D | 1 | 2 | 3 | 1 | 1 |
| D | 3 | 4 | 1 | 2 | 3 |
| City | Ambassador | Fiat | Dolphin | Maruti |
|---|---|---|---|---|
| Bombay | 2 | 1 | 3 | 2 |
| Calcutta | 4 | 5 | 1 | 0 |
| Delhi | 2 | 1 | 3 | 2 |
| Madras | 4 | 1 | 1 | 4 |

![](img/177eacb192165f90062789304bda281_221_0)

## 数组 211

## 内存布局

二维数组定义中的下标表示行和列。这种格式映射了数据在内存中的布局方式。所有数组元素连续存储在一个列表中。如果我们认为内存左侧为低地址，右侧为高地址，则简单数组的第一个元素在左侧，最后一个在右侧。同样，二维数组按行存储，将每行视为一个简单数组。如下所示：

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| row 0 | [0][0] | [0][1] | [0][2] | [1][0] | [1][1] | [1][2] | [2][0] | [2][1] | [2][2] | |
| row 1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | |
| row 2 | 7 | 8 | 9 | | | | | | |

对于多维数组，存储顺序是：第一个元素的所有下标均为 0，第二个元素除最右侧外的所有下标均为 1，以此类推。一个 2x3x3 数组的元素存储如下：

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 000 | 001 | 002 | 010 | 011 | 012 | 020 | 021 | 022 |
| 1 | 100 | 101 | 102 | 110 | 111 | 112 | 120 | 121 | 122 |

最右侧首先增加，其他下标从右向左增加。序号 1, 2, ..., 18 代表该元素在列表中的位置。

## 程序 7.7

图 7.8 中的程序展示了如何相乘两个 NxN 矩阵。

```c
#include<stdio.h>
#include<conio.h>
void main() {
    int a1[10][10], a2[10][10], c[10][10], i, j, k, a, b;
    clrscr();
    printf("输入方阵的大小\n");
    scanf("%d", &a);
    printf("你需要按行输入矩阵元素\n");
    for(i=0; i<a; i++)
    {
        for(j=0; j<b; j++)
        {
            printf("\n输入第一个矩阵的下一个元素=\n");
            scanf("%d", &a1[i][j]);
        }
    }
    for(i=0; i<a; i++)
    {
        for(j=0; j<b; j++)
        {
            printf("\n输入第二个矩阵的下一个元素=\n");
            scanf("%d", &a2[i][j]);
        }
    }
    printf("\n输入的矩阵为\n");
    for(i=0; i<a; i++)
    {
        for(j=0; j<b; j++)
        {
            printf("\n");
            printf("%d ", a1[i][j]);
        }
    }
    printf("\n");
    for(i=0; i<a; i++)
    {
        for(j=0; j<b; j++)
        {
            printf("\n");
            printf("%d ", a2[i][j]);
        }
    }
    printf("\n两个矩阵的积为\n");
    for(i=0; i<a; i++)
    {
        for(j=0; j<b; j++)
        {
            c[i][j] = 0;
            for(k=0; k<a; k++)
                c[i][j] = c[i][j] + a1[i][k]*a2[k][j];
        }
    }
    for(i=0; i<a; i++)
    {
        printf("%d\n", i);
        for(j=0; j<b; j++)
        {
            printf("%sd", c[i][j]);
        }
    }
    getch();
}
```

# 格拉-希尔出版公司

214 ANSI C编程

第 9步 - i = i + 1

第 10步 - 显示 b[][] 为矩阵 a[][] 的转置

第 11步 - 停止

流程图

```c
Program
#include <stdio.h>
#include <conio.h>
void main() {
    int i,j,a[3][3],b[3][3];
    clrscr();
    printf("Enter a 3 X 3 matrix:\n");
    for(i=0;i<3; i++) {
        for(j=0;j<3; j++) {
            scanf("%d", &a[i][j]);
        }
    }

    printf("\nThe entered matrix is:\n");
    for(i=0;i<3; i++) {
        printf("\n");
        for(j=0;j<3; j++) {
            printf("%d\t", a[i][j]);
        }
    }

    printf("\n\nThe transpose of the matrix is: \n");
    for(i=0;i<3; i++) {
        for(j=0;j<3; j++) {
            b[i][j]=a[j][i];
        }
    }
    printf("\n\n");
    printf("%d\t",b[i][j]);
}

getch();
}
```

![](img/177eacb192165f90062789304b5da281_225_0.png)

# 格拉-希尔出版公司

数组 215

输出

输入一个 3 X 3 矩阵：

a[0][0] = 1

a[0][1] = 2

a[0][2] = 3

a[1][0] = 4

a[1][1] = 5

a[1][2] = 6

a[2][0] = 7

a[2][1] = 8

a[2][2] = 9

输入的矩阵是：

1 2 3

4 5 6

7 8 9

矩阵的转置是：

1 4 7

2 5 8

3 6 9

![](img/177eacb192165f90062789304b5da281_226_0.png)

## 7.7 多维数组

C 语言允许三个或更多维的数组。具体的限制由编译器决定。多维数组的通用形式为：

```c
类型 数组名[s1][s2][s3]....[sm];

int survey[3][12];
float table[5][4][5][3];
```

其中 s 是第 i 维的大小。例如，`survey` 是一个包含 360 个整数元素的三维数组。同样，`table` 是一个包含 300 个浮点类型元素的四维数组。

数组 `survey` 可以代表五个城市在过去三年中从 1 月到 12 月的降雨量调查数据。

如果第一个索引表示年份，第二个表示城市，第三个表示月份，那么元素 `survey[2][3][10]` 表示第二 3 年 10 月的降雨量。

## ANSI C 编程

记住，三维数组可以表示为一系列二维数组，如下所示：

| 月份 城市 | 1 | 2 | ... | 12 |
|---|---|---|---|---|
| 年 1 | 1 | | | |
| | | | | |
| | | | | |
| | 5 | | | |
| 月份 城市 | 1 | 2 | ... | 12 |
|---|---|---|---|---|
| 年 2 | 1 | | | |
| | | | | |
| | | | | |
| | 5 | | | |
