

\(\widehat{\mathcal{H}}_{3,2}\) 的矩阵为

\[
\widehat{G} = \left[ \begin{array}{ccccc} 1 & 0 & 1 & 1 & 0 \\ 0 & 1 & 1 & -1 & -1 \end{array} \right]
\]
和
\[
\widehat{H} = \left[ \begin{array}{ccccc} 1 & 1 & 1 & 1 & 1 \\ -1 & -1 & 1 & 0 & 0 \\ -1 & 1 & 0 & 1 & 0 \end{array} \right] .
\]

如果先对一个码进行扩展，然后对新坐标进行删短，则得到原始码。但是，如果以相反顺序执行这些操作，通常会得到一个不同的码。

### 示例 1.5.5
如果对具有生成矩阵
\[
G = \left[ \begin{array}{ccccc} 1 & 1 & 0 & 0 & 1 \\ 0 & 0 & 1 & 1 & 0 \end{array} \right]
\]
的二进制码 \(\mathcal{C}\) 在其最后一个坐标上进行删短，然后（在右侧）扩展，则所得码的生成矩阵为
\[
G = \left[ \begin{array}{ccccc} 1 & 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 \end{array} \right] .
\]

在此示例中，我们的最后一步是扩展一个仅包含偶权重向量的二进制码。扩展坐标始终为 0。一般来说，当你扩展一个仅具有类偶码字的码时，情况正好如此。

### 练习 27
做以下各题。

- (a) 设 \(\mathcal{C} = \mathcal{H}_{3,2}\) 为示例 1.3.3 中定义的 \(\mathbb{F}_3\) 上的 \([4, 2, 3]\) 四元码，其生成矩阵为
\[
G = \left[ \begin{array}{cccc} 1 & 0 & 1 & 1 \\ 0 & 1 & 1 & -1 \end{array} \right] .
\]
给出通过从 \(\mathcal{C}\) 在最右侧坐标上进行删短然后在右侧扩展所得码的生成矩阵。同时确定所得码的最小权重。

- (b) 设 \(\mathcal{C}\) 为 \(\mathbb{F}_q\) 上的一个码。设 \(\mathcal{C}_r\) 为通过从 \(\mathcal{C}\) 在最右侧坐标上进行删短，然后对该删短码在右侧扩展所得的码。证明 \(\mathcal{C} = \mathcal{C}_r\) 当且仅当 \(\mathcal{C}\) 是一个类偶码。

- (c) 与 (b) 中定义的 \(\mathcal{C}_1\) 相同，证明如果 \(\mathcal{C}\) 是自正交的且包含全一码字 \(\mathbf{1}\)，则 \(\mathcal{C} = \mathcal{C}_1\)。

- (d) 与 (b) 中定义的 \(\mathcal{C}_1\) 相同，证明 \(\mathcal{C} = \mathcal{C}_1\) 当且仅当全一向量 \(\mathbf{1}\) 属于 \(\mathcal{C}^{\perp}\)。

## 1.5.3 缩短码

设 \(\mathcal{C}\) 为 \(\mathbb{F}_q\) 上的一个 \([n, k, d]\) 码，设 \(T\) 为任意 \(t\) 个坐标的集合。考虑在 \(T\) 上为 \(\mathbf{0}\) 的码字集合 \(\mathcal{C}(T)\)；该集合是 \(\mathcal{C}\) 的一个子码。在 \(T\) 上对 \(\mathcal{C}(T)\) 进行删短，得到一个长度为 \(n - t\) 的 \(\mathbb{F}_q\) 上的码，称为在 \(T\) 上 _缩短_ 的码，并记作 \(\mathcal{C}_T\)。

### 示例 1.5.6
设 $C$ 为具有生成矩阵的 \([6, 3, 2]\) 二进制码
\[
G = \begin{bmatrix} 1 & 0 & 0 & 1 & 1 & 1 \\ 0 & 1 & 0 & 1 & 1 & 1 \\ 0 & 0 & 1 & 1 & 1 & 1 \end{bmatrix}
\]
$C^\perp$ 也是一个具有生成矩阵的 \([6, 3, 2]\) 码
\[
G^\perp = \begin{bmatrix} 1 & 1 & 1 & 1 & 0 & 0 \\ 1 & 1 & 1 & 0 & 1 & 0 \\ 1 & 1 & 0 & 0 & 0 & 1 \end{bmatrix}
\]

