

证明。(i) 立即成立。(ii) 成立，因为对于任何数 $l$，只有有限多个 $m \le l$ 满足 $l <_o m <_o n$。(iii) 成立，因为 $<_o$ 是递归集合 $\{i \mid i <_o n\}$ 上的递归关系。

我们证明 (iv)。如果 $m = 3 \cdot 5^k <_o n$ 且 $|m| = \lim_{i \to \infty} \beta_i$，其中 $\{\beta_i\}$ 是极限序数的递增序列，那么对于任何 $i$，存在一个 $m' = 3 \cdot 5^{k'} <_o m$ 使得 $|m'| > \beta_i$，这样只要 $m' = 3 \cdot 5^{k'} <_o m$ 且 $|m'| > |m''|$，就有 $m' > m''$。因此 $|i_{0,m'}| > |m''|$。

将定理 11.2.2 扩展到任意层级的递归序数时的主要困难在于极限序数阶段的编码。这里，如同在定理 11.2.2 的证明中一样，在每个继承阶段，人们试图进行一种逐步下降的构造，以编码在极限层级计算出的信息。仅处理一个极限序数没有困难。当有多个极限序数时，必须选择其中一个进行编码。引理 11.2.7 允许在极限序数的近似中使用良序列，以便于选择。

为方便起见，在本节余下部分，令 $[n] = \beta_{\infty}$，并将每个 $\le_o n$ 的自然数与它作为序数表示法的序数 $\beta < \beta_{\infty}$ 相识别。特别是，我们用 $\lambda$ 表示那些是极限序数序数表示法的自然数。另外，当 $\lambda = |m|$ 时，令 $\beta_{j,\lambda} = |i_{j,m}|$。我们用 $\theta^{(\beta)}$ 和 $x^{(\beta)}$ 分别表示 $H_i$ 和 $H_i^X$，其中 $|i| = \beta$。最后，$\beta^+$ 与 $2^k$ 相识别，其中 $|k| = \beta$。

对于 $\beta \le_o n$，令

$$
\Lambda(\beta) = \{\lambda \mid \beta <_o \lambda \land (\exists j \in \omega)(\beta_{j,\lambda} \le_o \beta)\}.
$$

注意，根据引理 11.2.7，对于任何 $\beta \le_o n$，$\Lambda(\beta)$ 都是有限的。因此以下定义良好：

$$
j(\beta) = \max(\{0\} \cup \{j \mid (\exists \lambda \in \Lambda(\beta))(\beta_{j,\lambda} \le_o \beta)\}).
$$

对于每个 $a \in \omega$，定义以下“特化”到 $\omega \setminus a$ 的函数：

$$
p_a(\sigma) = \tau \Leftrightarrow (\forall i, j, k)(\tau(\langle j, i \rangle) = k > 0 \leftrightarrow j \notin a \land \sigma(\langle j, i \rangle) = k > 0).
$$

则

$$
p_a(T) = \{p_a(\sigma) \mid \sigma \in T\},
$$

且

$$
p_a(\dot{X}) = x \Leftrightarrow (\forall i, j, k)(x(\langle j, i \rangle) = k > 0 \leftrightarrow j \notin a \land \dot{X}(\langle j, i \rangle) = k > 0).
$$

对于 $\beta <_o \gamma \le_o \beta_{\infty}$，令

$$
(\beta, \gamma] = \{\delta \mid \beta <_o \delta \le_o \gamma\}.
$$

显然，如果 $\beta < \gamma < \delta$，则 $p_{(\beta, \delta]} = p_{(\beta, \gamma]} \circ p_{(\gamma, \delta]}$。如同在上一节中，存在一棵递归树 $T \subseteq \beta_{\infty} \times \omega^{<\omega}$，使得 $T(\beta) = \{\sigma \mid (\beta, \sigma) \in T\}$ 包含恰好一条路径 $\theta^{(\beta)}$。令

$$
T^{\beta_{\infty}} = \{\sigma \mid (\forall \beta)(\exists i)(\exists \tau)(\sigma(\beta, i) \text{ defined} \rightarrow ((\beta, \tau) \in T \land (\forall j)(\sigma(\beta, j) = \tau(j))))\}.
$$

因此 $T^{\beta_{\infty}}$ 将 $T$ 编码为一棵单一的树。对于 $\beta \le_o \beta_{\infty}$，令 $y_\beta$ 为一个实数，使得 $(\forall i, j, k)[y_\beta(\langle i, j \rangle) = k \leftrightarrow i \le_o \beta \wedge \theta^{\langle i \rangle}(j) = k]$。

