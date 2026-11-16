

其条目恰好一半等于 0，一半等于 1，这意味着

$$\sum_{u \in v+C} wt(u) = \frac{nM}{2}$$

或者等价地，

$$\sum_{i=0}^n i A_i(v) = \frac{nM}{2}.$$ (11.2)

其中 $\{A_i(v) \mid 0 \le i \le n\}$ 是 $\mathbf{v} + \mathcal{C}$ 的重量分布。方程 (11.2) 意味着 $\mathbf{v}$ 与 $\mathcal{C}$ 的码字之间的平均距离是 $n/2$。因此，$\mathbf{v}$ 与某个码字 $c \in \mathcal{C}$ 之间的距离至多为 $n/2$。根据定理 11.1.2(i)，我们得到部分 (i)。

现在假设 $\mathcal{C}$，因此也 $\mathbf{v} + \mathcal{C}$，具有强度 2。在 $M_t$ 中对应于向量 $\mathbf{u} \in \mathbf{v} + \mathcal{C}$ 的每一行中，都有 $\binom{n}{2}$ 个有序比特对。$M_t$ 中每个包含 $\binom{n}{2}$ 对不同列的块都恰好 $M/4$ 次包含二进制二元组 $(1, 1)$。因此

$$\sum_{u \in v+C} \binom{wt(u)}{2} = \sum_{u \in v+C} \frac{wt(u)(wt(u)-1)}{2} = \binom{n}{2} \frac{M}{4} = \frac{n}{2} \frac{n-1}{2} \frac{M}{4}.$$

使用 (11.2) 我们得到

$$\sum_{i=0}^n i^2 A_i(v) = \frac{n(n+1)M}{4}.$$ (11.3)

结合 (11.2) 和 (11.3) 得到

$$\sum_{i=0}^n (2i-n)^2 A_i(v) = nM.$$ (11.4)

这意味着存在一个使得 $A_i(v) \neq 0$ 的 $i$，满足 $(2i-n)^2 \ge n$。对不等式两边开平方表明，要么 $i \le \frac{n-\sqrt{n}}{2}$，要么 $i \ge \frac{n+\sqrt{n}}{2}$。

现在假设 $\mathcal{C}$ 是自补码。根据练习 629，$\mathbf{v} + \mathcal{C}$ 也是自补码。那么存在一个满足上述两个不等式中第一个且 $A_i(v) \neq 0$ 的 $i$。因此存在一个向量 $\mathbf{u} \in \mathbf{v} + \mathcal{C}$，使得 $wt(u) \le (n-\sqrt{n})/2$。故 (ii) 成立。

在二进制线性码的情况下，Norre 界可以重述如下。

### 推论 11.2.2 设 $\mathcal{C}$ 为长度为 $n$ 的二进制线性码。

- (i) 如果 $C^\perp$ 的最小距离至少为 2，则 $\rho(C) \le \lfloor n/2 \rfloor$。
- (ii) 如果 $C^\perp$ 的最小距离至少为 4 且全一向量 $\mathbf{1}$ 在 $C$ 中，则 $\rho(C) \le \lfloor (n-\sqrt{n})/2 \rfloor$。

### 练习 630 证明推论 11.2.2。

### 练习 631 设 $\mathcal{C}$ 为强度为 2 且 $\rho(C) = (n-\sqrt{n})/2$ 的自补二进制码，并设 $\mathbf{v} + \mathcal{C}$ 具有最小重量 $\rho(C)$。证明 $\mathbf{v} + \mathcal{C}$ 中一半向量的重量为 $(n - \sqrt{n})/2$，另一半向量的重量为 $(n + \sqrt{n})/2$。提示：检查 (11.4)。

我们现在准备考察在 1.10 节中首次定义的 Reed–Muller 码 $\mathcal{R}(r, m)$ 的覆盖半径。令 $\rho_{RM}(r, m)$ 表示 $\mathcal{R}(r, m)$ 的覆盖半径。根据练习 617，$\rho_{RM}(0, m) = 2^{m-1}$，因为 $\mathcal{R}(0, m)$ 是二进制重复码。同样，$\rho_{RM}(m, m) = 0$，因为 $\mathcal{R}(m, m) = \mathbb{F}_2^n$。我们考虑 $1 \le r < m$ 的情况。根据定理 1.10.1，$\mathcal{R}(r, m)^\perp = \mathcal{R}(m - r - 1, m)$ 具有最小重量 $2^{r+1} \ge 4$，因此根据练习 628，$\mathcal{R}(r, m)$ 具有强度 2。此外，根据定理 1.10.1，$\mathbf{1} \in \mathcal{R}(0, m) \subset \mathcal{R}(r, m)$，因此 $\mathcal{R}(r, m)$ 是自补码。因此，根据 Norre 界 (ii)，我们有以下定理。

