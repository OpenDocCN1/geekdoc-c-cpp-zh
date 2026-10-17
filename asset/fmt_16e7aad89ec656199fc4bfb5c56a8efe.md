
输出 5 位零件 ID、数量、单价、单元总成本

`end for`

输出总数量和总成本

`return`

```
/* */
/* main: 某工程公司的库存管理 */
/* */
/* 定义常量：- 不同零件的数量 */
/* NUMPRTS */
/* 输入变量： */
/* partid - 每个零件的标识符 */
/* partunits - 每个零件的单元数量 */
/* unitcost - 每个零件的成本 */
/* */
/* 计算变量：- 每个零件总单元的成本 */
/* totalunits - 所有部分的总数量 */
/* totalcost - 库存的总成本 */
/* */
/* 输出变量： */
/* partid - 每个零件的标识符 */
/* partunits - 每个零件的单元数量 */
/* unitcost - 每个零件的成本 */
/* unitscost - 每个零件总单元的成本 */
/* totalunits - 所有部分的总数量 */
/* */
/* totalcost - 库存的总成本 */
/* 调用的函数： */
/* funcinput() - 输入数据的函数 */
/* funccomp() - 计算每个零件 */
/* 总单元数量的函数 */
/* functotunits() - 计算所有部分 */
/* 总数量的函数 */
/* functotcost() - 计算所有部分的 */
/* 总成本的函数 */
/* funcoutput() - 输出数据的函数 */
/****************************************************************/
```

```c
#include <stdio.h>
#define NUMPRTS 5

void funcinput(int [], float [], int [], int);

void funccomp(int [], float [], float [], float [], int);

int functotunits(int [], int);

float functotcost(float [], int [], int);

void funcoutput(int [], int [], float [], float [], int, float);

int main() {
    int totalunits, partid[NUMPRTS], partunits[NUMPRTS];
    float totalcost, unitcost[NUMPRTS], unitcost[NUMPRTS];
    funcinput(partid, partunits, NUMPRTS);
    funccomp(partunits, unitcost, unitcost, NUMPRTS);
    totalunits = functotunits(partunits, NUMPRTS);
    totalcost = functotcost(unitcost, NUMPRTS);
    funcoutput(partid, partunits, unitcost, unitcost,
    totalunits, totalcost, NUMPRTS);
    return 0;
}
```

/****************************************************************/
/* funcinput: 从数据文件输入零件和成本 */
/****************************************************************/

```
/* 输入变量：
 *  partid1[n] - 零件标识
 *  unitcost1[n] - 每个单元的成本
 *  n - 零件数量
 *
 输出参数：
 *  partid1[n] - 零件标识
 *  unitcost1[n] - 每个单元的成本
 *  partunits1 - 零件单元数量
 *
 使用到的数据文件：
 *  filein1.dat - 零件标识和
 *  每个单元的成本
 *********************************************************************/
```

```c
void funcinput(int partid1[], float unitcost1[], int partunits1[], 
    int n) {
    FILE *inptr;
    int i;
    inptr = fopen("filein1.dat", "r");
```

```c
    for(i = 0; i < n; i++) {
        fscanf(inptr, "%d %f %d", &partid1[i], &unitcost1[i], &partunits1[i]);
    }
    fclose(inptr);
    return;
}
```

********************************************************************/
/* funccpute: 计算单元成本
 *********************************************************************/
/* 输入参数：
 *  partunits1[n] - 单元数量
 *  unitcost1[n] - 每个单元的成本
 *  n - 零件数量
 *
 计算变量：
 *  unitcost2[n] - 每个零件的总成本
/* 输出参数：
 *  unitcost2[n] - 每个零件的总成本
/*
****************************************************
```

```c
void funccomp(int partunits1[], float unitcost1[],
      float unitcost2[], int n)
{
    int i;
    for(i = 0; i < n; i++)
    {
        unitcost2[i] = partunits1[i] * unitcost1[i];
    }
    return;
}
```

****************************************************

/*
   functotunits: 计算所有部分的
   总数量
****************************************************

/*
/* 输入参数：
 *  partunits1[n] - 单元数量
 *  n - 零件数量
/*
   计算变量：
 *  totalunits - 所有部分的总数量
/*
   返回变量：
 *  totalunits - 所有部分的总数量
****************************************************

```c
int functotunits(int partunits1[], int n)
{
    int i, totalunits = 0;
    for(i = 0; i < n; i++)
    {
        totalunits += partunits1[i];
    }
    return totalunits;
}
```

****************************************************

/*
   functotcost: 计算所有部分的总成本
/*
****************************
/* 输入参数：
 *  unitcost1[n] - 每个单元的成本
 *  n - 零件数量
/*
 计算变量：
 *  totalcost - 所有部分的总成本
/*
   返回变量：
 *  totalcost - 所有部分的总成本
/*
***************************/