注意，存在常数 $d_0, d_1$，使得 $y_\beta \equiv_T \theta^{\langle \beta \rangle}$ 通过 $(d_0, d_1)$。我们构建一个系统，包含一致的 r.e. 树序列 $\{T_\beta\}_{\beta \le_o \beta_{\infty}} = \{T_\beta^{p_0} \times T_\beta^{p_1}\}_{\beta \le_o \beta_{\infty}}$、函数 $\{\psi_{\beta, \bar{p}}\}_{\beta \le_o \beta_{\infty}}$ 和常数 $\{c_i\}_{i \le 3}$，使得

- (1) $T_{\beta_{\infty}} = 2^\omega \times T^{\beta_{\infty}}$;
- (2) $T_\beta \cap \omega^{S(\beta)} \times \omega^{S(\beta)} = \{(\sigma, \tau) \in \omega^{S(\beta)} \times \omega^{S(\beta)} \mid (\exists \lambda \in \Lambda(\beta))(\exists \bar{j})(\exists \bar{p})(\beta_{\bar{j}, \lambda} \le \beta \wedge (\sigma, \bar{\tau}) \in T_\lambda \cap 2^{S(\beta)} \times 2^{S(\beta)} \wedge p_{P(\lambda, \bar{j})}(\bar{\tau}) = \tau \}$;
- (3) $T_\beta^p = p_{\beta, \bar{p}_\beta}(T_\beta^\infty)$ 且因此 $[T_\beta^p] = \{y_\beta\}$。令 $T_\beta^0 = \{\sigma \mid (\sigma, y_\beta \upharpoonright |\sigma|) \in T_\beta\} = \mathcal{O}_{C_1}^{\theta^{\langle \beta \rangle}}$;
- (4) $\psi_{\beta, \bar{p}} : T_\beta \to T_\beta^0$ 是一个 $C_1^{\theta^{\langle \beta \rangle}}$;
- (5) $\psi_{\beta, \bar{p}}$ 可视为从 $[T_\beta^0]$ 到 $[T_\beta^0]$ 的同态，使得 $(\forall x \in [T_\beta^0])[p_{\psi_{\beta, \bar{p}}^{-1}}(x) \oplus \theta^{\langle \beta \rangle} \equiv_T (x \oplus \theta^{\langle \beta \rangle})']$ 通过 $(c_2, c_3)$，且
- (5i) 对于 $\sigma, \tau \in T_\beta^0$，$\sigma \prec \tau \Rightarrow \psi_{\beta, \bar{p}}(\sigma) \le \psi_{\beta, \bar{p}}(\tau)$;
- (5ii) 如果 $\sigma \in T_\beta^0$，则 $|\psi_{\beta, \bar{p}}(\sigma)| \ge |\sigma|$；且
- (6) 对于 $\sigma \in T_\beta^0 \cap \omega^{S(\beta)}$，$\psi_{\beta, \bar{p}}(\sigma) = \sigma$。

假设我们有上述的树序列。根据 (4) 和 (5)，对于每个 $x \in T_0^0$，通过对 $\beta \le_o \beta_{\infty}$ 的归纳，可以得出 $x^{(\beta)} \equiv x \oplus \theta^{\langle \beta \rangle} \ge_T \theta^{\langle \beta \rangle}$。

乍看之下，(2) 对 $T_\beta \cap \omega^{S(\beta)} \times \omega^{S(\beta)}$ 设定的要求似乎是一个问题，因为来自 $T_\lambda$（其中 $\lambda \in \Lambda(\beta)$）的太多节点被放入其中。然而，以下引理表明，由于引理 11.2.7 (iv)，$T_\beta \cap \omega^{S(\beta)} \times \omega^{S(\beta)}$ 是一个有序结构。

## 引理 11.2.8.

假设 $\lambda \in \Lambda(\beta)$ 且对于某个 $j$，$\beta_{j, \lambda} \le_o \beta$。那么 $(\sigma, \tau) \in T_\beta \cap \omega^{S(j)} \times \omega^{S(j)}$ 当且仅当存在一个 $(\sigma, \bar{\tau}) \in T_\lambda$ 使得 $p_{\beta, \lambda}(\bar{\tau}) = \tau$。

证明。假设不成立。那么存在一个 $\lambda \in \Lambda(\beta)$，一个使得 $\beta_{j, \lambda} \le_o \beta$ 的 $j$，这样对于某个 $(\sigma, \tau) \in T_\beta \cap \omega^{S(j)} \times \omega^{S(j)}$，不存在 $(\sigma, \bar{\tau}) \in T_\lambda$ 使得 $p_{\beta, \lambda}(\bar{\tau}) = \tau$。

根据 (2)，存在一个 $\lambda_1 \in \Lambda(\beta)$ 使得 $\beta_{j, \lambda_1} \le_o \beta$ 且 $j \le j_1$，并且对于某个 $(\sigma, \bar{\tau}_1) \in T_{\lambda_1} \cap \omega^{S(j)} \times \omega^{S(j)}$，有 $p_{\beta, \lambda_1}(\bar{\tau}_1) = \tau$。

我们声称 $\lambda_1 <_o \lambda$。否则，$\lambda <_o \lambda_1$ 且因此 $\beta_{j, \lambda_1} \le_o \beta <_o \lambda_1$。换句话说，$\lambda_1 \in \Lambda(\lambda)$。将 (2) 应用于 $\lambda$，得到 $(\sigma, p_{\lambda, \lambda_1}(\bar{\tau}_1)) \in T_\lambda$。于是

$$
p_{\beta, \lambda}(p_{\lambda, \lambda_1}(\bar{\tau}_1)) = p_{\beta, \lambda_1}(\bar{\tau}_1) = \tau,
$$

产生矛盾。

因此 $\lambda \in \Lambda(\lambda_1)$。注意，不存在 $(\sigma, \bar{\tau}) \in T_\lambda \cap \omega^{S(j)} \times \omega^{S(j)}$ 使得 $p_{\lambda, \lambda_1}(\bar{\tau}) = \bar{\tau}_1$。将上述过程重复，将 $\beta$ 和 $(\sigma, \tau)$ 分别替换为 $\lambda_1$ 和 $(\sigma, \bar{\tau}_1)$，我们看到存在一个 $\lambda_2 \in \Lambda(\lambda_1)$ 和 $\beta_{j_1, \lambda_2} \le_o \lambda_1 <_o \lambda_2$ 使得 $\lambda_2 <_o \lambda$，

$(\sigma, \tau_j) \in T_{\lambda_i}$ 且 $p_{\beta_{j, \lambda_i}}(\tau_j) = \tau_i$。由此可知，存在一个极限序数的递增序列 $\lambda_1 <_o \lambda_2 <_o \cdots <_o \lambda$，使得对于每个 $i \in \omega$，$\beta_{j, \lambda} <_o \lambda_i$，这与引理 11.2.7 (iv) 矛盾。

对于 $\gamma \succeq \beta$，通过对 $\beta \preceq_o \beta_{c, o}$ 的归纳定义映射 $\psi_{\gamma, \beta} : T_\gamma^\infty \to T_\beta^\infty$。如果 $\beta = 0$，则 $\psi_{0, 0}$ 是恒等映射。在以下内容中，$\psi_{\beta, \beta}$ 始终是恒等映射。

如果 $\gamma \succ \beta$，则 $\psi_{\gamma, \beta} = \psi_{\gamma, \beta'} \cdot \psi_{\beta', \beta}$。如果 $\lambda$ 是极限序数，那么对于使得 $\beta \le_o \beta_{j, \lambda} <_o \lambda$ 的 $j$ 和 $\sigma \in T_\lambda^\infty \cap \omega^{<j}$，根据 (2) 和引理 11.2.8，有 $\sigma \in T_\beta^\infty$。定义 $\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_{j, \lambda}, \beta}(\sigma)$。

注意，在 $\beta = \beta_{j, \lambda}$ 的情况下，有 $\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_{j, \lambda}, \beta}(\sigma) = \sigma$。我们证明 $\psi_{\lambda, \beta}$ 定义良好。

