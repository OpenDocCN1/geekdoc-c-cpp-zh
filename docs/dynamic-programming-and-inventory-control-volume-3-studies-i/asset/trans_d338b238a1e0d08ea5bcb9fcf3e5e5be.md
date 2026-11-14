

我们现在用 \(m^3(x)\frac{\partial z}{\partial t}\frac{t}{t+1}\) 来检验方程 (15.6.16)，并获得
\[\frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx\]

\[+ \frac{t}{t+1} \int_s^{+\infty} m^{\frac{3}{2}}(x) \frac{\partial z}{\partial t} \left[ \frac{3}{2} \sigma^2 m' m^{\frac{1}{2}} \frac{\partial z}{\partial x} + \nu m^{\frac{3}{2}} \frac{\partial z}{\partial x} \right] (x,t) dx\]

\[- \lambda \frac{t}{t+1} \int_s^{+\infty} m^3(x) \frac{\partial z}{\partial t} \left[ \int_0^{+\infty} (z(x-\xi, t) - z(x,t)) \mu(\xi) d\xi \right] dx\]

\[+ \frac{\sigma^2}{4} \frac{t}{t+1} \frac{d}{dt} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx = 0\]

因此
\[\frac{1}{2} \frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx + \frac{\sigma^2}{4} \frac{t}{t+1} \frac{d}{dt} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial x} \right)^2 (x,t) dx\]

