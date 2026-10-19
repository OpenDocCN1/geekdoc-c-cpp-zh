
这个方程表示了温度$T_{i,j}$的隐式格式，其中“隐式”意味着我们必须求解联立方程以获得整个空间的完整解。相反，显式格式需要迭代才能得出解。可以同时求解(20.30)中在时间$j$和$j+1$的所有未知温度（$1 \le i \le N$）。我们从整个空间的初始温度分布、杆两端在所有时间的边界条件以及一阶导数的近似值开始：

$T_{i,0},\quad\text{已知},\quad T_{0,j},\quad\text{已知},\quad T_{N,j},\quad\text{已知},$ $T_{0,j+1}=T_{0,j}=0,\quad T_{N,j+1}=0,\quad T_{N,j}=0.\qquad(20.31)$

我们重新整理(20.30)，以便利用这些已知的$T$值，通过将(20.30)表示为一组联立线性方程（矩阵形式），将$j=0$的解向前推进：

$\begin{pmatrix} \left(\frac{2}{\eta}+2\right) & -1 & & & \\ -1 & \left(\frac{2}{\eta}+2\right) & -1 & & \\ & -1 & \left(\frac{2}{\eta}+2\right) & -1 & \\ & & \ddots & \ddots & \ddots \\ & & & -1 & \left(\frac{2}{\eta}+2\right) & -1 \\ & & & & -1 & \left(\frac{2}{\eta}+2\right) \end{pmatrix} \begin{pmatrix} T_{1,j+1} \\ T_{2,j+1} \\ T_{3,j+1} \\ \vdots \\ T_{n-2,j+1} \\ T_{n-1,j+1} \end{pmatrix} = \begin{pmatrix} T_{0,j+1}+T_{0,j}+\left(\frac{2}{\eta}-2\right)T_{1,j}+T_{2,j} \\ T_{1,j}+\left(\frac{2}{\eta}-2\right)T_{2,j}+T_{3,j} \\ T_{2,j}+\left(\frac{2}{\eta}-2\right)T_{3,j}+T_{4,j} \\ \vdots \\ T_{n-3,j}+\left(\frac{2}{\eta}-2\right)T_{n-2,j}+T_{n-1,j} \\ T_{n-2,j}+\left(\frac{2}{\eta}-2\right)T_{n-1,j}+T_{n,j}+T_{n,j+1} \end{pmatrix}.\qquad(20.32)$

注意，等式右边的$T$在各自位置均处于当前时间$j$，而在两端则处于未来时间$j+1$（通过边界条件已知所有时间的$T$）。我们从初始条件的$T_{i,j=0}$值开始该算法，然后求解矩阵方程以获得$T_{i,j=1}$。至此，我们知道方程右边所有项（杆内为$j=1$，两端为$j=2$），因此可以重复求解矩阵方程以获得杆内时间$j=2$的温度。这样，我们再次向前步进，只是现在每一步都需要求解矩阵方程。这直接给出了所有位置的空间解。

Crank–Nicolson方法不仅比低阶时间步进方法更精确，而且对于所有$\Delta t$和$\Delta x$的值都是稳定的。为了证明这一点，我们将第20.2.3节中讨论的冯·诺依曼稳定性分析应用于

## 20.4 改进的热流：Crank–Nicolson方法

Crank–Nicolson算法通过将(20.17)代入(20.30)，确定了一个放大因子

```
\xi(k) = \dfrac{1 - 2\eta \sin^2(k\Delta x/2)}{1 + 2\eta \sin^2(k\Delta x/2)}
```

因为sin²()是正定的，这证明了对于所有Δt、Δx和k，都有|ξ| ≤ 1。

Crank–Nicolson方程(20.32)是线性方程的标准[A]x = b形式，因此我们可以使用之前的方法来求解它们。然而，由于系数矩阵[A]是三对角的（除主对角线及其两侧的两条对角线外，其余元素为零），

```
\begin{pmatrix} d_1 & c_1 & 0 & 0 & \dots & & & 0 \\ a_2 & d_2 & c_2 & 0 \\ 0 & a_3 & d_3 & c_3 \\ \vdots & \vdots & \vdots & \ddots \\ 0 & 0 & 0 & 0 & a_N \\ 0 & 0 & 0 & 0 & d_N \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \\ \vdots \\ x_{N-1} \\ x_N \end{pmatrix} = \begin{pmatrix} b_1 \\ b_2 \\ b_3 \\ \vdots \\ b_{N-1} \\ b_N \end{pmatrix}
```

存在一种更稳健且更快的求解方法，使这种隐式方法与显式方法一样快。由于三对角系统经常出现，我们现在概述求解它们的专用技术（Press等，1994）。如果我们用双下标存储矩阵元素a_{i,j}，那么需要N²个元素位置和N²次操作来访问它们。然而，对于三对角矩阵，我们只需要存储向量{d_i}_{i=1,N}、{c_i}_{i=1,N-1}和{a_i}_{i=1,N-1}，分别对应主对角线、上方对角线和下方对角线。a_i、d_i和c_i的单下标将处理量从N²减少到(3N - 2)个元素。

