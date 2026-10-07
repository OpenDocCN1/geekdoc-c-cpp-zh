
### 示例 8.12
考虑在阿贝尔群 `$G$` 上的代数电路。任何此类电路都定义了一种形式 `$(x_1, \dots, x_{in}) \mapsto x^{a_1} \dots x^{a_{in}}$`，对应某些整数 `$(a_1, \dots, a_{in})$`。

### 示例 8.13
考虑在域 `$F$` 上的代数电路。一个在 `$(+, \cdot)$` 上的 `$(l_{in}, 1)`-代数电路定义了一种从 `$F[X_1, \dots, X_{in}]$` 中计算多元多项式的特定方法。代数电路中路径的长度是路径上内部顶点的数量。代数电路中路径的 `op`-长度是内部顶点的数量。

### 8.3.1 群同态加密系统

存在一类较大的加密系统具有相同的抽象结构，尽管底层的群结构非常不同。这些方案具有实际应用。

- 示例 8.14. 如示例 8.11 定义的 `ElGamal` 是一个群同态加密系统。密文空间是 `$G$`。一个 `$(l_{in}, l_{out})`-电路 `C` 具有输入和输出顺序，定义了函数 `C : S^{in} \to S^{out}`...（此处原文已截断且重复）

# 公开钥加密 ■ 255

示例 8.15。设如第 3.3.2 节定义的、以可逆元素为明文集的 `RSA` 是具有群同态性的。对于加密密钥 `$(n, e)$`，该群为 `$Z_n^*$`，解密映射是一个群自同。

示例 8.16。设 `n` 为两个质数 `p` 和 `q` 的乘积，使得 `$(p-1)/2` 和 `$(q-1)/2` 均为奇数。那么 `-1` 模 `p` 和 `q` 均具有勒让符号，因此 `-1` 是模 `n` 的二次非剩余数。

`Goldwasser-Micali` 密文系统的工作原理如下：

- 密钥生成算法按上所述生成 `RSA` 模 `n=pq`，并输出 `ek=n` 和 `dk=(p,q)`。
- 加密算法以 `ek=n` 和 `m \in \{-1, 1\}` 为输入，采样 `r \leftarrow Z_n^*` 并计算密文 `c \leftarrow r^2(-1)^m`。
- 解密算法以 `dk=p` 和 `c \in Z_n^*` 为输入。如果 `(\frac{c}{p})=1`，则输出 `m`，否则输出 `\perp`。

练习 8.33。证明 `Goldwasser-Micali` 密文系统是群同态的，并识别明文群。

示例 8.17。设 `n` 为两个质数 `p` 和 `q` 的乘积，使得 `gcd(n, (p-1)(q-1))=1`。那么 `n` 模 `$(p-1)(q-1)$` 可逆。`Paillier` 密文系统的工作原理如下：

- 密钥生成算法按上所述生成 `RSA` 模 `n=pq, d \leftarrow (p-1)(q-1)`，并输出 `ek=n` 和 `dk=n`。
- 加密算法以 `ek=n` 和 `m \in Z_n` 为输入，采样 `r \leftarrow Z_n^*` 并计算密文 `c \leftarrow r^n(1+n)^m`。
- 解密算法以 `dk=n` 和 `c \in Z_n^*` 为输入，并计算 `t \leftarrow c^d \pmod n^2`，`t' \leftarrow (t-1)/n`（在整数上）以及 `m \leftarrow t^{-1} \pmod n`。

练习 8.34。证明 `Paillier` 密文系统是群同态的，并识别明文群。

上述方案都是群同态的，并且对于所有密文空间和明文空间具有群结构，解密映射计算出一个群同态。这些方案具有非常良好的代数结构，事实上它们可以推广到一个抽象的密文系统中。

示例 8.18。考虑一个族 `\mathcal{F}=\{(G, H, \mathbb{P}, \phi_0, \phi_1)\}`,，其中 `G` 和 `\mathbb{P}` 是有限阿贝尔群，`H` 是 `G` 的子群，`\phi_0:G \to \mathbb{P}` 和 `\phi_1:G \to \mathbb{P}` 是同态，使得 `\phi_1 \circ \phi_0` 是 `\mathbb{P}` 上的恒等映射，且 `\phi_1=H`。我们假设描述足够从 `G` 和 `H` 中的均匀概率空间中采样。我们还假设存在一个采样算法 `K_0`，输出 `\mathfrak{K}` 中的一个元素。

