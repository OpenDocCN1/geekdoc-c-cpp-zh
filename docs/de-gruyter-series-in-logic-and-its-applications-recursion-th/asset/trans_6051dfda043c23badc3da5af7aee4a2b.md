

## Define

```
J_0[A] = \emptyset,
J_{\beta+1}[A] = \omega^\omega(J_\beta[A]),
J_\lambda[A] = \bigcup_{\beta<\lambda} J_\beta[A], \text{ if } \lambda \text{ is a limit ordinal.}
J[A] = \bigcup_\beta J_\beta[A]
```

如果 \( A = \emptyset \)，则我们将 \( J \) 写作 \( J[A] \)。直观地，并根据 Jensen [55]，\( J_{\beta+1} \) 是将 \( J_\beta \) 的可定义子集集合在秩中向上“拉伸” \( \omega \) 个层级而不添加新集合的结果。以下命题的证明可见 [22]。

### 命题 3.3.3. 对于所有 \(\beta\),

- \( J_\beta[A] \) 是过渡的。
- 存在一个 \(\Sigma_1\)-公式 \(\varphi(u, w)\)，使得对于任何两个序数 \( v < \beta \)，\( (J_\beta, \in) \models \varphi(v, x) \) 当且仅当 \( x = J_v \);
- 存在一个 \(\Sigma_1\)-公式 \(\varphi_\prec(u, v)\)，使得
  - (i) 对于任何 \(\beta\)，\(\varphi_\prec(u, v)\) 在 \( J_\beta \) 上定义一个良序 \( <_J \);
  - (ii) 对于任何 \( v > \beta \)，如果 \( y \in J_\beta \) 且 \( (J_v, \in) \models \varphi_\prec(x, y) \)，那么 \( x \in J_\beta \) 且 \( (J_\beta, \in) \models \varphi_\prec(x, y) \).
- 定理 3.3.2 对 \( J_\beta \) 依然成立;
- \( J_{\beta+1}[A] \cap \mathscr{P}(J_\beta[A]) = \text{Def}^\omega(J_\beta[A]) \).
- \( L_\beta[A] \subseteq J_\beta[A] \subseteq L_{\omega\beta} \).
- \( J_\beta[A] = L_\beta[A] \) 当且仅当 \( \alpha\beta = \beta \).
- \( L[A] = \bigcup_\beta J_\beta[A] \);
- 定理 3.3.2 对 \( J \) 依然有效。

Gödel 算子为构造 \( L \) 提供了一种算法化的方法。它揭示了对可定义性的引用中隐藏的“黑箱”。基于命题 3.3.3，我们可以将 \( L \) 视为在序数类上通过有效跨诱导获得的，类似于超算术集在 \( \omega_1^{\text{CK}} \) 上的定义方式。这种联系很有用，因为它表明 \( L \) 的初始段可作为一般环境下的计算模型。

## 3.3.2 紧缩与斯科伦化

如果在结构 \( \mathfrak{M} \) 内工作并执行 \( L \) 的逐阶段构造，那么当 \( \mathfrak{M} \) 满足如可接受性等足够强的条件时，对于每个 \( \beta \in M \)，都会得到相同的 \( L_\beta \)。以下定理形式化了这一思想。令 \( (L_\beta)^\mathfrak{M} \) 表示在 \( \mathfrak{M} \) 中构造的 \( L_\beta \)。

### 定理 3.3.4. 设 $\mathcal{M}$ 为 KP 的过渡模型。那么对于每个 $\beta < o(M)$，$L_\beta \in M$ 且 $(L_\beta)^\mathcal{M} = L_\beta$。

**证明.** 根据定理 3.3.2，公式 “$x = L_\beta$” 在 $\mathcal{M}` 上是 $\Delta_1`-可定义的。根据 $\Delta_0`-公式的绝对性，$L_\beta \in M` 且 $(L_\beta)^\mathcal{M} = L_\beta$。

### 推论 3.3.5. 假设 $\mathcal{M}` 是过渡的、可接受的，且 $\mathcal{M} \models \text{“V = L”}$。那么 $M = L_a$，其中 $a = o(\mathcal{M})$。

