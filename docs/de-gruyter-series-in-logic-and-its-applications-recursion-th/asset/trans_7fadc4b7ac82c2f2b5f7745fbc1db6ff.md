

现在假设存在一个 \(\le_M\)-序列 \(\langle F_n \rangle_{n<\omega}\)，使得对每个 \(n\)，(a) \(F_n\) 通过 \(t_n\) 是一致度不变的，且 (b) \(F_{n+1} \le_M F_n\) 在锥 \(\{x \mid x \ge_T z_n\}\) 上。

令 \(z = \Phi_{n<\omega} z_n\) 且 \(\langle t_n, e_0, e_1 \rangle = t_\infty(e_0, e_1)\)。对每个 \(n\)，我们为对 \((F_{n+1}, F_n)\) 定义集合 \(A_n\) 和 \(B_n\)，分别为 Lemma 7.2.1 和 Lemma 7.2.2 中对应的集合 \(A\)。然后对每个 \(n\)，I 对 \(G_n\) 具有获胜策略 \(\delta_n\)，其中 \(y = z \oplus t \oplus (\Phi_{n<\omega} \delta_n) \oplus (\Phi_{n<\omega} \bar{\delta}_n)\)。然后如同在 Lemma 7.2.1 的证明中一样，存在一个 y-算术关系 \(P(x_0, x_1)\)，使得对任意 \(n\)，\(F_{n+1}(y)\) 是使得 \(P(x, F_n(y))\) 成立的唯一实数 \(x\)。注意，由 Lemma 7.2.2，对每个 \(n\)，\(F_{n+1}(y) \le_T F_n(y)\)。

## 提议 7.2.3 (Steel [157])