如果坐标标记为 $1, 2, \dots, 6$，令 $T = \{5, 6\}$。缩短码 $C_T$ 和删短码 $C^T$ 的生成矩阵为
\[
G_T = \begin{bmatrix} 1 & 0 & 1 & 0 \\ 0 & 1 & 1 & 0 \\ 0 & 1 & 1 & 0 \end{bmatrix} \text{ 和 } G^T = \begin{bmatrix} 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 \end{bmatrix}
\]

对偶码进行缩短和删短得到码 $(C^\perp)_T$ 和 $(C^\perp)^T$，它们的生成矩阵为
\[
(G^\perp)_T = [1 \ 1 \ 1 \ 1] \text{ 和 } (G^\perp)^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 0 \end{bmatrix}
\]

从生成矩阵 $G_T$ 和 $G^T$ 可知，$C_T$ 和 $C^T$ 的偶码具有生成矩阵
\[
(G_T)^\perp = \begin{bmatrix} 1 & 1 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \text{ 和 } (G^T)^\perp = [1 \ 1 \ 1 \ 1]
\]

注意，这些矩阵表明 $(C^\perp)_T = (C^T)^\perp$ 且 $(C^\perp)^T = (C_T)^\perp$。

前一示例中观察到的结论普遍成立。

### 定理 1.5.7
设 $C$ 为 \(\mathbb{F}_q\) 上的一个 \([n, k, d]\) 码，设 \(T\) 为 \(t\) 个坐标的集合。则：
(i) $(C^\perp)_T = (C^T)^\perp$ 且 $(C^\perp)^T = (C_T)^\perp$；
(ii) 如果 $t < d$，则 $C_T$ 和 $(C^\perp)^T$ 的维数分别为 $k$ 和 $n - t - k$；
(iii) 如果 $t = d$ 且 \(T\) 是某个最小权重码字非零的坐标集合，则 \(C^T\) 和 \((C^\perp)_T\) 的维数分别为 \(k - 1\) 和 \(n - d - k + 1\)。

**证明.** 设 \(c\) 是在 \(T\) 上为 \(\mathbf{0}\) 的 \(C^\perp\) 的一个码字，\(c^*\) 为删除 \(T\) 中坐标后的码字。因此 \(c^* \in (C^\perp)_T\)。如果 \(\mathbf{x} \in C\)，则 \(\mathbf{0} = \mathbf{x} \cdot \mathbf{c} = \mathbf{x}^* \cdot \mathbf{c}^*\)，其中 \(\mathbf{x}^*\) 是在 \(T\) 上对 \(\mathbf{x}\) 进行删短后的码字。因此 \((C^\perp)_T \subseteq (C^T)^\perp\)。任何向量 \(\mathbf{c} \in (C^T)^\perp\) 都可以通过在 \(T\) 的位置插入 0 扩展为一个向量 \(\tilde{\mathbf{c}}\)。如果 \(\mathbf{x} \in C\)，在 \(T\) 上对 \(\mathbf{x}\) 进行删短以得到 \(\mathbf{x}^*\)。由于 \(\mathbf{0} = \mathbf{x}^* \cdot \mathbf{c} = \mathbf{x} \cdot \tilde{\mathbf{c}}\)，则 \(\tilde{\mathbf{c}} \in (C^\perp)_T\)。因此 \((C^T)^\perp = (C^\perp)_T\)。将 \(C\) 替换为 \(C^\perp\) 得到 \((C^\perp)^T = (C_T)^\perp\)，从而完成 (i) 的证明。

