

以上内容有一个明显的推广，允许在 \(\omega^\omega\) 中使用参数，从而得到相对于一个实数或一组有限实数的 \(\Sigma^0_n\)-谓词类。

### Definition 1.1.4.

- (i) 谓词 \(P^0(y, m)\) 是 \(\Sigma^1_1(\alpha)\)，当且仅当存在一个部分递归谓词 \(R(A, y, m)\)，使得对所有 \(y\) 和 \(m\)，\(P^0(y, m) \leftrightarrow R(\alpha, y, m)\)。
- (ii) \(P^0(y, m)\) 是 \(\Pi^0_n(\alpha)\)，当且仅当 \(\neg P^0(y, m)\) 是 \(\Sigma^0_n(\alpha)\)。
- (iii) \(P^0(y, m)\) 是 \(\Sigma^0_n(\alpha)\)，当且仅当存在一个 \(\Pi^0_n(\alpha)\)-谓词 \(R^0(y, m, k)\)，使得 \(P^0(y, m)\) 当 \((\exists k)R^0(y, m, k)\) 时成立。
- (iv) \(P^0(y, m)\) 是 \(\Delta^0_n(\alpha)\)，当且仅当它既是 \(\Sigma^0_{n+1}(\alpha)\) 也是 \(\Pi^0_{n+1}(\alpha)\)。

给定一组谓词 \(\Gamma\)，我们说集合 \(a \subseteq \omega\)（或 \(P^* \subseteq \omega^\omega\)）是一个 \(\Gamma\)-集，或 \(\Gamma\) 的一个成员，如果存在谓词 \(P(x, m) \in \Gamma\) 使得 \(m \in a \leftrightarrow P(0, m)\)（或 \(x \in P^* \leftrightarrow P(x, 0)\)）。对每个 \(n < \omega\)，令 \(\Sigma^0_n\)、\(\Pi^0_n\) 和 \(\Delta^0_n\) 分别表示 \(\Sigma^0_n\)、\(\Pi^0_n\) 和 \(\Delta^0_n\)-谓词的类。以下引理是众所周知的。证明可参见 [53]。

### Lemma 1.1.5.

- (i) 设 \(n < \omega\)。存在一个 \(\Sigma^0_n\)-集 \(U \subseteq \omega^\omega \times \omega^\omega\)，使得对每个 \(P \in \Sigma^0_n\)，都存在某个 \(y\) 使得 \(P = \{x \mid (x, y) \in U\}\)。
- (ii) 对每个 \(n\)，\(\Sigma^0_n \subset \Delta^0_{n+1} \subset \Sigma^0_{n+1}\) 且 \(\Pi^0_n \subset \Delta^0_{n+1} \subset \Pi^0_{n+1}\)。

