

引理 7.1.5. 存在一棵完美树 \( T_1 \subseteq T_0 \)，使得 \( T_1 \le_T T_0 \) 且 \( F \) 在 \( [T_1] \) 上要么是单射，要么是常数。

证明. 如果存在 \( \sigma \in T_0 \) 使得对所有 \( x, y \in [T_0] \cap [\sigma] \) 都有 \( \Phi^\sigma_{e_0}(x) = \Phi^\sigma_{e_0}(y) \)，则令 \( T_1 = T_0 \cap \{ \tau \in 2^{<\omega} \mid \tau \supset \sigma \} \)。显然 \( F \) 在 \( [T_1] \) 上是常数。否则，\( T_0 \)-递归地找到一棵完美子树 \( T_1 \subseteq T_0 \)，使得 \( F \) 在 \( [T_1] \) 上是单射。\(\square\)

根据引理 7.1.5，我们可以假设 \( F \) 在 \( T_0 \) 上是单射。令

```
\( S_0 = \{ \tau \in 2^{<\omega} \mid (\exists \sigma \in T_0)(\forall n \le |\tau|)(\tau(n) = \Phi^\sigma_{e_0}(n)) \} \)。
```

那么 \( S_0 \) 是一棵 \( T_0 \)-递归的完美树，使得 \( \Phi_{e_0} \) 是从 \( [T_0] \) 到 \( [S_0] \) 的同胚映射。

由于 \( T_0 \) 是完美的，令 \( p : 2^{<\omega} \to T_0 \) 为一个保序的、\( T_0 \)-递归的双射。那么 \( p \) 可视为从 \( 2^\omega \) 到 \( [T_0] \) 的同胚映射。令 \( \pi : 2^{<\omega} \to 2^{<\omega} \) 为一个递归函数，使得对任意 \( \sigma \) 和 \( i < 2 \)，若 \( \sigma^\frown i \neq \emptyset \) 且存在某个 \( j < |\sigma| \) 使得 \( \sigma(j) = 1 \)，则 \( p(\sigma^\frown i) = p(\sigma)^\frown i \)；否则 \( \pi(\sigma^\frown i) = \sigma^\frown (1-i) \)。通过令 \( \pi(\alpha) = (\bigcup_n \pi(\alpha \upharpoonright n)) \)，\( \pi \) 可视为从 \( 2^\omega \) 到 \( 2^\omega \) 的同胚映射。令

```
\( p_0 = p \circ \pi \circ p^{-1} \)。
```

那么 \( p_0 \) 是从 \( T_0 \) 到 \( T_0 \) 的同胚映射。我们将验证以下引理留给读者。

引理 7.1.6. 对任意 \( \sigma \)，\( \{\pi^{(n)}(\alpha)\}_{n \in 2^{<\omega}} \) 是 \( 2^{|\sigma|} \) 的一个排列。

令 \( p_1 = F \circ p_0 \circ F^{-1} \) 为从 \( [S_0] \) 到 \( [S_0] \) 的同胚映射，并固定一个 \( x_0 \in [T_0] \)。由于 \( T_0 \) 是一致指示的，存在一对 \( (i_0, j_0) \) 使得对任意 \( n \)，\( p_1^{(n)}(x_0) \equiv p_1^{(n+1)}(x_0) \) 通过 \( (i_0, j_0) \)。那么 \( F(p_0^{(n)}(x_0)) \equiv F(p_0^{(n+1)}(x_0)) \) 通过 \( (i_1, j_1) = \ell((i_0, j_0)) \)。注意对任意 \( n \)，\( F(p_0^{(n)}(x_0)) = p_1^{(n)}(F(x_0)) \)。因此实数 \( \Phi_{e_0}^{p}(p_1^{(n)}(F(x_0))) \) 在 \( p_1^{(n)}(x_0) = F(x_0) \) 中是递归的。

给定一棵完美树 \( T \) 和一个数 \( n \)，我们说一棵有限树 \( S \subseteq T \) 对 \( T \) 的 \( 2^n \) 副本进行编码，如果

- \( S \) 同构于 \( 2^n \);
- 对任意 \( \tau \in T \setminus S \)，存在一个终端节点 \( \sigma \in S \) 使得 \( \tau \supset \sigma \)。

引理 7.1.7. \( S_0 \) 在 \( F(x_0) \) 中是递归的。

证明. 注意我们可以将 \( F : [T_0] \to [S_0] \) 视为一个同胚映射。因此对任意 \( \sigma \)，存在一个 \( m \) 使得 \( p^{-1}(F^{-1}((F(x_0) \upharpoonright m))) \) 的长度为 \( 2^{|\sigma|} \)。根据引理 7.1.6，\( \{\pi^{(n)}(p^{-1}(F^{-1}((F(x_0) \upharpoonright m))))\}_{n \in 2^{<\omega}} \) 是 \( 2^{|\sigma|} \) 的一个排列。由于 \( F \) 和 \( p \) 都是同胚映射，有限树

