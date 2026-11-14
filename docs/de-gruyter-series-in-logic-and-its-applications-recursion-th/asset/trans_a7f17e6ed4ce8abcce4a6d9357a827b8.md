

### 2.7.3 练习

- 练习 2.7.1. 证明引理 2.4.8。

- 练习 2.7.2. 证明 \( y \in \Sigma_\beta \) 当且仅当 \( |T'| \le \beta + 1 \)。

## 3 可容纳性与可构性

本章从集合论视角介绍了有效可计算性的基本概念。乍看有些抽象，但从可定义性的角度来看，它们是自然而然的。

可容纳结构本质上是一种计算的内模。可构宇宙 \( L \) 通过对 Gödel 算子的超限迭代定义。通过考虑形成可容纳结构的 \( L \) 的适当初始段，我们将看到一个 \( \Pi^1_1 \)-集合在高阶递归理论中如何扮演可枚举（r.e.）集合的角色。

### 3.1 Kripke–Platek 集合论

Kripke–Platek (KP) 集合论由 Kripke [75] 和 Platek [113] 发展而来。KP 是 ZF 公理系统的一个弱化版本，捕捉了集合论环境下有效计算的基本特征。它为超越 \( \omega \) 的领域研究提供了一个自然的平台。

### 3.1.1 KP

定义 3.1.1. 设 \( \mathscr{L} \) 表示 ZF 的语言。\( \mathscr{L} \) 中的 \( \Delta_0 \)-公式集合是最小的集合 \( X \)，由 \( \mathscr{L} \) 的原子公式组成，并在以下运算下封闭：

- (i) 若 \( \varphi \in X \)，则 \( \neg \varphi \in X \)。
- (ii) 若 \( \varphi, \psi \in X \)，则 \( \{ \varphi \land \psi, \varphi \lor \psi \} \subseteq X \)。
- (iii) 若 \( \varphi \in X \)，则 \( \{ (\forall u \in v)\varphi, (\exists u \in v)\varphi \} \subseteq X \)。

在上述 (iii) 中，公式 \( (\forall u \in v)\varphi \) 或 \( (\exists u \in v)\varphi \) 均称为 *有界公式*。形式为 \( \exists u \in v \) 或 \( \forall u \in v \) 的前缀称为 *有界量词*。\( \Delta_0 \)-公式是递归理论中 *原始递归谓词* 的类比。

定义 3.1.2. 一个 \( \Delta_0 \)-公式也称为 \( \Sigma_0 \)-公式，也称为 \( \Pi_0 \)-公式。一般来说，公式 \( \varphi(u) \) 是 \( \Sigma_{n+1} \)，如果它形式为 \( (\exists v)\psi(u, v) \)，其中 \( \psi \) 是 \( \Pi_n \)-公式。公式 \( \varphi(u) \) 是 \( \Pi_{n+1} \)，如果它形式为 \( (\forall v)\psi(u, v) \)，其中 \( \psi \) 是 \( \Sigma_n \)-公式。

定义 3.1.3. \( \Sigma \)-公式类是最小的类 \( X \)，由 \( \Delta_0 \)-公式组成，并在合取、析取、有界量化下封闭，并且若 \( \varphi \in X \) 则 \( (\exists u)\varphi \in X \)。

\( \Pi \)-公式类是最小的类 \( X' \)，由 \( \Delta_0 \)-公式组成，并在合取、析取、有界量化下封闭，并且若 \( \varphi \in X' \) 则 \( (\forall u)\varphi \in X' \)。

\( \Sigma \)-公式是经典递归理论中递归可枚举谓词的类比。请注意，\( \Sigma_1 \)-公式与 \( \Sigma \)-公式之间存在区别。\( \Sigma_1 \)-公式是 \( \Sigma \)-公式，但反之不一定成立。

### 定义 3.1.4. 理论 KP 由以下公式的全称闭合组成：

- 外延性：\((\forall x)((\forall y)((y \in u \leftrightarrow x \in u) \rightarrow x = y))\)。
- 基础公理：\((\exists x)\varphi(x) \rightarrow (\exists x)(\varphi(x) \land (\forall y \in x)\neg\varphi(y))\)，适用于所有 \(y\) 不自由出现的公式 \(\varphi\)。
- 配对公理：\((\forall x)(\forall y)(\exists z)(x \in z \land y \in z)\)。
- 并集公理：\((\forall x)(\exists y)(\forall u \in x)(\forall v \in u)(v \in y)\)。
- \(\Delta_0\)-分离公理：\((\forall x)(\exists y)(\forall u)(u \in y \leftrightarrow u \in x \land \varphi(u))\)，适用于所有 \(u\) 不自由出现的 \(\Delta_0\)-公式 \(\varphi\)。
- \(\Delta_0\)-收集公理：\((\forall x)(\forall u \in x)(\exists v)\varphi(u, v) \rightarrow (\exists y)(\forall u \in x)(\exists v \in y)\varphi(u, v)\)，适用于所有 \(y\) 不自由出现的 \(\Delta_0\)-公式 \(\varphi\)。

给定一个公式 \(\varphi\)，我们记 \(\varphi^{(w)}\) 为将 \(\varphi\) 中每个无界量词替换为限制于 \(w\) 的有界量词所得的公式。具体而言，将 \(\exists u\) 替换为 \(\exists u \in w\)，将 \(\forall u\) 替换为 \(\forall u \in w\)。显然，若 \(\varphi\) 是 \(\Sigma\)，则 \(\exists w \varphi^{(w)}\) 是 \(\Sigma\)。在 KP 下，每个 \(\Sigma\)-公式都等价于一个 \(\Sigma_1\)-公式，如下列定理所示，该定理通过对公式复杂度进行归纳证明。我们将其留作练习。

### 定理 3.1.5（\(\Sigma\)-反射原理）。设 \(\varphi\) 为一个 \(\Sigma\)-公式。则

\(\text{KP} \vdash \varphi \rightarrow (\exists w) \varphi^{(w)}\)。

因此，该定理断言在 KP 下，对于给定的 \(\Sigma\)-公式，存在一个 \( \Delta_0 \)-可定义集合。事实上，它还说明了更多：

### 定理 3.1.6（\(\Sigma\)-收集原理）。设 \(\varphi\) 为一个 \( \Sigma \)-公式，\( a \) 为一个集合。则

\(\text{KP} \vdash (\forall x \in a)(\exists y) \varphi(x, y) \rightarrow (\exists w)((\forall x \in a)(\exists y \in w) \varphi(x, y) \land (\forall y \in w)(\exists x \in a) \varphi(x, y))\)。

证明。假设 \((\forall x \in a)(\exists y) \varphi(x, y)\)。那么公式 \((\forall x \in a)(\exists y) \varphi(x, y)\) 是 \( \Sigma \)。根据定理 3.1.5，存在一个集合 \( c \)，使得 \((\forall x \in a)(\exists y \in c) \varphi^{(c)}(x, y)\)。定义 \( b = \{y \mid (\exists x \in a) \varphi^{(c)}(x, y)\} \)。根据 \(\Delta_0\)-分离公理，这样的 \( b \) 存在。可以直接验证 \( \varphi^{(c)}(x, y) \) 蕴含 \( \varphi(x, y) \)，因为 \( \varphi(x, y) \) 是 \( \Sigma \)。故 \((\forall y \in b)(\exists x \in a) \varphi(x, y)\)。由于 \((\forall x \in a)(\exists y \in c) \varphi^{(c)}(x, y)\)，我们实际上有 \((\forall x \in a)(\exists y) \varphi^{(c)}(x, y)\)。由此可得 \((\forall x \in a)(\exists y \in b) \varphi^{(c)}(x, y)\)。

### 定理 3.1.7（\(\Delta\)-分离原理）。设 \( a \) 为一个集合。对于任意 \( \Sigma \)-公式 \( \varphi(x) \) 和 \( \Pi \)-公式 \( \psi(x) \)，

\(\text{KP} \vdash (\forall x \in a)(\varphi(x) \leftrightarrow \psi(x)) \rightarrow (\exists w)(\forall x)(x \in w \leftrightarrow x \in a \land \varphi(x))\)。

证明。假设 \((\forall x \in a)(\varphi(x) \leftrightarrow \psi(x))\)。则 \((\forall x \in a)(\varphi(x) \lor \neg \psi(x))\)。注意公式 \( \varphi(x) \lor \neg \psi(x) \) 是 \( \Sigma \)。根据定理 3.1.5，存在一个集合 \( c \)，使得 \((\forall x \in a)(\varphi(x) \lor \neg \psi(x)) \leftrightarrow (\forall x \in a)(\varphi^{(c)}(x) \lor \neg \psi^{(c)}(x))\)。定义 \( b = \{y \mid y \in a \land \varphi^{(c)}(y)\} \)。根据 \(\Delta_0\)-分离公理，这样的 \( b \) 存在。

若 \( y \in b \)，则 \( y \in a \land \varphi^{(c)}(y) \)，进而 \( y \in a \land \varphi(y) \)，因为 \( \varphi(y) \) 是 \( \Sigma \)。若 \( y \in a \land \varphi(y) \)，则 \( y \in a \land \psi(y) \)，进而 \( y \in a \land \psi^{(c)}(y) \)，因为 \( \psi \) 是 \( \Pi \)。

### 3.1.2 通过 \( \Sigma \)-递归定义

如第 1 章和第 2 章所示，使用有效超限归纳的递归定义是二阶算术中的一个强大工具。我们现在在可容纳集合论的环境下研究递归定义。这可以被视为对 \( \omega^{CK} \) 上递归的推广。

回顾，集合 \( x \) 是传递的，如果 \((\forall y)(\forall z)(y \in x \land z \in y \rightarrow z \in x)\)。注意，公式 "\( x \) 是传递的" 是 \( \Delta_0 \)。

函数 \( f \) 是 \( \Sigma \)，如果存在一个 \( \Sigma \)-公式 \( \varphi \)，使得 \( f(x) = y \leftrightarrow KP \vdash \varphi(x, y) \)。根据定理 3.1.5，\( f \) 由一个 \( \Sigma_1 \)-公式定义。不难看出，若 \( f \) 是 \( \Sigma \)，则对于任意集合 \( u \)，\( KP \vdash (\exists y)(v = f \upharpoonright u) \)，其中 \( f \upharpoonright u = \{(x, y) \mid f(x) = y \land x \in u\} \)。

### 定理 3.1.8。

设 \( G \) 是一个 \( n+2 \) 元 \( \Sigma \)-函数。存在一个 \( n+1 \) 元 \( \Sigma \)-函数 \( F \)，使得

```
KP \vdash F(y, x_1, \dots, x_n) = G(y, x_1, \dots, x_n, \langle z, F, x_1, \dots, x_n \rangle \mid z \in y).
```

证明。为简化起见，假设 \( n = 0 \)。设 \( P(f) \) 为句子：

```
f \text{ is a function } \land \text{Dom}(f) \text{ is transitive } \land
(\forall y \in \text{Dom}(f))(y = G(y, \langle z, f(z) \rangle \mid z \in y)).
```

注意 \( P(f) \) 是一个 \( \Sigma \)-公式。定义

```
Q(y, z) = (\exists f)(P(f) \land f(y) = z),
```

以及

```
F(y) = z \Leftrightarrow Q(y, z).
```

只需证明

```
KP \vdash F \text{ is a function } \land (\forall y)(\exists z)Q(y, z).
```

我们证明 KP \( \vdash (\forall y)(\exists z)Q(y, z) \)。另一个合取式可以用类似的论证来证明。假设 KP 不能证明 \( (\forall y)(\exists z)Q(y, z) \)。那么存在 KP 的一个模型 \( \mathcal{M} = \langle M, \in \rangle \)，使得 \( \mathcal{M} \models (\exists y)(\forall z)\neg Q(y, z) \)。根据基础公理，选择 \( y \) 使得

```
\mathcal{M} \models (\forall z)\neg Q(y, z) \land (\forall y' \in y)(\exists z)Q(y', z).
```

