
```
$x_1 = r \cos(\theta_1)$
$x_2 = r \sin(\theta_1) \cos(\theta_2)$
$x_3 = r \sin(\theta_1) \sin(\theta_2) \cos(\theta_3)$
$x_4 = r \sin(\theta_1) \sin(\theta_2) \sin(\theta_3) \cos(\theta_4)$
$x_{n-1} = r \sin(\theta_1) \sin(\theta_2) \sin(\theta_3) \cdots \sin(\theta_{n-2}) \cos(\theta_{n-1})$
$x_n = r \sin(\theta_1) \sin(\theta_2) \sin(\theta_3) \cdots \sin(\theta_{n-2}) \sin(\theta_{n-1})$
```

或者

```
$x_k = r \cos(\theta_k) \prod_{\ell=1}^{k-1} \sin(\theta_\ell), \quad \text{for } k=1, 2, \dots, n-1$
$x_n = r \prod_{\ell=1}^{n-1} \sin(\theta_\ell)$
```

其中 $r=1, -\pi \leq \theta_1 \leq \pi,$ 以及 $0 \leq \theta_j \leq \pi, 2 \leq j \leq n-1$。逆变换为：

```
$$\theta_k = \arccos\left(\frac{x_k}{\sqrt{r^2 - \sum_{j=1}^{k-1} x_j^2}}\right), \quad \text{for } k=1, 2, \dots, n-2$$
$\theta_{n-1} = \arctan\left(\frac{x_n}{x_{n-1}}\right)$
```

该变换的雅可比行列式 $J$ 为：

```
$J = r^{n-1} \prod_{p=1}^{n-1}(\sin(\theta_p))^{n-p-1}$
```

$\mathbb{R}^3$ 问题中其他有用的坐标系有：长椭球坐标由 $(a > 0)$ 给出：

```
$x_1(\eta, \alpha, \phi) = a \sinh(\eta) \sin(\alpha) \cos(\phi)$
$x_2(\eta, \alpha, \phi) = a \sinh(\eta) \sin(\alpha) \sin(\phi)$
$x_3(\eta, \alpha, \phi) = a \cosh(\eta) \cos(\phi)$
```