```
\( S_0^{[\sigma]} = \{ \tau \mid (\exists n < 2^{|\sigma|})(\tau \le p_1^{(n)}(F(x_0) \upharpoonright m)) \} \)。
```

对 \( S_0 \) 的 \( 2^{|\sigma|} \) 副本进行编码。

因此 \( \sigma \in S_0 \) 当且仅当 \( \sigma \in S_0^{[\sigma]} \)。显然 \( S_0^{[\sigma]} \) 可以从 \( \{p_1^{(n)}(F(x_0))\}_{n \in 2^{<\omega}} \) 中有效计算得到。故 \( S_0 \le_T F(x_0) \)。\(\square\)

这表明 \( S_0 \) 是一棵指示树。那么存在一个 \( x_1 \in [S_0] \) 使得 \( T_0 \oplus S_0 \le_T x_1 \)。由于 \( \Phi_{e_0} \) 是从 \( T_0 \) 到 \( S_0 \) 的同胚映射，不难看出唯一的实数 \( y \in [T_0] \) 使得 \( \Phi_{e_0}^y = x_1 \) 在 \( x_1 \) 中是递归的。换句话说，\( F(y) = x_1 \ge_T y \)，这产生了一个矛盾。

### 7.1.2 练习

练习 7.1.1. 证明引理 7.1.6。

## 7.2 一致度不变函数上的马丁猜想

本节讨论的结果归功于 Steel [159]。

引理 7.2.1. 假设 ZF + AD + DC。那么 \( \le_M \) 是在一致度不变且递增的函数集合上的一个线性序。

证明. 假设 \( F \) 和 \( G \) 是通过 \( t \) 在锥 \( \{x \mid x \ge_T z_0\} \) 上的一致度不变递增函数。定义集合 \( A \subseteq \omega^\omega \)，使得 \( x_0 \oplus x_1 \in A \) 当且仅当要么 \( x_1^i \notin 2^\omega \)，要么

- \( x_0^i \in 2^\omega \);
- \( \Phi_{e_0}^{x_0^i} = x_1^i\)，其中 \( x_0(0) = \langle e_0, n_0 \rangle\)，且
- 要么 \( \Phi_{e_1}^{x_1^i} \notin x_0^i \)，要么 \( n_0 \in F(x_0^i) \leftrightarrow n_1 \notin G(x_1^i) \)，其中 \( x_1(0) = \langle e_1, n_1 \rangle\)。

考虑由 I 和 II 在 \( A \) 上进行的两人博弈 \( \mathcal{G}_A \)，I 的第一步走 \( \langle e_0, n_0 \rangle \)。假设 I 对 \( \mathcal{G}_A \) 有一个获胜策略 \( \hat{\sigma} \)。固定一个实数 \( y \ge_T \hat{\sigma} \oplus z_0 \oplus t \)。根据相对于 \( y \) 的递归定理，对任意数 \( m \)，存在一个 \( e_1^m \) 使得 \( \Phi_{e_1^m} = (\delta(\overline{x_1^m})) \)，其中 \( x_1^m = (\langle e_1^m, m \rangle)^\frown y \)。注意函数 \( m \mapsto e_1^m \) 是递归的。令 \( x_0^m = \delta(\overline{x_1^m}) \) 和 \( x_0^m(0) = \langle e_0^m, n_0^m \rangle \)。注意函数 \( m \mapsto \langle e_0^m, n_0^m \rangle \) 是 \( y \)-递归的（实际上是一个常函数）。由于 \( \hat{\sigma} \) 是 I 的获胜策略，\( \Phi_{e_0^m}^{x_0^m} = y \) 且

\( n_0^m \in F(x_0^m) \leftrightarrow m \notin G(x_1^m) = G(y) \)。

注意 \( x_1^m \equiv_T y \) 通过 \( \langle e_0^m, e_1^m \rangle \)，因此我们有 \( F(x_0^m) \equiv_T F(y) \) 通过 \( \langle e_0^m, e_1^m \rangle = (i_0^m, i_1^m) \)。由于 \( F(y) \ge_T y \)，\( t \le_T y \) 且 \( m \mapsto \langle e_0^m, e_1^m \rangle \) 是 \( y \)-递归的，函数 \( m \mapsto (i_0^m, i_1^m) \) 是 \( F(y) \)-递归的。那么对任意 \( m \)，我们可以 \( F(y) \)-递归地找到 \( n_0^m \) 和 \( i_1^m \) 使得 \( \Phi_{i_1^m}^{F(y)}(n_0^m) = F(x_0^m)(n_0^m) = 1 - G(y)(m) \)。故 \( G(y) \le_T F(y) \)，从而 \( G \le_M F \)。

如果 II 有一个获胜策略，则通过类似的论证可以证明 \( F \le_M G \)。

