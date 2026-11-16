
练习 6 证明来自示例 1.3.2 的 \(\widehat{\mathcal{H}}_3\) 和来自示例 1.3.3 的 \(\mathcal{H}_{3,3}\) 是自偶代码。

练习 7 找出示例 1.3.3 中给出的四元码的所有信息集。

在研究域 \(\mathbb{F}_4\) 上的四元码（示例 1.1.3）时，考虑另一种内积通常很有用，称为厄米内积，由

\((\mathbf{x}, \mathbf{y}) = \mathbf{x} \cdot \overline{\mathbf{y}} = \sum_{i=1}^n x_i \overline{y_i},\)

给出，其中 \(\overline{-}\)，称为共轭，由 \(\overline{0} = 0, \overline{1} = 1\)，和 \(\overline{\omega} = \omega^2\) 给出。使用这个内积，我们可以定义四元码 \(\mathcal{C}\) 的厄米对偶为，类似于 (1.2)，

\(\mathcal{C}^{\perp_H} = \{ \mathbf{x} \in \mathbb{F}_q^n \mid (\mathbf{x}, \mathbf{c}) = 0 \text{ for all } \mathbf{c} \in \mathcal{C} \}.\)

定义 \(\mathcal{C}\) 的共轭为

\(\overline{\mathcal{C}} = \{ \overline{\mathbf{c}} \mid \mathbf{c} \in \mathcal{C} \},\)

其中 \(\overline{\mathbf{c}} = \overline{c_1} \overline{c_2} \cdots \overline{c_n}\) 当 \(\mathbf{c} = c_1 c_2 \cdots c_n\) 时。注意 \(\mathcal{C}^{\perp_H} = \overline{\mathcal{C}^\perp}\)。我们也有厄米自正交和厄米自偶：即，\(\mathcal{C}\) 是厄米自正交的如果 \(\mathcal{C} \subseteq \mathcal{C}^{\perp_H}\)，且 \(\mathcal{C}\) 是厄米自偶的如果 \(\mathcal{C} = \mathcal{C}^{\perp_H}\)。

练习 8 证明如果 \(\mathcal{C}\) 是 \(\mathbb{F}_4\) 上的码，则 \(\mathcal{C}^{\perp_H} = \overline{\mathcal{C}^\perp}.\)

示例 1.3.4 \([6, 3]\) 四元码 \(\mathcal{G}_6\) 在标准形式下的生成矩阵 \(G_6\) 由

\(G_6 = \begin{bmatrix} 1 & 0 & 0 & 1 & \omega & \omega \\ 0 & 1 & 0 & \omega & 1 & \omega \\ 0 & 0 & 1 & \omega & \omega & 1 \end{bmatrix}.\)

给出。该码通常称为六元码。它是厄米自偶的。

练习 9 验证 \(\mathbb{F}_4^n\) 上厄米内积的以下性质：

- (a) \((\mathbf{x}, \mathbf{x}) \in \{0, 1\}\) 对所有 \(\mathbf{x} \in \mathbb{F}_4^n\) 成立。
- (b) \((\mathbf{x}, \mathbf{y} + \mathbf{z}) = (\mathbf{x}, \mathbf{y}) + (\mathbf{x}, \mathbf{z})\) 对所有 \(\mathbf{x}, \mathbf{y}, \mathbf{z} \in \mathbb{F}_4^n\) 成立。
- (c) \((\mathbf{x} + \mathbf{y}, \mathbf{z}) = (\mathbf{x}, \mathbf{z}) + (\mathbf{y}, \mathbf{z})\) 对所有 \(\mathbf{x}, \mathbf{y}, \mathbf{z} \in \mathbb{F}_4^n\) 成立。
- (d) \(\overline{(\mathbf{x}, \mathbf{y})} = (\mathbf{y}, \mathbf{x})\) 对所有 \(\mathbf{x}, \mathbf{y} \in \mathbb{F}_4^n\) 成立。
- (e) \((\alpha \mathbf{x}, \mathbf{y}) = \alpha (\mathbf{x}, \mathbf{y})\) 对所有 \(\mathbf{x}, \mathbf{y} \in \mathbb{F}_4^n\) 成立。
- (f) \((\mathbf{x}, \alpha \mathbf{y}) = \overline{\alpha} (\mathbf{x}, \mathbf{y})\) 对所有 \(\mathbf{x}, \mathbf{y} \in \mathbb{F}_4^n\) 成立。

练习 10 证明示例 1.3.4 中的六元码 \(\mathcal{G}_6\) 是厄米自偶的。

## 1.4 权重和距离

码的一个重要不变量是码字之间的最小距离。两个向量 \(\mathbf{x}, \mathbf{y} \in \mathbb{F}_q^n\) 之间的（汉明）距离 \(d(\mathbf{x}, \mathbf{y})\) 定义为 x 和 y 不同的坐标数量。距离的以下性质的证明留作练习。

### 定理 1.4.1 距离函数 d(x, y) 满足以下四个性质：

- (i) (非负性) d(x, y) >= 0 对所有 x, y in F_q^n 成立。
- (ii) d(x, y) = 0 当且仅当 x = y。
- (iii) (对称性) d(x, y) = d(y, x) 对所有 x, y in F_q^n 成立。
- (iv) (三角不等式) d(x, z) <= d(x, y) + d(y, z) 对所有 x, y, z in F_q^n 成立。

