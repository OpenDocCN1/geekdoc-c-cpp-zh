

相反，如果 $\mathcal{C}$ 是具有满足 $(i)$ 的定义集 $T$ 的循环码，则 $\mathcal{C}$ 是 Hermitian 自正交。

**练习 263** 证明定理 4.4.16。

**推论 4.4.17** 设 $\mathcal{D} = \mathcal{C} + \langle \mathbf{1} \rangle$ 是 $\mathbb{F}_4$ 上长度为 $n$ 的循环码，且 $\mathcal{C}$ 是 Hermitian 自正交。则 $\mathcal{D} \cap \mathcal{D}_{\mu-2} = \langle \mathbf{1} \rangle$。

**练习 264** 证明推论 4.4.17。

下一个定理显示了一个相当显著的事实：二进制自正交循环码必须是双偶码。

**定理 4.4.18** 二进制自正交循环码是双偶码。

**证明：** 设 $\mathcal{C}$ 是具有定义集 $T$ 的 $[n, k]$ 二进制自正交循环码。根据定理 1.4.5(i)，$\mathcal{C}$ 只有偶权码字，因此根据练习 238，$0 \in T$。假设 $\mathcal{C}$ 不是双偶码。那么，$\mathcal{C}$ 的子码 $\mathcal{C}_0$（由权可被 4 整除的码字组成）根据定理 1.4.6 具有维数 $k-1$。显然，$\mathcal{C}_0$ 是循环码，因为向量的循环移位是具有相同权的向量。根据定理 4.4.2 和推论 4.2.5（或练习 239），$\mathcal{C}_0$ 的定义集为 $T \cup \{a\}$，其中 $a \notin T$。但此时 $\{a\}$ 必须是模 $n$ 的 2-徙动类，这意味着 $2a \equiv a \pmod n$。由于 $n$ 为奇数，故 $a = 0$，但这不可能，因为 $0 \in T$。

在定理 4.3.8 中，$\mathcal{R}_n$ 中的最小循环码被证明是具有生成多项式 $g(x)$ 的码，其中 $(x^n - 1)/g(x)$ 在 $\mathbb{F}_q$ 上不可约。因此，最小循环码有时被称为 *不可约循环码*。这些最小循环码可以使用迹函数来描述。

**定理 4.4.19** 设 $g(x)$ 是 $\mathbb{F}_q$ 上 $x^q - 1$ 的一个不可约因式。假设 $g(x)$ 的次数为 $s$，并令 $\gamma \in \mathbb{F}_{q^s}$ 为 $g(x)$ 的一个根。设 $\text{Tr}_i : \mathbb{F}_{q^s} \to \mathbb{F}_q$ 为从 $\mathbb{F}_{q^s}$ 到 $\mathbb{F}_q$ 的迹映射。则

```
$C_{\gamma'} = \left\{ \sum_{i=0}^{n-1} \text{Tr}_i(\xi \gamma'^i) x^i \mid \xi \in \mathbb{F}_{q^s} \right\}$
```

是具有非零根 $\{\gamma^{-q^i} \mid 0 \le i < s\}$ 的 $[n, s]$ 不可约循环码。

**证明：** 根据引理 3.8.5，$C_{\gamma'}$ 是 $\mathbb{F}_q$ 上的非零线性码。如果 $c_i(x) = \sum_{i=0}^{n-1} \text{Tr}_i(\xi \gamma'^i) x^i$，则在 $\mathcal{R}_n$ 中 $c_{\gamma'}(x) = c_i(x)$，这意味着 $C_{\gamma'}$ 是循环码。设 $g(x) = \sum_{i=0}^{n-1} g_i x^i$。根据引理 3.8.5，由于 $g_i \in \mathbb{F}_q$ 且 $g(\gamma) = 0$，

```
$\sum_{i=0}^{n-1} g_i \text{Tr}_i(\xi \gamma'^i) = \text{Tr}_i \left( \xi \sum_{i=0}^{n-1} g_i \gamma'^i \right) = \text{Tr}_i(0) = 0.$
```

