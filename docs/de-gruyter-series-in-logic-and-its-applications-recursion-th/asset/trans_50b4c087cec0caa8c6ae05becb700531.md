

根据推论 4.2.7 的证明，我们有关于 \(\Delta^1_2\)-实数的以下刻画。

**推论 4.2.8.** _实数 x 是_ \(\Delta^1_2\) _当且仅当 x 可在某个_ \(\Pi^1_1\)_-单子中递归。因此，_ \(\Delta^1_2\)_-实数的集合是_ \(\Sigma^1_2\) _。_

**推论 4.2.9** (肖恩菲尔德 [129])**.** (i) _如果_ \(A \subseteq 2^\omega\) _非空且为_ \(\Sigma^1_2\) _，则存在_ \(x \in A \cap L\) _可在某个_ \(\Pi^1_1\)_-单子中递归。_
(ii) _每个_ \(\Delta^1_2\)_-实数都是可构的。_

_证明._ (i) 如果 \(A \subseteq 2^\omega\) 是非空 \(\Sigma^1_2\)-集，则存在 \(\Pi^1_1\)-集 \(B \subseteq 2^\omega \times 2^\omega\)，使得 \(x \in A\) 当且仅当存在 _y_ 使得 _B_(_x_, _y_)。根据命题 4.2.25，存在 \(\Pi^1_1\)-单子 _B_(_x_<sub>0</sub>, _y_<sub>0</sub>)。根据推论 4.1.3，\((x_0, y_0) \in L\)。因此 \(x_0 \in A\) 是可在 \(\Pi^1_1\)-单子 \(x_0 \oplus y_0\) 中递归的可构实数。
(ii) 直接由 (i) 得出，因为每个 \(\Delta^1_2\)-实数都是 \(\Sigma^1_2\)-单子。\(\square\)

推论 4.2.9 (i) 在文献中被称为 _肖恩菲尔德绝对性引理_。集合论中有许多这样的应用。例如，给定一个 \(\Sigma^1_2\)-谓词 _P_，则 \((L, \varepsilon) \models P\) 当且仅当 \(\langle V, \varepsilon \rangle \models P\)。

## 4.2.4 练习

**练习 4.2.1.** _证明存在一个_ \(\Sigma^1_1\)_-关系_ \(R \subseteq 2^\omega \times 2^\omega\) _，该关系不能由任何_ \(\Sigma^1_1\)_-关系一致化。_

**练习 4.2.2.** _证明不存在_ \(\Pi^1_1\)_-集_ \(x \subseteq \emptyset\) _，其中_ \(<_\omega\) _限制到 x 上是序数类型为_ \(\omega_1^{CK}\) _的良序，并且存在一个部分递归函数_ \(p : \omega^2 \to \omega\) _满足练习 1.4.1 的性质_ (i)_-_(iii) _。_

**练习 4.2.3.** _从定理 4.2.1 证明定理 4.1.2。_

## 4.3 刻画稀疏 \(\Pi^1_1\)-集

如果一个集合不包含任何完美子集，则称其为 _稀疏_。存在关于 \(\Pi^1_1\)-稀疏集的可构性方面的优美刻画。

### 4.3.1 最大稀疏 \(\Pi^1_1\)-集

令 \(\mathbb{C} = \{x \mid x \in L_{\omega_1}\}\)。

**引理 4.3.1.** \(\mathbb{C}\) _是一个稀疏_ \(\Pi^1_1\)_-集。_

_证明._ \(x \in L_{\omega_1}\) 当且仅当 \((L_{\omega_1}[x], \in) \models (\exists \beta)(x \in L_\beta)\)。根据定理 3.3.2 和推论 3.7.2，C 是 \(\Pi^1_1\)。假设 \(\mathcal{C}\) 不是稀疏的。令

\(B = \{T \in 2^{<\omega} \mid T \text{ 是一个完美树，其中每条无限路径都属于 } \mathcal{C}\}.\)

