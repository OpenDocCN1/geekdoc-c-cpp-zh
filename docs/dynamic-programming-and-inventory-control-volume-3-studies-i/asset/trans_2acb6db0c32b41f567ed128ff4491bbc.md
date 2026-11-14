
证明。注意，根据 $S_i$ 的定义，有

$$G_{i+1}(S_i) - G_i(S_i) \ge G_{i+1}(S_{i+1}) - G_i(S_{i+1}),$$

因此

$$(c_{i+1} - c_i)S_i \ge (c_{i+1} - c_i)S_{i+1},$$

从而

$$S_i \le S_{i+1}.$$

还具有以下性质

### 引理 11.2.

如果 $s_i \le s_j$，对 $i \le j$ 则 $w_i(x) \ge w_j(x)$ 对所有 $x$ 成立

**证明。** 如果 $x \le s_i$ 则

$$\begin{aligned} w_i(x) &= -c_i x + G_i(s_i) \\ &= -c_i x + (c_i - c_j)s_i + G_j(s_i) \\ \ge -c_i x + (c_i - c_j)s_i + G_j(s_i) \\ &= -c_i x + (c_i - c_j)s_i + w_j(x) + c_j x \\ \ge w_j(x) \end{aligned}$$

如果 $s_i \le x \le s_j$，则

$$\begin{aligned} w_i(x) &= -c_i x + G_i(x) \\ &= -c_i x + G_j(x) \\ \ge -c_i x + G_j(s_i) \\ &= w_j(x) \end{aligned}$$

最后，如果 $x \ge s_j$，则 $w_i(x) = w_j(x)$

证明结束。

因此可以舍弃供应商 $i$。因此剩下 $m \le M$ 个供应商，其配置如下

$$s_m < s_{m-1} < \cdots < s_1 \le S_1 \le \cdots \le S_m.$$

我们现在定义广义 $s, S$ 策略的概念（参见定理陈述）。它由一个双序列组成

$$s_m^* < s_{m-1}^* < \cdots < s_i^* < S_i < S_2 \cdots < S_m,$$

伴随反馈

$$\delta(x) = \begin{cases} S_m, & \text{if } x \le s_m^* \\ S_i, & \text{if } s_{i+1}^* < x \le s_i^*, i = 1, \cdots, m-1 \\ x, & \text{if } x > s_1^* \end{cases}$$

回顾 $\delta(x) = \delta_{i(x)}(x)$，我们看到广义 $s, S$ 策略只有在以下条件下才可能

$$s_i^* \le s_i, s_1^* = s_1.$$

我们可以将优化问题的主要结果表述如下

### 定理 11.4.

(11.2.10) 中的函数 \( w(x) \) 通过广义 \( s,S \) 策略得到。具体来说，存在 $m \le M$ 和 $[1, \cdots, M]$ 的一个子集，我们可以将其按递增顺序重新编号为 $[1, \cdots, m]$，以及一个关联序列 $s_i^*$，满足 $s_i^* > s_{i+1}^*, s_i^* \le s_i, s_1^* = s_1$，使得

$$w(x) = \begin{cases} -c_m x + G_m(s_m), & \text{if } x \le s_m^*, i(x) = m \\ -c_i x + G_i(s_i), & \text{if } s_{i+1}^* < x \le s_i^*, i=1, \cdots, m-1, i(x)=i \\ -c_1 x + G_1(x), & \text{if } x > s_1^* = s_1, \text{no order} \end{cases}$$

**证明。** 定义

$$s_{ij} = \frac{G_i(s_i) - G_j(s_j)}{c_i - c_j};$$

$$s_j^* = \min \left( s_{j1}, \min_{i=1,\cdots,j-1} s_{ij} \right).$$

我们将证明

$$i(x) \text{ may be chosen } \ge j \text{ if } x \le s_j^*$$
$$i(x) \text{ may be chosen } \le j - 1 \text{ if } x > s_j^*$$

事实上，如果 $x \le s_j^*$，则

$$w_j(x) = -c_j x + G_j(s_j),$$

并且对于 $i \le j-1$，$x \le s_{ij}$ 蕴含

$$x \le \frac{G_i(s_i) - G_j(s_j)}{c_i - c_j}.$$

因此

