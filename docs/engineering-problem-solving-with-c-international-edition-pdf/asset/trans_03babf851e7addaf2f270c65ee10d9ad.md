

修改后的方程组如下

```
3x + 2y - z = 10,
0x + \frac{11}{3}y + \frac{5}{3}z = \frac{25}{3},
0x - \frac{5}{3}y - \frac{2}{3}z = -\frac{13}{3}.
```

我们现在已消去除了第一个方程外所有方程中的第一个变量。

下一步是消去除了第一个和第二个方程外所有方程中的第二个变量，方法是将方程与第二个方程的缩放形式相加：

```
0x - \frac{5}{3}y - \frac{2}{3}z = -\frac{13}{3} \quad \text{(third equation)},
0x + \frac{5}{3}y + \frac{25}{33}z = \frac{125}{33} \quad \left(\text{second equation times } \frac{5}{11}\right),
\underline{0x + 0y + \frac{3}{33}z = -\frac{18}{33}} \quad \text{(sum)}.
```

修改后的方程组如下

```
3x + 2y - z = 10,
0x + \frac{11}{3}y + \frac{5}{3}z = \frac{25}{3},
0x + 0y + \frac{3}{33}z = -\frac{18}{33}.
```

因为第三个方程之后没有方程，算法的这部分已完成。

我们现在执行回代以求解方程组。最后一个方程只有一个变量，因此我们可以将方程乘以一个选定的缩放因子，使该变量的系数等于1。因此，我们将最后一个方程乘以 \frac{33}{3}，即11，得到

```
0x + 0y + z = -6.
```

将z的值代入倒数第二个方程，得到

```
0x + \frac{11}{3}y + \frac{5}{3}(-6) = \frac{25}{3}.
```

将方程化简，使所有常数项都在右边，得到

```
0x + \frac{11}{3}y = \frac{55}{3}.
```

这个方程只有一个变量，因此我们现在将其乘以一个选定的缩放因子，使新系数等于1：

```
0x + y = 5.
```

我们回到下一个方程，即本例中的最后一个方程：

```
3x + 2y - z = 10.
```

代入已确定的值，得到

```
3x + 2(5) - (-6) = 10,
```

或

```
3x = -6
```

因此，x的值为-2。

高斯消元法因此分为两部分：消元和回代。首先，修改方程，使得第k个变量在第k个方程之后的所有方程中被消去。然后，从最后一个方程开始，计算最后一个变量的值。接下来，使用该值和倒数第二个方程，计算倒数第二个变量的值。这种回代持续进行，直到确定所有变量的值。如果某个变量的所有系数都为零或非常接近零，则该系统是**病态条件**或没有唯一解。

病态条件
选主元

一种称为**选主元**的过程可以应用于提高高斯消元法的精度。行选主元涉及在执行高斯消元之前重新排序行，列选主元涉及在执行该过程之前重新排序列。完全选主元涉及重新排序行和列。这些过程在章末的问题中讨论。

## 练习！

使用高斯消元数值技术求解下列一组联立线性方程组的解：

- 1. -2x + y = -3
   x + y = 3

- 2. 3x + 5y + 2z = 8
   2x + 3y - z = 1
   x - 2y - 3z = -1

## 8.6 应用问题求解：电路分析

电路分析通常涉及求解一组联立方程。这些方程通常使用描述进入和离开节点电流的电流方程，或描述电路中网格回路电压的电压方程来推导。例如，考虑图8.4所示的电路。描述三个回路电压的方程如下：

![](img/f2bfa570e453b020c16e048c79a3ea0e_435_0.png)

图8.4 带有两个电压源的电路。

-V_1 + R_1 i_1 + R_2(i_1 - i_2) = 0,
R_2(i_2 - i_1) + R_3 i_2 + R_4(i_2 - i_3) = 0,
R_4(i_3 - i_2) + R_5 i_3 + V_2 = 0.

