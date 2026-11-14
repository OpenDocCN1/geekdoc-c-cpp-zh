

汇总结果可得

(15.6.40) \(\Theta_{a_\epsilon}(T\epsilon) \le \lambda \epsilon T + \frac{2}{\sqrt{2\pi}} \int_0^{+\infty} \frac{a_0 - \nu \epsilon T}{\sigma \sqrt{\epsilon T}} \exp -\frac{\xi^2}{2} d\xi.\)

接下来，若 \(|D(\epsilon u)| < a_0\)，则有 \(x - D(\epsilon u) \in [s, M]\)。由于 \(\varphi(x)\) 在 \([s, M]\) 上一致连续，存在一个函数 \(\gamma_M(\delta)\)，它单调递增，且当 \(\delta\) 趋于 0 时趋于 0，并且

\(|\varphi(x') - \varphi(x'')| \le \gamma_M(\delta) \text{ if } |x' - x''| \le \delta.\)

因此

\(|\varphi(x - D(\epsilon u)) - \varphi(x)| \le \gamma_M(|D(\epsilon u)|) + 4||\varphi|| \mathbb{I}_{|D(\epsilon u)| \ge a_0}.\)

由于

\(|D(\epsilon u)| \le \nu \epsilon T + \sigma \sup_{0 \le u \le \epsilon T} w(u) + N(\epsilon T),\)

我们得到

\(E|\varphi(x - D(\epsilon u)) - \varphi(x)| \le E \gamma_M \left( \nu \epsilon T + \sigma \sup_{0 \le s \le \epsilon T} w(u) + N(\epsilon T) \right) + 4||\varphi|| \Theta_{a_\epsilon}(T\epsilon).\)

最后，对于 \(s + a_0 \le x \le M\)，我们得到估计

\(|\varphi_\epsilon(x) - \varphi(x)| \le 2||\varphi|| \exp -T + 6||\varphi|| \Theta_{a_\epsilon}(T\epsilon) + E \gamma_M \left( \nu \epsilon T + \sigma \sup_{0 \le s \le \epsilon T} w(u) + N(\epsilon T) \right),\)

以及

\(E \gamma_M \left( \nu \epsilon T + \sigma \sup_{0 \le s \le \epsilon T} w(u) + N(\epsilon T) \right) \le \frac{2}{\sqrt{2\pi}} \int_0^{+\infty} \gamma_M(\nu \epsilon T + \sigma \sqrt{\epsilon T} \xi) \exp -\frac{\xi^2}{2} d\xi + \frac{2}{\sqrt{2\pi}} \lambda \epsilon T \int_0^{+\infty} \exp -\frac{\xi^2}{2} \left( \int_0^{+\infty} \gamma_M(\nu \epsilon T + \sigma \sqrt{\epsilon T} \xi + v) \mu(v) dv \right) d\xi.\)

我们可以汇总估计并写出

\(|\varphi_\epsilon(x) - \varphi(x)| \le 2||\varphi|| \exp -T + C_M(\epsilon T),\)

以及

\(C_M(\epsilon T) \to 0, \text{ as } \epsilon T \to 0.\)

结果 (15.6.37) 易得。

我们现在完成 (15.6.26) 的证明。我们假设 \(\varphi(s) = \varphi(S)\)。首先，利用此假设并假设

\(s + a_0 < S < M, \quad s + 2a_0 < M\)

（\(a_0\) 将取很小值，因此这不是限制），然后应用 (15.6.37)

\(\sup_{s \le x \le M} |\varphi_\epsilon(x) - \varphi(x)| \le \max \left[ \sup_{s+a_0 \le x \le M} |\varphi_\epsilon(x) - \varphi(x)|, \sup_{s \le x \le s+a_0} |\varphi_\epsilon(x) - \varphi(x)| \right]\)

\(\le \sup_{s+a_0 \le x \le M} |\varphi_\epsilon(x) - \varphi(x)| + \sup_{s \le x \le s+a_0} |\varphi_\epsilon(x) - \varphi(x)| + \sup_{s \le x \le s+a_0} |\varphi(x) - \varphi(s)|.\)

第一项由 (15.6.37) 得出，第三项将通过 \(\varphi(x)\) 在 \([s, M]\) 上的一致连续性来处理。因此我们专注于第二项。我们可以写出

\[
\varphi_t(x) - \varphi(s) = \int_0^T \exp -u \, E(\varphi(y_\epsilon(\epsilon u)) - \varphi(s)) du + \int_T^{+\infty} \exp -u \, E(\varphi(y_\epsilon(\epsilon u)) - \varphi(s)) \exp -T.
\]

考虑 \(u \le T\)，然后在考虑可能的情况后，人们可以确信以下关系

\[
E\varphi(y_\epsilon(\epsilon u)) - \varphi(s) = -\varphi(s) E\mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| \ge a_0} + E\mathbb{I}_{\tau_T^s > \epsilon u} \mathbb{I}_{|D(\epsilon u)| \ge a_0})
\]
\[
+ E(\varphi(x - D(\epsilon u)) - \varphi(s)) \mathbb{I}_{\tau_T^s > \epsilon u} \mathbb{I}_{|D(\epsilon u)| < a_0}
\]
\[
+ E\varphi(S - D(\epsilon u) + D(\tau_T^s)) \mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| \ge a_0}
\]
\[
+ E(\varphi(S - D(\epsilon u) + D(\tau_T^s)) - \varphi(S)) \mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| < a_0}
\]
\[
+ E\varphi(y_\epsilon(\epsilon u)) \mathbb{I}_{\tau_{a_1, s} \le \epsilon u}.
\]