### 定理 11.2.3 设 $1 \le r < m$。则 $\rho_{RM}(r, m) \le 2^{m-1} - 2^{m-r/2-1}$。特别是，$\rho_{RM}(1, m) \le 2^{m-1} - 2^{m/2-1/2}$。

请注意，根据练习 618 和 Reed–Muller 码的嵌套性质，对 $\rho_{RM}(1, m)$ 的任何上界自动也是 $1 < r$ 时 $\rho_{RM}(r, m)$ 的上界。

我们现在要找一阶 Reed–Muller 码覆盖半径的递推关系，结合定理 11.2.3，这将使我们在 $m$ 为偶数时能够得到 $\rho_{RM}(1, m)$ 的精确值。

### 引理 11.2.4 对于 $m \ge 2$，

\(\rho_{RM}(1, m) \ge 2\rho_{RM}(1, m - 2) + 2^{m-2}\)。

**证明：** 对于向量 $\mathbf{x} \in \mathbb{F}_2^n$，令 $\bar{\mathbf{x}} = \mathbf{1} + \mathbf{x}$ 表示 $\mathbf{x}$ 的补码。根据练习 632，$\mathcal{R}(1, m)$ 中的每个码字都有以下形式之一：

- (a) \((\mathbf{x}|\mathbf{x}|\mathbf{x}|\mathbf{x})\),
- (b) \((\mathbf{x}|\bar{\mathbf{x}}|\mathbf{x}|\bar{\mathbf{x}})\),
- (c) \((\mathbf{x}|\bar{\mathbf{x}}|\bar{\mathbf{x}}|\mathbf{x})\), or
- (d) \((\mathbf{x}|\mathbf{x}|\bar{\mathbf{x}}|\bar{\mathbf{x}})$，

其中 $\mathbf{x} \in \mathcal{R}(1, m - 2)$。选择向量 $\mathbf{v} \in \mathbb{F}_2^{2^{m-2}}$，使得陪集 $\mathbf{v} + \mathcal{R}(1, m - 2)$ 的重量等于 $\rho_{RM}(1, m - 2)$。因此，

\(\text{d}(\mathbf{v}, \mathbf{x}) \ge \rho_{RM}(1, m - 2)\) (11.5)

对所有 $\mathbf{x} \in \mathcal{R}(1, m - 2)$ 成立。请注意，

\(\text{d}(\mathbf{v}, \bar{\mathbf{x}}) = \text{d}(\bar{\mathbf{v}}, \mathbf{x}) = 2^{m-2} - \text{d}(\mathbf{v}, \mathbf{x}) = 2^{m-2} - \text{d}(\bar{\mathbf{v}}, \bar{\mathbf{x}})\) (11.6)

如果我们在 $\mathbb{F}_2^{2^{m-2}}$ 中找到一个向量 $\mathbf{y}$，使其与所有码字 $\mathbf{c} \in \mathcal{R}(1, m)$ 的距离至少为 $2\rho_{RM}(1, m - 2) + 2^{m-2}$，则该引理得证。令 $\mathbf{y} = (\mathbf{v}|\mathbf{v}|\bar{\mathbf{v}}|\bar{\mathbf{v}})$。我们来检查上面 $\mathbf{c}$ 的每种可能性 (a) 到 (d)。对于相应的情况，使用 (11.5)、(11.6) 以及若 $\mathbf{x} \in \mathcal{R}(1, m - 2)$ 则 $\bar{\mathbf{x}} \in \mathcal{R}(1, m - 2)$ 这一事实，我们有：

- (a) \(\text{d}(\mathbf{y}, \mathbf{c}) = 3\text{d}(\mathbf{v}, \mathbf{x}) + \text{d}(\bar{\mathbf{v}}, \mathbf{x}) = 2^{m-2} + 2\text{d}(\mathbf{v}, \mathbf{x}) \ge 2^{m-2} + 2\rho_{RM}(1, m - 2)\),
- (b) \(\text{d}(\mathbf{y}, \mathbf{c}) = \text{d}(\mathbf{v}, \mathbf{x}) + 2\text{d}(\bar{\mathbf{v}}, \mathbf{x}) + \text{d}(\bar{\mathbf{v}}, \bar{\mathbf{x}}) = \text{d}(\mathbf{v}, \mathbf{x}) + 3\text{d}(\bar{\mathbf{v}}, \bar{\mathbf{x}}) = 2^{m-2} + 2\text{d}(\bar{\mathbf{v}}, \bar{\mathbf{x}}) \ge 2^{m-2} + 2\rho_{RM}(1, m - 2)\),
- (c) \(\text{d}(\mathbf{y}, \mathbf{c}) = 2\rho_{RM}(1, m - 2) + 2^{m-2}$, and
- (d) \(\text{d}(\mathbf{y}, \mathbf{c}) = 2\text{d}(\mathbf{v}, \mathbf{x}) + 2^{m-2} \ge 2\rho_{RM}(1,m-2) + 2^{m-2}$。

结果随之得出。

### 练习 632 证明 $\mathcal{R}(1, m)$ 中的每个码字都有以下形式之一：

- (a) \((\mathbf{x}|\mathbf{x}|\mathbf{x}|\mathbf{x})\),
- (b) \((\mathbf{x}|\bar{\mathbf{x}}|\mathbf{x}|\bar{\mathbf{x}})\),
- (c) \((\mathbf{x}|\bar{\mathbf{x}}|\bar{\mathbf{x}}|\mathbf{x})\), or
- (d) \((\mathbf{x}|\mathbf{x}|\bar{\mathbf{x}}|\bar{\mathbf{x}})$，

其中 $\mathbf{x} \in \mathcal{R}(1, m-2)$。提示：参见 1.10 节。

### 练习 633 完成以下任务：

- (a) 证明 $\rho_{RM}(1, 1) = 0$。
- (b) 证明如果 $m$ 为奇数，则 $\rho_{RM}(1, m) \ge 2^{m-1} - 2^{(m-1)/2}$。提示：使用 (a) 和引理 11.2.4。
- (c) 证明 $\rho_{RM}(1, 2) = 1$。
- (d) 证明如果 $m$ 为偶数，则 $\rho_{RM}(1, m) \ge 2^{m-1} - 2^{(m-2)/2}$。提示：使用 (c) 和引理 11.2.4。

结合定理 11.2.3 和练习 633(d)，当 $m$ 为偶数时，得到了 $\rho_{RM}(1, m)$ 的精确值。

### 定理 11.2.5 对于偶数 $m$，$\rho_{RM}(1, m) = 2^{m-1} - 2^{(m-2)/2}$。

当 $m$ 为奇数时，练习 633(b) 中的不等式对 $m$ 的前四个值取等号。根据练习 633(a)，$\rho_{RM}(1, 1) = 0$。由于 $\mathcal{R}(1, 3)$ 是 $[8, 4, 4]$ 扩展海明码，根据定理 11.1.7，$\rho_{RM}(1, 3) = 2$。证明 $\rho_{RM}(1, 5) = 12$ 并不困难；一个理论证明是作为引理 9.4 在 [34] 中的一个结果给出的，或者计算覆盖半径的计算机软件包也可以验证这一点。Mykkeltveit [242] 表明 $\rho_{RM}(1, 7) = 56$。从这四个案例中，人们会推测 $m$ 为奇数时练习 633(b) 中的下界取等号。然而，这是错误的；当 $m = 15$ 时，$\mathcal{R}(1, 15)$ 的覆盖半径至少为 $16276 = 2^{14} - 2^7 + 20$ [250, 251]。

对于 $1 < r$，存在对 $\rho_{RM}(r, m)$ 的界，但给出 $\rho_{RM}(r, m)$ 精确值的结果相对较少。其中一个结果见 [237]。

### 定理 11.2.6

\[
\rho_{RM}(m-3, m) = \begin{cases} m+2 & \text{当 } m \text{ 为偶数时} \\ m+1 & \text{当 } m \text{ 为奇数时} \end{cases}
\]

表 11.1（见 [34]）给出了 $1 \le r \le m \le 9$ 时 $\rho_{RM}(r, m)$ 的精确值和界。条目的参考文献可见 [34]。

### 练习 634 计算机代数软件包对此问题将很有用。证明球覆盖界给出了表 11.1 中 $\rho_{RM}(r, m)$ 的下界，适用于：

- (a) $(r, m) = (3, 8)$ 以及
- (b) 当 $2 \le r \le 5$ 时 $(r, m) = (r, 9)$。

