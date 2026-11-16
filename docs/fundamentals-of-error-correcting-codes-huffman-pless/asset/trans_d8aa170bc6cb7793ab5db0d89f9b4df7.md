

### 练习 685
找出所有长度 \(n \le 4\) 的自双码的标准型生成矩阵，以单式等价为准。给出每个码的类型。

如果 C 的标准型生成矩阵为 (12.1)，则 \(C^\perp\) 的生成矩阵为

\(\displaystyle G^\perp = \begin{bmatrix} -(B_1 + 2B_2)^T - C^T A^T & C^T \\ 2A^T & I_{k_1-k_2} \\ O & O \end{bmatrix}.\) (12.2)

其中 \(O\) 是 \(k_2 \times (n - k_1 - k_2)\) 的零矩阵。特别是，\(C^\perp\) 的类型为

\(4^{n-k_1-k_2}2^{k_2}.\) (12.3)

### 练习 686
给出示例 12.1.1 中码 \(\mathcal{C}\) 的 \(C^\perp\) 的生成矩阵 (12.2)。

### 练习 687
证明 \(G^\perp G^T\) 是零矩阵，其中 \(G\) 如 (12.1) 所给，\(G^\perp\) 如 (12.2) 所给。

与 \(\mathbb{F}_2\) 上的码不同，\(\mathbb{Z}_4^n\) 中向量的权重概念可能有多种含义。事实上，在处理 \(\mathbb{Z}_4\) 上的码时，使用了三种不同的权重，因此也有三种不同的距离。设 \(\mathbf{x} \in \mathbb{Z}_4^n\)。假设 \(n_i(\mathbf{x})\) 表示 \(\mathbf{x}\) 中等于 \(i\) 的分量数，对所有 \(i \in \mathbb{Z}_4\) 成立。\(\mathbf{x}\) 的 **汉明权重** 为 \(w_H(\mathbf{x}) = n_1(\mathbf{x}) + n_2(\mathbf{x}) + n_3(\mathbf{x})\)，\(\mathbf{x}\) 的 **李权重** 为 \(w_L(\mathbf{x}) = n_1(\mathbf{x}) + 2n_2(\mathbf{x}) + n_3(\mathbf{x})\)，\(\mathbf{x}\) 的 **欧几里得权重** 为 \(w_E(\mathbf{x}) = n_1(\mathbf{x}) + 4n_2(\mathbf{x}) + n_3(\mathbf{x})\)。因此，等于 1 或 3 的分量对每种权重贡献 1，而 2 对李权重贡献 2，对欧几里得权重贡献 4。\(\mathbf{x}\) 和 \(\mathbf{y}\) 之间的 **汉明、李和欧几里得距离** 分别为 \(d_H(\mathbf{x}, \mathbf{y}) = w_H(\mathbf{x} - \mathbf{y})\)、\(d_L(\mathbf{x}, \mathbf{y}) = w_L(\mathbf{x} - \mathbf{y})\) 和 \(d_E(\mathbf{x}, \mathbf{y}) = w_E(\mathbf{x} - \mathbf{y})\)。

### 练习 688
做以下题目：
- (a) 向量 \(120\,203\,303\) 的汉明、李和欧几里得权重分别是多少？
- (b) 向量 \(30\,012\,221\) 和 \(20\,202\,213\) 之间的汉明、李和欧几里得距离分别是多少？

### 练习 689
求示例 12.1.1 中码 \(\mathcal{C}\) 的汉明、李和欧几里得权重分布。

### 练习 690
设 \(\mathcal{C}\) 为一个包含仅由 1 和 3 组成的代码字的 \(\mathbb{Z}_4\)-线性码。证明 \(C^\perp\) 中所有代码字的李权重均为偶数。

以下定理是定理 1.4.5(iv) 的 \(\mathbb{Z}_4\) 类比。

