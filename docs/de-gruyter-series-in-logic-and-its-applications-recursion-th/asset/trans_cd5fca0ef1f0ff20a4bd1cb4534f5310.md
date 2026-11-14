

由于 Q(y, z) 是 \(\Sigma_1\)，根据定理 3.1.6，存在 \(v \in M\) 使得

\(M \models (\forall y' \in y)(\exists f \in v)(\exists z'(f(y') = z \land P(f))).\)

因此存在 \(w \in M\) 使得 \(w = \{f \mid f \in v \land P(f)\}\)。

对于任意 \(f_1, f_2 \in w\) 和 \(y' \in \text{Dom}(f_1) \cap \text{Dom}(f_2)\)，我们声称 \(f_1(y') = f_2(y')\)。假设不然。那么再次根据基础公理，存在一个 \(y'\) 使得 \(f_1(y') \neq f_2(y')\)，但对于所有 \(y'' \in y'\)，有 \(f_1(y'') = f_2(y'')\)。然而，

\(f_1(y') = G(y', (\langle y'', f_1(y'') \rangle \mid y'' \in y')) = G(y', (\langle y'', f_2(y'') \rangle \mid y'' \in y')) = f_2(y')\),

这产生矛盾。

现在取 \(f' = \bigcup_{f \in w} f\)。根据定理 3.1.7，\(f \in M\)。显然，Dom(f) 是传递的，因此 P(f) 成立。定义 \(f' = f \cup \{\langle y, G(y, f \upharpoonright y) \rangle\}\)。那么 \(M \models f'(y) = G(y, f \upharpoonright y) \land P(f')\)，从而 \(M \models Q(y, G(y, f' \upharpoonright y))\)。因此 \(M \models (\exists z)Q(y, z)\)，这产生矛盾。

因此 KP ⊢ \((\forall y)(\exists z)Q(y, z)\)。

### 备注 3.1.9.

在定理 3.1.8 中定义类似 G 的函数，通常需要经过一系列简单但繁琐的 \(\Sigma_1\)-归纳步骤。今后我们将把这些步骤的细节留给读者，并简单地称之为“通过 \(\Sigma_1\)-归纳应用定理 3.1.8”。

定理 3.1.8 是可容集理论中的核心结果。它在描述集论中扮演着与有效超限归纳相同的角色。我们通过该定理的一个应用来说明这一点。定义传递闭包算子 TC 为：

\(\text{TC}(\emptyset) = \emptyset\)，且

\(\text{TC}(a) = a \cup \bigcup \{\text{TC}(x) \mid x \in a\}.\)

通过对关系 \(\in\) 进行归纳，可以证明对于任意集合 x，TC(x) 是包含 x 的最小传递集合。问题是该算子在 KP 中是否定义良好。

设 G 为一个 \(\Sigma\)-函数，使得 \(G(\emptyset, y) = \emptyset\) 且 \(G(x, y) = x \cup \bigcup \{y_1 \mid \langle y_0, y_1 \rangle \in y\}\)。那么根据定理 3.1.8，存在一个 \(\Sigma\)-函数 F 使得 \(F(x) = G(x, (\langle y, F(y) \rangle \mid y \in x))\)。不难验证对于每个 x，F(x) = TC(x)。我们有以下推论。

### 推论 3.1.10.

KP ⊢ TC(x) 是一个 \(\Sigma\)-函数。

根据推论 3.1.10，结合定理 3.1.8 的证明，我们有以下定理。

### 定理 3.1.11.

设 G 为一个 n+2 元 \(\Sigma\)-函数。存在一个 n+1 元 \(\Sigma\)-函数 F 使得

\(\text{KP} \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, (\langle z, F(z, x_1, \dots, x_n) \rangle \mid z \in \text{TC}(y))).\)

设 rk 为一个函数，使得

rk(∅) = 0，且

rk(x) = sup{rk(y) + 1 | y ∈ x}.

根据定理 3.1.8，rk 是从集合到序数的一个 \(\Sigma\)-函数。对于任意集合 x，rk(x) 称为 x 的秩。在进行超限归纳时，秩函数是一个方便的工具。

### 3.1.3 折叠引理

如果对于所有 y ∈ x 都有 y ⊆ z ⊆ x，则称集合 x 在 z 中是传递的。如果 z = x，即对于所有 y ∈ x 都有 y ⊆ x，则称集合 x 是传递的。使用定理 3.1.8，我们定义一个 \(\Sigma\)-运算 C_x(y) 如下：

C_x(∅) = ∅；

C_x(a) = \{C_x(y) \mid y \in a \cap x\}.

不难验证对于所有 b，C_b(b) 都是传递的。此外，如果 a ⊆ b 且 a 是传递的，那么对于所有 x ∈ a，C_b(x) = x。定义 c_b = \{(x, C_b(x)) \mid x \in b\}。可以将 c_b 视为从 b 到传递集合 C_b(b) 的映射。通常，c_b 不是单射。

如果对于所有 b_1, b_2 ∈ a，(∀x ∈ a)(x ∈ b_1 ↔ x ∈ b_2) → b_1 = b_2，则称集合 a 是外延的。换句话说，如果 a 中的每个集合都由其在 a 中的成员关系确定，则 a 是外延的。显然，任何传递集都是外延的。以下定理表明任何外延集都与一个传递集同构。

### 定理 3.1.12 (Mostowski [108]).

如果 a 是外延的，那么 c_a 是 a 与 C_a(a) 之间的双射。此外，对于所有 x, y ∈ a，x ∈ y 当且仅当 C_a(x) ∈ C_a(y)。

**证明。** 显然 c_a 是从 a 到 C_a(a) 的满射，且 x ∈ y 蕴含 c_a(x) ∈ c_a(y)。我们证明对于所有 x, y ∈ a，c_a(x) ∈ c_a(y) 蕴含 x ∈ y。然后根据 a 的外延性，c_a 是单射。

假设存在 y_0 ∈ a，使得对于所有 rk(y) < rk(y_0) 的 y ∈ a 和 x ∈ a，x ∈ y 当且仅当 c_a(x) ∈ c_a(y)，但存在 x_0 ∈ a 使得 x_0 ∉ y_0 且 c_a(x_0) ∈ c_a(y_0)。因为 c_a(x_0) ∈ c_a(y_0)，存在 z ∈ a∩y_0 使得 c_a(x_0) = c_a(z) = c_a(y_0)。那么 rk(z) < rk(y_0)。然而，这意味着 x_0 = z ∈ y_0，产生矛盾。

### 3.1.4 可定义性

用 M 表示结构 M 的定义域。

### 定义 3.1.13.

设 F 为语言 L 中的一组公式。

- (i) 给定一个结构 M 和 A ⊆ M，如果存在公式 φ(u, v_0, ..., v_n) ∈ F 和 M 中的有限序列 a_0, ..., a_n，使得 x ∈ A 当且仅当 M ⊨ φ(x, a_0, ..., a_n)，则称 A 在 M 中是 F-可定义的；
- (ii) 如果 \(\mathfrak{M}\) 是一组结构，且对于 \(\mathfrak{M} \in \mathfrak{M}\) 有 \(A_M \subseteq M\)，那么如果存在 \(\mathfrak{F}\) 中的一个无参数公式 \(\varphi(u)\)，使得对于任何 \(\mathfrak{M} \in \mathfrak{M}\)，\(x \in A_{\mathfrak{M}}\) 当且仅当 \(\mathfrak{M} \models \varphi(x)\)，则称 \(\{A_M\}_{\mathfrak{M} \in \mathfrak{M}}\) 在 \(\mathfrak{M}\) 中是 \(\mathfrak{F}\)-一致可定义的。

注意，要使一组结构一致可定义，定义它的公式中不应有参数。

### 3.1.5 绝对性

### 定义 3.1.14.

给定语言 \(\mathscr{L}\) 中的一组句子 \(\mathfrak{F}\)，如果对于每个 \(\varphi \in \mathfrak{F}\)，\(\mathfrak{M} \models \varphi \Leftrightarrow \mathfrak{N} \models \varphi\)，则称两个 \(\mathscr{L}\)-结构 \(\mathfrak{M}\) 和 \(\mathfrak{N}\) 是 \(\mathfrak{F}\)-初等等价的，记作 \(\mathfrak{M} \equiv_{\mathfrak{F}} \mathfrak{N}\)。

如果 \(\mathfrak{F}\) 是所有句子的集合，则称 \(\mathfrak{M}\) 和 \(\mathfrak{N}\) 是 *初等等价* 的，并记作 \(\mathfrak{M} \equiv \mathfrak{N}\)。

### 定义 3.1.15.

给定一组句子 \(\mathfrak{F}\)，如果对于每个 \(\varphi(\bar{v}) \in \mathfrak{F}\) 和有限序列 \(\bar{a} \in M^{<\omega}\)，\(\mathfrak{M} \models \varphi(\bar{a}) \Leftrightarrow \mathfrak{N} \models \varphi(j(\bar{a}))\)，则称从 \(\mathfrak{M}\) 到 \(\mathfrak{N}\) 的嵌入 \(j\) 是 \(\mathfrak{F}\)-初等的，并记作 \(\mathfrak{M} \prec_j^{\mathfrak{F}} \mathfrak{N}\)。

如果 \(\mathfrak{F}\) 是所有公式的集合，则记作 \(\mathfrak{M} \prec^j \mathfrak{N}\)。如果 \(j\) 是包含映射，则记作 \(\mathfrak{M} < \mathfrak{N}\)，并称 \(\mathfrak{M}\) 是 \(\mathfrak{N}\) 的 *初等子结构*，\(\mathfrak{N}\) 是 \(\mathfrak{M}\) 的 *初等扩展结构*。

### 定义 3.1.16.

给定结构类 \(\mathfrak{M}\) 和公式 \(\varphi(\bar{v})\)，(i) 如果对于 \(\mathfrak{M}\) 中的每一对 \(\mathfrak{M} \subseteq \mathfrak{N}\) 和任何有限序列 \(\bar{a} \in M^{<\omega}\)，\(\mathfrak{M} \models \varphi(\bar{a})\) 蕴含 \(\mathfrak{N} \models \varphi(\bar{a})\)，则称 \(\varphi\) 是 \(\mathfrak{M}\)-向上绝对的；(ii) 如果对于 \(\mathfrak{M}\) 中的每一对 \(\mathfrak{M} \subseteq \mathfrak{N}\) 和任何有限序列 \(\bar{a} \in M^{<\omega}\)，\(\mathfrak{N} \models \varphi(\bar{a})\) 蕴含 \(\mathfrak{M} \models \varphi(\bar{a})\)，则称 \(\varphi(\bar{v})\) 是 \(\mathfrak{M}\)-向下绝对的；(iii) 如果 \(\varphi(\bar{v})\) 既是 \(\mathfrak{M}\)-向上绝对的又是 \(\mathfrak{M}\)-向下绝对的，则称 \(\varphi(\bar{v})\) 是 \(\mathfrak{M}\)-绝对的。

### 命题 3.1.17.

设 \(\mathfrak{M}\) 为传递结构类。(i) 每个 \(\Sigma_0\)-公式都是 \(\mathfrak{M}\)-绝对的；(ii) 每个 \(\Sigma_1\)-公式都是 \(\mathfrak{M}\)-向上绝对的；(iii) 每个 \(\Pi_1\)-公式都是 \(\mathfrak{M}\)-向下绝对的。因此每个 \(\Delta_1\)-公式都是 \(\mathfrak{M}\)-绝对的。

**证明。** 我们通过对 \(\Sigma_0\)-公式的复杂度进行归纳来证明 (i)，并将 (ii) 和 (iii) 留给读者。假设 \(\mathfrak{M} \subseteq \mathfrak{N}\) 且 \(\varphi(a)\) 的形式为 \((\exists u \in a)\psi(u, a)\)，其中 \(\psi(u, a)\) 是某个 \(\Sigma_0\)-公式，且 \(a \in M\)。如果 \(\mathfrak{M} \models \varphi(a)\)，则存在 \(a' \in M\) 使得 \(\mathfrak{M} \models \psi(a', a)\)。因为 \(\mathfrak{M} \subseteq \mathfrak{N}\)，根据归纳假设，\(\mathfrak{N} \models \psi(a', a)\)。如果 \(\mathfrak{N} \models \varphi(a)\)，则存在 \(a' \in N\) 使得 \(\mathfrak{N} \models \psi(a', a)\)。因为 \(a' \in a\) 且 \(a \in M\)，根据传递性，有 \(a' \in M\)。然后根据归纳假设，\(\mathfrak{M} \models \psi(a', a)\)。