$$w_j(x) \le -c_i x + G_i(s_i), \forall i \le j-1.$$

然而

$$w_i(x) = \begin{cases} -c_i x + G_i(s_i), & \text{if } x \le s_i \\ -c_{i+1} x + G_i(x), & \text{if } x > s_i \end{cases}$$

还要注意

$$w_i(x) \le -c_i x + G_i(x), \forall x.$$

因此如果 $x \le s_i$，我们可以断言 $w_i(x) \ge w_j(x)$。另一方面，如果 $x > s_i$，则 $w_i(x) = -c_{i+1}x + G_i(x) \ge w_j(x)$。所以第一部分已证明。

假设现在 $x > s_j^*$，我们要证明存在某个 $i \le j-1$，使得 $w_i(x) \le w_j(x)$。有几种情况。如果 $s_j^* = s_i$，则 $w_j(x) = -c_j x + G_j(x)$，因此

$$w_j(x) = -c_i x + G_i(x) \ge w_i(x) \forall i \neq j.$$

假设 $s_j^* = \min_{i=1,\cdots,j-1} s_i < s_j$，那么如果 $x \ge s_j$，我们有与之前相同的情况。剩下的情况是 $s_j^* < x < s_j$。在这种情况下，$w_j(x) = -c_j x + G_i(s_i)$，并且存在 $i \le j-1$，使得 $s_{ij} = s_j^* < x$，这蕴含 $w_j(x) > -c_{i+1}x + G_i(s_i)$。而且 $s_i > s_j$，因为 $i \le j-1$。因此 $x < s_i$，且 $w_i(x) = -c_{i+1}x + G_i(s_i)$。我们立即得到 $w_i(x) < w_j(x)$。所以我们已经证明存在 $i \le j-1$，优于或等价于 $j$。

由此可得

$$s_i^* \le s_j^*$$

那么供应商 $i$ 永远不会被选择。事实上，我们知道如果 $x \le s_j^*$，我们可以在供应商 $j, \cdots, M$ 中选择，因此索引 $i$ 可以被排除。另一方面，如果 $x > s_j^* \ge s_i^*$，那么 $i$ 和 $j$ 都可以被排除。因此我们消除所有索引 $i$，使得存在 $j > i$ 且 $s_i^* \le s_j^*$。剩下 $m$ 个索引，且 $s_i^*$ 递减。我们可以重新编号它们，并以此定义序列 $s_1^* > s_2^* > \dots > s_m^*$。由此可知，如果 $s_{i+1}^* < x \le s_i^*$，则 $i(x)$ 可以在大于或等于 $i$ 的索引中选择，但我们可以排除 $i+1, \dots, m$，因此 $i$ 是最优的。如果 $x > s_1^* = s_1$，我们可以消除所有索引，因此不订购是最优的。

证明已完成。

我们现在证明函数 $w$ 的一些性质

### 推论 11.1.

函数 $w(x)$ 在 $(-\infty, a_1]$ 上递减，且 $w(x) + c_1 x$ 在 $[a_1, +\infty)$ 上是 $K_1$ 非递减的。

**证明。** 回顾 $w(x)$ 是连续的。从引理 11.4 中证明的公式可知，$w(x)$ 在 $(-\infty, s_1]$ 上递减，并且根据 $G_1$ 的性质，在 $(s_1, a_1)$ 上也递减。第二部分显而易见。

让我们检查 $w$ 的其他性质。

### 推论 11.2.

$w(x) + c_i x$ 在整条直线 $R$ 上是 $K_i$ 非递减的。假设 $a_m \ge 0$，则 $w(x) + c_m x$ 在 $(-\infty, 0]$ 上递减。

**证明。** 注意到 $G_i(x) = G_1(x) + (c_i - c_1)x$。

我们可以写出 $G_i^*(x) = \inf_{y \ge x} \{ K_i \mathbb{I}_{y > x} + G_1(y) - c_1 y + c_i y \}$。

因为 $w_i(x) = -c_i x + G_i^*(x)$。

由此可得 $w_i(x) = \inf_{y \ge x} \{ K_i \mathbb{I}_{y > x} + c_i(y - x) + G_1(y) - c_1 y \}$。

由此可得 $w(x) = \inf_{z \ge x} \{ C(z - x) + G_1(z) - c_1 z \}$。