我们通过逐个操作方程来求解矩阵方程，直到系数矩阵变为上三角矩阵且主对角线所有元素等于1。首先将第一个方程除以d_1，然后减去第一个方程的a_2倍，

```
\begin{pmatrix} 1 & c_1/d_1 & 0 & 0 & \dots & & & 0 \\ 0 & d_2 - a_2 c_1 / d_1 & c_2 & 0 \\ 0 & a_3 & d_3 & c_3 \\ \vdots & \vdots & \vdots & \ddots \\ 0 & 0 & 0 & 0 & a_N \\ 0 & 0 & 0 & 0 & d_N \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \\ \vdots \\ x_{N-1} \\ x_N \end{pmatrix} = \begin{pmatrix} b_1/d_1 \\ b_2 - a_2 b_1 / d_1 \\ b_3 \\ \vdots \\ b_{N-1} \\ b_N \end{pmatrix}
```

然后将第二个方程除以第二个对角线元素，

![](img/bccda43674e4a93dee81c749eba8d2f7_511_0.png)

假设我们可以重复这些步骤而不除以零，方程组将被化为上三角形式，

![](img/bccda43674e4a93dee81c749eba8d2f7_511_1.png)

其中$h_1=c_1/d_1$，$p_1=b_1/d_1$。然后我们对其他元素进行递推：

$$h_i=\frac{c_i}{d_i-a_i h_{i-1}},\qquad p_i=\frac{b_i-a_i p_{i-1}}{d_i-a_i h_{i-1}}.$$

最后，回代得出未知数的显式解：

$$x_i=p_i-h_i x_{i-1},\qquad i=n-1,n-2,\ldots,1,\qquad x_N=p_N.$$

在清单20.2中，我们给出了使用Crank–Nicolson算法通过三对角化简求解热方程的HeatCNTridiag.py程序。

**清单20.2  HeatCNTridiag.py** 是通过Crank–Nicolson方法在一维空间和时间上求解热方程的完整程序。生成的矩阵方程通过专门针对三对角矩阵的技术求解。

```python
# HeatCNTridiag.py: solution of heat eqtn via CN method

import matplotlib.pylab as p;
from mpl_toolkits.mplot3d import Axes3D;
from numpy import *;
import numpy;

Max = 51; n = 50; m = 50
Ta = zeros((Max),float); Tb = zeros((Max),float); Tc = zeros((Max),float)
Td = zeros((Max),float); a = zeros((Max),float); b = zeros((Max),float)
c  = zeros((Max),float); d = zeros((Max),float); x = zeros((Max),float)
```

```
t = zeros( (Max, Max),float)

def Tridiag(a, d, c, b, Ta, Td, Tc, Tb, x, n):
    Max = 51
    h = zeros( (Max), float )
    p = zeros( (Max), float )
    for i in range(1,n+1):
        a[i] = Ta[i]
        b[i] = Tb[i]
        c[i] = Tc[i]
        d[i] = Td[i]
    h[1] = c[1]/d[1]
    p[1] = b[1]/d[1]
    for i in range(2,n+1):
        h[i] = c[i] / (d[i]-a[i]*h[i-1])
        p[i] = (b[i] - a[i]*p[i-1]) / (d[i]-a[i]*h[i-1])
    x[n] = p[n]
    for i in range( n - 1, 1,-1 ): x[i] = p[i] - h[i]*x[i+1]

width = 1.0; height = 0.1; ct = 1.0
for i in range(0, n):  t[i,0] = 0.0
for i in range(1, m):  t[0][i] = 0.0
h = width / ( n - 1 )
k = height / ( m - 1 )
r = ct * ct / ( h * h )

for j in range(1,m+1):
    t[1,j] = 0.0
    t[n,j] = 0.0
for i in range(2, n):  t[i][1] = sin( pi * h *i)          # BCs
for i in range(1, n+1): Td[i] = 2. + 2./r
Td[1] = 1.; Td[n] = 1.
for i in range(1,n): Ta[i] = -1.0;      Tc[i] = -1.0;    # Off diagonal
Ta[n-1] = 0.0;  Tc[1] = 0.0; Tb[1] = 0.0; Tb[n] = 0.0
print("I'm working hard, wait for fig while I count to 50")

for j in range(2,m+1):
    print(j)
    for i in range(2,n): Tb[i] = t[i-1][j-1] + t[i+1][j-1] \
      + (2/r-2) * t[i][j-1]
    Tridiag(a, d, c, b, Ta, Td, Tc, Tb, x, n)          # Solve system
    for i in range(1, n+1):  t[i][j] = x[i]
print("Finished")
x = list(range(1, m+1))                               # Plot every other x
y = list(range(1, n+1))                               # every other y
X, Y = p.meshgrid(x,y)

def functz(t):
    z = t[X, Y]                                       # Potential
    return z

Z = functz(t)
fig = p.figure()
ax = Axes3D(fig)
ax.plot_wireframe(X, Y, Z, color='r')
ax.set_xlabel('t')
ax.set_ylabel('x')
ax.set_zlabel('T')
p.show()                                              # Display figure
```

