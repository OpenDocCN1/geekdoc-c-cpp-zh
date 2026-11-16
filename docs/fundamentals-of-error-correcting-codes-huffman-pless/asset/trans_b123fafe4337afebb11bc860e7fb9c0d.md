

回顾一个在 $\mathbb{F}_q$ 上的 $[n, k]$ 广义Reed-Solomon码定义为

$$GRS_k(\gamma, v) = \{(v_0 f(\gamma_0), v_1 f(\gamma_1), \dots, v_{n-1} f(\gamma_{n-1})) \mid f \in \mathcal{P}_k\},$$

其中 $\gamma = (\gamma_0, \gamma_1, \dots, \gamma_{n-1})$ 是 $\mathbb{F}_q$ 中 $n$ 个不同元素的 $n$ 元组，$v = (v_0, v_1, \dots, v_{n-1})$ 是 $\mathbb{F}_q$ 中 $n$ 个非零元素的 $n$ 元组，且 $\mathcal{P}_k$ 是 $\mathbb{F}_q[x]$ 中次数不超过 $k-1$（包括零多项式）的多项式集合。假设 $c = c_0 c_1 \dots c_{n-1} \in GRS_k(\gamma, v)$ 被发送，且 $y' = y'_0 y'_1 \dots y'_{n-1} = c + e$ 被接收。那么存在唯一的 $f \in \mathcal{P}_k$，使得对 $0 \le i \le n-1$ 有 $c_i = v_i f(\gamma_i)$。如果我们能确定多项式 $f$，就可以找到 $e$。令 $\mathcal{A} = \{(\gamma_0, y_0), (\gamma_1, y_1), \dots, (\gamma_{n-1}, y_{n-1})\}$，其中 $y_i = y'_i / v_i$。暂时假设在 $c$ 的传输中没有发生错误。那么对于 $0 \le i \le n-1$ 有 $y_i = c_i / v_i = f(\gamma_i)$。特别是，$\mathcal{A}$ 的所有点都位于多项式 $p(x, y) = y - f(x)$ 上。现在假设发生错误。稍微改变我们之前的术语，定义一个 *错误定位多项式* $\Lambda(x, y)$ 为 $\mathbb{F}_q[x, y]$ 中的任意多项式，使得对所有满足 $y_i \neq c_i / v_i$ 的 $i$ 有 $\Lambda(\gamma_i, y_i) = 0$。由于如果 $y_i = c_i / v_i$ 则 $y_i - f(\gamma_i) = 0$，$\mathcal{A}$ 的所有点都位于多项式 $p(x, y) = \Lambda(x, y)(y - f(x))$ 上。Sudan-Guruswami 算法的基本思想是找到一个多项式 $p(x, y) \in \mathbb{F}_q[x, y]$，其中 $\mathcal{A}$ 的每个元素都是具有特定重数的根，然后找到该多项式形式为 $y - f(x)$ 的因式。对 $p(x, y)$ 施加进一步限制，以保证算法的纠错能力。

### 针对 $[n, k, n-k+1]$ 码 $GRS_k(\gamma, v)$ 的 Sudan-Guruswami 解码算法

- I. 固定一个正整数 $m$。选取 $\delta$ 为满足下式的最小正整数
  
  $$\frac{nm(m+1)}{2} < N_{k-1}(\delta). \tag{5.21}$$

  回顾 $N_{k-1}(\delta)$ 是 $(1, k-1)$-加权次数不超过 $\delta$ 的一项式 $x^i y^j$ 的数量。令

  $$t = \left\lfloor \frac{\delta}{m} \right\rfloor + 1.$$

- II. 构造一个非零多项式 $p(x, y) \in \mathbb{F}_q[x, y]$，使得 $\mathcal{A}$ 的每个元素都是 $p(x, y)$ 重数至少为 $m$ 的根，且 $p(x, y)$ 的 $(1, k-1)$-加权次数至多为 $\delta$。

- III. 找出 $p(x, y)$ 所有形式为 $y - f(x)$ 的因式，其中 $f(x) \in \mathcal{P}_k$ 且对于至少 $t$ 个 $i$ 值满足 $f(\gamma_i) = y_i$。对于每个这样的 $f$，在 $GRS_k(\gamma, v)$ 中生成对应的码字。

我们必须验证该算法可行，并给出其可纠正的错误数量上界。需要以下三个引理。

### 引理 5.4.15
设 $(\alpha, \beta) \in \mathbb{F}_q^2$ 是 $p(x, y) \in \mathbb{F}_q[x, y]$ 的一个重数至少为 $m$ 的根。如果 $f(x)$ 是 $\mathbb{F}_q[x]$ 中的一个多项式，使得 $f(\alpha) = \beta$，那么 $g(x) = p(x, f(x)) \in \mathbb{F}_q[x]$ 可被 $(x - \alpha)^m$ 整除。

