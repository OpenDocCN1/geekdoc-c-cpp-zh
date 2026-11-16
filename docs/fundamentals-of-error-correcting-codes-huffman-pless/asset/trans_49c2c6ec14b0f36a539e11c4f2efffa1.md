

$\mathbb{F}_4$ 由 $\mu_{-1}$ 和 $\mu_{-2}$ 共同给出。最后，如果 $p = 73$，$\text{ord}_p(2) = 9$ 且 73 在 $\mathbb{F}_2$ 上有一个由 $\mu_{-1}$ 和 $\mu_{-2}$ 共同给出的分裂；73 在 $\mathbb{F}_4$ 上也有一个由 $\mu_{-1}$ 和 $\mu_{-2}$ 共同给出的分裂。

## 练习 350 找出示例 6.4.11 中提及的分裂。还有哪些其他分裂，以及哪些乘数给出它们？

## 练习 351 本练习解释了定理 6.4.10 的一部分。在第 6.6 节中，我们将讨论 $\mathbb{F}_q$ 上的二次剩余码，它们仅仅是长度为奇素数 $p$ 的双码，其在 $\mathbb{F}_q$ 上的分裂由 $S_1 = \mathcal{Q}_p$ 和 $S_2 = \mathcal{N}_p$ 给出，其中 $\mathcal{Q}_p$ 是 $\mathbb{F}_p$ 中的非零平方数，$\mathcal{N}_p$ 是 $\mathbb{F}_p$ 中的非平方数。如果 $p \equiv \pm 1 \pmod 8$，则存在二进制二次剩余码；$\mathbb{F}_4$ 上的二次剩余码对任何奇素数 $p$ 都存在。请做以下事情：

- (a) 证明在 $\mathbb{F}_p$ 中，两个平方数或两个非平方数的乘积是一个平方数。
- (b) 证明在 $\mathbb{F}_p$ 中，一个平方数和一个非平方数的乘积是一个非平方数。
- (c) 证明如果 $p \equiv 1 \pmod 8$，则 $-1, 2, \text{和 } -2$ 都是 $\mathbb{F}_p$ 中的平方数。
- (d) 证明如果 $p \equiv 1 \pmod 8$，在 $\mathbb{F}_p$ 上的分裂 $S_1 = \mathcal{Q}_p$ 和 $S_2 = \mathcal{N}_p$ 不能由 $\mu_{-1}$ 或 $\mu_{-2}$ 给出。

我们现在考虑 $\mathbb{F}_q$ 上的奇型双码。回顾，如果 $\mathcal{D}$ 是长度为 $n$ 的奇型码，则 $\mathcal{D}$ 的普通扩展 $\widehat{\mathcal{D}}$ 定义为 $\widehat{\mathcal{D}} = \{ \widehat{\mathbf{c}} \mid \mathbf{c} \in \mathcal{D} \}$，其中 $\widehat{\mathbf{c}} = \mathbf{c} c_0 c_1 \cdots c_{n-1} c_\infty$ 且

$c_\infty = - \sum_{j=0}^{n-1} c_j$.

由于奇型双码由定理 6.1.3(v) 为 $[n, (n+1)/2]$ 码，扩展码将是 $[n+1, (n+1)/2]$ 码。因此这些码可能是自双的。如果 $\mathcal{D}$ 是一个奇型双码，则 $\mathcal{D}$ 是通过将 $\bar{j}(x)$ 添加到其偶型子码 $\mathcal{C}$ 的基中得到的。但 $\bar{j}(x)$ 仅仅是全一向量 $\mathbf{1}$ 的一个倍数，因此如果我们想以一种方式扩展 $\mathcal{D}$，使其扩展要么是自双的，要么是另一个扩展型双码的双码，那么我们必须以一种方式扩展 $\mathbf{1}$，使其与自身正交。普通扩展并不总能产生这种结果。然而，下一个结果表明，我们可以修改 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 的扩展方法，在 $\mu_{-1}$ 给出分裂且方程

$1 + \gamma^2 n = 0$

在 $\mathbb{F}_q$ 中有解的情况下。设 $\mathcal{D}$ 为一个奇型双码，并假设 (6.11) 有解。如果 $\mathbf{c} = c_0 c_1 \cdots c_{n-1} \in \mathcal{D}$，令 $\bar{\mathbf{c}} = c_0 c_1 \cdots c_{n-1} c_\infty$，其中

