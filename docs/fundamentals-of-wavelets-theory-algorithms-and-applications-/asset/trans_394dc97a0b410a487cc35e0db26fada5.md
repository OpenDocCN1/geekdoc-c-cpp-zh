

$$x_s(t) = \sum_k a_{k,s} \phi(2^s t - k),$$ (5.5)

且任何函数 $y_s(t) \in W_s$ 可表示为

$$y_s(t) = \sum_k w_{k,s} \psi(2^s t - k),$$ (5.6)

其中系数 $\{a_{k,s}\}_{k \in \mathbb{Z}}, \{w_{k,s}\}_{k \in \mathbb{Z}} \in \mathbb{R}$。

由于

$$
\begin{aligned}
A_{s+1} &= W_s \oplus A_s \\
&= W_s \oplus W_{s-1} \oplus A_{s-1} \\
&= W_s \oplus W_{s-1} \oplus W_{s-2} \oplus \cdots
\end{aligned}
$$ (5.7)

我们有

$$A_s = \oplus_{\ell = -\infty}^{s-1} W_\ell.$$

观察到 $\{A_s\}$ 是嵌套的，而 $\{W_s\}$ 是两两正交的。因此，我们有

$$
\begin{cases}
A_\ell \cap A_m = A_\ell; m \ge \ell \\
W_\ell \cap W_m = \{0\}; \ell \ne m \\
A_\ell \cap W_m = \{0\}; \ell \le m.
\end{cases}
$$

$A_s$ 和 $W_s$ 的层次结构示意图如图 5.2 所示。

## 图 5.2：MRA 子空间的分割。

![](img/f73ae67732328dc36596b27ffe8d0152_188_0.png)

## 5.2 正交、双正交和半正交分解

