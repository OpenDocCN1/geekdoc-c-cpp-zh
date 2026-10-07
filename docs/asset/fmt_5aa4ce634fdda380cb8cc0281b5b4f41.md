
```csharp
static void TestBarycentric()
{
  double[] xdata = new double[] {0, 4, 8, 12, 16};
  double[] ydata = new double[] {0, 8, 32, 72, 128};
  double[] x = new double[] {2, 6, 10, 14};
  double[] y = BarycentricInterpolation(xdata, ydata, x);
  Rvector xvec = new RVector(x);
  Rvector yvec = new RVector(y);
  Console.Clear();
  Console.WriteLine("Running Barycentric Interpolation Test\n\n");
  Console.WriteLine("x = " + xvec.ToString());
  Console.WriteLine("y = " + yvec.ToString() + "\n\n");
  Console.WriteLine("Press ENTER to continue...");
  Console.ReadLine();
}
OUTPUT: Running Barycentric Interpolation
x = (2, 6, 10, 14)
y = (2, 18, 50, 98)
```

# 插值

## 7.4.3 牛顿差分插值

通常，如果你有 $n+1$ 个点 $\{(x_0, y_0), (x_1, y_1), \dots, (x_n, y_n)\}$，牛顿插值多式可以写为：

$P_n(x) = \sum_{k=0}^{n} a_k n_k(x) = a_0 + a_1(x-x_0) + a_2(x-x_0)(x-x_1) + \dots + a_n(x-x_0)(x-x_1)\cdots(x-x_{n-1})$

其中语句 $p(x)$ 插值给定的数据点意味着 $P_n(x_i) = f(x_i), \forall i = 0, \dots, n$。牛顿基函数已定义，$n_k(x)$ 的前几项给出：

$n_0(x) = 1$

$n_1(x) = (x - x_0)$

$n_2(x) = (x - x_0)(x - x_1)$

$n_3(x) = (x - x_0)(x - x_1)(x - x_2)$

$\vdots$

$n_n(x) = (x - x_0)(x - x_1)\cdots(x - x_{n-1})$

在 $x_0$ 处求 $n$ 阶牛顿插值多式 $P_n(x)$，得到：

$P_n(x_0) = \sum_{k=0}^{n} a_k n_k(x_0) = a_0 = f(x_0)$

我们看到 $f[x_0]$ 被称为零阶差。同样，在 $x_1$ 处求 $n$ 阶牛顿插值多式 $P_n(x)$，得到：

$P_n(x_1) = \sum_{k=0}^{n} a_k n_k(x_1) = a_0 + a_1(x_1 - x_0) = f[x_0] + a_1(x_1 - x_0)$

从中我们可以提取一阶差分：

$a_1 = \frac{f[x_1] - f[x_0]}{x_1 - x_0} = f[x_0, x_1]$

其中 $f[x_0, x_1]$ 被称为一阶差分。同样，在 $x_2$ 处求 $n$ 阶牛顿插值多式 $P_n(x)$，得到：

$P_n(x_2) = \sum_{k=0}^{n} a_k n_k(x_2) = a_0 + a_1(x_2 - x_0) + a_2(x_2 - x_0)(x_2 - x_1) = f[x_0] + f[x_0, x_1](x_2 - x_0) + a_2(x_2 - x_0)(x_2 - x_1)$

从中我们可以解出 $a_2$：

$a_2(x_2 - x_1) = f[x_2] - f[x_0] - f[x_0, x_1](x_2 - x_0)$

$a_2 = \frac{f[x_2] - f[x_0] - f[x_0, x_1](x_2 - x_0)}{x_2 - x_1} = f[x_0, x_1, x_2]$

(b) $S_i(x_i) = f(x_i)$ 和 $S_i(x_{i+1}) = f(x_{i+1})$，对于每个 $i = 0, 1, \dots, n-1$。

(c) $S_{i+1}(x_{i+1}) = S_i(x_{i+1})$，对于每个 $i = 0, 1, \dots, n-2$。

(d) $S'_{i+1}(x_{i+1}) = S'_i(x_{i+1})$，对于每个 $i = 0, 1, \dots, n-2$。

(e) $S'_{i+1}(x_{i+1}) = S'_i(x_{i+1})$，对于每个 $i = 0, 1, \dots, n-2$。

并且满足以下边界条件之一：

```
$S''(x_0) = S''(x_n) = 0$ (自由边界或自然边界)
```

```
$S'(x_0) = f'(x_0)$ 和 $S'(x_n) = f'(x_n)$ (固定边界)
```

为了为给定函数 $f(x)$ 构造三次多项式，将条件 (a)-(f) 直接应用于三次多项式：

```
$S_i(x) = a_i + b_i(x-x_i) + c_i(x-x_i)^2 + d_i(x-x_i)^3$ 对于每个 $i = 0, 1, \dots, n-1$。
```

由于 $S_i(x_i) = f(x_i)$，条件 (c) 可以得到：

