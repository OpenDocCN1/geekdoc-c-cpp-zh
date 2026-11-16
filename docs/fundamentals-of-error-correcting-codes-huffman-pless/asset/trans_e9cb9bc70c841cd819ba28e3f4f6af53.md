

证明：设 \( G \) 为 \( \mathcal{C} \) 的生成矩阵。根据引理 7.10.8 及其证明，存在一个秩为 \( r \) 的 \( r \times k \) 矩阵 \( A \)，使得 \( U = \{ \mathbf{y} \in \text{col}(G) \mid A\mathbf{y} = \mathbf{0} \} \)，其中 \( \text{span}(U) \in \mathcal{F}_{k, k-r} \) 且 \( d_r(C) = n - m(U) \)。此外，\( AG \) 生成 \( \mathcal{C} \) 的一个 \( r \) 维子码 \( \mathcal{D} \)。根据习题 431，\( \mathcal{D} \) 有 \( t = (q^r - 1)/(q - 1) \) 个 \( (r-1) \) 维子码 \( V_1, V_2, \dots, V_t \)。每个 \( V_i \) 对应一个秩为 \( r-1 \) 的 \( (r-1) \times k \) 矩阵 \( A_i \)，使得 \( A_i G \) 是 \( V_i \) 的生成矩阵。令 \( U_i = \{ \mathbf{y} \in \text{col}(G) \mid A_i \mathbf{y} = \mathbf{0} \} \)，我们看到 \( \text{span}(U_i) \in \mathcal{F}_{k, k-r+1} \)，如引理 7.10.8 的证明所示。此外 \( U \subset U_i \)，因为 \( AG \) 的某一列为 \( \mathbf{0} \) 意味着 \( A_i G \) 的同一列也是 \( \mathbf{0} \)，原因是 \( V_i \) 是 \( \mathcal{D} \) 的子码。反之，如果 \( U' \subset \text{col}(G) \) 且 \( U \subseteq U' \) 以及 \( \text{span}(U') \in \mathcal{F}_{k, k-r+1} \)，则存在一个秩为 \( r-1 \) 的 \( (r-1) \times k \) 矩阵 \( A' \)，使得 \( U' = \{ \mathbf{y} \in \text{col}(G) \mid A' \mathbf{y} = \mathbf{0} \} \)。由于 \( U \subseteq U' \)，\( \mathcal{D} = \text{span}(U) \subseteq \text{span}(U') \)。因此 \( A'G \) 生成 \( \mathcal{D} \) 的一个 \( (r-1) \) 维子空间，记为 \( V_i \)，故 \( U' = U_i \)。

\( d_{r-1}(C) \le n - m(U_i) \quad \text{对 } 1 \le i \le t \text{ 成立。} \)

因而

\( d_r(C) - d_{r-1}(C) \ge n - m(U) - [n - m(U_i)] = m(U_i \setminus U) \quad \text{对 } 1 \le i \le t \text{ 成立。} \)

\( G \) 中不在 \( U \) 中的每一列恰好属于某一个 \( U_i \)，因为根据上一段，\( U \) 加上这一列，再加上可能的其他列，张成 \( \mathcal{F}_{k, k-r+1} \) 的一个子空间。因此

\( t(d_r(C) - d_{r-1}(C)) \ge \sum_{i=1}^t m(U_i \setminus U) = n - m(U) = d_r(C). \)

引理得证。

## 习题 431

证明：在 \( \mathbb{F}_q \) 上的一个 \( r \) 维码中存在 \( t = (q^r - 1)/(q - 1) \) 个 \( (r-1) \) 维子码。

## 定理 7.10.10（广义格里斯默界）

设 \( \mathcal{C} \) 是 \( \mathbb{F}_q \) 上的一个 \( [n, k] \) 码。则对 \( 1 \le r \le k \)，

\( n \ge d_r(C) + \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^i(q^r-1)} d_r(C) \right\rceil. \)

**证明：** 若 \( r = k \)，不等式退化为显然的断言 \( n \ge d_k(C) \)；参见定理 7.10.1。现假设 \( r < k \)。不失一般性，根据定理 7.10.1(ii)，我们可以假设 \( \mathcal{C} \) 有一个如下形式的生成矩阵 \( G \)：

\( G = \begin{bmatrix} G_1 & O \\ G_2 & G_3 \end{bmatrix}. \)

