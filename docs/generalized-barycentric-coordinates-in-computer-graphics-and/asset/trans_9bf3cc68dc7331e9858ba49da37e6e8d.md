

![](img/4913dd83a2a14bc205a0a92cce102c82_88_0.png)

图 4.6 利用路径 $\psi_i$ 构造中间多边形 $\Omega^{t_k}$。

其中 $M = M_1 + \cdots + M_n$ 且 $d = \max_{1 \le i \le n} \|u_i\|$。总体而言，这意味着当
$$d < \frac{\sqrt{5}-1}{2M}.$$
时，映射 $f$ 是单射的。

## 4.3 双射复合重心映射

第 4.2.1 节表明，如果源多边形和目标多边形足够接近，则映射接近恒等映射，因此是双射的。因此，通过将从源多边形到目标多边形的重心映射“拆分”为有限个中间步骤，其中每个步骤仅轻微扰动顶点，应该可以得到双射复合映射。

为此，假设 $\psi_i: [0, 1] \to \mathbb{R}^2, i = 1, \dots, n$ 是一组连续顶点路径，连接每个源向量 $v_i^0 = \psi_i(0)$ 及其对应的目标向量 $v_i^1 = \psi_i(1)$，如图 4.6 所示。令 $\tau = (t_0, t_1, \dots, t_m)$，其中 $t_0 = 0, t_m = 1$，令 $t_k < t_{k+1}$ 对于 $k = 0, \dots, m-1$ 是 $[0, 1]$ 的一个划分，并令 $f_k$ 是基于重心坐标 $\phi_i^{t_k}$ 从 $\Omega^{t_k}$ 到 $\Omega^{t_{k+1}}$ 的重心映射。

![](img/4913dd83a2a14bc205a0a92cce102c82_88_1.png)

图 4.7 对于 $\tau = [0, 0.5, 1]$ 构造复合重心映射。

![](img/4913dd83a2a14bc205a0a92cce102c82_89_0.png)

图 4.8 不同数量均匀步数的均匀复合平均值映射示例。

映射
$$
\boldsymbol{f}_{\tau} = \boldsymbol{f}_{m-1} \circ \boldsymbol{f}_{m-2} \circ \cdots \circ \boldsymbol{f}_{0}
$$
被称为从 \(\tilde{\Omega}^0\) 到 \(\tilde{\Omega}^1\) 的 *复合重心映射* [350]。正方形与凹四边形之间的复合重心映射示例见图 4.7。

记 \(\tilde{\Omega}^{t_k}\) 与 \(\tilde{\Omega}^{t_{k+1}}\) 之间的最大位移距离为
$$
d_k = \max_{1 \le i \le n} \left\| \boldsymbol{v}_i^{t_k} - \boldsymbol{v}_i^{t_{k+1}} \right\|,
$$
根据前面的结果，当
$$
d_{\tau} = \max_{0 \le k < m} d_k < \frac{\sqrt{5} - 1}{2nM^*},
$$
时，\(\boldsymbol{f}_{\tau}\) 是双射的，其中
$$
M^* = \max_{1 \le i \le n} \sup_{t \in [0,1]} \sup_{\boldsymbol{x} \in \Omega^t} \left\| \nabla \boldsymbol{\psi}^t_i(\boldsymbol{x}) \right\|.
$$

![](img/4913dd83a2a14bc205a0a92cce102c82_89_1.png)

图 4.9 具有 1000 个均匀步数的复合平均值映射示例。放大图中网格的分辨率提高了 4 倍。

对于平均值映射的特殊情况，可以证明该界对于任意凸多边形之间的映射都满足（参见第 2 章）。图 4.8 表明，当有足够多的中间步骤时，映射 $f$ 变为双射。

特别是，存在某个 $m \in \mathbb{N}$，使得均匀划分 $t_k$（其中 $t_k = k/m$）给出双射复合重心映射 $f_{r_m}$。图 4.9 显示了两个嵌套正方形的复合平均值映射示例，其中内部正方形在目标配置中使用均匀划分 1000 旋转了 90 度。

### 4.3.1 复合重心映射的极限

均匀复合重心映射的想法引出了关于极限行为的有趣问题。为此，我们考虑 *无限复合重心映射* $f_\infty = \lim_{m \to \infty} f_{r_m}$ 及其后向映射 $g_\infty : \Omega^1 \to \Omega^0$。图 4.10 显示了使用均匀复合映射 $f_{r_m}$ 与其后向映射 $g_{r_m} : \Omega^1 \to \Omega^0$（步数相同）对一个五角星进行映射的结果。对 $\Omega^0$ 中一百万个随机点 $x$ 计算最大距离 $\|x - g_{r_m}(f_{r_m}(x))\|$ 表明，该距离趋于零，因此当 $m \to \infty$ 时 $g_{r_m} = f_{r_m}^{-1}$。因此，无限重心映射的逆映射很可能本身也是一个无限重心映射，而这对于标准重心映射则不成立。

这一观察可以通过考虑两个连续步骤之间的差异并取其极限来证明 [145]。对于任意点 $x^0 \in \Omega^0$，我们计算复合映射 $f$ 的第一步 $f_0$，
$$
x^{t_1} = f_0(x^0) = \sum_{i=1}^n \phi_i^{t_0}(x^0) \psi_i(t_1).
$$
由于线性再现性质，
$$
x^0 = \sum_{i=1}^n \alpha_i^0 \phi_i^{t_0}(x^0) \psi_i(t_0),
$$

