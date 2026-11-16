

或 [149]。令 $\mathcal{D}^{\text{ext}}$ 为奇异型二次剩余码 $\mathcal{D}$ 的扩展 $\widehat{\mathcal{D}}$、$\widetilde{\mathcal{D}}$ 或 $\breve{\mathcal{D}}$ 之一，视情况而定。$\mathcal{D}^{\text{ext}}$ 的坐标标记为 $\{0, 1, \dots, p-1, \infty\} = \mathbb{F}_p \cup \{\infty\}$。显然，对于 $g \in \mathbb{F}_p$，由 $T_g \equiv i + g \pmod p$（对所有 $i \in \mathbb{F}_p$）和 $\infty T_g = \infty$ 给出的映射 $T_g$ 属于 $\text{PAut}(\mathcal{D}^{\text{ext}})$，因为它们在 $\{0, 1, \dots, p-1\}$ 上作循环移位并固定 $\infty$。另外，若 $a \in \mathcal{Q}_p$，乘数 $\mu_a$ 可通过令 $\infty \mu_a = \infty$ 来扩展；根据定理 6.6.3，这也属于 $\text{PAut}(\mathcal{D}^{\text{ext}})$。到目前为止，我们尚未发现任何移动坐标 $\infty$ 的自同构；然而，Gleason-Prange 定理给出了这样的映射。我们不证明此结果。

### 定理 6.6.21（Gleason-Prange 定理）
令 $\mathcal{D}^{\text{ext}}$ 为 $\widehat{\mathcal{D}}$、$\widetilde{\mathcal{D}}$ 或 $\breve{\mathcal{D}}$，其中 $\mathcal{D}$ 是 $\mathbb{F}_q$ 上长度为 $p$ 的 *奇异型二次剩余码*。令 $P$ 为由置换给出的置换矩阵，该置换将 $\infty$ 与 $0$ 互换，并对 $g \in \mathbb{F}_p$、$g \neq 0$ 将 $g$ 与 $-1/g$ 互换。那么存在一个对角矩阵 $D$，其所有对角元均为 $\pm 1$，使得 $DP \in \text{MAut}(\mathcal{D}^{\text{ext}})$。

我们对对角矩阵 $D$ 的精确形式留得比较模糊，因为它取决于未扩展码所使用的具体生成幂等项。不过请注意，如果域 $\mathbb{F}_q$ 的特征为 2，则 $D$ 为单位矩阵。由 $g \in \mathbb{F}_p$ 的 $T_g$、$a \in \mathcal{Q}_p$ 的 $\mu_a$ 以及 $P$ 给出的置换矩阵生成一个记为 $\text{PSL}_2(p)$ 的群，称为 *射影特殊线性群*。除三种情况外，全自同构群 $\text{PAut}(\mathcal{D}^{\text{ext}})$ 仅略大一些（我们可以添加与 $\mathbb{F}_q$ 的域自同构相关的自同构）。三种例外情况发生在 $p=23$ 且 $q=2$ 时（此时 $\mathcal{D}^{\text{ext}}$ 与扩展二进制 Golay 码具有相同的基）、$p=11$ 且 $q=3$ 时（此时 $\mathcal{D}^{\text{ext}}$ 与扩展三元 Golay 码具有相同的基），以及 $p=5$ 且 $q=4$ 时（此时 $\mathcal{D}^{\text{ext}}$ 与六码具有相同的基）。

### 练习 371
求当 $p=5$、$p=11$ 和 $p=23$ 时，Gleason-Prange 定理中置换矩阵 $P$ 对应的循环形式置换。注意，这些 $p$ 值出现在示例 6.6.15 中。

Gleason-Prange 定理中的自同构，连同 $g \in \mathbb{F}_p$ 的 $T_g$ 和 $a \in \mathcal{Q}_p$ 的 $\mu_a$，表明 $\text{MAut}(\mathcal{D}^{\text{ext}})$ 是传递的。根据定理 1.7.13，这意味着 $\mathcal{D}$ 的最小权重等于其最小奇异型权重。由于二次剩余码是二元码，平方根界适用。我们将此总结如下。

