

因此 $R_a$ 是 $\Sigma^1_1(r_a)$。令 $r'_a \le_T r_a$ 成为 $\omega$ 的一个序类型为 $\alpha + 1$ 的良序。则 $x \in R_a$ 当且仅当

- (vf) $(\forall n \in O^{r_a*})(f$ 不是 $r_a^*$ 到 $O^{r_a*}$ 的嵌入) $\wedge$
- (vn) $(\exists m \in O^{r_a*})(\exists g$ 是 $(m \mid m <_{r_a} n)$ 到 $(i \mid i \prec_\omega m)$ 的初始段的同构)。

根据练习 3.6.4，上述表达式中的 $g$ 可以取为相对 $r_a \oplus [i \prec_\omega m]$ 的超算术，而后者又相对 $r_a \oplus x$ 是超算术的。因此 $R_a$ 也是 $\Pi^1_1(r_a)$，从而是 $\Delta^1_1(r_a)$。

### Lemma 3.7.8.

对于任意 $\alpha < \omega_1$，关系 $C_\alpha(x, y) \Leftrightarrow y \le_B x \wedge x \in R_a$ 是 $\Delta^1_1(r_a)$。

### Proof.

根据推论 2.2.2 和引理 3.7.7，$C_a$ 是 $\Pi^1_1(r_a)$。

我们证明 $C_a$ 是 $\Sigma^1_1(r_a)$。现在 $y \le_B x$ 当且仅当存在一个 $n \in O^{r_a}$ 使得 $y \le_T H_n^a$，且根据前一引理，后者成立当且仅当存在一个 $n \in O^{r_a*}$ 和一个 $f : [m \mid m <_{\omega^*} n] \to \omega$，使得对所有 $i <_{\omega^*} j$，$(f(i), f(j)) \in r_a$。于是 $y \le_B x$ 是 $\Sigma^1_1(r_a)$。因此 $C_a$ 是 $\Sigma^1_1(r_a)$。

### Lemma 3.7.9.

- (i) 每个 $\Pi^1_1$-实数集是 $\aleph_1$ 个博雷尔集的并。
- (ii) 每个 $\Sigma^1_1$-实数集是 $\aleph_1$ 个博雷尔集的并。

### Proof.

(i) 假设 $A \in \omega^\omega$ 是 $\Pi^1_1$。根据推论 3.7.4，存在一个算术谓词 $A(x, z)$，使得 $x \in A \Leftrightarrow (\exists z \le_B x)\Sigma(x, z)$。对任意 $\alpha < \omega_1$，令 $A_\alpha = A \cap R_\alpha$。则 $A_\alpha$ 是 $\Pi^1_1(r_\alpha)$。根据引理 3.7.8，$A_\alpha$ 也是 $\Sigma^1_1(r_\alpha)$。因此 $A_\alpha$ 是 $\Delta^1_1(r_\alpha)$，从而是博雷尔集。

(ii) 假设 $A \subseteq 2^\omega$ 是 $\Sigma^1_1$。则存在一个 $\Pi^0_2$ 集合 $B \subseteq \omega^\omega \times 2^\omega$，使得 $x \in A$ 当且仅当 $(\exists \beta)B(f, x)$。对 $\alpha < \omega_1$，令 $A_\alpha = A \cap R_\alpha$。根据引理 3.7.7，$A_\alpha$ 是 $\Sigma^1_1(r_\alpha)$。

根据甘迪基数定理 2.5.3，$x \in A$ 当且仅当 $(\exists f <_B O^{r_\alpha}) B(f, x)$。由于 $\omega_1^{f*_1} > \omega_1^r$，我们有 $x \notin r_\alpha$。将推论 2.4.10 的证明相对化到 $r_\alpha$ 得到 $O^{r_\alpha} \le_B x \oplus r_\alpha$。我们得出结论，$A_\alpha$ 是 $\Pi^1_1(r_\alpha)$，从而是 $\Delta^1_1(r_\alpha)$。

### Corollary 3.7.10 (Lusin [86]).

每个 $\Pi^1_1$-实数集是可测的。

### Proof.