## 引理 11.2.9.

设 $\delta \le_o \beta_{c, o}$。

- (i) 如果 $\beta \le_o \delta$，则 $\psi_{\delta, \beta}$ 定义良好。
- (ii) 对于 $\beta \le_o \beta_1 \le_o \delta$，$\psi_{\delta, \beta} = \psi_{\beta_1, \beta} \circ \psi_{\delta, \beta_1}$。
- (iii) 对于 $\beta \le_o \delta$ 和 $\sigma, \tau \in T_\beta^\infty$，$\sigma \le_T \psi_{\delta, \beta}(\sigma) \succeq \psi_{\delta, \beta}(\tau)$。而且，$|\psi_{\delta, \beta}(\sigma)| \ge |\sigma|$。
- (iv) 存在一个递归函数 $g$，使得对于每个 $\beta \le_o \delta$，$\psi_{\delta, \beta} = g^{\psi_{\delta, \beta}(\beta)}$。

证明。我们通过对 $\delta$ 的归纳同时证明 (i) 和 (ii)。根据 $\psi_{\delta, \beta}$ 的定义，唯一非平凡的情况是 $\delta = \lambda$ 对于某个极限序数 $\lambda$。

对于 (i)，固定 $\alpha <_o \lambda$ 和 $\beta \le_o \beta_{j_0, \lambda} <_o \beta_{j_1, \lambda} <_o \lambda$，其中 $j_0 < j_1$。假设 $\sigma \in T_\lambda^\infty \cap \omega^{<j_0}$ 且 $j_0$ 用于定义 $\psi_{\lambda, \beta}(\alpha)$。根据 (2) 和引理 11.2.8，$\sigma \in T_{\beta_{j_0, \lambda}}^\infty \cap T_{\beta_{j_1, \lambda}}^\infty$。注意，对于任何满足 $\beta_{j_0, \lambda} <_o \gamma \le_o \lambda$ 的 $\gamma$，都有 $\lambda \in \Lambda(\gamma)$ 且 $j(\gamma) \ge j_0$。根据 (6) 以及对 $\gamma$ 在 $(\beta_{j_0, \lambda}, \lambda]$ 上的归纳，$\psi_{\gamma, \beta_{j_0, \lambda}}(\sigma) = \sigma$。用同样的论证，对于 $\gamma$ 在 $(\beta_{j_1, \lambda}, \lambda]$，有 $\psi_{\gamma, \beta_{j_1, \lambda}}(\sigma) = \sigma$。因此，通过对 $\beta$ 的归纳，$\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_{j_0, \lambda}, \beta}(\psi_{\lambda, \beta_{j_0, \lambda}}(\sigma)) = \psi_{\beta_{j_0, \lambda}, \beta}(\psi_{\beta_{j_1, \lambda}, \beta_{j_0, \lambda}}(\sigma)) = \psi_{\beta_{j_1, \lambda}, \beta}(\psi_{\lambda, \beta_{j_1, \lambda}}(\sigma)) = \psi_{\beta_{j_1, \lambda}, \beta}(\sigma)$。故 $\psi_{\delta, \beta}$ 定义良好。

