

如果我们假设电阻 \(R_1, R_2, R_3, R_4, \text{和 } R_5\) 和电压源 \(V_1 \text{和 } V_2\) 的值已知，那么网电流 \(i_1, i_2, \text{和 } i_3\) 是未知的。然后我们可以按照如下方式重新排列方程组：

\((R_1 + R_2)i_1 - R_2 i_2 + 0 i_3 = V_1\),
\(-R_2 i_1 + (R_2 + R_3 + R_4)i_2 - R_4 i_3 = 0\),
\(0 i_1 - R_4 i_2 + (R_4 + R_5)i_3 = -V_2\).

编写一个程序，允许用户输入五个电阻的值和两个电压源的值。然后程序应计算三个网电流。

## 1. 问题描述

计算图 5.6 所示电路中的三个网电流。

## 2. 输入/输出描述

I/O 图显示，电阻值和电压值是输入值。三个网电流是输出值。

![](img/02c4582f051c5b51776411c92b079035_295_0.png)

## 3. 手算示例

通过使用电阻值和电压值，可以使用问题定义中重新排列的这组方程定义一个三元方程组：

\((R_1 + R_2)i_1 - R_2 i_2 + 0 i_3 = V_1\),
\(-R_2 i_1 + (R_2 + R_3 + R_4)i_2 - R_4 i_3 = 0\),
\(0 i_1 - R_4 i_2 + (R_4 + R_5)i_3 = -V_2\).

例如，假设每个电阻值为 1 欧姆，并假设两个电压源均为 5 伏特。那么，相应的方程组如下：

\(2i_1 - i_2 + 0 i_3 = 5\),
\(-i_1 + 3i_2 - i_3 = 0\),
\(0 i_1 - i_2 + 2i_3 = -5\).

一旦确定了方程组，解法遵循前一节手算示例中所示的步骤。对于这组方程，解为 \(i_1 = 2.5, i_2 = 0, \text{和 } i_3 = -2.5\)。

## 4. 算法开发

我们首先开发分解大纲，因为它将解法分解为一系列顺序步骤：

### 分解大纲

- 1. 读取电阻值和电压值。
- 2. 指定方程组的系数。
- 3. 执行高斯消元法以确定电流。
- 4. 打印电流。

步骤 1 读取指定电路值所需的信息。步骤 2 使用此信息指定方程组的系数。步骤 3 开发消元和回代步骤的详细信息。为了保持主函数简洁易读，消元和回代都使用了函数。该解法的结构图已在图 4.1 中使用。

联立方程的系数存储在二维数组中；解存储在一维数组中。变量 index 指示在消元函数中正在消除哪个变量；该变量范围从 0 到 n - 1，以匹配 C 中的下标。

由于必须指定详细的下标，高斯消元算法在伪代码中难以描述。请结合手算示例逐一过遍此伪代码，以确保您对下标处理感到熟悉：

### 伪代码细化

```
main:
 read resistor values and voltage values
 specify array coefficients, a[i][j]
 set index to zero
 while index <= n - 2
   eliminate(a,n,index)
   increment index by 1
 back_substitution(a,n,soln)
 print current values
eliminate(a,n,index):
 set row to index + 1
 while row <= n - 1
   set scale_factor to -a[row][index] / a[index][index]
   set a[row][index] to zero
   set col to index + 1
   while col <= n
     add a[index][col] * scale_factor
     to a[row][col]
     increment col by 1
   increment row by 1
back_substitute(a,n,soln):
    set soln[n - 1] to   a[n-1][n]
                           -----------
                           a[n-1][n-1]
    set row to n - 2
    while row >= 0
        set col to n - 1
        while col >= row + 1
            subtract soln[col] * a[row][col]
            from a[row][n]
        subtract 1 from col
        set soln[row] to   a[row][n]
                           -----------
                           a[row][row]
        subtract 1 from row
```

一旦我们熟悉伪代码，将其转换为 C 语言就相对简单了。

```c
//--------------------------------------------------------------//
//  Program chapter5_8                                          //
//                                                              //
//  This program uses Gauss elimination to determine the      //
//  mesh currents for a circuit.                                //
//                                                              //
```

