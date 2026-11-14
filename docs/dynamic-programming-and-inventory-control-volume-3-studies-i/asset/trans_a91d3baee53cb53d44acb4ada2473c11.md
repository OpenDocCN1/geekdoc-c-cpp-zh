

定义对于 $n \ge 0$ 的整数

$$\xi(n) = \exp -\lambda L \left[ \frac{h}{\lambda} \sum_{j=0}^{n+1} \frac{(\lambda L)^j}{j!} - \frac{p}{\lambda} \sum_{j=n+2}^{n+1+s} \frac{(\lambda L)^j}{j!} \right].$$

我们有

$$\xi(n+1) - \xi(n) = \frac{(\lambda L)^{n+2}}{(n+2)!} \frac{\exp -\lambda L}{\lambda} \left[ h + p - p \frac{(\lambda L)^{-s}}{(n+3)\cdots(n+2-s)} \right].$$

定义 $n_0 = n_0(s)$ 为使得

$$(n+3)\cdots(n+2-s) \ge \frac{p(L\lambda)^{-s}}{h+p}$$

成立的第一个正整数。

### 引理 14.5.
对于 $s \le 0$，存在且仅存在一个值 $S$ 是局部最小值。即满足

$$\psi'_s(S+0) \ge 0, \psi'_s(S-1+0) < 0.$$

最小值 $S$ 是满足此条件的唯一值

**证明。** $n_0$ 是 $\xi(n)$ 的最小值。我们首先检查

(14.9.6) $$\xi(0) \ge 0 \Rightarrow \xi(n) \ge 0, \forall n.$$

因此

$$\psi'_s(n+0) \text{ 是递增的.}$$

如果 $\psi'_s(0+) \ge 0$，则 $\psi'_s(n+0) \ge 0, \forall n$。因此 $S=0$。如果 $\psi'_s(0+) < 0$，注意到对于足够大的 $n$，$\psi'_s(n+0) > 0$，存在且仅存在一个满足局部最小值性质的 $S$。

让我们证明性质 (14.9.6)。注意

$$\xi(0) \ge 0 \Rightarrow h(1+\lambda L) \ge p \sum_{j=2}^{1+s} \frac{(\lambda L)^j}{j!}.$$

因此

$$\xi(n) \ge \frac{p \exp -\lambda L}{\lambda(1+\lambda L)} \left[ \sum_{j=2}^{1+s} \frac{(\lambda L)^j}{j!} \sum_{j=0}^{n+1} \frac{(\lambda L)^j}{j!} - \sum_{j=n+2}^{n+1+s} \frac{(\lambda L)^j}{j!} (1+\lambda L) \right].$$

令

$$b_j = \frac{(\lambda L)^j}{j!}, \nu = 1+s \ge 1.$$

$\xi(n)$ 的正性将是以下不等式的结果

$$\sum_{j=0}^\nu b_j \sum_{k=0}^{n+1} b_k - \sum_{j=0}^{n+\nu} b_j \sum_{k=0}^{n+1} b_k$$

要证明该不等式，只需证明

$$\frac{\sum_{j=0}^{n+\nu} b_j}{\sum_{k=0}^{n+1} b_k}$$

关于 $n$ 是递减的。

比较 $n$ 和 $n+1$ 中的项，这等同于证明

$$b_{n+1+\nu} \sum_{k=0}^{n+1} b_k \le b_{n+2} \sum_{j=0}^{n+\nu} b_j,$$

并且只需证明

$$b_{n+1+\nu} \sum_{k=0}^{n+1} b_k \le b_{n+2} \sum_{j=\nu-1}^{n+\nu} b_j = b_{n+2} \sum_{k=0}^{n+1} b_{\nu-1+k}$$

因此只需检查

$$\frac{b_k}{b_{n+2}} \le \frac{b_{\nu-1+k}}{b_{n+1+\nu}} \forall k \le n+1.$$

这归结为检查性质

$$(k+1)\cdots(n+2) \le (k+\nu)\cdots(n+1+\nu), \forall k \le n+1,$$

该性质成立。

