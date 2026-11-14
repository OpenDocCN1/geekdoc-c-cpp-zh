

考虑到 \(\chi\) 在两个变量中的梯度，我们有

\[
\sup_{\xi \le x, z} |D\chi_a(x, z)| \le \frac{C}{1 - \delta_0(x)}.
\]

从这个估计出发，并利用 \(\chi_a(x, z) = 0, \forall x < 0\) 这一事实，我们可以断言，对于一个子序列（仍记为 \(\alpha\)）

\[
\sup_{x \le M, z \le N} |\chi_a(x, z) - \chi(x, z)| \to 0, \text{ as } \alpha \to 0, \forall M, N.
\]

我们如同在定理 12.3 中所做的那样，来证明

\[
\sup_{x \le M, z} |aE[\chi_a(x-x_2, z_2)|z_1=z] - E[\chi(x-x_2, z_2)|z_1=z]| \to 0, \forall M
\]

由 (13.2.34) 可知

\[
\chi(x, z) = g(x, z) + E[\chi(x-x_2, z_2)|z_1=z], \forall x > S(z),
\]

其中

\[
g(x, z) = h - (p+h)F(x|z).
\]

另外，若 \(x < S(z)\)，则 \(\chi(x,x)=0\)。而且，由

\[
0 = g_a(S_a(z), z) + aE[\chi_a(S_a(z)-x_2, z_2)|z_1=z],
\]

和

\[
\sup_{z \le N} |aE[\chi_a(S_a(z)-x_2, z_2)|z_1=z] - E[\chi(S(z)-x_2, z_2)1_{S(z)>z_2}|z_1=z]| \to 0
\]

我们容易得到

\[
0 = g(S(z), z) + E[\chi((S(z)-z_2)^+, z_2)|z_1=z],
\]

且函数 \(\chi(x,z)\) 在 \(x\) 中是连续的。

我们设

\[
\Gamma_a(z) = E[u_a(0, z_2)|z_1=z],
\]

则由第一个方程 (13.2.25) 可验证

\[
\Gamma_a(z) = \Psi_a(z) + aE[\Gamma_a(z_2)|z_1=z],
\]

其中

\[
\Psi_a(z) = c(1-a)S_a(z) + ahE[(S_a(z)-z_2)^+|z_1=z] + a\rho E[(S_a(z)-z_2)^+|z_1=z] + acE[z_2|z_1=z] + aE\left[\int_0^{(S_a(z)-z_2)^+} \chi_a(\xi, z_2)d\xi | z_1=z \right]
\]

我们有

\[
0 \le \Psi_a(z) \le m_0 \max(h, c) \left(1 + \frac{1}{1 - \delta_0(m_0)}\right) + (p+c)c_1
\]

考虑

\[
\Psi(z) = hE[(S(z) - z_2)^+ | z_1 = z] + pE[(S(z) - z_2)^- | z_1 = z] + cE[z_2 | z_1 = z] + E \left[ \int_0^{(S(z)-z_2)^+} \chi(\xi, z_2) d\xi | z_1 = z \right]
\]

以及 \(\Gamma(z)\) 为以下方程的解

\[
\Gamma(z) + \rho = \Psi(z) + E[\Gamma(z_2) | z_1 = z],
\]

其中

