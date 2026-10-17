
考虑位字符串 $x = \dots0101010101\dots$ 和左移位映射 $\sigma$

img/e89136779f66a50f0bd7e926e51d2_312_3.png

其中括号表示位置 0。找到 $x$ 和 $\sigma^2$ 之间的距离。

# 第 11 章

# 求解方程

## 11.1 引言

在本章中，我们考虑非线性方程的数值积分方法（Scheid [219], Fröberg [76], Hairer 等 [97]）。几乎所有的非线性方程都无法求闭式解。必须应用数值方法。例如，如果方程源自保守哈密顿系统，则数值方案应该保持总能量，这是一个运动常量。对于非线性方程，离散化可能会导致混沌映射。非线性方程的稳定点在离散化后变得不稳定。我们还会发现所谓的伪解（也称为鬼解）。

我们考虑自治一阶

```
$\frac{du}{dt} = f(u)$
```

和非自治一阶常微分方程组

```
$\frac{du}{dt} = g$
```

我们讨论了欧拉方法、李级数技术（与泰勒级数技术密切相关）以及 Runge-库塔-费尔堡五阶法。分子动力学中的 Verlet 方法也被介绍。最后，讨论了具有第一积分的常微分方程组的数值积分。

## 294 第 11 章 常常微分方程的解法

**定理。**（存在性与唯一性）考虑一阶微分方程 $du/dt = f(u)$，其中 $f$ 及其对 $u_i$ 的一阶偏导数在开集 $U \subset \mathbb{R}^n$ 上是连续的。那么对于任意实数 $t_0$ 和实向量 $\mathbf{u}_0$，在 $t_0$ 附近存在一个开区间，在该区间上存在一个满足初始条件 $u(t_0) = \mathbf{u}_0$ 的解，且该解是唯一的。

**定义。** 令 $U$ 为 $\mathbb{R}^n$ 中的一个开集。如果函数 $f$ 在 $U$ 上被称为 Lipschitz 连续的，则存在一个常数 $L$ 使得

$|f(\mathbf{u}) - f(\mathbf{v})| \le L|\mathbf{u} - \mathbf{v}|$

对于 $U$ 中的所有 $\mathbf{u}, \mathbf{v}$ 均成立。常数 $L$ 称为 $f$ 的 *Lipschitz 常数*。

**示例。** 考虑非线性一阶微分方程

$\frac{du}{dt} = -u^{1/3}, \quad u(0) = u_0 > 0.$

积分得初值问题的解为

$u(t) = \left( -\frac{2t}{3} + u_0^{2/3} \right)^{3/2}, \quad 0 \le t \le \frac{3}{2}u_0.$

该方程不满足 Lipschitz 条件。

同一个一阶微分方程组的两个相邻解之间的分离速率不大于

$e^{Lt}$

其中 $L$ 是该微分方程组的 Lipschitz 常数。*Gronwall 不等式*是流作为初始条件的函数的连续性的基础（Gronwall [90], Bellman [23]）。

**定理。** 令 $\mathbf{f}$ 定义在 $\mathbb{R}^n$ 中的开集 $U$ 上。假设 $\mathbf{f}$ 在变量 $\mathbf{u}$ 上具有 Lipschitz 常数 $L$。令 $\mathbf{v}(t)$ 和 $\mathbf{w}(t)$ 为 $du/dt = \mathbf{f}(\mathbf{u})$ 的解，并令 $[t_0, t_1]$ 为两个解域的一个子集。

$|\mathbf{v}(t) - \mathbf{w}(t)| \le |\mathbf{v}(t_0)|e^{L(t-t_0)}$

对于 $[t_0, t_1]$ 中的所有 $t$。

这意味着相邻的解的发散速度不会快于由微分方程 Lipschitz 常数决定的指数状态。

## 11.2 欧拉法

用欧拉法数值求解一阶常微分微分方程组

$\frac{d\mathbf{u}}{dt} = \mathbf{g}(\mathbf{u}, t)$

这涉及使用差分方程对于参数 $t_k$ 计算一组离散的 $\mathbf{u}_k$ 值：

$\mathbf{u}_{k+1} = \mathbf{u}_k + hg(t_k, \mathbf{u}_k), \quad h := t_{k+1} - t_k.$

这里 $h$ 是步长。通过在关于 $t$ 的带余项的泰勒序列中展开 $u(t+h)$，可以看出