```
$a_{i+1} = S_{i+1}(x_{i+1}) = S_i(x_{i+1}) = a_i + b_i(x_{i+1}-x_i) + c_i(x_{i+1}-x_i)^2 + d_i(x_{i+1}-x_i)^3$
```

对于每个 $i = 0, 1, \dots, n-2$。由于项 $x_{i+1}-x_i$ 在推导中反复使用，便于为每个 $i = 0, 1, \dots, n-1$ 定义 $h_i = x_{i+1}-x_i$。如果我们还定义 $a_n = f(x_n)$，则得到：

```
$a_{i+1} = a_i + b_ih_i + c_ih_i^2 + d_ih_i^3$
```

对于每个 $i = 0, 1, \dots, n-1$ 成立。

同样地，$b_n = S'(x_n)$ 并观察到：

```
$S'_i(x_i) = b_i + 2c_i(x-x_i) + 3d_i(x-x_i)^2$
```

意味着对于每个 $i = 0, 1, \dots, n-1$，$S'_i(x_i) = b_i$。应用条件 (d) 得到：

```
$b_{i+1} = b_i + 2c_ih_i + 3d_ih_i^2$
```

对于每个 $i = 0, 1, \dots, n-2$。$S_i$ 系数之间的另一个关系是 $S''(x_n) = 2c_n$ 并应用条件 (e)。那么，对于每个 $i = 0, 1, \dots, n-1$，我们有：

```
$c_{i+1} = c_i + 3d_ih_i$
```

解出 $d_i$ 并将其代入 $a_{i+1}$ 和 $b_{i+1}$ 的方程中，对于每个 $i = 0, 1, \dots, n-1$，得到得到新方程：

```
$a_{i+1} = a_i + b_ih_i + \frac{h_i^2}{3}(2c_i + c_{i+1})$
```

以及

```
$b_{i+1} = b_i + h_i(c_i + c_{i+1})$
```

## 数值方法、算法与工具

涉及系数的最终关系通过首先求解上述两个方程 $b_i$ 得到：

```
$b_i = \frac{1}{h_i}(a_{i+1} - a_i) - \frac{h_i}{3}(2c_i + c_{i+1})$
```

然后通过缩小索引得到 $b_{i-1}$，得到：

```
$b_{i-1} = \frac{1}{h_{i-1}}(a_i - a_{i-1}) - \frac{h_{i-1}}{3}(2c_{i-1} + c_i)$
```将这些值代入索引减一的 $b_{i+1}$ 方程中，得到线性方程组：

```
$h_{i-1}c_{i-1} + 2(h_{i-1} + h_i)c_i + h_{i+1} = \frac{3}{h_i}(a_{i+1} - a_i) - \frac{3}{h_{i-1}}(a_i - a_{i-1})$
```

对于每个 $i=1, 2, \dots, n-1$。该系统仅包含 $\{c_i\}_{i=0}^n$ 作为未知数，因为 $\{h_i\}_{i=0}^n$ 和 $\{a_i\}_{i=0}^n$ 分别由 $\{x_i\}_{i=0}^n$ 的间距和 $f(x)$ 的值给出。一旦确定了 $\{c_i\}_{i=0}^n$，通过上述关系找到剩余的 $\{b_i\}_{i=0}^n$ 和 $\{d_i\}_{i=0}^n$ 并构造三次多项式 $\{S_i(x)\}_{i=0}^n$ 是简单的。

### 7.5 自然样条

自然三次样条满足条件：$S''(x_0) = S''(x_n) = 0$。这意味着 $2c_0 = 0$ 且 $S''(x_0) = 2c_0 + 6d_0h_0 = 0$，使得 $c_0=0$。两个方程 $c_0=0$ 和 $c_n=0$ 配合线性方程组

```
$h_{i-1}c_{i-1} + 2(h_{i-1} + h_i)c_i + h_{i+1} = \frac{3}{h_i}(a_{i+1} - a_i) - \frac{3}{h_{i-1}}(a_i - a_{i-1})$
```

产生由矩阵 $Ax=b$ 描述的系统，其中 $A$ 是 $(n+1) \times (n+1)$ 矩阵：

| | 1 | 0 | ... | 0 |

|---|---|---|---|---|

| $h_0$ | $2(h_0+h_1)$ | $h_1$ | | 0 |

| $0$ | 1 | $2(h_1+h_2)$ | $h_2$ | ... | 0 |

| | | ... | ... | : | : |

| 0 | 0 | 0 | $h_{n-2}2(h_{n-2}+h_{n-1})$ | $h_{n-1}$ |

| | 0 | 0 | 0 | 1 |

且 $b$ 和 $x$ 是由以下向量给出：

