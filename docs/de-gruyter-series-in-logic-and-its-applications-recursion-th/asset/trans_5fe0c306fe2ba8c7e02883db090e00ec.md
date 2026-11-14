

## 14.3.3 随机实数的超度

由推论 14.2.6 可知，$\Delta_1^1$-随机实数集合的超度包含以 0 为基的超度锥。这引出了一个自然问题：$\Delta_1^1$-随机实数的超度是否向上封闭。

**命题 14.3.5.** 如果 $x$ 是 $\Delta_1^1$-随机且 $\omega_1^x = \omega_1^{CK}$，则存在 $y \ge_h x$，使得没有 $z \equiv_h y$ 是 $\Delta_1^1$-随机。

**证明.** 假设 $x$ 是 $\Delta_1^1$-随机且 $\omega_1^x = \omega_1^{CK}$。令

$F(x) = \{ y \mid y \ge_T x \land (\forall f \le_T y)(\forall g \le_h x)(g < f) \}.$

则 $F(x)$ 是 $\Sigma_1^x(x)$。由于 $\emptyset^x \in F(x)$，$F(x)$ 非空。根据甘地基定理并相对化到 $x$，存在 $y \in F(x)$ 使得 $\omega_1^y = \omega_1^x = \omega_1^{CK}$。根据推论 14.3.2 和命题 14.3.4，没有 $z \equiv_h y$ 是 $\Delta_1^1$-随机。

另一方面，$\Pi_1^1$-随机实数的超度是向下封闭的。

**引理 14.3.6.** 如果 $x$ 是 $\Pi_1^1$-随机且 $y \le_h x$，则存在递归序数 $\gamma$ 使得 $y \le_T x \oplus \emptyset^{(\gamma)}$。

**证明.** 由于 $x$ 是 $\Pi_1^1$-随机，我们有 $\omega_1^x = \omega_1^{CK}$。令 $y \le_h x$。则存在公式 $\varphi(\dot{n}, \dot{x})$，其秩至多为 $\beta_0 < \omega_1^{CK}$，使得

$n \in y \Leftrightarrow \mathfrak{A}(\omega_1^{CK}, x) \vDash \varphi(\dot{n}, \dot{x})$.

根据引理 13.1.11，存在递归序数 $\beta > \beta_0$ 使得

$A_{\beta_0} = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ has rank at most } \beta_0 \land \mu(\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi \}) > 0 \}$

在 $\emptyset^{(\beta)}$ 中是递归的。根据引理 13.1.10，存在递归序数 $\beta_1 \ge \beta$ 使得对于任意数 $i$ 和秩为 $\beta$ 的公式 $\psi$，存在秩至多为 $\beta_1$ 的公式 $\psi'$，使得 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi' \}$ 是 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$ 的一个 $\Pi_1^0(\emptyset^{(\beta)})$-子集，且度量差小于 $2^{-i}$。注意，从 $\beta_0$ 搜索 $\beta_1$ 的过程在 $L_{\omega_1^x}$ 中是有效的。这样，在 $L_{\omega_1^x}$ 中得到一个序数的 $\Delta_1$-序列 $\beta_0 < \beta_1 < \cdots$。令 $\gamma = \bigcup_{i < \omega} \beta_i$。则对于任意 $\beta < \gamma$，

- (i) $A_\beta = \{ \ulcorner \varphi \urcorner \mid \varphi \text{ has rank at most } \beta \land \mu(\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi \}) > 0 \}$

在 $\emptyset^{(\beta)}$ 中是递归的，且

- (ii) 对于任意数 $i$ 和秩为 $\beta$ 的公式 $\psi$，存在秩小于 $\gamma$ 的公式 $\psi'$，使得 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi' \}$ 是 $\{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$ 的一个 $\Pi_1^0(\emptyset^{(\beta)})$-子集（对某个 $\beta' < \gamma$），且度量差小于 $2^{-i}$。

注意，对于任意带秩的公式 $\psi$，如果 $x \in P_\psi = \{ z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi \}$，则 $P_\psi$ 具有正度量。

由于 \( x \) 是 \( \Delta^1_1 \)-支配的，存在一个超算术函数 \( f : \omega \to \omega \) 使得对于任意 \( e \) 和 \( n \in \omega \) 且 \( |n| < \gamma \)，如果 \( \Phi_e^{H_e} \) 计算出一棵树 \( T_{e,n} \)，且 \( x \notin [T_{e,n}] \)，则 \( f(n,e) \notin T_{e,n} \)。

现在在 \( x \oplus 0^{(\beta)} \oplus f \) 中递归地搜索一个秩小于 \( \gamma \) 的公式 \( \psi_0 \)，使得 \( S_0 = \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi_0\} \) 包含 \( x \)，并且是 \( \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi(z, 0)\} \) 或 \( \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \neg \varphi(z, 0)\} \) 的一个闭子集。

