

与

$$G(x, \eta) = \int_{\eta}^{x} \frac{\varpi(\xi)}{\varpi(\eta)} d\xi,$$

以及

$$
\frac{\varpi(\xi)}{\varpi(\eta)} = \exp - \frac{2}{\sigma^2} \left[ \frac{k}{2} (\xi - \eta)(\xi + \eta + 2\nu) - \nu(\xi - \eta) \right].
$$

对于 \(\xi \ge \eta \ge 0\)，有

$$
\frac{\varpi(\xi)}{\varpi(\eta)} \le \exp \frac{2\nu}{\sigma^2} (\xi - \eta),
$$

因此对于 \(x \ge \eta \ge 0\)

$$
G(x, \eta) \le \frac{\exp \frac{2\nu}{\sigma^2}(x - \eta) - 1}{\frac{2\nu}{\sigma^2}}.
$$

另外

$$
\varpi(x) \le \exp \frac{2\nu}{\sigma^2} x.
$$

我们在 (16.3.15) 中使用这些不等式，并注意到 \(y(0) = 1\) 且 \(\tilde{z}(\eta) \le 0\)。经过整理后，我们得到不等式

(16.3.16) $$
\tilde{z}(x) \ge \tilde{z}(0) + \frac{\alpha + k}{\nu} y(0) - \frac{\alpha + k}{\nu} \cdot \exp \frac{2\nu}{\sigma^2} x \left( y(0) - \int_0^x \tilde{z}(\eta) \exp - \frac{2\nu}{\sigma^2} \eta d\eta \right) - \frac{\alpha + k}{\nu} \int_0^x \tilde{z}(\eta) d\eta.
$$

我们接着引入函数 \(u(x)\)，它是以下方程的解

(16.3.17) $$
\begin{aligned}
u(x) = \tilde{z}(0) + \frac{\alpha + k}{\nu} y(0) - \frac{\alpha + k}{\nu} \cdot \exp \frac{2\nu}{\sigma^2} x \Bigg( y(0) - \int_0^x u(\eta) \exp - \frac{2\nu}{\sigma^2} \eta d\eta \Bigg) - \frac{\alpha + k}{\nu} \int_0^x u(\eta) d\eta.
\end{aligned}
$$

可以轻易验证 \(u(x)\) 满足

$$-\frac{\sigma^2}{2} u''(x) + \nu u'(x) + (\alpha + k)u(x) = 0,$$

并且还有

$$u(0) = \tilde{z}(0), \quad u'(0) = -\frac{2}{\sigma^2}(\alpha + k)y(0).$$

考虑方程

$$-\frac{\sigma^2}{2} \beta^2 + \nu \beta + (\alpha + k) = 0,$$

的根，记为 \(\beta_k < 0, \beta_k^* > 0\)，我们可以用公式表示函数 \(u(x)\)

(16.3.18) $$
\begin{aligned}
u(x) = \frac{\tilde{z}(0)}{\beta_k^* - \beta_k} (-\beta_k \exp \beta_k^* x + \beta_k^* \exp \beta_k x) - \frac{2}{\sigma^2} (\alpha + k)y(0) \frac{1}{\beta_k^* - \beta_k} (\exp \beta_k^* x - \exp \beta_k x).
\end{aligned}
$$

让我们验证 \(\tilde{z}(x) \ge u(x)\)。确实，如果令 \(w(x) = \tilde{z}(x) - u(x)\)，则有不等式

$$w(x) \ge \frac{\alpha + k}{\nu} k \int_0^x \left( \exp \frac{2\nu}{\sigma^2}(x - \eta) - 1 \right) w(\eta) d\eta,$$

因此

\( w(x) \ge - \frac{\alpha + k}{\nu} \int_0^x \left( \exp \frac{2\nu}{\sigma^2}(x - \eta) - 1 \right) w(\eta) d\eta; \)

\( w(x) \exp - \frac{2\nu}{\sigma^2} x \le \frac{\alpha + k}{\nu} \int_0^x \exp - \frac{2\nu}{\sigma^2} \eta \ w(\eta) d\eta. \)

根据 Gronwall 不等式，我们断言

\( w(x) - \exp \frac{2\nu}{\sigma^2} x = 0, \)

这意味着结果成立。回顾一下

\( \tilde{z}(0) = -y'(0) \exp -\frac{k\gamma^2}{\sigma^2} = \Phi'(0) \exp -\frac{k\gamma^2}{\sigma^2}; \)

\( y(0) = \Phi(0) = 1; \quad \beta_k \beta_k^* = -\frac{2}{\sigma^2}(\alpha + k); \quad \beta_k^* + \beta_k = \frac{2\nu}{\sigma^2}, \)

并重新整理后，我们可以写成

