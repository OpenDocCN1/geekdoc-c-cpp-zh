

定义 \( T = \{\sigma \in 2^{<\omega} \mid (\exists y \in B)(y \succ \sigma)\} \)。显然 \( B \subseteq [T] \)。由于 \( B \) 是 \( \Sigma_1^1 \)，\( [T] \) 是 \( \Sigma_1^1 \)。由于 \( A \) 是闭集，我们有 \( [T] \subseteq A \)。另外，\( A \) 是零集意味着 \( [T] \) 也是零集。根据引理 13.1.10 和 \( \Pi_1^1 \)-一致化的常规应用，存在一个全态的 \( \Sigma_1^1 \)-函数 \( f : \omega \to \text{HYP} \)，使得对于任意 \( k \)，\( f(k) \in \Sigma_1 \cap \text{HYP} \)，\( A_{f(k)} \subseteq 2^\omega \setminus [T] \) 且 \( \mu(A_{f(k)}) > 2^{-k} \)。令

```
\( C = \{z \mid (\forall k)(z_k \notin A_{f(k)})\} \)。
```

那么 \( C \) 是一个 \( \Sigma_1^1 \)-闭零集。然而，\( x \in C \)，这产生了矛盾。

## 14.1.2 Kurtz 随机实数的圆锥基

从定理 14.1.3 的证明可以看出，高于 \( \mathcal{O} \) 的超度都包含一个 \( \Sigma_1^1 \)-Kurtz 随机实数。这对于 \( \Pi_1^1 \)-Kurtz 随机性不成立。我们说，一个超度 \( \mathbf{a} \) 是 *T-Kurtz 随机性的圆锥基*，如果对于每个超度 \( \mathbf{b} \ge \mathbf{a} \)，\( \mathbf{b} \) 包含一个 \( T \)-Kurtz 随机实数。

\( \mathcal{O} \) 的超度是 \( \Sigma_1^1 \)-Kurtz 随机性的圆锥基，如定理 14.1.3 所证明。并非每个非零超度都是 \( \Sigma_1^1 \)-Kurtz 随机性的圆锥基（见引理 14.6.1）。是否存在 \( \Pi_1^1 \)-Kurtz 随机性的圆锥基？如果存在，这样的基，比如说 \( \mathbf{b} \)，不能高算术归约到一个 \( \Pi_1^1 \)-单元。这意味着充当基的超度必须相当复杂。

