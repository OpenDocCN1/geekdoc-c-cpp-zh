

它在 $x$ 上是 $C^1$ 的，在 $z$ 上是 Lipschitz 连续的。以下估计成立

(12.2.34)
\[
\begin{aligned}
\sup_{\xi \le x} \frac{|u(\xi, z)|}{z} &\le \frac{C}{1 - \delta_0(x)}, \\
|u(x,z) - u(x,z')| &\le \left[ C_0(m_0) + \frac{C_1(m_0)x}{1 - \delta_0(x)} \right] |z - z'|.
\end{aligned}
\]

(12.2.35)
\[
\begin{aligned}
(1 - \delta_0(x)) \sup_{\xi \le x} \frac{|u_{xx}(\xi, z)|}{z} &\le C, \\
(1 - \delta_0(x)) \sup_{\xi \le x} \frac{|u_{xz}(\xi, z)|}{z} &\le C, \quad \text{a.e.}
\end{aligned}
\]

给定 $S(z)$，满足上述条件且 $\int u(0,z)\varpi(z)dz = 0$ 的对 $u(x,z)$、$\rho$ 是唯一确定的。

另外

(12.2.36)
\[
u(x,z) + \rho = \inf_{v \ge 0} [l(x, z+v) + \Phi'' u(x,z)].
\]

### 证明

我们从 (12.2.30) 开始。首先注意到，由于 $c_0 = 0$，我们有

(12.2.37)
\[
S_\alpha(z) \le \frac{c_1(p+h)}{\min(h,c)} = m_0.
\]

我们继续使用定理 12.2 中获得的估计。首先，我们有

\[
(S_\alpha(z) - S_\alpha(z'))(G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z'), z)) \ge 2 \min(h,c)\gamma(m_0)(S_\alpha(z) - S_\alpha(z'))^2
\]

我们知道 $u_\alpha(x,z)$ 在 $x$ 上是 $C^1$ 的。然后，根据 (12.2.26)，我们有（记 $u'_\alpha(x,z)$）

\[
u'_\alpha(x,z) = h - c \quad \text{if } x < S_\alpha(z), \qquad
u'_\alpha(x,z) = h - p\bar{F}(x) + \alpha E[u'_\alpha(x-z_2, z_2) \mathbb{1}_{x>z_2} \mid z_1 = z] \quad \text{if } x > S_\alpha(z)
\]

由此我们可以断言

(12.2.38)
\[
\sup_{\xi \le x} \frac{|u'_\alpha(\xi, z)|}{z} \le \frac{\max(h,p)}{1 - \delta_0(x)}.
\]

因此

\[
|G'_\alpha(S_\alpha(z), z') - G'_\alpha(S_\alpha(z), z)| = \left( p + \frac{\max(h,p)}{1 - \sup_z F(m_0 z)} \right) \int |f(\zeta|z') - f(\zeta|z)| \, d\zeta,
\]

\[
|G'_\alpha(S_\alpha(z'), z') - G'_\alpha(S_\alpha(z'), z)| = \left( p + \frac{\max(h,p)}{1 - \sup_z F(m_0 z)} \right) \int |f(\zeta|z') - f(\zeta|z)| \, d\zeta.
\]

汇总结果，我们得到估计

(12.2.39)
\[
|S_\alpha(z) - S_\alpha(z')| \le \frac{p + \max(h,p)}{\min(h,c)\gamma(m_0)} \frac{1}{1 - \delta_0(m_0)} \int |f(\zeta|z') - f(\zeta|z)| \, d\zeta,
\]

并且根据第一个假设 (12.2.29)，我们最终得到