我们然后考虑以下估计

\(\mathbb{I}_{|D(u)| \ge a_0} \le \nu_{cT+N(T)} + s \mathbb{I}_{\sup_{0 \le u \le T} w(u)} + \mathbb{I}_{\nu_{cT} + N(\epsilon T) + \sigma \sup_{0 \le u \le \epsilon T} w(u)}\)

因此

\(E\mathbb{I}_{|D(u)| \ge a_0} \le 2\Theta_{a_0}(\epsilon T).\)

经过一些额外的努力，我们还可以验证

\(E\mathbb{I}_{\tau_T^s \le \epsilon u} \mathbb{I}_{|D(u) - D(\tau_T^s)| \ge a_0} \le 2\Theta_{a_0}(\epsilon T);\)

\(E\mathbb{I}_{\tau_{a_1, s} \le u} \le \Theta_{S-s}(\epsilon T).\)

另外

\(E|\varphi(x - D(\epsilon u)) - \varphi(s)| \mathbb{I}_{|D(\epsilon u)| < a_0} \le \gamma_M(2a_0);\)

\(E|\varphi(S - D(\epsilon u) + D(\tau_T^s)) - \varphi(S)| \mathbb{I}_{|D(\epsilon u) - D(\tau_T^s)| < a_0} \le \gamma_M(a_0),\)

其中 \(\gamma_M(\delta)\) 是 \(\varphi(x)\) 在 \([s, M]\) 上的连续性模量。汇总结果，我们可以断言对于 \(u \le T\)

\(|E\varphi(y_\epsilon(u)) - \varphi(s)| \le ||\varphi|| (4\Theta_{a_*}(\epsilon T) + \Theta_{S-s}(\epsilon T)) + \gamma_M(2a_0) + \gamma_M(a_0),\)

因此

\(\sup_{s \le u \le s+a_0} |\varphi_t(x) - \varphi(s)| \le ||\varphi|| (4\Theta_{a_*}(\epsilon T) + \Theta_{S-s}(\epsilon T) + 2 \exp -T) + \gamma_M(2a_0) + \gamma_M(a_0),\)

这意味着

\(\limsup_{\epsilon \to 0} \sup_{s \le u \le s+a_0} |\varphi_t(x) - \varphi(s)| \le 2 ||\varphi|| \exp -T + \gamma_M(2a_0) + \gamma_M(a_0).\)

因此也

\(\limsup_{\epsilon \to 0} \sup_{s \le u \le s+a_0} |\varphi_t(x) - \varphi(s)| \le 2 ||\varphi|| \exp -T + \gamma_M(2a_0) + \gamma_M(a_0)\)
\(+ \sup_{s \le u \le s+a_0} |\varphi(x) - \varphi(s)|.\)