### 定理 3.3.6. $a` 是可接受的，当且仅当 $(L_a, \in)` 是可接受的。

**证明.** 如果 $(L_a, \in)` 是可接受的，那么 $a` 是可接受的。

如果对于某个可接受的 $\mathcal{M}`，$a = o(\mathcal{M})$，那么根据定理 3.3.4，对于每个 $\beta < a$ 都有 $(L_\beta)^\mathcal{M} = L_\beta$。因此，只需证明 $L_a = \bigcup_{\beta < a}(L_\beta)^\mathcal{M}` 是可接受的。我们验证 $\Delta_0`-收集在 $L_a` 中成立，并将其他性质的验证留给读者。

假设 $(L_a, \in) \models (\forall x \in a)(\exists y)\varphi(x, y)$。根据 $\Delta_0`-公式的绝对性，对于每个 $x \in a$，存在一个（最小的）$\beta < a` 使得

$\mathcal{M} \models (\exists y \in \mathcal{E}) \varphi(x, y).$

那么，定理 3.3.2 和关于 $\Sigma`-收集的定理 3.1.6 蕴含存在一个 $a_0 < a` 使得 $a \in L_{a_0}$，且

$\mathcal{M} \models (\forall x \in a)(\exists \beta < a_0)(\exists y \in L_\beta)\varphi(x, y).$

现在，$\Delta_1`-公式的绝对性给出

$(L_a, \in) \models (\forall x \in a)(\exists y)\varphi(x, y).$

那么如果 $y \in (L_a, \in) \models (\exists x \in a)\varphi(x, y)) \in L_{a_0+1}$ 且包含在 $L_a` 中。

显然，如果 $a = \omega$，那么 $L_a = \text{HF}$。因此，$L_a` 是最小的可接受集合（参见定理 3.2.4）。注意，如果 $a > \omega` 是可接受的，那么 $\omega a = a`。

$L` 的一个基本性质是以下被称为紧缩的性质：

### 定理 3.3.7. 假设 $\beta > 0` 且 $(X, \in) \prec_{\Sigma_1} (J_\beta, \in)$。那么对于某些 $\gamma \le \beta`，$(X, \in) \cong (J_\gamma, \in)$。而且，对于每个 $x \in X`，$\pi(x) \supseteq x`。

**证明.** 假设 $(X, \in) \prec_{\Sigma_1} (J_\beta, \in)$。那么 $(X, \in)` 是良基的，并满足外延公理。根据定理 3.1.12，存在一个过渡集合 $M` 使得

$\pi : (X, \in) \cong (M, \in).$

我们声称 $M = J_\gamma$，其中 $\gamma = \sup(\pi[\delta]) \in \delta \cap \text{On}$。

显然，$\langle M, \in \rangle \prec_{\Sigma_1}^{\Sigma_1} \langle J_\beta, \in \rangle` 且 $M` 是过渡的。根据命题 3.3.3，存在一个 $\Sigma_0`-公式 $\varphi(x, \delta, s)`，使得对于任何 $x \in J_\delta` 和 $\delta < \beta`，$(J_\beta, \in) \models \exists \exists \varphi(x, \delta, s)` 当且仅当 $x = J_\delta$。由于 $M` 是过渡的，通过对 $\delta < \gamma` 的归纳，我们证明对于任何 $\delta < \gamma` 都有 $J_\delta \in M`。因此 $J_\gamma \subseteq M`。

显然 $J_0 = \emptyset \in M`。如果 $\delta > 0`，那么 $\pi^{1+\delta}(\beta) < \beta`。那么 $(J_\beta, \in) \models (\exists x)(\exists s)\varphi(x, \pi^{-1}(\delta), s)`，因此 $(M, \in) \models (\exists x)(\exists s)\varphi(x, \delta, s)`。令 $x \in M` 和 $s \in M` 使得 $(M, \in) \models \varphi(x, \delta, s)`。根据 $\varphi(x, \delta, s)` 的绝对性，任何包含 $x, s` 和 $\delta` 的可接受结构 $\aleph` 都满足 $\varphi(x, \delta, s)`。根据命题 3.3.3，$J_\delta \ni x \in M`。

