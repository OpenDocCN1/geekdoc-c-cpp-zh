

$\mathcal{M}$ 有一半的行在该列中有 1。所以 $\mathcal{M}$ 包含 $13 \cdot 4 = 52$ 个 1；但 $\mathcal{M}$ 有七行权重为 8，这意味着 $\mathcal{M}$ 有 56 个 1，产生矛盾。所以 $d_3 = 14$。

由于 Wei [348]，$\mathcal{C}$ 的权重层次与 $\mathcal{C}^\perp$ 的权重层次之间存在关系。首先我们证明一个引理。

### 引理 7.10.3
设 $\mathcal{C}$ 为 $\mathbb{F}_q$ 上的一个 $[n, k]$ 码。对于正整数 $s < n$，设 $r$ 为最大整数，使得 $\mathcal{C}$ 具有如下形式的生成矩阵 $G$：

$G = \begin{bmatrix} G_1 & O \\ G_2 & G_3 \end{bmatrix}$.

其中 $G_1$ 是秩为 $r$ 的 $r \times s$ 矩阵，$G_3$ 是 $(k-r) \times (n-s)$ 矩阵。那么 $\mathcal{C}$ 具有如下形式的校验矩阵：

$H = \begin{bmatrix} H_1 & H_2 \\ O & H_3 \end{bmatrix}$.

其中 $H_1$ 是秩为 $s-r$ 的 $(s-r) \times s$ 矩阵，$H_3$ 是秩为 $n-k-s+r$ 的 $(n-k-s+r) \times (n-s)$ 矩阵。此外，$n-k-s+r$ 是 $\mathcal{C}^\perp$ 的子空间中支持包含在最后 $n-s$ 个坐标中的最大维数。

证明：设 $H = [A \ B]$，其中 $A$ 是 $(n-k) \times s$ 矩阵，$B$ 是 $(n-k) \times (n-s)$ 矩阵。由于 $H$ 的行与 $G$ 的行正交，$A$ 的行与 $G_1$ 的行正交。因此 $A$ 的秩至多为 $s-r$。假设 $A$ 的秩小于 $s-r$。那么存在一个长度为 $s$ 的向量，它不在 $G_1$ 生成的码中，但与 $A$ 的行正交。将 $n-s$ 个 0 附加到该向量的末尾，我们得到一个与 $H$ 的行正交的向量，因此该向量在 $\mathcal{C}$ 中，但不在 $[G_1 \ O]$ 生成的码中，这与 $r$ 的极大性矛盾。因此 $A$ 的秩等于 $s-r$，从而 $\mathcal{C}$ 具有满足引理结论的校验矩阵 $H$。

### 定理 7.10.4
设 $\mathcal{C}$ 为 $\mathbb{F}_q$ 上的一个 $[n, k]$ 码。则

$\{d_r(\mathcal{C}) \mid 1 \le r \le k\} = \{1, 2, ..., n\} \setminus \{n+1-d_r(\mathcal{C}^\perp) \mid 1 \le r \le n-k\}.$

证明：令 $s = d_r(\mathcal{C}^\perp)$，其中 $1 \le r \le n-k$。只需证明不存在 $1 \le r \le k$ 使得 $d_r(\mathcal{C}) = n+1-s$。由于 $s = d_r(\mathcal{C}^\perp)$，存在一组 $s$ 个坐标，它们支持 $\mathcal{C}^\perp$ 的一个 $r$ 维子码。重新排列列，使这些成为前 $s$ 个坐标。因此 $\mathcal{C}^\perp$ 具有如下形式的 $(n-k) \times n$ 生成矩阵：

$H = \begin{bmatrix} H_1 & O \\ H_2 & H_3 \end{bmatrix}$.

其中 $H_1$ 是秩为 $r$ 的 $r \times s$ 矩阵。根据定理 7.10.1，$d_r(\mathcal{C}^\perp) < d_{r+1}(\mathcal{C}^\perp)$，因此没有更大的子码在这些 $s$ 个坐标上有支持。将引理 7.10.3 应用于 $\mathcal{C}^\perp$（代替 $\mathcal{C}$）和 $n-k$（代替 $k$），存在 $\mathcal{C}$ 的一个 $(k-s+r)$ 维子码，它在前 $s$ 个坐标位置上为零。因此