那么 \(B\) 是一个 \(\Pi^1_1\)-集。根据定理 4.1.2，存在 \(T \in B\) 使得 \(T \in L_{\omega_1}\)。通过将甘迪基数定理 (2.5.3) 相对化到 \(T\)，存在一个实数 \(x \in [T] \subseteq \mathcal{C}\)，使得 \(x \not\le_h T\) 且 \(\omega_1^x \le \omega_1^{x \oplus T} = \omega_1^T\)。因此 \(x \notin L_{\omega_1}\)，矛盾。

**引理 4.3.2** (曼斯菲尔德 [87], 索洛维 [149]). 设 \(A \subseteq 2^\omega\) 为 \(\Pi^1_1\)。如果存在 \(x \in A\) 使得 \(x \notin L_{\omega_1}\)，则存在一个完美树 \(T \in L\)，其所有无限路径都属于 \(A\)。

**证明.** 令 \(\mathcal{C}\) 如前定义。假设 \(A \subseteq 2^\omega\) 是 \(\Pi^1_1\) 且存在 \(x \in A \setminus \mathcal{C}\)。令 \(\alpha_0\) 为最小序数 \(\alpha\)，使得存在 \(x \in A \setminus \mathcal{C}\) 使得 \(\alpha = \alpha_1^x\)。

令 \(T_0\) 为 \(A\) 的树表示，\(T_0^\alpha\) 按定理 4.1.2 证明中定义。由于 \(\mathcal{C}\) 是 \(\Pi^1_1\)-集，存在递归树 \(T_1 \subseteq 2^{<\omega} \times \omega^{<\omega}\)，使得 \(x \notin \mathcal{C}\) 当且仅当 \((\exists y)((x, y) \in [T_1])\)。现在令 \(T_2 \subseteq 2^{<\omega} \times \omega^{<\omega} \times 2^{<\omega}\) 为如下定义的树：\((\sigma, p, \tau) \in T_2\) 当且仅当 \((\sigma, p) \in T_0^\alpha\) 且 \((\sigma, \tau) \in T_1\)。根据假设，\(T_2\) 中存在无限路径 \((x, f, y)\)。

