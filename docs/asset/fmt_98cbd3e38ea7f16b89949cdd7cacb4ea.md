
```
a+d=0, \quad ad<bc; \quad \dot{x}=0, \quad x(t)=x(0)+\tilde{x}(t), \quad (4.45a–d)
```

中间情况 `(4.45b)` 对应于匀速运动 `(4.45c, d)`，一阶驻滞点 `(4.35a–c)` 附近的轨迹对应于相同广义振子的组合，它们是正交的 `(x, y)` 且耦合的可以解耦（第`4.2.3` 节）。

### 4.2.3 分解为一对耦合坐标

广义振子的线性二阶微分方程 `(4.37a, b)` 有两个特解 `$\zeta(t), \eta(t)$`，如果它们满足解耦的微分方程（与 `(4.35a–c)` 不同），则可以被称为**解耦**坐标。广义振子的正交耦合坐标是以下项的线性组合：

```
\begin{pmatrix} x(t) \\ y(t) \end{pmatrix} = \begin{bmatrix} C_1 & C_2 \\ D_1 & D_2 \end{bmatrix} \begin{pmatrix} \zeta(t) \\ \eta(t) \end{pmatrix} \quad (4.46)
```

其中 `(C_1, C_2)` 是任意积分常数，`(D_1, D_2)` 是取决于与 `(4.35b, c)` 兼容性的 `(C_1, C_2)` 的函数；因此解耦坐标 `$\zeta,\eta$` 修正了通常为斜的线性轴。一阶奇异奇异微分方程 `(4.5b)` 的曲线对应于两个独立的正交广义振子 `(4.35a–c)(4.37a, b)`，它们可以解耦为沿 `(4.46)` 轴 `($\zeta,\eta$)` 的运动，由于它们是广义振子的线性无关特解，因此它们是不同的。特征多项式 `(4.40b)` 的判别式：

```
\Delta=4(\lambda^2 - \omega_0^2) = (a+d)^2 - 4(ad-bc) = (a-d)^2 + 4bc, \quad (4.47)
```

与指定主线的二次型或二项式 `(4.8c)` 的 `(4.47) = (4.34) = (4.11a)` 一致；即沿主线的解耦坐标。因此出现三种情况：(i) `(4.8c)` 的双实根，对应于接触点（第`4.1.4` 节）和临界阻尼的广义振子（第`4.2.4` 节）；(ii) `(4.8c)` 的两个不同根，对应于（第`4.1.5` 节）鞍点（第`4.1.6` 节）或焦点、节点或单点（第`4.1.7` 节），以及过临界阻尼的广义振子（第`4.2.5` 节）；以及 (iii) `(4.8c)` 的共共轭复根，对应于（第`4.1.8 (4.1.9)` 节）亚临界阻尼广义振子的中心（渐近点）（第`4.2.6` 节）。

### 4.2.4 临界阻尼与双根

在 `(问题 80)` 的情况 `(i)` 中，特征多项式 `(4.48b)` 有实双根 `(4.48a)`：

```
$0 = \Delta = 4(\lambda^2 - \omega_0^2); \quad P_2(D) = D^2 + 2\lambda D + \lambda^2 = (D+\lambda)^2, \quad (4.48a, b)
```

线性无关的特解 `(2.85a, b) ≡ (4.49a, b)`：

```
$$\zeta(t) = e^{-\lambda t}, \quad \eta(t) = te^{-\lambda t}, \quad (4.49a, b)
```

它们分别满足一阶和二阶微分方程：

```
$0 = (D+\lambda)\zeta = \dot{\zeta} + \lambda\zeta, \quad 0 = (D+\lambda)\eta = \dot{\eta} + \lambda\eta; \quad (4.50a, b)
```

尽管解耦方程 `(4.50a, b)` 的阶数相加为 `1+2=3`，但它们是相关的，系统的实际阶数 `(4.35a–c)` 仍为 `2`。将 `(4.49a, b)` 代入 `(4.46)` 的第一行得到 `(4.51a)`：

```
$x(t) = (C_1 + C_2)e^{-\lambda t}; \quad (4.51a)
```