**证明：** 设 $f_1(x) = f(x + \alpha) - \beta$。根据假设，$f_1(0) = 0$，因此 $f_1(x) = x f_2(x)$ 对某个多项式 $f_2(x) \in \mathbb{F}_q[x]$ 成立。定义 $g_1(x) = p(x + \alpha, f_1(x) + \beta)$。由于 $(\alpha, \beta)$ 是 $p(x, y)$ 重数至少为 $m$ 的根，$p(x + \alpha, y + \beta)$ 没有次数小于 $m$ 的一项式。在 $p(x + \alpha, y + \beta)$ 中令 $y = f_1(x) = x f_2(x)$ 表明 $g_1(x)$ 可被 $x^m$ 整除，这意味着 $g_1(x - \alpha)$ 可被 $(x - \alpha)^m$ 整除。然而，$g_1(x - \alpha) = p(x, f_1(x - \alpha) + \beta) = p(x, f(x)) = g(x)$，表明 $g(x)$ 可被 $(x - \alpha)^m$ 整除。

### 引理 5.4.16
固定正整数 $m, t, \text{and } \delta$，使得 $mt > \delta$。设 $p(x, y) \in \mathbb{F}_q[x, y]$ 为一个多项式，使得 $(\gamma_i, y_i)$ 是 $p(x, y)$ 重数至少为 $m$ 的根，对 $i \le n - 1$ 成立。此外，假设 $p(x, y)$ 的 $(1, k - 1)$-加权次数至多为 $\delta$。设 $f(x) \in \mathcal{P}_k$，其中对于 $0 \le i \le n - 1$ 中至少 $t$ 个 $i$ 值满足 $y_i = f(\gamma_i)$。那么 $y - f(x)$ 整除 $p(x, y)$。

**证明：** 设 $g(x) = p(x, f(x))$。由于 $p(x, y)$ 的 $(1, k - 1)$-加权次数至多为 $\delta$，$g(x)$ 要么是零多项式，要么是次数至多为 $\delta$ 的非零多项式。假设 $g(x)$ 非零。令 $S = \{i \mid 0 \le i \le n - 1, f(\gamma_i) = y_i\}$。根据引理 5.4.15，对于 $i \in S$，$(x - \gamma_i)^m$ 整除 $g(x)$。由于 $\gamma_i$ 互不相同，$h(x) = \prod_{i \in S} (x - \gamma_i)^m$ 整除 $g(x)$。由于 $h(x)$ 的次数至少为 $mt > \delta$，而 $\delta$ 是 $g(x)$ 的最大次数，如果 $g(x)$ 非零则会产生矛盾。因此 $g(x)$ 是零多项式，这意味着 $y = f(x)$ 是将 $p(x, y)$ 视为 $x$ 的有理函数域上的 $y$ 多项式时的一个根。根据除法算法，$y - f(x)$ 是该多项式的一个因式。

### 引理 5.4.17
设 $p(x, y) = \sum_j \sum_t p_{j,t} x^j y^t \in \mathbb{F}_q[x, y]$。假设 $(\alpha, \beta) \in \mathbb{F}_q^2$ 且 $p'(x, y) = \sum_a \sum_b p'_{a,b} x^a y^b = p(x + \alpha, y + \beta)$。那么

$$p'_{a,b} = \sum_{j \ge a} \sum_{t \ge b} \binom{j}{a} \binom{t}{b} \alpha^{j-a} \beta^{t-b} p_{j,t}.$$

**证明：** 我们有

$$p'(x, y) = \sum_j \sum_t p_{j,t} (x + \alpha)^j (y + \beta)^t$$

$$= \sum_j \sum_t p_{j,t} \sum_{a=0}^j \binom{j}{a} x^a \alpha^{j-a} \sum_{b=0}^t \binom{t}{b} y^b \beta^{t-b}.$$

显然，$x^a y^b$ 的系数 $p'_{a,b}$ 正如所声称的那样。

现在我们有立场验证 Sudan-Guruswami 算法，并给出算法有效的误差界限。

### 定理 5.4.18
将 Sudan-Guruswami 解码算法应用于 $[n, k, n - k + 1]$ 码 $GRS_k(\gamma, v)$ 将生成所有与接收向量汉明距离不超过 $e$ 的码字，其中 $e = n - \lfloor \delta/m \rfloor - 1$。

