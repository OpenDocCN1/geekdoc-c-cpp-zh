
```java
// QuarticPotential.java

import java.awt.*;
import java.awt.event.*;
import java.awt.Graphics;

public class QuarticPotential extends Frame {
    public QuarticPotential() {
        setSize(600,500);
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent event) { System.exit(0); }
        });
    }

    public void system(double h, double t, double[] u, double[] hf) {
        double r = 0.15;
        hf[0] = h*(1.0-r)*u[2]/2.0-u[3];
        hf[1] = h*(1.0-r)*u[3]/2.0-u[2];
        hf[2] = h*u[0];
        hf[3] = h*u[1];
    }

    public void map(double[] u, int steps, double h, int N) {
        double[] uk = new double[6];
        double tk;
        double[] a = {0.0, 1/4.0, 3.0/8.0, 12.0/13.0, 1.0, 1/2.0};
        double[] c = {16.0/135.0, 0.0, 6656.0/12825.0, 28561.0/56430.0, -9.0/50.0, 2.5/55.0};
        double[][] b = new double[6][6];
        b[0] = {0.0, 0.0, 0.0, 0.0, 0.0, 0.0};
        b[1] = {0.25, 0.0, 0.0, 0.0, 0.0, 0.0};
        b[2] = {3.0/32.0, 9.0/32.0, 0.0, 0.0, 0.0, 0.0};
        b[3] = {1932.0/2197.0, -720.0/2197.0, 7296.0/2197.0, 0.0, 0.0, 0.0};
        b[4] = {439.0/216.0, -8.0, -3680.0/513.0, -845.0/4104.0, 0.0, 0.0};
        b[5] = {-8.0/275.0, 2.0, -3544.0/2565.0, 1859.0/4104.0, -11.0/40.0};

        double[] f = new double[N];
        int i, j, l, k;
        for(i=0; i<steps; i++) {
            system(h, t, uk, f); // 注意：原始 OCR 在此处有逻辑错误
            system(h, t, uk, hf); // 假设的积分逻辑
            for(k=0; k<6; k++) tk += a[k]*h;
            for(l=0; l<N; l++) uk[l] = u[l];
            for(j=0; j<k-1; j++) uk[j] += b[k][j]*f[j];
        }
    }

    public void paint(Graphics g) {
        g.drawRect(30,30,570,400);
    }

    public static void main(String[] args) {
        Frame f = new QuarticPotential(); f.setVisible(true);
    }
}
```

## 4.4. 练习

(1) 考虑氦原子（一个原子核和两个电子）经典三体问题的运动（Yamamoto 和 Kaneko [278]）：

```math
$M\frac{d^2r_0}{dt^2} = \frac{r_1-r_0}{r_{10}^3}e^2 + \frac{r_2-r_0}{r_{20}^3}e^2$
$\frac{d^2r_1}{dt^2} = \frac{r_0-r_1}{r_{10}^3}e^2 + \frac{r_2-r_1}{r_{12}^3}e^2$
$\frac{d^2r_2}{dt^2} = \frac{r_0-r_2}{r_{20}^3}e^2 + \frac{r_1-r_2}{r_{12}^3}e^2$
```

第一个粒子（粒子 0）带有 2e 电荷的原子核，$M$ 是核与电子的质量比。两个电子（粒子 1 和 2）带有 -e 电荷。

(2) 摆动阿特拉斯机由哈密顿函数描述：

```math
$H_{\mu}(r, \theta, p_r, p_{\theta}) = \frac{p_r^2}{2m(1+\mu)} + \frac{p_{\theta}^2}{2mr^2} + mgr(\mu-\cos \theta)$
```

其中 $\mu > 0$ 是分叉参数。运动方程为：

```math
$\frac{\partial dr}{dt} = \frac{p_r}{m(1+\mu)}$
$\frac{\partial d\theta}{dt} = \frac{p_{\theta}}{mr^2}$
$\frac{\partial dp_r}{dt} = \frac{p_r^2}{mr^3} - mg(\mu-\cos \theta)$
$\frac{\partial dp_{\theta}}{dt} = -mgr\sin \theta$
```

证明当 $\mu=10$ 时可以找到混沌行为。

(3) 为了寻找具有柱对称性的系系中粒子运动的第三积分，Syntopoulos 等人 [47] 被引导得出具有两个自由度的哈密顿函数：

```math
$H(p, q) = \frac{1}{2}(p_1^2+p_2^2) + \frac{1}{2}(q_1^2+q_2^2) - q_1q_2.$
```

# 第 4 章。非线性哈密顿系统

研究哈密顿运动方程的固定点。

(4) 考虑由哈密顿函数给出的六角势能中的动力学（Zaslavskii 等 [282]）：

```
$H(\mathbf{p}, \mathbf{q}) = \frac{1}{2}(p_1^2 + p_2^2) + \sum_{j=1}^{3} q_1 \cos(2\pi j/3) + q_2 \sin(2\pi j/3).$
```

研究该哈密顿函数的混沌行为。

(5) 考虑线性微分方程组：