```
$by(t) = \dot{x}-ax = C_2 - (\lambda+a)C_1e^{-\lambda t} - C_2(\lambda+a)e^{-\lambda t}; \quad (4.51b)
```

将 `(4.51a)` 代入 `(4.35b)` 得到 `(4.51b)`。将 `(4.51b)` 与 `(4.46)` 的第二行比较确定：

```
$$\begin{bmatrix} D_1 \\ D_2 \end{bmatrix} = \frac{1}{b} \begin{bmatrix} -\lambda & a \\ 0 & -\lambda-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}. \quad (4.52)
```

将解耦坐标 `(4.49a, b)` 代入 `(4.51a, b)` 确定解耦轴 `$\zeta, \eta$` 相对于正交轴 `$x, y$` 的阶：

```
$$\begin{bmatrix} x(t) \\ y(t) \end{bmatrix} = \frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_2(\lambda+a) & -C_1(\lambda+a) \end{bmatrix} \begin{bmatrix} \zeta(t) \\ \eta(t) \end{bmatrix}. \quad (4.53)
```

### 非线性微分方程与动力学系统

消去解耦坐标 `(4.49a, b)` 中的参数 `$t$` 得到：

```
$-\lambda t = \log \zeta; \quad -\lambda\eta(t) = \zeta(t)\log\{\zeta(t)\}; \quad (4.54a, b)
```

积分曲线 `$\zeta$` `(4.54b)` 对应于（问题 `80` 到 `4.13c`）在主线 `$\zeta$` 处的（情况 `I`）拐点（图 `4.1a`）；位于解耦坐标 `(4.49a, b)` 和具有临界阻尼的耦合正交振子 `(4.53)(4.48a` 或 `$\omega_0 = \lambda$` `4.41a, b)`。

### 4.2.5 过临界阻尼与不同根

在特征多项式 `(4.40b)` 不同根的情况 `(ii)` 下：

```
$\Delta > 0; \quad P_2(D)=(D-r)(D-s), \quad r,s=\frac{a+d\pm\sqrt{\Delta}}{2}; \quad (4.55a, b)
```

特解 `(4.56a, b)`：

```
$\zeta(t)=e^\eta, \quad \eta(t)=e^\zeta; \quad \zeta=r\zeta, \quad \eta=s\eta; \quad (4.56a-d)
```

它们满足实一阶微分方程 `(4.56c, d)`。将 `(4.56a, b)` 代入 `(4.46)` 的第一行得到 `(4.57a)`：

```
$x(t)=C_1e^\eta+C_2e^\zeta; \quad by(t)=\dot{x}-ax=C_1(r-a)e^\eta+C_2(s-a)e^\zeta; \quad (4.57a, b)
```

将 `(4.57a)` 代入 `(4.35b)` 得到 `(4.57b)`。将 `(4.57b)` 与 `(4.46)` 的第二行比较确定 `4.58a` 中的系数 `$(D_1, D_2)$`：

$$\begin{matrix} D_1 \\ D_2 \end{matrix} = \frac{1}{b} \begin{bmatrix} r-a & 0 \\ 0 & s-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}; \quad y(t)=\frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_1(r-a) & C_2(s-a) \end{bmatrix} \begin{bmatrix} \zeta(t) \\ \eta(t) \end{bmatrix}; \quad (4.58a, b)

$$

同样，`(4.57a, b)=(4.58b)` 表示了斜交解耦轴 `($\zeta, \eta$)` 相对于正交耦合轴 `$(x, y)$` 的方向。消去 `(4.56a, b)` 中的时间 `$t$`：

```
$\zeta(t)=(e^\eta)'=(\eta^1)'=\{\eta(t)\}^{\gamma/s}; \quad (4.59)
```

确定了斜交解耦轴 `$\zeta, \eta$` 中的积分曲线 `(4.59)`，它们对应于正交耦合轴 `$x, y$` 中的 `(4.23a, b)`，导致

### 非稳态、非线性与混沌系统

或焦点、节点或单点（第`4.1.7` 节）和过临界阻尼的广义振子（第`4.2.5` 节）；以及 `(iii)` `(4.8c)` 的共共轭复根，对应于（第`4.1.8 (4.1.9)` 节）亚临界阻尼广义振子的中心（渐近点）（第`4.2.6` 节）。

