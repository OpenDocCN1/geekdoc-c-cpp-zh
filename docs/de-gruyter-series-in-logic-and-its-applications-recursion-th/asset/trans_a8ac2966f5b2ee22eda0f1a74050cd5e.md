
对于 (iii)，假设 \( f : \omega \to \omega \) 是一个 \(\Delta^1_1\)-函数，使得对于每个 \( n \)，存在一个 \( m \in [2^n, 2^{n+1}) \) 使得 \( f(m) = x(m) \)。那么存在一个分级公式 \( \varphi \)，使得 \( f(n) = m \Leftrightarrow \mathcal{A}(\omega_1^{CK}, x) \models \varphi(\bar{n}, \bar{m}) \)。此外，\(\mathcal{A}(\omega_1^{CK}, x) \models (\forall n)(\exists m \in [2^n, 2^{n+1}))(\varphi(m, x(m)))\)。因此存在一个条件 \( T \)，它强制 \( (\forall n)(\exists m \in [2^n, 2^{n+1}))(\varphi(m, x(m))) \) 且 \( x \in T \)。令 \( n \) 使得 \( T \) 在层级 \( n \) 处完全分裂，并令 \( \sigma \in 2^{n-1} \) 成为 \( T \) 中的一个字符串。令 \( v \) 成为一个字符串，使得 \( v(m) = 1 - f(m + 2^{n-1}) \)。定义 \( S = \{\sigma^\frown \tau \mid \tau \in T\} \subseteq T \)。那么 \( S \Vdash (\forall m \in [2^n, 2^{n+1}))(\neg \varphi(m, x(m)))\)。但 \( S \) 比 \( T \) 更强，这是一个矛盾。根据推论 13.3.12，\( x \) 不是 \(\Delta^1_1\)-可迹的。

我们现在可以将 \(\Delta^1_1\)-可迹性与 \(\Delta^1_1\)-半递归性和 \(\Delta^1_1\)-支配性的合取分开。

### 定理 13.3.18 (Kjos-Hanssen, Nies, Stephan and Yu [68]). 存在 \( 2^{\aleph_0} \) 个 \(\Delta^1_1\)-支配且 \(\Delta^1_1\)-半递归实数，它们不是 \(\Delta^1_1\)-可迹的。

**证明.** 这直接由引理 13.3.17 得出。注意存在 \( 2^{\aleph_0} \) 个泛化实数。

通过与定理 5.3.12 证明中完全相同的论证，我们有以下结论。

### 命题 13.3.19. 存在一个不可数的 \(\Sigma^1_1\)-集合，它仅包含 \(\Delta^1_1\)-支配和 \(\Delta^1_1\)-半递归实数。

### 13.3.4 练习

- **练习 13.3.1.** 证明没有 Cohen 泛化实数是 \(\Delta^1_1\)-支配的。

- **练习 13.3.2.** 证明每个 Cohen 泛化实数都是 \(\Delta^1_1\)-半递归的。

- **练习 13.3.3.** 证明命题 13.3.19。

## 14 高阶随机性理论

高阶随机性理论利用超算术理论和集合论的技术和思想，研究随机性的算法复杂性问题。由于二阶算术提供了对实数更广阔（尽管有时更粗略）的视角，人们得到的随机性图景与一阶理论的图景截然不同。

### 14.1 高阶 Kurtz 随机性

### 14.1.1 \(\Delta^1_1\) 和 \(\Pi^1_1\)-Kurtz 随机性

**定义 14.11.** 令 \(x \in 2^\omega\)。给定实数集的一个类 \(\Gamma\)，如果 \(x\) 不属于 \(\Gamma\) 中的任何闭零集，则称 \(x\) 是 \(\Gamma\)-Kurtz 随机的。

我们关注 \(\Delta^1_1\)、\(\Sigma^1_1\) 和 \(\Pi^1_1\)-Kurtz 随机性。回顾（§ 2.7.1），BC 表示博雷尔码的集合，\(\{A_z \mid z \in \text{BC}\}\) 是由这些码生成的实数集合。

### 命题 14.12.