我们声明，对于任何 \((\sigma, p, \tau) \in T_2\)，如果 \(T_{2, (\sigma, p, \tau)} = \{(\sigma', p', \tau') \in T_2 \mid (\sigma', p', \tau') \succ (\sigma, p, \tau)\}\) 中存在无限路径，则存在 \(T_{2, (\sigma, p, \tau)}\) 中的 \((\sigma_0, p_0, \tau_0)\) 和 \((\sigma_1, p_1, \tau_1)\)，其中 \(\sigma_0\) 和 \(\sigma_1\) 不兼容，使得 \(T_{2, (\sigma_0, p_0, \tau_0)}\) 和 \(T_{2, (\sigma_1, p_1, \tau_1)}\) 都有无限路径。否则，选取 \(T_2\) 中一个使得此命题不成立的 \((\sigma, p, \tau)\)。那么 \(T_{2, (\sigma, p, \tau)}\) 中存在无限路径 \((x, f, y)\)。注意 \(\omega_1^x \ge \alpha_0\)。根据假设，对于任何 \(\sigma' \succ \sigma\) 且不是 \(x\) 的初始段，树

\(T_{2, \sigma'} = \{(\sigma'', p'', \tau'') \in T_{2, (\sigma, p, \tau)} \mid \sigma' \succ \sigma\}\)

是良基的。然后，与定理 4.1.2 证明相同，存在 \(\gamma < \omega_1^x\) 使得集合 \(\{\sigma' \mid (\exists \sigma'', p'', \tau'') \in T_{2, (\sigma, p, \tau)}\, \sigma' \subseteq \sigma''\}\) 属于 \(L_\gamma\)。因此 \(x \in L_{\gamma+1} \subseteq L_{\omega_1}\)，这与 \(x \notin \mathcal{C}\) 矛盾。

根据该声明，可以执行定理 1.1.10 的第一个构造以获得一个完美树，其所有路径都属于 \(A\)。因此集合 \(\{T \mid T \text{ 是完美的且 } [T] \subseteq A\}\) 是一个非空 \(\Pi^1_1\)-集。根据定理 4.1.2，存在完美树 \(T \in L\) 使得 \([T] \subseteq A\)。

根据引理 4.3.1 和引理 4.3.2，我们有关于最大稀疏 \(\Pi^1_1\)-集的以下刻画。

**定理 4.3.3.** \(\mathcal{C}\) 是最大稀疏 \(\Pi^1_1\)-集。

### 4.3.2 \(\mathcal{C}\) 的一些性质

由于每个实数的 \(\Pi^1_1\)-集都包含一个 \(x \in \mathcal{C}\)，且该 \(x\) 也是 \(\Pi^1_1\)-单子，人们可能会问 \(\mathcal{C}\) 中的每个实数是否都是 \(\Pi^1_1\)-单子。这是错误的，因为 \(\mathcal{C}\) 在 \(L\) 中是不可数的。

**命题 4.3.4.** 对于任何实数 \(x \in L\)，存在 \(z \in \mathbb{C}\) 使得 \(z \geq_T x\)。

证明. 令 \(x \in L\)。根据推论 3.3.8，存在 \(a < (\omega_1)^L\) 使得 \(x \in L_{a+1} \setminus L_a\)。那么对于某些 \(n\)，\(x\) 是 \(\Sigma_n(L_{a+1})\)。根据定理 3.4.11，存在实数 \(z \in L_{a+1} \setminus L_a\)，它是 \(\Sigma_n\)-主代码。因此 \(\rho_a^L = \omega\)。根据 \(\Sigma_n\)-主代码的定义，存在 \(a\) 的 \(z\)-递归良序。换句话说，\(\omega_1^x > a\)。因此 \(z \in L_{\omega_1^x}\) 且 \(x \leq_T z\)。

**命题 4.3.5.** 存在 \(x \in \mathbb{C}\)，使得其中每个 \(\Pi^1_1\)-单子都是递归的。

证明. 根据命题 4.1.3，每个 \(\Pi^1_1\)-单子都在 \(L\) 中。由于 \((L, \in) \vDash \text{ZFC}\)，陈述 "只有可数个 \(\Pi^1_1\)-单子" 在 \(L\) 中为真。因此存在实数 \(y \in L\)，使得 \(L\) 中的每个 \(\Pi^1_1\)-单子在 \(y\) 中都是递归的。根据命题 4.3.4，存在 \(z \in \mathbb{C}\) 使得 \(y \leq_T z\)。

**推论 4.3.6.** (i) \(\mathbb{C}\) 是最大可数 \(\Pi^1_1\)-实数集当且仅当 \((\omega_1)^L < \omega_1\)。 (ii) 存在不可数稀疏 \(\Pi^1_1\)-集当且仅当 \((\omega_1)^L = \omega_1\)。

证明. (i) 根据命题 4.3.4，如果 \(\mathbb{C}\) 是可数的，则 \(L \cap 2^\omega\) 是可数的。因此 \((\omega_1)^L\) 是可数的。假设 \((\omega_1)^L\) 是可数的。那么根据命题 4.3.2，每个可数 \(\Pi^1_1\)-实数集都是 \(\mathbb{C}\) 的子集。根据推论 3.3.8，\(\mathbb{C}\) 是可数的。 (ii) 由 (i) 得出。

### 4.3.3 练习

**练习 4.3.1.** 证明如果 \(\omega_1 = (\omega_1)^L\)，则不存在最大可数 \(\Pi^1_1\)-实数集。

## 4.4 \(\Sigma^1_2\)-集

实数的 \(\Sigma^1_2\)-集和 \(\Pi^1_2\)-集在多个方面相似。我们在此列举其中一些。

**推论 4.4.1.** \(2^\omega \cap L\) 是 \(\Sigma^1_2\)。

证明. 根据命题 4.3.4，\(x \in L\) 当且仅当存在 \(y \in \mathbb{C}\) 使得 \(y \geq_T x\)。

**命题 4.4.2.** \(x \leq_L y\) 是 \(\Sigma^1_2\)-关系。

证明. \(x \leq_L y\) 当且仅当 \(x, y \in L\) 且存在二元关系 \(E \subseteq \omega\)，使得

- \((\omega, E)\) 是良基的；
- \((\omega, E) \models V = L + \text{KP}\)；
- \((\omega, E) \models x \leq_L y\)。

因此关系 \(x \leq_L y\) 是 \(\Sigma^1_2\)。

