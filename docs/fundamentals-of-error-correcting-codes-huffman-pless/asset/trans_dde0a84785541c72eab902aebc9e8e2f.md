

## 12.3.4 在 \(\mathbb{Z}_4\) 上循环码的幂等元生成

### 定理 12.3.20
如果 \( C = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle \) 是 \(\mathbb{Z}_4\) 上奇数长度 \( n \) 的循环码，且 \( f(x)g(x)h(x) = x^n - 1 \)，则 \( C^\perp = \langle h^*(x)g^*(x) \rangle \oplus \langle 2h^*(x)f^*(x) \rangle \)。此外，如果 \( g(x) = 1 \)，则 \( C = \langle f(x) \rangle \) 且 \( C^\perp = \langle h^*(x) \rangle \)；如果 \( h(x) = 1 \)，则 \( C = \langle 2f(x) \rangle \) 且 \( C^\perp = \langle g^*(x) \rangle \oplus \langle 2f^*(x) \rangle \)。

证明：令 \( s(x) = h^*(x)g^*(x) \)；则 \( s^*(x) = \pm h(x)g(x) \)，且在 \( \mathbb{Z}_4[x] \) 中 \( f(x)g(x)s^*(x) = \pm (x^n - 1) \times g(x) \)，这意味着在 \( \mathfrak{R}_n \) 中 \( f(x)g(x)s^*(x) = 0 \)。同样地，\( 2f(x)h(x)s^*(x) = 0 \)。因此，根据引理 12.3.18，\( h^*(x)g^*(x) \in C^\perp \)。同理，\( 2h^*(x)f^*(x) \) 与 \( f(x)g(x) \) 及其循环移位正交。由于在 \( \mathfrak{R}_n \) 中对所有 \( \mathbb{Z}_4[x] \) 中的 \( a(x) \) 和 \( b(x) \) 有 \( 2a(x)2b^*(x) = 0 \)，\( 2h^*(x)f^*(x) \) 与 \( 2f(x)h(x) \) 及其循环移位正交。因此 \( 2h^*(x)f^*(x) \in C^\perp \)。由于 \( x^n - 1 = f^*(x)g^*(x)h^*(x) \)，根据定理 12.3.13，\( \langle h^*(x)g^*(x) \rangle + \langle 2h^*(x)f^*(x) \rangle \) 是直和。因此
\( \langle h^*(x)g^*(x) \rangle \oplus \langle 2h^*(x)f^*(x) \rangle \subseteq C^\perp \)。(12.11)
由于 \( C \) 的类型为 \( 4^{\deg h} 2^{\deg g} 2^{\deg f} \)，根据 (12.3)，\( C^\perp \) 的类型为 \( 4^{\deg h - \deg k - \deg g} 2^{\deg g} 2^{\deg f} \)。但 \( \langle h^*(x)f^*(x) \rangle \) 的类型为 \( 4^{\deg g} 2^{\deg h} 2^{\deg f} \)。由于这些类型一致，在 (12.11) 中取等号，从而证明了第一个陈述。第二个陈述由第一个陈述通过直接计算得出，因为 \( g(x) = 1 \) 意味着 \( g^*(x) = 1 \) 且 \( h^*(x)f^*(x) = x^n - 1 \)，而 \( h(x) = 1 \) 意味着 \( h^*(x) = 1 \)。

### 示例 12.3.21
表 12.1 中的编号 14 码具有 \( f(x) = g_2(x) \)、\( g(x) = g_3(x) \) 和 \( h(x) = g_1(x) \)。因此其对偶码为 \( \langle g_1^*(x)g_3^*(x) \rangle \oplus \langle 2g_1^*(x)g_2^*(x) \rangle = \langle g_1(x)g_3(x) \rangle \oplus \langle 2g_1(x)g_2(x) \rangle \)，即编号 19 码。编号 22 码具有 \( f(x) = 1 \)、\( g(x) = g_1(x)g_2(x) \) 和 \( h(x) = g_2(x) \)。因此其对偶码为 \( \langle g_2^*(x)g_1^*(x)g_2^*(x) \rangle \oplus \langle 2g_2^*(x) \rangle = \langle 2g_2(x) \rangle \)，即编号 11 码。编号 17 码具有 \( f(x) = g_2(x) \)、\( g(x) = g_1(x) \) 和 \( h(x) = g_3(x) \)。其对偶码为 \( \langle g_3^*(x)g_1^*(x) \rangle \oplus \langle 2g_3^*(x)g_2^*(x) \rangle = \langle g_2(x)g_3(x) \rangle \oplus \langle 2g_2(x)g_3(x) \rangle \)，使得该码为自对偶码。长度为 7 的循环自对偶码有三个。