### 定理 12.1.5
设 \(\mathcal{C}\) 为一个自正交 \(\mathbb{Z}_4\)-线性码，且 \(\mathbf{c} \in C\)。则：
- (i) \(w_L(\mathbf{c}) \equiv 0 \pmod 2\)，
- (ii) \(w_E(\mathbf{c}) \equiv 0 \pmod 4\)。

### 练习 691
证明定理 12.1.5。

对于长度为 \(n\) 的 \(\mathbb{Z}_4\)-线性码 \(\mathcal{C}\)，也存在类似于 MacWilliams 方程的类比。

设

\(\displaystyle \text{Ham}_C(x, y) = \sum_{\mathbf{c} \in C} x^{w_H(\mathbf{c})} y^{n - w_H(\mathbf{c})}\)

为 C 的汉明权重枚举子。设

$$Lee_C(x, y) = \sum_{c \in C} x^{wt_L(c)} y^{2n - wt_L(c)}$$

为 C 的李权重枚举子；注意 y 指数中存在 2n，这是因为可能存在李权重高达 2n 的代码字。第 7.2 节中的 (M_3) 的类比为 [59, 116, 173, 174]:

$$Ham_{C^\perp}(x, y) = \frac{1}{|C|} Ham_C(y - x, y + 3x), \text{ 且 }$$

$$Lee_{C^\perp}(x, y) = \frac{1}{|C|} Lee_C(y - x, y + x).$$

### 练习 692
给出示例 12.1.1 中自双码 C 的汉明和李权重枚举子。然后对该码验证 (12.5) 和 (12.6)。

与 \(\mathbb{Z}_4\)-线性码相关的还有另外两个感兴趣的权重枚举子。与之前定义的 \(n_t(v)\) 一样，设

$$cwec(a, b, c, d) = \sum_{v \in C} a^{n(v)} b^{f_0(v)} c^{e_2(v)} d^{f_1(v)}$$

表示 C 的完整权重枚举子，并设

$$swec(a, b, c) = \sum_{v \in C} a^{n(v)} b^{f_0(v) + n_2(v)} c^{f_1(v)}$$

表示 C 的对称化权重枚举子。注意，等价码具有相同的对称化权重枚举子（因此这个更有用），而等价码可能不具有相同的完整权重枚举子。相应的 MacWilliams 方程为：

$$cwec_{C^\perp}(a, b, c, d) = \frac{1}{|C|} cwec(a + b + c + d, a + ib - c - id, a - b + c - d, a - ib - c + id), \text{ 且 }$$

$$swec_{C^\perp}(a, b, c) = \frac{1}{|C|} swec(a + 2b + c, a - c, a - 2b + c),$$

其中 \(i = \sqrt{-1}\)。

### 练习 693
给出示例 12.1.1 中自双码 C 的完整和对称化权重枚举子。然后对该码验证 (12.8) 和 (12.9)。

### 练习 694
做以下题目：
- (a) 证明 \(swec(a, b, c) = cwec(a, b, c, b)\)。
- (b) 在假设 (12.8) 有效的情况下，验证 (12.9)。
- (c) 证明 \(Ham_C(x, y) = swec(x, y, x)\)。
- (d) 在假设 (12.9) 有效的情况下，验证 (12.5)。

## 12.2 从 \(\mathbb{Z}_4\)-线性码得到的二进制码

从 \(\mathbb{Z}_4\)-线性码得到二进制码的载体是 Gray 映射 \(\mathfrak{G} : \mathbb{Z}_4 \to \mathbb{F}_2^2\)，定义为

\(\mathfrak{G}(0) = 00, \mathfrak{G}(1) = 01, \mathfrak{G}(2) = 11, \text{且 } \mathfrak{G}(3) = 10.\)