```c
#include <stdio.h>
#define N 3    /* number of unknown currents */
```

```c
int main(void)
{
    /* Declare variables and function prototypes. */
    int index;
    double r1, r2, r3, r4, r5, v1, v2, a[N][N+1], soln[N];
    void eliminate(double a[N][N+1], int n, int index);
    void back_substitute(double a[N][N+1], int n,
                         double soln[N]);

    /* Get user input. */
    printf("Enter resistor values in ohms: \n");
    scanf("%lf %lf %lf %lf %lf\n", &r1,&r2,&r3,&r4,&r5);
    printf("Enter voltage values in volts: \n");
    scanf("%f %f",&v1,&v2);

    /* Specify equation coefficients. */
    a[0][0] = r1 + r2;
    a[0][1] = a[1][0] = -r2;
    a[0][2] = a[2][0] = a[1][3] = 0;
    a[1][1] = r2 + r3 + r4;
    a[1][2] = a[2][1] = -r4;
    a[2][2] = r4 + r5;
    a[0][3] = v1;
    a[2][3] = -v2;

    /* Perform elimination step. */
    for (index=0; index<=N-2; index++)
        eliminate(a,N,index);
    /* Perform back substitution step. */
    back_substitute(a,N,soln);
    /* Print solution. */
    printf("Solution:\n");
    for (index=0; index<=N-1; index++)
        printf("Mesh Current %d: %f \n",index+1,soln[index]);
    /* Exit program. */
    return 0;
}
```

```c
/*-----------------------------------------------------------*/
/* This function performs the elimination step. */
/*-----------------------------------------------------------*/
void eliminate(double a[N][N+1],int n,int index)
{
/* Declare variables. */
int row, col;
double scale_factor;
/* Eliminate variable from equations. */
for (row=index+1; row<=n-1; row++)
{
    scale_factor = -a[row][index]/a[index][index];
    a[row][index] = 0;
    for (col=index+1; col<=n; col++)
    a[row][col] += a[index][col]*scale_factor;
}
/* Void return. */
return;
}
```

```c
/*-----------------------------------------------------------*/
/* This function performs the back substitution. */
/*-----------------------------------------------------------*/
void back_substitute(double a[N][N+1],int n,
double soln[N])
{
/* Declare variables. */
int row, col;
/* Perform back substitution in each equation. */
soln[n-1] = a[n-1][n]/a[n-1][n-1];
for (row=n-2; row>=0; row--)
{
    for (col=n-1; col>=row+1; col--)
    a[row][n] -= soln[col]*a[row][col];
    soln[row] = a[row][n]/a[row][row];
}
/* Void return. */
return;
}
/*-----------------------------------------------------------*/
```

为了处理更大的方程组，必须更改符号常量 N；高斯消元的步骤不需要任何修改。

## 5. 测试

使用手算示例中的数据进行的程序交互如下：

```
Enter resistor values in ohms:
(R1, R2, R3, R4, R5)
1 1 1 1 1
Enter voltage values in volts:
(V1, V2)
5 5
Solution:
Mesh Current 1: 2.500000
Mesh Current 2: 0.000000
Mesh Current 3: -2.500000
```

该程序假设方程组有解，这意味着没有任何方程表示相同的方程或平行方程。我们可以通过添加额外的语句或函数来修改此程序以检查这些条件。

## 修改！

- 1. 如果所有五个电阻均为 5 欧姆且两个电压源均为 10 伏特，确定网电流。
- 2. 使用本节讨论的矩阵乘法验证问题 1 中的答案。（本问题假设您已学习前一节关于矩阵和向量的内容。）
- 3. 如果电阻值为 2、8、6、6 和 4 欧姆，电压源值为 40 和 20 伏特，确定网电流。
- 4. 通过将答案代回原始三元方程组来验证问题 3 的答案。

## 5.13 高维数组*

C 允许定义具有两个以上下标的数组。例如，此语句定义一个 **三维数组**：

```c
int b[3][4][2];
```

指定特定元素所需的三个下标，如果将数组放置在三维空间的原点，将分别对应 x、y 和 z 坐标，如图 5.7 所示。因此，阴影位置对应 b[2][0][1]。

*可选部分.