```
$$\frac{d\mathbf{u}}{dt} = A(t)\mathbf{u}$$
```

其中 $A(t)$ 是可微 $n \times n$ 矩阵。考虑由独立解 $u_i(t)$ ($j=1, \dots, n$) 组成的基础矩阵 $U(t) = (u_1(t), \dots, u_n(t))$。证明：

```
$$\det(U(t)) = \det U(0) \exp\left(\int_{0}^{t} tr(A(\tau))d\tau\right)$$
```

其中 tr 表示迹。

(6) 考虑单参数哈密顿函数族：

```
$H(p_1, p_2, q_1, q_2) = \frac{1}{2}(p_1^2 + p_2^2 + (q_1^2 q_2^2)^{1/\gamma})$$
```

其中 $0 \leq \gamma \leq 1$。在 $\gamma \rightarrow 0$ 的极限下我们得到双曲线。增加 $\gamma$ 意味着台球壁逐渐软化，当 $\gamma = 1$ 时，我们得到 $q_1^2 q_2^2$。

- (i) 证明这些系统中的周期轨道可以使用使用三个字母 [2,1,0] 表表的符号动力学来描述。
- (ii) 证明这些角区域内的运动可以用绝热近似处理。

(7) 考虑质量为 $m$、电荷为 $q$ 的带电粒子在磁矩为 $\mathbf{M}$ 的磁偶极场中的非相对性运动。它由哈密顿函数描述：

```
$H(\mathbf{p}, \mathbf{r}) = \frac{1}{2m}(\mathbf{p} - q\mathbf{A}(\mathbf{r}))$
```

其中矢量势 $\mathbf{A}$ 由下给出：

```
$$\mathbf{A}(\mathbf{r}) = \frac{1}{r^3}(\mathbf{M} \times \mathbf{r})$$
```

证明通过沿 $\mathbf{M}$ 方向选择 $z$ 轴，即 $\mathbf{M} = (0, 0, M)$），我们有：

```
$$H(p_x, p_y, x, y) = \frac{1}{2} \left( (p_x + \frac{ay}{r^3})^2 + (p_y - \frac{ax}{r^3})^2 + p_z^2 \right).$$
```

# 第 5 章

## 非线性耗散系统

## 5.1 固定点与稳定性

我们考虑具有混沌行为的非线性耗散系统（Arrowsmith and Place [9], Marek and Schreiber [168], Seydel [225], Hirsch and Smale [115], Smale [230], Guckenheim and Holmes [91]）。特别研究了 Lorenz 模型（Lorenz [159], Sparrow [228]）。假设系统的动力学行为由自治一阶微分方程组的解曲线建模（*动力系统*）：

```
$$\frac{du}{dt} = f(u), \quad f : U \to \mathbb{R}^n$$
```

其中 $U$ 是 $\mathbb{R}^n$ 的开集。我们假设 $f$ 是 $C^1$。在大多数应用中，我们有 $\text{div} f < 0$，其中 $\text{div}$ 表示散度。在大多数情况下，$f_j$ 是多项式。如果 $f_j : \mathbb{R}^n \to \mathbb{R}$ 是解析函数，则初值问题的解可以表示为（*李级数*）：

```
$$\mathbf{u}(t) = \exp(t)\mathbf{u}|_{\mathbf{u}_0}$$
```

$V = f_1(\mathbf{u})\frac{\partial}{\partial u_1} + \dots + f_n(\mathbf{u})\frac{\partial}{\partial u_n}$

如果点 $\mathbf{u}^* \in U$ 被称为动力系统的*固定点*（也称为*平衡点*或驻点），则：

```
$$f(\mathbf{u}^*) = \mathbf{0}.$$
```

根据解的唯一性，没有其他解曲线可以通过 $\mathbf{u}^*$。令：

```
$$\Phi_t : U \to \mathbb{R}^n$$
```

为动力系统相关的流。集合 $U \subset \mathbb{R}^n$ 是一个开集。

对于 $U$ 中的每个 $\mathbf{u}$，映射 $t \to \Phi(t, \mathbf{u}) = \Phi_t(\mathbf{u})$ 是 $t=0$ 时通过 $\mathbf{u}$ 的解；它在某个开区间内定义。如果 $\mathbf{u}^*$ 是固定点，则：

```
$$\Phi_t(\mathbf{u}^*) = \mathbf{u}^*$$
```

对于所有 $t \in \mathbb{R}$。$\mathbf{u}^*$ 是矢量场 $\mathbf{f}$ 的奇异点。

假设 $\mathbf{f}$ 是线性的。我们写 $f(\mathbf{u}) = A\mathbf{u}$，其中 $A$ 是 $\mathbb{R}^n$ 上的线性算子（方阵）。原点 $0 \in \mathbb{R}^n$ 是固定点。如果 $\lambda < 0$ 大于 $A$ 的特征值的实部，则解 $\Phi_t(\mathbf{u})$ 指数级趋于 $0$：

```
$$|\Phi_t(\mathbf{u})| \le Ce^{mt}$$
```

