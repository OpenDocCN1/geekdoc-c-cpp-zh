
```c
// Eigenvalues and eigenvectors of inverse of symmetric matrix
#include <stdio.h>
#include <time.h>
#include "linsys.h"
#include "eigsy s.h"
#include "matutil.h"

int main()
{
    double **a, **a1, **x, **x1, *d, *d1;
    double det, norm;
    int i, j, n;

    n = 100;                                            // order of matrix
    a = Matrix(1,n,1,n);                                // coefficient matrix
    a1 = Matrix(1,n,1,n);                               // inverse of a
    x = Matrix(1,n,1,n);                                // eigenvectors of a
    x1 = Matrix(1,n,1,n);                               // eigenvectors of a1
    d = Vector(1,n); d1 = Vector(1,n);                  // eigenvalues of a and a1

    srand(time(NULL));                                  // initialize random number generator
    for (i=1; i<=n; i++)                                // generate random coefficient matrix
        for (j=1; j<=n; j++) {
            a[i][j] = a[j][i] = (double)rand()/RAND_MAX;
            a1[i][j] = a1[j][i] = a[i][j];              // copy a in a1
        }

    Jacobi(a,x,d,n);                                    // solve eigenvalue problem for a
    EigSort(x,d,n,1);                                   // sort eigenvalues and eigenvectors

    MatInv(a1,n,det);                                   // a1 = a^(-1)
    Jacobi(a1,x1,d1,n);                                 // solve eigenvalue problem of a^(-1)
    for (i=1; i<=n; i++) d1[i] = 1e0/d1[i]; // invert eigenvalues before sorting
    EigSort(x1,d1,n,1);                                 // sort eigenvalues and eigenvectors

    for (j=1; j<=n; j++)                                // loop over eigenvectors
        if (x[1][j] * x1[1][j] < 0)                     // eigenvectors have different sign?
            for (i=1; i<=n; i++) x1[i][j] = -x1[i][j];  // match sign

    VecDiff(d,d1,d1,n);                                 // difference of eigenvalues in d1
```
### PROBLEM 8.2

考虑一根无质量的弹性振动弦，加载有 `n` 个相同点质量 `m`，以相等距离 `d` 分布在恒定张力 `T` 下。假设弦的小横向位移，确定其振动的正常模式的频率和位移。特别考虑 `n=100` 且 `dm/T=1`，并检查无量纲特征频率是否为 `π` 的倍数。

### Solution

用 `$u_i=u_i(t)$`，`i=1,2,…,n` 表示各点的瞬时横向位移，弦对点质量 `i` 施加的横向力可近似为 (Maor 1975)

$$F_i=T\frac{u_{i-1}-2u_i+u_{i+1}}{d},$$

相应的运动方程为

$$m\ddot{u}_i=(T/d)(u_{i-1}-2u_i+u_{i+1}),\qquad i=2,\ldots,n-1.$$

这组耦合方程必须补充边界条件，在最简单的两端固定的弦情况下，读作：

$$u_1=u_n=0.$$

弦的正常模式以所有点同相振动、具有共同角频率 `$\omega$` 为特征。因此，每个点的运动规律将具有形式：

$$u_i=x_i\exp(j\omega t),$$

其中 `x_i` 是相应的 *横向位移*（振幅），`j` 是虚数单位。离散化的运动方程连同边界条件最终导致以下具有三对角矩阵的特征值问题：

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_271_0.png)

# Listing 8.9 Normal Modes of Loaded String (C/C++ Coding)

