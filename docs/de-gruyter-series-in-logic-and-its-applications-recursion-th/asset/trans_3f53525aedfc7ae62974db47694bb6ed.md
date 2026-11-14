

注意，$\mathcal{P}$ 是一个 $\Pi^0_1$-关系。那么 $\mathcal{X}$ 可以由一个部分 $\Pi^0_1$-函数 $F : \omega 2^{<\omega} \times \mathscr{S} \to \mathscr{S}$ 一致化。根据假设，对于任何 $R \le T$，$\sigma \in R$ 和 $i \in \omega$，$F(R, i, \sigma)$ 有定义。利用 $F$，一个高算族 $\{P_\sigma \mid \sigma \in 2^{<\omega}\}$ 通过对 $\sigma$ 的递归定义：

$P_0 \vDash T.$

如果 $\sigma \notin P_\sigma$，令 $P_{\sigma 0} = P_{\sigma 1} = \emptyset$。否则，令 $P_{\sigma 0}$ 和 $P_{\sigma 1}$ 为比 $P_\sigma$ 更强的（即包含于 $P_\sigma$ 中的）不相容条件，且 $P_{\sigma 0} \vDash [0]$，$P_{\sigma 1} \vDash [1] = [\sigma] = \{\tau \mid \tau \prec \sigma\}$，使得 $P_{\sigma 0}, P_{\sigma 1} \vDash \lambda_{\sigma \sqcup \rho} \varphi_\rho$。

令 $Q = \bigcup_{\sigma \in P_\sigma} P_\sigma$。那么 $Q \in \mathscr{S}$。

对于每个 $i$ 和 $\sigma \in 2^{i+1}$，要么 $P_\sigma = \emptyset$，要么 $P_\sigma \Vdash \varphi_i$。假设 $\varphi_i$ 的形式为 $(\exists \beta^i)(z)$，其中 $\psi(z)$ 是有秩的。那么当 $P_\sigma \neq \emptyset$ 时，对某些 $\beta_\sigma$，有 $P_\sigma \Vdash (\exists \beta^i)\psi(z^{\beta_\sigma})$。令 $\beta = \bigcup_{\sigma \in 2^{i+1}} \beta_\sigma$。根据强制关系的定义，有 $Q \Vdash (\exists \beta^i)\psi(z^\beta)$。

$\text{故 } (\exists \beta^i)(\varphi_i(z^\beta))$。

因此，对于每个 $i$，有 $Q \Vdash \varphi_i$。

## Lemma 5.3.4. 对于任何句子 $\varphi$ 和条件 $T$，存在一个 $S \le T$，使得要么 $S \Vdash \varphi$，要么 $S \Vdash \neg \varphi$。

Proof. 如果 $\varphi$ 是无秩的，则该引理直接由定义得出。对于秩为 $\beta$ 的 $\varphi$，我们通过对 $\beta$ 进行归纳来证明该引理。不失一般性，假设 $\varphi$ 的形式为 $(\exists \beta^i)\psi(x^\beta)$，其中 $\psi$ 的秩小于 $\beta$。令 $\{\dot{\varphi}_i(n)\}_{i < \omega}$ 成为所有秩至多为 $\beta$ 且唯一自由变量为 $n$ 的公式的高算枚举。如果存在一个 $i$ 和 $S \le T$ 使得 $S \Vdash \psi(x^\beta \mid \dot{\varphi}_i)$，则证毕。否则，根据 Lemma 5.3.3 和归纳假设，存在一个 $S \le T$，使得对每个 $i$ 都有 $S \Vdash \neg \psi(x^\beta \mid \dot{\varphi}_i)$。那么 $S \Vdash \neg \varphi$。

## 5.3.2 Sacks 泛型实数

一个集合 $D \subseteq \mathscr{S}$ 称为稠密的，如果对于任何条件 $T$，存在一个 $S \in D$ 使得 $S \le T$。一个实数 $x$ 称为 Sacks 泛型的，如果对于任何在 $\emptyset$ 中可算的稠密集合 $D \subseteq \mathscr{S}$，存在一个条件 $T \in \mathscr{S}$ 使得 $x \in [T]$。注意，根据 Lemma 5.3.2 和 Lemma 5.3.4，对于任何句子 $\varphi$，集合 $D_p = \{T \in \mathscr{S} \mid T \Vdash p \text{ 或 } T \Vdash \neg p\}$ 是稠密且在 $\emptyset$ 中可算的。

