

- 1. 每个在锥上不递增的度不变函数在锥上是常数；
- 2. \(\le_M\) 对在锥上递增的度不变函数进行良序。而且，如果 \(F\) 的 \(\le_M\)-阶是 \(\alpha\)，则 \(F'\) 的 \(\le_M\)-阶是 \(\alpha + 1\)，其中 \(F'(x) = (F(x))'\)，即 \(F(x)\) 的图灵跳跃。

马丁猜想是递归理论中最深刻的猜想之一。基本上它说，唯一的“自然不可解问题”是停机问题。我们将在第7章中详细讨论这个话题。

## 6.6.6 练习

- 练习 6.6.2 (Blass [7])。证明对于任何超算术实数 \(x\)，存在一个 \(\Pi^0_1\)-集 \(A\)，使得 \(\Pi\) 对 \(G_A\) 有获胜策略，但没有在 \(x\) 中递归的获胜策略。

- 练习 6.6.3。假设 \(A\) 是一个 \(\Pi^1_1\)-集，使得对于任何图灵度 \(\mathbf{x}\)，\(\mathbf{x} \cap A \neq \emptyset\)。那么存在一个指示树 \(T\) 使得 \([T] \subseteq A\)。

- 练习 6.6.4 (Blass [7])。证明存在一个 \(\Pi^0_1\)-集 \(A\)，使得 \(\Pi\) 有获胜策略，但对 \(G_A\) 没有超算术获胜策略。

- 练习 6.6.5。证明存在一个图灵度 \(\mathbf{a}\) 使得
  \((\mathscr{P}(\le \mathbf{a}), \le) \equiv (\mathscr{P}(\le \mathbf{b}), \le)\)
  对于任何图灵度 \(\mathbf{b} \ge \mathbf{a}\)，其中 \(\mathscr{P}(\le \mathbf{a}) = \{ \mathbf{c} \mid \mathbf{c} \le \mathbf{a} \}\)。

- 练习 6.6.6。假设 \(\mathbf{b} \ge \mathbf{a}\)，ZF + PD。证明存在一个图灵度 \(\mathbf{a}\) 使得
  \((\mathscr{P}(\ge \mathbf{a}), \le) \equiv (\mathscr{P}(\ge \mathbf{b}), \le)\) 对于任何图灵度 \(\mathbf{b} \ge \mathbf{a}\)，其中 \(\mathscr{P}(\ge \mathbf{a}) = \{ \mathbf{c} \mid \mathbf{c} \ge \mathbf{a} \}\)。

- 练习 6.6.7 (Jockusch and Soare [59])。证明 \((\mathscr{A}, \le) \not\equiv (\mathscr{P}, \le)\)，其中 \(\mathscr{A}\) 是算术集的图灵度集合。

- 练习 6.6.8。假设 ZFC。证明存在一个函数序列 \(\{f_n\}_{n < \omega}\) 使得对所有 \(n\) 都有 \(f_{n+1} \le_M f_n\)。

- 练习 6.6.9 (Simpson [138])。假设 ZF + \(\Pi^1_1\)-确定性。证明存在一个 \(x\) 使得对于任何 \(y \ge x\)，\(y\) 的超度是最小覆盖。

- *练习 6.6.10 (Harrington and Kechris [46])。设 \(P \subseteq 2^\omega\) 是一个 \(\Pi^0_1\)-集，关于超算术集的图灵度是终沓的，即，对于任何 \(x \in \text{HYP}\) 存在 \(y \in P\) 使得 \(y \ge_T x\)。证明任何 \(x \ge_T 0\) 都与任何 \(y \in P\) 图灵等价。*

## 7 跳算子分类

图灵跳算子 \(x \mapsto x'\) 是度不变的，即，如果 \(x \equiv_T y\) 则 \(x' \equiv_T y'\)。度不变性是该算子的一个基本性质，它促使引入了马丁猜想（§ 6.6.5）。在本章中，我们讨论一个更强的性质，称为 _均匀度不变性_，并给出满足该性质的函数分类。

### 7.1 均匀度不变函数

**定义 7.1.1。**
- 如果 \(e = (e_0, e_1)\)，我们说 \(x\) 通过 \(e\) 与 \(y\) 图灵等价（\(x \equiv_T y\) via \(e\)）如果 \(x = \Phi_{e_0}^y\) 且 \(y = \Phi_{e_1}^x\)；
- 一个函数 \(F : 2^\omega \to 2^\omega\) 在以 \(z\) 为基的锥 \(C = \{x \mid x \ge_T z\}\) 上是 _均匀度不变_ 的，如果存在一个函数 \(t : \omega \to \omega\) 使得对于任何 \(x, y \ge_T z\) 且 \(x\) 通过 \(e\) 与 \(y\) 图灵等价，都有 \(F(x)\) 通过 \(t(e)\) 与 \(F(y)\) 图灵等价。

注意在上述定义中，\(t(e)\) 的值与实数 \(x, y\) 无关。

1967年，Sacks 对于 Post 问题的一般解，提出了关于存在度不变函数 \(x \mapsto W^x\) 的猜想。该猜想与马丁猜想相矛盾，因为后者断言任何这样的函数至少必须和跳算子一样强：

**猜想 7.1.2 (Sacks [119])。** _存在一个_ \(\Sigma^1_1\)_-谓词_ \(W \subseteq 2^\omega \times \omega\) _使得，如果_ \(W^x = \{n \mid W(x, n)\}\)_，则_ \(x <_T W^x < x'\) _并且对于任何_ \(y \equiv_T x\)_，_ \(W^x \equiv_T W^y\)。

1975年，Lachlan [80] 证明该猜想对均匀度不变的 \(W\) 不成立。

### 7.1.1 非递增均匀度不变函数

均匀度不变函数在 ZF + DC + AD 下表现良好。下面的定理表明，一个均匀度不变函数要么在锥上是常数，要么在锥上是递增的。

**定理 7.1.3 (Slaman and Steel [142])。** _假设_ ZF + DC + AD_。如果 F 是均匀度不变的且在锥上不递增，则 F 在锥上是常数。_

我们将定理 7.1.3 的证明分解为一系列引理。设 \(F\) 是通过 \(\leq a\) 均匀度不变的，且在锥上不递增。

**引理 7.1.4。** _假设_ ZF+DC+AD_。如果 F 是均匀度不变的且在锥上非递增，则在锥上 \(F(x) <_T x$。_

证明。假设 \(F\) 是均匀度不变的且在锥上不递增。那么集合 \(\{x \mid F(x) \not\ge_T x\}\) 在图灵度中是终沓的。根据命题 6.6.5，存在一个指示树 \(T\) 使得 \(F\) 在 \(T\) 上通过一个函数 \(\iota : \omega \to \omega\) 均匀度不变，并且对于任何 \(x \in [T]\)，\(F(x) \not\ge_T x\)。

给定 \(x\)，令 \(x^\iota(i) = 2(x_i + 1)\) 对于 \(i < \omega\)。设 \(A \subseteq \omega^\omega\) 使得 \(x = x_0 \oplus x_1 \in A\) 当且仅当以下条件之一成立：\(x_1^\iota \not\ge_T 2^\omega$ 或
- \(x_0^\iota \in 2^\omega\)；
- 对某些 \(e, n < \omega\)，\(x_0(i) = \langle e, n \rangle\)；
- 要么 \(x_0 \not\le_T x_1$ 或 \(F(x_0^\iota)(n) = 0 \leftrightarrow x_1(x_1(0)) \neq 0$，并且
- \(x_0^\iota \in [T] \wedge \Phi_e^{x_0^\iota} = x_1$。

考虑由 I 和 II 进行的双人博弈 \(\mathcal{G}_A$，两者像往常一样交替选择数字。根据 AD，I 或 II 对 \(\mathcal{G}_A$ 拥有获胜策略。假设 I 拥有一个获胜策略 \(\delta$。我们将证明在 \(T \oplus \delta$ 之上的锥上 \(x \le_T F(x)$，这将导致矛盾。

令 \(z_0 \ge_T T \oplus \delta$ 且对于 \(m < \omega\)，\(x_1^m = m \frown z_0$。令 \(x_0^m$ 为 I 在 \([T]$ 中作为对 II 下 \(x_1^m$ 的回应而下出的实数，即 \(\delta(x_1^m) = \langle e_0, n_0 \rangle \frown x_0^m$，其中 \(\langle e_0, n_0 \rangle$ 编码了数对 \(e_0, n_0$，且 \(\delta(0) = \langle e_0, n_0 \rangle$ 是 \(\delta$ 规定的第一步。由于 I 获胜，对每个 \(m\) 都有 \(x^m = x_0^m \oplus x_1^m \in A$。因为 \(x_1^m \ge_T \delta$，所以 \(x_1^m \ge_T x_0^m$。于是对每个 \(m\)，
\(F(x_0^m)^+(n_0) = 0 \leftrightarrow x_1^m(m) = 1.\)

由于 \(\Phi_{e_0}^{(x_0^m)^+} = x_1^m$ 且 \(x_1^m = m \frown z_0$，存在一个 \(i$ 使得对每个 \(m\) 都有 \(\Phi_i^{(x_0^m)^+} = (x_0^{m+1})^+$。类似地，存在一个 \(j$ 使得对每个 \(m\) 都有 \(\Phi_j^{(x_0^m)^+} = (x_0^m)^+$。因此 \((x_0^m)^+ \equiv_T (x_0^{m+1})^+$ 通过 \(\langle i, j \rangle$，于是 \(F((x_0^m)^+) \equiv_T F((x_0^{m+1})^+)$ 通过 \(t(i, j) = \langle i', j' \rangle$。由于 \(F$ 是度不变的且 \(z_0 \equiv_T x_0^m \equiv_T (x_0^m)^+$，存在某个 \(k$ 使得 \(\Phi_k^{(x_0^m)} = F((x_0^m)^+)$。令 \(l_m = F((x_0^m)^+)(n_0)$。注意 \(F((x_0^m)^+) = \Phi_k^{F(z_0)}$ 且 \(F((x_0^{m+1})^+) = \Phi_k^{F((x_0^m)^+)}$。所以 \(\{l_m\}_{m \in \omega}$ 是 \(F(z_0)$-递归的。注意 \(z_0(m) = x_1^{m+1}(m+1) = 1 - l_{m+1}$。因此 \(z_0 \le_T F(z_0)$，矛盾。

因此 II 拥有一个获胜策略 \(\tilde{\tau}$。我们将证明在 \(T \oplus \tilde{\tau}$ 之上的锥上 \(F(x) <_T x$。固定一个实数 \(x_0 \in [T]$ 使得 \(x_0 \ge_T T \oplus \tilde{\tau}$。根据相对于 \(x_0$ 的递归定理，存在一个 \(e_0$ 使得对每个 \(n, m$ 都有 \(\tilde{\tau}((e_0, n)^\frown x_0)(m) = \Phi_{e_0}^{e_0}(\langle n, m \rangle)$。对每个 \(n$，令 \(x_1^n = \tilde{\tau}((e_0, n)^\frown x_0)$。由于 II 获胜，必有 \(x_0 \le_T x_1^n$ 且 \(F(x_0^n)(n) = x_1^n(x_1^n(0))$。于是
\(F(x_0^n)(n) = x_1^n(x_1^n(0)) = \Phi_{e_0}^{e_0}(\langle n, x_0^n(e_0(n, 0)) \rangle)\)
因此 \(F(x_0) \le_T x_0$。由于 \(F$ 是度不变的，我们得出在锥上 \(F(x) <_T x$。

根据引理 7.1.4，固定一个 \(x_0$ 使得在锥 \(\{x \mid x \ge_T x_0\}\) 上 \(F(x) <_T x$。那么存在一个 \(e_0$ 使得集合 \(C = \{x \mid \Phi_{e_0}^x = F(x) \wedge x \ge_T x_0\}\) 是终沓的。根据命题 6.6.5，存在一个完美树 \(T_0$ 和一个数 \(i$ 使得 \([T_0] \subseteq C$ 并且对于每个 \(x \in [T_0]$ 都有 \(T_0 = \Phi_i^x$。