### 定理 6.6.22
令 $\mathcal{D}$ 为 $\mathbb{F}_q$ 上长度为 $p$ 的 *奇异型二次剩余码*。$\mathcal{D}$ 的最小权重是其最小 *奇异型权重* $d_o$。此外，$d_o^2 \ge p$。如果 $p \equiv -1 \pmod 4$，则 $d_o^2 - d_o + 1 \ge p$。而且，每个最小权重代码字都是奇异型的。如果 $\mathcal{D}$ 是二进制码，其最小权重 $d=d_o$ 为奇数，并且如果此外 $p \equiv -1 \pmod 8$，则 $d \equiv 3 \pmod 4$。

**证明：** 除最后一项外，所有陈述均源自平方根界和定理 1.7.13，并结合以下观察：$\mu_{-1}$ 在 $-1 \in N_q$ 时（即由引理 6.2.4 知 $p \equiv -1 \pmod 4$）恰好给出二次剩余码的分割。如果 $\mathcal{D}$ 是二进制码，其最小权重 $d$ 为奇数，因为奇异型二进制向量具有奇权重。根据定理 6.6.14，如果 $p \equiv -1 \pmod 8$，则 $\widehat{\mathcal{D}}$ 是双偶码；由于 $\widehat{\mathcal{D}}$ 的最小权重为 $d+1$，故 $d \equiv 3 \pmod 4$。$\square$

### 示例 6.6.23
利用定理 6.6.22，我们可以轻松确定长度分别为 $p=23$ 和 $47$、维数为 12 和 24 的二进制奇异型二次剩余码的最小权重。令 $\mathcal{D}$ 为这样的码。由于 $p \equiv -1 \pmod 4$，每个码都满足 $d_o^2 - d_o + 1 \ge p$ 且 $d_o$ 为奇数。当 $p=23$ 时，该界意味着 $d_o \ge 6$，因此由于 $d_o$ 为奇数，故 $d_o \ge 7$。球型堆积界排除了更高的 $d_o$ 值。根据定理 6.6.14，$\widehat{\mathcal{D}}$ 是一个 [24, 12, 8] 自偶双偶码（扩展二进制 Golay 码）。当 $p=47$ 时，由界得 $d_o \ge 8$，由定理 6.6.22 得 $d_o \equiv 3 \pmod 4$。特别是，$d_o \ge 11$。球型堆积界表明 $d_o < 15$，且由于 $d_o \equiv 3 \pmod 4$，故 $d_o = 11$。因此 $\mathcal{D}$ 是一个 [47, 24, 11] 码。利用定理 6.6.14，$\widehat{\mathcal{D}}$ 是一个 [48, 24, 12] 自偶双偶码。截至目前，尚无其他已知的具有 $d \ge 12$ 的 [48, 24, $d$] 二进制码。

### 练习 372
求长度为 31 的奇异型二进制二次剩余码的最小距离。♦

### 示例 6.6.24
令 $\mathcal{D}$ 为 $\mathbb{F}_3$ 上长度为 $p=11$、维数为 6 的奇异型二次剩余码。设 $\mathcal{D}$ 的最小权重为 $d$，$\widehat{\mathcal{D}}$ 的最小权重为 $\widehat{d}$。根据定理 6.6.14，由于 $p \equiv -1 \pmod{12}$，$\widehat{\mathcal{D}}$ 是自偶码。因此，$3 \mid \widehat{d}$。根据 Singleton 界，$\widehat{d} \le 7$，这意味着 $\widehat{d}=3$ 或 $\widehat{d}=6$。根据定理 6.6.22，$d \ge 4$。由于 $d \le \widehat{d}$，故 $\widehat{d}=6$。由于 $d \ge \widehat{d}-1$，故 $d \ge 5$。根据定理 6.6.10，$\mathcal{D}$ 的生成幂等项权重为 5。因此 $\mathcal{D}$ 是一个 [11, 6, 5] 码，$\widehat{\mathcal{D}}$ 是一个 [12, 6, 6] 自偶码（扩展三元 Golay 码）。

