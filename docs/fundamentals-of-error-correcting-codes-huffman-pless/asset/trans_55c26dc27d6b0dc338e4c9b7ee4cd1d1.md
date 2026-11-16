

和射影几何；参见 [4, 5]。这些代码可以定义为几种不同的方式。这里我们选择基于 (u | u + v) 构造的递归定义。

令 m 为正整数，r 为非负整数且 r < m。我们构造的二进制代码长度为 2^m。对于每种长度，将有 m + 1 个线性代数，记作 R(r, m)，称为长度为 2^m 的 r 阶 Reed-Muller 码，或 RM 码。代码 R(0, m) 和 R(m, m) 是平凡代码：0 阶 RM 码 R(0, m) 是长度为 2^m 的二进制重复码，基为 {1}，而 m 阶 RM 码 R(m, m) 是整个空间 F_2^{2^m}。对于 1 <= r < m，定义

\(\mathcal{R}(r, m) = \{(\mathbf{u}, \mathbf{u} + \mathbf{v}) \mid \mathbf{u} \in \mathcal{R}(r, m-1), \mathbf{v} \in \mathcal{R}(r-1, m-1)\}.\) (1.7)

令 G(0, m) = [11...1] 且 G(m, m) = I_{2^m}。根据上述描述，这些分别是 R(0, m) 和 R(m, m) 的生成矩阵。对于 1 <= r < m，使用 (1.5)，R(r, m) 的一个生成矩阵 G(r, m) 为

\(G(r, m) = \begin{bmatrix} G(r, m-1) & G(r, m-1) \\ O & G(r-1, m-1) \end{bmatrix}.\)

我们通过生成 1 <= r < m <= 3 的 R(r, m) 的生成矩阵来说明这一构造：

\(G(1, 2) = \begin{bmatrix} 1 & 0 & 1 & 0 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 \end{bmatrix}, \quad G(1, 3) = \begin{bmatrix} 1 & 0 & 1 & 0 & 1 & 0 & 1 & 0 \\ 0 & 1 & 0 & 1 & 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 & 0 & 0 & 1 & 1 \\ 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 \end{bmatrix}, \quad \text{and}\)

\(G(2, 3) = \begin{bmatrix} 1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 & 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 0 & 1 & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 & 0 & 1 & 0 & 1 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 \end{bmatrix}.\)

从这些矩阵中，注意 R(1, 2) 和 R(2, 3) 分别是 \(\mathbb{F}_2^4\) 和 \(\mathbb{F}_2^8\) 中所有偶权重向量的集合。还要注意 R(1, 3) 是一个 [8, 4, 4] 自偶码，根据练习 56，它必须是 \(\widehat{\mathcal{H}}_3\)。

二进制 Reed-Muller 码的维数、最小权重和对偶码可以直接从其定义中计算得出。

**定理 1.10.1** 令 r 为满足 0 <= r <= m 的整数。则以下结论成立：
(i) 如果 \(0 \le i \le j \le m\)，则 \(\mathcal{R}(i, m) \subseteq \mathcal{R}(j, m)\)。
(ii) \(\mathcal{R}(r, m)\) 的维数等于 \(\binom{m}{0} + \binom{m}{1} + \dots + \binom{m}{r}\)。
(iii) \(\mathcal{R}(r, m)\) 的最小权重等于 \(2^{m-r}\)。
(iv) \(\mathcal{R}(m, m)^\perp = \{\mathbf{0}\}\)，并且如果 \(0 \le r < m\)，则 \(\mathcal{R}(r, m)^\perp = \mathcal{R}(m - r - 1, m)\)。

证明：部分 (i) 当 $m=1$ 时通过直接计算显然成立，当 $j=m$ 时也成立，因为 $\mathcal{R}(m, m)$ 是整个空间 $\mathbb{F}_2^{2^m}$。假设通过归纳法，对于所有 $0 \le k \le \ell < m$，都有 $\mathcal{R}(k, m-1) \subseteq \mathcal{R}(\ell, m-1)$。令 $k < m$。则：

$$\mathcal{R}(i, m) = \{ (\mathbf{u}, \mathbf{u} + \mathbf{v}) \mid \mathbf{u} \in \mathcal{R}(i, m-1), \mathbf{v} \in \mathcal{R}(i-1, m-1) \} \subseteq \{ (\mathbf{u}, \mathbf{u} + \mathbf{v}) \mid \mathbf{u} \in \mathcal{R}(j, m-1), \mathbf{v} \in \mathcal{R}(j-1, m-1) \} = \mathcal{R}(j, m).$$