### 练习 722
验证 \(\mathbb{Z}_4\) 上长度为 7 的循环码的对偶码如表 12.1 所示。

## 12.3.4 在 \(\mathbb{Z}_4\) 上循环码的幂等元生成

设 \( C \) 是 \(\mathbb{Z}_4\) 上奇数长度 \( n \) 的非零循环码。根据定理 12.3.13，存在唯一的首一多项式 \( f(x) \)、\( g(x) \) 和 \( h(x) \)，使得 \( x^n - 1 = f(x)g(x)h(x) \) 且 \( C = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle \)。根据定理 12.3.12(i)，\(\{f(x)g(x)\}\) 和 \(\{2f(x)h(x)\}\) 分别可以表示为形式为 \(\langle \bar{g}_i(x) \rangle\) 和 \(\langle 2\bar{g}_i(x) \rangle\) 的理想的直和，其中 \( x^n - 1 = \bar{g}_1(x)\bar{g}_2(x) \cdots \bar{g}_t(x) \) 是 \( x^n - 1 \) 在 \(\mathbb{Z}_4[x]\) 中分解为不可约多项式的乘积，且 \(\bar{g}_i(x) = \prod_{j \in J_i} g_j(x)\)。因此，对于 \(\{1, 2, \dots, t\}\) 的某些子集 \( J \) 和 \(\mathcal{J}\)，有 \( f(x)g(x) = \sum_{i \in J} \langle \bar{g}_i(x) \rangle \) 和 \(\langle 2g(x)h(x) \rangle = \sum_{j \in J} \langle 2\bar{g}_j(x) \rangle\)。定理 12.3.12(iv) 表明 \(\langle \bar{g}_i(x) \rangle = \langle \bar{e}_i(x) \rangle\)，其中 \(\bar{e}_i(x)\) 是 \(\mathfrak{R}_n\) 的一个幂等元。根据练习 723(a) 和 (b)，\(\langle f(x)g(x) \rangle = \langle e(x) \rangle\) 和 \(\langle g(x)h(x) \rangle = \langle E(x) \rangle\)，其中 \( e(x) \) 和 \( E(x) \) 是 \(\mathfrak{R}_n\) 中的幂等元。这证明了以下定理。

### 定理 12.3.22
设 \( C = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle \) 是 \(\mathbb{Z}_4\) 上奇数长度 \( n \) 的非零循环码，且 \( x^n - 1 = f(x)g(x)h(x) \)。则：

- (i) 如果 \( g(x) = 1 \)，\(\mathcal{C} = \langle f(x) \rangle = \langle e(x) \rangle\)。
- (ii) 如果 \( h(x) = 1 \)，\(\mathcal{C} = \langle 2f(x) \rangle = \langle 2E(x) \rangle\)，且
- (iii) 如果 \( g(x) \neq 1 \) 且 \( h(x) \neq 1 \)，\(\mathcal{C} = \langle f(x)g(x) \rangle \oplus \langle 2f(x)h(x) \rangle = \langle e(x) \rangle \oplus \langle 2E(x) \rangle\)，
  其中 \( e(x) \) 和 \( E(x) \) 是 \(\mathfrak{R}_n\) 中的非零幂等元。