$c_\infty = -\gamma \sum_{i=0}^{n-1} c_i$。

$\mathcal{D}$ 的新扩展定义为 $\tilde{\mathcal{D}} = \{ \tilde{\mathbf{c}} \mid \mathbf{c} \in \mathcal{D} \}$。注意，码 $\widehat{\mathcal{D}}$ 和 $\tilde{\mathcal{D}}$ 是单式等价的，因为 $\tilde{\mathcal{D}} = \widehat{\mathcal{D}}D$，其中 $D$ 是 $(n+1) \times (n+1)$ 对角矩阵 $D = \text{diag}(1, 1, \dots, 1, \gamma)$。

## 定理 6.4.12 设 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 为 $\mathbb{F}_q$ 上长度为 $n$ 的一对奇型双码。假设 (6.11) 有一个解 $\gamma \in \mathbb{F}_q$。以下成立：(i) 如果 $\mu_{-1}$ 为 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 给出分裂，则 $\widetilde{\mathcal{D}}_1$ 和 $\widetilde{\mathcal{D}}_2$ 是自双的。(ii) 如果 $\mathcal{D}_1\mu_{-1} = \mathcal{D}_1$，则 $\widetilde{\mathcal{D}}_1$ 和 $\widetilde{\mathcal{D}}_2$ 是彼此的双码。

证明：设 $\mathcal{C}_1$ 和 $\mathcal{C}_2$ 为与 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 关联的一对偶型双码。我们有以下两个观察：(a) $\widetilde{j(x)}$ 与自身正交。(b) $\widetilde{j(x)}$ 与 $\widetilde{\mathcal{C}}$ 正交。

第一个成立，因为作为向量，$\widetilde{j(x)}$ 是 $(1/n, 1/n \dots, 1/n, -\gamma) \in \mathbb{F}_q^{n+1}$。由于 $\gamma$ 的选择，$\widetilde{j(x)}$ 与自身正交。第二个成立，因为 $\mathcal{C}_i$ 是偶型的，且 $\widetilde{\mathcal{C}}_i$ 中的扩展坐标始终为 0。

假设 $\mu_{-1}$ 给出 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 的分裂。则 $\mathcal{C}_1\mu_{-1} = \mathcal{C}_2$。由定理 6.4.2，$\mathcal{C}_1 = \mathcal{D}_1^+$；此外，$\mathcal{C}_i$ 由定理 6.4.1 是自正交的。由于 $\mathcal{C}_1$ 的扩展是平凡的，$\widetilde{\mathcal{C}}_1$ 是自正交的。由 (a) 和 (b)，由 $\widetilde{\mathcal{C}}_1$ 和 $\widetilde{j(x)}$ 生成的码是自正交的。由定理 6.1.3(v) 和 (ix)，这个自正交码是 $\widetilde{\mathcal{D}}_1$，因此是自双的。类似地，$\widetilde{\mathcal{D}}_2$ 是自双的，从而证明 (i)。

现在假设 $\mathcal{D}_1\mu_{-1} = \mathcal{D}_1$。则 $\mathcal{C}_1\mu_{-1} = \mathcal{C}_1$。由定理 6.4.3，$\mathcal{C}_2 = \mathcal{D}_1^\perp$，因此由定理 6.1.3(vi)，$\widetilde{\mathcal{C}}_2$ 和 $\widetilde{\mathcal{C}}_1$ 互相正交。由 (a) 和 (b)，由 $\widetilde{\mathcal{C}}_1$ 和 $\widetilde{\mathcal{C}}_2$ 生成的码以及由 $\widetilde{\mathcal{C}}_1$ 和 $\widetilde{j(x)}$ 生成的码互相正交。由定理 6.1.3(v) 和 (ix)，这些码是维为 $(n+1)/2$ 的 $\widetilde{\mathcal{D}}_1$ 和 $\widetilde{\mathcal{D}}_2$；因此它们是彼此的双码。

在继续之前，我们做几点说明。