```c
// Normal modes of a loaded string with fixed ends
#include <math.h>
#include "memalloc.h"
#include "eigsy s.h"
#include "graphlib.h"

int main(int argc, wchar_t** argv)
{
    double **a, **x, *d, *xp, *yp;
    double h, omega;
    int i, mode, n;
    char title[20];

    n = 100;                                            // number of point masses
    a = Matrix(1,n,1,n);                                // coefficient matrix
    x = Matrix(1,n,1,n);                                // eigenvectors = displacements
    d = Vector(1,n);                                    // eigenvalues ~ frequencies^2
    xp = Vector(1,n);                                   // mesh points for plotting
    yp = Vector(1,n);                                   // function values for plotting

    for (i=1; i<=n; i++) a[i][i] = 2e0;                  // build coefficient matrix
    for (i=2; i<=n-2; i++) { a[i+1][i] = -1e0; a[i][i+1] = -1e0; }

    Jacobi(a,x,d,n);                                    // solve eigenvalue problem
    EigSort(x,d,n,1);                                   // sort eigenvalues and eigenvectors

    h = 1e0/(n-1);
    for (i=1; i<=n; i++) xp[i] = (i-1) * h;              // mesh points for plotting

    PyGraph w(argc, argv);
    w.GraphInit(1200,600);

    mode = 1;                                           // normal mode 1
    omega = sqrt(d[mode])*(n-1);                        // frequency
    for (i=1; i<=n; i++) yp[i] = x[i][mode];             // displacements
    sprintf(title,"omega(%i) = %6.2f",mode,omega);
    w.Plot(xp,yp,n,"blue",3,0.10,0.45,0.60,0.90,"x","y",title);

    mode = 2;                                           // normal mode 2
    omega = sqrt(d[mode])*(n-1);                        // frequency
    for (i=1; i<=n; i++) yp[i] = x[i][mode];             // displacements
    sprintf(title,"omega(%i) = %6.2f",mode,omega);
    w.Plot(xp,yp,n,"blue",3,0.60,0.95,0.60,0.90,"x","y",title);

    mode = 3;                                           // normal mode 3
    omega = sqrt(d[mode])*(n-1);                        // frequency
    for (i=1; i<=n; i++) yp[i] = x[i][mode];             // displacements
    sprintf(title,"omega(%i) = %6.2f",mode,omega);
    w.Plot(xp,yp,n,"blue",3,0.10,0.45,0.10,0.40,"x","y",title);

    mode = 4;                                           // normal mode 4
    omega = sqrt(d[mode])*(n-1);                        // frequency
    for (i=1; i<=n; i++) yp[i] = x[i][mode];             // displacements
    sprintf(title,"omega(%i) = %6.2f",mode,omega);
    w.Plot(xp,yp,n,"blue",3,0.60,0.95,0.10,0.40,"x","y",title);

    w.MainLoop();
}
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_274_0.png)

# 图 8.1 固定端带载弦的最低四阶正常模态。

# 问题 8.3

考虑四面体甲烷分子 `CH₄`，其相对原子质量为 `m_C = 12` 和 `m_H = 1`，且在体固定参考系中 5 个原子的以下笛卡尔位置（单位 Å）：

```
x = [0.000  0.635  -0.635  -0.635   0.635],
 y = [0.000  0.635  -0.635   0.635  -0.635],
 z = [0.000  0.635   0.635  -0.635  -0.635],
 r = [1.700  1.200   1.200   1.200   1.200].
```

`C` 原子位于原点，量 `r` 表示原子的范德华半径（Bondi 1964）。

+   a. 通过从各个坐标中减去质心坐标，将分子置于其质心系中：

```
x_CM = 1/m_CM Σ_i m_i x_i,   y_CM = 1/m_CM Σ_i m_i y_i,   z_CM = 1/m_CM Σ_i m_i z_i,
```

其中

```
m_CM = Σ_i m_i
```

为原子系统总质量。

+   b. 计算分子在笛卡尔质心系中的惯性张量：

```
I = [ [I_xx, I_xy, I_xz], [I_yx, I_yy, I_yz], [I_zx, I_zy, I_zz] ] ,
```

其中

$I_{xx}=\sum_i m_i(y_i^2+z_i^2),\quad I_{xy}=I_{yx}=-\sum_i m_i x_i y_i,$

$I_{yy}=\sum_i m_i(z_i^2+x_i^2),\quad I_{xz}=I_{zx}=-\sum_i m_i z_i x_i,$

$I_{zz}=\sum_i m_i(x_i^2+y_i^2),\quad I_{yz}=I_{zy}=-\sum_i m_i y_i z_i.$

c. 求解惯性张量的特征值问题，

\begin{bmatrix} I_{xx} & I_{xy} & I_{xz} \\ I_{yx} & I_{yy} & I_{yz} \\ I_{zx} & I_{zy} & I_{zz} \end{bmatrix} \begin{bmatrix} R_{xx} & R_{xy} & R_{xz} \\ R_{yx} & R_{yy} & R_{yz} \\ R_{zx} & R_{zy} & R_{zz} \end{bmatrix} = \begin{bmatrix} R_{xx} & R_{xy} & R_{xz} \\ R_{yx} & R_{yy} & R_{yz} \\ R_{zx} & R_{zy} & R_{zz} \end{bmatrix} \begin{bmatrix} I_x & 0 & 0 \\ 0 & I_y & 0 \\ 0 & 0 & I_z \end{bmatrix},

以确定主转动惯量—`I₁`、`I₂` 和 `I₃`——作为特征值，以及旋转矩阵 `R` 作为模态矩阵，其列包含特征向量。

d. 使用转置变换矩阵 `Rᵀ` 将原子坐标旋转到主轴系：

\begin{bmatrix} x'_i \\ y'_i \\ z'_i \end{bmatrix} = \begin{bmatrix} R_{xx} & R_{yx} & R_{zx} \\ R_{xy} & R_{yy} & R_{zy} \\ R_{xz} & R_{yz} & R_{zz} \end{bmatrix} \begin{bmatrix} x_i \\ y_i \\ z_i \end{bmatrix},\quad i=1,2,\dots,n.

e. 使用包含在库 `graphlib.py` 和 `graphlib.h` 中的例程 `PlotParticles` 可视化初始构型，以及分别以 `x` 轴和 `z` 轴为主对称轴的构型（详见第 3 章）。

# 解法

用于将粒子系统置于质心系并旋转到主轴系的 Python 函数包含在模块 `coords.py` 中，并在列表 8.10 中给出。C/C++ 对应版本作为补充材料提供在文件 `coords.h` 中。

Python 主程序显示在列表 8.11 中，C/C++ 版本作为补充材料提供（`P08-MomInert.cpp`）。产生的图形输出显示在图 8.2 中。

# 列表 8.10 粒子系统坐标的变换（coords.py）
