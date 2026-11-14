

并且必须有

$$L_{-k+1} \ge L_{-k} \ge L_{-k^*} \ge k^* + 2.$$

由此可得

$$z_n = y_n + \sum_{-k^* \le k \le n-1 \\ k+L_k \ge n+1} v_k.$$

当然，订单 $v_{-k}$ 是已知的。因此，只需给出时刻 1 的库存位置，即 $z_1 = z$。考虑成本目标

$$J(V) = \sum_{j=1}^\infty \alpha^{j-1} EC(v_j) + \sum_{j=1}^\infty \alpha^{j-1} El(y_j).$$

基于我们对提前期的假设，函数 $n + L_n$ 关于 $k$ 严格单调递增。因此我们可以写成

$$J(V) = \sum_{j=1}^\infty \alpha^{j-1} EC(v_j) + E \sum_{j=1}^\infty \alpha^{j-1} El(y_j) + \sum_{n=1}^\infty E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j)$$

接下来

$$E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = E \alpha^{n+L_{n-1}-2} \sum_{k=0}^{L_n-L_{n-1}-1} \alpha^k l(y_{n-1+L_{n-1}+k}).$$

然而

$$y_{n-1+L_{n-1}+k} = y_{n-1+L_{n-1}} - (D_{n-1+L_{n-1}} + \cdots + D_{n-2+L_{n-1}+k}), \quad 0 \le k \le L_n - L_{n-1},$$ 其中当 $k=0$ 时求和省略。这是因为在时刻 $n-1+L_{n-1}+k$（$1 \le k \le L_n - L_{n-1}$）没有订单到达。考虑到 $y_{n-1+L_{n-1}+1}$ 的值，我们得到

$$y_{n-1+L_{n-1}+k} = z_n - (D_n + \cdots + D_{n-2+L_{n-1}+k}), \quad 0 \le k \le L_n - L_{n-1}.$$

因此

$$\sum_{n=1}^\infty E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = \sum_{n=1}^\infty E \alpha^{n+L_{n-1}-2} \cdot L_n - L_{n-1} \sum_{k=0}^{L_n-L_{n-1}} \alpha^k l(z_n - (D_n + \cdots + D_{n+L_{n-1}+k-2})).$$

定义函数

(13.2.41) $$\lambda(i, x) = El(x - (D_1 + \cdots + D_i)), \quad i \ge 0,$$ 其中当 $i=0$ 时求和省略。因此，$\lambda(0, x) = l(x)$。

从独立性性质出发，可以写成

$$\sum_{n=1}^\infty E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = \sum_{n=1}^\infty \alpha^{n-1} E \alpha^{L_{n-1}-1} \sum_{k=0}^{L_{n-1}-1} \alpha^k \lambda(L_{n-1}-1+k; z_n)$$

接下来定义

(13.2.42) $$\bar{I}_n(x) = E \alpha^{L_{n-1}-1} \sum_{k=0}^{\epsilon_{n-1}} \alpha^k \lambda(L_{n-1} + 1 + k, x).$$

从需求和提前期的独立性出发，我们得到

$$\sum_{n=1}^{\infty} E \sum_{n+L_{n-1}-1}^{n+L_n-1} \alpha^{j-1} El(y_j) = \sum_{n=1}^{\infty} \alpha^{n-1} E \bar{I}_n(z_n).$$

接下来，量 \(E \sum_{j=1}^{L_n-1} \alpha^{j-1} El(y_j)\) 是固定的，与控制无关。因此我们最终得到以下优化问题

(13.2.43) $$J_\epsilon(V) = \sum_{n=1}^{\infty} \alpha^{n-1} E C(v_n) + \sum_{n=1}^{\infty} \alpha^{n-1} E \bar{I}_n(z_n),$$

伴随演化 (13.2.40)。这个问题不是标准的，因为它是非平稳的。每个周期 \(n\) 的成本取决于 \(n\)。为了简化记号，本书未处理非平稳问题。然而，动态规划的技术可以适应无限时域的非平稳问题。与有限时域情况不同，它不会归约为一个序列。它仍然是一个函数方程，因为无法启动该序列。