遵循引理 3.7.9 的记号，对每个 $n \in \omega$ 和 $\alpha < \omega_1$，令 $D_{n, \alpha} = \{x \mid n \in O^{r_\alpha*} \wedge ([m \mid m <_{\omega^*} n, l <_{\omega^*}) \equiv r_\alpha\}$。

则 $D_{n, \alpha}$ 是 $\Sigma^1_1(r_\alpha)$。根据引理 3.7.8 的证明和练习 3.6.4，

$D_{n, \alpha} = \{x \mid n \in O^{r_\alpha} \wedge ([m \mid m <_{\omega^*} n, l <_{\omega^*}) \equiv r_\alpha\}$

且是 $\Pi^1_1(r_\alpha)$。因此 $D_{n, \alpha}$ 是博雷尔集。注意当 $\alpha \neq \beta$ 时，$D_{n, \alpha} \cap D_{n, \beta} = \emptyset$。故对任意 $n$，存在一个 $\alpha_n < \omega_1$，使得当 $\beta \geq \alpha_n$ 时 $\mu(D_{\beta, n}) = 0$。令 $\alpha_\omega < \omega_1$ 为这些 $\alpha_n$ 的一个上界。

现在假设 $A$ 是 $\Pi^1_1$。则对任意 $\alpha > \alpha_\omega$，$x \in A_\alpha$ 蕴含存在一个 $n$ 使得 $x \in D_{n, \alpha_\omega}$。换句话说，$\bigcup_{\alpha > \alpha_\omega} A_\alpha \subseteq \bigcup_n D_{n, \alpha_\omega}$。根据 $\alpha_\omega$ 的选取，\(\mu(\bigcup_{n<\omega} A_n) = 0\)。但 \(\bigcup_{n<\omega} A_n\) 是一个可测的博雷尔集。我们得出结论，\(A = \bigcup_{\alpha<\omega} A_\alpha\) 是可测的。

我们将在第 14 章计算 \(\alpha_\omega\) 的值。

### Theorem 3.7.11 (Sierpinski [135]). 每个 \(\Sigma^1_2\)-实数集是 \(\omega_1\) 个博雷尔集的并。

### Proof.

假设 \(A \subseteq 2^\omega\) 是 \(\Sigma^1_2\)。则存在一个 \(\Pi^1_1\)-集合 \(B \subseteq \omega^\omega\)，使得 \(x \in A\) 当且仅当 \((\exists f \in \omega^\omega) B(f, x)\)。根据引理 3.7.9 的 (i)，存在一个博雷尔集的 \(\omega_1\)-序列 \(\{B_\alpha\}_{\alpha<\omega_1}\)，使得 \(\bigcup_{\alpha<\omega_1} B_\alpha = B\)。则对每个 \(\alpha < \omega_1\)，\(C_\alpha = \{x \mid (\exists f \in \omega^\omega) B_\alpha(f, x)\}\) 是 \(\Sigma^1_1\)。显然 \(A = \bigcup_{\alpha<\omega_1} C_\alpha\)。通过将引理 3.7.9 的 (ii) 相对化，每个 \(C_\alpha\) 是 \(\omega_1\) 个博雷尔集的并。因此 \(A\) 是 \(\omega_1\) 个博雷尔集的并。

### Corollary 3.7.12. 每个势大于 \(\aleph_1\) 的 \(\Sigma^1_2\)-实数集都有一个完美子集。

### Proof.

根据定理 3.7.11，每个 \(\Sigma^1_2\)-实数集 \(A\) 都是 \(\aleph_1\) 个博雷尔集的并。如果 \(A\) 的势大于 \(\aleph_1\)，则其中一个博雷尔集是不可数的，因而有一个完美子集。

## 3.7.4 练习

### Exercise 3.7.1. 以下是定理 2.4.7 的另一个证明。

- (i) 证明 \(\emptyset\) 在 \(L_{\omega_1^{CK}}\) 上是 \(\Sigma_1\)-可定义的；
- (ii) 证明对任意实数 \(x\) 和 \(y\)，\(x \le_T y\) 当且仅当 \(x \in L_{\omega_1^y}[y]\)，从而 \(\emptyset \le_B y\) 当且仅当 \(\omega_1^x < \omega_1^y\)。

### Exercise 3.7.2. 证明存在一个实数序列 \(\{x_n\}_{n<\omega}\)，使得对每个 \(n\)，\(x_n \ge_T x_{n+1}^T\)。

### Exercise 3.7.3. 证明如果 \(\{x_n\}_{n<\omega}\) 是如上序列，则对每个 \(n\)，\(x_n\) 不是超算术的。

### Exercise 3.7.4. 使用 Spector–Gandy 定理（3.7.1）的第一个版本来证明定理 3.7.11。

### Exercise 3.7.5. 证明如果 \(x\) 是一个实数，使得每个非空的 \(\Pi^0_1\) 集合 \(A \subseteq \omega^\omega\) 都有一个相对 \(x\) 超算术的元素，则 \(x \ge_T \emptyset\)。

### Exercise 3.7.6. 证明集合 \(\{(x, y) \mid x_0^y > \omega_1^x\}\) 是 \(\Pi^1_1\) 但不是 \(\Sigma^1_1\)。

### Exercise 3.7.7. 假设 \(\mathsf{MA} + 2^{\aleph_0} > \aleph_1\)（参见定义 6.1.5）。证明每个 \(\Sigma^1_2\)-集合是可测的。

## 4 \(\Pi^1_1\)-集合的理论

\(\Pi^1_1\)-实数集被赋予了丰富的结构性质，包括那些从可构造宇宙 \(L\) 的角度来看最易理解的性质。本章对这类集合进行更深入的分析，以阐明这一点。

### 4.1 一个 \(\Pi^1_1\)-基数定理

### 4.1.1 \(\Pi^1_1\)-集合的树表示

回顾，给定一个 \(\Pi^1_1\)-集合 \(A \subseteq 2^\omega\)，存在一个递归谓词 \(P \subseteq 2^{<\omega} \times \omega^\omega\)，使得 \(x \in A\) 当且仅当 \((\forall f)(\exists n) \neg P(x \mid n \mid f \mid n)\)。换句话说，\(x \in A\) 当且仅当 \(x\)-递归树 \(T_x = \{\sigma \mid (\forall \tau)(\tau \subseteq \sigma \rightarrow P(x \mid |\tau|, \tau))\}\) 在 Kleene-Brouwer 序下是良基的。那么存在一个函数 \(p_x : T_x \rightarrow \omega_1^\omega\)，其中 \(p_x \in L_{\omega_1^x}[x]\)，使得 \(p_x\) 在 Kleene-Brouwer 序下是序保持的。

现在令 \(T \subseteq 2^{<\omega} \times \omega_1^{<\omega}\) 成为一个集合，使得 \((\sigma, p) \in T\) 当且仅当 \(p\) 是从 \(\{\tau \mid \tau \subseteq [\sigma]^{|\sigma|}\} \wedge (\forall \tau')( \tau' \subseteq \tau \rightarrow P(\sigma \mid [\tau'], \tau'))\) 到 \(\omega_1\) 的一个序保持的有限函数。定义 \((\sigma', p') \geqslant (\sigma, p)\) 当且仅当 \(\sigma' \supseteq \sigma\) 且 \(p'\) 扩展 \(p\)。那么 \(T\) 在 \(>\) 下是一棵树。因此 \(x \in A\) 当且仅当存在一个 \(f : T_x \rightarrow \omega_1\) 使得 \((x, f)\) 是 \(T\) 中的一条无限路径，这当且仅当存在一个 \(f : T_x \rightarrow \omega_1\) 且 \(f \in L_{\omega_1^x}[x]\) 使得 \((x, f)\) 是 \(T\) 中的一条无限路径。

树表示的优势在于 \(x\) 的伴随路径存在于 \(L_{\omega_1^x}[x]\) 中。

- 给定 \((\sigma, p), (\sigma', p') \in 2^{<\omega} \times \omega_1^{<\omega}\)，我们说 \((\sigma', p') \prec_l (\sigma, p)\) 如果
  - 要么 \((\sigma', p') \prec (\sigma, p)\)，或
  - 存在一个 \(i\) 使得 \(\sigma'(i) < \sigma(i)\) 且对所有 \(j < i\)，\(\sigma'(j) = \sigma(j)\)，或
  - 存在一个 \(v \in \omega^{<\omega}\) 使得 \(p'(v) < p(v)\) 且对所有 \(v' \prec_{KB} v\)，\(v \in \text{Dom}(p) \Rightarrow p'(v') = p(v')\)。

\(T\) 中的一条无限路径 \((x, f)\) 是 *最左路径* 如果在 \(\{(\sigma, p) \mid (\sigma, p) \prec_l (x \mid [n], f \mid \text{Dom}(p))\}\) 中不存在无限路径。

### Lemma 4.1.1. 假设 \((x, f)\) 是 \(T\) 的最左路径。则 \(f \in L_{\omega_1^x}[x]\)。

### Proof.

假设 \((x, f)\) 是 \(T\) 的最左路径。则 \(f\) 是从 \(x\)-递归树 \(T_x = \{\sigma \mid P(x \mid |\sigma|, o)\}\) 到 \(\omega_1^x\) 的一个初始段的唯一序保持函数。由于 \(L_{\omega_1^x}[x]\) 是可接受的，根据 \(\Sigma\)-归纳定理（3.18），我们有 \(f \in L_{\omega_1^x}[x]\)。

