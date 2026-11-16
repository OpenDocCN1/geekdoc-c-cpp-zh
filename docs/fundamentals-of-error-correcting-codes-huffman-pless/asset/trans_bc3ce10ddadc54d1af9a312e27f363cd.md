

但是如果在坐标 $i$ 上对 $C_i(\alpha)$ 进行删短，你将得到一个 $(n-1, m_{i,\alpha}, d)$ 码，其码字权重为 $w-1$。因此 $m_{i,\alpha} \le A_q(n-1, d, w-1)$，从而

$$
wM = \sum_{\alpha \in \mathbb{F}_q^*} \sum_{i=1}^n m_{i,\alpha} \le q^* n A_q(n-1, d, w-1).
$$

因此，

$$
A_q(n, d, w) \le \left\lfloor \frac{nq^*}{w} A_q(n-1, d, w-1) \right\rfloor. \tag{2.11}
$$

通过归纳，反复使用 (2.11)，

$$
A_q(n, d, w) \le \left\lfloor \frac{nq^*}{w} \left\lfloor \frac{(n-1)q^*}{w-1} \left\lfloor \dots \left\lfloor \frac{(n-i+1)q^*}{w-i+1} A_q(n-i, d, w-i) \right\rfloor \dots \right\rfloor \right\rfloor \right\rfloor
$$

对任意 $i$ 成立。若 $d = 2e - 1$，令 $i = w - e + 1$；则根据定理 2.3.3(i)，$A_q(n-i, d, w-i) = A_q(n-w+e-1, 2e-1, e-1) = 1$，且此情形下部分 (ii) 成立。令 $i = w - e$，则 $A_q(n-i, d, w-i) = A_q(n-w+e, 2e, e) \le \frac{(n-w+e)q^*}{e}$，根据定理 2.3.3(ii)，此情形下部分 (ii) 同样成立。

部分 (iii) 和 (iv) 由 (i) 和 (ii) 在 $d = 2e - 1$ 时借助定理 2.3.3(iv) 得出。

例 2.3.7 在例 2.3.2 中我们证明了 $A_2(24, 8, 8) \ge 759$。受限约翰逊界不能用于对 $A_2(24, 8, 8)$ 求上界，但不受限约翰逊界可以。根据该界，

$$
A_2(24, 8, 8) \le \left\lfloor \frac{24}{8} \left\lfloor \frac{23}{7} \left\lfloor \frac{22}{6} \left\lfloor \frac{21}{5} \left\lfloor \frac{20}{4} \right\rfloor \right\rfloor \right\rfloor \right\rfloor \right\rfloor = 759.
$$

因此 $A_2(24, 8, 8) = 759$。

## 练习 100 执行以下操作：

- (a) 证明 $A_2(n, d, w) = A_2(n, d, n-w)$。提示：若 $\mathcal{C}$ 是长度为 $n$ 且所有码字权重均为 $w$ 的二进制恒重码，那么码 $\mathbf{1} + \mathcal{C}$ 是什么？

证明

$$
A_2(n, d, w) \le \left\lfloor \frac{n}{n-w} A_2(n-1, d, w) \right\rfloor.
$$

提示：使用 (a) 和 (2.11)。

- (c) 直接证明 $A_2(7, 4, 6) = 1$。

- (d) 利用部分 (b) 和 (c) 证明 $A_2(8, 4, 6) \le 4$。构造一个长度为 8、具有四个权重为 6 的码字且任意两码字间距离至少为 4 的二进制恒重码，从而证明 $A_2(8, 4, 6) = 4$。

- (e) 利用部分 (b) 和 (d) 证明 $A_2(9, 4, 6) \le 12$。

- (f) 使用不受限约翰逊界，对 $A_2(9, 4, 6)$ 和 $A_2(9, 4, 3)$ 的界是什么？注意根据部分 (a)，$A_2(9, 4, 6) = A_2(9, 4, 3)$。

- (g) 证明 $A_2(9, 4, 6) = 12$。提示：根据部分 (a)，$A_2(9, 4, 6) = A_2(9, 4, 3)$。存在一个二进制 $(9, 12, 4)$ 码，其所有码字权重均为 3，且对于每个坐标，恰好有四个码字在该坐标上为 1。

## 练习 101 执行以下操作：

- (a) 使用练习 100 中给出的技术证明 \( A_2(8, 4, 5) \le 8 \)。