给定 \( x \) 和 \( y \)，我们说 \( x \equiv_M y \) 通过 \( (e_0, e_1) \)，如果存在两个递归函数 \( \Phi_{e_0} \) 和 \( \Phi_{e_1} \) 使得对任意 \( n \)，

- \( n \in y \Leftrightarrow \Phi_{e_0}(n) \downarrow \in x \); 且
- \( n \in x \Leftrightarrow \Phi_{e_1}(n) \downarrow \in y \)。

引理 7.2.2. 假设 ZF+AD+DC。如果 \( F \) 和 \( G \) 是通过 \( t \) 的一致度不变递增函数且 \( F <_M G \)，那么 \( F' \le_M G \)。

证明. 假设 \( F <_M G \) 在锥 \([x \mid x \ge_T z_0]\) 上，但 \( F' \not\le_M G \)。令 \( p : 2^{<\omega} \to \omega \) 为一个递归双射，并对任意 \( x \)，令 \( G_1(x) = y \)，其中

\( y = \{n \mid (\forall m)(p(G(x) \mid m) \neq n)\} \)。

那么对每个 \( x \)，\( G_1(x) \equiv_T G(x) \)。而且，由于 \( G \) 是一致度不变的，\( G_1 \) 也是。

我们应用与引理 7.2.1 中相同的方法。定义 \( A \subseteq \omega^\omega \)，使得 \( x_0 \oplus x_1 \in A \) 当且仅当要么 \( x_1^t \notin 2^\omega \)，要么

- \( x_0^t \in 2^\omega \);
- \( \Phi_{e_1}^{x_0^t} = x_1^t \)，其中 \( x_0(0) = \langle e_0, n_0 \rangle\)，且
- 要么 \( \Phi_{e_1}^{x_1^t} \neq x_0^t \)，要么 \( n_0 \in F'(x_0^t) \Leftrightarrow n_1 \notin G_1(x_1^t) \)，其中 \( x_1(0) = \langle e_1, n_1 \rangle\)。

两名玩家 I 和 II 进行博弈 \( \mathcal{G}_A \)。如同在引理 7.2.1 中，如果 II 对 \( \mathcal{G}_A \) 有一个获胜策略，那么 \( F' \le_M G_1 \)，这与假设矛盾。

因此 I 对 \( \mathcal{G}_A \) 有一个获胜策略 \( \vartheta \)。固定 \( y \ge_T \vartheta \oplus z_0 \oplus t \)。根据相对于 \( y \) 的递归定理，对每个 \( m \) 存在一个 \( e_1^m \) 使得 \( \Phi_{e_1^m} = (\delta(x_1^m))' \)，其中 \( x_1^m = (e_1^m, m)^\frown y \)。注意函数 \( m \mapsto e_1^m \) 是递归的。令 \( x_0^m = \delta(x_1^m) \) 和 \( x_0^m(0) = \langle e_0^m, n_0^m \rangle \)。函数 \( m \mapsto (e_0^m, n_0^m) \) 是 \( y \)-递归的。由于 \( \vartheta \) 是 I 的获胜策略，\( \Phi_{e_0^m}^{x_1^m} = y \) 且

\( n_0^m \in F'(x_0^m) \Leftrightarrow m \notin G_1(x_1^m) = G_1(y) \)。

注意 \( x_0^m \equiv_T y \) 通过 \( (e_0^m, e_1^m) \)。那么我们有 \( F(x_0^m) \equiv_T F(y) \) 通过 \( t(e_0^m, e_1^m) = (i_0^m, i_1^m) \)。由于 \( t \le_T y \) 且 \( m \mapsto (e_0^m, e_1^m) \) 是 \( y \)-递归的，函数 \( m \mapsto (i_0^m, i_1^m) \) 也是 \( y \)-递归的。因此存在一个 \( y \)-递归函数 \( m \mapsto (j_0^m, j_1^m) \) 使得 \( F'(x_0^m) \equiv_T F(y) \) 通过 \( (j_0^m, j_1^m) \)。于是对任意 \( m \)，可以 \( y \)-递归地找到 \( x_0^m \) 和一个 \( j_1^m \) 使得

\( F'(y)(\Phi_{j_1^m}(n_0^m)) = F'(x_0^m)(n_0^m) = 1 - G_1(y)(m) \)。

由于 \( F(y) \ge_T y \)，集合 \( E_1 = \{m \mid F'(y)(\Phi_{j_1^m}(n_0^m)) = 1\} \) 是无限的且是 \( F(y) \)-可枚举的。令 \( E_2 \subseteq E_1 \) 为无限的 \( F(y) \)-递归集合。那么对任意 \( m \in E_2 \)，存在一个 \( n_m \) 使得 \( p^{-1}(m) = G_1(y) \downarrow n_m \)。故 \( G(y) \le_T F(y) \)，从而 \( G \le_M F \)，这与假设矛盾。

我们得出结论 \( F' \le_M G \)。