在经典递归论中，集合 \(a \subseteq \omega\) 是 \(\Sigma^0_1\) 当且仅当 \(a\) 是 \(\Sigma^0_1(\emptyset')\)。然而，这对于实数集通常不成立。例如，集合 \(\{\emptyset^{(\omega)}\}\) 是 \(\Sigma^0_3\)，但对于任何 \(x \in \omega^\omega\)，它都不是 \(\Sigma^0_1(x)\)（作为单元素集）（参见练习 1.1.5）。

## 1.1.2 解析谓词

### Definition 1.1.6.

- (i) 谓词 \(P(x, m)\) 是 \(\Sigma^1_1\)，如果它是 \(\Sigma^1_1\)；
- (ii) 谓词 \(P(x, m)\) 是 \(\Pi^0_n\)，如果 \(\neg P(x, m)\) 是 \(\Sigma^0_n\)；
- (iii) 谓词 \(P(x, m)\) 是 \(\Sigma^0_{n+1}\)，当且仅当存在一个 \(\Pi^0_n\)-谓词 \(R(x, y, m) \in \omega^\omega \times \omega^\omega \times \omega\)，使得 \(P(x, m)\) 当且仅当 \((\exists y)R(x, y, m)\)。
- (iv) 谓词 \(P(x, m)\) 是 \(\Delta^0_1\)，当且仅当它既是 \(\Pi^0_1\) 也是 \(\Sigma^0_1\)。
- (v) 谓词 \(P\) 是 *解析的*，如果存在某个 \(n\) 使得 \(P \in \Sigma^1_n\)。

如同引理 1.1.5 所示，我们有以下易于验证的事实。

### Lemma 1.1.7.

- (i) 设 \(n < \omega\)。存在一个 \(\Sigma^1_n\)-集 \(U \subseteq \omega^\omega \times \omega^\omega\)，使得对每个 \(P \in \Sigma^1_n\)，都存在某个 \(y\) 使得 \(P = \{x \mid (x, y) \in U\}\)。
- (ii) 对每个 \(n\)，\(\Sigma^1_n \subset \Delta^1_{n+1} \subset \Sigma^1_{n+1}\) 且 \(\Pi^1_n \subset \Delta^1_{n+1} \subset \Pi^1_{n+1}\)。
- (iii) 每个算术集都是 \(\Delta^1_1\)。

关于解析集的更多基本事实可参见 Jech [53]。对 \(\sigma \in \omega^{<\omega}\)，令 \([\sigma]\) 表示 \(\omega^\omega\) 中扩展 \(\sigma\) 的函数集合。我们说函数 \(f : \omega^\omega \to \omega^\omega\) 属于类 \(\Gamma\)，如果 \(\{(x, \sigma) \in \omega^\omega \times \omega^{<\omega} \mid x \in f^{-1}([\sigma])\} \in \Gamma\)。注意，每个 \(\Sigma_1^1\)-函数都是连续的。

以下命题是直接的。

### Proposition 1.1.8.

- (i) 如果 \(f : \omega \to \omega\) 是全函数，则 \(f \in \Sigma_2^0\) 当且仅当 \(f \in \Delta_2^0\)。
- (ii) 函数 \(f : \omega^\omega \to \omega^\omega\) 是 \(\Sigma_1^1\) 当且仅当其图 \(G' = \{(x, y) \mid f(x) = y\}\) 是 \(\Sigma_1^1\)；如果 \(f\) 是 \(\Pi_1^1\)，则 \(G' \in \Pi_1^1\)；如果 \(f\) 是 \(\Delta_1^1\)，则 \(G' \in \Delta_1^1\)。
- (iii) 如果 \(f\) 是全函数，则 \(G'\) 是 \(\Delta_1^1\) 当且仅当 \(f\) 是 \(\Delta_1^1\)。
- (iv) 如果 \(f : \omega^\omega \to \omega^\omega\) 是全函数，则 \(f \in \Sigma_1^1\) 当且仅当 \(f \in \Delta_1^1\)。

证明。(i) 显而易见。对于 (ii)，注意 \((x, y) \in G'\) 当且仅当 \((\forall n)(\forall \sigma \prec x \in f^{-1}([\sigma]))\)。因此，如果 \(f\) 是 \(\Sigma_1^1\)（或 \(\Pi_1^1\)），则 \(G'\) 是 \(\Sigma_1^1\)（或 \(\Pi_1^1\)）。此外，如果 \(G'\) 是 \(\Sigma_1^1\)，则 \(x \in f^{-1}([\sigma])\) 当且仅当 \((\exists y)(\forall \sigma \prec x, (y) \in G')\)。所以 \(f\) 是 \(\Sigma_1^1\) 当且仅当其图 \(G' = \{(x, y) \mid f(x) = y\}\) 是 \(\Sigma_2^1\)。
(iii). 如果 \(f\) 是全函数，则 \(x \in f^{-1}([\sigma])\) 当且仅当 \((\forall y)(\forall \tau \prec x \in f^{-1}([\tau]))\)。
(iv). 如果 \(f\) 是全函数，则 \(x \in f^{-1}([\sigma])\) 当且仅当 \((\forall y)(\forall \sigma \prec x, y) \in G'\)。所以如果 \(G'\) 是 \(\Sigma_n^1\)，则 \(f\) 是 \(\Pi_n^1\)。由 (iii)，\(f\) 是 \(\Delta_n^1\)。

给定 \(\omega^{<\omega}\) 中的 \(\sigma_i\) 和 \(\sigma'_i\)，其中 \(i \le n\)，如果对每个 \(i\) 都有 \(\sigma'_i \subseteq \sigma_i\)，则我们说 \((\sigma'_0, \dots, \sigma'_n)\) 是 \((\sigma_0, \dots, \sigma_n)\) 的子串。假设树 \(T \subseteq \omega^{<\omega} \times \dots \times \omega^{<\omega}\)（\(n\)-重积）具有如下性质：如果 \((\sigma_0, \dots, \sigma_n) \in T\)，则其所有子串都在 \(T\) 中。出于我们的目的，所有树都向下生长，根在顶部。以下树表示定理为 \(\Sigma_1^1\)-实数集提供了有用的图景。

### Proposition 1.1.9.

谓词 \(P(x, m)\) 是 \(\Sigma_1^1\) 当且仅当存在递归树的递归序列 \(\{T_m\}_{m < \omega}\)，使得 \(T_m \subseteq \omega^{<\omega} \times \omega^{<\omega}\) 且

\(P(x, m) \Leftrightarrow (\exists y)(\forall n)(\langle x \mid n, y \mid n \rangle \in T_m).\)

证明。谓词 \(P(x, m)\) 是 \(\Sigma_1^1\) 当且仅当存在一个部分递归函数 \(\Phi(\sigma, \tau, m)\)，它满足定义 1.1.1 的性质 (i)—(iii)，使得 \(P(x, m) \Leftrightarrow (\exists y)(\forall k)(\Phi(x \mid k, y \mid k, m) \downarrow \to \Phi(x \mid k, y \mid k, m) \neq 0)\)。在阶段 \(\max\{|\sigma|, |\tau|\}\) 时，当且仅当 \(\Phi(\sigma, \tau, m) \downarrow\) 或 \(\Phi(\sigma, \tau, m) \neq 0\) 时，将 \((\sigma, \tau)\) 放入 \(T_m\)。我们留给读者验证 \(\{T_m\}_{m \in \omega}\) 满足要求。

## 1.1.3 \(\Sigma_1^1\)-实数集

实数集是 \(\Sigma_1^1\)，当且仅当存在一个 \(\Sigma_1^1\)-谓词 \(P\)（可能带有数参数 \(m\)），使得 \(P(x, m)\) 成立当且仅当 \(x\) 属于该集合。实数集是 \(\Pi_1^1\)，当且仅当其补集是 \(\Sigma_1^1\)。\(\Sigma_1^1\) 和 \(\Pi_1^1\)-实数集在高阶递归论中都扮演着重要角色。在本节中，我们介绍关于这些集合的一些基本事实。

回顾，\( P \subseteq \omega^\omega \) 是完美的，如果它是没有孤立点的闭集。下一定理表明，每个不可数的 \(\Sigma^1_1\)-实数集都具有可称为完美集性质的性质。

### Theorem 1.1.10 (Suslin [162]).

如果 \( P \) 是 \(\Sigma^1_1\) 且不可数，则它包含一个完美子集。

证明。假设 \( P(x) \) 是 \(\Sigma^1_1\)（为简化起见，假定没有定义 \( P \) 的数变量）。我们给出定理 1.1.10 的两个证明。一个是集合论的，另一个是递归论的。

集合论证明。由命题 1.1.9，存在递归树 \( T \subseteq \omega^{<\omega} \times \omega^{<\omega} \)，使得 \( x \in P \) 当且仅当 \( (\exists y)(\forall n)[x \mid y, n) \in T \)。令 \( T' \) 为 \( T \) 的子树，使得

\( (\sigma, \tau) \in T' \iff \{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} > \aleph_0 \)。

定义

\( Q = \{x \mid (\exists y)(\forall n)(\langle x \mid y, n \rangle \in T'\} \)。

由于 \( P \) 是不可数的，\( Q \) 非空。显然 \( Q \subseteq P \)。注意，如果 \( (\sigma, \tau) \in T' \)，则存在 \( k \) 和 \( k' \) 使得 \( (\sigma \mid k, \tau \mid k') \in T' \)。我们将证明 \( Q \) 包含一个完美集。通过对 \( n \) 归纳，构造一棵完美树 \( S_0 \) 和一棵树 \( S_1 \)，具有以下性质：

- (i) \( S_1 \subseteq T' \);
- (ii) 令 \( [S_0] \) 表示 \( S_0 \) 中的无限路径集合。则 \( [S_0] \) 包含于 \( \{x \mid (\exists y)(\forall n)(\langle x \mid y, n \rangle \in S_1\}\) 中；
- (iii) \( (\forall(\sigma, \tau) \in S_1)(\{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} > \aleph_0) \)。

我们从第 0 层开始，令 \( S_0 \) 和 \( S_1 \) 为空。假设我们在第 \( n+1 \) 层。令 \( \sigma \in S_0 \) 为第 \( n \) 层定义且 \( |\sigma| = n \)。由归纳假设，存在 \( \tau \) 使得 \( (\sigma, \tau) \in S_1 \) 在第 \( n \) 层被定义，且 \( Q_{\sigma, \tau} = \{x > \sigma \mid (\exists y > \tau)(\forall n)(\langle x \mid y, n \rangle \in T)\} \) 是不可数的。

声明。存在 \(\sigma\) 的不兼容扩展 \(\sigma_0, \sigma_1\)，使得 \( Q_{\sigma_0, \tau} \) 和 \( Q_{\sigma_1, \tau} \) 都是不可数的。

如果声明为假，则存在唯一的 \( x > \sigma \)，使得如果 \(\sigma' > \sigma\) 与 \( x \) 不兼容，则 \( Q_{\sigma', \tau} \) 是可数的。但这将意味着 \( Q_{\sigma, \tau} = \{x\} \cup \bigcup_{\sigma' > \sigma, \sigma' \neq x} Q_{\sigma', \tau} \) 是可数的，这与假设矛盾。

按声明固定 \((\sigma_0, \sigma_1)\)。则存在 \(\tau_0, \tau_1 > \tau\)，使得对 \( i = 0, 1 \)，\( |\{x > \sigma_i \mid (\exists y > \tau_i)(\forall n)(\langle x \mid y, n \rangle \in T)\}| > \aleph_0 \)。将 \(\sigma_0\) 和 \(\sigma_1\) 放入 \( S_0 \)，并将 \((\sigma_i, \tau_i)\)，对 \( i = 0, 1 \)，放入 \( S_1 \)。该过程对每个 \(\sigma \in S_0\) 进行。显然 \( S_0 \) 是一棵完美树，且对每个 \( x \) 存在 \( y \) 使得 \( (\forall n)(\langle x \mid y, n \rangle \in S_1 \)。由于 \( S_1 \subseteq T' \subseteq T \)，\( [S_0] \subseteq Q \subseteq P \)。