## Lemma 5.3.5. 设 $x$ 为 Sacks 泛型且 $x \in [T_0] \cap [T_1]$。那么存在一个 $T \le T_0 \cap T_1$ 使得 $x \in [T]$。

Proof. 令 $i \in \{0, 1\}$。由于 $T_i$ 是高算的，存在一个有秩公式 $\varphi_i$ 使得

$(\forall \sigma)(\sigma \in T_i \leftrightarrow \mathfrak{A}(\omega_1^{\text{CK}}) \models \varphi_i(\sigma))$。

因此，对于 $i < 2$，

$(\forall i < 2)(z \in [T_i] \leftrightarrow \mathfrak{A}(\omega_1^{\text{CK}}, z) \vDash (\forall n)\varphi_i(z \upharpoonright n))$。

由于 \( x \in [T_0] \cap [T_1] \)，

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)\varphi_0(x \upharpoonright n) \wedge (\forall n)\varphi_1(x \upharpoonright n)\)。

根据 $x$ 的泛型性和有秩公式的强制定义，存在一个条件 $T$ 使得 $x \in [T]$ 且

\( T \vDash (\forall n)\varphi_0(\dot{x} \upharpoonright n) \wedge (\forall n)\varphi_1(\dot{x} \upharpoonright n)\)。

这意味着

\((\forall z)(z \in [T] \Rightarrow \mathfrak{A}(\omega_1^{\text{CK}}, z) \vDash (\forall n)\varphi_0(z \upharpoonright n) \wedge (\forall n)\varphi_1(z \upharpoonright n))\)

因此 $T \le T_0, T_1$。

## Lemma 5.5.6. 假设 $x$ 是 Sacks 泛型的。那么对于任何句子 $\varphi$，

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi \Rightarrow (\exists T)(x \in [T] \land T \Vdash \varphi)\)。

Proof. 如果 $\varphi$ 是有秩的，则根据强制定义，$(\exists T)(x \in [T] \land T \Vdash \varphi)$ 蕴含 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi\)。反之，假设 \(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi\)。$x$ 的泛型性蕴含存在一个条件 $T$ 使得 $x \in [T]$ 且要么 $T \Vdash \varphi$，要么 $T \Vdash \neg \varphi$。然后再次根据强制定义，$T \Vdash \varphi$。

如果 $\varphi$ 是无秩的，则可以像在 Theorem 5.2.4 中所做的那样，通过对 $\varphi$ 的复杂性进行归纳来证明该引理。与 Cohen 强制的唯一区别在于当 $\varphi$ 是两个句子的合取时，但这可以通过应用 Lemma 5.5.35 来解决。

## Lemma 5.5.7. 如果 $x$ 是 Sacks 泛型的，那么 \(\mathfrak{A}(\omega_1^{\text{CK}}, x)\) 满足 \(\Delta_1^1\)-理解公理，因而 \(\omega_1^x = \omega_1^{\text{CK}}\)。

Proof. 假设

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)(\exists z)\varphi(n, z) \leftrightarrow (\forall z)\psi(n, z),\)

其中 \(\varphi(n, z)\) 和 \(\psi(n, z)\) 都是可算的。

因此

\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)(\exists z)(\varphi(n, z) \vee \neg \psi(n, z))\)。

令 $T$ 为一个条件，使得

\( T \Vdash (\forall n)(\exists z)(\varphi(n, z) \vee \neg \psi(n, z))\)。

根据强制定义，

\((\forall S \le T)(\neg S \Vdash (\exists n)(\neg \exists z)(\varphi(n, z) \vee \neg \psi(n, z)))\)。

因此

\((\forall S \le T)(\forall n)(\neg S \Vdash \neg \exists z(\varphi(n, z) \vee \neg \psi(n, z)))\)，

蕴含