# 非线性微分方程与动力学系统

将 `(4.67a, b)` 代入 `(4.46)` 的第一行得到 `(4.68a)`：

```
$x(t) = e^{-\lambda t} \{C_1 \cos(\delta t) + C_2 \sin(\delta t)\}; \quad (4.68a)
```

```
$y(t) = \dot{x} - ax = e^{-\lambda t} [(-\lambda + a)C_1 + C_2\delta]\cos(\delta t) - (C_1\delta + (\lambda + a)C_2)\sin(\delta t); \quad (4.68b)
```

将 `(4.68a)` 代入 `(4.35b)` 得到 `(4.68b)`，这意味着解耦斜轴 `($\phi, \psi$)` 相对于正交耦合轴 `$(x, y)$` 的方向由下式给定：

```
$$\begin{bmatrix} x(t) \\ y(t) \end{bmatrix} = \frac{1}{b} \begin{bmatrix} C_1b & C_2b \\ C_2\delta - (\lambda + a)C_1 & -C_1\delta - C_2(\lambda + a) \end{bmatrix} \begin{bmatrix} \phi(t) \\ \psi(t) \end{bmatrix}; \quad (4.69)$$
```

`(4.46) = (4.69)` 的比较导致：

```
$$\begin{bmatrix} x(t) \\ y(t) \end{bmatrix} = \begin{bmatrix} C_1 & C_2 \\ D_1 & D_2 \end{bmatrix} \begin{bmatrix} \phi(t) \\ \psi(t) \end{bmatrix}; = \frac{1}{b} \begin{bmatrix} -\lambda-a & \delta \\ \delta & -\lambda-a \end{bmatrix} \begin{bmatrix} C_1 \\ C_2 \end{bmatrix}; \quad (4.70a, b)$$
```

在 `(4.67a, b)` 中部分消去 `$t$` 得到：

```
${\{\phi(t)\}^2 +{\{\psi(t)\}^2 = \exp(-2\lambda t)}; \quad (4.71)$$
```

解耦斜轴 `($\phi, \psi$)` 中的积分曲线 `(4.67a-c)` 对应于亚临界阻尼广振子在耦合正交轴 `$(x, y)$` 中的 `(4.33a-c)`，代表：（问题 `85` 中的子情况 `VII`）`$\lambda>0$`（阻尼放大），（子情况 `V`）螺旋下落，`$\phi\to 0, \psi\to 0$` 向原点收敛，`$t\to \infty$` 是渐近点（图 `4.1ig`）；（问题 `86` 中 `$\lambda=0$` 的子情况 `VI`）无阻尼，耦合相同的无阻尼振子在斜轴 `$\phi, \psi$`（正交 `$(x, y)$` 轴）具有相同的曲线（椭圆），以原点为共同中心（图 `4.1if`）。

### 4.2.7 正交无阻尼振子的叠加

作为子情况 `VI` 的扩展，考虑两个正交无阻尼振子：

```
$x(t) = a\cos(\omega t), \quad y(t) = b\cos(\omega t - \phi) = b[\cos(\omega t)\cos\phi + \sin(\omega t)\sin\phi]; \quad (4.72a-c)$
```

具有不同的幅和相同的频率 `$\omega$`；选择初始时间 `$t=0$` 使第一个振子的相位为零 `(4.72a)`，使得第二个振子 `(4.72b)` 中的 `$\phi$` 为两个振子之间的相位差。从格式为 `(4.73)` 的第二个振子 `(4.72c)`：

```
${y(t)-b\cos(\omega t)\cos\phi\}^2=b^2\sin^2(\omega t)\sin^2\phi[1-\cos^2(\omega t)],$ (4.73)
```

可以使用第一个 `(4.72a)` 消去时间：

```
$[y(t)-\frac{b}{a}x(t)\cos\phi\}^2=b^2\{1-\frac{x(t)^2}{a^2}\}\sin^2\phi;$ (4.74)
```

这导致了方程：

```
$a^2y^2+b^2x^2-2abxy\cos\phi=a^2b^2\sin^2\phi.$ (4.75)
```

如果（问题 `87`）没有相位差 `(4.76a)`：