假设 \(t < d\)。则 \(n - d + 1 \le n - t\)，这意味着根据定理 1.4.15，\(C\) 的任何 \(n - t\) 个坐标都包含一个信息集。因此 \(C^T\) 必须是 \(k\) 维的，进而根据 (i)，\((C^\perp)_T = (C^T)^\perp\) 的维数为 \(n - t - k\)；这证明了 (ii)。

与 (ii) 类似，若要完成 (iii)，只需证明 \(C^T\) 的维数为 \(k-1\)。如果 \(S \subset T\) 且 \(|S| = d-1\)，则根据部分 (ii)，\(C^S\) 的维数为 \(k\)。显然 \(C^S\) 的最小距离为 1，而 \(C^T\) 是通过在 \(C^S\) 中一个权重为 1 的码字的非零坐标上对 \(C^S\) 进行删短得到的。根据定理 1.5 (ii)，\(C^T\) 的维数为 \(k-1\)。

### 练习 28
设 \(\mathcal{C}\) 为示例 1.2.2 中描述的长度为 \(n\) 的二进制重复码。对任意 \(T\)，描述 \((\mathcal{C}^\perp)_T\) 和 \((\mathcal{C}_T)^\perp\)。

### 练习 29
设 \(\mathcal{C}\) 为示例 1.4.4 中长度为 6 的码。当 \(T = \{1, 2\}\) 和 \(T = \{1, 3\}\) 时，给出 \((\mathcal{C}^\perp)_T\) 和 \((\mathcal{C}_T)^\perp\) 的生成矩阵。

## 1.5.4 直和

对于 \(i \in \{1, 2\}\)，设 \(\mathcal{C}_i\) 为在同一有限域 \(\mathbb{F}_q\) 上的一个 \([n_i, k_i, d_i]\) 码。则它们的 *直和* 是 \([n_1 + n_2, k_1 + k_2, \min\{d_1, d_2\}]\) 码
\[
\mathcal{C}_1 \oplus \mathcal{C}_2 = \{(\mathbf{c}_1, \mathbf{c}_2) | \mathbf{c}_1 \in C_1, \mathbf{c}_2 \in C_2\}.
\]

如果 \(\mathcal{C}_i\) 的生成矩阵为 \(G_i\) 且奇偶校验矩阵为 \(H_i\)，则
\[
G_1 \oplus G_2 = \begin{bmatrix} G_1 & O \\ O & G_2 \end{bmatrix} \text{ 和 } H_1 \oplus H_2 = \begin{bmatrix} H_1 & O \\ O & H_2 \end{bmatrix} \quad (1.4)
\]
分别是 \(\mathcal{C}_1 \oplus \mathcal{C}_2\) 的生成矩阵和奇偶校验矩阵。

### 练习 30
设 \(\mathcal{C}_i\) 对于 \(i \in \{1, 2\}\) 具有生成矩阵 \(G_i\) 和奇偶校验矩阵 \(H_i\)。证明 \(\mathcal{C}_1 \oplus \mathcal{C}_2\) 的生成矩阵和奇偶校验矩阵如 (1.4) 所示。

### 练习 31
设 \(\mathcal{C}\) 为具有生成矩阵的二进制码

| 1 | 1 | 0 | 0 | 1 | 1 | 0 |
|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 1 | 1 |

给出 \(\mathcal{C}\) 的另一个生成矩阵，以表明 \(\mathcal{C}\) 是两个二进制码的直和。

### 示例 1.5.8
示例 1.4.4 中的 [6, 3, 2] 二进制码 \(\mathcal{C}\) 是 [2, 1, 2] 码 \(\mathcal{D} = (00, 11)\) 的直和 \(\mathcal{D} \oplus \mathcal{D} \oplus \mathcal{D}\)。

由于两个码的直和的最小距离不超过任一码的最小距离，两个码的直和在应用中通常用处不大，主要具有理论意义。

## 1.5.5 [u | u + v] 构造

相同长度的两个码可以以类似于直和构造的方式组合形成一个长度加倍的第三个码。设 \(\mathcal{C}_i\) 为 \(i \in \{1, 2\}\) 的一个 \([n, k_i, d_i]\) 码，

