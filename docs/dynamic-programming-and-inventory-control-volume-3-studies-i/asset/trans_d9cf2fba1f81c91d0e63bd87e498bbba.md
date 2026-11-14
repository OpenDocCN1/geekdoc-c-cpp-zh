

让我们考虑时间 \(\tau_k+1\) 和 \(\tau_{k+1}-1\) 之间的库存，如果 \(\tau_{k+1}-2 \ge \tau_k\)。如果 \(\tau_{k+1}-1 = \tau_k\)，则有 \(y_{\tau_k+1} = y_{\tau_{k+1}}\)。否则，考虑 \(\theta_{k+1}\) 的位置很重要。如果 \(\theta_{k+1} = \tau_k + 1\)，则第一个库存 \(y_{\tau_k+1}\) 为负，且直到 \(\tau_{k+1}-1\) 的所有库存均为负。如果 \(\tau_{k+1}-1 \ge \theta_{k+1} \ge \tau_k+2\)，则有

\(\begin{aligned} y_{\tau_k+1} &= S - D_{\tau_k} > 0 \\ \dots \\ y_{\theta_{k+1}} &= S - (D_{\tau_k} + \dots + D_{\theta_{k+1}-2}) > 0 \\ y_{\theta_{k+1}} &= S - (D_{\tau_k} + \dots + D_{\theta_{k+1}-1}) \le 0 \\ y_{\tau_{k+1}-1} &= S - (D_{\tau_k} + \dots + D_{\tau_{k+1}-2}) \le 0 \end{aligned}\)

如果 \(\theta_{k+1} = \tau_{k+1}\)，则从 \(\tau_k + 1\) 到 \(\tau_{k+1} - 1\) 的库存均为正。因此我们可以写

\(\begin{aligned} J_\tau(V_s, s) &= \sum_{k=1}^\infty E \alpha^{\tau_k-1} (K + cS - (c+p))y_{\tau_k} \\ &+ \sum_{k=1}^\infty \mathbb{I}_{\theta_{k+1} \ge \tau_k+2} \sum_{n=\tau_k+1}^{\tau_{k+1}-1} \alpha^{n-1}(hy_n^+ + py_n^-). \end{aligned}\)

我们也可以写

(9.3.31) \(\begin{aligned} J_\tau(V_s, s) &= K + cS - (p+c)x \\ &+ \sum_{k=2}^\infty E \alpha^{\tau_k-1}(K + cS - cy_{\tau_k}) \\ &+ (h+p)E \sum_{k=1}^\infty \mathbb{I}_{\theta_{k+1} \ge \tau_k+2} \sum_{n=\tau_k+1}^{\theta_{k+1}-1} \alpha^{n-1}y_n \\ &- pE \sum_{k=1}^\infty \sum_{n=\tau_k+1}^{\tau_{k+1}} \alpha^{n-1}y_n, \end{aligned}\)

我们将其写为

\(J_\tau(V_s, s) = K + cS - (p+c)x + Z_1.\)

让我们计算 \(Z_1\)。我们首先注意到

\(\begin{aligned} E \sum_{k=1}^\infty \mathbb{I}_{\theta_{k+1} \ge \tau_k+2} \sum_{n=\tau_k+1}^{\theta_{k+1}-1} \alpha^{n-1}y_n &= E \sum_{n=\tau_k+1}^\infty \alpha^{\tau_k-1} \left[ S\alpha \frac{1-\alpha^{\theta_{k+1}-\tau_k-1}}{1-\alpha} \right. \\ &\left. - \sum_{l=0}^{\theta_{k+1}-\tau_k-1} D_{\tau_k+l} \alpha^l \frac{\alpha - \alpha^{\theta_{k+1}-\tau_k-1}}{1-\alpha} \right]. \end{aligned}\)

同样地，有

\(\begin{aligned} E \sum_{k=1}^\infty \sum_{n=\tau_k+1}^{\tau_{k+1}} \alpha^{n-1}y_n &= E \sum_{k=1}^\infty \alpha^{\tau_k-1} \left[ S\alpha \frac{1-\alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha} \right. \\ &\left. - \sum_{l=0}^{\tau_{k+1}-\tau_k-1} D_{\tau_k+l} \alpha^l \frac{\alpha - \alpha^{\tau_{k+1}-\tau_k-1}}{1-\alpha} \right]. \end{aligned}\)

我们还写