**证明：** 我们首先必须验证步骤 II 中的多项式 $p(x, y)$ 确实存在。为了使 $p(x, y)$ 存在，$p(x + \gamma_i, y + y_i)$ 必须对 $0 \le i \le n - 1$ 没有次数小于 $m$ 的项。根据引理 5.4.17，如果对于每个 $0 \le i \le n - 1$，

$$\sum_{j \ge a} \sum_{t \ge b} \binom{j}{a} \binom{t}{b} \gamma_i^{j-a} y_i^{t-b} p_{j,t} = 0 \quad \text{for all } a \ge 0, b \ge 0 \text{ with } a + b < m. \quad (5.22)$$

则可实现这一点。对于每个 $i$，(5.22) 中有 $(m(m + 1))/2$ 个方程，因为集合 $\{(a, b) \in \mathbb{Z}^2 \mid a \ge 0, b \ge 0, a + b < m\}$ 的大小为 $(m(m + 1))/2$；因此在未知系数 $p_{j,t}$ 中总共有 $(nm(m + 1))/2$ 齐次线性方程。由于我们希望生成一个 $(1, k - 1)$-加权次数至多为 $\delta$ 的非平凡多项式，在这个 $(nm(m + 1))/2$ 齐次线性方程组中总共有 $N_{k-1}(\delta)$ 个未知系数 $p_{j,t}$。根据 (5.21)，方程数少于未知数，因此存在非平凡解，步骤 II 可以完成。根据步骤 I 中对 $t$ 的选择，$mt > \delta$。如果 $f(x) \in \mathcal{P}_k$ 是一个多项式，对于至少 $t$ 个 $i$ 值满足 $f(\gamma_i) = y_i$，根据引理 5.4.16，$y - f(x)$ 是 $p(x, y)$ 的一个因式。因此，算法的步骤 III 将生成所有与接收向量距离不超过 $e = n - t = n - \lfloor \delta/m \rfloor - 1$ 的码字。

由于步骤 I 需要计算 $N_{k-1}(\delta)$，下一个引理很有用。

### 引理 5.4.19
设 $s$ 和 $\delta$ 为正整数。那么 $N_s(\delta) = \left( \delta + 1 - \frac{s}{2} \left\lfloor \frac{\delta}{s} \right\rfloor \right) \left( \left\lfloor \frac{\delta}{s} \right\rfloor + 1 \right) \ge \frac{\delta(\delta + 2)}{2s}$。

**证明：** 按定义，$N_s(\delta) = \sum_{i=0}^{\lfloor \delta/s \rfloor} (\delta + 1 - is) = (\delta + 1) \left( \left\lfloor \frac{\delta}{s} \right\rfloor + 1 \right) - \frac{s}{2} \left\lfloor \frac{\delta}{s} \right\rfloor \left( \left\lfloor \frac{\delta}{s} \right\rfloor + 1 \right) \ge \left( \left\lfloor \frac{\delta}{s} \right\rfloor + 1 \right) \left( \delta + 1 - \frac{\delta}{2} \right) \ge \frac{\delta}{s} \cdot \frac{\delta + 2}{2}$。

结果得证。

### 示例 5.4.20
设 $\mathcal{C}$ 为在 $\mathbb{F}_{16}$ 上的 $[15, 6, 10]$ Reed-Solomon码。Peterson-Gorenstein-Zierler 解码算法最多可纠正四个错误。如果在 Sudan-Guruswami 解码算法中选择 $m = 2$，则 $(nm(m + 1))/2 = 45$，且使 $45 < N_s(\delta)$ 成立的最小 $\delta$ 值为 $\delta = 18$，在这种情况下，根据引理 5.4.19，$N_s(18) = 46$。那么 $t = \lfloor \delta/m \rfloor + 1 = 10$，根据定理 5.4.18，Sudan-Guruswami 算法可以纠正 $15 - 10 = 5$ 个错误。

### 练习 311
设 $\mathcal{C}$ 为示例 5.4.20 中的码。在 Sudan-Guruswami 算法中选择 $m = 6$。证明使 $(nm(m + 1))/2 = 315 < N_s(\delta)$ 成立的最小 $\delta$ 值为 $\delta = 53$。验证使用这些参数时 Sudan-Guruswami 算法可以纠正六个错误。

### 练习 312
设 $\mathcal{C}$ 为在 $\mathbb{F}_{32}$ 上的 $[31, 8, 24]$ Reed-Solomon码。Peterson-Gorenstein-Zierler 算法最多可纠正 11 个错误。(a) 在 Sudan-Guruswami 算法中选择 $m = 1$。找出使 $(nm(m + 1))/2 = 31 < N_s(\delta)$ 成立的最小 $\delta$ 值。使用 $m = 1$，Sudan-Guruswami 算法可以纠正多少个错误？