由于 \( x \) 是 \( \Pi^1_1 \)-随机，根据 (ii) 存在这样的 \( \psi_0 \)。注意，需要 \( x \oplus 0^{(\beta)} \oplus f \) 来判定 \( x \in S_0 \)。归纳地，对于每个 \( n \)，在 \( x \oplus 0^{(\beta)} \oplus f \) 中递归地搜索一个秩小于 \( \gamma \) 的公式 \( \psi_{n+1} \)，使得 \( S_{n+1} = \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \psi_{n+1}\} \) 包含 \( x \)，具有正度量，并且是 \( S_n \cap \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \varphi(z, n+1)\} \) 或 \( S_n \cap \{z \mid \mathfrak{A}(\omega_1^{CK}, z) \vDash \neg \varphi(z, n+1)\} \) 的一个闭子集。

由于 \( x \) 是 \( \Pi^1_1 \)-随机，根据 (ii)，这样的 \( \psi_{n+1} \) 存在。这意味着 \( y \not\le_T x \oplus 0^{(\beta)} \oplus f \)。

由于 \( f \) 是超算术的，存在 \( \gamma_0 < \omega_1^{CK} \) 使得 \( f \le_T 0^{(\gamma_0)} \)。不失一般性，假设 \( \gamma_0 \le \gamma$（必要时将 \( \gamma \) 替换为 \( \gamma_0 + \gamma \)）。则 \( y \not\le_T x \oplus 0^{(\gamma)} \)。\(\square\)

## **推论 14.3.7.** 如果 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \)，则存在递归序数 \( \beta \)、函数 \( f \le_T 0^{(\beta)} \) 和递归泛函 \( \Psi \)，使得对每个 \( n \)，\( y(n) = \Psi^{x \oplus 0^{(\beta)}(n)}(n)[f(n)] \)。

**证明.** 假设 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \)。根据引理 14.3.6，存在递归序数 \( \gamma \) 和递归函数 \( \Phi \)，使得对每个 \( n \)，\( y(n) = \Phi^{x \oplus 0^{(\gamma)}(n)}(n)[g(n)] \)。由于 \( x \) 是 \( \Pi^1_1 \)-支配的，存在函数 \( g \le_h x \) 使得对每个 \( n \)，\( y(n) = \Phi^{x \oplus 0^{(\gamma)}(n)}(n)[g(n)] \)。由于 \( x \) 是 \( \Pi^1_1 \)-支配的，存在超算术函数 \( h \) 使得对所有 \( n \)，\( h(n) > g(n) \)。

因此存在足够大的递归序数 \( \beta \)，使得 \( x \) 和 \( h \) 都多一归约到 \( 0^{(\beta)} \)。定义函数 \( f \le_T 0^{(\beta)} \) 和递归函数 \( \Psi \) 并不困难，使得对每个 \( n \)，\( y(n) = \Psi^{x \oplus 0^{(\beta)}(n)}(n)[f(n)] \)。\(\square\)

## **定理 14.3.8.** 如果 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \) 不是超算术的，则存在 \( \Pi^1_1 \)-随机 \( z \equiv_h y \)。

**证明.** 假设 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \le_h x \) 不是超算术的。根据推论 14.3.7，存在递归序数 \( \beta \)、非递减函数 \( f \le_T 0^{(\beta)} \) 和递归函数 \( \Psi \)，使得 \( \lim_{n \to \infty} f(n) = \infty \) 且对每个 \( n \)，

\( y(n) = \Psi^{x \oplus 0^{(\beta)}(n)}(n)[f(n)] \).

对于每个 \( u \in 2^{<\omega} \)，令

