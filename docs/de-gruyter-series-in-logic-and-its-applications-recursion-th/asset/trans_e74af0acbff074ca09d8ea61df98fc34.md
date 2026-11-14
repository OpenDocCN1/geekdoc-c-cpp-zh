

根据 (2),

\(\mu(U_{n_0, <\beta_0} \cap [\sigma_0]) > \frac{1}{2} \cdot 2^{-|\sigma_0|}.\)

根据 (1) 和 (4),

\(\mu(\bigcap_{n>n_0} U_{n, <\beta_0} \cap [\sigma_0]) > \frac{1}{4} \cdot 2^{-|\sigma_0|}.\)

因此存在一个 \(\sigma_1 > \sigma_0\) 使得

\(\mu(\bigcap_{n>n_0} U_{n, <\alpha} \cap [\sigma_1]) > \frac{3}{4} \cdot 2^{-|\sigma_1|}.\)

令 \(n_1 = |\sigma_1| + 2\)。存在一个 \(\beta_1 < \beta_0\) 使得

\(\mu(U_{n_1, <\beta_0} \cap [\sigma_1]) > \frac{3}{4} \cdot 2^{-|\sigma_1|}.\)

重复该过程，得到一个无限下降的序数序列 \(\beta_0 > \beta_1 > \cdots\)，这产生了矛盾。由此可见，\(\{U_n\}_{n<\omega}\) 是一个广义 \(\Pi^1_1\)-ML 测试，且 \(x \in \bigcap_{n<\omega} U_n\).

**定理 14.2.13** (Chong, Nies 和 Yu). _存在一个实数，它是_ \(\Pi^1_1\)_-ML随机，但不是强_ \(\Pi^1_1\)_-ML随机。_

_证明._ 根据推论 14.4.26，存在一个正测度的 \(\Sigma^1_1\)-闭集 _P_，其仅由 \(\Pi^1_1\)-ML 随机实数组成。根据引理 14.2.12，存在一个 \(x \in P\)，它不是强 \(\Pi^1_1\)-ML 随机。

### 14.2.5 练习

- **练习 14.2.1** (Sacks [123]). _证明每个_ \(\Delta^1_1\)_-随机实数是_ \(\Sigma^1_1\)_-随机。_

- **练习 14.2.2.** _证明对于任意_ \(\Delta^1_1\)_-随机 x 和递归序数_ \(\beta\)_,_ \(f^{x(\beta)} \equiv_T x \oplus 0^{(\beta)}\)_._

- **练习 14.2.3** (Yu [171]). _证明_ \(\Delta^1_1\)_-随机实数的集合不是_ \(\Sigma^0_2\)_。_

- **练习 14.2.4.** _证明对于任意_ \(\Delta^1_1\)_-随机 x 和递归函数_ \(f: 2^\omega \to 2^\omega\)_, 如果 f 几乎处处可微，则 f 在 x 处可微。_

- **练习 14.2.5** (Bienvenu, Greenberg 和 Monin). _证明对于任何 x，它是_ \(\Sigma^1_1\)_-闭实数集的最左路径，存在一个广义_ \(\Pi^1_1\)_-Martin-Löf 测试_ \(\{U_n\}_{n<\omega}\) _，使得_ \(x \in \bigcap_{n<\omega} U_n\) _且_ \(\bigcap_{n<\omega} U_n\) _是可数的。_

- **练习 14.2.6** (Chong 和 Yu). _证明对于任意_ \(x \ge_T 0\)_, 存在一个_ \(z \equiv_T x\) _，它是_ \(\Pi^1_1\)_-Martin-Löf 随机但不是强_ \(\Pi^1_1\)_-Martin-Löf 随机。_

## 14.3 \(\Pi^1_1\)-随机性

### 14.3.1 最大的 \(\Pi^1_1\)-零集

\(\Pi^1_1\)-随机性的概念由 Hjorth 和 Nies [51] 引入，是高阶随机性研究特有的概念。在经典随机性理论中没有此概念的类比。

**定理 14.3.1** (Kechris [64]; Stern [161]; Hjorth 和 Nies [51]). _存在一个最大的_ \(\Pi^1_1\)_-零集。_

_证明._ 定义