**引理 14.1.5.** 对于任意实数 \( x \) 和 \( z \ge_T x' \)，存在一个 \( x \)-Kurtz 随机实数 \( y \equiv_T z \)。

**证明.** 令 \( z \ge_T x' \) 并固定 \( x \)-t.e. 开集 \( \{U_n^s\}_{n < \omega} \) 的一个枚举。我们按如下方式构造字符串的一个递增序列 \( \{\sigma_s\}_{1 \le s < \omega} \)。

- 令 \( \sigma_0 = 0 \)。

- 阶段 \( s + 1 \)。令 \( l_0 = 0, l_1 = |\sigma_s| \)，且对于 \( n > 1 \)，\( l_{n+1} = 2^{l_n} \)。对于每个这样的 \( n \)，令

```
\( A_n = \{\sigma \in 2^{l_{n-1}} \mid (\exists m < n)(\forall i)(\forall j)(l_m \le i, j < l_{m+1} \implies \sigma(i) = \sigma(j))\} \)。
```

那么

```
\( |A_n| \le 2 \cdot 2^{-l_{n+1}} \)。
```

换句话说，

```
\( \mu(B_n = \bigcup \{[\sigma] \mid \sigma \ge \sigma_s \wedge \sigma \notin A_n\}) \ge 2^{-l_1} \cdot (1 - 2^{-l_{n+1} + l_{n+1}}) \)。
```

情况 1。存在一个 \( m > l_1 + 1 \)，使得 \( |\{\sigma \ge \sigma_s \mid \sigma \in 2^m \cap [\sigma] \subseteq U_k^s\}| > 2^{m-l_1-1} \)。

令 \( n = m + 1 \)。那么 \( l_{n+1} - 1 - l_n > 2 \) 且 \( l_n > m \)。存在一个 \( \sigma \in 2^{l_{n-1}} \setminus A_n \) 和一个 \( \tau \le \sigma \)，使得 \( [\tau] \subseteq U_k^s \) 且 \( \tau \ge 2^m \)。

令 \( \sigma_{s+1} = \sigma(s)^{[l_{n-1}]} \)。

情况 2。否则。令 \( \sigma_{s+1} = \sigma_s^c(s)^{[l_{s-1}]} \)。

这完成了阶段 \( s + 1 \) 的构造。令 \( U = \bigcup_s \sigma_s \)。显然该构造在 \( z \) 中是递归的，因此 \( y \ge_T z \)。此外，如果 \( U_k^s \) 的测度为 1，那么情况 1 在阶段 \( s + 1 \) 成立。因此 \( y \) 是 \( x \)-Kurtz 随机的。

令 \( l_0 = 0 \) 且对于 \( n > 0 \)，令 \( l_n = 2^n \)。要从 \( y \) 计算 \( z(n) \)，用 \( y \)-递归方式找到第 \( n \) 个 \( l_m \)，使得对于所有 \( i \)、\( j \) 且 \( l_m \le i < j < l_{m+1} \)，有 \( y(i) = y(j) \)。那么 \( z(n) = y(l_m) \)。

我们称 \( A \subseteq \omega \times 2^\omega \) 为一个通用的 \( \Pi_1^1 \)-闭集，如果 (i) 它是 \( \Pi_1^1 \)，(ii) 对于每个 \( n \)，\( A_n = \{x \mid (n, x) \in A\} \) 是一个 \( \Pi_1^1 \)-闭集，且 (iii) 每个 \( \Pi_1^1 \)-闭集都是某个 \( n \) 的 \( A_n \)。根据定理 13.1.3 和 13.1.14，实数 \( x_0 = \{n \mid \mu(A_n) = 0\} \) 是 \( \Sigma_1^1 \)。令

\( c = \{(n, \sigma) \mid n \in x_0 \wedge (\exists x)(n, x) \in A \wedge \sigma \prec x\} \subseteq \omega \times 2^{<\omega} \)。

那么 \( c \) 可以被视为一个 \( \Sigma_1^1 \)-实数。由于每个 \( \Pi_1^1 \)-零闭集都是 \( \Pi_1^1(c) \)，每个 \( c \)-Kurtz 随机实数都是 \( \Pi_1^1 \)-Kurtz 随机的。

## 定理 14.1.6. \( c \) 的超度是 \( \Pi_1^1 \)-Kurtz 随机性的圆锥基。

证明。引理 14.1.5 意味着任何 \( y \ge_T c' \) 的图灵度包含一个成员，该成员是 \( c \)-Kurtz 随机的，因此也是 \( \Pi_1^1 \)-Kurtz 随机的。因此 \( c \) 是 \( \Pi_1^1 \)-Kurtz 随机性的一个基。

我们分析 \( c \) 的复杂度。由于每个 \( \Pi_1^1 \)-单元在 \( c \) 中是递归的，\( c \notin L_{\delta_1^1} \)。此外，集合 \( \{x \mid x \text{ 是一个 } \Pi_1^1\text{-单元}\} \) 是 \( \Delta_1^1(c) \)。换句话说，\( \{x \mid x \text{ 是一个 } \Pi_1^1\text{-单元}\} \in L_{\omega_1^{ck}}[c] \)。因此有 \( \omega_1^c > \delta_1^1 \)。应用与命题 4.4.4 中相同的论证，\( L_{\delta_1^1} \) 中的实数恰好是那些 \( \Delta_1^1 \) 的实数，因此 \( c \) 不是 \( \Delta_1^1 \)。此外，由于 \( c \) 是 \( \Sigma_2^1 \)，它在 \( L_{\delta_1^1} \) 上是 \( \Sigma_1^1 \) 可定义的，因此 \( c \in L_{\delta_1^1+1} \)。确实，所有 \( \Sigma_1^1 \)-实数都属于 \( L_{\delta_1^1+1} \)。因此，

\( c \) 在所有 \( \Sigma_2^1 \) 实数中具有最大的超度。

## 14.1.3 练习

练习 14.1.1. 证明 \( \Delta_1^1 \) 实数集和 \( \Pi_1^1 \)-Kurtz 随机实数集都不是 \( \Sigma_2^0 \)。

练习 14.1.2. 证明存在一个不是 Schnorr 随机的 \( \Pi_1^1 \)-Kurtz 随机实数。

练习 14.1.3. 证明 \( \Pi_1^1 \)-Kurtz 随机实数集不是 \( \Pi_1^1 \)。

练习 14.1.4. 证明 \( \langle L_{\delta_1^1}, \in \rangle <_{\Sigma_1} \langle L, \in \rangle \)。

## 14.2 \( \Delta_1^1 \) 和 \( \Pi_1^1 \)-Martin-Löf 随机性

### 14.2.1 \( \Delta_1^1 \)-随机性

定义 14.2.1. 设 \( \Gamma \) 是实数集的一个可定义类。我们说 \( x \) 是 \( \Gamma \)-随机的，如果它不属于任何 \( \Gamma \)-零集。

在本节中，我们研究 \( \Delta^1_1 \)-随机性的关键性质。

命题 14.2.2. 假设 \( A \) 是一个 \( \Delta^1_1 \)-零集。存在一个 \( \Delta^1_1 \)-集 \( V \subseteq \omega \times 2^{<\omega} \)，使得 \( (\forall n)(\mu(V_n) = 2^{-n}) \) 且 \( A \subseteq \bigcap_{n<\omega} V_n \)，其中 \( V_n = \{\sigma \mid (n, \sigma) \in V\} \) 是一个 \( \Delta^1_1 \)-开集。

证明。如前所述，\( \{A_s\} \) 是由 Borel 码 \( z \) 生成的实数集的集合（§2.7.1）。由于 \( A \) 是一个 \( \Delta^1_1 \)-零集，根据引理 13.11.10，存在一个 \( \Delta^1_1 \)-函数 \( f : \omega \to \Sigma_1 \cap \text{HYP} \)，使得对于每个 \( n < \omega \),

- \( \mu(A_{f(n)}) < 2^{-n} \)，且
- \( A \subseteq A_{f(n)} \)

那么 \( A_{f(n)} = [U_n] \) 对于某个 \( \Delta^1_1 \)-集 \( U_n \subseteq 2^{<\omega} \)。现在只需证明 \( \{U_n\}_{n<\omega} \) 可以扩展为一个 \( \Delta^1_1 \)-集族 \( \{V_n\}_{n<\omega} \)，使得 \( U_n \subseteq V_n \) 且 \( \mu(V_n) = 2^{-n} \)。由于集合 \( U = \{(n, \sigma) \mid \sigma \in U_n\} \) 是 \( \Delta^1_1 \)，存在一个 \( m \in \Theta \) 使得 \( U \le_T H_m \)。注意集合 \( \{(x, e, p) \in 2^\omega \times \omega \times \mathbf{Q} \mid \mu(\{o\} \mid (\exists i)(\Phi_e^i(i) = o\})) > p\} \) 是 r.e. 的。然后，通过经典随机性理论中相对于 \( H_{2^m} \) 的标准技术，存在一个 \( V \subseteq \omega \times 2^{<\omega} \)，在 \( H_{2^m} \) 中是递归的，使得对于每个 \( n \)，\( \mu(V_n) = 2^{-n} \) 且 \( U_n \subseteq V_n \)。那么 \( A \subseteq \bigcap_{n<\omega} V_n \)。

根据命题 14.2.2，\( \Delta^1_1 \)-随机性可以被视为 Schnorr 随机性的高阶类比。

命题 14.2.3 (Martin-Löf [97])。\( \Delta^1_1 \)-随机实数集是 \( \Sigma^1_1 \) 但不是 \( \Delta^1_1 \)。

证明。定义一个 \( \Sigma^1_1 \)-集

```
\( A = \{x \mid (\forall e)(\forall n)((m \in \Theta)(\mu m[\{i(\{o\} \mid \exists i)(\Phi_e^{H_n}(\langle m, i \rangle) = o\})) \le 2^{-m}) \to (\exists m)(\forall i)(x \not\prec \Phi_e^{H_n}(\langle m, i \rangle))).\)
```

根据命题 14.2.2，\( A \) 正是 \( \Delta^1_1 \)-随机实数集。由于 \( A \) 不包含任何高算术成员，根据定理 13.13.13，它不是 \( \Delta^1_1 \)。

### 14.2.2 \( \Pi^1_1 \)-Martin-Löf 随机性

开集序列 \( \{U_n\}_{n<\omega} \) 是一个 Martin-Löf 测试（ML 测试），如果对于所有 \( n \)，\( \mu(U_n) < 2^{-n} \)。给定实数集的一个类 \( \Gamma \)（例如，\( \Pi^1_1 \)），\( \{U_n\}_{n<\omega} \) 是一个 \( \Gamma \)-ML 测试，如果 \( \{(n, \sigma) \mid \sigma \in 2^{<\omega} \wedge [\sigma] \in U_n\} \in \Gamma \)。

定义 14.2.4. 设 \( \Gamma \) 是实数集的一个类。那么 \( x \) 是 \( \Gamma \)-ML 随机的，如果对于任何 \( \Gamma \) ML 测试 \( \{U_n\}_{n<\omega} \)，\( x \notin \bigcap_{n<\omega} U_n \)。

命题 14.2.5 (Jorhth and Nies [51])。存在一个通用的 \( \Pi^1_1 \)-ML 测试 \( \{U_n\}_{n<\omega} \)，即，对于每个 \( \Pi^1_1 \)-ML 测试 \( \{V_n\}_{n<\omega} \)，\( \bigcap_{n<\omega} V_n \subseteq \bigcap_{n<\omega} U_n \)。

