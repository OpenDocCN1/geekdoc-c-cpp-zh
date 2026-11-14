

- (i) Range($h_p$) $\supseteq y_0 \cup \{\infty\}$;
- (ii) 对于任意 $m$，$f((\exists z^{>n})(\varphi(n, z^{>n}) \lor \neg \psi(n, z^{>n})) < \gamma_{m+1}$，并且对于任意 $n$ 以及 $L_{\gamma_{m+1}}$ 中的 $p_n \le p$，存在一个 $q_n \le p_n$ 且 $q_n \in L_{\gamma_{m+1}}$，使得 $q_n \Vdash (\exists z^{>n+1})(\varphi(n, z^{>n+1}) \lor \neg \psi(n, z^{>n+1}))$，且
- (iii) 对于每个 $m$，$\gamma_{m+1} = \omega \gamma_{m+1}$。

令 $\beta = \bigcup_{m < \omega} \gamma_m = \omega \beta$。则 $\beta < \alpha$。我们声称

$p \Vdash (\forall n)((\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))$。

强制关系等价于

$(\forall n)(\forall q \le p)(\exists r \le q)(q \Vdash (\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))).$

给定 $n$ 和 $q \le p$，令 $q'$ 为一个条件，使得 $t'_{q'} = t_q$ 且当 $h_q(\alpha) < \beta$ 时 $h_{q'}(\alpha) = h_q(\alpha)$，否则 $h_{q'}(\alpha) = \infty$。由 (i)，$q' \le p$ 且对于某个 $m$，$q' \in L_{\gamma_m}$。由 (ii)，存在一个条件 $r' \in L_p$ 使得 $r' \le q'$ 且

$r' \Vdash (\exists z^{\gamma_m})(\varphi(n, z^{\gamma_m}) \lor \neg \psi(n, z^{\gamma_m})).$

由 (iii)，Ret$(\omega\beta, q, q')$ 成立且

$\omega \cdot f((\exists z^{\gamma_m})(\varphi(n, z^{\gamma_m}) \lor \neg \psi(n, z^{\gamma_m}))) < \beta.$

由引理 5.4.5 和引理 5.4.6，存在一个条件 $r \le q$ 使得

$r \Vdash (\exists z^\beta)(\varphi(n, z^{\gamma_m}) \lor \neg \psi(n, z^{\gamma_m})).$

因此

$r \Vdash (\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)).$

由引理 5.4.10，

$\mathfrak{A}(\alpha, T) \Vdash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)).$

令 $y$ 满足 $y \in \dot{y}$ 当且仅当 $\mathfrak{A}(\alpha, T) \Vdash (\exists z^\beta)\varphi(n, z^\beta)$。则 $y \in \mathfrak{A}(\alpha, T)$，因此 $\mathfrak{A}(\alpha^{<\omega}, T)$ 满足 $\Delta_1^\xi$-理解公理。$\square$

总之，我们有以下结论：

## **定理 5.4.12** (Sacks [122]). 对于任何可数可接受序数 $\alpha > \omega$，存在一个实数 $x$ 使得 $\omega_1^x = \alpha$。

## **注释 5.4.13.** 在文献中，有若干个定理 5.4.12 的证明。Sacks 最初的证明采用完备集强制法，并给出了更强的结论。第二个证明由 Friedman 和 Jensen [31] 提出，通过应用 Barwise 紧致性定理 [3]。第三个证明尚未发表，由 Jensen [54] 提出，使用了一类 Lévy 折叠运算，可视为 Steel 强制的变体。

## 5.4.3 练习

- 练习 5.4.1. 证明对于任何满足 \( x \notin L_{\omega_1^x} \) 的 x，存在一个 y 使得 \( y \ge_h x \)、\( y \notin_h x \) 且 \( \omega_1^x = \omega_1^y \)。

- 练习 5.4.2. 证明 \( x \in L_{\omega_1^x} \) 当且仅当对于所有 y，\( \omega_1^y \ge \omega_1^x \) 蕴含 \( y \ge_h x \)。

- 练习 5.4.3. 令 \( \alpha_n \) 为第 n 个可接受序数。则 \( \bigcup_{n<\omega} \alpha_n \) 不是可接受的。

- 练习 5.4.4 (Chong [11]). 假设 \( y > \omega \) 是一个序数，使得 \( J_{y+1} \backslash J_y \cap 2^\omega \neq \emptyset \)。则对于任何可接受序数 \( \alpha < \gamma^+ \)，其中 \( \gamma^+ \) 是大于 y 的最小可接受序数，存在一个 x \( \in J_y \backslash J_y \) 使得 \( \omega_1^x = \alpha \)。