\(\mathcal{P} = \{(\ulcorner \varphi \urcorner, x) \mid \varphi \text{ is a ranked formula} \land \Omega(\mathfrak{A}_1^{\text{CK}}, x) \vDash \varphi(x) \land \mu(\{x \mid \Omega(\mathfrak{A}_1^{\text{CK}}, x) \vDash \neg \varphi(x)\}) \ge 1\}\)

和

\(\Omega_{\ulcorner \varphi \urcorner} = \{x \mid (\ulcorner \varphi \urcorner, x) \in \mathcal{P}\}.\)

定义

\(\Omega = \bigcup_{n < \omega} \Omega_n \cup \{x \mid \omega_1^x > \omega_1^{\text{CK}}\}.\)

我们证明 \(\Omega\) 是最大的 \(\Pi^1_1\)-零集。根据定理 13.11.1，\(\Omega\) 是 \(\Pi^1_1\)。此外，对于所有 \(n < \omega\)，\(\mu(\Omega_n) = 0\)。根据定理 13.1.4，\(\mu(\Omega) = 0\)。

如果 \(A\) 是一个 \(\Pi^1_1\)-零集，那么根据推论 3.74，存在一个算术公式 \(\varphi(x, z)\)，使得如果 \(\omega_1^x = \omega_1^{\text{CK}}\)，则 \(x \in A \Leftrightarrow \mathfrak{A}(\omega_1^x, x) \vDash (\exists y)\varphi(x, y)\)。因此，如果 \(\omega_1^x = \omega_1^{\text{CK}}\)，则对于某些 \(\beta < \omega_1^{\text{CK}}\)，\(x \in A \Leftrightarrow \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\exists y)\beta(\varphi, y^\beta)\)。由于 \(A\) 是零集，我们有

\(A \cap \{z \mid \omega_1^z = \omega_1^{\text{CK}}\} \subseteq \bigcup_{\beta < \omega_1^{\text{CK}}} \Omega_{\ulcorner (\exists y)\beta(\varphi, y^\beta) \urcorner}.\)

因此 \(A \subseteq \Omega\).

**推论 14.3.2.** _对于任意_ \(x \in 2^\omega\)_, 以下等价：_

- (i) \(x\) 是 \(\Pi^1_1\)-随机；
- (ii) \(x\) 是强 \(\Pi^1_1\)-ML 随机且 \(\omega_1^x = \omega_1^{\text{CK}}\)；
- (iii) \(x\) 是 \(\Pi^1_1\)-ML 随机且 \(\omega_1^x = \omega_1^{\text{CK}}\)。
- (iv) \(x\) 是 \(\Delta^1_1\)-随机且 \(\omega_1^x = \omega_1^{\text{CK}}\)。

_证明._ 假设 \(x\) 是 \(\Pi^1_1\)-随机。由于 \(\{z \mid \omega_1^z > \omega_1^{\text{CK}}\}\) 是一个 \(\Pi^1_1\)-零集，我们有 \(\omega_1^x = \omega_1^{\text{CK}}\)，因此 (i) \(\Rightarrow\) (ii) \(\Rightarrow\) (iii)。

根据定理 14.2.10，(iii) 蕴含 (iv)。我们现在证明 (iv) \(\Rightarrow\) (i)。根据定理 4.31 的证明，如果 \(\omega_1^x = \omega_1^{\text{CK}}\) 且 \(x \in \Omega\)，则对于某些 \(n\)，\(x \in \Omega_n\)。由于 \(\Omega_n\) 是一个 \(\Delta^1_1\)-零集，如果 \(\omega_1^x = \omega_1^{\text{CK}}\) 且 \(x\) 是 \(\Delta^1_1\)-随机，那么它是 \(\Pi^1_1\)-随机。

(i) 和 (iv) 之间的等价性也由 Stern [161] 得到。

### 14.3.2 支配与 \(\Pi^1_1\)-随机性

**引理 14.3.3.** 如果 \(x\) 是 \(\Pi^1_1\)-随机，那么它是 \(\Delta^1_1\)-支配的。