群同态公钥加密系统 `PKE_{\mathfrak{K}} = (\mathcal{K}, \mathcal{E}, \mathcal{D})` 为：

- 密钥生成算法 `\mathcal{K}` 采样 `$(G, H, \mathfrak{P}, \phi_0) \leftarrow` 输出 `ek = (G, H, \mathfrak{P}, \phi_0)` 和 `dk = (G, \mathfrak{P}, \phi_1)`。
- 加密算法接受输入 `ek = (G, H, \mathfrak{P}, \phi_0)` 和 `m \in \mathfrak{P}`。它采样 `r \leftarrow H` 并计算 `c = r\phi_0(m)`。输出为 `c`。
- 解密算法接受输入 `dk = (G, \mathfrak{P}, \phi_1)` 和 `c \in G`。它计算 `m = \phi_1(c)` 并输出 `m`。

由于这里 `r \in H`，对于 `\phi_1` 我们有 `\phi_1(r\phi_0(m)) = (\phi_1 \circ \phi_0)(m) = m`。也就是说，我们有一个公钥加密系统，由于 `\phi_0` 和 `\phi_1` 是同态的，它是群同态的。我们需要 `\mathfrak{K}' = \{G, H, \mathfrak{P}, \phi_0\}`，这与 `\mathfrak{K}` 相同，除了 `\phi_1` 被忘记了。相应的采样算法 `\mathcal{K}_0` 使用 `K_0` 采样 `$(G, H, \mathfrak{P}, \phi_1)$` 并输出 `$(G, H, \mathfrak{P}, \phi_0)$`。

练习 8.35。证明示例 8.11, 8.16 和 8.17 都是示例 8.18 中抽象同态密文系统的特例。对于每个示例，描述该族 `\mathfrak{K}`、如何从群中采样以及如何求同态的值。该密文系统的核心思想是 `H = \ker \phi_1` 充当隐藏消息的噪声，这可以通过同态 `\phi_1` 移除。如果我们能够将 `H` 的加密与不在子群中的元素区分来，我们就可以区分恒元的加密与非恒元的加密。反之亦然。

**定义 8.9.** 设 `\mathfrak{S} = \{(S, T, aux)\}` 是一个元组族，其中 `S` 是一个集合，`T` 是 `S` 的子集，`aux` 是某些信息。我们假设描述足够在 `S` 和 `T` 上的均匀概率空间上进行采样。设 `K_{\alpha}` 为输出 `\mathfrak{S}` 中一个元素的算法。子集成员性问题 `(\mathfrak{S}, K_{\alpha})` 的 `\tau`-区分别器 `A` 是一个与图 8.4 中的实验交互的算法，其中区分别器和实验的运行时间最多为 `\tau`。区分别器的*优势*定义为

`Adv_{\mathfrak{S}, K_{\alpha}}^{lmp}(A) = Pr[E],`

子集成员性问题的区分实验如下，对抗者 `\mathcal{A}`:

1. 计算 `$(S, T, aux) \leftarrow \mathcal{K}_0$` 并采样 `b \leftarrow \{0,1\}`。如果 `b=0`，采样 `s \in S`。否则，采样 `s \in T`。
2. 将 `$(S, T, aux, s)$` 发给 `\mathcal{A}`。

最终输出 `b' \in \{0,1\}`。

**图 8.4** 实验 `Exp_{smp}^{\mathcal{K}_0}(\mathcal{A})` 用于子集成员性问题，其中 `\mathcal{A}` 的输出 `b'` 等于挑战位 `b`。

对于 `\mathcal{K}_0` 采样的 `$(S, T, aux)$`，`S` 是一个群且 `T` 是 `S` 的子群，则称 `(\mathfrak{g}, \mathcal{K}_0)` 为子群成员性问题。

**定理 8.18.** `\mathfrak{g}', \mathcal{K}'_0` 和 `PKE` 如示例 8.18 所示。设 `\mathcal{A}` 是针对 `PKE` 的 `(\tau, 1, 0)`-真实或随机对抗者。则存在针对子群成员性问题 `(\mathfrak{g}', \mathcal{K}'_0)` 的 `\tau'`-区分别器 `\mathcal{B}`，其中 `\tau'` 几乎等于 `\tau`，且 `Adv_{smp}^{\mathcal{K}_0}(\mathcal{B}) = Adv_{PKE}(\mathcal{A})`。