如果 \(L_n = L$（随机），则 \(\epsilon_n = 0$。在这种情况下

$$\bar{I}_n(x) = \bar{I}(x) = E \alpha^{L-1} \lambda(L-1, x),$$

如果 $L$ 是确定的，我们恢复 (13.2.8)。

## 13.3. 没有库存位置的模型

### 13.3.1. 订购约束

我们考虑第 13.2.1 节的模型，其中提前期 $L$ 是确定的。然而，我们将在订购过程中引入一个约束。当有未决订单时，不能下单。因此，未决订单的数量最多为一个。订购策略 \(V\) 由一系列订购时刻组成

$$\tau_1, \cdots, \tau_j, \cdots,$$

它们是 \(\mathcal{F}^{n-1}$ 停时。对每个订购时刻 \(\tau_j\)，关联一个数量 \(v_{\tau_j}\)，它是 \(\mathcal{F}^{\tau_j-1}$ 可测的，即订购量。新的元素是通常条件 \(\tau_j \le \tau_{j+1}$ 被约束所取代

$$\tau_{j+1} \ge \tau_j + L.$$

库存演化如下

$$y_{n+1} = y_n + v_n - D_n, \quad y_1 = x,$$

其中

$$v_n = 0, \quad \text{if } n \neq \tau_j, \text{ for some } j.$$

目标函数与通常相同

$$J_\epsilon(V) = \sum_{n=1}^{\infty} \alpha^{n-1} (l(y_n) + C(v_n)),$$

价值函数是

$$u(x) = \inf_V J_\epsilon(V).$$

### 13.3.2. 动态规划

考虑到初始时刻的可能性，很容易推导出 Bellman 方程。如果时刻 0 没有订单，那么可以达到的最佳结果是

$$l(x) + \alpha E u(x - D).$$

另一方面，如果在时刻 0 下一个大小为 $v$ 的订单，由于没有未决订单，这是可能的，那么库存演化如下

$$y_1 = x;$$
$$y_2 = x - D_1;$$
$$\dots$$
$$y_{L+1} = x - (D_1 + \dots + D_L) + v,$$

可以达到的最佳结果是

$$K + c v + l(x) + E \sum_{j=2}^L \alpha^{j-1} l(-(D_1 + \dots + D_{j-1})) + \alpha^L E u(x + v - (D_1 + \dots + D_L)).$$

从这些考虑中，我们可以轻松推导出 Bellman 方程

(13.3.1) $$u(x) = \min \left\{ \begin{array}{l} l(x) + \alpha E u(x - D), \\ K - c x + E \sum_{j=0}^{L-1} \alpha^j l(x - D^{(j)}) + \inf_{\eta \ge x} \{ c \eta + \alpha^L E u(\eta - D^{(L)}) \} \end{array} \right\}$$

其中我们使用记号

$$D^{(j)} = D_1 + \dots + D_j \text{ if } j \ge 1, \text{ if } j = 0$$

### 13.3.3. (s, S) 策略

首先，通过引入常数 $s \in R$，并将 $u(x)$ 变换为 $H_s(x)$，使用公式来变换 (13.3.1)

(13.3.2) $$u(x) = -c x + E \sum_{j=0}^{L-1} \alpha^j l(x - D^{(j)}) + C_s + H_s(x),$$

其中 $C_s$ 将在下面定义。事实上，令

$$g(x) = (1 - \alpha) c x + \alpha^L E l(x - D^{(L)}),$$

然后取

$$C_s = \frac{g(s) + \alpha c \bar{D}}{1 - \alpha},$$

其中 \(\bar{D}\) 是 \(D\) 的期望值。

我们然后注意公式

$$E \sum_{j=0}^{L-1} \alpha^j g(x - D^{(j)}) = c x (1 - \alpha^L) - \alpha c \bar{D} \frac{1 - \alpha^L}{1 - \alpha} + \alpha^L c D L + E \sum_{j=0}^{L-1} \alpha^{j+L} l(x - D^{(j+L)})$$

我们然后检查 \(H_s(x)\) 是以下方程的解

(13.3.3) $$H_s(x) = \min \left\{ \begin{array}{l} g(x) - g(s) + \alpha E H_s(x - D), \\ K + \inf_{\eta \ge x} \left[ E \sum_{j=0}^{L-1} \alpha^j (g(\eta - D^{(j)}) - g(s)) + \alpha^L E H_s(\eta - D^{(L)}) \right] \end{array} \right\}.$$

另一方面，对于任何 \(s\)，我们以唯一的方式定义以下方程的解

(13.3.4) $$H_s(x) = g(x) - g(s) + \alpha E H_s(x - D), \quad x \ge s$$
$$= 0, \quad x \le s$$

我们在 (13.3.3) 和 (13.3.4) 之间使用了相同的记号 \( H_s(x) $，因为我们想要找到 \(s\)，使得 (13.3.4) 的解也是 (13.3.3) 的解。记 \( \mu(x) = g'(x) $，(13.3.4) 的解明确给出为

(13.3.5) $$H_s(x) = \int_s^x \Gamma(x - \eta) f(\eta) d\eta, x > s,$$

其中我们回顾 \( \Gamma(x) $ 是以下方程的解

(13.3.6) $$\Gamma(x) = 1 + \alpha \int_0^x \Gamma(x - \eta) f(\eta) d\eta, x > 0.$$

令

$$g_s(x) = (g(x) - g(s)) \mathbb{I}_{x \ge s},$$

那么 (13.3.4) 的解满足

(13.3.7) $$H_s(x) = g_s(x) + \alpha E H_s(x - D), \forall x.$$

从这个关系出发，经过迭代我们推导出

$$H_s(x) = E \sum_{j=0}^{L-1} \alpha^j g_s(x - D^{(j)}) + \alpha^L E H_s(x - D^{(L)}),$$

因此还有

$$E \sum_{j=0}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) + \alpha^L E H_s(x - D^{(L)}) = H_s(x) + E \sum_{j=0}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) \mathbb{I}_{x - D^{(j)} < s},$$

定义

(13.3.8) $$\Psi_s(x) = H_s(x) + E \sum_{j=0}^{L-1} \alpha^j (g(x - D^{(j)}) - g(s)) \mathbb{I}_{x - D^{(j)} < s},$$

那么如果我们希望 \( H_s(x) $ 满足 (13.3.3)，我们必须有

(13.3.9) $$H_s(x) = \min \left\{ g(x) - g(s) + \alpha E H_s(x - D), K + \inf_{\eta > x} \Psi_s(\eta) \right\}.$$

这个关系激励了 \(s\) 的选择。我们想要找到 \(s\)，使得

(13.3.10) $$K + \inf_{\eta > s} \Psi_s(\eta) = 0.$$

如果这样的 \(s\) 存在，我们定义 \( S = S(s) $ 为取得下确点的点。

(13.3.11) $$\inf_{\eta > s} \Psi_s(\eta) = \Psi_s(S(s)).$$

注意，当 \( L = 1 \) 时，对于 \( x > s \)，\( \Psi_s(x) $ 与 \( H_s(x) $ 重合。