- - $\widetilde{\mathcal{D}}_i$ 的一个生成矩阵可通过取 $\mathcal{C}_i$ 的任意生成矩阵，添加一列零并添加表示 $n\widetilde{j(x)}$ 的行 $1, \dots, 1, 1, -\gamma n$ 得到。
- - 一般来说，满足 (6.11) 的 $\gamma$ 在 $\mathbb{F}_q$ 中存在，当且仅当 $n$ 和 $-1$ 在 $\mathbb{F}_q$ 中都是平方数或都是非平方数。
- - 如果 $q$ 是平方数，则 $\mathbb{F}_q$ 包含使 (6.11) 成立的 $\gamma$，正如我们现在所见。如果 $q = \gamma^{2r}$，其中 $r$ 是素数，则系数在 $\mathbb{F}_r$ 中的每个二次多项式在 $\mathbb{F}_r$ 中都有根，根据定理 3.5.3，$\mathbb{F}_r$ 是 $\mathbb{F}_q$ 的子域。由于 $\gamma$ 是二次式 $nx^2 + 1$ 的根，$\mathbb{F}_r \subseteq \mathbb{F}_q$ 包含 $\gamma$。
- - 在 (6.11) 中，如果 $\mathbb{F}_q$ 的特征为 $r$ 且 $n \equiv -1 (\text{mod } r)$，则 $\gamma = 1$。对于这种情况，$\widehat{\mathcal{D}}_i = \widetilde{\mathcal{D}}_i$。特别是，如果 $\mathbb{F}_q$ 的特征为 2，则是这种情况。更具体地说，如果 $\widehat{\mathcal{D}}_i = \widetilde{\mathcal{D}}_i$，则码要么在 $\mathbb{F}_2$ 上，要么在 $\mathbb{F}_4$ 上。
- - 存在 $n$ 和 $q$ 的值，使得双码存在但 $\gamma$ 不存在。例如，如果 $q = 3$，则根据定理 6.3.3，双码仅在 $n \equiv \pm 1 (\text{mod } 12)$ 时存在。假设 $n \equiv 1 (\text{mod } 12)$。如果 $\gamma \in \mathbb{F}_3$ 满足 (6.11)，则在 $\mathbb{F}_3$ 中 $1 + \gamma^2 = 0$，这是不可能的。如果 $n \equiv -1 (\text{mod } 12)$ 且 $\gamma \in \mathbb{F}_3$ 满足 (6.11)，则在 $\mathbb{F}_3$ 中 $1 - \gamma^2 = 0$，其解为 $\gamma = \pm 1$。因此，如果 $n \equiv -1 (\text{mod } 12)$，我们可以选择 $\gamma = 1$，此时 $\widetilde{\mathcal{D}}_i$ 是普通扩展 $\widehat{\mathcal{D}}_i$。

## 示例 6.4.13 模 11 的 5-循环类为 $C_0 = \{0\}$、$C_1 = \{1, 3, 4, 5, 9\}$ 和 $C_2 = \{2, 6, 7, 8, 10\}$。11 在 $\mathbb{F}_5$ 上有一个分裂 $S_1 = C_1$ 和 $S_2 = C_2$；它由 \(\mu_{-1}\) 给出。设 \(i_1(x) = x + x^3 + x^4 + x^5 + x^9\) 和 \(i_2(x) = x^2 + x^6 + x^7 + x^8 + x^{10}\)。\(\mathcal{E}_{11}\) 在 \(\mathbb{F}_4\) 上的生成幂等元为 \(-i_1(x) - i_2(x)\)。长度为 11 的偶型双码 \(\mathcal{C}_1\) 和 \(\mathcal{C}_2\) 在 \(\mathbb{F}_3\) 上具有生成幂等元 \(e_1(x) = i_1(x) - 2i_2(x)\) 和 \(e_2(x) = -2i_1(x) + i_2(x)\)。奇型双码 \(\mathcal{D}_1\) 和 \(\mathcal{D}_2\) 具有生成幂等元 \(1 + 2i_1(x) - i_2(x)\) 和 \(1 - i_1(x) + 2i_2(x)\)。(6.11) 的解为 \(\gamma = \pm 2\)。因此 \(\widehat{\mathcal{D}}_i \neq \widetilde{\mathcal{D}}_i\)；然而，\(\widetilde{\mathcal{D}}_i\) 根据定理 6.4.12(i) 是自双的。

## 练习 352 验证示例 6.4.13 中提出的主张。