在第 5.1 节中，我们对小波子空间 \(\boldsymbol{W}_s\) 的唯一要求是它是 \(\boldsymbol{A}_{s+1}\) 中 \(\boldsymbol{A}_s\) 的补空间。除此之外，如果还要求 \(\boldsymbol{W}_s \perp \boldsymbol{A}_s$，则这种分解称为 *正交分解*。让我们进一步解释 \(\boldsymbol{A}_s\) 和 \(\boldsymbol{W}_s\) 的正交性。为简单起见，令 \(s = 0\)。在这种情况下，\(\{\phi(t - k) : k \in \mathbb{Z}\}\) 张成 \(\boldsymbol{A}_0\)；同样，\(\{\psi(t - k) : k \in \mathbb{Z}\}\) 张成 \(\boldsymbol{W}_0\)。那么 \(\boldsymbol{A}_0 \perp \boldsymbol{W}_0\) 意味着

(5.8) \(\int_{-\infty}^{\infty} \phi(t)\psi(t - \ell)dt = 0 \quad \text{for all } \ell \in \mathbb{Z}.\)

一般来说，\(\{\phi(t-k) : k \in \mathbb{Z}\}\) 和 \(\{\psi(t-k) : k \in \mathbb{Z}\}\) 本身不一定正交；即，

(5.9) \(\int_{-\infty}^{\infty} \phi(t)\phi(t-\ell) dt \neq 0\)

(5.10) \(\int_{-\infty}^{\infty} \psi(t)\psi(t-\ell) dt \neq 0.\)

让我们放宽 \(\boldsymbol{A}_s\) 和 \(\boldsymbol{W}_s\) 彼此正交的条件，并假设小波 \(\psi_{k,s} \in \boldsymbol{W}_s\) 有一个对偶 \(\tilde{\psi}_{k,s} \in \tilde{\boldsymbol{W}}_s\)。对偶性意味着双正交条件得到满足；即

(5.11) \(\langle \psi_{k,j}, \tilde{\psi}_{m,\ell} \rangle = \delta_{k,m} \cdot \delta_{j,\ell}, \quad j, k, \ell, m \in \mathbb{Z}.\)

虽然我们不要求 \(\boldsymbol{W}_s \perp \boldsymbol{A}_s\)，但我们确实需要 \(\tilde{\boldsymbol{W}}_s \perp \boldsymbol{A}_s\)，其重要性将在后面变得清晰。

与双小波 \(\tilde{\psi}_{k,s}\) 类似，我们还考虑一个双标度函数 \(\tilde{\phi}_{k,s}\)，它生成 \(L^2\) 的另一个 MRA \(\{\tilde{\boldsymbol{A}}_s\}\)。换句话说，\(\phi_{k,s}\) 和 \(\psi_{k,s}\) 与 MRA \(\{\boldsymbol{A}_s\}\) 相关联，而 \(\tilde{\phi}_{k,s}\) 和 \(\tilde{\psi}_{k,s}\) 与 MRA \(\{\tilde{\boldsymbol{A}}_s\}\) 相关联。

在解释其重要性之前，让我们先总结迄今为止的结果。

### MRA \(\{\boldsymbol{A}_s\}$$

$$
\left\{\begin{array}{ll} A_{s+1} & = A_s + W_s; \\ A_r \cap A_m & = A_r; m \ge \ell \\ W_r \cap W_m & = \{0\}; \ell \neq m \\ A_r \cap W_m & = \{0\}; \ell \le m. \end{array}\right.
$$

### MRA \(\{\tilde{A}_s\}$$

$$
\left\{\begin{array}{ll} \tilde{A}_{s+1} & = \tilde{A}_s + \tilde{W}_s; \\ \tilde{A}_r \cap \tilde{A}_m & = \tilde{A}_r; m \ge \ell \\ \tilde{W}_r \cap \tilde{W}_m & = \{0\}; \ell \neq m \\ \tilde{A}_r \cap \tilde{W}_m & = \{0\}; \ell \le m. \end{array}\right.
$$

$$
\left\{\begin{array}{l} W_s \perp \tilde{A}_s \Rightarrow \tilde{A}_r \cap W_m = \{0\} \text{ for } \ell \le m \\ \tilde{W}_s \perp A_s \Rightarrow A_r \cap \tilde{W}_m = \{0\} \text{ for } \ell \le m. \end{array}\right.
$$

迄今讨论的分解过程称为双正交分解。为了理解其重要性，让我们简要说明将函数分解为各个尺度的过程，如图 5.1 所示。详细内容留待第 7 章。

给定一个函数 \(x(t) \in L^2\)，分解为各个尺度首先将函数映射到足够高分辨率的子空间 \(A_M\)，即，

(5.12) \(L^2 \ni x(t) \mapsto x_M = \sum_k a_{k,M} \phi(2^M t - k) \in A_M.\)

现在由于

$$
\begin{aligned}
A_M &= W_{M-1} + A_{M-1} \\
&= W_{M-1} + W_{M-2} + A_{M-2} \\
&= \sum_{n=1}^N W_{M-n} + A_{M-N},
\end{aligned}
$$

(5.13)

我们可以写成

\( x_M(t) = \sum_{n=1}^N y_{M-n}(t) + x_{M-N}(t) \)

(5.14)

其中 \( x_{M-N}(t) \) 是 \( x_M(t) \) 的最粗糙近似，且

\( x_s(t) = \sum_k a_{k,s} \phi(2^s t - k) \in A_s \)

(5.15)

\( y_s(t) = \sum_k w_{k,s} \psi(2^s t - k) \in W_s \)

(5.16)

现在双小波的重要性变得清晰了。通过使用双正交条件 (5.11)，我们可以得到系数 \(\{w_{k,s}\}\) 为

\( w_{k,s} = 2^s \int_{-\infty}^{\infty} y_s(t) \tilde{\psi}(2^s t - k) dt. \)

(5.17)

回顾 \(\tilde{\psi}(2^s t - k) \in \tilde{W}_s\) 且当 \(t \le s\) 时 \(A_t \perp \tilde{W}_s\)。因此，通过对 (5.14) 与 \(\tilde{\psi}_{k,s}(t)\) 取内积并使用条件 (5.11)，我们有

$$
\begin{aligned}
w_{k,s} &= 2^s \int_{-\infty}^{\infty} x_M(t) \tilde{\psi}(2^s t - k) dt \\
&= 2^{s/2} W_{\psi} x_M \left( \frac{k}{2^s}, \frac{1}{2^s} \right).
\end{aligned}
$$

(5.18)

双小波 \(\tilde{\psi}\) 可用于通过在所需时间-尺度位置计算函数 \(x_M\) 的积分小波变换来分析该函数，而 \(\psi\) 可用于在任何尺度下获得其函数表示。因此，我们称 \(\tilde{\psi}\) 为分析小波，而 \(\psi\) 称为合成小波。

当然，如果我们有正交分解 \(A_s \perp W_s\) 且正交正规基 \(\{\phi, \psi\}\)，则分析小波和合成小波相同。请注意，当我们说正交正规 (o.n.) 小波时，这意味着小波不仅在尺度上正交，而且在给定尺度上关于平移也正交。但正交正规标度函数意味着标度函数仅在给定尺度上关于平移正交正规；由于 MRA 的嵌套性质，不在尺度上正交正规。

出现的一个问题是，为什么我们需要双正交 (b.o.) 小波？与正交情况中由单个函数承担分析和合成职责相比，在双正交情况下将分析和合成职责委托给两个不同函数的一个吸引人的特点是，在前者中，我们可以具有紧支持的对称分析和合成小波及标度函数，这是连续 o.n. 基无法实现的。此外，o.n. 标度函数和小波的时间-尺度定位性较差。

在后续章节中将讨论的一些应用中，我们需要交换分析和合成对 \(\{\phi, \psi\}\)、\(\{\tilde{\phi}, \tilde{\psi}\}\) 的角色。在 b.o. 分解中，我们无法轻易做到这一点，因为 \(\phi\) 和 \(\tilde{\phi}\) 分别生成两个不同的 MRA，\(A\) 和 \(\tilde{A}\)。为了进行这种交换，我们需要将给定函数 \(x \mapsto \tilde{x}_M \in \tilde{A}_M\) 映射，然后我们可以使用 \(\psi\) 作为分析小波和 \(\tilde{\psi}\) 作为合成小波。

除了 b.o. 和 o.n. 分解之外，还有一类称为 *半正交分解* 的分解，其中 \(A_s \perp W_s\)。由于在这个系统中，标度函数和小波是非正交的，我们仍然需要它们的对偶 \(\tilde{\phi}\) 和 \(\tilde{\psi}\)。但是，与 b.o. 情况不同，没有双空间。即，对于某个适当的尺度 \(s\)，\(\phi, \tilde{\phi} \in A_s\) 且 \(\psi, \tilde{\psi} \in W_s\)。在这个系统中，交换 \(\phi, \psi\) 与 \(\tilde{\phi}, \tilde{\psi}\) 的角色非常容易。

对于半正交标度函数和小波，我们有