- (b) 证明 \( A_2(8, 4, 5) = 8 \)。提示：根据练习 100，\( A_2(8, 4, 5) = A_2(8, 4, 3) \)。存在一个二进制 \( (8, 4, 4) \) 码，其所有码字权重均为 3，且对于每个坐标，恰好有三个码字在该坐标上为 1。

## 2.3.3 针对 \( A_q(n, d) \) 的约翰逊界

\( A_q(n, d, w) \) 的界也可用于由 Johnson [159] 给出 \( A_q(n, d) \) 的上界。从证明可以看出，这些界加强了球包界。证明的思路是不仅计算距离所有码字在 \( t = \lfloor (d-1)/2 \rfloor \) 以内的 \( \mathbb{F}_q^n \) 中的向量（即以码字为中心、半径为 $t$ 的不相交球面），还计算不在这些球面内且距离码字为 $t+1$ 的向量。为实现此目标，我们需要以下记号。若 \( \mathcal{C} \) 是 \( \mathbb{F}_q \) 上长度为 $n$ 的码，且 \( \mathbf{x} \in \mathbb{F}_q^n \)，令 \( d(\mathcal{C}, \mathbf{x}) \) 表示 \( \mathbf{x} \) 到 \( \mathcal{C} \) 的距离。即 \( d(\mathcal{C}, \mathbf{x}) = \min\{d(\mathbf{c}, \mathbf{x}) \mid \mathbf{c} \in \mathcal{C}\} \)。

## 定理 2.3.8（针对 \( A_q(n, d) \) 的约翰逊界）令 \( t = \lfloor (d-1)/2 \rfloor \)。