仍需考虑 $\xi(0) < 0$ 的情况，此时 $\xi(n_0) < 0$。

由于对于足够大的 $n$，$\xi(n) > 0$，存在 $S_1 > n_0$ 使得

$$\xi(S_1) \ge 0, \xi(S_1 - 1) < 0.$$

则

$$\xi(n) \ge 0 \forall n \ge S_1; \xi(n) < 0 \forall 0 \le n < S_1.$$

因此 $S_1$ 是唯一确定的。

故

$$\psi'_s(n+1+0) - \psi'_s(n+0) \ge 0, \forall n \ge S_1,$$

$$\psi'_s(n+1+0) - \psi'_s(n+0) < 0, \forall 0 \le n < S_1.$$

因此 $S_1$ 是 $\psi'_s(n+0)$ 的最小值。如果该最小值为正，我们可以得出 $S=0$。否则，很容易检查出存在唯一的局部最小值 $S > S_1$。证明完毕。

我们现在考虑 $s > 0$ 的情况，此时自然 $S(s) \ge s > 0$。我们首先计算导数

$$\psi'_s(x+0) = R_s([x]) = -pL + \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} \frac{(\lambda L)^j}{j!} ([x] - s - j + 1)$$

$$+ \frac{h+p}{\lambda} \exp -\lambda L \sum_{k=0}^{[x]-1} \frac{(\lambda L)^k}{k!} ([x] - s + 1)$$

$$+ \sum_{k=s}^{[x]} \frac{(\lambda L)^k}{k!} ([x] - k + 1) - \sum_{k=0}^{[x]-s} \frac{(\lambda L)^k}{k!} ([x] - k + 1 - s)$$

$$+ \exp -\lambda L \sum_{j=[x]+1-s}^{[x]} \sum_{m=0}^{[x]-j} \sum_{k=j+1}^{\infty} \left[ \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].$$

函数 \(R_s(n), n \ge s\) 关于 \(n\) 是递增的。我们确实可以检查

\(R_s(n+1) - R_s(n) = \frac{h}{\lambda} \exp -\lambda L \sum_{j=0}^{n+1-s} \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=n+2-s}^{n+1} \frac{(\lambda L)^j}{j!} - \exp -\lambda L \sum_{m=0}^{s-1} \sum_{j=n+2-s}^{n+2-m} \frac{(\lambda L)^j}{j!} \frac{(\lambda L)^m}{m!} \right],\)

和

\(R_s(n+1) - R_s(n) \ge 0, \forall n \ge s\)

我们接下来考虑 \(R_s(s), s \ge 0\)。我们首先检查

\(R_s(s) = -pL + \frac{h}{\lambda} \exp -\lambda L + \frac{h+p}{\lambda} \exp -\lambda L \left[ - \sum_{j=s+1}^{\infty} \frac{(\lambda L)^j}{j!} + \exp -\lambda L \sum_{j=0}^{s} \sum_{m=0}^{s-j} \sum_{k=1}^{\infty} \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \right].\)

很容易检查 \(R_s(s)\) 是一个递增函数。我们可以继续以唯一方式定义 \(S(s)\)。我们需要 \(\hat{s}\) 为使得 \(R_s(s) \ge 0\) 的第一个正整数。该数是唯一确定的。

### 引理 14.6.
对于 \(s > \hat{s}\) 我们有 \(S(s) = s\)，而对于 \(0 \le s \le \hat{s}\)，$S(s)$ 是使得 \(R_s(s) \ge 0\) 的第一个整数。

**证明。** 证明直接来自 \(R_s(x)\) 的单调性性质。

## 提前期情况下的小定律.
我们考虑正提前期 \(L\) 的小定律。假设在起始时刻初始库存为 \(x\)。依次定义

\(\theta = \inf\{t|x - D(t) \le 0\}; \quad \tau = \inf\{t|x - D(t) \le s\}.\)

注意

\(D(\tau) - D(\theta) = -s, \text{ 如果 } \tau \neq \theta, \tau \neq 0.\)