其中 $C(z) = \min_{i=1}^m \{ K_i \mathbb{I}_{z > 0} + c_i z \}$。

取 $y \ge x$，则 $w(x) \le \inf_{z \ge y} \{ C(z - x) + G_1(z) - c_1 z \}$。

并且根据 $C(z)$ 的次可加性，以及 $z \ge y \ge x$，可得 $w(x) \le w(y) + C(y - x)$。

由此我们推断 $w(x) \le w(y) + K_i + c_i(y - x)$，对所有 $i$ 成立。

因此 $w(x) + c_i x$ 在整条直线 $R$ 上是 $K_i$ 非递减的。接下来

$$w(x) + c_m x = \begin{cases} G_m(s_m), & \text{if } x \le s_m^* \\ (c_m - c_i)x + G_i(s_i), & \text{if } s_{i+1}^* < x \le s_i^* \\ (c_m - c_1)x + G_1(x), & \text{if } x > s_1^* \end{cases}$$

事实上，可以观察到 $w(x) + c_m x = G_m(x)$，如果 $x > s_1^*$。

从上述表达式，使用 $c_m \le c_i$ 对所有 $i$，以及 $a_m \ge 0$ 的事实，因此 $G_m(x)$ 在 $(-\infty, 0]$ 上递减，推论 11.2 的第二部分随之得出。

## 11.2.3. 多供应商问题的应用。

要将前面的结果应用于多供应商问题，我们需要一个额外的中间结果。考虑一个分段连续的函数 $\psi(x)$，当 $|x| \to +\infty$ 时趋于 $+\infty$，因此达到其最小值。设 $D$ 为一个正随机变量，密度为 $f$。量 $\chi(x) = E\psi(x - D)$ 是一个连续函数，当 $x \to +\infty$ 时也趋于 $+\infty$。

练习 11.6。证明前述性质。使用 $\psi(x)$ 达到其最小值这一事实。

然而，如果 $\psi$ 在 $(-\infty, a]$ 上递减，且在 $[a, +\infty)$ 上是非 $K$ 递减的，那么该性质不会传递给 $\chi$。只要 $\psi$ 是准 $K$ 凸的，就会出现同样的糟糕情况。在 $K$ 凸的情况下，该性质会传递。不过要注意，$\chi(x)$ 在 $(-\infty, a]$ 上递减，并且由于当 $x \to +\infty$ 时它趋于 $+\infty$，必然存在某个 $b \ge a$，使得 $\chi(x)$ 在 $(-\infty, b]$ 上递减，之后可能增加。因此 $b$ 是一个局部最小值。我们希望将自己限制在分布 $f$ 上，使得以下性质 $\mathcal{P}$ 成立：函数 $\chi$ 在 $[b, +\infty)$ 上是非 $K$ 递减的。

让我们证明，每当分布 $f$ 是泊松分布或泊松分布的卷积时，性质 $\mathcal{P}$ 成立。假设 $f$ 是参数为 $\lambda$ 的泊松分布，则 $f(x) = \lambda \exp -\lambda x$。

练习 11.7。验证 $\chi'(x) = \lambda(\psi(x) - \chi(x))$。

设 $S$ 为 $\chi$ 的最小值。由于 $\chi'(b) = \chi'(S) = 0$，我们有 $\chi(S) = \psi(S)$ 且 $\chi(b) = \psi(b)$。设 $h > 0$。考虑函数 $z(x) = \chi(x) - \chi(x + h) - K$，则我们有 $z(b) \le \chi(b) - \chi(S) - K = \psi(b) - \psi(S) - K \le 0$，因为 $a \le b \le S$。

练习 11.8。验证 $z'(x) \le -\lambda z(x)$。

因此 $\frac{dz}{dx} \exp \lambda x \le 0$，

由此可得 $z(x) \exp \lambda x \le z(b) \exp \lambda b$，对所有 $x \ge b$ 成立，因此 $z(x) \le 0$，对所有 $x \ge b$ 成立。这意味着 $\chi$ 对 $x \ge b$ 是 $K$ 非递减的。性质 $\mathcal{P}$ 传递到泊松分布的卷积。事实上，如果 $D = \sum_{j=1}^J D_j$，