同样，设 `\mathcal{B}'` 是 `(\mathfrak{g}, \mathcal{K}_0)` 的 `\tau''`-区分别器。则存在针对 `PKE` 的 `(\tau''', 1, 0)`-真实或随机对抗者 `\mathcal{A}'`，其中 `\tau''` 几乎等于 `\tau`，且 `Adv_{PKE}(\mathcal{A}') = Adv_{smp}^{\mathcal{K}_0}(\mathcal{B}')`。

以下结果足以建立特征群 `\mathfrak{G}` 的结构，这是证明该定理的关键。

**引理 8.19.** 设 `\mathfrak{g}` 如示例 8.18 所示，且 `$(G, \mathfrak{H}, \mathfrak{P}, \phi_0, \phi_1) \in \mathfrak{g}$`。对于任意 `c \in G`，存在唯一的对 `$(r, m) \in H \times \mathfrak{P}$` 使得 `c = r\phi_0(m)`。

练习 8.36。使用上述引理证明定理 8.18。

## 8.4 承诺方案

有时 Alice 需要在某个时间点做出决定。Alice 需要对她的决定保密，但同时，Bob 必须能够确保她不会改变主意。

我们通过承诺方案（commitment schemes）来实现这一点，该方案允许 Alice 通过向 Bob 提供一个承诺来承诺某个值，稍后通过打开该承诺来说服 Bob 她确实承诺了该值。对于某些方案，Alice 和 Bob 需要从一个公共引用字符串获取一个承诺密钥。

**定义 8.10.** 一个承诺方案由三个算法 `$(CK, CC, CO)$` 组成：

- 密钥生成算法 `CK` 不接受输入并输出一个承诺密钥 `ck`。明文集 `\mathcal{P}` 与承诺密钥 `ck` 关联。
- 算法 `CC` 以承诺密钥 `ck` 和消息 `m \in \mathcal{P}` 为输入，并输出一个承诺 `u` 和一个开示值（opening） `o`。
- 验证算法 `CO` 以承诺密钥 `ck`、消息 `m \in \mathcal{P}` 和开示值 `o` 为输入，并输出 0 或 1。

对于由 `CC` 输出的任何承诺密钥 `ck`，任何消息 `m \in \mathcal{P}` 以及 `CC` 在输入 `ck` 和 `m` 时输出的任何承诺 `u` 和开示值 `o`，我们有：

```
CO(ck, u, m, o) = 1.
```

备注。某些承诺方案不需要承诺密钥，此时 `CK` 输出空字符串。在这种情况下，我们通常省略承诺方案和密钥生成算法。

我们首先考虑五种承诺方案，其中三个基于哈希函数，一个基于公钥加密系统，一个基于循环群。

**示例 8.20.** 令 `h: \mathcal{P} \to S` 为哈希函数。没有承诺密钥。要承诺消息 `m`，我们计算承诺 `u \leftarrow h(m)`。要验证 `u` 是对 `m` 的承诺，检查 `u = h(m)`。

**示例 8.21.** 令 `h: \mathcal{P} \to \mathbb{Z}_n^+` 为哈希函数。没有承诺密钥。要承诺消息 `m`，采样 `o \leftarrow \mathbb{Z}_n^+` 并计算承诺 `u \leftarrow h(m) + o`。开示值为 `o`。

要验证 `o` 是 `u` 的开示值，检查 `u = h(m) + o`。

**示例 8.22.** 令 `h: T \times \mathcal{P} \to \mathcal{B}` 为哈希函数。没有承诺密钥。要承诺消息 `m`，采样 `o \leftarrow T` 并计算承诺 `u \leftarrow h(o, m)`。开示值为 `o`。

要验证 `o` 是 `u` 的开示值，检查 `u = h(o, m)`。

**示例 8.23.** 令 `(\mathcal{K}, \mathcal{E}, \mathcal{D})` 为一个公钥加密系统。将类似于 `\mathcal{E}` 的概率算法视为一个确定性算法，它以公钥 `ek`、`m` 以及其随机性 `r` 为输入。我们将该确定性算法记为 `\mathcal{E}_{ek}(m,r)`。

生成承诺密钥：`$(ek, dk) \leftarrow \mathcal{K}$` 并令 `ck = ek`。

要承诺消息 `m`，采样随机性 `o` 并计算承诺 `u = \mathcal{E}_{ek}(m,o)`。开示值为 `o`。