- (i) \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的，当且仅当 \(x\) 不属于任何 \(\Pi^1_1(\text{HYP})\)-零集。

- (ii) \(\Delta^1_1\)-Kurtz 随机实数的集合是 \(\Sigma^1_1\) 但不是 \(\Delta^1_1\)。

证明. 注意 (i) 直接由定理 2.7.4 得出。此处给出一个自包含的证明。

根据定理 2.7.2，每个 \(\Pi^1_1(\text{HYP})\)-集合都是一个 \(\Delta^1_1\)-集合。因此没有 \(\Delta^1_1\)-Kurtz 随机实数属于一个 \(\Pi^1_1(\text{HYP})\)-零集。反之，令 \(P\) 成为一个 \(\Delta^1_1\)-零集。那么 \(U = \{\sigma \mid (\forall z)(\forall x \in P \to z \neq \sigma) \text{ 是 } \Pi^1_1\}\)。由于 \(P\) 是闭集，且超算术实数的集合是稠密的，我们有

\(\sigma \in U \iff (\forall z \in \text{HYP})(z > \sigma \to z \notin P)\).

根据推论 2.2.12，\(U\) 也是 \(\Sigma^1_1\)，因此是 \(\Delta^1_1\)。故 \(P \in \Pi^1_1(\text{HYP})\)。由此可见 \(x\) 不属于一个 \(\Pi^1_1(\text{HYP})\)-零集，因此 \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的。

为了证明 (ii)，观察集合

\(C = \{(\langle n, e \rangle, y) \mid n \in \emptyset \land \Delta^{B_n}_e \in \Pi_1 \cap \text{HYP} \land y \in A_{\varrho^{B_n}_e}\}\)

是 \(\Pi^1_1\)，其中 \(A_z\) 如 § 2.7.1 所定义。根据命题 13.1.6，集合

\(D = \{(\langle n, e \rangle, y) \mid \mu(y \mid ((\langle n, e \rangle, y) \in C)) = 0\}\)

是 \(\Pi^1_1\)。因此集合

\(E = \{y \mid (\exists m)((m, y) \in D)\}\)

是一个 \(\Pi^1_1\)-零集。此外，根据 (i)，

\((\forall x)(x \in E \to x \text{ 不是 } \Delta^1_1\text{-Kurtz 随机}).\)

因此 \(\Delta^1_1\)-Kurtz 随机实数的集合是 \(\Sigma^1_1\)。现在 \(\mu(E) = 1\)，并且由于没有超算术实数是 \(\Delta^1_1\)-Kurtz 随机的，根据定理 13.11.3 可得出 \(E\) 不是 \(\Delta^1_1\)。

### 定理 14.1.3 (Kjos-Hanssen, Nies, Stephan and Yu [68]). \(\Pi^1_1\)-Kurtz 随机性 \(\subset \Sigma^1_1\)-Kurtz 随机性 \(= \Delta^1_1\)-Kurtz 随机性。

证明. 显然 \(\Pi^1_1\)-Kurtz 随机性 \(\subseteq \Sigma^1_1\)-Kurtz 随机性 \(\subseteq \Delta^1_1\)-Kurtz 随机性。我们表明第一个包含是真包含。令

\(R(\langle e, n \rangle, z) \Leftrightarrow n \in \emptyset \wedge \Phi_e^\emptyset \in \Sigma^1_1 \wedge \exists z \in \Phi_e^\emptyset \wedge\)
\((\mu(A_\sigma) > 1 - 2^{-(e,n)}).\)

根据命题 13.16.1，\(R\) 是 \(\Pi^1_1\)，并且根据定理 4.2.1，存在一个 \(\Pi^1_1\)-函数 \(f: \omega \to 2^{<\omega}\) 一致化 \(R\)。令

\(C = \{y \mid (\forall m)(f(m) \downarrow \to y \in A_{f(m)})\}.\)