如果在 \(\mathbb{F}_q\) 中 (6.11) 无解，只要我们愿意对 \(\mathcal{D}_1\) 和 \(\mathcal{D}_2\) 的最后一个坐标进行不同的重新缩放，如果 \(\mathcal{D}_1\mu_{-1} = \mathcal{D}_1$，则可以得到双码。作为练习留待证明：如果 \(\mathcal{D}_1\mu_{-1} = \mathcal{D}_1$，则 \(\widehat{\mathcal{D}}_1\) 和 \(\widehat{\mathcal{D}}_2\) 是双码，其中 \(D' = \text{diag}(1, 1, \dots, 1, -1/n)\)。

## 练习 353 设 \(\mathcal{D}_1\) 和 \(\mathcal{D}_2\) 为 $\mathbb{F}_q$ 上长度为 $n$ 的两个奇型双码，且 \(\mathcal{D}_1\mu_{-1} = \mathcal{D}_1\)。证明 \(\widehat{\mathcal{D}}_1\) 和 \(\widehat{\mathcal{D}}_2\) 是双码，其中 \(D' = \text{diag}(1, 1, \dots, 1, -1/n)\)。

以类似于定理 6.4.12 的方式，以下定理解释了在 Hermitian 内积下 $\mathbb{F}_4$ 上扩展奇型双码的双重性。回顾，在这种情况下，$\gamma = 1$ 是 (6.11) 的解，且 $\widehat{\mathcal{D}}_i = \widetilde{\mathcal{D}}_i$。

## 定理 6.4.14 设 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 为 $\mathbb{F}_4$ 上长度为 $n$ 的一对奇型双码。以下成立：(i) 如果 $\mu_{-2}$ 为 $\mathcal{D}_1$ 和 $\mathcal{D}_2$ 给出分裂，则 $\widehat{\mathcal{D}}_1$ 和 $\widehat{\mathcal{D}}_2$ 是 Hermitian 自双的。(ii) 如果 $\mathcal{D}_1\mu_{-2} = \mathcal{D}_1$，则 $\widehat{\mathcal{D}}_1$ 和 $\widehat{\mathcal{D}}_2$ 是彼此的 Hermitian 双码。

## 练习 354 证明定理 6.4.14。

我们可以表征存在自双扩展循环二进制码的长度。为此，我们需要以下两个引理。

## 引理 6.4.15 对于奇素数 $p$ 和正整数 $b$，$-1$ 是模 $p^b$ 的 2 的幂，当且仅当 $\text{ord}_p(2)$ 是偶数。

证明：假设 $\text{ord}_p(2)$ 是偶数。设 $w = \text{ord}_p(2)$，由于 $2^w \equiv 1 (\text{mod } p^b)$ 蕴含 $2^w \equiv 1 (\text{mod } p)$，$w$ 不能是奇数。因此 $w = 2r$ 且 $(2^r)^2 \equiv 1 (\text{mod } p^b)$。于是 $2^r \not\equiv 1 (\text{mod } p^b)$ 是 $x^2 \equiv 1 (\text{mod } p^b)$ 的一个解。根据练习 355，$2^r \equiv -1 (\text{mod } p^b)$，且 $-1$ 是模 $p^b$ 的 2 的幂。反之，假设 $-1$ 是模 $p^b$ 的 2 的幂。那么 $-1$ 是模 $p$ 的 2 的幂，因此 $\text{ord}_p(-1) = 2$，$\text{ord}_p(2)$ 是偶数。

## 练习 355 设 $p$ 为奇素数，$b$ 为正整数。证明 $x^2 \equiv 1 (\text{mod } p^b)$ 的唯一解是 $x \equiv \pm 1 (\text{mod } p^b)$。

## 引理 6.4.16 设 $p$ 为奇素数，$a$ 为正整数。由乘数 $\mu_{-1}$ 给出的 $p^a$ 在 $\mathbb{F}_2$ 上的分裂存在，当且仅当 $\text{ord}_p(2)$ 是奇数。

证明：设 $C_i$ 为模 $p^a$ 包含 $i$ 的 2-循环类。假设由 $\mu_{-1}$ 给出的 $p^a$ 在 $\mathbb{F}_2$ 上的分裂 $S_1$ 和 $S_2$ 存在。那么 $C_1$ 和 $C_{\mu-1}$ 不在