$\frac{u(t+h) - u(t)}{h} = \frac{u(t) + hu'(\xi) + \frac{1}{2}h^2u''(\xi) - u(t)}{h} = u'(t) + \frac{1}{2}hu''(\xi)$

$(t \le \xi \le t+h)$，只要解 $\mathbf{u}$ 的二阶导数在感兴趣的时间范围内是有界的，那么欧拉法的左侧就是其所取代导数的 $O(h)$ 近似。随着 $h$ 趋于零，欧拉近似越来越好地表示原始微分方程；即它与微分方程是一的。关于误差估计的更多细节，参考 Hairer 等人 [97]。

**示例。** 考虑非线性一阶微分方程

$\frac{du}{dt} = u(1-u)$

带有初始条件 $u(t=0) = u_0 > 0$。该非线性微分方程允许固定点

$u_1^* = 0, \quad u_2^* = 1.$

固定点 $u_1^* = 0$ 是不稳定的，而固定点 $u_2^* = 1$ 是稳定的。这可以通过研究变分方程看出。欧拉法导致差分方程

$\mathbf{u}_{k+1} = \mathbf{u}_k + hf(\mathbf{u}_k) = \mathbf{u}_k + hu_{\mathbf{u}_k}(1-\mathbf{u}_k), \quad k=0, 1, 2, \dots$

其中 $h$ 是步长。注意差分方程也允许 0 和 1 这两个点。在 Java 程序 `Euler.java` 中，我们设置 `h = 0.005`。初始值为 `u0 = 0.1`。我们发现随着 `k -> infinity`，`u_k` 趋于稳定固定点 `u* = 1`。

```java
import java.awt.*;
import java.awt.event.*;
import java.awt.Graphics;

public class Euler {
    // ... (代码逻辑保持不变)
}
```

## 11.3. 李级数法

如果要在所有连续且连续可导函数的范围内确定解的唯一性，可以通过实分析的已知方法来证明。

上述讨论的李级数可以限制在实数域内。对于我们的数值研究，我们考虑自律微分方程组：

```
\frac{du}{dt} = f(u)
```

其中 `u = (u1, ..., un)^T`。设 `f_j` (`j=1, ..., n`) 为定义在 `R^n` 上的解析函数。考虑向量场：

```
V = \sum_{j=1}^n f_j(u) \frac{\partial}{\partial u_j}
```

对于足够小的 `t`，自律系统初值问题的解可以用李级数给出：

```
u_j(t) = \exp(tV)|u_j|_{u=u(0)}
```

其中 `j=1, 2, ..., n`。在大多数情况下，展开指数函数得到：

```
u_j(t) = u_j(0) + tV(u_j)|_{u=u(0)} + \frac{t^2}{2}V(V_j)|_{u=u(0)} + \cdots$
```

其中 `j=1, 2, ..., n`。在实际情况下，对于微分方程的数值积分只需取该展开的有限项。这种方法已在第3章用于耗散系统。另一种近似方法是考虑：

```
\exp(t(V_1 + V_2)) = \prod_{j=1}^n \exp(c_j t V_1)\exp(d_j t V_2) + O(t^{n+1})
```

如果向量 `V` 可以写为：

```
V = V_1 + V_2.
```

在二阶范围内我们有：

```
\exp(t(V_1 + V_2)) = \exp(\frac{t}{2}V_1)\exp(\frac{t}{2}V_2) + O(t^2)
```

其中 `k=1` 且 `c1=d1=1`。在三阶范围内有：

```
\exp(t(V_1 + V_2)) = \exp(\frac{t}{2}V_1)\exp(\frac{t}{2}V_2)\exp(\frac{t}{2}V_1) + O(t^3)
```

这些是辛结构积分器（Yoshida [280]）。

## 第11章. 求解常微分方程

动力系统在复时间平面上的奇异结构研究对于具有混沌行为的系统具有意义。C++的标准模板库（STL）提供了复数类型。在：

```
complex<double> z(x,y)
```

`x` 是复数的实部，`y` 是复数的虚部。该类在以下程序中用于实现李级。我们在复域内研究洛伦兹模型。

```cpp
// complexlie.cpp

#include <iostream>
#include <complex>
using namespace std;

int main(void)
{
    complex<double> r(40.0,0.0), s(16.0,0.0), b(4.0,0.0);
    complex<double> count(0.0,0.0);
    complex<double> eps(0.0,0.01);
    complex<double> half(0.5,0.0);
    complex<double> u1(0.8,0.0), us2(0.8,0.0), us3(0.8,0.0);
    complex<double> V1, V2, V3, W1, W2, W3;

    while (abs(count) < 2.0)
    {
        u1 = us1; u2 = us2; u3 = us3;
        V1 = s*(u1-u2); V2 = -u2-u1+u3+r*u1; V3 = u1*u2-b*u3;
        W1 = s*(u3-u1) + s*(-u2-u1+u3+r*u1);
        W2 = u2+u1*u3-r*u1-s(u3)*(u1*u2-b*u3)*u1*r*s*(u2-u1);
        W3 = s*u2*(V1)+(-u2-u3+r*u3)*u1-b*(u1*u2-u3));
        us1 = u1+eps+V1+half*eps*W1;
        us2 = u2+eps+V2+half*eps*W2;
        us3 = u3+eps+V3+half*eps*W3;
        count += eps;
    }

    cout << "us1 = " << us1 << endl;
    cout << "us2 = " << us2 << endl;
    cout << "us3 = " << us3 << endl;
    return 0;
}
```

## 11.4. RUNGE-KUTTA-FEHLBERG 方法

Runge-Kutta-Fehlberg 方法（Shid [219], Fehlberg [76], Hairer等 [97]）开发是为了避免计算高阶导数。在这些导数的地方，使用了给定函数 `g(u,t)` 的额外值，这本质上复制了泰勒项式的精度。我们给出了五阶 Runge-Kutta-Fehlberg 方法的公式。假设常微分方程组的初值问题是一阶的，其中 `u(0) = u0`。典型的积分步长 `h` 在 `t0+h` 处的公式为：

```
u(t) = u_0 + h \sum_{k=0}^{5} c_k g^{(k)},
```

其中 `g^{(0)} = g(u,0)`，`u(t) = u_0 + h \sum_{j=0}^{k-1} b_j g^{(j)}` 近似精确解。系数 `c_k` (`k=0, 1, ..., 5`) 为：

```
c_0 = 16/135, c_1 = 0, c_2 = 6656/12825, c_3 = 28561/56430, c_4 = 9/50, c_5 = 2/55
```

系数 `b_j` (`j=0, 1, ..., 5, k=0, 1, ..., 4`) 为：

```
b_0 = 0, b_1 = 1/4, b_2 = 0, b_3 = 0, b_4 = 0,
```

对于 `k=4` 时：

```
b_0 = 19/2197, b_1 = -7200/2197, b_2 = 7296/2197, b_3 = 3/4, b_4 = 0,
```