此外，对于任何 $x \in M`，存在一个 $\delta < \beta` 使得 $\pi^{-1}(x) \in J_\delta`。因此 $(J_\beta, \in) \models (\exists \delta)(\exists y)[(\exists s)\pi^{-1}(x) \in y \wedge \varphi(y, \delta, s)]`。那么 $(M, \in) \models (\exists \delta)(\exists y)[(\exists s)x \in y \wedge \varphi(y, \delta, s)]`。再次根据命题 3.3.3，对于某些 $\delta' < \gamma`，有 $x \in J_{\delta'}`。我们得出 $J_\gamma \supseteq M`，因此 $J_\gamma = M`。

假设对于某些 $x \in X`，有 $x <_{J_\beta} \pi(x)`。取 $x_0` 为这样的 $<_{J_\beta}`-最小集合。由于 $\pi(x_0) \in J_\beta`，所以 $x_0 \in J_\beta`，因此存在一个 $x_1 \in X` 使得 $\pi(x_1) = x_0`。如果 $x_0 <_{J_\beta} x_1`，那么 $\pi(x_0) <_{J_\beta} \pi(x_1) = x_0`，这与假设 $x_0 <_{J_\beta} \pi(x_0)` 矛盾。所以 $x_1 <_{J_\beta} \pi(x_1) = x_0`，这与选择 $x_0` 为 $<_{J_\beta}`-最小反例相矛盾。

紧缩定理（3.3.7）的一个直接后果是 $V = L` 蕴含连续统假设。我们将证明留作练习。

### 推论 3.3.8. $2^\omega \cap L = 2^\omega \cap L_\alpha$。

在可构性理论中，另一个重要工具是使用斯科伦函数。如果一个关系或函数在 $\aleph` 上是 $\Sigma_n`-可定义的（可能带有参数），则称其为 $\Sigma_n(\aleph)`-可定义的。

### 定义 3.3.9. 给定一个结构 $\mathfrak{M}`，$\aleph` 的一个 $\Sigma_n`-斯科伦函数是一个带有参数 $p \in M` 的 $\Sigma_n(\aleph)`-可定义函数 $h : \omega \times M \to M`，使得对于任何在 $\aleph` 上带有参数 $p, x \in M` 且是 $\Sigma_n`-可定义的 $A \subseteq M`，存在一个 $i \in \omega` 使得 $h(i, x) \in A$。

因此，一个 $\Sigma_n`-斯科伦函数是 $\Sigma_n`-集合的一个 $\Sigma_n`-可定义选择函数。

### 命题 3.3.10. 假设 $a > 0` 是可接受的，且 $h` 是 $(J_a, \in)` 的一个 $\Sigma_n`-斯科伦函数。那么

- (i) 对于任何 $x \in J_a`，$x \in \text{Range}(h(\omega \times \{x\}))` 且 $(\text{Range}(h(\omega \times \{x\})), \in) \prec_{\Sigma_n} (J_a, \in)`；
- (ii) 如果 $q \in J_a` 且 $X \subseteq J_a` 在有序对下封闭，那么 $X \cup \{q\} \subseteq \text{Range}(h(\omega \times (X \cup \{q\})))` 且 $(\text{Range}(h(\omega \times (X \cup \{q\}))), \in) \prec_{\Sigma_n} (J_a, \in)`。

证明。注意 (i) 验证起来很简单，是模型论中的一个标准事实。对于 (ii)，由于 $X` 在有序对下封闭，用于在 $\text{Range}(h(\omega \times (X \cup \{q\})))` 中定义有序序列的来自 $X` 的任何有限序列都可以由单个参数编码。因此，证明 $(\text{Range}(h(\omega \times (X \cup \{q\}))), \in) \prec_{\Sigma_n} (J_a, \in)` 是常规的。

我们指出，$\Sigma_n`-斯科伦函数的存在并非平凡事实。在模型论中，为结构 $\mathfrak{M}` 定义斯科伦函数需要对 $M` 进行良序。然而，在可构宇宙 $L` 中，存在一个一致的 $\Sigma_1`-可定义斯科伦函数。