故 $\langle g(x) \rangle \subseteq C_{\gamma'}^+$。根据定理 4.4.9，$C_{\gamma'}^+$ 是一个不等于 $\mathcal{R}_n$ 的循环码，因为 $C_{\gamma'} \neq \langle \mathbf{0} \rangle$。由于 $g(x)$ 在 $\mathbb{F}_q$ 上不可约，$\langle g(x) \rangle$ 和 $\mathcal{R}_n$ 之间不存在真循环码。因此 $\langle g(x) \rangle = C_{\gamma'}^+$。结果由定理 4.4.9(iii) 得出。

## 4.5 循环码的最小距离

对于任何码，确定最小距离以确定其纠错能力非常重要。因此，对最小距离（尤其是下界）有界限是有帮助的。循环码最小距离有若干已知的下界。其中最古老的是 Bose-Ray-Chaudhuri-Hocquenghem 界 [28, 132]，通常称为 BCH 界，它是第 5 章中介绍的 BCH 码定义的基础。Hartmann 和 Tzeng [117] 以及后来的 van Lint 和 Wilson [203] 对该界进行了改进。这里介绍了 BCH 界、Hartmann-Tzeng 界以及 van Lint 和 Wilson 的一种界定技术。BCH 界和 Hartmann-Tzeng 界取决于码的零点，尤其是寻找“连续”零点串的能力。

在介绍 BCH 界之前，我们陈述一个引理，该引理用于 BCH 界的证明，在其他地方也很有用，关于 Vandermonde 矩阵的行列式。设 \(\alpha_1, ..., \alpha_s\) 是域 \(\mathbb{F}\) 中的元素。\(s \times s\) 矩阵 \(V = [v_{i,j}]\)，其中 \(v_{i,j} = \alpha_j^{i-1}\)，称为 Vandermonde 矩阵。注意，该矩阵的转置也称为 Vandermonde 矩阵。

**引理 4.5.1** det \(V = \prod_{1 \le i < j \le s} (\alpha_j - \alpha_i)\)。特别是，如果元素 \(\alpha_1, ..., \alpha_s\) 互不相同，则 \(V\) 是非奇异的。

在本节中，我们将假设 $\mathcal{C}$ 是 $\mathbb{F}_q$ 上长度为 $n$ 的循环码，且 $\omega$ 是 $\mathbb{F}_{q^t}$ 中的原始 $n$ 次单位根，其中 $t = \text{ord}_n(q)$。回顾，如果 $\mathcal{C}$ 的零点为 $\{\alpha^i \mid i \in T\}$，则 $T$ 是 $\mathcal{C}$ 的一个定义集。因此，$T$ 必须是模 $n$ 的 $q$-徙动类的并集。我们说 $T$ 包含一组 $s$ 个连续元素 $S$，前提是存在一组 $s$ 个连续整数 $\{b, b + 1, ..., b + s - 1\}$，使得

\(\{b, b + 1, ..., b + s - 1\} \text{ mod } n \subseteq S \subseteq T.\)

**例 4.5.2** 考虑定义集为 $T = \{0, 3, 6, 5\}$ 的长度为 7 的二进制循环码 $\mathcal{C}$。那么 $T$ 包含一组三个连续元素 $S = \{5, 6, 0\}$。

**定理 4.5.3（BCH 界）** 设 $\mathcal{C}$ 是 $\mathbb{F}_q$ 上具有定义集 $T$ 的长度为 $n$ 的循环码。假设 $\mathcal{C}$ 的最小权为 $d$。假设 $T$ 对于某个整数 $\delta$ 包含 $\delta - 1$ 个连续元素。则 $d \ge \delta$。

**证明：** 根据假设，$\mathcal{C}$ 的零点包括 $\alpha^b, \alpha^{b+1}, ..., \alpha^{b+\delta-2}$。设 $c(x)$ 是 $\mathcal{C}$ 中权为 $w$ 的非零码字，并令

