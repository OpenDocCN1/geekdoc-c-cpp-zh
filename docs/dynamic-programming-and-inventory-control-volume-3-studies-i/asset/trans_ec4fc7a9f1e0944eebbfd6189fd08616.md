
## 14.10. 带提前期的泊松需求：使用库存位置

### 14.10.1. 问题的表述。

考虑前一节定义的问题，我们稍微改变一下符号，因为系统的状态将不再是库存，而是一个新概念，称为_库存位置_。冲动控制仍将用

\( M(t; V) = \sum_{\{n|\theta_n < t\}} v_n, \)

表示，这次停止时间 \(\theta_n\) 没有约束。库存将用 \(\bar{y}_x(t; V)\) 表示。然而，\(x\) 并不代表初始库存，而是初始库存位置。

相对于实际库存，库存位置加上所有尚未交付的订单。因此，库存位置 \(y_x(t; V)\) 的演化由

\( y_x(t; V) = x - D(t) + M(t; V), \)

描述，其中 \(x\) 是其初始值，将在时间 \(L\) 成为库存的一部分。显然我们有关系

\(\bar{y}_x(t + L; V) = y_x(t; V) - D(t + L) + D(t).\)

该关系定义了大于 \(L\) 时刻的库存。在 \(L\) 之前，库存不受提前期区间内决策的影响。如果我们没有 0 之前订单的记录，那么 \(L\) 之前的库存就是时间 0 时的库存扣除需求后的结果。无论如何，相应的成本是固定的，没有优化的可能性。

对应于冲动控制 \(V\) 的成本由

\( J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) e^{-\alpha \theta_n} + \int_L^\infty f(\bar{y}_x(t; V)) e^{-\alpha t} dt \right] . \)

给出。在此表述中，我们没有包括区间 \(0, L\) 上的成本，它是一个常数。该成本可以立即写为

\( J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) e^{-\alpha \theta_n} + e^{-\alpha L} \int_0^\infty f(y_x(t; V) - D(t + L) + D(t)) e^{-\alpha t} dt \right] \)

我们注意到 \(D(t+L)-D(t)\) 与 \(y_x(t; V)\) 无关。因此，我们可以引入函数

\(\phi(x) = e^{-\alpha L} E f(x - D(L)),\)

成本由

\( J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) e^{-\alpha \theta_n} + \int_0^\infty \phi(y_x(t; V)) e^{-\alpha t} dt \right] . \)

给出。对于库存位置，我们得到与没有提前期的库存问题相同的问题，但积分成本 \(\phi(x)\) 代替 \(f(x)\)。相应的函数 \( g(x) \) 与前一节所考虑问题中进入的函数相同，见方程 (14.87)。

### 14.10.2. 值函数问题。

值函数

\( u(x) = \inf_V J_x(V), \)

满足一组不等式和互补条件

\( u(x) + cx \le K + \inf_{\eta \ge x} (c\eta + u(\eta)); \)

\( (\alpha + \lambda)u(x) - \lambda u(x-1) \le \phi(x); \)

\( [(\alpha + \lambda)u(x) - \lambda u(x-1) - \phi(x)][u(x) + cx - K - \inf_{\eta \ge x} (c\eta + u(\eta))] = 0. \)

### 14.10.3. s, S 策略。

与我们在无延迟情况下所做的一样，我们寻找一个函数 \( u_s(x) \)，使得

\( u_s(x) + cx = u_s(s) + cs, \forall x \le s \)

\( (\alpha + \lambda)u_s(x) - \lambda u_s(x-1) = \phi(x), \forall x \ge s \)

\( u_s(s) + cs = K + \inf_{\eta \ge s} (c\eta + u_s(\eta)). \)

最后一个表达式是关于 s 的方程，一旦函数 \( u_s(x) \) 唯一确定。为了定义任何 s 的 \( u_s(x) \)，我们需要 \( u_s(s) \) 的值。这个数由

\( u_s(s) = \frac{\phi(s) + \lambda c}{\alpha}. \)

给出。这促使引入函数 \( H_s(x) \)，它是以下方程的解