\(\sum_{k=2}^{\infty} E \alpha^{\tau_k - 1}(K + cS - c y_{\tau_k}) = E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1} \alpha^{\tau_{k+1} - \tau_k - 1} \left( \alpha K + \alpha c \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right).\)

从独立性性质我们可以写

\(E \left[ S \alpha \frac{1 - \alpha^{\theta_{k+1} - \tau_k - 1}}{1 - \alpha} - \sum_{l=0}^{\theta_{k+1} - \tau_k - 1} D_{\tau_k + l} \frac{\alpha^l - \alpha^{\theta_{k+1} - \tau_k - 1}}{1 - \alpha} \middle| \mathcal{F}^{\tau_k} \right] = E \left[ S \alpha \frac{1 - \alpha^{\tilde{\theta}}}{1 - \alpha} - \sum_{l=0}^{\tilde{\theta}} D_{1+l} \frac{\alpha^l - \alpha^{\tilde{\theta}}}{1 - \alpha} \right],\)

其中 \(\tilde{\theta} = \theta_2 - 2\)。同样地

\(E \left[ S \alpha \frac{1 - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \frac{\alpha^l - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} \middle| \mathcal{F}^{\tau_k} \right] = E \left[ S \alpha \frac{1 - \alpha^{\theta}}{1 - \alpha} - \sum_{l=0}^{\theta} D_{1+l} \frac{\alpha^l - \alpha \alpha^{\theta}}{1 - \alpha} \right],\)

其中 \(\theta = \tau_2 - 2\)。最后

\(E \left[ \alpha^{\tau_{k+1} - \tau_k - 1} \left( \alpha K + \alpha c \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right) \middle| \mathcal{F}^{\tau_k} \right] = E \left[ \alpha^{\theta} \left( \alpha K + \alpha c \sum_{l=0}^{\theta} D_{1+l} \right) \right].\)

因此我们有

\(Z_1 = E X_1 E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1},\)

以及

\(E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1} = \sum_{k=1}^{\infty} (E \alpha \alpha^{\theta})^{k-1},\)

并且根据引理 9.6

\(E \sum_{k=1}^{\infty} \alpha^{\tau_k - 1} = \frac{1}{(1 - \alpha) \Gamma(S - s)}.\)

此外

\(X_1 = \alpha^{\theta} \left( \alpha K + \alpha c \sum_{l=0}^{\theta} D_{1+l} \right) + (h + p) \left( S \alpha \frac{1 - \alpha^{\hat{\theta}}}{1 - \alpha} - \sum_{l=0}^{\hat{\theta}} D_{1+l} \frac{\alpha^l - \alpha^{\hat{\theta}}}{1 - \alpha} \right) - p \left( S \alpha \frac{1 - \alpha^{\theta}}{1 - \alpha} - \sum_{l=0}^{\theta} D_{1+l} \frac{\alpha^l - \alpha \alpha^{\theta}}{1 - \alpha} \right).\)

我们回顾

$$E \sum_{l=0}^a \alpha^l D_{l+1} = D\Gamma(S-s),$$

以及

$$E\alpha^\theta \sum_{l=0}^\theta D_{l+1} = D\Gamma(S-s) + \frac{1-\alpha}{\alpha} \left( \int_0^{S-s} \Gamma(x)dx - (S-s)\Gamma(S-s) \right).$$

因此，汇总结果我们得到

$$EX_1 = K(1-(1-\alpha)\Gamma(S-s)) - cS(1-\alpha)\Gamma(S-s) \\
+\Gamma(S-s)(\alpha cD + sc(1-\alpha) + p\alpha D - p\alpha s) \\
+(p+h) \left( \int_0^S \Gamma(\xi)d\xi - S \right) + (c(1-\alpha) - p\alpha) \int_0^{S-s} \Gamma(\xi)d\xi.$$

注意

$$g(s) = \alpha cD + sc(1-\alpha) + p\alpha D - p\alpha s.$$

此外，根据 \(\Gamma\) 的积分方程 (9.2.19)，通过积分我们有

$$\Gamma(S) - S = \alpha \int_0^\infty \Gamma(S-\xi)F(\xi)d\xi \\
= \alpha \int_s^S \Gamma(S-\xi)F(\xi)d\xi.$$

因为 \(s \le 0\) 且 \(F(\xi) = 0\)，对于 \(\xi \le 0\)。另外