$d_{k-s+r}(\mathcal{C}) \le n-s$. (7.17)

反证假设存在 $t$ 使得 $d_t(\mathcal{C}) = n + 1 - s$。由 (7.17) 可得

$t > k - s + r. \quad (7.18)$

如有必要，将 $\mathcal{C}$ 替换为排列等价码，$\mathcal{C}$ 具有 $k \times n$ 生成矩阵

$G = \begin{bmatrix} G_1 & O \\ G_2 & G_3 \end{bmatrix}.$

其中 $G_1$ 是秩为 $t$ 的 $t \times (n + 1 - s)$ 矩阵。再次，由于 $d_t(\mathcal{C}) < d_{t+1}(\mathcal{C})$，引理 7.10.3 适用，其中 $t$ 代替 $r$，$n + 1 - s$ 代替 $s$。因此存在 $\mathcal{C}^\perp$ 的一个 $(s - 1 - k + t)$ 维子码，它在前 $n + 1 - s$ 个位置上为零。由于 $s = d_r(\mathcal{C}^\perp)$，我们有 $s - 1 - k + t < r$，这与 (7.18) 矛盾。

我们现在说明如何使用定理 7.10.4 来计算自双码的权重层次。

### 示例 7.10.5
设 $\mathcal{C}$ 为一个 $[24, 12, 8]$ 自双二进制码。（这必定是扩展二进制 Golay 码。）我们利用 $\mathcal{C}$ 的自双性和定理 7.10.4 计算 $\{d_r(C) \mid 1 \le r \le 12\}$。由于 $d_1(C) = 8$，根据定理 7.10.1，我们有 $1, 2, \dots, 7 \notin \{d_r(C) \mid 1 \le r \le 12\}$，因此 $24, 23, \dots, 18 \in \{d_r(C^\perp) \mid 1 \le r \le 12\}$ 且 $17 \notin \{d_r(C^\perp) \mid 1 \le r \le 12\}$。很容易看出，长度小于 12 的最小权重为 8 的 2 维自正交二进制码不存在。因此 $d_2(C) \ge 12$ 且 $9, 10, 11 \notin \{d_r(C) \mid 1 \le r \le 12\}$。于是 $16, 15, 14 \in \{d_r(C^\perp) \mid 1 \le r \le 12\}$。由于 $\mathcal{C} = C^\perp$，我们现在得出 $\{8, 14, 15, 16, 18, 19, 20, 21, 22, 23, 24\}$ 包含于 $\{d_r(C) \mid 1 \le r \le 12\}$ 且 $12 \le d_2(C) \le 13$。一个简单的论证表明，一个 $[13, 2, 8]$ 自正交二进制码的生成矩阵中必须有一列全为零。因此 $d_2(C) = 12$。所以我们有：

| r | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| $d_r(C)$ | 8 | 12 | 14 | 15 | 16 | 18 | 19 | 20 | 21 | 22 | 23 | 24 |

### 练习 427
做以下题目：
- (a) 证明长度小于 12 的最小权重为 8 的 2 维自正交二进制码不存在。
- (b) 证明一个 $[13, 2, 8]$ 自正交二进制码的生成矩阵中必须有一列全为零。

### 练习 428
求示例 7.5.6 中生成矩阵 $G_1$ 的 $[16, 8, 4]$ 自双双偶二进制码的权重层次。

### 练习 429
求示例 7.5.6 中生成矩阵 $G_2$ 的 $[16, 8, 4]$ 自双双偶二进制码的权重层次。

### 练习 430
$[7, 3, 4]$ 二进制单纯码和 $[7, 4, 3]$ 二进制海明码的权重层次分别是什么？

Wei [348] 观察到最小支持权重推广了 Singleton 界。

### 定理 7.10.6 (广义 Singleton 界)
对于 $\mathbb{F}_q$ 上的一个 $[n, k, d]$ 线性码，当 $1 \le r \le k$ 时，$d_r \le n - k + r$。