\( z(x) \exp \frac{k}{\sigma^2}(x+\gamma)^2 \ge \beta_k \exp -\beta_k x \frac{\beta_k^* - \Phi'(0) \exp -\frac{k\gamma^2}{\sigma^2}}{\beta_k^* - \beta_k} + \beta_k^* \exp -\beta_k^* x \frac{-\beta_k + \Phi'(0) \exp -\frac{k\gamma^2}{\sigma^2}}{\beta_k^* - \beta_k}. \)

最后，回顾 \( z(x) = \Phi'(x) - x \ge 0 \)，我们很容易推导出估计 (16.3.9)。我们有 \( \Phi(x) > 0, \Phi'(x) < 0 \)。让我们验证

(16.3.19) \( \quad \Phi'(x) \to -\infty, \text{ as } x \to -\infty. \)

确实，根据 (16.3.14)，\(\tilde{z}(x)\) 是严格递减的。因此

\( z(x) = \tilde{z}(x) \exp \frac{2}{\sigma^2} \left[ k \frac{(x+\gamma)^2}{2} - \nu x \right] \le \tilde{z}(0) \exp \frac{2}{\sigma^2} \left[ k \frac{(x+\gamma)^2}{2} - \nu x \right] \to -\infty, \text{ as } x \to +\infty \)

故 (16.3.19)。考虑 \(\Psi(x) = \Phi'(x)\)。它是 (16.3.12) 的一个解，且 \(\Psi(x) < 0, \forall x \le 0\)。此外

\( \Psi(x) \to -\infty, \text{ as } x \to -\infty \)

我们还知道 \(\Psi'(0) = \Phi''(0) > 0\)。必然有

\( \Psi'(x) = \Phi''(x) > 0, \forall x < 0 \)

否则将存在一点 \(x_0\)，使得 \(\Psi'(x_0) = 0\)。我们可以取最大的负数这样的点。它是 \(\Psi(x)\) 的一个局部最小值。但根据方程 (16.3.12)，\(\Psi(x)\) 在 \(x < 0\) 时不能有负的局部最小值。证明完成。\(\square\)

我们称 \(\Phi(x)\) 为问题 (16.3.3) 的 Green 函数，类比于线性 P.D.E. 的解。注意当 \(k=0\) 时，

\( \Phi(x) = \exp \beta x, \)

其中 \(\beta\) 是方程

\( -\frac{\sigma^2}{2} \beta^2 + \nu \beta + \alpha = 0. \)

的负根。

## 16.3.3. (16.3.3) 的解

得益于 Green 函数，我们可以给出 (16.3.3) 解的显式公式。令

(16.3.20)
$$
\vartheta(x) = \varpi(-x)
= \exp -\frac{2}{\sigma^2} \left[ k \frac{(x-\gamma)^2}{2} + \nu x \right].
$$

我们先考虑函数

(16.3.21)
$$
\chi(x) = \vartheta(x)\Phi(x), x \in R,
$$

它满足微分方程

(16.3.22)
$$
-\frac{\sigma^2}{2}\chi''(x) - (k(x-\gamma) + \nu)\chi'(x) + \alpha\chi(x) = 0
$$

$$
\chi(0) = \exp -\frac{k}{\sigma^2}\gamma^2, \chi(+\infty) = 0
$$

### Lemma 16.1

(16.3.22) 存在且仅存在一个解。此外

(16.3.23)
$$
\chi'(x) < 0, \chi(x) \to +\infty, \text{as } x \to -\infty.
$$

**Proof.** 由 (16.3.22) 定义的函数是一个解，通过直接检查可得。唯一性来自线性微分方程理论，与 \(\Phi(x)\) 的情况相同。我们只需证明 \(\chi'(x) < 0\)。必然有 \(\chi'(0) < 0\)，否则 \(\chi(x)\) 在 \(x > 0\) 且接近 0 时会增加。但随后，由于它在 \(x \to +\infty\) 时趋于 0，\(\chi(x)\) 将在 \((0, +\infty)\) 上有一个正的最大值，这是不可能的。然后我们有 \(\chi'(x) = \vartheta(x)\Phi'(x) - \frac{2}{\sigma^2}(k(x-\gamma) + \nu)\)。由于 \(\Phi'(x) < 0\)，对于 \(x \ge \gamma\)，有 \(\chi'(x) < 0\)。如果 \(\chi'(x)\) 在 \((0, \gamma)\) 的某点 \(x^*\) 处消失，则第一个这样的点必须是局部最小值。但随后 \(\chi(x)\) 在 \(x^*\) 之后，靠近 \(x^*\) 处会增加。但随后将有一个正的局部最大值，这是不可能的。因此，对于 \(x \ge 0\)，有 \(\chi'(x) < 0\)。当 \(x < 0\) 时，同样 \(\chi'(x)\) 不能消失并改变符号，否则 \(\chi(x)\) 将有一个正的局部最大值。它不能有拐点，因为二阶导数将为 0，而根据二阶方程 (16.3.22) 这是不可能的。\(\chi(x) \to +\infty\) 当 \(x \to -\infty\) 这一事实立即从 \(\chi'(x) < 0\) 且对于足够小的 \(x\) 有 \(\chi'(x) > 0\) 得出。

然后我们陈述

### Theorem 16.2

(16.3.3) 的解是唯一的，并由公式给出

(16.3.24)
$$
H_s(x) = \frac{2}{\sigma^2} \int_s^x \frac{\Phi(x)}{\Phi(\xi)} \left( \int_\xi^{+\infty} g(\eta) \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi, x \ge s.
$$

**Proof.** 首先要证明的是，由 (16.3.24) 定义的函数，为简洁起见称为 \(H_s(x)\)，是有界的。由于 \(g'(x)\) 是有界的，只需证明函数

$$
Z_s(x) = \frac{2}{\sigma^2} \int_s^x \frac{\Phi(x)}{\Phi(\xi)} \left( \int_\xi^{+\infty} \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi, x \ge s
$$

是有界的。从函数 \(\Phi(x)\) 和 \(\chi(x)\) 的性质可以轻易验证，只需证明 \(Z_0(x)\) 是有界的。但我们将证明

(16.3.25)
$$
Z_0(x) = \frac{1 - \Phi(x)}{\alpha + k}.
$$

确实，让我们按 (16.3.25) 定义 \(Z_0(x)\)。它是下式的一个有界解

(16.3.26) 
$$
-\frac{\sigma^2}{2} Z_0'' + (\nu + k(x - \gamma))Z_0' + (\alpha + k)Z_0 = 1, \quad x > 0
$$
$$
Z_0(0) = 0
$$

接着定义

$$
A(x) = \frac{Z_0(x)}{\Phi(x)} = - \frac{1}{\alpha + k} + \frac{1}{\alpha + k} \frac{1}{\Phi(x)}
$$

然后，通过直接计算，我们有

$$
A''(x) + A'(x) \left[ 2 \frac{\Phi'(x)}{\Phi(x)} - \frac{2}{\sigma^2}(\nu + k(x - \gamma)) \right] = - \frac{2}{\sigma^2 \Phi(x)},
$$

因此也有

$$
\frac{d}{dx} (A'(x) \Phi^2(x) \vartheta(x)) = - \frac{2}{\sigma^2} \Phi(x) \vartheta(x).
$$

但也从 \(A(x)\) 的定义可得

$$
A'(x) \Phi^2(x) \vartheta(x) = - \frac{1}{\alpha + k} \Phi'(x) \vartheta(x).
$$

由于在 \(x > 0\) 时，\(\Phi'(x)\) 是有界的，右边在 \(x \to +\infty\) 时趋于 0。因此，必然有

$$
A'(x) \Phi^2(x) \vartheta(x) = \frac{2}{\sigma^2} \int_x^{+\infty} \chi(\eta) d\eta.
$$

现在，由于 \(A(0) = 0\)，我们得到

$$
A(x) = \frac{2}{\sigma^2} \int_0^x \frac{1}{\Phi(\xi)} \left( \int_\xi^{+\infty} \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi,
$$

因此，\(Z_0(x)\) 也由公式给出

$$
Z_0(x) = \frac{2}{\sigma^2} \int_0^x \frac{\Phi(\eta)}{\Phi(\xi)} \left( \int_\xi^{+\infty} \frac{\chi(\eta)}{\chi(\xi)} d\eta \right) d\xi, \quad x \ge 0,
$$

这证明了右边也是有界的。接下来，由 (16.3.24) 定义的函数是 (16.3.3) 的解。

让我们证明有界解的唯一性。当然，只需证明

$$
AH_s(x) + (\alpha + k)H_s(x) = 0, \quad x > s
$$
$$
H_s(s) = 0
$$

的有界解为 0。假设 \(H_s(x)\) 变为严格正。它不能有正的局部最大值。否则，如果 \(x^*\) 是严格大于 \(s\) 的最小局部最大值，则

$$
H_s'(x^*) = 0, \quad H_s''(x^*) < 0,
$$

这会导致矛盾。因此 \(H_s(x) > 0\)。由于 \(H_s(x)\) 是有界的，我们必须有 \(H_s'(x) \to 0\)，当 \(x \to +\infty\)。考虑一点 \(x_0\)，使得 \(\nu + k(x_0 - \gamma) > 0\)。存在一点 \(x^*\)，使得 \(H_s''(x^*) < 0\)。在这一点上，再次出现矛盾。因此 \(H_s(x) \le 0\)。通过类似的推理，我们很容易看出 \(H_s(x)\) 不能变为严格负。因此它为 0。证明已完成。\(\square\)