![](img/4913dd83a2a14bc205a0a92cce102c82_90_0.png)

图 4.10 随着均匀步数 $m$ 的增加，映射 $f_{r_m}$ 与后向映射 $g_{r_m}$ 的复合趋于恒等映射。

因此，
$$
x^{t_1} - x^0 = \sum_{i=1}^n \phi_i^{t_0}(x^0)(\psi_i(t_1) - \psi_i(t_0)).
$$
除以 $t_1 - t_0$ 并取 $t_1 \to t_0$ 的极限，得到
$$
x'(t) = \sum_{i=1}^n \phi_i(x(t), t)\psi'_i(t),
$$
这是关于 $x(t)$ 的形式为
$$
x'(t) = F(t, x(t)).
$$
的一阶微分方程，初始条件为 $x(0) = x^0$。

如果重心坐标 $\phi_i$ 是 Lipschitz 连续的，那么 $F$ 也是 Lipschitz 连续的，根据皮卡德-林德勒夫定理 [250, 308]，这是局部唯一解存在的充分条件。该微分方程的解也是全局解，因为 $x(t)$ 始终位于所有中间多边形内部。这是因为映射是双射的，且边被映射为边。

为了证明 $g^{-1} = f$，我们考虑任意点 $x^t = x(1) \in \bar{\Omega}^1$，
$$
y'(t) = \sum_{i=1}^n \phi_i(x(1-t), 1-t)\bar{\psi}'_i(t), \quad \bar{\psi}_i(t) = \psi_i(1-t),
$$
其中 $y(0) = x(1)$ 是将 $x^1$ 从 $\bar{\Omega}^1$ 映射到 $\bar{\Omega}^0$。由于 $\bar{\psi}'_i(t) = -\psi'_i(1-t)$，我们得出 $y(t) = x(1-t)$。因此，$y(1) = x^0$ 且 $g$ 有一个由前一个方程生成的逆映射，满足 $g^{-1} = f$。

## 4.4 扩展

保证多边形之间复合重心映射双射性的充分条件可以自然地扩展到闭合曲线和多面体之间的映射。

### 4.4.1 闭合平面曲线

我们定义闭合平面源曲线 $\gamma^0(s)$ 与闭合平面目标曲线 $\gamma^1(s)$（其中 $s \in [0, 1]$）之间的 *重心映射* 为
$$
f(x) = \int_0^1 \phi(s, x)\gamma^1'(s)ds,
$$
其中 $\phi(s, x)$ 是相对于 $\gamma^0$ 的跨有限重心坐标（参见第 3 章）。类似于多边形的情况，我们现在考虑受扰目标曲线 \(\gamma^1(s) = \gamma^0(s) + \boldsymbol{u}(s)\) 并假设最大位移距离满足
$$
d = \sup_{s \in [0,1]} \|\boldsymbol{u}(s)\| < \frac{\sqrt{5}-1}{2M},
$$
其中
$$
M = \sup_{s \in [0,1]} \sup_{\boldsymbol{x} \in \gamma^0} \|\nabla \phi(s, \boldsymbol{x})\|.
$$
我们利用线性再现性质重写
$$
\boldsymbol{f}(\boldsymbol{x}) = \boldsymbol{x} + \int_0^1 \phi(s, \boldsymbol{x}) \boldsymbol{u}(s) ds
$$
并计算
$$
J\boldsymbol{f}(\boldsymbol{x}) = \left| \begin{matrix} 1 + \int \partial_1 \phi(s, \boldsymbol{x}) u_1(s) ds & \int \partial_2 \phi(s, \boldsymbol{x}) u_1(s) ds \\ \int \partial_1 \phi(s, \boldsymbol{x}) u_2(s) ds & 1 + \int \partial_2 \phi(s, \boldsymbol{x}) u_2(s) ds \end{matrix} \right| = 1 + \int \nabla \phi(s, \boldsymbol{x}) \cdot \boldsymbol{u}(s) ds + \iint \partial_1 \phi(s, \boldsymbol{x}) \partial_2 \phi(r, \boldsymbol{x}) (\boldsymbol{u}(s) \times \boldsymbol{u}(r)) ds dr,
$$
其中积分范围从零到一。因此，
$$
J\boldsymbol{f}(\boldsymbol{x}) \ge 1 - Md - M^2 d^2,
$$
当 \(Md < (\sqrt{5}-1)/2\) 时，该值严格为正。因此，只要 \(d < \frac{\sqrt{5}-1}{2M}\)，映射就是单射的。值得注意的是，这个界与多边形情况下的相同。

现在假设 \(\boldsymbol{\psi}\) 是源曲线 \(\gamma^0 = \boldsymbol{\psi}(0)\) 与目标曲线 \(\gamma^1 = \boldsymbol{\psi}(1)\) 之间的连续 _闭合曲线_ 插值函数。同样，我们令 \(\tau = (t_0, t_1, \dots, t_m)\)，其中 \(t_0 = 0, t_m = 1\)，且 \(t_k < t_{k+1}$ 对于 \(k = 0, \dots, m-1$ 是 \([0,1]$ 的一个 _划分_，并令 \(\boldsymbol{f}_k\) 是基于重心坐标 \(\phi^k$ 从 \(\gamma^{t_k}$ 到 \(\gamma^{t_{k+1}}$ 的重心映射。映射
$$
\boldsymbol{f}_\tau = \boldsymbol{f}_{m-1} \circ \boldsymbol{f}_{m-2} \circ \cdots \circ \boldsymbol{f}_0,
$$