```
$b = \left( \frac{3}{h_1}(a_2-a_1) - \frac{3}{h_0}(a_1-a_0), \dots, \frac{3}{h_{n-1}}(a_n-a_{n-1}) - \frac{3}{h_{n-2}}(a_{n-1}-a_{n-2}) \right) \text{ 和 } x = \begin{pmatrix} c_0 \\ c_1 \\ \vdots \\ c_n \end{pmatrix}$
```

C# 实现为函数 $f(x)$ 构造三次样条插值 $S(x)$，由数字 $x_0 < x_1 < \dots < x_n$ 定义并满足自然边界条件 $S''(x_0)=S''(x_n)=0$。

```csharp
public static void NaturalCubicSpline(double[] x, double[] y, double xvalue)
{
 int i, j, m;
double S = 0.0;
double delta = 0.0;
 n = 4; // 三次样条系数个数 A,B,C,D
double[] A = new double[n + 1];
double[] B = new double[n + 1];
double[] C = new double[n + 1];
double[] D = new double[n + 1];
double[] H = new double[n + 1];
double[] X = new double[n + 1];
double[] XL = new double[n + 1];
double[] XU = new double[n + 1];
double[] XZ = new double[n + 1];
for (i = 0; i < n; i++) A[i] = y[i];
m = n - 1;
for (i = 0; i <= m; i++)
H[i] = x[i + 1] - x[i];
for (i = 1; i <= m; i++)
XA[i] = 3 * (A[i+1] - A[i]) / H[i] - (A[i] - A[i-1]) / (H[i-1]);
XL[0] = 1; XU[0] = 0; XZ[0] = 0;
for (i = 1; i < m; i++)
{
XL[i] = 2 * (x[i + 1] - x[i - 1]) - H[i] * XU[i-1];
XU[i] = H[i] / XL[i];
XZ[i] = (XA[i] - H[i] * XZ[i-1]) / XL[i];
}
XL[n] = 1; XZ[n] = 0; C[n] = 0;
for (i = 0; i <= m; i++)
{
j = m - i;
C[j] = XZ[j] - XU[j] * C[j + 1];
B[j] = (A[j+1] - A[j]) / H[j] - (C[j+1] + 2*C[j])/3;
D[j] = (C[j] - C[j-1]) / (3 * H[j-1]);
}
Console.WriteLine("\nTesting cubic splines;");
Console.WriteLine("\nInput data in (x[i],y[i]):Value to interpolate = " + xvalue + ".");
for (i = 0; i <= m; i++)
{
if (x >= x[i] && x < x[i + 1])
{
delta = x - x[i];
S = A[i]+B[i]*delta+C[i]*delta*delta+D[i]*delta*delta;
Console.WriteLine("Interpolated x value={0}={1}",xvalue,S);
}
}
static void NaturalCubicSplineTest()
{}
int = 4;
double[] xdata = new double[size];
double[] ydata = new double[size];
xdata[0] = 0.1;
xdata[1] = 0.2;
xdata[2] = 0.3;
xdata[3] = 0.4;
ydata[0] = -0.62409958;
ydata[1] = -0.28398668;
ydata[2] = 0.00660095;
ydata[3] = 0.24842440;
NaturalCubicSpline(xdata, ydata, 0.25);
Console.ReadLine();
static void Main(string[] args)
{
NaturalCubicSplineTest();
}
```

OUTPUT: Testing cubic splines;
Input data in (x[i],y[i]):Value to interpolate = 0.25.
Interpolated x value=0.25=-0.1359375

# C# 中的数值方法、算法与工具

确定一个形式为 $Ax = b$ 的线性方程组，其中

```
A = \begin{pmatrix} 2h_0 & h_0 & 0 & \dots & 0 \\ h_0 & 2(h_0+h_1) & h_1 & 0 & 0 \\ 0 & h_1 & 2(h_1+h_2) & h_2 & \dots \\ \vdots & \vdots & \vdots & \vdots & \vdots \\ 0 & 0 & h_{n-2} & 2(h_{n-2}+h_{n-1}) & h_{n-1} \\ 0 & 0 & 0 & h_{n-1} & 2h_{n-1} \end{pmatrix}
```

且 $b$ 和 $x$ 是给出的向量：

```
b = \begin{pmatrix} \frac{3}{h_0}(a_1-a_0)-3f'(a) & & & \\ \frac{3}{h_1}(a_2-a_1)-\frac{3}{h_0}(a_1-a_0) & & & c_0 \\ \vdots & \vdots & & c_1 \\ \frac{3}{h_{n-1}}(a_n-a_{n-1})-\frac{3}{h_{n-2}}(a_{n-1}-a_{n-2}) & & & c_n \\ & \frac{3}{h_{n-1}}f'(b) & & \end{pmatrix} x = \begin{pmatrix} \vdots \end{pmatrix}
```

C 实现了为函数 $f(x)$ 构建三次样条插值函数 $S(x)$，定义在点 $x_0 < x_1 < \dots < x_n$ 上，并满足边界条件 $S'(x_0)=f'(x_0)$ 和 $S'(x_n)=f'(x_n)$。