```
$$\phi=0:\quad 0=(ay-bx)^2, \quad y=\frac{b}{a}x; (4.76a-c)
```

即振子在同一时间通过原点（图 `4.2a`），且路径 `(4.76b)` 是由幅值比决定的直线。如果两个振子（问题 `88`）完全反相 `(4.77a)`：

```
$$\phi=\frac{\pi}{2}:\quad 0=a^2y^2+b^2x^2, \quad \frac{x^2}{a^2}+\frac{y^2}{b^2}=1; (4.77a-c)
```

即当一个振子处于最大位移时，另一个处于零位移 `(4.77b)`，轨迹是一个椭圆（图 `4.2b`），其轴沿坐标轴，且半轴等于幅值。

### 4.2.8 同相、反相和中间情况

二维谐振子由具有相同频率、不同幅值和相位差 `$\theta$` 的运动叠加组成，这导致：

- (i) 相位差为零，得到斜率为 `b/a` 的通过原点的直线；
- (ii) 反相情况 `$\phi = \pi/2$`，得到一个沿坐标轴、半轴为 `$(a, b)$` 的椭圆，中心在原点；
- (iii) 在所有 `0 < \phi < \pi/2` 的情况下，中心保持在原点，且椭圆的轴通过角度 `$\theta$` 旋转（图 `4.3`），通过以下方式联系：

```
$z = x + iy, \quad \xi = \zeta + i\eta; \quad \xi = e^{-i\theta}\zeta, \quad (78a)
```

在复坐标系中：

```
$x + iy = (\cos\theta + i\sin\theta)(\xi + i\eta) \qquad \xi + iy = (\cos\theta - i\sin\theta)(x + iy); \quad (78e, f)
```

平面上的点由复数表示，对应于相位的变化。对应的实坐标变换为：

```
$x = \zeta\cos\theta - \eta\sin\theta, \quad y = \zeta\sin\theta + \eta\cos\theta, \quad (79a)
```

```
$\zeta = x\cos\theta + y\sin\theta, \quad \eta = -x\sin\theta + y\cos\theta, \quad (79c)
```

沿顺时针方向旋转角度 `$\theta$` `(79a)`，即逆时针方向旋转 `(79c)`，通过将 `$\theta$` 替换为 `$-\theta$` 得到。将 `(79a, b)` 代入 `(4.75)` 得到：

```
$a^2b^2\sin^2\varphi = \zeta^2 [a^2\cos^2\theta + b^2\cos^2\theta - ab\cos\varphi] (20)]$
```

$$+\eta^2 [a^2\cos^2\theta + b^2\sin^2\theta + ab\cos\varphi] \quad (4.80)$$

$$$$+\zeta\eta [(a^2 - b^2)\sin(2\theta)].$$

```

当 `(4.80)` 中 `$\zeta$` 的系数消失时，椭圆的轴与 `($\xi, \eta$)` 坐标轴对齐（图 `4.2b`）；即对于旋转角度 `(4.81a)`：

```

$2\cos\varphi\cot(2\theta) = \frac{a^2 - b^2}{ab} = \frac{a}{b} \cdot \frac{b}{a} \dots \quad \left(\frac{\xi}{A}\right)^2 + \left(\frac{\eta}{B}\right)^2 = 1, \quad (4.81a, b)$

```

导出轴为 `(4.82a, b)` 的椭圆方程 `(4.81b)`：

```

$A^2 = \frac{a^2b^2 \sin^2\varphi}{a^2\sin^2\theta + b^2\cos^2\theta - ab\cos\theta\cos(2\theta)}, \quad (4.82a)

```

```

$B^2 = \frac{a^2b^2 \sin^2\varphi}{a^2\cos^2\theta + b^2\sin^2\theta}, \quad (4.82b)

```

已经证明对于问题 `(88)`，具有相同频率 `$\omega$` 和幅值 `$(a, b)$` 的两个正交振子 `(4.72a, b)` ：
- (i) 对于问题 `(88)`，任意相位差 `(4.83a)` 椭圆 `(4.2c)` `(4.79c, d)`，其半轴 `(4.82a, b)` 沿角度为 `(4.81a)` 的 `$\theta$` 和 `$\theta + \pi/2$` 的直线：