这使得距离函数成为向量空间 F_q^n 上的一个度量。

### 练习 11 证明定理 1.4.1。

码 C 的（最小）距离是不同码字之间的最小距离，对于确定 C 的纠错能力很重要；如我们稍后将看到，最小距离越高，码能纠正的错误越多。向量 x in F_q^n 的（汉明）权重 wt(x) 是 x 中非零坐标的数量。距离和权重之间的以下关系的证明也留作练习。

### 定理 1.4.2 如果 x, y in F_q^n，则 d(x, y) = wt(x - y)。如果 C 是线性码，则最小距离 d 与 C 的非零码字的最小权重相同。

作为该定理的结果，对于线性码，最小距离也称为码的最小权重。如果已知 [n, k] 码的最小权重 d，则我们将该码称为 [n, k, d] 码。

### 练习 12 证明定理 1.4.2。

在处理 F_2, F_3 或 F_4 上的码时，关于码字权重有一些初等结果被证明是有用的。我们将它们收集在此，并将证明留给读者。

### 定理 1.4.3 以下成立：

- (i) 如果 x, y in F_2^n，则 wt(x + y) = wt(x) + wt(y) - 2wt(x AND y)，其中 x AND y 是 F_2^n 中的向量，恰好在 x 和 y 都有 1 的位置上有 1。
- (ii) 如果 x, y in F_2^n，则 wt(x AND y) = x . y (mod 2)。
- (iii) 如果 x in F_2^n，则 wt(x) = x . x (mod 2)。
- (iv) 如果 x in F_3^n，则 wt(x) = x . x (mod 3)。
- (v) 如果 x in F_4^n，则 wt(x) = (x, x) (mod 2)。

### 练习 13 证明定理 1.4.3。

设 A_i，也记作 A_i(C)，为 C 中权重为 i 的码字数量。0 <= i <= n 的列表 A_i 称为 C 的权重分布或权重谱。大量研究致力于计算特定码或码族的权重分布。

### 示例 1.4.4 设 C 为具有生成矩阵的二进制码

$$
G = \begin{bmatrix} 1 & 1 & 0 & 0 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 & 1 \end{bmatrix}.
$$

C 的权重分布为 A_0 = A_6 = 1 和 A_2 = A_4 = 3。注意通常只列出非零的 A_i。

### 练习 14 找出具有生成矩阵的三元码的权重分布

$$
G = \begin{bmatrix} 1 & 1 & 0 & 0 & 0 & 0 \\ 0 & 0 & 1 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 & 1 \end{bmatrix}.
$$

将你的结果与示例 1.4.4 进行比较。

关于权重分布的某些初等事实收集在以下定理中。关于码的权重分布的更深入结果将在第 7 章中介绍。

### 定理 1.4.5 设 \(\mathcal{C}\) 为 \(\mathbb{F}_q\) 上的 [n, k, d] 码。则：

- (i) \(A_0(\mathcal{C}) + A_1(\mathcal{C}) + \cdots + A_n(\mathcal{C}) = q^k\)。
- (ii) \(A_0(\mathcal{C}) = 1\) 且 \(A_1(\mathcal{C}) = A_2(\mathcal{C}) = \cdots = A_{d-1}(\mathcal{C}) = 0\)。
- (iii) 如果 \(\mathcal{C}\) 是包含码字 \(\mathbf{1} = 11\cdots 1\) 的二进制码，则 \(A_i(\mathcal{C}) = A_{n-i}(\mathcal{C})\) 对 \(0 \le i \le n\) 成立。
- (iv) 如果 \(\mathcal{C}\) 是二进制自正交码，则每个码字具有偶权重，且 \(\mathcal{C}^\perp\) 包含码字 \(\mathbf{1} = 11\cdots 1\)。
- (v) 如果 \(\mathcal{C}\) 是三元自正交码，则每个码字的权重可被三整除。
- (vi) 如果 \(\mathcal{C}\) 是四元厄米自正交码，则每个码字的权重是偶数。

### 练习 15 证明定理 1.4.5。

定理 1.4.5(iv) 指出二进制自正交码 \(\mathcal{C}\) 中的所有码字都有偶权重。如果我们查看 \(\mathcal{C}\) 中权重可被四整除的码字子集，我们会惊讶地发现它是 \(\mathcal{C}\) 的一个子码；即，权重可被四整除的码字子集构成 \(\mathcal{C}\) 的一个子空间。对于非自正交码，情况不一定如此。

### 定理 1.4.6 设 \(\mathcal{C}\) 为 [n, k] 二进制自正交码。设 \(\mathcal{C}_0\) 为 \(\mathcal{C}\) 中权重可被四整除的码字集合。则以下之一成立：

- (i) \(\mathcal{C} = \mathcal{C}_0\)，或
- (ii) \(\mathcal{C}_0\) 是 \(\mathcal{C}\) 的 [n, k-1] 子码，且 \(\mathcal{C} = \mathcal{C}_0 \cup \mathcal{C}_1\)，其中 \(\mathcal{C}_1 = \mathbf{x} + \mathcal{C}_0\) 对于任何权重为偶数但不可被四整除的码字 \(\mathbf{x}\)。此外，\(\mathcal{C}_1\) 由 \(\mathcal{C}\) 中所有权重不可被四整除的码字组成。