注意 $\cosh^2(\eta) - \sinh^2(\eta) = 1$。在三维欧几里得空间中，扁椭球坐标由 $(a > 0, \phi \in [0,2\pi)$ 给出：

```
$x_1(\eta, \alpha, \phi) = \cosh(\eta)\sin(\alpha)\cos(\phi)$
$x_2(\eta, \alpha, \phi) = \cosh(\eta)\sin(\alpha)\sin(\phi)$
$x_3(\eta, \alpha, \phi) = \sinh(\eta)\cos(\phi)$
```

在三维欧几里得空间中，抛物线坐标由 $(\eta > 0, \xi > 0)$ 给出：

```
$x_1(\xi, \eta, \phi) = \xi\cos(\phi)$
$x_2(\xi, \eta, \phi) = \xi\sin(\phi)$
$x_3(\eta, \alpha, \phi) = \frac{1}{2}(\xi^2 - \eta^2)$
```

在三维欧几里得空间中，球锥坐标由给出（sn, cn, dn 是 Jacobi 椭圆函数）：

```
$x_1(r, \mu, \nu) = r sn(\mu, k)sn(\nu, k)$
$x_2(r, \mu, \nu) = r\frac{1}{k}cn(\mu, k)cn(\nu, k)$
$x_3(r, \mu, \nu) = r\frac{1}{k^2}dn(\mu, k)dn(\nu, k)$
```

其中 $k$ 是模 $(0 \le k \le 1)$ 且 $k' = \sqrt{1-k^2}$。注意：

```
$sn(0,k) = 0, \quad cn(0,k) = 1, \quad dn(0,k) = 1$
$sn(x,0) = \sin(x), \quad cn(x,0) = \cos(x), \quad dn(x,0) = 1$
```

并且 Jacobi 椭圆函数满足恒等式：

```
$sn^2(x,k) + cn^2(x,k) = 1$
$dn^2(x,k) - k^2cn^2(x,k) = 1 - k^2$
$sn^2(x,k) + dn^2(x,k) = 1$
```

此外，我们还有恒等式：

```
$$\frac{d^2}{dx^2}sn(x,k) = 2k^2sn^3(x,k) - (1+k^2)sn(x,k).$$
```

该恒等式可以用于求解线性微分方程：

```
$$\frac{d^2u}{dx^2} = Au + Bu^3.$$
```

## 12.4 微分形式与 Cartan 形式

使用微分形式（Cartan [33], Flanders [73], von Westholz [265], Steeb [244], Zizza [287]）求解约束最小化问题相比于格朗日乘子法的优势在于，格朗日乘子被消除了。因此，需要求解的方程数量较少。

如上述，对于形式为 $g(x) = c$ 的单一约束最大化或最小化 $f$，格朗日条件的方法利用了以下观察：在临界点，$f$ 和 $g$ 的等高线是相切的。微分形式之间的方程等价于格朗日条件：

```
$df|_p = \lambda dg|_p$
```

几何上，格朗日条件意味着 $f$ 的等高线与约束的切线是一致的。对于 $m=1$ 的情况，我们从约束中得到了额外的方程：

```
$df \wedge dg = 0$
```

其中 $\wedge$ 表示外积，$d$ 表示外导。**示例**：对于 $f$ 的最优值，我们发现 $f(x_1, x_2) = x_1^2 + x_2^2$ 受到约束 $g(x_1, x_2) = x_1 + x_2 = 1$ 的限制。对于微分，我们得到：

因此，我们必须求解这两个方程：

$x_1x_2(x_1 - 1) = 0, \quad (3 - x_1)^3 - x_2^2 = 0.$

$x_1 = 0$的情况意味着 $x_2 = \sqrt{27}$，且 $f(x_1, 0, x_2 = \sqrt{27}) = 0$。$x_1 = 1$的情况意味着 $x_2 = \sqrt{8}$，且 $f(x_1 = 1, x_2 = \sqrt{8}) = -1$。$x_2 = 0$的情况产生全局最大值 $x_1 = 3$。

非相对论和相对论经典力学可以使用不同的形式。在非相对论经典力学中，起点是微分形式（也称为*卡坦形式*）

$$\alpha = \sum_{i=1}^N \sum_{j=1}^3 p_{ij}dq_{ij} - H(p_{11}, \dots, p_{N3}, q_{11}, \dots, q_{N3})dt$$

其中 $H$ 是哈密顿函数，$N$ 是粒子数。对于 $\Gamma = \{p_{11}, \dots, p_{N3}, q_{11}, \dots, q_{N3}, t\}$ 中的一条闭合曲线 $C$，若要求积分

![](img/e89136779f66a50f0bd7e926e5daf1d2_348_0.png)

对于任何通过点沿轨迹任意位移得到的 $C$ 的形变都是不变的，则导出正则方程（哈密顿运动方程）

$$\frac{dp_{ij}}{dt} = \frac{\partial H}{\partial q_{ij}}, \quad \frac{dq_{ij}}{dt} = \frac{\partial H}{\partial p_{ij}}$$

因此，运动方程由下式确定：

$Z|d\alpha = 0$

其中 $Z$ 是*矢量场*

$$Z = \sum_{i=1}^N \sum_{j=1}^3 (V_{ij}(\mathbf{p}, \mathbf{q}) \frac{\partial}{\partial p_{ij}} + W_{ij}(\mathbf{p}, \mathbf{q}) \frac{\partial}{\partial q_{ij}}) + \frac{\partial}{\partial t}$$

以及微分形式与矢量场的 $f$-线性收缩（内积），$d$ 是外导数。条件 $Z|d\alpha=0$ 意味着微分一形式 $\alpha$ 是 $Z$ 的相对积分不变量。矢量场 $Z$ 对应于自常微分方程组

$$\frac{dp_{ij}}{\epsilon} = V_{ij}, \quad \frac{dq_{ij}}{\epsilon} = W_{ij}, \quad \frac{dt}{\epsilon} = 1$$

其中 $t(\epsilon=0) = 0$。因此 $t(\epsilon) = \epsilon$，且 $\epsilon$ 可以识别为时间 $t$。

## 12.4. 微分形式与卡坦形式

运动方程也可以如下所示推导。考虑相空间 $\mathbb{R}^{6N} = \{(p_{11}, \dots, p_{N3}, q_{11}, \dots, q_{N3})\}$ 和微分二形式

$$\omega = \sum_{i=1}^{N} \sum_{j=1}^{3} dp_{ij} \wedge dq_{ij}$$

$\omega$ 被称为辛形式，$(\mathbb{R}^{6N}, \omega)$ 被称为辛流形。二形式 $\omega$ 可以作为微分形式的外导数得到

$$\Theta = \sum_{i=1}^{N} \sum_{j=1}^{3} p_{ij} dq_{ij}.$$

设

$$V = \sum_{i=1}^{N} \sum_{j=1}^{3} V_{ij}(\mathbf{p}, \mathbf{q}) \frac{\partial}{\partial p_{ij}} + W(\mathbf{p}, \mathbf{q}) \frac{\partial}{\partial q_{ij}}$$

为 $\mathbb{R}^{6N}$ 上的解析矢量场，其中 $\mathbf{p} = (p_{11}, \dots, p_{N3})$ 且 $\mathbf{q} = (q_{11}, \dots, q_{N3})$。矢量场 $V$ 通过*李级数*生成

$$\exp(V)(p_{11}, \dots, p_{N3}, q_{11}, \dots, q_{N3}))^T$$