\[
\rho = \int \Psi(z) \varpi(z) dz.
$$

根据遍历理论，参见第 3 章，定理 3.3，我们可以断言

\[
\sup_z |\Gamma(z)| \le \sup_z |\Psi(z) - \rho| \frac{3 - \beta}{1 - \beta},
$$

其中 \(0 < \beta < 1\)，仅取决于马尔可夫链。

同样，若设

\[
\rho_\alpha = \int \Psi_\alpha(z) \varpi(z) dz, \quad \tilde{\Gamma}_\alpha(z) = \Gamma_\alpha(z) - \frac{\rho_\alpha}{1 - \alpha}
$$

则可写成

\[
\tilde{\Gamma}_\alpha(z) + \rho_\alpha = \Psi_\alpha(z) + \alpha E[\tilde{\Gamma}_\alpha(z_2) | z_1 = z],
$$

我们也可以断言

\[
\sup_z |\tilde{\Gamma}_\alpha(z)| \le \sup_z |\Psi_\alpha(z) - \rho_\alpha| \frac{3 - \beta}{1 - \beta} \le \left[ m_0 \max(h, c) \left( 1 + \frac{1}{1 - \delta_0(m_0)} \right) + (p + c)c_1 \right] \frac{3 - \beta}{1 - \beta}.
$$

而且

\[
\tilde{\Gamma}_\alpha(z) - \tilde{\Gamma}_\alpha(z') = \Psi_\alpha(z) - \Psi_\alpha(z') + \alpha \int \tilde{\Gamma}_\alpha(\zeta) (f(\zeta|z) - f(\zeta|z')) d\zeta.
$$

由于，利用 (13.2.33)

\[
|\Psi_\alpha(z) - \Psi_\alpha(z')| \le C(m_0) \delta |z - z'|,
$$

并且由 (12.3.32) 可断言

\[
|\tilde{\Gamma}_\alpha(z) - \tilde{\Gamma}_\alpha(z')| \le C_1(m_0) \delta |z - z'|.
$$

因此函数 \(\tilde{\Gamma}_\alpha(z)\) 一致 Lipschitz 连续且有界。由此可知，对于一个子序列我们得到

\[
\sup_{0 \le z \le N} \left| \Gamma_\alpha(z) - \frac{\rho_\alpha}{1 - \alpha} - \Gamma(z) \right| \to 0, \forall N
$$

因此

\[
\sup_{x \le M, 0 \le z \le N} \left| u_\alpha(x, z) - \frac{\rho_\alpha}{1 - \alpha} - u(x, z) \right| \to 0, \forall x, \forall M, N
$$

其中

\[
u(x, z) = hx^+ + px^- - cx + \int_0^x \chi(\xi, z) d\xi + \Gamma(z).
$$

我们推导出 \(u(0,z) = \Gamma(z)\)。而且，容易验证

\[
\Gamma(z) = \rho + cS(z) + E[u(S(z) - z_2, z_2)|z_1 = z].
$$

因此第一个关系 (13.2.28) 得证。

现在考虑 \(x \ge S(z)\) 的情况。定义函数

\[
\bar{u}(x,z) = hx^+ + px^- + E[u(x - z_2, z_2)|z_1 = z].
$$

我们得到

\[
\begin{aligned}
\bar{u}'(x,z) &= h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0} + E[u'(x-z_2, z_2)|z_1 = z] \\
&= h\mathbb{I}_{x>0} - p\mathbb{I}_{x<0} + c + \chi(x,z), \quad x \ge S(z) \\
&= u'(x,z), \quad x \ge S(z).
\end{aligned}
$$

又

\[
\begin{aligned}
\bar{u}(S(z), z) &= hS(z) + E[u(S(z) - z_2, z_2)|z_1 = z] \\
&= (h - c)S(z) + \rho + \Gamma(z) \\
&= u(S(z), z) + \rho
\end{aligned}
$$

由这两个关系可得 \(\bar{u}(x,z) = u(x,z) + \rho, \forall x \ge S(z)\)。

这就完成了 (13.2.28) 的第二部分。

(12.3.40) 的证明与定理 12.3 的证明类似。

我们接下来有

\[
u_\alpha(x,z) - u_\alpha(x,z') = \Gamma_\alpha(z) - \Gamma_\alpha(z') + \int_0^x (\chi_\alpha(\xi,z) - \chi_\alpha(\xi,z')) d\xi
$$

利用已证明的估计我们得到

\[
|u_\alpha(x,z) - u_\alpha(x,z')| \le \left[ C_1(m_0) + \frac{C(m_0)x^+}{1 - \delta_0(x)} \right] \delta|z - z'|
$$

极限 \(u(x,z)\) 满足所有估计 (12.3.37), (12.3.39)。唯一性的证明与定理 12.3 的证明类似。

证明已完成 \(\square\)

## 12.4. 无积压和设置成本

### 12.4.1. 模型.

我们现在研究设置成本的情况，并从无短缺模型开始。我们需要研究 Bellman 方程

\[
u(x,z) = \inf_{v \ge 0} \{K \mathbb{I}_{v > 0} + l(x,z,v) + \alpha \Phi^v u(x,z)\},
$$

其中

\[
\begin{aligned}
\Phi^v \varphi(x,z) &= E[\varphi((x+v-z_2)^+, z_2)|z_1 = z] \\
&= \int_0^{x+v} \varphi(x+v-\zeta, \zeta) f(\zeta|z) d\zeta + \int_{x+v}^\infty \varphi(0, \zeta) f(\zeta|z) d\zeta
\end{aligned}
$$

并且

\[
f(\zeta|z) \text{ 在两个变量中一致连续且有界}
\]

\[
\int_0^{+\infty} \zeta f(\zeta|z) d\zeta \le c_0 z + c_1
$$

\[
l(x,z,v) = cv + hx + pE[(x+v-z_2)^-|z_1 = z].
$$

我们在区间 \([0, w_0(x,z)]\) 中寻找 (12.4.1) 的解，其中

\[
u_0(x,z) = l_0(x,z) + \alpha E[u_0(x-z_2, z_2)|z_1=z].
$$

在引理 12.1 中，我们已证明估计

\[
u_0(x,z) \le \frac{hx}{1-\alpha} + \frac{pc_0z}{1-c_0\alpha} + \frac{pc_1}{(1-\alpha)(1-c_0\alpha)},
$$

并假设

\[
c_0\alpha < 1.
$$

如常，我们考虑收益函数

\[
J_{x,z}(V) = E \sum_{n=1}^\infty \alpha^{n-1} [K \mathbb{I}_{v_n > 0} + l(y_n, z_n, v_n)],
$$

其中 \(V = (v_1, \cdots, v_n, \cdots)\) 为取正值的自适应过程，且

\[
y_{n+1} = (y_n + v_n - z_{n+1})^+, y_1 = x.
$$

我们定义值函数

\[
u(x,z) = \inf_V J_{x,z}(V).
$$

我们陈述

**定理 12.7.** 我们假设 (12.4.2), (12.4.3), (12.4.4), (12.4.5), (12.4.8)。在 (12.4.11) 中定义的值函数是区间 \([0, w_0]\) 上 Bellman 方程 (12.4.1) 的唯一下半连续解。存在一个最优反馈 \(\hat{v}(x,z)\)。

### 12.4.2. s(z), S(z) 策略.

我们现在证明以下结果

**定理 12.8.** 我们做出定理 12.7 的假设且 \(p > c\)。那么函数 \(u(x,z)\) 是 \(K\)-凸且连续的。当 \(x \to +\infty\) 时，它趋向于 \(+\infty\)。函数

\[
G(x,z) = cx + pE[(x-z_2)^-|z_1=z] + \alpha E[u((x-z_2)^+, z_2)|z_1=z],
$$

也是 \(K\)-凸且连续的。当 \(x \to +\infty\) 时，它趋向于 \(+\infty\)。考虑与 \(G(x,z)\) 相关的数 \(s(z)\)、\(S(z)\)，最优反馈由

\[
\hat{v}(x,z) = \begin{cases} S(z) - x, & \text{如果 } x \le s(z) \\ 0, & \text{如果 } x > s(z) \end{cases}
$$

给出。

函数 \(s(z)\)、\(S(z)\) 是连续的。

证明. 我们考虑递增序列

\[
u_{n+1}(x,z) = \inf_{v \ge 0} \{ K \mathbb{I}_{v > 0} + cv + hx + pE[(x+v-z_2)^-|z_1=z] + \alpha E[u_n((x+v-z_2)^+, z_2)|z_1=z] \},
$$

其中 \(u_0(x,z) = 0\)。定义

\[
G_n(x,z) = cx + pE[(x-z_2)^-|z_1=z] + \alpha E[u_n((x-z_2)^+, z_2)|z_1=z].
$$

我们可以写成

\[
u_{n+1}(x,z) = (h-c)x + \inf_{\eta \ge z} \{ K \mathbb{I}_{\eta \ge z} + G_n(\eta, z) \}.
$$

我们将通过归纳法证明，对于 \(n \ge 1\)，\(u_n(x,z)\) 和 \(G_n(x,z)\) 在 \(x\) 中均为 \(K\)-凸、连续，并且当 \(x \to +\infty\) 时趋向于 \(+\infty\)。对于