因此，如果 $0 < i$，(i) 通过归纳法得证。如果 $i = 0$，我们只需证明长度为 $2^m$ 的全一向量对于 $j < m$ 属于 $\mathcal{R}(j, m)$。归纳假设长度为 $2^{m-1}$ 的全一向量属于 $\mathcal{R}(j, m-1)$。然后根据定义 (1.7)，长度为 $2^m$ 的全一向量属于 $\mathcal{R}(j, m)$，因为 $\mathbf{u}$ 的一个选择是 $\mathbf{1}$，$\mathbf{v}$ 的一个选择是 $\mathbf{0}$。对于 (ii)，当 $r = m$ 时结果成立，因为 $\mathcal{R}(m, m) = \mathbb{F}_2^{2^m}$ 且

$$\binom{m}{0} + \binom{m}{1} + \dots + \binom{m}{m} = 2^m.$$

对于 $m = 1$，通过观察也可知结果成立。现在假设 $\mathcal{R}(i, m-1)$ 的维数为 $$\binom{m-1}{0} + \binom{m-1}{1} + \dots + \binom{m-1}{i} \quad \text{for all } 0 \le i < m.$$

根据第 1.5.5 节的讨论（以及练习 33），$\mathcal{R}(r, m)$ 的维数等于 $\mathcal{R}(r, m-1)$ 和 $\mathcal{R}(r-1, m-1)$ 维数之和，即，$$\binom{m-1}{0} + \binom{m-1}{1} + \dots + \binom{m-1}{r} + \binom{m-1}{0} + \binom{m-1}{1} + \dots + \binom{m-1}{r-1}.$$

该结果由二项式系数的基本性质得出：$$\binom{m-1}{0} = \binom{m}{0} \quad \text{and} \quad \binom{m-1}{i} + \binom{m-1}{i-1} = \binom{m}{i}.$$

部分 (iii) 对于 $m = 1$ 通过观察同样成立，对 $r = 0$ 和 $r = m$ 也成立，因为 $\mathcal{R}(0, m)$ 是长度为 $2^m$ 的二进制重复码，且 $\mathcal{R}(m, m) = \mathbb{F}_2^{2^m}$。假设 $\mathcal{R}(i, m-1)$ 的最小权重为 $2^{m-1-i}$，对所有 $0 \le i < m$ 成立。如果 $0 < r < m$，则根据定义 (1.7) 和第 1.5.5 节的讨论（以及练习 33），$\mathcal{R}(r, m)$ 的最小权重为 $\min(2 \cdot 2^{m-1-r}, 2^{m-1-(r-1)}) = 2^{m-r}$。要证明 (iv)，我们首先注意到 $\mathcal{R}(m, m)^\perp$ 是 $\{\mathbf{0}\}$，因为 $\mathcal{R}(m, m) = \mathbb{F}_2^{2^m}$。因此，如果我们定义 $\mathcal{R}(-1, m) = \{\mathbf{0}\}$，则对于所有 $m > 0$，都有 $\mathcal{R}(-1, m)^\perp = \mathcal{R}(m - (-1), m)$。通过直接计算，对于所有满足 $-1 \le r \le m - 1$ 的 $r$，都有 $\mathcal{R}(r, m)^\perp = \mathcal{R}(m - r - 1, m)$。假设通过归纳法，如果 $-1 \le i \le m - 1$，则 $\mathcal{R}(i, m-1)^\perp = \mathcal{R}((m-1) - i - 1, m-1)$。令 $0 \le r < m$。要证明 $\mathcal{R}(r, m)^\perp = \mathcal{R}(m - r - 1, m)$，只需证明 $\mathcal{R}(m - r - 1, m) \subseteq \mathcal{R}(r, m)^\perp$，因为根据 (ii)，$\dim \mathcal{R}(r, m) + \dim \mathcal{R}(m - r - 1, m) = 2^m$。注意，有了 $\mathcal{R}(-1, m)$ 的定义，(1.7) 扩展到 $r = 0$ 的情况。令 $\mathbf{x} = (\mathbf{a}, \mathbf{a} + \mathbf{b}) \in \mathcal{R}(r - 1, m)$，其中 $\mathbf{a} \in \mathcal{R}(r - 1, m - 1)$ 且 $\mathbf{b} \in \mathcal{R}(r - m - 2, m - 1)$，并令 $\mathbf{y} = (\mathbf{u}, \mathbf{u} + \mathbf{v}) \in \mathcal{R}(r, m)$，其中 $\mathbf{u} \in \mathcal{R}(r, m - 1)$ 且 $\mathbf{v} \in \mathcal{R}(r - 1, m - 1)$。则 $\mathbf{x} \cdot \mathbf{y} = 2\mathbf{a} \cdot \mathbf{u} + \mathbf{a} \cdot \mathbf{v} + \mathbf{b} \cdot \mathbf{u} + \mathbf{b} \cdot \mathbf{v} = \mathbf{a} \cdot \mathbf{v} + \mathbf{b} \cdot \mathbf{u} + \mathbf{b} \cdot \mathbf{v}$。每一项均为 0，如下所示。由于 $\mathbf{x} \in \mathcal{R}(r - 1, m - 1)$，$\mathbf{b} \cdot \mathbf{u} = \mathcal{R}(r - 1, m - 1)^\perp \cdot \mathbf{a} \cdot \mathbf{v} = 0$。由于 $\mathbf{b} \in \mathcal{R}(m - r - 2, m - 1) = \mathcal{R}(r, m - 1)^\perp$，$\mathbf{b} \cdot \mathbf{u} = 0$ 且 $\mathbf{b} \cdot \mathbf{v} = 0$，使用 (i) 中的 $\mathcal{R}(r - 1, m - 1) \subseteq \mathcal{R}(r, m - 1)$。我们得出结论 $\mathcal{R}(m - r - 1, m) \subseteq \mathcal{R}(r, m)^\perp$，从而完成 (iv) 的证明。