（参数 $t \in \mathbb{R}$）是自微分方程组的李群变换，我们具有恒等式

$$\frac{dp_{ij}}{dt} = V_{ij}(\mathbf{p}, \mathbf{q}), \quad \frac{dq_{ij}}{dt} = W_{ij}(\mathbf{p}, \mathbf{q})$$

其中 $i = 1, \dots, N$ 且 $j = 1, 2, 3$。现在考虑条件 $L_V\omega = 0$，$L_V\omega$ 表示 $\omega$ 关于 $V$ 的李导数。

$$L_V\omega = d(V\omega) + Vd\omega$$

由于 $d\omega = 0$，我们得到

$$d(V\omega) = 0.$$

这里 $V|\omega$ 是矢量场 $V$ 对微分二形式的收缩。因此 $V|\omega$ 是一个形式。庞加莱引告诉局部存在一个 0形式（函数）$H$， 使得

$$V|\omega = -dH.$$

函数 $H$ 是哈密顿函数，相差一个常数。条件 $V|\omega = -dH$ 导出矢量场

$$V = \sum_{i=1}^N \sum_{j=1}^3 (\frac{\partial H}{\partial q_{ij}} + \frac{\partial H}{\partial p_{ij}})$$

这提供了运动方程。

## Karush-Kuhn-Tucker 条件

许多优化问题包含不等式。Karush-Kuhn-Tucker（即 Karush 和 Tucker）扩展了拉格朗日乘子法以包含不等式约束。对于具有凸域 $\Omega \subseteq \mathbb{R}^n$ 的优化问题

$$\minimize f(x), \quad x \in \Omega$$

$$\text{约束为} \quad g_j(x) \leq 0, \quad j=1, \dots, k$$

$$h_j(x)=0, \quad j=1, \dots l$$

我们定义广义拉格朗日函数

$$L(x, \alpha, \beta) = f(x) + \sum_{j=1}^k \alpha_j g_j(x) + \sum_{j=1}^l \beta_j h_j(x)$$

其中 $T$ 表示转置。假设函数 $f, g_j, h_j$ 是连续可微的。我们有

**定理.** 对于上述具有凸域 $\Omega \subseteq \mathbb{R}^n$ 的优化问题，点 $\mathbf{x}^*$ 为最优点的充要条件是存在 $\alpha^*$ 和 $\beta^*$，使得

$$\frac{\partial L(\mathbf{x}^*, \alpha^*, \beta*)}{\partial x} = 0$$