对于某些 $C > 0$。现在假设 $\mathbf{f}$ 是固定点 $0 \in \mathbb{R}^n$ 的 $C^1$ 矢量场。考虑 $n \times n$ 矩阵：

$$A := Df(\mathbf{u}) = (\partial f/\partial \mathbf{u})$$

注：第 184-185 页的 OCR 文本具有高度冗余性，我已逻辑上合并了唯一的数学内容。

# 第5章 非线性耗散系统

**定义。** 向量场 $f$ 的奇异点 $u^*$，如果 $Df(u^*)$ 的特征特征值实部都不为零，则称其为双形。

**示例。** 考虑动力系统

```
$\frac{du_1}{dt} = u_2, \quad \frac{du_2}{dt} = -u_1 - ru_2, \quad r \neq 0$
```

那么唯一的固定点是 $(u^*_1, u^*_2) = (0,0)$。$(0,0)$ 处的雅可比矩阵为

```
$J(0,0) = \begin{pmatrix} 0 & 1 \\ -1 & -r \end{pmatrix}$
```

特征值为 $(-r \pm \sqrt{r^2-4})/2$。对于所有 $r \neq 0$ 的值，特征值均具有非实部。因此固定点 $(0,0)$ 是双形固定点。

如果 $u^*$ 是 $f$ 的奇异点，那么它是流 $du/dt = f(u)$ 的固定点。因此，如果流 $\exp(Df(u^*)t)u$（$du/dt = f(u)$ 的线性化）是双形的，则 $u^*$ 是 $f$ 的双形奇异点。有时便于区分 $Df(u^*)$ 至少有一个零特征值的非双形奇异点。这些点往往是非单纯的。

**定理。** (Hartman-Grobman)  $u^*$ 为 $du/dt = f(u)$ 的双形固定点，其流为 $\Phi_t : U \subseteq \mathbb{R}^n \to \mathbb{R}^n$。则存在 $u^*$ 的一个邻域 $N$，在该邻域上 $\Phi_t$ 与线性流 $\exp(Df(u^*)t)u$ 拓扑共。

不变流形*定理*也适用于流。我们有

```
$W_{loc} := \{ \mathbf{u} \in U \mid \Phi_t(\mathbf{u}) \to \mathbf{u}^* \}$
```

```
$W_{loc}^s := \{ \mathbf{u} \in U \mid \Phi_t(\mathbf{u}) \to \mathbf{u}^* \}$
```

当 $t \to -\infty$ 时。全局稳定不稳定流形 $W^*$ 和 $W^u$ 通过对实数 $t > 0$ 取 $\Phi_{-t}(W_{loc}^s, W_{loc}^u)$ 分并定义。

以下对双形固定点进行分类。

**定理。** $u^*$ 为 $du/dt = f(u)$ 的双形固定点，其流为 $\Phi_t : U \subseteq \mathbb{R}^n \to \mathbb{R}^n$。则存在 $u^*$ 的一个邻域 $N$，在该邻域上 $\Phi_t$ 与线性微分方程组的流拓扑等。

```
$\frac{du_s}{dt} = -\mathbf{u}_s, \quad \mathbf{u}_s \in \mathbb{R}^{n_s} \\ \frac{du_u}{dt} = \mathbf{u}_u, \quad \mathbf{u}_u \in \mathbb{R}^{n_u}$
```

其中 $n_u = n-n_s$。这里 $n_s$ 是 $\exp(Df(u^*)t)$ 的稳定特征空间的维。

## 5.1. 固定点的稳定性

**示例。** 考虑 Lorenz 模型固定点的稳定性。Lorenz 模型是作为下方流体层中对流的偏微分方程的近似（Bénard 问题）。其形式为：

```
\frac{du_1}{dt} = \sigma(u_2 - u_1)\\
\frac{du_2}{dt} = -u_1u_3 + ru_1 - u_2\\
\frac{du_3}{dt} = u_1u_2 - bu_3$
```

$\sigma, r$ 和 $b$ 是正常数。固定点由代数方程组确定

```
$u_2^2 - u_1^2 = 0$
$-u_1u_3 + ru_1 - u_2^2 = 0$
$u_1u_2 - bu_3 = 0$
```

我们发现对于所有的参数值 $\sigma, r$ 和 $b$，都有 $u_1^* = u_2^* = u_3^*$。如果 $r < 1$，该固定点是吸引的（汇点）。如果 $r$ 大于 1，该固定点失去其吸引特性（其中一个特征值变为正），并出现了两个新的固定定点。对于 $r > 1$，我们找到了固定点

```
$u_1^* = u_2^* = \pm\sqrt{b(r-1)}, \quad u_3^* = r-1$.
```

使用 SymbolicC++ 的 C++ 程序 `lorenzfix.cpp` 从变分方程寻找特征值的特征方程，然后确定固定点 (0,0,0) 的稳定性。参数值为 $r = 40, \sigma = 16$ 和 $b = 4$。对于 $r > 1$，原点 (0,0,0) 变得不稳定，即三个特征值之一变为正（而另外两个保持为负）。