- 练习 5.4.5 (Jensen [54]). 假设 \( \alpha \) 是可接受序数的可数极限。则存在一个集合 \( A \subseteq \alpha \)，使得对于任何可接受的 \( \beta < \alpha \)，\(\langle L_\beta[A], \epsilon, A \cap L_\beta[A] \rangle\) 是可接受的，且 \(\langle L_\alpha[A], \epsilon, A \cap L_\beta[A] \rangle \models \text{\texttt{"$\beta$ is countable"}}\)。

- 练习 5.4.6 (Jensen [54]). 假设 \( \omega < \alpha_0 < \cdots < \alpha_n \) 是一组可数可接受序数的有限序列。证明存在一个 x，使得对于任何 \( i \le n \)，\( \alpha_i \) 是 L[x] 中第 i + 1 个可数可接受序数。

## 6 集合论

本章回顾具有递归论应用的集合论结果。其中一些结果将不作证明，以供日后参考。

### 6.1 集合论强制法

强制法的技术在第 5 章的递归论背景下讨论过。Cohen [18] 中提出的该方法的原始版本与 § 5.2 中发展的方法非常相似。这里我们遵循 Shoenfield [130] 引入的非分层强制法（关于该主题的优秀论述见 Kunen [78]）。

### 6.1.1 强制法与泛化性

令 M = (M, ∈) 为 ZFC 的一个可数传递模型，令 P = (P, ≤) 为 M 中的一个偏序。元素 p ∈ P 称为一个条件。给定两个条件 p, q ∈ P，如果 p ≤ q，则我们说 q 比 p 更强。D ⊆ P 是稠密的，如果对于任何 p ∈ P，存在 q ∈ D 使得 q ≤ p。

滤子 F ⊆ P 是一个非空集合，使得

- (∀p)(∀q)(q ≤ p ∈ P → p ∈ F);
- (∀p)(∀q)((∃r) ∈ F ∧ q ≤ r → r ∈ F ∧ r ≤ p ∧ r ≤ q).

泛化集 G ⊆ P 是一个与每个稠密集相交的滤子。一般来说，泛化集不属于 M，除非是非常特殊的偏序。如果 G ∉ M，则存在 ZFC 的一个模型 M[G] = (M[G], ∈)，使得 M ∪ {G} ⊆ M[G] 且 o(M) = o(M[G])。其定义如下。

首先，M 中的 P-名通过归纳定义：

- ∅ 是一个 P-名；
- 如果 τ ⊆ P-名集合 × P，则 τ 是一个 P-名。

我们用 M^P 表示 P-名的类。注意 M^P ⊂ M 且不是 M 的元素。假设 G 是泛化的。通过归纳定义 val(τ, G)：

- 如果 τ 不是 P-名，则 val(τ, G) = τ；
- 否则，val(τ, G) = {val(σ, G) | (σ, p) ∈ τ ∧ p ∈ G}.

令

```
M[G] = {val(τ, G) | τ ∈ M}.
```

因此，M[G] 中的每个元素 x 都有一个对应的 P-名。我们用 ẋ 表示 x 的 P-名。对于任何 a ∈ M，我们通过 a 的秩进行归纳，用 ȧ 表示 ⟨⟨ḃ, p⟩ | b ∈ a ∧ p ∈ P⟩。由于对于任何 \(a \in M\)，\(\text{val}(\tilde{a}, G) = a\)，我们有 \(M \subseteq M[G]\)。此外，\(\tilde{G} = \{(\check{p}, p) \mid p \in \mathbf{P}\}\) 是一个 \(\mathbf{P}\)-名，且 \(\text{val}(\tilde{G}, G) = G\)。因此 \(G \in M[G]\)。\(\langle M[G], \in \rangle\) 是 ZFC 的一个传递模型，且 \(o(M) = o(M[G])\)。

**定义 6.1.11.** 给定一个条件 \(p \in \mathbf{P}\) 和一个公式 \(\varphi(\tau_0, \dots, \tau_n)\)，其中 \(\tau_0, \dots, \tau_n \in M^\mathbf{P}\)，我们说 \(p\) *强制* \(\varphi(\tau_0, \dots, \tau_n)\)，或 \(p \Vdash \varphi(\tau_0, \dots, \tau_n)\)，当且仅当对于任何包含 p 的泛化集 G，\(\langle M[G], \in \rangle \models \varphi(\text{val}(\tau_0, G), \dots, \text{val}(\tau_n, G))\)。