$$\frac{\partial L(\mathbf{x}^*, \alpha^*, \beta*)}{\partial \beta} = 0$$

$$\alpha_j^* g_j(\mathbf{x}^*) = 0, \quad j=1, \dots, k$$

$$g_j(\mathbf{x}^*) \leq 0, \quad j=1, \dots, k$$

$$\alpha_j^* \geq 0, \quad j=1, \dots, k.$$

第三个关系被称为 KKT 互补性条件。也就是说，约束是是（即 $g_j(x)=0$），或者相应的乘子满足 $\alpha_j^*=0$。此外，如果 $f, h_j, g_j$ 是二阶连续可微的，则

$$y^T \nabla^2 L(\mathbf{x}^*, \alpha^*, \beta*) y \geq 0$$

对于所有列向量 $y \in \mathbb{R}^n$，使得

$$\nabla h_i(\mathbf{x}^*)^T y = 0, \quad i=1, \dots, m, \quad (\nabla g_j(\mathbf{x}^*))^T y = 0$$

对于 $j \in A(x^*)$，$A(x^*)$ 是 $\mathbf{x}^*$ 处的活跃约束集。

## 12.5. KKT 条件

**例 1.** 找到函数 $f : \mathbb{R}^2 \to \mathbb{R}$ 的最小值

$$f(\mathbf{x}) = (x_1 - 2)^2 + (x_2 - 1)^2$$

约束条件为

$$g_1(\mathbf{x}) = x_2 - x_1^2 \ge 0, \quad g_2(\mathbf{x}) = 2 - x_1 - x_2 \ge 0, \quad g_3(\mathbf{x}) = x_1 \ge 0.$$

因此我们必须将约束重写为

$-x_2 + x_1^2 \le 0, \quad -2 + x_1 + x_2 \le 0, \quad -x_1 \le 0$

然后拉格朗日函数 $L$ 为

$$L(\mathbf{x}, \alpha) = (x_1 - 2)^2 + (x_2 - 1)^2 + \alpha_1(-x_2 + x_1^2) + \alpha_2(-2 + x_1 + x_2) + \alpha_3(-x_1).$$

KKT 条件提供了

$$2(x_1 - 2) + 2\alpha_1x_1 + \alpha_2 + \alpha_3 = 0$$

$$2(x_2 - 1) - \alpha_1 + \alpha_2 = 0$$

$$-x_2 + x_1^2 \le 0$$

$$-2 + x_1 + x_2 \le 0$$

$$-x_1 \le 0$$

$$\alpha_1(-x_2 + x_1^2) = 0$$

$$\alpha_2(-2 + x_1 + x_2) = 0$$

$$\alpha_3(-x_1) = 0$$

以及 $\alpha_1 \ge 0, \alpha_2 \ge 0, \alpha_3 \ge 0$。这些方程和不等式可以从 $\alpha_3 = 0$ 开始求解。通过这种研究得到 $x_1^* = 1, x_2^* = 1, \alpha_1^* = 1, \alpha_2^* = 0, \alpha_3^* = 2$。

**例 2.** 我们想要最大化 $f : \mathbb{R}^2 \to \mathbb{R}$

$$f(\mathbf{x}) = -3.6x_1 + 0.4x_2$$

为了应用 KKT 条件，我们需要将问题重写为

$-3.6x_1 + 0.4x_2$

拉格朗日函数 $L$ 是

$$L(\mathbf{x}, \alpha) = -3.6x_1 + 0.4x_2 + \alpha_1(-3.6x_1 + 0.4x_2).$$

我们得到

$$-3.6 - 3.6\alpha_1 = 0$$

$$0.4 + 0.4\alpha_1 = 0$$

这导出 $\alpha_1 = -1$。但这与 $\alpha_1 \ge 0$ 矛盾，因此该问题在可行域内无解。

**例 3.** 考虑 $\mathbb{R}^2$ 中的

$$S = \{(x_1, x_2) : x_1^2 + x_2^2 \le 1, x_1 \ge 0, x_2 \ge 0\}$$

这显然是凸的。最大化函数

$$f(x_1, x_2) = x_1 + x_2$$