$$\int_0^{S-s} \Gamma(\xi)d\xi = \int_s^S \Gamma(S-\xi)d\xi.$$

因此

$$(p+h) \left( \int_0^S \Gamma(\xi)d\xi - S \right) + (c(1-\alpha) - p\alpha) \int_0^{S-s} \Gamma(\xi)d\xi \\
= \int_s^S \Gamma(S-\xi)(c(1-\alpha) - p\alpha + \alpha(p+h)F(\xi))d\xi \\
= \int_s^S \Gamma(S-\xi)\mu(\xi)d\xi \\
= H(S).$$

因此

$$EX_1 = K(1-(1-\alpha)\Gamma(S-s)) - cS(1-\alpha)\Gamma(S-s) + \Gamma(S-s)g(s) + H(S).$$

由此可得

$$Z_1 = \frac{K+H(S)}{(1-\alpha)\Gamma(S-s)} + \frac{g(s)}{1-\alpha} - (K+cS),$$

这意味着

$$J_s(V_{s,S}) = -(p+c)x + \frac{g(s)}{1-\alpha} + \frac{K+H(S)}{(1-\alpha)\Gamma(S-s)},$$

因此，在此情况下 (9.3.27) 得证。

## II- \( s \ge 0, x \le s \):

在这种情况下，停止时间 \(\theta_k\) 不相关。然而 \(y(\tau_k)\) 可以是正或负。我们可以写

\(J_s(V_s, s) = K + c(S - x) + hx^+ + px^- + \sum_{k=1}^{\infty} E\alpha^{\tau_{k+1}-1}(K + c(S - y_{\tau_{k+1}}) + hy_{\tau_{k+1}}^+ + py_{\tau_{k+1}}^-) + hE \sum_{k=1}^{\infty} \mathbf{I}_{\tau_{k+1} \ge \tau_k + 2} \sum_{n=\tau_k+1}^{\tau_{k+1}-1} \alpha^{n-1} y_n.\)

按照之前的操作，我们得到

\(\sum_{k=1}^{\infty} \mathbf{I}_{\tau_{k+1} \ge \tau_k + 2} \sum_{n=\tau_k+1}^{\tau_{k+1}-1} \alpha^{n-1} y_n = \sum_{k=1}^{\infty} \alpha^{\tau_k-1} \left[ S\alpha \frac{1 - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \alpha \frac{\alpha^l - \alpha^{\tau_{k+1} - \tau_k - 1}}{1 - \alpha} \right],\)

以及

\(\sum_{k=1}^{\infty} \alpha^{\tau_{k+1}-1}(K + c(S - y_{\tau_{k+1}}) + hy_{\tau_{k+1}}^+ + py_{\tau_{k+1}}^-) = \sum_{k=1}^{\infty} \alpha^{\tau_k-1} \alpha^{\tau_{k+1} - \tau_k - 1} \left[ \alpha K + \alpha c \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} + \alpha h \left( S - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right) + \alpha p \left( S - \sum_{l=0}^{\tau_{k+1} - \tau_k - 1} D_{\tau_k + l} \right) \right].\)

由此可得

\(J_s(V_s, s) = K + c(S - x) + hx^+ + px^- + Z_2,\)

其中

\(Z_2 = \frac{EX_2}{(1 - \alpha)\Gamma(S - s)},\)

以及

\(X_2 = \alpha^{\theta} \Phi \left( \sum_{l=0}^{\theta} D_{1+l} \right) + h \left[ S\alpha \frac{1 - \alpha^{\theta}}{1 - \alpha} - \sum_{l=0}^{\theta} D_{1+l} \alpha \frac{\alpha^l - \alpha^{\theta}}{1 - \alpha} \right],\)

其中

\(\Phi(\xi) = \alpha K + \alpha c + \alpha h(S - \xi)^+ + \alpha p(S - \xi)^-.\)

要计算 \(EX_2\)，我们需要使用引理 9.6 的公式 (9.2.47)。重排后我们得到

\(E\alpha^{\theta} \Phi \left( \sum_{l=0}^{\theta} D_{1+l} \right) = K(1 - (1 - \alpha)\Gamma(S - s)) - cS(1 - \alpha)\Gamma(S - s) - hs\Gamma(S - s) + \Gamma(S - s)g(s) + H(S) + hS - h \int_s^S \Gamma(S - \xi) d\xi,\)

