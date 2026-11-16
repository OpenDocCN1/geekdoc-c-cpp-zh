

### 练习 755 证明示例 12.2.5 和 12.7.3 中的生成矩阵生成相同的 $\mathbb{Z}_4$-线性码。

我们现在使用相对迹来列出 $K(r+1)$ 和 $\widehat{K}(r+1)$ 中的所有代码字。令 $\mathbf{I}_n$ 表示长度为 $n$ 的全一向量。

### 引理 12.7.4 设 $r \ge 2$ 且 $n = 2^r - 1$。则 $\mathbf{c} \in K(r+1)$ 当且仅当存在 $\lambda \in \mathcal{R} = \text{GR}(4^r)$ 和 $\epsilon \in \mathbb{Z}_4$ 使得

$$\mathbf{c} = (\text{TR}(\lambda), \text{TR}(\lambda\xi), \text{TR}(\lambda\xi^2), \dots, \text{TR}(\lambda\xi^{n-1})) + \epsilon \mathbf{I}_n.$$ (12.23)

$\mathbf{c}$ 的奇偶校验为 $\epsilon$。

**证明：** 利用练习 755，$\sum_{i=0}^{n-1} (\text{TR}_r(\lambda \xi^i) + \epsilon) = \text{TR}_r(\lambda \sum_{i=0}^{n-1} \xi^i) + (2^r - 1)\epsilon = \text{TR}_r(\lambda \frac{\xi^n - 1}{\xi - 1}) + (2^r - 1)\epsilon \equiv (\text{TR}_r(0) + (2^r - 1)\epsilon \equiv (2^r - 1)\epsilon \equiv 3\epsilon \text{ (mod 4)}$。所以 $\mathbf{c}$ 的奇偶校验为 $\epsilon$。

令 $\mathcal{C} = \{(\text{TR}(\lambda), \text{TR}(\lambda\xi), \text{TR}(\lambda\xi^2), \dots, \text{TR}(\lambda\xi^{n-1})) + \epsilon \mathbf{I}_n \mid \lambda \in \text{GR}(4^r), \epsilon \in \mathbb{Z}_4\}$。我们首先证明 $\mathcal{C}$ 有 $4^{r+1}$ 个代码字；只要证明 $\text{TR}_r(\lambda \xi^i) + \epsilon = \text{TR}_r(\lambda_1 \xi^i) + \epsilon_1$ 对 $0 \le i \le n-1$ 蕴含 $\lambda = \lambda_1$ 和 $\epsilon = \epsilon_1$，这就很明显了。但由于 $\mathbf{c}$ 的奇偶校验为 $\epsilon$，所以 $\epsilon = \epsilon_1$。因此根据练习 753，$\text{TR}_r(\xi^i) = 0$ 对 $0 \le i \le n-1$ 成立，其中 $\lambda = \lambda - \lambda_1$。我们只需证明 $\xi = 0$。由于 $\text{TR}_r(\xi^i) = 0$，$\text{TR}_r(\xi^{2i}) = 0$ 对 $0 \le i \le n-1$ 成立，其中 $\lambda = \lambda - \lambda_1$。

我们现在证明 $\epsilon$ 可以采用 (12.23) 的形式，那么 $\mathbf{c} \in K(r+1)$。由于 $\mathbf{I}_n \in K(r+1)$，我们只需证明当 $\epsilon = 0$ 时 $\mathbf{c} \in K(r+1)$。若 $\lambda = 0$，结果显然。若 $\lambda \ne 0$，则根据上述论证 $c(x) \ne 0$。现在 $c^*(x)$ 是 $p(x) = \alpha \sum_{i=0}^{n-1} \text{TR}_r(\lambda \xi^{n-1-i}) x^i$ 的某个循环移位，其中 $\alpha \in \mathbb{Z}_4$ 被选定使得首项系数为 1 或 2（由于我们不知道 $c(x)$ 的次数，$c^*(x)$ 可能不等于未移位的 $p(x)$）。根据引理 12.7.2，若 $H(\mathbf{c})p(x) = 0$ 在 $\mathfrak{A}_n$ 中，则 $\mathbf{c} \in K(r+1)$。与引理 12.7.2 证明中的相同论证，乘积 $H(\mathbf{c})p(x)$ 中 $x^k$ 的系数（对 $0 \le k \le n-1$）为

$$\alpha \sum_{i+j \equiv k \text{ (mod } n)} H_i \text{TR}_r(\lambda \xi^{n-1-j}) = \alpha \text{TR}_r \left( \lambda \sum_{i=0}^{n-1} H_i \xi^{n-1-k+i} \right) = \alpha \text{TR}_r \left( \lambda \xi^{n-1-k} \sum_{i=0}^{n-1} H_i \xi^i \right),$$

利用练习 753，因为 $H_i \in \mathbb{Z}_4$。后一个迹为 $\text{TR}_r(\lambda \xi^{n-1-k} H(\xi)) = \text{TR}_r(0) = 0$，因此 $H(\mathbf{c})p(x) = 0$ 在 $\mathfrak{A}_n$ 中。所以 $\mathbf{c} \in K(r+1)$。由于 $K(r+1)$ 和 $\mathcal{C}$ 各有 $4^{r+1}$ 个代码字且 $\mathcal{C} \subseteq K(r+1)$，故 $\mathcal{C} = K(r+1)$。

### 练习 756 设 $\mathcal{R} = \text{GR}(4^r)$ 具有原始元素 $\xi$；令 $n = 2^r - 1$。利用 $\text{TR}_r : \mathcal{R} \to \mathbb{Z}_4$ 在加法下是满射群同态的事实（练习 753），证明以下内容：

- (a) 对每个 \( a \in \mathbb{Z}_4 \)，$\mathcal{R}$ 中恰有 \( 4^{r-1} \) 个元素的相对迹等于 \( a \)。
- (b) 对每个 \( s \in \{0, 2\xi, 2\xi^2, \dots, 2\xi^{k-1}\} = 2\mathcal{R} \)，\(\text{Tr}_r(s) \in \{0, 2\}\) 且至少有一个值等于 2。
- (c) 对 $a = 0$ 或 2，$2\mathcal{R}$ 中恰有 \( 2^{r-1} \) 个元素的相对迹等于 \( a \)。

在给出 \(\widehat{\mathcal{K}}(r+1)\) 的李权重分布之前，我们还需要一个计算结果。

### 引理 12.7.5 设 \(\mathcal{R} = \text{GR}(4^r)\) 具有原始元素 \(\xi\)。令 \(n = 2^r - 1\)。假设 \(\lambda \in \mathcal{R}\) 但 \(\lambda \notin 2\mathcal{R}\)。则 \(\mathcal{S} = \mathcal{S}_1 \cup \mathcal{S}_2\) 的所有元素互不相同，其中 \(\mathcal{S}_1 = \{(\xi^j - \xi^k) \mid 0 \le j \le n-1, 0 \le k \le n-1, j \neq k\}\) 且 \(\mathcal{S}_2 = \{\pm \lambda \xi^j \mid 0 \le j \le n-1\}\)，并且它们恰好是 \(\mathcal{R} \setminus 2\mathcal{R}\) 的元素。

**证明：** 根据练习 748，\(\mathcal{R}\) 中的可逆元集合为 \(\mathcal{R} \setminus 2\mathcal{R}\)。我们只需证明 \(\mathcal{S}\) 的元素可逆且互不相同，因为 \(\mathcal{R} \setminus 2\mathcal{R}\) 有 \(4^r - 2^r\) 个元素，且若 \(\mathcal{S}\) 的元素互不相同，则 \(\mathcal{S}\) 有 \((2^r - 1)(2^r - 2) + 2(2^r - 1) = 4^r - 2^r\) 个元素。

由于 \(\lambda\) 可逆，\(\mathcal{S}_2\) 的元素可逆。显然，\(\mathcal{S}_2\) 的元素互不相同，因为 \(-\xi^j = \xi^j + 2\xi^j\) 对任何 \(j\) 和 \(k\) 都不能等于 \(\xi^k\)。

要证明 \(\mathcal{S}_1\) 的元素可逆，只需证明当 \(j \neq k\) 时 \(\xi^j - \xi^k\) 可逆。若该元素不可逆，则 \(\xi^j - \xi^k \in 2\mathcal{R}\)。回顾在练习 749 之前讨论过的模 2 约化同态 \(\overline{\pi} : \mathcal{R} \to \mathbb{F}_{2^r} = \mathcal{R}/2\mathcal{R}\)，它将 \(\mathcal{R}\) 的原始元素 \(\xi\) 映射为 \(\mathbb{F}_{2^r}\) 的原始元素 \(\theta\)。因此 \(\overline{\pi}(\xi^j) + \overline{\pi}(\xi^k) = 0\)，蕴含 \(\theta^j = \theta^k\)。但对于 \(0\) 到 \(n-1\) 之间的 \(j \neq k\)，有 \(\theta^j \neq \theta^k\)。因此 \(\mathcal{S}_1\) 的元素可逆。我们现在证明 \(\mathcal{S}_1\) 的元素互不相同。假设 \(\xi^j - \xi^k = \xi^\ell - \xi^m\) 且 \(j \neq k\)、\(\ell \neq m$，则

$$1 + \xi^a = \xi^b + \xi^c, \tag{12.24}$$

其中 \(m - j \equiv a \pmod n\)、\(\ell - j \equiv b \pmod n\) 且 \(k - j \equiv c \pmod n\)。所以 \((1 + \xi^a)^2 = v_2(1 + \xi^a) = (\xi^b + \xi^c)^2 = v_2(\xi^b + \xi^c)\)，蕴含 \(1 + \xi^{2a} + 2\xi^a - v_2(1) - v_2(\xi^a) = \xi^{2b} + \xi^{2c} + 2\xi^{b+c} - v_2(\xi^b) - v_2(\xi^c)\)，其中 \(v_2\) 是 Frobenius 自同构。因此 \(2\xi^a = 2\xi^{b+c}\)，故 \(a = b + c \pmod n\)。因此若 \(x = \xi^a\)、\(y = \xi^b\)、\(z = \xi^c\)，则 \(x = yz\)。对 (12.24) 作用 \(\overline{\pi}\)，我们也有 \(1 + x = y + z\)。故 \(0 = 1 + yz + y + z = (1 + y)(1 + z)\) 在 \(\mathbb{F}_{2^r}\) 中成立，蕴含 \(y = 1\) 或 \(z = 1\)。所以 \(b \equiv 0 \pmod n\) 或 \(c \equiv 0 \pmod n\)。故 \(\ell = j\) 或 \(k = j\)；由于后者不可能，我们有 \(\ell = j\)，这也得出 \(k = m\)。所以 \(\mathcal{S}_1\) 的元素互不相同。

最后，我们证明 \(\mathcal{S}_1 \cup \mathcal{S}_2\) 的元素互不相同。假设 \(\xi^j - \xi^k = \pm \xi^m\)。通过移项并提取 \(\xi\) 的幂次，\(1 + \xi^a = \xi^b\)。所以 \((1 + \xi^a)^2 = v_2(1 + \xi^a) = \xi^{2b} - v_2(\xi^b)\)，得出 \(1 + 2\xi^a + \xi^{2a} - (1 + \xi^{2a}) = \xi^{2b} - \xi^{2b}\)。因此 \(2\xi^a = 0\)，这与事实矛盾。

我们现在有了工具来求 \(\widehat{\mathcal{K}}(r+1)\) 的李权重分布，这也是根据定理 12.2.2 二进制克尔多克码 \(\mathcal{K}(r+1) = \Phi(\widehat{\mathcal{K}}(r+1))\) 的汉明权重分布。

### 定理 12.7.6 设 \(r \ge 3\) 且 \(r\) 为奇数。令 \(A_i\) 为 \(\widehat{K}(r+1)\) 中李权为 \(i\) 的向量个数。则

\(\begin{aligned} A_i = \left\{ \begin{array}{ll} 1 & \text{若 } i = 0, \\ 2^{r+1}(2^r - 1) & \text{若 } i = 2^r - 2^{(r-1)/2}, \\ 2^{r+2} - 2 & \text{若 } i = 2^r, \\ 2^{r+1}(2^r - 1) + 2^{(r-1)/2} & \text{若 } i = 2^r + 2^{(r-1)/2}, \\ 1 & \text{若 } i = 2^{r+1}, \\ 0 & \text{否则.} \end{array} \right. 
\end{aligned}\)

这也是克尔多克码 \(\mathcal{K}(r+1)\) 的汉明权重分布。

**证明：** 令 \(\mathcal{R} = \text{GR}(4^r)\) 且

\(\mathbf{v}_\lambda = (\text{Tr}_r(\lambda \kappa), \text{Tr}_r(\lambda \kappa^2), \dots, \text{Tr}_r(\lambda \kappa^{n-1})),\)

其中 \(n = 2^r - 1\)。根据引理 12.7.4，\(\widehat{K}(r+1)\) 中的向量形式为 \((0, \mathbf{v}_\lambda) + \epsilon \mathbf{1}_{n+1}\)，其中 \(\lambda \in \mathcal{R}\) 且 \(\epsilon \in \mathbb{Z}_4\)。我们通过考察三种情况来计算这些向量各自的李权。前两种情况给出 \(i = 0, 2^r\) 和 \(2^{r+1}\) 时的 \(A_i\)。最后一种情况给出其余的 \(A_i\)。

### 情况 I：\(\lambda = 0\)

在此情况下，\(\mathbf{v}_\lambda\) 是零向量，且 \((0, \mathbf{v}_\lambda) + \epsilon \mathbf{1}_{n+1} = \epsilon \mathbf{1}_{n+1}\) 若 \(\epsilon = 0\) 则李权为 0，若 \(\epsilon = 1\) 或 3 则李权为 \(n+1 = 2^r\)，若 \(\epsilon = 2\) 则李权为 \(2(n+1) = 2^{r+1}\)。此情形贡献一个李权为 0 的向量、两个李权为 \(2^r\) 的向量和一个李权为 \(2^{r+1}\) 的向量。

### 情况 II：\(\lambda \in 2\mathcal{R}\) 且 \(\lambda \neq 0\)

因此 \(\lambda = 2\xi^i\) 对某些 \(0 \le i \le n-1\)。故 \(\mathbf{v}_\lambda\) 的分量集合始终为 \(\{ \text{Tr}_r(2\xi^j) \mid 0 \le j \le n-1 \}\)（以某种顺序），与 \(i\) 无关。但根据练习 756(c)，其中恰有 \(2^{r-1}\) 个值为 2，其余 \(2^{r-1} - 1\) 个值为 0。因此每个向量 \((0, \mathbf{v}_\lambda) + \epsilon \mathbf{1}_{n+1}\) 要么有 \(2^{r-1}\) 个 2 和 \(2^{r-1}\) 个 0（当 \(\epsilon = 0\) 或 2 时），要么有 \(2^{r-1}\) 个 1 和 \(2^{r-1}\) 个 3（当 \(\epsilon = 1\) 或 3 时）。在所有情况下，这些向量的李权均为 \(2^r\)。此情形贡献 \(4n = 2^{r+2} - 4\) 个李权为 \(2^r\) 的向量。

### 情况 III：\(\lambda \in \mathcal{R}\) 且 \(\lambda \notin 2\mathcal{R}\)

令 \(\mathcal{R}^* = \mathcal{R} \setminus 2\mathcal{R}\)。对于 \(j \in \mathbb{Z}_4\)，令 \(n_j = n_j(\mathbf{v}_\lambda)\) 为 \(\mathbf{v}_\lambda\) 等于 \(j\) 的分量个数。我们建立一组关于 \(n_j\) 的方程，然后求解这些方程。令 \(i = \sqrt{-1}\)。定义

\( S = \sum_{j=0}^{n-1} i^{\text{Tr}_r(\lambda \kappa^j)} = n_0 - n_2 + i(n_1 - n_3). \) (12.25)