\((\forall P \le T)(\forall n)(\exists S \le P)(S \Vdash \exists z(\varphi(n, z) \vee \neg \psi(n, z)))\)。

根据 Lemma 5.3.3，

\((\exists S \le T)(\forall n)(S \Vdash \exists z(\varphi(n, z) \lor \neg \psi(n, z)))\)。

根据 Lemma 5.3.2，定义一个 \(\Pi^1_1$-关系 \(R \subseteq \omega \times \omega\)，使得 \(R(n, m)\) 当且仅当
\(m \in O_1 \land S \Vdash (\exists z^{|m|})(\varphi(n, z^{|m|}) \lor \neg \psi(n, z^{|m|}))\)。

根据 Theorem 4.2.1，存在一个全态 \(\Pi^1_1$ 因而也是 \(\Delta^1_1$ 的函数 $f$ 一致化 $R$。根据 Corollary 1.5.2，存在一个 $m_0 \in O_1$，使得对任何 $n$，都有 $f(n) \le m_0$，因此
\((\forall n)(S \Vdash (\exists z^{|m_0|})(\varphi(n, z^{|m_0|}) \lor \neg \psi(n, z^{|m_0|})))\)。

因此，对于任何满足 \(T \Vdash (\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))\) 的条件 $T$，存在一个 $S \le T$ 和 \(\beta < \omega_1^{\text{CK}}\)，使得
\((\forall n)(S \Vdash (\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)))\)。

令

\(\mathcal{D} = \{S \mid S \Vdash \neg(\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z)) \lor (\exists \beta < \omega_1^{\text{CK}})(S \Vdash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta)))\}\)。

那么 \(\mathcal{D}$ 是一个在 $\mathcal{O}$ 中可算的稠密条件集合。根据 $x$ 的泛型性，存在一个 $T \in \mathcal{D}$ 使得 $x \in [T]$。根据 Lemma 5.3.6 和假设，$T \Vdash \neg(\forall n)(\exists z)(\varphi(n, z) \lor \neg \psi(n, z))$。因此
\(T \Vdash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))\)

对某些 \(\beta < \omega_1^{\text{CK}}\)。根据强制定义，
\(\mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash (\forall n)(\exists z^\beta)(\varphi(n, z^\beta) \lor \neg \psi(n, z^\beta))\)。

因此，如同 Theorem 5.2.5 的证明中那样，\(\mathfrak{A}(\omega_1^{\text{CK}}, x)\) 满足 \(\Delta^1_1$ 理解公理。

## Theorem 5.3.8 (Gandy 和 Sacks [36]). 假设 $x$ 是 Sacks 泛型的且 $y \le_h x$ 不是高算的。那么 $x \le_h y$，即 $x$ 是一个最小超度的集合。

**Proof.** 假设 $y \le_h x$ 不是高算的。根据 Corollary 5.1.4 和 Lemma 5.3.7，存在一个有秩公式 $\varphi$ 使得
\((\forall n)(y(n) = i \Rightarrow \mathfrak{A}(\omega_1^{\text{CK}}, x) \vDash \varphi(n, i))\)。
根据 Lemma 5.3.6，令 $T$ 为一个条件，使得 $x \in [T]$ 且
\(T \Vdash (\forall n)(\exists i)(i < 2 \land \varphi(n, i))\)。

### Claim. 对于任何 $S \le T$，存在 $Q_i \le S$（$i < 2$）和一个 $n$，使得 $Q_i \Vdash \varphi(\bar{n}, i)$。否则，固定一个 $S$，使得对所有 $Q_i$ 和所有 $n$，都不存在 $Q_0 \Vdash \varphi(\bar{n}, 0)$ 和 $Q_1 \Vdash \varphi(\bar{n}, 1)$ 的情况。那么
\(n \in y \Leftrightarrow (\exists Q \le S)Q \Vdash \varphi(\bar{n}, 0)\)
且
\(n \notin y \Leftrightarrow (\exists Q \le S)Q \Vdash \varphi(\bar{n}, 1)\)，
根据 Lemma 5.3.2 蕴含 $y$ 是高算的，这与假设矛盾。