### 示例 6.6.25
令 $\mathcal{D}$ 为 $\mathbb{F}_4$ 上长度为 $p=5$、维数为 3 的奇异型二次剩余码。假设 $\mathcal{D}$ 和 $\widehat{\mathcal{D}}$ 的最小权重分别为 $d$ 和 $\widehat{d}$。根据定理 6.6.14，$\widehat{\mathcal{D}}$ 是 Hermitian 自偶码，这意味着 $2 \mid \widehat{d}$。根据 Singleton 界，$d \le 3$ 且 $\widehat{d} \le 4$。根据定理 6.6.22，$d \ge 3$。因此 $d=3$ 且 $\widehat{d}=4$。所以 $\mathcal{D}$ 是一个 [5, 3, 3] 码，$\widehat{\mathcal{D}}$ 是一个 [6, 3, 4] Hermitian 自偶码（六码）。

### 示例 6.6.26
考虑 $\mathbb{F}_4$ 上长度为 $n=17$ 的二元码。模 17 的 4-循环类为

$C_0 = \{0\}, C_1 = \{1, 4, 16, 13\}, C_2 = \{2, 8, 15, 9\}, C_3 = \{3, 12, 14, 5\},$ 以及 $C_6 = \{6, 7, 11, 10\},$

奇异型二次剩余码 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 的定义集分别为 $Q_{17} = C_1 \cup C_2$ 和 $N_{17} = C_3 \cup C_6$；根据定理 6.6.14，扩展码 $\widehat{\mathcal{D}}_1$ 和 $\widehat{\mathcal{D}}_2$ 在普通内积或 Hermitian 内积下互为对偶码。根据定理 6.6.2，$\mathcal{D}_1$ 和 $\mathcal{D}_2$ 均具有二进制幂等项。根据定理 6.6.22，$\mathcal{D}_1$ 和 $\mathcal{D}_2$ 的最小权重至少为 5；由于所有最小权重代码字都是奇异型的，$\mathcal{D}_1$ 和 $\mathcal{D}_2$ 的最小权重至少为 6。事实上，两者均为 [18, 9, 6] 码。此信息包含在表 6.1 中。还有另外两个分割，分别由 $S_1 = C_1 \cup C_3$ 配合 $S_2 = C_2 \cup C_6$，以及 $S'_1 = C_1 \cup C_6$ 配合 $S'_2 = C_2 \cup C_3$ 给出。这些分割由 $\eta_{46}$ 互换，从而得到等价码对。具有定义集 $S_1$ 和 $S_2$ 的奇异型码 $\mathcal{D}'_1$ 和 $\mathcal{D}'_2$ 具有一个由 $\mu_{-2}$ 给出的分割。根据定理 6.4.14，$\mathcal{D}'_1$ 和 $\mathcal{D}'_2$ 是 Hermitian 自偶码。结果表明，两者均为 [18, 9, 8] 码；这些扩展二元码的最小权重高于扩展二次剩余码的最小权重。这些是表 6.3 中总结的码。文献 [148] 表明，$\mathbb{F}_4$ 上的 Hermitian 自偶 [18, 9, 8] 码是唯一的。后来，文献 [249] 表明，$\mathbb{F}_4$ 上的 [18, 9, 8] 码是唯一的。

本节通过介绍二进制扩展奇异型二次剩余码的自同构群来结束。证明请参见 [149]；我们在示例 9.6.2 中讨论 (i)，在第 10.1.2 节中讨论 (ii)。

### 定理 6.6.27
设 $p$ 为满足 $p \equiv \pm 1 \pmod 8$ 的素数。令 $\mathcal{D}$ 为长度为 $p$ 的二进制奇异型二次剩余码，其扩展码 $\widehat{\mathcal{D}}$ 的长度为 $p+1$。以下结论成立：

- (i) 当 $p=7$ 时，$\Gamma\text{Aut}(\widehat{\mathcal{D}}) = \text{PAut}(\widehat{\mathcal{D}})$ 与阶为 1344 的仿射群 $\text{GA}_2(2)$ 同构。
- (ii) 当 $p=23$ 时，$\Gamma\text{Aut}(\widehat{\mathcal{D}}) = \text{PAut}(\widehat{\mathcal{D}})$ 与阶为 244 823 040 的 Mathieu 群 $\mathcal{M}_{23}$ 同构。
- (iii) 如果 $p \notin \{7, 23\}$，则 $\Gamma\text{Aut}(\widehat{\mathcal{D}}) = \text{PAut}(\widehat{\mathcal{D}})$ 与阶为 $p(p^2 - 1)/2$ 的群 $\text{PSL}_2(p)$ 同构。