### 练习 723
设 \( I \subseteq \{1, 2, \dots, k\} \)，并令 \( I' = \{1, 2, \dots, k\} \setminus I \) 为 \( I \) 的补集。完成以下任务：

- (a) 证明 \( \sum_{i \in I} \hat{e}_i(x) \) 是 \(\mathfrak{R}_n\) 中的一个幂等元。提示：回顾 \(\{\hat{e}_i(x) \mid 1 \leq i \leq k\}\) 是两两正交的幂等元。
- (b) 证明 \( \sum_{i \in I} \hat{e}_i(x) = (\sum_{i \in I'} \hat{e}_i(x)) \)。
- (c) 证明 \( [\{ \sum_{i \in I} \hat{e}_i(x) \}] = (\sum_{i \in I} \hat{e}_i(x)) \)。提示：参见定理 12.3.13 的证明。

根据定理 12.3.22，\(\mathcal{C} = \langle e(x) \rangle \oplus \langle 2E(x) \rangle\)，其中 \( e(x) \) 和 \( E(x) \) 是幂等元。根据练习 724，\(\mathcal{C} = \langle e(x) + 2E(x) \rangle\)。我们称 \( e(x) + 2E(x) \) 为 \(\mathcal{C}\) 的“生成幂等元”。我们将使用引号，因为 \( e(x) + 2E(x) \) 并非真正的幂等元（除非 \( E(x) = 0 \)）；然而，使用这个术语是恰当的，因为 \( e(x) \) 和 \( E(x) \) 是组合生成 \(\mathcal{C}\) 的幂等元。当 \( E(x) = 0 \) 且因此 \(\mathcal{C}\) 实际上由一个幂等元生成时（定理 12.3.22 的情况 (i)），我们将使用术语生成幂等元，不加引号。

### 练习 724
设 \(\mathcal{C} = \langle e(x) \rangle \oplus \langle 2E(x) \rangle\)，其中 \( e(x) \) 和 \( E(x) \) 是幂等元。证明 \(\mathcal{C} = \langle e(x) + 2E(x) \rangle\)。

回顾，乘数 \(\mu_a\) 在 \(\{0, 1, \dots, n-1\}\) 上由 \( i\mu_a \equiv ia \pmod n \) 定义，当 \(\gcd(a, n) = 1\) 时，它是长度为 \( n \) 的循环码的坐标位置 \(\{0, 1, \dots, n-1\}\) 的一个排列。我们可以将乘数应用于 \(\mathbb{Z}_4\)-线性码。与 \(\mathbb{F}_q\) 上的循环码一样，\(\mu_a\) 对 \(\mathfrak{R}_n\) 的作用为：对于 \( f(x) \in \mathfrak{R}_n \)，\( f(x)\mu_a \equiv f(x^a) \pmod{x^n - 1} \)。参见 (4.4)。此外，对于 \(\mathfrak{R}_n\) 中的 \( f(x) \) 和 \( g(x) \)，有 \( (f(x)g(x))\mu_a = f(x)\mu_a g(x)\mu_a \)。这意味着，如果 \( e(x) \) 是 \(\mathfrak{R}_n\) 中的幂等元，那么 \( e(x)\mu_a \) 也是。在某些情况下，我们可以计算 \(\mathbb{Z}_4\) 上循环码的对偶码的生成幂等元以及两个这样的码的交和；请与定理 4.3.7 和 4.4.9 相比较。

### 引理 12.3.23
以下结论成立：

- (i) 设 \(\mathcal{C} = \langle e(x) \rangle\) 为具有生成幂等元 \( e(x) \) 的 \(\mathbb{Z}_4\)-线性循环码。则 \(\mathcal{C}^\perp\) 的生成幂等元为 \( 1 - e(x)\mu_{-1} \)。
- (ii) 对于 \( i = 1 \) 和 \( 2 \)，设 \(\mathcal{C}_i = \langle e_i(x) \rangle\) 为具有生成幂等元 \( e_i(x) \) 的 \(\mathbb{Z}_4\)-线性循环码。则 \(\mathcal{C}_1 \cap \mathcal{C}_2\) 的生成幂等元为 \( e_1(x)e_2(x) \)，\(\mathcal{C}_1 + \mathcal{C}_2\) 的生成幂等元为 \( e_1(x) + e_2(x) - e_1(x)e_2(x) \)。

**证明：** 由于在 \(\mathfrak{R}_n\) 中 \( e(x)(1 - e(x)) = 0 \)，根据引理 12.3.18，\( e(x) \) 与 \( 1 - e(x) \) 的倒多项式及其所有移位正交；但这些仅仅是 \( 1 - e(x)\mu_{-1} \) 的循环移位的标量倍数。因此 \( 1 - e(x)\mu_{-1} \in \mathcal{C}^\perp \)。在定理 12.3.13 的记号中，\(\mathcal{C}\) 的生成多项式为 \( f(x) \)，其中 \( g(x) = 1 \) 且 \( f(x)h(x) = x^n - 1 \)，因为 \(\mathcal{C}\) 具有生成幂等元（与由幂等元加上两倍幂等元生成相对）。根据定理 12.3.20，\(\mathcal{C}^\perp\) 的生成多项式为 \( h^*(x) \)，然而，\( 1 - e(x) \)