\( H_s(x) = 0, \forall x \le s \)

\( (\alpha + \lambda)H_s(x) - \lambda H_s(x-1) = \lambda g(x) - g(x), \forall x \ge s \)

\( 0 = K + \inf_{\eta \ge s} H_s(\eta), \)

函数 \( g(x) \) 由

\( g(x) = \phi(x) + \rho cx, \)

定义，这是上一节（14.8.7）中已引入的函数。我们有关系

\( H_s(x) = u_s(x) + cx - cs - \frac{\lambda c + \phi(s)}{\alpha}. \)

我们回顾 \( H_s(x) \) 的公式。

(14.10.1)
\( H_s(x) = \sum_{j=0}^{\lfloor x-s \rfloor} \frac{(g(x-j) - g(s))\lambda^j}{(\alpha + \lambda)^{j+1}}, \forall x \ge s; H_s(x) = 0, \forall x \le s. \)

14.6 节发展的理论适用，其中 \( g(x) \) 的最小值是 \(\hat{n}\)，它是一个正整数，而不是 0。

首先考虑 \( S(s) \)，它使 \( H_s(\eta), \eta \ge s \) 最小。我们有

\( S(s) = s, \text{ if } s > \hat{n}. \)

接下来考虑 \( s < \hat{n} \) 的情况。如同在 14.6 节中，我们证明 \( H_s(x) \) 在 \( (s, \infty) \) 上达到其最小值。选取最小的最小值 \( S(s) \)，我们为 \( s < \hat{n} \) 定义函数 \( S(s) \)。必然有

\( S(s) \ge \hat{n}. \)

剩下的就是找到 s。它必须满足关于 s 的方程

\[ \min_{n \ge s} H_n(s) = -K. \]

再次，14.6 节的理论证明了解 s 的存在性和唯一性。接下来我们可以陈述定理 14.2 的等价定理

定理 14.4。我们假设 \( c\alpha - p e^{-\alpha L} < 0 \)。那么，s, S 策略是最优的。

## 14.11. 带提前期的库存位置的遍历理论

### 14.11.1. 问题的表述。

我们现在考虑 \(\alpha = 0\)。问题归结为以下内容。首先

\[ g(x) = E f(x - D(L)), \]

和 \(\phi(x) = g(x)\)。

函数 \(H_s(x)\) 满足

\[ H_s(x) - H_s(x-1) = \frac{g(x) - g(s)}{\lambda}, \forall x \ge s; H_s(x) = 0, \forall x \le s. \]

对 s, S 由

\[ H_s(S) = \inf_{n \ge s} H_n(s) = -K. \]

定义。我们得到

\[ H_s(x) = \frac{1}{\lambda} \left[ \sum_{j=0}^{\lfloor x-s \rfloor} (g(x-j) - g(s)) \right]. \]

右导数满足

\[ H'_s(x+0) = \frac{1}{\lambda} \sum_{j=0}^{\lfloor x-s \rfloor} g'(x-j+0). \]

由于函数 \(H_s(x)\) 是分段线性的，\(H_s(x)\) 的计算归结为使用公式的 x 为整数的情况