(12.2.40)
\[
|S_\alpha(z) - S_\alpha(z')| \le \frac{p + \max(h, p)}{\min(h, c)\gamma(m_0)} \delta |z - z'|.
\]

因此，序列 $S_\alpha(z)$ 是一致 Lipschitz 连续的。可以提取一个子序列，它在紧集上的连续函数空间中收敛到一个函数 $S(z)$，这是标准的（参见附录 A.4），对于任何紧集 $K$ 都成立。因此 (12.2.30) 得到满足。

定义 $\chi_\alpha(x, z) = u'_\alpha(x, z) - h + c$。我们有

(12.2.41)
\[
\begin{aligned}
\chi_\alpha(x, z) &= g_\alpha(x, z) \\
&\quad + \alpha E[\chi_\alpha(x - 2z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z], \quad x > S_\alpha(z) \\
&= 0, \qquad x \le S_\alpha(z)
\end{aligned}
\]

其中

(12.2.42)
\[
g_\alpha(x, z) = (c + \alpha(h - c) - (p + \alpha(h - c))F(x|z).
\]

如同对 $u'_\alpha(x, z)$ 所做的那样，我们可以断言

(12.2.43)
\[
\sup_{0 \le \xi \le z} |\chi_\alpha(\xi, z)| \le \frac{\max(h, p)}{1 - \delta_0(x)}.
\]

如果我们考虑 $\psi_\alpha(x, z) = \chi'_\alpha(x, z) = u''_\alpha(x, z)$，那么利用 $\chi_\alpha(0, z) = 0$ 这一事实，我们看到

(12.2.44)
\[
\begin{aligned}
\psi_\alpha(x, z) &= (p + \alpha(h - c))f(x|z) \\
&\quad + \alpha E[\psi_\alpha(x - 2z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z], \quad x > S_\alpha(z) \\
&= 0, \qquad x < S_\alpha(z)
\end{aligned}
\]

函数 $\psi_\alpha(x, z)$ 不是连续的，但它是可测且有界的。我们有

(12.2.45)
\[
\sup_{0 \le \xi \le x} |\psi_\alpha(\xi, z)| \le \frac{((h - c)^+ + p)\|f\|}{1 - \delta_0(x)},
\]

其中 $\|f\| = \sup_{x,z} f(x|z)$。

接下来，我们对 $\chi_\alpha(x, z) - \chi_\alpha(x, z')$ 进行估计。首先假设 $x > S_\alpha(z), x > S_\alpha(z')$。那么，根据 (12.2.41)，我们有

\[
\begin{aligned}
\chi_\alpha(x, z) - \chi_\alpha(x, z') &= g_\alpha(x, z) - g_\alpha(x, z') \\
&\quad + \alpha \int_0^x \chi_\alpha(x - \zeta, \zeta)(f(\zeta|z) - f(\zeta|z')) \, d\zeta.
\end{aligned}
\]

根据估计 (12.2.43) 和第一个假设 (12.2.29)，我们推断

\[
|\chi_\alpha(x, z) - \chi_\alpha(x, z')| \le \left(p + (h - c)^+ + \frac{\max(h, p)}{1 - \delta_0(x)}\right) \delta |z - z'|,
\qquad x > S_\alpha(z), \; x > S_\alpha(z').
\]

现在，为了明确起见，假设 $S_\alpha(z') > x > S_\alpha(z)$。那么 $\chi_\alpha(x, z') = 0$ 且

\[
0 = g_\alpha(S_\alpha(z), z) + \alpha E[\chi_\alpha(S_\alpha(z) - 2z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z].
\]

因此

\[
\begin{aligned}
\chi_\alpha(x, z) - \chi_\alpha(x, z')
&= g_\alpha(x, z) - g_\alpha(S_\alpha(z), z) + \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \\
&\quad - \alpha E[\chi_\alpha(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] \\
&= (p + \alpha(h - c))(F(x|z) - F(S_\alpha(z)|z)) \\
&\quad + \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2 > S_\alpha(z)} \mid z_1 = z] \\
&\quad + \alpha E[(\chi_\alpha(x - z_2, z_2) - \chi_\alpha(S_\alpha(z) - z_2, z_2)) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z].
\end{aligned}
\]

由此可得

\[
\begin{aligned}
|\chi_\alpha(x, z) - \chi_\alpha(x, z')|
&\le \left[ p + (h - c)^+ + \frac{\max(h, p)}{1 - \delta_0(x)} + \frac{(h - c)^+ + p}{1 - \delta_0(x)} \right] f(\|x - S_\alpha(z)\|).
\end{aligned}
\]

最后，我们可以给出估计

(12.2.46)
\[
|\chi_\alpha(x, z) - \chi_\alpha(x, z')| \le \frac{C(m_0)}{1 - \delta_0(x)} \delta |z - z'|,
\]

其中 $C(m_0)$ 仅依赖于常数和 $m_0$。因此，考虑 $\chi_\alpha$ 在两个变量上的梯度，我们得到了估计

(12.2.47)
\[
|D\chi_\alpha(x, z)| \le \frac{C}{1 - \delta_0(x)}.
\]

根据这个估计，我们可以断言，对于一个子序列（仍记为 $\alpha$）

(12.2.48)
\[
\begin{aligned}
\sup_{\substack{x \le M \\ z \le N}} |\chi_\alpha(x, z) - \chi(x, z)| \to 0, \qquad \text{as } \alpha \to 0, \; \forall M, N.
\end{aligned}
\]

因此也

\[
\begin{aligned}
\sup_{\substack{x \le M \\ z \le M}} \left| \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \\
\le \sup_{\substack{x \le M \\ z \le M}} \left| E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \\
+ (1 - \alpha) \frac{\max(h, p)}{1 - \delta_0(M)},
\end{aligned}
\]

并且

\[
\begin{aligned}
\sup_{\substack{x \le M \\ z \le M}} \left| E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \\
\le \sup_{\substack{x \le M \\ z \le N}} |\chi_\alpha(x, z) - \chi(x, z)| + 2 \frac{\max(h, p)}{1 - \delta_0(M)} \frac{c_1}{N},
\end{aligned}
\]

由此我们很容易推断

\[
\sup_{x \le M} \sup_z \left| \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right| \to 0, \qquad \forall M.
\]

根据 (12.2.41)，可得

\[
\chi(x, z) = g(x, z) + E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z], \qquad \forall x > S(z),
\]

其中

(12.2.49)
\[
g(x, z) = h - (p - h + c)\bar{F}(x|z).
\]

另外，如果 $x < S(z)$，则 $\chi(x,z)=0$。而且，根据

\[
0 = g_\alpha(S_\alpha(z), z) + \alpha E[\chi_\alpha(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z]
\]

和

\[
\begin{aligned}
&\left| \alpha E[\chi_\alpha(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] - E[\chi(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] \right| \\
&\quad \le \sup_{x \le M} \sup_z \left| \alpha E[\chi_\alpha(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] - E[\chi(x - z_2, z_2) \mathbb{1}_{x > z_2} \mid z_1 = z] \right|
\end{aligned}
\]

\[
\begin{aligned}
&\left| E[\chi(S_\alpha(z) - z_2, z_2) \mathbb{1}_{S_\alpha(z) > z_2} \mid z_1 = z] - E[\chi(S(z) - z_2, z_2) \mathbb{1}_{S(z) > z_2} \mid z_1 = z] \right| \\
&\quad \le \frac{(h - c + p)\|f\|_1}{1 - \delta_0(m_0)} |S_\alpha(z) - S(z)| + \frac{2 \max(h, p)}{1 - \delta_0(m_0)} |F(S_\alpha(z)|z) - F(S(z)|z)|
\end{aligned}
\]

我们很容易得到

\[
0 = g(S(z), z) + E[\chi((S(z) - z_2)^+, z_2) \mid z_1 = z],
\]

并且函数 $\chi(x, z)$ 在 $x$ 上是连续的。

接下来，我们设

\[
\Gamma_\alpha(z) = u_\alpha(0, z), \qquad G_\alpha(z) = E[(S_\alpha(z) - z_2)^- \mid z_1 = z],
\]

然后，从第一个方程 (12.2.26) 可以验证

\[
\Gamma_\alpha(z) = cS_\alpha(z) + pG_\alpha(z) + \alpha E[u_\alpha(S_\alpha(z) - z_2, z_2)^+ \mid z_1 = z] = \Psi_\alpha(z) + \alpha E[\Gamma_\alpha(z_2) \mid z_1 = z].
\]

其中

\[
\Psi_\alpha(z) = cS_\alpha(z) + pG_\alpha(z) + \alpha E\left[\int_0^{(S_\alpha(z) - z_2)^+} (h - c + \chi(\xi, z_2)) \, d\xi \,\middle|\, z_1 = z\right],
\]

并且

\[
0 \le \Psi_\alpha(z) \le \left[\max(h, c) + \frac{\max(h, p)}{1 - \delta_0(m_0)}\right] m_0 + pc_1.
\]

这个估计对于极限也成立

\[
\Psi(z) = cS(z) + pG(z) + E\left[\int_0^{(S(z) - z_2)^+} (h - c + \chi(\xi, z_2)) \, d\xi \,\middle|\, z_1 = z\right]
\]

其中

\[
G(z) = E[(S(z) - z_2)^- \mid z_1 = z].
\]