那么 \(C\) 是一个闭的 \(\Sigma^1_1\)-集合，且 \(\mu(C) \ge 2^{-1}\)。注意，如果 \(z_1 \in \Sigma^1_1 \cap \text{HYP}\) 且对于某个 \(p\) 有 \(\mu(A_{z_1}) > p\)，那么存在一个有限的 \(z \le z_1\) 在 \(\Sigma^1_1 \cap \text{HYP}\) 中，使得 \(\mu(A_z) > p\)。根据命题 14.1.2，\(C\) 中的每个实数都是 \(\Delta^1_1\)-Kurtz 随机的。由于 \(C\) 是闭集且是 \(\Sigma^1_1\)，它可以由一个 \(\Sigma^1_1\)-树表示。根据定理 11.1.2，存在一个 \(x \in C\) 使得 \(x \equiv_h \emptyset\)。令 \(e\) 和 \(n \in \emptyset'\) 使得 \(x = \Phi_e^{H_n^\emptyset}\)。那么

\(z \in \{x\} \Leftrightarrow (\exists y \le_P x)(y \in \{0\} \Leftrightarrow x = \Phi_e^{H_n^\emptyset}).\)

换句话说，\(x\) 是一个 \(\Pi^1_1\)-单点，因此不是 \(\Pi^1_1\)-Kurtz 随机的。

我们现在表明每个 \(\Delta^1_1\)-Kurtz 随机实数都是 \(\Sigma^1_1\)-Kurtz 随机的。令 \(A\) 成为一个测度为 1 的 \(\Pi^1_1\)-开集。定义 \(X = \{ \sigma \in 2^{<\omega} (\forall y)(\forall \sigma \to y \in A) \}\)。那么 \(x\) 是一个编码 \(A\) 的 \(\Pi^1_1\)-实数（即 \(y \in A\) 当且仅当存在一个 \(\sigma \in x\) 使得 \(y \in A_\sigma\)）。因此存在一个递归函数 \(f : 2^{<\omega} \to \omega\)，使得 \(\sigma \in x\) 当且仅当 \(f(\sigma) \in \emptyset\)。定义一个 \(\Pi^1_1\)-关系 \(R \subseteq \omega \times \omega\)，使得 \((k, n) \in R\) 当且仅当 \(n \in \emptyset\) 且 \(\mu(\bigcup \{ \sigma \mid \exists m \in \emptyset_n)(f(\sigma) = m) \}) > 1 - \frac{1}{k}\)。显然 \(R\) 是一个可以由 \(\Pi^1_1\)-函数 \(f\) 一致化的 \(\Pi^1_1\)-关系。由于 \(\mu(A) = 1\)，\(f\) 是一个全函数。因此 \(f\) 的值域被一个记号 \(n \in \emptyset\) 所界定。定义 \(B = \{ y \mid (\exists \sigma)(y > \sigma \land f(\sigma) \in \emptyset_n) \}\)。那么 \(B \subseteq A\) 是一个测度为 1 的 \(\Delta^1_1\)-开集。由此可见，每个 \(\Pi^1_1\)-开余零集都有一个 \(\Delta^1_1\)-开余零子集。故 \(\Sigma^1_1\)-Kurtz 随机性 \(= \Delta^1_1\)-Kurtz 随机性。

以下结果阐明了 \(\Delta^1_1\) 和 \(\Pi^1_1\)-Kurtz 随机性之间的联系。

### 命题 14.1.4. 如果 \(\omega_1^x = \omega_1^{CK}\)，那么 \(x\) 是 \(\Pi^1_1\)-Kurtz 随机的，当且仅当 \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的。

证明. 假设 \(\omega_1^x = \omega_1^{CK}\) 且 \(x\) 是 \(\Delta^1_1\)-Kurtz 随机的。如果 \(A\) 是一个 \(\Pi^1_1\)-闭零集，使得 \(x \in A\)，那么根据 Spector-Gandy 定理 3.7.3，存在一个算术公式 \(\varphi(z, y)\)，使得公式 \((\exists z \in \text{HYP})\varphi(z, y)\) 定义 \(A\)。由于 \(\omega_1^x = \omega_1^{CK}\)，存在一个递归序数 \(\beta\)，使得

\(x \in B = \{ y \mid \exists \beta(\omega_1^{CK}, y) = (\exists \beta 2^\beta)(\varphi(x^\beta, y) \subseteq A \}.\)