证明：该证明对 $k - r$ 进行归纳。当 $k - r = 0$ 时，根据定理 7.10.1，$d_r = d_k \le n = n - k + r$。假设对某个 $r \le k$ 有 $d_r \le n - k + r$，则根据同一定理，$d_{r-1} \le d_r - 1 \le n - k + (r - 1)$，从而得出结果。

Singleton Bound 是广义 Singleton 界中 $r = 1$ 的情况。从广义 Singleton 界的证明可知，如果一个码达到 Singleton Bound，则当 $1 \le r \le k$ 时 $d_{r-1} = d_r - 1$ 且 $d_k = n$。按定义，达到 Singleton Bound 的码是 MDS 码；因此 MDS 码也满足广义 Singleton 界，从而其广义 Hamming 权重被确定。

### 定理 7.10.7
设 $C$ 为 $\mathbb{F}_q$ 上的一个 MDS 码。则：(i) 对于所有 $1 \le r \le k$，$C$ 满足广义 Singleton 界；(ii) 当 $1 \le r \le k$ 时，$d_r = d + r - 1$。

我们现在研究最小支持权重满足的 Griesmer Bound [124, 128] 的一个推广。设 $G$ 为码 $C$ 的生成矩阵。设 col($G$) 为 $G$ 的不同列的集合。如果 $\mathbf{x} \in \text{col}(G)$，定义 $m(\mathbf{x})$ 为 $\mathbf{x}$ 在 $G$ 中的重数，如果 $U \subseteq \text{col}(G)$，定义

$m(U) = \sum_{\mathbf{x} \in U} m(\mathbf{x}).$

对于 $U \subseteq \text{col}(G)$，设 span($U$) 为由 $U$ 张成的 $\mathbb{F}_q^k$ 的子空间。最后，对于 $1 \le r \le k$，设 $\mathcal{F}_{r,r}$ 为由 $G$ 的列张成的 $\mathbb{F}_q^k$ 的所有 $r$ 维子空间的集合。在陈述广义 Griesmer Bound 之前，我们需要两个引理。第一个引理给出了用函数 $m(U)$ 表示的 $d_r(C)$ 的公式。

### 引理 7.10.8
设 $C$ 为具有生成矩阵 $G$ 的 $[n, k]$ 码。对于 $1 \le r \le k$，$d_r(C) = n - \max\{m(U) \mid U \subseteq \text{col}(G) \text{ 且 } \text{span}(U) \in \mathcal{F}_{k-k+r}\}$。

证明：设 $\mathcal{D}$ 为 $C$ 的一个 $[n, r]$ 子码。那么存在一个秩为 $r$ 的 $r \times k$ 矩阵 $A$，使得 $AG$ 是 $\mathcal{D}$ 的生成矩阵。而且，对于每个这样的矩阵 $A$，$AG$ 都是 $C$ 的一个 $[n, r]$ 子码的生成矩阵。按定义，$|\text{supp}(\mathcal{D})| = n - m$，其中 $m$ 是 $AG$ 的零列数。因此 $|\text{supp}(\mathcal{D})| = n - m(U)$，其中 $U = \{\mathbf{y} \in \text{col}(G) \mid A\mathbf{y} = \mathbf{0}\}$。

由于 $A$ 的秩为 $r$ 且 $G$ 的秩为 $k$，span($U$) 在 $\mathcal{F}_{k-k+r}$ 中。反之，如果 $U \subseteq \text{col}(G)$ 且 span($U$) 在 $\mathcal{F}_{k-k+r}$ 中，则存在一个秩为 $r$ 的 $r \times k$ 矩阵 $A$，使得 $A\mathbf{y} = \mathbf{0}$ 当且仅当 $\mathbf{y} \in \text{span}(U)$。但 $AG$ 是 $C$ 的一个 $[n, r]$ 子码 $\mathcal{D}$ 的生成矩阵。因此，由于 $d_r(C)$ 是任何这样的 $\mathcal{D}$ 的最小支持大小，结果得证。

利用这个引理及其证明，我们可以关联 $d_r(C)$ 和 $d_{r-1}(C)$。

### 引理 7.10.9
设 $C$ 为 $\mathbb{F}_q$ 上的一个 $[n, k]$ 码。则对于 $1 < r \le k$，$(q^r - 1)d_{r-1}(C) \le (q^r - q)d_r(C)$。