证明. 根据定理 13.3.2 的证明，对于每个 \(e \in \omega\) 和 \(n \in \omega\)，集合 \(A_{e,n} = \{x \mid (\exists f \in HYP)(\Phi_e^{f(x)} \text{ is total} \rightarrow \Phi_e^{f(x)} < f)\}\) 的测度为 1。注意 \(A_{e,n} \in \Pi^1_1\)。根据推论 13.11.1，存在一个 \(\Delta^1_1\)-集 \(\hat{A}_{e,n} \subseteq A_{e,n}\)，使得 \(\mu(A_{e,n}) = 1\)。因此，如果 \(x\) 是 \(\Pi^1_1\)-随机，则 \(x \in \hat{A}_{e,n}\)。根据推论 14.3.2，\(\omega_1^{CK} = \omega_1^x\)。因此，如果 \(g \le_T x\)，则对于某些 \(e\) 和 \(n \in \omega\)，\(g = \Phi_e^{f(x)}\)，从而证明了引理。

**命题 14.3.4** (Kjos-Hanssen, Nies, Stephan 和 Yu [68]). 对于任意 \(x \in 2^\omega\)，以下等价：

- (i) \(x\) 是 \(\Pi^1_1\)-随机；
- (ii) \(x\) 是强 \(\Pi^1_1\)-ML 随机且 \(\Delta^1_1\)-支配；
- (iii) \(x\) 是 \(\Pi^1_1\)-ML 随机且 \(\Delta^1_1\)-支配；
- (iv) \(x\) 是 \(\Delta^1_1\)-随机且 \(\Delta^1_1\)-支配；
- (v) \(x\) 是 \(\Pi^1_1\)-Kurtz 随机且 \(\Delta^1_1\)-支配。
- (vi) \(x\) 是 \(\Delta^1_1\)-Kurtz 随机且 \(\Delta^1_1\)-支配。

证明. 根据推论 14.3.2 和引理 14.3.3，我们有 (i) \(\Rightarrow\) (ii) \(\Rightarrow\) (iii) \(\Rightarrow\) (iv) \(\Rightarrow\) (v) \(\Rightarrow\) (vi)。

要证明 (vi) \(\Rightarrow\) (i)，根据推论 14.3.2，只需证明 (vi) \(\Rightarrow\) (iv)。假设 \(x\) 是 \(\Delta^1_1\)-支配且 \(\Delta^1_1\)-Kurtz 随机。令 \((U_n)_{n < \omega}\) 为一个 \(\Delta^1_1\) ML 测试。那么存在一个递归函数 \(f : \omega \times 2^{<\omega} \rightarrow \omega\)，使得对于任意对 \((n, \sigma)\)，\(\sigma \in U_n\) 当且仅当 \(f(n, \sigma) \in \omega\)。由于 \(x\) 是 \(\Delta^1_1\)-支配，\(\omega_1^x = \omega_1^{CK}\)。定义一个 \(\Pi^1_1(x)\) 关系 \(R \subseteq \omega \times \omega\)，使得

\(R(n, m) \equiv (\exists \sigma)(m \equiv \sigma \wedge f(n, \sigma) \in O_m \wedge \sigma \prec x),\)

其中 \(O_m = \{i \in \omega \mid i < |m|\}\)。根据 \(\Pi^1_1\)-一致化定理 (4.2.1)，存在一个一致化 \(R\) 的部分函数 \(p\)。由于 \(x \in \cap_n U_n\)，\(p\) 是一个全函数，因此是 \(\Delta^1_1(x)\)。由于 \(\omega_1^x = \omega_1^{CK}\)，存在一个 \(m_0 \in \omega\)，使得对于每个 \(n\)，\(p(n) \in O_{m_0}\)。定义一个 \(\Delta^1_1\)-Martin-Löf 测试 \((\hat{U}_n)_{n < \omega}\)，使得 \(\sigma \in \hat{U}_n\) 当且仅当 \(f(n, \sigma) \in O_{m_0}\)。那么 \(x \in \cap_n \hat{U}_n\)。令

\(\hat{f}(n) = \min\{l \mid (\exists \sigma \in 2^{<\omega})(\sigma \in \hat{U}_n \wedge x \prec [\sigma])\}\)

为一个 \(\Delta^1_1(x)\)-函数。那么存在一个 \(\Delta^1_1\)-函数 \(f\) 支配 \(\hat{f}\)。对于 \(n < \omega\)，定义

\(V_n = \{\sigma \mid \sigma \in 2^{\le f(n)} \wedge \sigma \in \hat{U}_n\}.\)

那么 \(P = \cap_{n \in \omega} V_n\) 是一个 \(\Delta^1_1\)-闭集，且 \(x \in P\)。因此 \(x\) 不是 \(\Delta^1_1\)-Kurtz 随机，产生矛盾。