令 \(a_0\) 趋于 0，然后 \(T\) 趋于 \(+\infty\)，我们看到右边为 0。这完成了中间结果的证明，从而也完成了定理 15.5 的证明。

### 15.6.4. 查普曼-科尔莫戈罗夫方程。

从公式 (15.6.34) 可以看出，对于任何 \(t > 0\)，\(y_\tau(t)\) 都有一个密度。这直接源于 \(x - D(t)\) 在 \(t > 0\) 时有一个密度这一事实。因此，对于 \(\varphi(x) \ge 0\),

\[
\Psi(x, t) \le E\varphi(x - D(t)) = \int \varpi(\xi, t)\varphi(\xi)d\xi,
\]

其中 \(\varpi(\xi, t)\) 是 \(x - D(t)\) 的密度。因此我们可以写出

\[
z(x, t) = E\varphi(y_\tau(t)) = \int p(\xi, t)\varphi(\xi)d\xi,
\]

并且 \(p(\xi, t)\) 是变量 \(y_\tau(t)\) 的密度。形式上我们可以写出

\[
p(\xi, 0) = \delta(\xi - x).
\]

由于当 \(\varphi = 0\) 在 \((s, +\infty)\) 上时 \(z(x, t) = 0\)（再次参见公式 (15.6.34)），我们有对于 \(\xi \le s\) 的 \(p(\xi, t) = 0\)。查普曼-科尔莫戈罗夫方程描述了 \(p(\xi, t)\) 的演化。通过与不变量度类似的考虑，我们可以推导这个方程并得到

\[
\frac{\partial p}{\partial t} - \frac{\sigma^2}{2} \frac{\partial^2 p}{\partial \xi^2} - \nu \frac{\partial p}{\partial \xi} - \lambda \int_0^{+\infty} (p(\xi + \eta, t) - p(\xi, t)) \mu(\eta) d\eta = 0, \quad \text{if } \xi > s
\]
\[
p(\xi, t) = 0, \quad \text{if } \xi \le s
\]
\[
p(\xi, 0) = \delta(\xi - x)
\]

我们已经证明了弱收敛

\[
\int p(\xi, t)\varphi(\xi)d\xi \to \int m(\xi)\varphi(\xi)d\xi, \quad \text{as } t \to +\infty.
\]

注意 \(\frac{\partial p}{\partial \xi}\) 在 \(S\) 处有不连续点，关系为

\[
\frac{\sigma^2}{2} \left( \frac{\partial p}{\partial \xi}(S+0, t) - \frac{\partial p}{\partial \xi}(S-0, t) + \frac{\partial p}{\partial \xi}(s+0, t) \right) + \lambda \int_s^{+\infty} p(x, t) \int_{x-s}^{+\infty} \mu(\xi) d\xi = 0.
\]

我们不展开查普曼-科尔莫戈罗夫方程的细节，因为它没有显式解，且所有关于遍历理论的结果都可以绕过这个方程。

### 15.6.5. 与 s, S 策略相关的成本。

我们现在可以计算与由 (17.2.2) 定义的 s, S 策略相关的成本，适用于一般冲动控制。冲动时间是随机时间 \(\tau_n^s\)，冲动（订单）是 \(S - y_{\tau_n^s}^s(\tau_n^s - 0), \quad n \ge 1\)。回顾公式 (15.6.8)，并使用类似的推理，人们可以确信相关成本由以下给出

\[
u_\alpha^{s,S}(x) = E \int_0^{\tau^s} \exp - \alpha t f(y_{\tau^s}^s(t)) dt + E [\exp - \alpha \tau_s^s (K + c(S - y_{\tau^s}^s(\tau_s^s - 0)))] + E \exp - \alpha \tau_s^s \frac{E \int_0^{\tau^s} \exp - \alpha t f(y_{\tau^s}^s(t)) dt}{1 - E \exp - \alpha \tau_s^s} + E \exp - \alpha \tau_s^s \left[ \frac{\exp - \alpha \tau_s^s (K + c(S - y_{\tau^s}^s(\tau_s^s - 0)))}{1 - E \exp - \alpha \tau_s^s} \right].