\(c(x) = \sum_{j=1}^{w} c_{i_j} x^{i_j}.\)

反向假设 $w < \delta$。由于对于 $b \le i \le b + \delta - 2$ 有 $c(\alpha^i) = 0$，故 $M \mathbf{u}^t = \mathbf{0}$，

其中

![](img/0af7e79235839ec0eb8bcf8d229f37d4_170_0.png)

且 $\mathbf{u} = c_{i_1} c_{i_2} \cdots c_{i_w}$。由于 $\mathbf{u} \neq \mathbf{0}$，$M$ 是奇异矩阵，因此 $\det M = 0$。但 $\det M = \alpha^{(i_1+i_2+\cdots+i_w)b} \det V$，其中 $V$ 是 Vandermonde 矩阵

![](img/0af7e79235839ec0eb8bcf8d229f37d4_170_1.png)

由于 $\alpha^i$ 互不相同，根据引理 4.5.1，$\det V \neq 0$，这与 $\det M = 0$ 矛盾。

**练习 265** 找出一个三重纠错 [15, 5] 二进制循环码的生成多项式和生成矩阵。

BCH 界断言，你希望在定义集中找到最长的一组连续元素。然而，定义集取决于所选的原始元素。设 $\beta = \alpha^a$，其中 $\gcd(a, n) = 1$；因此 $\beta$ 也是原始 $n$ 次单位根。所以，如果 $a^{-1}$ 是 $a$ 模 $n$ 的乘法逆元，则最小多项式 $M_{\beta^a}(x)$ 和 $M_{\beta^{a-1}}(x)$ 相等。因此，相对于原始元素 $\alpha$ 具有定义集 $T$ 的码，与相对于原始元素 $\beta$ 具有定义集 $a^{-1}T \mod n$ 的码相同。因此，在应用 BCH 界或任何其他下界时，如果对定义集应用乘数，可能会得到更高的下界。或者，两个码 $\mathcal{C}$ 和 $\mathcal{C}_{\mu_a}$ 是等价的，并且相对于同一原始元素 $\alpha$ 具有定义集 $T$ 和 $a^{-1}T$（根据推论 4.4.5）；因此它们具有相同的最小权，所以可以使用任一组定义集来产生最佳界。

**例 4.5.4** 设 $\mathcal{C}$ 是具有定义集 $T = \{0, 3, 6, 12, 24, 17\}$ 的 [31, 25, d] 二进制循环码。对 $\mathcal{C}$ 应用 BCH 界，我们看到 $d \ge 2$，因为 $T$ 中最长的连续集大小为 1。然而，将 $T$ 乘以 $3^{-1} \equiv 21 \pmod{31}$，我们得到 $3^{-1}T \mod 31 = \{0, 1, 2, 4, 8, 16\}$。将 $\alpha$ 替换为 $\alpha^3$ 或将 $\mathcal{C}$ 替换为 $\mathcal{C}_{\mu_3}$ 并应用 BCH 界，我们得到 $d \ge 4$。实际上，$\mathcal{C}$ 是 Hamming 码 $\mathcal{H}_5$ 的偶权子码，且 $d = 4$。

**例 4.5.5** 设 $\mathcal{C}$ 是具有定义集 $T = \{1, 2, 3, 4, 6, 8, 9, 12, 13, 16, 18\}$ 的 [23, 12, d] 二进制循环码。BCH 界蕴含 $d \ge 5$，因为 $T$ 有四个连续元素。注意，$T = C_1$，即模 23 包含 1 的 2-徙动类。模 23 下，只有另外两个 2-徙动类：$C_0 = \{0\}$ 和 $C_5 = \{5, 7, 10, 11, 14, 15, 17, 19, 20, 21, 22\}$。设 $\mathcal{C}_e$ 为 $\mathcal{C}$ 的偶权子码