基于此定理，我们做一些观察。首先，由于 R(0, m) 是长度为 2^m 的重复码，R(m - 1, m) = R(0, m)^⊥ 是 F_2^{2^m} 中所有偶权重向量的代码。我们之前已经观察到这一点关于 R(1, 2) 和 R(2, 3)。其次，如果 m 为奇数且 r = (m - 1)/2，则从部分 (iii) 和 (iv) 可以看出 R((m-1)/2, m) 是自偶码，最小权重为 2^{(m-1)/2}。我们同样之前关于 R(1, 3) 观察到这一点。在练习中，你还将验证一般结果：对 R(1, m) 进行删短，然后取偶权重向量的子码，将产生长度为 2^m - 1 的单纯码 S_m。

### 练习 62

在本练习中，我们为 R(1, m) 生成另一个生成矩阵 G'(1, m)。定义

\(G'(1, 1) = \begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}.\)

对于 m >= 2，递归定义

\(G'(1, m) = \begin{bmatrix} G'(1, m-1) & G'(1, m-1) \\ 00 \cdots 0 & 11 \cdots 1 \end{bmatrix}.\)

并定义 G''(1, m) 为从 G'(1, m) 中移除底行并将其放置为矩阵的第二行，将下方的行向下移动后得到的矩阵。

- (a) 证明 G'(1, 1) 是 R(1, 1) 的生成矩阵。
- (b) 求出矩阵 G'(1, 2)、G''(1, 2)、G'(1, 3) 和 G''(1, 3)。
- (c) 你注意到从 G''(1, 2) 和 G''(1, 3) 中删除第一行和第一列后得到的矩阵的列有什么特点？
- (d) 使用归纳法、部分 (a) 和定义 (1.7) 证明 G'(1, m) 是 R(1, m) 的生成矩阵。
- (e) 制定部分 (c) 的一个推广，适用于从 G''(1, m) 中删除第一行和第一列后得到的矩阵。证明你的推广是正确的。
- (f) 证明由从 G''(1, m) 中删除第一行和第一列后得到的矩阵生成的代码是单纯码 S_m。
- (g) 证明代码 R(m - 2, m) 是扩展二进制海明码 \hat{\mathcal{H}}_m。

注意，本题表明扩展二进制海明码及其对偶码都是 Reed-Muller 码。

## 1.11 编码、解码与香农定理

自编码理论诞生以来，代码已以多种多样的方式被使用；除了在通信信道和计算机中提供可靠性之外，它们还在光盘录音中提供高保真度，并且还使来自外太空的图像传输变得成功。新的用途不断出现。由于代码的主要应用是存储或传输数据，我们介绍对消息进行编码和解码的过程。