对于 (ii)，给定使得 $|d| < j$ 且 $\beta \le_o \beta_1 <_o \beta_{j, \lambda} \le_o \lambda$ 的 $j$。则 $\psi_{\lambda, \beta_1}(\sigma) = \sigma$。根据 $\psi_{\lambda, \beta_1}$ 的定义，$\psi_{\lambda, \beta}(\sigma) = \psi_{\beta_1, \beta}(\sigma)$。然后通过归纳，$\psi_{\beta_1, \beta}(\sigma) = \psi_{\beta_1, \beta}(\psi_{\lambda, \beta_1}(\sigma))$。

我们通过使用 (5i) 和 (5ii) 以及对 $\beta$ 的归纳得到 (iii)。最后，(iv) 从 (3) 得出。

如果 $x \in [T_\beta^\infty]$，令 $\psi_{\beta, \delta}(x) = \cup_{m < \omega} \psi_{\beta, \delta}(x \upharpoonright m)$。根据引理 11.2.9 (iii)，$\psi_{\delta, \beta}$ 定义良好。

## 引理 11.2.10.

对于任何 $\beta \le_o \gamma \le_o \beta_{c, o}$，$\psi_{\gamma, \beta} : [T_\gamma^\infty] \to [T_\beta^\infty]$ 是一个同胚。

证明。这是通过对 $\gamma$ 的归纳证明的。首先，(5) 意味着唯一非平凡的情况是 $\gamma = \lambda$，一个极限序数。

对于 $x \in [T_\gamma^\infty]$ 和 $m \in \omega$，选择 $j_m > m$ 使得 $\beta <_o \beta_{j_m, \lambda}$。通过归纳，存在唯一的 $z_m \in [T_{\beta_{j_m, \lambda}}]$ 使得 $\psi_{\beta_{j_m, \lambda}, \beta}(z_m) = x$。根据引理 11.2.9 (iii)，$\psi_{\beta_{j_m, \lambda}, \beta}(z_m \upharpoonright m) \succeq x \upharpoonright m$。令 $\sigma_m = z_m \upharpoonright m$。根据引理 11.2.9 的 (ii) 和 (iii)，存在 $z = \cup_m \sigma_m$。由于 $j_m > m$，对于每个 $m$ 都有 $\sigma_m \in T_\lambda$。因此 $z \in [T_\beta^\infty]$。而且，