如果假设电阻值（$R_1, R_2, R_3, R_4,$ 和 $R_5$）和电压源值（$V_1$ 和 $V_2$）已知，则方程组中的未知数为网格电流（$i_1, i_2,$ 和 $i_3$）。然后我们可以将方程组重新排列为以下形式：

$(R_1 + R_2)i_1 - R_2 i_2 + 0i_3 = V_1,$
$-R_2 i_1 + (R_2 + R_3 + R_4)i_2 - R_4 i_3 = 0,$
$0i_1 - R_4 i_2 + (R_4 + R_5)i_3 = -V_2.$

编写一个程序，允许用户输入五个电阻的值和两个电压源的值，并将这些值存储在二维数组中。然后程序应计算三个网格电流。

### 1. 问题描述

计算图8.4所示电路中的三个网格电流。

### 2. 输入/输出说明

I/O图显示电阻值和电压值为输入值。三个网格电流为输出值。

![](img/f2bfa570e453b020c16e048c79a3ea0e_435_1.png)

### 3. 手算示例

使用电阻值和电压值，可以根据问题定义中的这组重新排列的方程定义一个三元方程组：

(R_1 + R_2)i_1 - R_2i_2 + i_3 = V_1,
-R_2i_1 + (R_2 + R_3 + R_4)i_2 - R_4i_3 = 0,
0i_1 - R_4i_2 + (R_4 + R_5)i_3 = -V_2.

例如，假设每个电阻值为1欧姆，两个电压源均为5伏特。那么相应的方程组如下：

2i_1 - i_2 + i_3 = 5,
-i_1 + 3i_2 - i_3 = 0,
0i_1 - i_2 + 2i_3 = -5.

一旦确定了方程组，解法遵循前一节手算示例中所示的步骤。对于这组方程，解为 i_1 = 2.5，i_2 = 0，i_3 = -2.5。

### 4. 算法开发

我们首先开发分解大纲，因为它将解法分解为一系列顺序步骤：

*分解大纲*

- 1. 读取电阻值和电压值。
- 2. 指定方程组的系数。
- 3. 执行高斯消元法以确定电流。
- 4. 打印电流。

在步骤1中，我们读取指定电路值所需的信息，在步骤2中，我们使用这些信息来指定方程组的系数。然后，在步骤3中，我们开发消元和回代步骤的详细信息。为了保持主函数简洁易读，消元和回代都使用了函数。此解法的结构图在图[?]中使用。

联立方程的系数存储在二维数组中；解存储在一维数组中。变量index指示在消元函数中正在消去哪个变量；该变量范围从0到n-1，以匹配C++中的下标。

由于必须指定详细的下标，高斯消元算法用伪代码描述起来比较困难。请结合手算示例通读此伪代码，以确保您对下标处理感到熟悉。

### 伪代码细化

```
main: read resistor values and voltage values
    specify array coefficients. a[i][j]
    set index to zero
    while index <= n - 2
        eliminate(a,n,index)
        increment index by 1
    back.substitute(a,n,soln)
    print current values
eliminate(a,index):
    set row to index + 1
    while row <= n-1
        set scale.factor to -a[row][index] / a[index][index]
        set a[row][index] to zero

        set col to index + 1
        while col <= n
            add a[index][col] . scale.factor
                to a[row][col]
            increment col by 1
        increment row by 1
back.substitute(a,n,soln):
    set soln[n-1] to a[n-1][n] / a[n-1][n-1]
    set row to n-2
    while row >= 0
        set col to n-1
        while col >= row + 1
            subtract soln[col] . a[row][col]
                from a[row][n]
            subtract 1 from col
        set soln[row] to a[row][n] / a[row][row]
        subtract 1 from row
```

一旦我们熟悉伪代码，将其转换为C++就相对简单了：

```
/* ...........................................*/
/* Program chapter8_6                        */
/*                                           */
/* This program uses Gauss elimination to    */
/* determine the mesh currents for a circuit. */
/*                                           */

#include <iostream>    //Required for cin, cout
using namespace std;

// Define global constant for number of unknowns.
const int N = 3;