其中 \( G_1 \) 是秩为 \( r \) 的 \( r \times d_r(C) \) 矩阵，\( G_3 \) 是一个 \( (k-r) \times (n-d_r(C)) \) 矩阵。矩阵 \( [G_2 \ G_3] \) 的秩为 \( k-r \)。若 \( G_3 \) 的秩小于 \( k-r \)，则由 \( [G_2 \ G_3] \) 生成的码中存在一个非零码字 \( \mathbf{x} \)，其在最后 \( n-d_r(C) \) 个坐标上为零，这与定理 7.10.1 中的 \( d_r(C) < d_{r+1}(C) \) 矛盾。因此 \( G_3 \) 的秩为 \( k-r \) 且生成一个 \( [n-d_r(C), k-r] \) 码 \( C_3 \)。

设 \( \mathbf{c} = c_1 \cdots c_n \in C \)，其中 \( w((c_{d_r(C)+1} \cdots c_n)) = a > 0 \)。由 \( \mathbf{c} \) 和 \( G \) 的前 \( r \) 行生成的 \( \mathcal{C} \) 的子码是一个支持大小为 \( a + d_r(C) \) 的 \( (r+1) \) 维子码。故 \( a \ge d_{r+1}(C) - d_r(C) \)，这意味着 \( C_3 \) 的最小重量至少为 \( d_{r+1}(C) - d_r(C) \)，通过选择上述 \( c \) 使得 \( wt((c_{d_r(C)+1} \cdots c_n)) \) 在 \( C_3 \) 中具有最小重量。对 \( C_3 \) 应用格里斯默界，

\( n - d_r(C) \ge \sum_{i=0}^{k-r-1} \left\lceil \frac{d_{r+1}(C) - d_r(C)}{q^i} \right\rceil = \sum_{i=1}^{k-r} \left\lceil \frac{d_{r+1}(C) - d_r(C)}{q^{i-1}} \right\rceil. \)

根据引理 7.10.9，\( (q^{k-1} - 1)d_r(C) \le (q^{k-1} - q)d_{r+1}(C) \)。利用此式，

\( d_{r+1}(C) - d_r(C) \ge \left( 1 - \frac{q^{k-1} - q}{q^{k-1} - 1} \right) d_{r+1}(C) = \frac{q-1}{q^{k-1} - 1} d_{r+1}(C). \)

因此，

\( n - d_r(C) \ge \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^{i-1}(q^{k-1} - 1)} d_{r+1}(C) \right\rceil. \)

但再次利用引理 7.10.9，

\( n - d_r(C) \ge \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^{i-1}(q^{k-1} - q)} d_r(C) \right\rceil = \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^i(q^r - 1)} d_r(C) \right\rceil. \) \(\square\)

格里斯默界是广义格里斯默界在 \( r = 1 \) 时的情形。我们现在证明，若一个码达到格里斯默界，则它对所有 \( r \) 也达到广义格里斯默界，且其重量层次是唯一确定的；该结果的二元情形见文献 [128]。为简化记号，令

\( b_r = d_r(C) + \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^i(q^r - 1)} d_r(C) \right\rceil \text{ 对 } 1 \le r \le k \text{ 成立。} \)

广义格里斯默界则断言 \( n \ge b_r \)，对 \( 1 \le r \le k \)。我们首先证明 \( b_{r+1} \ge b_r \)，并确定 \( b_{r+1} = b_r \) 成立的条件。

## 引理 7.10.11

设 \( 1 \le r < k \)。则 \( b_{r+1} \ge b_r \)。此外，\( b_{r+1} = b_r \) 当且仅当以下两点均成立：

- (i) \( d_{r+1}(C) = \lceil (q^{k-1} - 1)d_r(C) / (q^{k-1} - q) \rceil \)，且
- (ii) \( \lceil (q - 1)d_{r+1}(C) / (q^i(q^{r+1} - 1)) \rceil = \lceil (q - 1)d_r(C) / (q^{i+1}(q^r - 1)) \rceil \) 对 \( 1 \le i \le k - r - 1 \) 成立。

**证明：** 引理 7.10.9 蕴含

\( d_{r+1}(C) \ge \left\lceil \frac{q^{k-1} - 1}{q^{k-1} - q} d_r(C) \right\rceil \) (7.19)

以及