- (i) 若 \( d$ 为奇数，则
  $$
  A_q(n, d) \le \frac{q^n}{\sum_{i=0}^t \binom{n}{i}(q-1)^i + \frac{\binom{n}{t+1}(q-1)^{t+1}}{\binom{t+1}{t} - \left(\frac{d}{t}\right)} A_q(n, d, d)}.
  $$

- (ii) 若 \( d$ 为偶数，则
  $$
  A_q(n, d) \le \frac{q^n}{\sum_{i=0}^t \binom{n}{i}(q-1)^i + \frac{\binom{n}{t+1}(q-1)^{t+1}}{A_q(n, d, t+1)}}.
  $$

- (iii) 若 \( d$ 为奇数，则
  $$
  A_2(n, d) \le \frac{2^n}{\sum_{i=0}^t \binom{n}{i} + \frac{\binom{n}{t+1} - \binom{d}{t} A_2(n, d, d)}{\lfloor \frac{n}{t+1} \rfloor}}.
  $$

- (iv) 若 \( d$ 为偶数，则
  $$
  A_2(n, d) \le \frac{2^n}{\sum_{i=0}^t \binom{n}{i} + \left\lfloor \frac{n}{t+1} \right\rfloor}.
  $$ (2.12)

- (v) 若 \( d$ 为奇数，则
  $$
  A_2(n, d) \le \frac{2^n}{\sum_{i=0}^t \binom{n}{i} + \frac{\binom{n}{t} \left( \frac{n-t}{t+1} - \frac{n-t}{t+1} \right)}{\left\lfloor \frac{n}{t+1} \right\rfloor}}.
  $$ (2.13)

**证明：** 令 $\mathcal{C}$ 为 $\mathbb{F}_q$ 上的一个 $(n, M, d)$ 码。注意 $t$ 是 $\mathcal{C}$ 的包络半径；若 $d$ 为奇数则 $d = 2t + 1$，若 $d$ 为偶数则 $d = 2t + 2$。因此以码字为中心、半径为 $t$ 的球面不相交。这些球面中的向量恰好是距离 $\mathcal{C}$ 不超过 $t$ 的 $\mathbb{F}_q^n$ 中的向量。我们将把这些向量与距离 $\mathcal{C}$ 为 $t+1$ 的向量一起计数，并利用该计数得出我们的界。为此，令 $\mathcal{N}$ 为距离 $\mathcal{C}$ 为 $t+1$ 的向量集合；即 $\mathcal{N} = \{ \mathbf{x} \in \mathbb{F}_q^n \mid d(\mathcal{C}, \mathbf{x}) = t + 1 \}$。令 $|\mathcal{N}|$ 表示 $\mathcal{N}$ 的大小。因此，

$$
M \sum_{i=0}^t \binom{n}{i} (q-1)^i + |\mathcal{N}| \le q^n. \tag{2.14}
$$

因为左边的求和计算了以码字为中心、半径为 $t$ 的球面中的向量；参见 (1.11)。在我们对 $|\mathcal{N}|$ 得到下界后，我们的界将随之得出。

令 $\mathcal{X} = \{ (\mathbf{c}, \mathbf{x}) \in \mathcal{C} \times \mathcal{N} \mid d(\mathbf{c}, \mathbf{x}) = t + 1 \}$。为了得到 $|\mathcal{N}|$ 的下界，我们对 $|\mathcal{X}|$ 求出下界和上界估计。

我们首先对 $|\mathcal{X}|$ 求下界估计。令 $\mathcal{X}_c = \{ \mathbf{x} \in \mathcal{N} \mid (\mathbf{c}, \mathbf{x}) \in \mathcal{X} \}$。则

$$
|\mathcal{X}| = \sum_{\mathbf{c} \in \mathcal{C}} |\mathcal{X}_c|. \tag{2.15}
$$

固定 $\mathbf{c} \in \mathcal{C}$。令 $\mathbf{x} \in \mathbb{F}_q^n$ 为距离 $\mathbf{c}$ 为 $t+1$ 的向量，使得 $wt(\mathbf{c} - \mathbf{x}) = t + 1$。这样的向量 $\mathbf{x}$ 恰有

$$
\binom{n}{t+1}(q-1)^{t+1}
$$

这样的向量 $\mathbf{x}$ 是通过自由改变 $\mathbf{c}$ 的任意 $t+1$ 个坐标得到的。其中一些在 $\mathcal{X}_c$ 中，另一些不在。因为 $wt(\mathbf{c} - \mathbf{x}) = t + 1$，所以 $d(\mathcal{C}, \mathbf{x}) \le t + 1$。令 $\mathbf{c}' \in \mathcal{C}$ 且 $\mathbf{c}' \neq \mathbf{c}$。根据定理 1.4.1 的三角不等式，$d(\mathbf{c}', \mathbf{c}) = wt(\mathbf{c}' - \mathbf{x} + \mathbf{x} - \mathbf{c}) \le wt(\mathbf{c}' - \mathbf{x}) + wt(\mathbf{c} - \mathbf{x}) = wt(\mathbf{c}' - \mathbf{x}) + t + 1$，这意味着

$$
d - t - 1 \le wt(\mathbf{c}' - \mathbf{x}). \tag{2.16}
$$

若 $d = 2t + 2$，则 $wt(\mathbf{c}' - \mathbf{x}) \ge t + 1$，从而 $d(\mathcal{C}, \mathbf{x}) = t + 1$，因为 $\mathbf{c}' \in \mathcal{C}$ 是任意的，且我们之前已知 $d(\mathcal{C}, \mathbf{x}) \le t + 1$。因此所有这样的 $\mathbf{x}$ 都在 $\mathcal{X}_c$ 中，给出

$$
|\mathcal{X}_c| = \binom{n}{t+1}(q-1)^{t+1},
$$

因此

$$
|\mathcal{X}| = M \binom{n}{t+1}(q-1)^{t+1} \quad \text{if } d = 2t + 2. \tag{2.17}
$$

## 2.3 约翰逊上界

若 $d = 2t + 1$，则由 (2.16) 得 $wt(\mathbf{c}' - \mathbf{x}) \ge t$，从而 $t \le d(\mathcal{C}, \mathbf{x}) \le t + 1$。由于我们只想计算 $d(\mathcal{C}, \mathbf{x}) = t + 1$ 的 $\mathbf{x}$，因此将舍弃那些 $d(\mathcal{C}, \mathbf{x}) = t$ 的 $\mathbf{x}$。这样的 $\mathbf{x}$ 必须同时距离 $\mathcal{C}$ 中某个码字 $\mathbf{c}'$ 为 $t$ 且距离 $\mathbf{c}$ 为 $t+1$。根据三角不等式，$\mathbf{c}'$ 到 $\mathbf{c}$ 的距离最多为 $2t + 1 = d$；同时该距离至少也为 $d$，因为这是 $\mathcal{C}$ 的最小距离。因此我们有 $wt(\mathbf{c}' - \mathbf{c}) = 2t + 1$。可能的 $\mathbf{c}'$ 有多少个？由于集合 $\{ \mathbf{c}' - \mathbf{c} \mid \mathbf{c}' \in \mathcal{C} \}$ 构成一个长度为 $n$、最小距离为 $d$ 且码字权重均为 $d$ 的恒重码，因此这样的 $\mathbf{c}'$ 最多有 $A_q(n, d, d)$ 个。对于每个 $\mathbf{c}'$，有多少个 $\mathbf{x}$ 满足 $wt(\mathbf{x} - \mathbf{c}) = t + 1$ 且 $t = wt(\mathbf{c}' - \mathbf{x}) = wt((\mathbf{c}' - \mathbf{c}) - (\mathbf{x} - \mathbf{c}))$？由于 $wt(\mathbf{c}' - \mathbf{c}) = 2t + 1$，$\mathbf{x} - \mathbf{c}$ 是通过从 $\mathbf{c}' - \mathbf{c}$ 的 $2t + 1$ 个非零分量中任意选择 $t$ 个并将其置零得到的。这可以通过 $\binom{n}{t}$ 种方式完成。因此

$$
\binom{n}{t}(q-1)^{t+1} - \binom{d}{t} A_q(n, d, d) \le |\mathcal{X}_c|
$$

由 (2.15) 可得

$$
M \left[ \binom{n}{t+1} (q-1)^{t+1} - \binom{d}{t} A_q(n, d, d) \right] \le |\mathcal{X}| \quad \text{if } d = 2t + 1. \tag{2.18}
$$

我们现在准备好对 \( |\mathcal{X}|$ 求上界估计了。固定 $\mathcal{N}$ 中的 $\mathbf{x}$。$\mathcal{C}$ 中有多少个 $\mathbf{c}$ 满足 $d(\mathbf{c}, \mathbf{x}) = t + 1$？集合 $\{ \mathbf{c} - \mathbf{x} \mid \mathbf{c} \in \mathcal{C} \text{ 且 } d(\mathbf{c}, \mathbf{x}) = t + 1 \}$ 是一个长度为 $n$、码字权重为 $t+1$ 且最小距离为 $d$ 的恒重码，因为 $\mathbf{c}' - \mathbf{x} = (\mathbf{c} - \mathbf{x}) - (\mathbf{c}' - \mathbf{c}) = \mathbf{c}' - \mathbf{c}$。因此对于 $\mathcal{N}$ 中的每个 $\mathbf{x}$，最多有 $A_q(n, d, t + 1)$ 个 $\mathbf{c}$ 的选择使得 $d(\mathbf{c}, \mathbf{x}) = t + 1$。故 $|\mathcal{X}| \le |\mathcal{N}| A_q(n, d, t + 1)$，即

$$
\frac{|\mathcal{X}|}{A_q(n, d, t + 1)} \le |\mathcal{N}|. \tag{2.19}
$$

我们通过结合 (2.14)、(2.18) 和 (2.19) 得到界 (i)，并通过结合 (2.14)、(2.17) 和 (2.19) 得到界 (ii)。界 (iii) 和 (iv) 由 (i) 和 (ii) 得出，因为根据定理 2.3.3，$A_q(n, 2t + 1, t + 1) = A_q(n, 2t + 2, t + 1) = (n / (t + 1))$。最后，界 (v) 由 (iii) 以及以下观察得出（详情留作练习 102）：

$$
\binom{d}{t} A_q(n, d, d) = \binom{d}{t} A_2(n, 2t + 1, 2t + 1) = \binom{d}{t} A_2(n, 2t + 2, 2t + 1) \le \binom{n}{t} \left\lfloor \frac{n-t}{t+1} \right\rfloor
$$

根据定理 2.3.3(iv) 和不受限约翰逊界。

## 练习 102 使用不受限约翰逊界证明 \(\binom{d}{t} A_2(n, 2t + 2, 2t + 1) \le \binom{n}{t} \left\lfloor \frac{n-t}{t+1} \right\rfloor.\)

## 例 2.3.9 使用 (2.12) 我们计算出 $A_2(16, 6)$ 的上界为 263。回顾 $A_2(16, 6) = A_2(15, 5)$。使用 (2.13)，我们发现 $A_2(15, 5)$，因此也就 $A_2(16, 6)$，