然后将此映射分量扩展为从 \(\mathbb{Z}_4^n\) 到 \(\mathbb{F}_2^{2n}\) 的映射，也记为 \(\mathfrak{G}\)。如果 \(\mathcal{C}\) 是一个 \(\mathbb{Z}_4\)-线性码，则其 Gray 图像将是二进制码 \(\mathfrak{G}(\mathcal{C})\)。注意 \(\mathcal{C}\) 和 \(\mathfrak{G}(\mathcal{C})\) 具有相同的大小。然而，一般来说，\(\mathfrak{G}(\mathcal{C})\) 将是非线性的。

### 练习 699
找出 \(\mathbb{Z}_4\) 中所有元素对 \(a\) 和 \(b\)，使得 \(\mathfrak{G}(a + b) \neq \mathfrak{G}(a) + \mathfrak{G}(b)\)。

### 练习 696
设 \(\mathcal{C}\) 为示例 12.1.1 中的 \(\mathbb{Z}_4\)-线性码。
- (a) 列出 \(\mathfrak{G}(\mathcal{C})\) 的 16 个代码字。
- (b) 证明 \(\mathfrak{G}(\mathcal{C})\) 是线性的。
- (c) 得到的二进制码是什么？

### 练习 697
设 \(\mathcal{C}\) 为长度为 3 的 \(\mathbb{Z}_4\)-线性码，其生成矩阵为
\(G = \begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & 3 \end{bmatrix}.\)
- (a) 列出 \(\mathcal{C}\) 中的 16 个代码字。
- (b) 列出 \(\mathfrak{G}(\mathcal{C})\) 中的 16 个代码字。
- (c) 证明 \(\mathfrak{G}(\mathcal{C})\) 是非线性的。

在做练习 696 和 697 时，你会注意到 \(\mathbf{v} \in \mathbb{Z}_4^n\) 的李权重是其 Gray 图像 \(\mathfrak{G}(\mathbf{v})\) 的普通汉明权重。这导致了 \(\mathbb{Z}_4\)-线性码的 Gray 图像的一个重要性质。一个码 \(\mathcal{C}\)（在 \(\mathbb{Z}_4\) 或 \(\mathbb{F}_q\) 上）被称为距离不变，如果对所有 \(\mathbf{c} \in \mathcal{C}\)，\(\mathbf{c} + \mathcal{C}\) 的汉明权重分布都相同。注意，所有线性码（在 \(\mathbb{Z}_4\) 或 \(\mathbb{F}_q\) 上）都必须是距离不变的，仅仅因为对所有 \(\mathbf{c} \in \mathcal{C}\) 都有 \(\mathbf{c} + \mathcal{C} = \mathcal{C}\)。

### 示例 12.2.1
在处理非线性二进制码时，码的距离分布比权重分布更重要，因为前者提供了关于码的纠错能力的信息。回顾第 2 章，长度为 \(n\) 的码 \(\mathcal{C}\) 的汉明距离分布是集合 \(\{B_i(\mathcal{C}) | 0 \le i \le n\}\)，其中

\(B_i(\mathcal{C}) = \frac{1}{|\mathcal{C}|} \sum_{\mathbf{c} \in \mathcal{C}} |\{\mathbf{v} \in \mathcal{C} | d(\mathbf{v}, \mathbf{c}) = i\}|\)

并且 \(d(\mathbf{v}, \mathbf{c})\) 是 \(\mathbf{c}\) 和 \(\mathbf{v}\) 之间的汉明距离；对于 \(\mathbb{Z}_4\) 上的码，使用相同的定义，用 \(d_H\) 代替 d。因此 \(\{B_i(\mathcal{C}) | 0 \le i \le n\}\) 是所有 \(\mathbf{c} \in \mathcal{C}\) 的 \(\mathbf{c} + \mathcal{C}\) 的权重分布的平均值。如果码是距离不变的，则距离分布与任何集合 \(\mathbf{c} + \mathcal{C}\) 的权重分布相同；如果此外码包含零代码字，则距离分布与 \(\mathcal{C}\) 的权重分布相同。因此，距离不变性是码的一个强大性质。例如，设 \(\mathcal{C}\) 为二进制