令 \(R \subseteq 2^\omega \times 2^\omega\) 为一个算术关系。如果 \(\langle x_n \rangle_{n<\omega}\) 是一串实数，使得 \(x_{n+1}\) 是满足 \(R(y, x_n)\) 的唯一 \(y\)，则存在某个 \(n\)，使得 \(x'_{n+1} \le_T x_n\)。

证明。假设为了矛盾，对每个 \(n\) 都有 \(x'_{n+1} \le_T x_n\)。定义

\(P(x, i, j) \Leftrightarrow (\exists k > j + 1)(\exists \sigma \in \omega^{<\omega})(|\sigma| = j + 1 \wedge \Phi_e^{(x)}(i) = x \wedge (\forall k' < k)R(\Phi_{\sigma(k')}^{\sigma(k+1)}, \Phi_{\sigma(k)}^{\sigma(k)}) \wedge (\exists e)(\Phi_e^x(i) = 0 \wedge \Phi_e^x = (\Phi_{\sigma(k)}^{\sigma(j+1)})).\)

根据对序列 \(\langle x_n \rangle_{n<\omega}\) 的假设，对任意 \(n\) 我们有

\((\forall i)(\forall j)(P(x_n, i, j) \Leftrightarrow (\exists k > j + 1)(i \notin (x_{n+k})^{(j+1)})).\)

由于 \(P\) 是算术的，存在 \(m\) 和 \(e\) 使得

\(P(x, i, j) \Leftrightarrow \Phi_e^{(m)}(i, j) = 1.\)

那么对任意 \(n, i, j\)，

\(\Phi_e^{(x_n)}(i, j) = 1 \Leftrightarrow (\exists k > j + 1)(i \notin (x_{n+k})^{(j+1)}).\)

令 \(j = m\)，存在一个 \(e_0\) 使得对每个 \(i\)，

\(\Phi_{e_0}^{(x_n)}(i) = 1 \Leftrightarrow \Phi_e^{(x_n)}(i, m) = 1 \Leftrightarrow (\exists k > m + 1)(i \notin (x_{n+k})^{(m+1)}).\)

当 \(i = e_0\) 时，对任意 \(n\) 我们有

\(e_0 \in (x_n)^{(m+1)} \Leftrightarrow (\exists k > m + 1)(e_0 \notin (x_{n+k})^{(m+1)}).\)

因此 \(e_0 \in (x_0)^{(m+1)}\) 当且仅当 \((\exists k > m + 1)(e_0 \notin (x_k)^{(m+1)})\)，且 \(e_0 \in (x_{k_0})^{(m+1)}\) 当且仅当 \((\exists k > m + 1)(e_0 \notin (x_{k_0+k})^{(m+1)})\)。于是 \(e_0 \in (x_0)^{(m+1)}\) 当且仅当 \(e_0 \in (x_{k_0+k})^{(m+1)}\)。再次由上述等价式，\(e_0 \in (x_0)^{(m+1)}\) 当且仅当 \(e_0 \notin (x_0)^{(m+1)}\)，这产生了矛盾。

将提议 7.2.3 相对化到 \(y\)，存在一个 \(n\) 使得 \(F_{n+1}(y)' \not\le_T F_n(y)\)，这与我们对序列 \(\langle F_n \rangle_{n<\omega}\) 的假设以及 Lemma 7.2.2 相矛盾。因此我们有：

## 引理 7.2.4

假设 ZF + AD + DC，在一致度不变函数上的偏序 \(\le_M\) 是良序。

综上所述，我们有以下定理。

## 定理 7.2.5 (Steel [159], Slaman and Steel [142])

假设 ZF + AD + DC，马丁猜想（6.6.9）对一致度不变函数成立。

## 注释 7.2.6

H. Friedman [30] 证明存在一个超算术谓词 R 和一串 \(\{x_n\}_{n<\omega}\)，使得 \(x'_{n+1} \le_T x_n\) 且 \(x_{n+1}\) 是满足 \(R(y, x_n)\) 的唯一 y。

### 7.2.1 练习

- 练习 7.2.1. 证明存在一个算术谓词 P，使得对任意 n > 0，存在一串 \(\{x_i\}_{i \le n}\) 满足：(i) 对任意 i < n，\(x'_{i+1} \le_T x_i\)，(ii) \(P(x_{i+1}, x_i)\) 且 (iii) 若 \(P(x, y)\) 则 \(y = x_{i+1}\)。

- 练习 7.2.2. 证明存在一个算术谓词 R 和一个 \(<_h\)-降序列 \(\{x_n\}_{n<\omega}\)，使得对任意 n，\(x_{n+1}\) 是满足 \(R(y, x_n)\) 的唯一实数 y。

## 7.3 Posner–Robinson 定理

### 7.3.1 原始 Posner–Robinson 定理

## 定理 7.3.1 (Posner and Robinson [114])

对任意非递归 \(x \le_T 0'\)，存在一个 g 使得 \(x \oplus g \equiv_T g' \equiv_T 0'\)。

因此给定一个非递归的 \(\Delta^0_2\)-实数 x，定理 7.3.1 说明存在一个相对于它 x 是其图灵跳的 g。

证明。为了证明这一点，我们使用 Jockusch 和 Shore [57] 的方法。固定 \(x >_T 0\) 为 \(\Delta^0_2\)。我们可以假设 x 不是递归可枚举的。对每个 e，考虑以下陈述：

\((\forall \alpha \in 2^\omega)(\exists n)(n \in x \wedge (\forall \tau \supseteq \sigma \supseteq 0^n1)(\Phi_e^\tau(e)[s] \uparrow) \vee (n \notin x \wedge (\exists \tau \supseteq \sigma \supseteq 0^n1)(\Phi_e^\tau(e)[s] \downarrow)).\)

由于 x 不是递归可枚举的，\((\sharp_e)\) 对每个 e 都成立。我们通过归纳构造 g。

步骤 0：定义 \(g_0 = \emptyset\)。

步骤 s + 1：

- 子步骤 1. 定义 \(g(s, 1) = g_s^\frown 0'(s)\)。

- 子步骤 2. 找到最小的 n，使得以下之一成立

  \((n \in x \wedge \forall \tau \supseteq g(s, 1)^\frown 0^n 1)(\Phi_s^\tau(s)[s] \uparrow)\)

  或

  \((n \notin x \wedge (\exists \tau \supseteq g(s, 1)^\frown 0^n 1)(\Phi_s^\tau(s)[s] \downarrow)).\)

由 \((t_s)\)，这样的 n 存在。在第一种情况下，定义 \(g_{s+1} = g(s, 1) \ulcorner 0^s 1 \urcorner\)。在第二种情况下，选择字典序最小的 \(\tau\) 使得 \(\tau \supseteq g(s, 1) \ulcorner 0^s 1 \urcorner (\Phi_s^\tau(s)[|\tau|] \downarrow)\)。定义 \(g_{s+1} = \tau \ulcorner 1 \urcorner\)。

令 \(g = \bigcup_{s < \omega} g_s\)。注意该构造是一致 \(x \oplus \emptyset'\)-递归的。因此 \(\emptyset' \geqslant_T x \oplus \emptyset'\)。我们将证明 \(0'(s)\) 和 \(g_s\) 是一致 \(g \oplus x\)-递归的。假设我们已计算出 \(g_s\) 和 \(0'(s)\)。那么 \(0'(s + 1) = g(|g_s| + 1)\)。要计算 \(g_{s+1}\)，搜索唯一的 n 使得 \((g \upharpoonright |g_s| + 1) \ulcorner 0^s 1 \urcorner < g\)。根据构造，以下之一成立

- (1) \(n < s\) 或
- (2) \(n \notin x\) 且存在一个 \(\tau \supseteq (g \upharpoonright |g_s| + 1) \ulcorner 0^s 1 \urcorner\) 使得 \(\tau < g\) 且 \(\Phi_s^\tau(s)[|\tau|] \downarrow\)。

若 (1) 成立，则 \(g(s+1) = \langle g \upharpoonright |g_s| + 1 \rangle \ulcorner 0^s 1 \urcorner\)。若 (2) 成立，则存在唯一的 \(\tau \supseteq (g \upharpoonright |g_s| + 1) \ulcorner 0^s 1 \urcorner\) 使得 \(\tau < g\) 且 \(\Phi_s^\tau(s)[|\tau|] \downarrow\)。由此 \(g_{s+1} = \tau\)。因此 \(\emptyset' \geqslant_T g \oplus x\)。

要证明 \(g' \leq_T g \oplus \emptyset'\)，观察到对每个 e 存在一个 n 使得以下之一成立：\(\Phi_e^{g \oplus \emptyset'}(e) \downarrow\) 或对任意 \(\tau > g \upharpoonright n\) 有 \(\Phi_e^\tau(e) \downarrow\)。利用这一点，可以立即验证 \(g' \leq_T g \oplus \emptyset'\)。\(\square\)

### 7.3.2 一个超限 Posner-Robinson 定理

定理 7.3.1 可以以多种不同的方式迭代到超限。以下是第一个版本。

## 定理 7.3.2 (Slaman and Steel [142])

令 \(0 < b < \omega_1^{CK}\) 且令 z 为一个实数，使得对每个 \(y < b\) 都有 \(0^{(y)} <_T z\)。则存在一个 g 使得 \(g \oplus z \equiv_T g^{(b)}\)。

本节其余部分专门用于证明定理 7.3.2。

令 \(a \in \mathcal{O}\)。第一步是引入一个由 \(|a|\) 索引的算术谓词枚举。由定理 1.3.4，集合 \(\{b \mid b <_O a\}\) 是递归可枚举的。应用递归定理，我们可以假设存在一个部分递归函数 \(\Phi : a^2 \to \omega\) 使得对每个 \(b <_O a\)，\(\{\Phi(b, i)\}_{i < \omega}\) 是 "\(\Sigma_b^0\)-谓词" 的 Gödel 数集合的一个枚举。为了简化记号，我们将谓词与其 Gödel 数识别。

我们通过归纳引入 \(\Sigma_b^0\) 谓词的一个枚举。\(\Sigma_1^0\)-谓词的枚举是标准的。如果 \(b = 2^e \in \mathcal{O}\) 且 \(b <_O a\)，则谓词 \(P(x, n)\) 是第 \(i\) 个 \(\Sigma_b^0\)-谓词，或 \(P(x, n) = P_{\Phi(b, i)}(x, n)\)，如果 \(P(x, n) \leftrightarrow (\exists m)\neg Q(x, n, m)\)，其中 \(Q(x, n, m)\) 是第 \(i\) 个 \(\Sigma_b^0\)-谓词。

如果 \(b = 3 \cdot 5^e \in \mathcal{O}\) 且 \(b <_O a\)，则谓词 \(P(x, n)\) 是第 \(i\) 个 \(\Sigma_b^0\)-谓词，或 \(P(x, n) = P_{\Phi(b, i)}(x, n)\)，如果 \(P(x, n) \leftrightarrow P_{\Phi(i, \Phi(b, n))}(x, n)\)，其中 \(P(i, \Phi(b, n)) = (i_0(n), i_1(n))\) 使得对每个 n 都有 \(i_0(n) <_O b\)。下一个引理通过对 b 的记号进行归纳证明，留给读者。

## 引理 7.3.3

存在递归函数 \(f : \omega \to \omega\) 和 \(g : \omega \to \omega^2\) 使得对任意 \(b <_O a\)，

- (i) 若 \(b = 1\) 或 \(2^e\)，则 \(P_{\Phi(b, f(b))} \equiv_T H_{f(b)}^2\) 通过 \(g(b)\)；
- (ii) 若 \(b = 3 \cdot 5^e <_O a\)，则 \(P_{\Phi(b, f(b))} \equiv_T H_{f(b)}^2\) 通过 \(g(b)\)。