\[ H_s(x) = H_s(\lfloor x \rfloor) + H'_s(\lfloor x \rfloor+0)(x-\lfloor x \rfloor). \]

因此我们可以考虑 x 为整数。那么

\[ H_s(x) = \frac{1}{\lambda} \sum_{j=0}^{x+\lfloor -s \rfloor} (g(x-j) - g(s)) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{x} (g(k) - g(s)), \]

和

\[ H'_s(x+0) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{x} g'(k+0). \]

为了得到整数 s, S，我们按以下步骤进行：我们写出条件

\[ H'_s(S+0) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{S} g'(k+0) \ge 0; \]

\[ H'_s(S-1+0) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{S-1} g'(k+0) < 0, \]

和

\[ H_s(S) = \frac{1}{\lambda} \sum_{k=-\lfloor -s \rfloor}^{S} (g(k) - g(s)) = -K. \]

接下来我们使用恒等式

\[ g(k+1) = g(-\lfloor -s \rfloor) + \sum_{j=-\lfloor -s \rfloor}^{k} g'(j+0). \]

第二个关系写为

\[ -K\lambda = (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1) + \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0)(S-j). \]

使用第一个条件，我们可以写出

(14.11.1)
\[ \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0)j < K\lambda + (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1); \]
\[ \sum_{j=-\lfloor -s \rfloor}^{S} g'(j+0)j \ge K\lambda + (g(-\lfloor -s \rfloor) - g(s))(S + \lfloor -s \rfloor + 1). \]

我们还加上

(14.11.2)
\[ \sum_{j=-\lfloor -s \rfloor}^{S-1} g'(j+0) < 0; \]
\[ \sum_{j=-\lfloor -s \rfloor}^{S} g'(j+0) \ge 0. \]

### 14.11.2. 近似。

如果我们用 s 的整数值近似 s，我们得到以下系统

(14.11.3)
\[ \sum_{j=s}^{S-1} g'(j+0)j < K\lambda; \]
\[ \sum_{j=s}^{S} g'(j+0)j \ge K\lambda. \]

(14.11.4)
\[ \sum_{j=s}^{S-1} g'(j+0) < 0; \]
\[ \sum_{j=s}^{S} g'(j+0) \ge 0. \]

首先我们注意到，如果忽略 \(K\)，我们得到基础库存策略

\( s = S = \bar{n}. \)

接下来我们用方程近似这些条件

\[ \sum_{j=s}^{S} g'(j+0) = 0, \]

和

\[ \sum_{j=s}^S jg'(j+0) = K\lambda. \]

我们对这些关系进行连续近似

(14.11.5)
\[ g(s) = g(S) \]
\[ \int_s^S xg'(x+0)dx = K\lambda \]

### 14.11.3. 解释。

我们可以通过对成本函数进行直接推理来恢复系统 (14.11.5)。我们考虑一对 s, S，假设它们是整数。应用 s, S 策略，库存的演化描述如下。设 Q = S - s，并依次定义停止时间序列

\[ T_{n+1} = T_n + \tau_n, T_0 = 0, \]

其中

\[ \tau_n = \inf\{t > 0 | D(T_n + t) - D(T_n) \ge Q\}, \]

并设 \(\tau_0 = \tau\)。

停止时间 \(\tau_n\) 是独立同分布的随机变量，分布与随机变量 \(\tau\) 相同。考虑从 S 开始的库存演化，记为 \(y_S(t)\)。我们有

\[ y_S(t) = S - D(t) + D(T_n), T_n \le t < T_{n+1}, \]

并且我们可以将 \(T_n\) 解释为

\[ T_{n+1} = \inf\{t \ge T_n | y_S(t-0) \le s\}, \]

和

\[ y_S(T_n) = S, y_S(T_n - 0) \le s. \]

定义

\[ C_\alpha(s, Q) = E \int_0^\infty e^{-\alpha t} \phi(y_S(t)) dt. \]

我们计算

\[ C_\alpha(s, Q) = \sum_{n=0}^\infty E \int_{T_n}^{T_{n+1}} e^{-\alpha t} \phi(S - D(t) + D(T_n)) dt, \]

\[ C_\alpha(s, Q) = \sum_{n=0}^\infty E e^{-\alpha T_n} \int_0^{\tau_n} e^{-\alpha t} \phi(S - D(T_n + t) + D(T_n)) dt, \]

并且根据独立性考虑

\[ C_\alpha(s, Q) = \sum_{n=0}^\infty E(e^{-\alpha \tau})^n E \int_0^\tau e^{-\alpha t} \phi(S - D(t)) dt. \]

最后我们得到

(14.11.6)
\[ C_\alpha(s, Q) = \frac{E \int_0^\tau e^{-\alpha t} \phi(S - D(t)) dt}{1 - E(e^{-\alpha \tau})} \]

现在考虑从任意值 x 开始的库存演化。我们首先定义

\[ \tau_x = \inf\{t > 0 | D(t) \ge x - s\}. \]