**定理 6.1.2.** (i) 类 \(\langle p, \varphi, (\tau_0, \dots, \tau_n) \rangle \mid p \Vdash \varphi(\tau_0, \dots, \tau_n)\rangle\) 在 \(\mathfrak{M}\) 中可定义；(ii) 对于每个泛化集 G 和公式 \(\varphi(\tau_0, \dots, \tau_n)\)，其中 \(\tau_0, \dots, \tau_n \in M^\mathbf{P}\)，\(\langle M[G], \in \rangle \models \varphi(\text{val}(\tau_0, G), \dots, \text{val}(\tau_n, G)) \Leftrightarrow (\exists p \in G)(p \Vdash \varphi(\tau_0, \dots, \tau_n))\)。

定理 6.1.2 与 §5.2 中 \(\Vdash\) 的定义（见 [78]）结合起来并不令人惊讶。关于强制关系的以下事实是标准的。

**命题 6.1.3.** 对于任何公式 \(\varphi\)、条件 \(p\) 和 \(\mathbf{P}\)-名 \(\tau_0, \dots, \tau_n\)，(i) \(q \le p \land p \Vdash \varphi \implies q \Vdash \varphi\)；(ii) \(p \Vdash \varphi \land \psi\) 当且仅当 \(p \Vdash \varphi\) 且 \(p \Vdash \psi\)；(iii) \(p \Vdash \neg \varphi\) 当且仅当 \((\forall q \le p) q \not\Vdash \varphi\)；(iv) 集合 \(\{p \mid p \Vdash \neg \varphi \lor p \Vdash \varphi\}\) 是稠密的；(v) \(p \Vdash (\exists x)\varphi(x)\) 当且仅当集合 \(\{q \mid q \le p \text{ 且 } \exists \tau (q \Vdash \varphi(\tau))\}\) 是稠密的；(vi) \(p \Vdash (\exists x)\varphi(x)\) 当且仅当存在一个 \(\mathbf{P}\)-名 \(\tau \in M^\mathbf{P}\) 使得 \(p \Vdash \varphi(\tau)\)。

### 6.1.2 \(\kappa\)-链条件与 Martin 公理

给定一个偏序 \(\mathbf{P} = (\mathbf{P}, \le)\)，集合 \(A \subseteq \mathbf{P}\) 是一个 *反链*，如果对于 A 中的 \(p \neq q\)，不存在满足 \(r \le p\) 和 \(r \le q\) 的 \(r\)。\(\mathbf{P}\) 满足 \(\kappa\)-*链条件*，或 \(\kappa\)-c.c.，如果在 \(\mathfrak{M}\) 中 \(\mathbf{P}\) 的每个反链的基数小于 \(\kappa\)。特别是，\(\omega_1\)-c.c. 称为可数链条件，或 c.c.c. 链条件限制了泛化扩展中函数的可能取值。事实上，链条件被用作泛化扩展中基数保持的基本工具。例如，如果 \(\mathbf{P} = (\mathbf{P}, \le)\) 满足 c.c.c. 且 \(f : \omega \to (\omega_1)^{\mathbf{M}}\) 是某个泛化集 G 下 \(\mathbf{M}[G]\) 中的一个函数，那么对于每个 \(n < \omega\)，集合 \(A_n = \{(\alpha, \omega_1)^{\mathbf{M}} \mid (\exists p)(p \Vdash f(\check{n}) = \check{\alpha})\} \in \mathbf{M}\) 在 \(\mathfrak{M}\) 中是可数的，因此 \(\bigcup_n A_n \in \mathbf{M}\) 在 \(\mathfrak{M}\) 中也是可数的。因此 \(\mathbf{P}\) 不会折叠 \((\omega_1)^{\mathbf{M}}\)。

**引理 6.1.14.** 如果 \(\mathbf{P}\) *满足* \(\kappa\)*-链条件*，则对于任何泛化集 G，\((\kappa)^{\mathbf{M}} = (\kappa)^{\mathbf{M}[G]}\)。

**定义 6.1.5** (Martin 公理 [90]). 令 \(\kappa\) 为一个基数。\(\text{MA}_\kappa\) 断言对于任何 c.c.c. 偏序 \(\mathbf{P} = (\mathbf{P}, \le)\) 和任何 \(\kappa\)-序列的稠密集 \(\{D_\alpha\}_{\alpha < \kappa}\)，存在一个滤子 \(G \subseteq \mathbf{P}\) 与每个 \(D_\alpha\) 相交。我们用 \(\text{MA}\) 表示 \((\forall \kappa < 2^{\aleph_0})\text{MA}_\kappa\)。