在时刻 \(\tau\)，如果 \(\tau > 0$ 下订单大小为 \(S - s$，如果 \(\tau = 0$ 下订单大小为 \(S - x\)。它在时刻 \(\tau + L$ 交付。因此交付后库存为 \(S - D(\tau + L) + D(\tau)\)。注意我们假设 \(s$ 为整数（正或负）。

缺货的可能性仅在 \(\theta < \tau + L$ 时存在。否则没有缺货和等待时间。如果 \(S - D(\tau + L) + D(\tau) > 0$，则缺货在时刻 \(\tau + L$ 被吸收。如果不是正数，人口 \(D(\tau + L) - D(\tau) - S$ 必须等到下一次交付。定义

\(\tau_1 = \inf\{t \ge \tau + L|S - D(t) + D(\tau) \le s\} - \tau - L,\)

则该部分人口将在时刻 \(\tau + L + \tau_1 + L$ 被服务。注意

\(S - D(\tau + L) + D(\tau) < s \Rightarrow \tau_1 = 0.\)

而且

\(S - D(\tau + L) + D(\tau) > s \Rightarrow S - D(\tau + L + \tau_1) + D(\tau) = s.\)

### 练习 14.12.
验证公式

\(\lambda E \tau_1 = E(S - s - D(\tau + L) + D(\tau))^+.\)

一个周期是区间 \(\min(\theta, \tau), \tau + L$。我们考虑在周期内到达的需求，它们在被服务前构成的缺货以及相应的等待时间。如果 \(\theta > \tau + L$，则没有缺货和等待时间。在时刻 \(\tau + L$ 被服务的人口为

- \(-s + \min(S, D(\tau + L) - D(\tau))$ 如果 \(\tau > 0\)，
- \(-x + \min(S, D(L))$ 如果 \(\tau = 0\)。

如果在 \(\tau + L$ 时库存为负，则周期内的所有需求无法在时刻 \(\tau + L$ 时得到满足。剩余部分将在时刻 \(\tau + L + \tau_1$ 被服务。其水平为 \((S - D(\tau + L) + D(\tau))^-\)。因此平均缺货可以表示为

$$B = \int_0^1 (D(\theta) + \rho(\tau + L - \theta)^+ - D(\theta))\,d\rho + (S - D(\tau + L) + D(\tau))^- \frac{L}{\tau + L - \theta} + (S - D(\tau + L) + D(\tau))^- \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}}$$

则预期缺货为

$$EB = \frac{\lambda}{2} E(\tau + L - \theta)^+ + L E \frac{(S - D(\tau + L) + D(\tau))^-}{\tau + L - \theta} + E \left[ \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}} \frac{(S - D(\tau + L) + D(\tau))^-}{\tau + L - \theta} \right].$$

我们现在可以考虑等待时间。首先我们注意到，整个人口在周期内平均等待时间为 \(\frac{1}{2}(\tau + L - \theta)^+$。此外，结转部分需要额外等待时间 \(L + \tau_1$，其中 \(\tau_1$ 可以为 0。按人口比例加权，我们得到预期平均等待时间

$$EWT = \frac{1}{2} E(\tau + L - \theta)^+ + L E \frac{(S - D(\tau + L) + D(\tau))^-}{D(\tau + L) - D(\theta)} + E \left[ \tau_1 1_{\{S - s - D(\tau + L) + D(\tau) > 0\}} \frac{(S - D(\tau + L) + D(\tau))^-}{D(\tau + L) - D(\theta)} \right]$$

小定律：

$$EB = \lambda EWT,$$

不成立。如果忽略结转的概率，它近似成立。即我们假设

$$\text{Prob } \{D(\tau + L) - D(\tau) > S\} \sim 0,$$

这意味着

$$\sum_{j=S+1}^\infty \frac{(\lambda L)^j}{j!} \sim 0.$$

另一种近似是将总人口 \(D(\tau + L) - D(\theta)$ 在 \((S - D(\tau + L) + D(\tau))^-\) 的系数中替换为 \(\lambda(\tau + L - \theta)$。这两个随机变量具有相同的期望值。使用这些近似，小定律仍然有效。这些近似要求提前期不能太大。