\( \left\lceil \frac{q-1}{q^i(q^{r+1} - 1)} d_{r+1}(C) \right\rceil \ge \left\lceil \frac{q-1}{q^i(q^{r+1} - q)} d_r(C) \right\rceil = \left\lceil \frac{q-1}{q^{i+1}(q^r - 1)} d_r(C) \right\rceil \) (7.20)

根据 (7.19) 和 (7.20)，

```
\begin{aligned}
b_{r+1} &= d_{r+1}(C) + \sum_{i=1}^{k-r-1} \left\lceil \frac{q-1}{q^i(q^{r+1}-1)} d_{r+1}(C) \right\rceil \\
&\ge \left\lceil \frac{q^{k-1}-1}{q^{k-1}-q} d_r(C) \right\rceil + \sum_{i=1}^{k-r-1} \left\lceil \frac{q-1}{q^i(q^{r+1}-q)} d_r(C) \right\rceil \\
&= \left\lceil d_r(C) + \frac{q-1}{q(q^r-1)} d_r(C) \right\rceil + \sum_{i=2}^{k-r} \left\lceil \frac{q-1}{q^i(q^r-1)} d_r(C) \right\rceil \\
&= d_r(C) + \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^i(q^r-1)} d_r(C) \right\rceil = b_r.
\end{aligned}
```

显然，\( b_{r+1} = b_r \) 当且仅当 (7.19) 以及当 \( 1 \le i \le k-r-1 \) 时的 (7.20) 中均取等号。

## 定理 7.10.12

设 \(\mathcal{C}\) 是 \( \mathbb{F}_q \) 上的一个达到格里斯默界的 \( [n, k, d] \) 码。则：

- (i) \(\mathcal{C}\) 对所有 \( 1 \le r \le k \) 的 \( r \) 达到广义格里斯默界，且
- (ii) \( d_r(\mathcal{C}) = \sum_{i=0}^{r-1} \lceil d/q^i \rceil \) 对 \( 1 \le r \le k \) 成立。

**证明：** 根据广义格里斯默界 \( n \ge b_k \)；利用引理 7.10.11，

\( n \ge b_k \ge b_{k-1} \ge \cdots \ge b_1 \)。

由于 \(\mathcal{C}\) 达到格里斯默界，\( b_1 = n \)。因此对 \( 1 \le r \le k \) 有 \( b_r = n \)，从而得到 (i)。

注意当 \( r=1 \) 时 (ii) 成立，因为 \( d_1(\mathcal{C}) = d \)。假设 \( 1 < r \le k \)。根据引理 7.10.11，

\( \left\lceil \frac{q-1}{q^r(q^r-1)} d_r(\mathcal{C}) \right\rceil = \left\lceil \frac{q-1}{q^{r+1}(q^{r-1}-1)} d_{r-1}(\mathcal{C}) \right\rceil, \)

对 \( 1 < s < k \) 和 \( 1 \le i \le k-s \) 成立。对 \( s = r, r-1, \dots, 2 \) 归纳应用此式，得

\( \left\lceil \frac{q-1}{q^r(q^r-1)} d_r(\mathcal{C}) \right\rceil = \left\lceil \frac{q-1}{q(q-1)} d_1(\mathcal{C}) \right\rceil = \left\lceil \frac{d}{q^{r+1}} \right\rceil, \)

对 \( 1 \le i \le k-r \) 成立，因为根据定理 7.10.1，\( d(\mathcal{C}) = d \)。由于 \(\mathcal{C}\) 达到格里斯默界，故 \( b_r = n \)，我们有

\( \sum_{i=1}^{k-r} \left\lceil \frac{d}{q^i} \right\rceil = n = d_r(\mathcal{C}) + \sum_{i=1}^{k-r} \left\lceil \frac{q-1}{q^i(q^r-1)} d_r(\mathcal{C}) \right\rceil = d_r(\mathcal{C}) + \sum_{i=1}^{k-r} \left\lceil \frac{d}{q^{i+r-1}} \right\rceil. \)

所以

\( d_r(\mathcal{C}) = \sum_{i=0}^{k-1} \left\lceil \frac{d}{q^i} \right\rceil - \sum_{i=r}^{k-1} \left\lceil \frac{d}{q^{i+r-1}} \right\rceil = \sum_{i=0}^{r-1} \left\lceil \frac{d}{q^i} \right\rceil, \)

从而 (ii) 成立。