\[\le \int_s^{+\infty} m \left( \frac{\partial z}{\partial x} \right)^2 \left( \frac{3}{2} \sigma^2 m' + \nu m \right)^2 (x,t) dx\]

\[+ \lambda^2 \int_s^{+\infty} m^3 \int_0^{+\infty} (z(x-\xi, t) - z(x,t))^2 \mu(\xi) d\xi.\]

从已经获得的估计 (15.6.30) 我们推导出 (15.6.27)，并且还有
(15.6.31) \(\int_s^{+\infty} \frac{t}{t+1} \int_s^{+\infty} m^3(x) \left( \frac{\partial z}{\partial t} \right)^2 (x,t) dx dt \le C ||\varphi||^2.\)

## (15.6.27) 的证明：

令 \(x_0 \in [s_0, M]\)。取 \(\rho\) 使得
\(0 < \rho \le \frac{s_0 - s}{2}.\)

我们记
\(z_R(x,t) = E \mathbb{1}_{Y_x(t) \ge R}.\)

我们使用估计
\(\int_s^{+\infty} m^3(x) \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \le C \frac{t+1}{t},\)
且常数不依赖于 R。特别是我们推导出
(15.6.32) \(\int_s^{M + \frac{s_0 - s}{2}} \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \le C_{s_0, M} \left( 1 + \frac{1}{t} \right),\)

这里我们使用了 \(m(x)\) 在区间 \([\frac{s+s_0}{2}, M + \frac{s_0-s}{2}]\) 上有正下确界的事实。现在我们有
\[\int_s^{+\infty} m(x) z_R(x,t) dx = \int_s^{+\infty} m(x) \mathbb{1}_R(x) dx = \int_R^{+\infty} m(x) dx\]
\[\ge \int_{x_0 - \rho}^{+\infty} m(x) z_R(x,t) dx\]

现在对于 \(x \in [x_0 - \rho, x_0 + \rho]\) 我们有
\(|z_R(x,t) - z_R(x_0,t)| \le \rho^{\frac{1}{2}} \left( \int_{\frac{x+x_0}{2}}^{M + \frac{x_0-x}{2}} \left( \frac{\partial z_R}{\partial x} \right)^2 (x,t) dx \right)^{\frac{1}{2}} \le \rho^{\frac{1}{2}} (C_{s_0, M})^{\frac{1}{2}} \left( 1 + \frac{1}{t} \right)^{\frac{1}{2}} .\)

现在假设 \(t \ge \delta\) 并设
\(C_{s_0, M, \delta} = (C_{s_0, M})^{\frac{1}{2}} \left( 1 + \frac{1}{\delta} \right)^{\frac{1}{2}} ,\)

我们可以写，使用先前的估计
\(\int_R^{+\infty} m(x) dx \ge (z_R(x_0, t) - \rho^{\frac{1}{2}} C_{s_0, M, \delta}) \int_{x_0 - \rho}^{x_0 + \rho} m(x) dx ,\)

从而
\(z_R(x_0, t) \le \rho^{\frac{1}{2}} C_{s_0, M, \delta} + \frac{\int_R^{+\infty} m(x) dx}{\int_{x_0 - \rho}^{x_0 + \rho} m(x) dx} ,\)

因此也
\(\sup_{x \in [s_0, M]} \sup_{t \ge \delta} z_R(x_0, t) \le \rho^{\frac{1}{2}} C_{s_0, M, \delta} + \frac{\int_R^{+\infty} m(x) dx}{\inf_{x \in [s_0, M]} \int_{x - \frac{\rho}{2}}^{x + \frac{\rho}{2}} m(\xi) d\xi} .\)

令 \(R \to +\infty\)，然后 \(\rho \to 0\)，我们得到性质 (15.6.27)。这个论证是

## 连续性证明 (15.6.43)：

我们首先证明在固定正 \(t\) 时，\(z(x,t)\) 在 \((s, +\infty)\) 内关于 \(x\) 的连续性。这是估计 (15.6.27) 的直接结果。确实，对于任何固定的正 \(t\) 和任何紧集 \([s_0, M]\)，\(z(x,t)\) 在 \(x\) 上的偏导数在 \(L^2(s_0, M)\) 中有界。因此它在 \([s_0, M]\) 上是 \(x\) 的连续函数。所以剩下的是证明在 \(s\) 处的右连续性，即

(15.6.33) \(z(s + \epsilon, t) \to z(S, t) \forall t > 0, \text{ as } \epsilon \to 0 .\)

由于在 \(s\) 的左侧，\(z(x,t) = z(S,t)\)，性质 (15.6.33) 将意味着在任何点处关于 \(x\) 的连续性。回顾在 15.6.1 节中引入的记号 \(\tau_{x,n}\) 以表征轨迹 \(y_x(t)\)，其中 \(\tau_{x,0} = 0, \tau_{x,1} = \tau_x^S\) 且

与
\(\tau_{x,n+1} = \tau_{x,n} + X_{x,n}, \quad n \ge 1 ,\)
\(X_{x,n} = \inf \{ u \ge 0 | S - D(\tau_{x,n} + u) + D(\tau_{x,n}) \} .\)

变量 \(X_{x,n}\) 是独立的且具有相同的概率分布，即 \(\tau_x^S\) 的分布。如果我们定义
\(F_x(t) = \mathbb{E}[\mathbb{I}_{\tau_x^S < t}] ,\)

那么 \(X_{x,n}\) 的概率分布是 \(F_S(t)\)。注意
\(y_x(t) = \begin{cases} x - D(t), & \text{if } t < \tau_x^S \\ S - D(t) + D(\tau_{x,n}), & \text{if } \tau_{x,n} \le t < \tau_{x,n+1} \end{cases}\)

我们可以然后得到 \(z(x,t), t > 0\) 的公式。我们有
\(z(x,t) = E\varphi(x - D(t)) \mathbb{I}_{t < \tau_x^S} + \sum_{n=1}^{+\infty} E\varphi(S - D(t) + D(\tau_{x,n})) \mathbb{I}_{\tau_{x,n} \le t < \tau_{x,n+1}}\)

定义

\(\Psi(x,t) = E\varphi(x - D(t)) \mathbb{1}_{t < \tau_x^S},\)

然后，回顾 \(\mathcal{F}^t = \sigma(D(s), s \le t)\)，通过相对于 \(\mathcal{F}^{\tau_{x,n}}\) 条件化并使用独立性性质，可以检查

\(E\varphi(S - D(t) + D(\tau_{x,n})) \mathbb{1}_{\tau_{x,n} \le t < \tau_{x,n+1}} = E\mathbb{1}_{\tau_{x,n} \le t} \Psi(S, t - \tau_{x,n}), n \ge 1.\)

由于

\(\tau_{x,n} = \tau_x^S + \sum_{j=1}^{n-1} X_{n,j}, n \ge 2,\)

使用独立性性质，我们容易检查

\(E\mathbb{1}_{\tau_{x,n} \le t} = F_x \otimes F_S^{(n-1)}(t),\)

其中 \(F_S^{(n-1)}\) 表示概率分布 \(F_S\) 的 \(n-1\) 次卷积。累积分布函数 \(F_S(t)\) 具有密度 \(f_S(t)\) 且

\(dF_S^{(n-1)}(t) = f_S^{(n-1)}(t)dt.\)

注意对于 \(n=1\) 没有密度且 \(f_S^{(0)}(t) = 1, \forall t > 0\)。在这种情况下 \(f_S^{(0)}(t)dt\) 必须被 0 处的 Dirac 测度所取代。汇总结果我们可以最终写出公式

(15.6.34) \(z(x,t) = \Psi(x,t) + \sum_{n=1}^\infty \int_0^t f_x(t-\eta) \left( \int_0^\eta \Psi(S, \xi) f_S^{(n-1)}(\eta - \xi) d\xi \right) d\eta\)

所以我们必须考虑

(15.6.35) \(z(s+c, t) = \Psi(s+c, t) + \int_0^t f_{s+c}(t-\eta) \Psi(S, \eta) d\eta + \sum_{n=2}^\infty \int_0^t f_{s+c}(t-\eta) \left( \int_0^\eta \Psi(S, \xi) f_S^{(n-1)}(\eta - \xi) d\xi \right) d\eta\)

然而 \(\Psi(x,t)\) 是柯西问题的解

(15.6.36) \(\frac{\partial \Psi}{\partial t} + A\Psi = 0, \quad x > s\)
\(\Psi(x,t) = 0, \quad x \le s\)
\(\Psi(x,0) = \varphi(x)\)

这是一个具有 Dirichlet 边界条件的经典柯西问题。注意解不依赖于 \(x \le s\) 时 \(\varphi(x)\) 的值。然后可以标准地检查

\(\Psi(s+c, t) \to 0, \text{ as } \epsilon \to 0, \forall t > 0.\)

现在如果我们在 (15.6.35) 中取 \(\varphi(x) = 1\)，那么我们看到

\(E\mathbb{1}_{t < \tau_x^{++}} \to 0, \text{ as } \epsilon \to 0, \forall t > 0.\)

这意味着

\(\mathbb{1}_{t < \tau_x^{++}} \to 0 \text{ a.s. as } \epsilon \to 0, \forall t > 0.\)

然后很容易检查

\(E \frac{\tau_x^{s+\epsilon}}{1 + \tau_x^{s+\epsilon}} \to 0,\)

并且也 \(\sigma_t^{r++} \to 0\)，几乎必然。但然后我们可以在公式 (15.6.35) 中取极限并得到

\(z(s + \epsilon, t) \to \Psi(S,t) + \sum_{m=2}^\infty \int_0^t \Psi(S, \xi) f_S^{(m-1)}(t - \xi) d\xi\)
\(= z(S,t)\)

最后的等式通过与 (15.6.34) 比较来检查。

## (15.6.26) 的证明：

我们首先证明一个较弱的结果。令 \(0 < a_0 \le \frac{M}{2}\)，那么我们有

(15.6.37) \(\sup_{s+a_0 \le x \le M} |\varphi_\epsilon(x) - \varphi(x)| \to 0, \text{ as } \epsilon \to 0.\)

这个结果需要 \(\varphi\) 的连续性（但不一定是 \(\varphi(s) = \varphi(S)\)）。我们使用

\(\varphi_\epsilon(x) = \frac{1}{\epsilon} E \int_0^{+\infty} \exp\left(-\frac{t}{\epsilon}\right) \varphi(y_\epsilon(t)) dt\)
\(= E \int_0^{+\infty} \exp(-u) \varphi(y_\epsilon(\epsilon u)) du\)

对于固定的 \(T\) 设置

\(\varphi_\epsilon^T(x) = E \int_0^T \exp(-u) \varphi(y_\epsilon(\epsilon u)) du,\)

并且

(15.6.38) \(|\varphi_\epsilon(x) - \varphi_\epsilon^T(x)| \le ||\varphi|| \exp(-T).\)

接下来我们断言对于 \(u \le T\)

\(E\varphi(y_\epsilon(\epsilon u)) = E\varphi(x - D(\epsilon u)) + E(\varphi(y_\epsilon(\epsilon u)) - \varphi(x - D(\epsilon u))) \mathbf{I}_{\tau_\epsilon^z \le T},\)

因此对于 \(u \le T\)

(15.6.39) \(|E\varphi(y_\epsilon(\epsilon u)) - E\varphi(x - D(\epsilon u))| \le 2||\varphi|| E \mathbf{I}_{\tau_\epsilon^z \le T}.\)

很容易看出

\(E \mathbf{I}_{\tau_\epsilon^z \le T} \le P \left( \nu \epsilon T + \sigma \sup_{0 \le u \le T} w(u) + N(\epsilon T) \ge a_0 \right) = \Theta_{a_0}(\epsilon T).\)

这个量当然在 \(\nu \epsilon T \ge a_0\) 时等于 1。为了在 \(\nu \epsilon T < a_0\) 时评估这个量，我们将回顾以下概率分布

\(P \left( \sup_{0 \le u \le T} w(u) \le y \right) = \frac{2}{\sqrt{2\pi T}} \int_0^y \exp\left(-\frac{\xi^2}{2T}\right) d\xi\)

（参见 I. Karatzas, S. Shreve [27]），并且

\(P(N(\epsilon T) \le y) = 1 - \lambda \epsilon T \int_y^{+\infty} \mu(\eta) d\eta + o(\epsilon)\)

但然后

\(P \left( N(\epsilon T) + \sigma \sup_{0 \le u \le T} w(u) \ge y \right) \le \lambda \epsilon T + P \left( \sigma \sup_{0 \le u \le T} w(u) \ge y \right).\)