```c
float functotcost(float unitcost1[], int n)
{
    int i;
    float totalcost = 0.0;
    for(i = 0; i < n; i++)
    {
        totalcost += unitcost1[i];
    }
    return totalcost;
}
```

************************************************************
/* funcoutput: 将数据输出到文件 */
/* 输入参数：
 *  partid1[n] - 零件标识
 *  partunits1[n] - 单元数量
 *  unitcost1[n] - 每个单元的成本
 *  unitcost2[n] - 每个零件的总成本
 *  totalunits1[n] - 所有部分的总数量
 *  totalcost1 - 所有部分的总成本
 *  n - 零件数量
/* 输出变量：
 *  partid1[n] - 零件标识
 *  partunits1[n] - 单元数量
/* unitcost1[n] - 每个单元的成本
/* unitcost2[n] - 每个零件的总成本
/* totalunits1 - 所有部分的总数量
/* totalcost1 - 所有部分的总成本
/* * */
/* 使用的数据文件： */
/* fileout.dat - 输出库存表
********************************************************************

```c
void funcoutput(int partid[], int partunits1[], 
    float unitcost1[], float unitcost2[],
    int totalunits1, float totalcost1, int n)
{
    FILE *outptr;
    int i;

    outptr = fopen("fileout.dat", "w");

    for(i = 0; i < n; i++)
    {
        fprintf(outptr, "%2d %5d %3f %5.2f %8.2f\n",
            partid[i], partunits1[i], unitcost1[i],
            unitcost2[i]);
    }
    fprintf(outptr, "\nTotalunits:%d Totalcost:%8.2f\n",
        totalunits1, totalcost1);
    fclose(outptr);

    return;
}
```

输入数据文件: `"filein.dat"`
65478 18 2.56
75396 25 3.67
89352 16 1.25
97169 45 4.86
99578 29 6.54

输出数据文件: `"fileout.dat"`
0 65478 18 46.08
1 75396 25 3.67 91.75
2 89352 16 20.00
3 97169 45 4.86 218.70
4 99578 29 6.54 189.66

Totalunits:133 Totalcost:566.19

# 483 章节总结

一维数组是派生自基本类型 `int`、`float`、`double` 或 `char` 的数据类型。当数据被处理多次或不是按提供的顺序进行处理时，一维数组用于以列表的形式存储大量数据。在科学和工程应用中，一维数组用于存储向量。在 C 语言中一维数组声明的通用形式如下：

```c
数据类型 数组名[元素个数];
```

例如：

```c
int value[5];
```

数据可以通过三种不同的方式存储在数组元素中：

- 在声明时初始化数组
- 使用赋值语句为每个单独元素分配数据值
- 使用输入函数 `scanf()` 或 `fscanf()` 输入数据值

数组的输入和输出可以使用索引数组元素的 `for` 循环方便地实现。初始化如下：

```c
int i, a[5];
for (i = 0; i < 5; i++)
a[i] = 0;
```

```c
或 int a[5] = {0, 0, 0, 0, 0};
or[0] = 0; a[1] = 0; a[2] = 0; a[3] = 0; a[4] = 0;
```

输入如下：

```c
for (i = 0; i < 5; i++)
scanf("%d", &a[i]);
```

输出如下：

```c
for (i = 0; i < 5; i++)
printf("%d\n", a[i]);
```

对单个变量执行的所有算术和逻辑操作也可以在数组元素上执行。算术和逻辑操作可以通过使用显式索引随机访问或使用 `for` 循环索引顺序访问数组元素来完成。需要排序或搜索的小量数据可以存储在数组中。如果数据已经过排序，可以使用快速二分查找。

一维数组通过传递数组名传递给函数。当通过数组名传递给函数时，函数知道数组的起始地址。当在函数中更改数组值时，这些更改将反映在调用函数所传递的参数中。

```c
#define ARSIZE 10 /* 定义常量 */
void func(int [ ]); /* 函数原型 */
int array[ARSIZE]; /* 数组声明 */
func(array, ARSIZE); /* 传递数组名和大小函数调用 */
void func(int arr[ ], int n) /* 函数头 */
```

可以通过显式指定元素的索引将数组元素传递给函数。在将元素传递给函数时，可以按值传递或按地址传递，并被处理为普通变量。以下显示了使用显式索引将数组元素按值传递给函数：

```c
#define ARSIZE 10 /* 编译器常量 */
void funccomput(int, int); /* 函数原型 */
int i, a[ARSIZE] = { 2, 3, 4, 5, 6 }; /* 数组声明和初始化 */
funccomput(a[4]); /* 函数调用，传递数组元素 */
void funccomput(int x) /* 函数头 */
{
	...
	return;
}
```

数组元素 `a[4]` 按值传递的。如果更改函数中参数的值，该更改将不会反映在调用函数的参数中。

```c
#define ARSIZE 10
void funccomp( int *x); /* 函数原型 */
int i, a[5] = { 2, 3, 4, 5, 6 }; /* 数组声明和初始化 */
funccomp(&a[4]); /* 函数调用 */
void funccomp(int *x) /* 函数头和函数体 */
{
  .
  return;
}
```

在这里，数组元素 `a[4]` 按地址传递并被指针变量接收。如果更改函数中参数的值，该更改将反映在调用函数的参数中。

## 练习

- 1. 编写一个程序，输入 100 个值到数组 `a[100]` 中。计算正数的计数、和和平均值，以及负数的计数、和和平均值。输出数组（每行十个数）、以及正、负数的计数、和和平均值。
- 2. 编写一个程序，使用随机生成器生成 1 到 20 之间的 500 个数字。统计每个数字在该集合中出现的次数，并打印数字及其频率。使用数组存储这些数字。
- 3. 编写一个程序，根据半径为 `$r$`、角度以 `$5^{\circ}$` 为增量的圆，从极坐标生成笛卡尔坐标。将 `$x$` 和 `$y$` 坐标值存储在一维数组中。极坐标到笛卡尔坐标的转换公式如下：

```
x = r \cos \theta
y = r \sin \theta
```

- 4. 编写一个程序，以直径 `$d$` 为输入计算螺旋在各种速度 `$s$`（单位为每分钟转）下的端速。令 `$s = 50, 100, 150, \dots, 1000$`。将螺旋的端速存储在表中并打印该表。计算英尺/秒径向速度的公式如下：

```
\omega = \frac{2\pi s}{60} \quad v = \frac{\omega d}{2}
```

`$d$` 是以英尺为单位的螺旋直径。
`$s$` 是每分钟转的速度
`$\omega$` 是每分钟弧弧的径向速度
`$v$` 是每分钟的速度

- 5. 编写一个程序，在二维数组中记录温度和压力，然后识别极值。编写一个程序，将每次测量值相对于基线的高度存储在二维数组中。计算平均值。
- 6. 编写一个程序，在二维数组中存储调查值。使用二维数组找到众数。
- 7. 编写一个程序，在二维数组中输入重量数据并按降序排序。
- 8. 编写一个程序，找到二维数组中出现次数最多的数字。

# 第 8 章

## 多维数组

## 目标

处理行列形式的数据、矩阵以及两个以上的维度。

- 8.1 二维数组简介
- 8.2 二维数组的输入
- 8.3 二维数组的输出
- 8.4 数组的操作
- 8.5 传递给函数
- 8.6 高维数组
- 8.7 示例程序

行列形式的均匀数据是二维的。二维空间中的点表示为 `$f(x, y)$` 并存储在二维数组中。如果点位于空间和时间，它们存储在三维数组中。许多科学应用中的变量是二维的，表示为 `$f(x, y)$`。依赖于二维空间的函数为 `$f(x, y, t)$`。

## 总结