\( l(u) = \sum_{\tau \in 2^{|\tau|} \cap \text{Cl}} \left( \sum_{g \in 2^{|\tau|} \wedge \forall \rho \prec u \exists \rho' \in [u] [f(|\rho|)] \|\tau\| = \tau} 2^{-|\sigma|} \right) \)

和

\( r(u) = l(u) + \sum_{\sigma \in 2^{|\tau|} \wedge \forall \rho \prec u \exists \rho' \in [u] [f(|\rho|)] \|\tau\| = u} 2^{-|\sigma|} \),

其中 \( \tau < u \) 表示，作为字符串，\( \tau \) 在 \( u \) 的左侧。

可以将 \(\sum_{\sigma \in 2^{<\omega}} \lambda \mu[\text{ext}(\sigma) \oplus \emptyset^{(\beta)}[f(|\sigma|)]]_{r(\sigma)} 2^{-|\sigma|}\) 视为 \( \tau \) 的一个“度量”。对于每个 \( n \)，令

\( l_n = l(y \upharpoonright n) \)，且 \( r_n = r(y \upharpoonright n) \)。

则 \( l_n \le l_{n+1} \le r_{n+1} \le r_n$。由于 \( y \) 不是超算术的，不难看出 \(\lim_{n \to \infty} r_n = 0\)。因此存在唯一的

\( z = \bigcap_{n<\omega} (l_n, r_n) \)。

显然 \( z \le_T y \oplus \emptyset^{(\beta)} \)。我们留给读者验证 \( y \le_T z \oplus \emptyset^{(\beta)} \)。因此 \( z \equiv_T y \)。

假设 \( z \) 不是 \( \Delta^1_1 \)-随机。则存在递归序数 \( \gamma < \beta \) 和一个 \( \emptyset^{(\gamma)} \)-ML-测试 \( \{V_n\}_{n \in \omega} \) 使得 \( z \in \bigcap_{n<\omega} V_n \)。令

\( \tilde{V}_n = \{u \mid (\exists v)(v \text{ is the } k\text{-th string in } V_n \wedge (\exists p \in \mathbb{Q})(\exists q \in \mathbb{Q})(p < l(u) < r(u) < q \land \forall \sigma \sqsubseteq u (q - p < 2^{-|v|} - 2^{-n-k-2}))\} \).

直观地，\( \{\tilde{V}_n\}_{n<\omega} \) 是相对于度量 \( \lambda \) 的 \( \Delta^1_1 \)-Martin-Löf 测试，其中对任意 \( \sigma \in 2^{<\omega} \)，\( \lambda(\sigma) = \sum_{\tau \in C(\sigma)} 2^{-|\tau|} \)。

由于 \( z \in V_n \)，对每个 \( n \) 都有 \( y \in \tilde{V}_n \)。注意 \( \{\tilde{V}_n\}_{n<\omega} \) 是 \( \emptyset^{(\gamma+1+\beta)} \)-递归可枚举。令

\( U_n = \{\sigma \mid (\exists \tau \in \tilde{V}_n)(|\sigma| = f(|\tau|) \land \tau \oplus \emptyset^{(\gamma)}[f(|\tau|)][f(|\tau|)] \ge \tau)\} = \bigcup_{u \in \tilde{V}_n} C(u) \).

则 \( \{U_n\}_{n<\omega} \) 是 \( \emptyset^{(\gamma+1+\beta)} \)-递归可枚举 且 \( x \in \bigcap_{n<\omega} U_n \)。注意对每个 \( n \)，

\( \mu(U_n) \le \mu(V_n) + \sum_{k<\omega} 2^{-n-k-2+1} < 2^{-n} + 2^{-n} = 2^{-n+1} \).

则 \( \{U_{n+1}\}_{n<\omega} \) 是一个 \( \emptyset^{(\gamma+1+\beta)} \)-ML-测试。因此 \( x \) 不是 \( \Delta^1_1 \)-随机，矛盾。

## 14.3.4 练习

**练习 14.3.1** (Jorhth and Nies [51]). 证明 \( x \oplus y \) 是 \( \Pi^1_1 \)-随机当且仅当 \( x \) 是 \( \Pi^1_1 \)-随机且 \( y \) 是 \( \Pi^1_1(x) \)-随机。

**练习 14.3.2** (Yu [171]). 对任意 \( z \ge_h \emptyset \)，存在 \( \Delta^1_1 \)-随机 \( x \equiv_h z \)，且 \( x \) 不是 \( \Pi^1_1 \)-ML 随机。

**练习 14.3.3.** 证明如果 \( x \) 是 \( \Pi^1_1 \)-随机，则对于任何包含 \( x \) 的 \( \Sigma^1_1 \)-实数集 \( A \)，

\( \lim_{n \to \infty} \frac{\mu(A \cap [x \upharpoonright n])}{2^{-n}} = 1 \).