要验证 `o` 是 `u` 对 `m` 的开示值，检查 `u = \mathcal{E}_{ek}(m,o)`。

**示例 8.24.** 这是 *Pedersen* 承诺方案。令 `G` 为一个阶为 `n` 的循环群。生成承诺密钥：采样两个非单位群元素 `g` 和 `h`。承诺为 `ck = (g,h)`。

要承诺消息 `m \in \{0, 1, \dots, n-1\}`,采样 `o \leftarrow \{0, 1, \dots, n-1\}` 并计算承诺 `u \leftarrow g^m h^o`。开示值为 `r`。

要验证 `o` 是 `u` 对 `m` 的开示值，检查 `u = g^m h^o`。

*练习 8.37.* 证明上述五个示例都是承诺方案。

承诺方案具有双向保密性要求。承诺不能向 Bob 暴露任何关于消息的信息。此外，Alice 不可能改变她对承诺内容的意图。

**示例 8.25.** 考虑示例 8.20 中的承诺方案。当 Bob 得到 `u` 时，他只需检查 `u` 是否等于 `h(m)`，就可以判断出 Alice 是否承诺了消息 `m`。

**示例 8.26.** 考虑示例 8.21 中的承诺方案。当 Alice 拥有消息 `m` 的承诺 `u` 开示值为 `o` 时，对于任何消息 `m'`，值 `o' = o \cdot h(m-m')` 是 `u` 对 `m'` 的开示值。

**定义 8.11.** 考虑承诺方案 `COM = (CK, CO)`。针对隐藏性（hiding）的 `(\tau, \ell_c)`-对手是一个交互算法 `\mathcal{A}`，它与图 8.5 中的实验 `Exp_{COM}^{hide}(\mathcal{A})` 交互，最多提出 `\ell_c` 次挑战，且运行时间为 `\tau`。针对绑定性（binding）的 `\tau`-对手是一个交互算法 `\mathcal{A}`，它与图 8.5 中的实验 `Exp_{COM}^{bind}(\mathcal{A})` 交互，且运行时间最多为 `\tau`。

对手隐藏性和绑定性的优势为：

`Adv_{COM}^{hide}(A) = 2|Pr[E] - 1/2|`

`Adv_{COM}^{bind}(A) = Pr[F]`,

其中 `E` 是 `Exp_{COM}^{hide}(\mathcal{A})` 中 `b = b'` 的事件，`F` 是 `m_0 \neq m_1` 且在 `Exp_{COM}^{bind}(\mathcal{A})` 中 `CO(ck, u, m_1, o_1) = 1` 的事件。

对手 `\mathcal{A}` 的实验 `Exp_{COM}^{hide}(\mathcal{A})` 步骤如下：

1. 采样 `b \leftarrow \{0,1\}`。
2. 计算 `ck \leftarrow CK` 并将 `ck` 发给 `\mathcal{A}`。
3. 当发送查询 `m_0, m_1`（挑战）时：
   (a) 计算 `$(u, o) \leftarrow CC(ck, m_b)$` 并将 `u` 发给 `\mathcal{A}`。

最终，对手输出 `b'`。

对手 `\mathcal{A}` 的实验 `Exp_{COM}^{bind}(\mathcal{A})` 步骤如下：

1. 计算 `ck \leftarrow CK` 并将 `ck` 发给 `\mathcal{A}`。

最终，对手输出 `u, m_0, o_0` 和 `o_1`。

图 8.5 承诺方案 `CM=(CK, CO)` 的定义实验

我们定义了计算隐藏。如果对于任何承诺 `ck` 和任意两个不同的消息 `m_0, m_1 \in \mathcal{M}`，`CC(ck, m_i)` 产生的概率是 `\epsilon`-接近，则具有统计隐藏。如果它们是 `0`-接近，则具有完美隐藏。我们还定义了计算绑定。如果任何对手的优势均为 0，则具有无条件绑定。

在其他条件相同的情况下，无条件的优于统计的，统计的优于计算。

**练习 8.38.** 证明如果承诺方案是完美隐藏的，则任何对手的优势为 0。此外，如果承诺方案是统计隐藏且边界为 `\epsilon`，则任何对手的优势为 `2\epsilon`。

**练习 8.39.** 证明承诺方案是无条件绑定的，当且仅当对于任何承诺存在一个从承诺集到消息集的函数 `f_{ck}`，使得对于所有消息 `m`，都有 `f_{ck}(CC(ck, m)) = m`。该函数不易计算。
