

定理 2.5.5（Spector [155]）。存在实数 $x$ 和 $y$，使得 $x \not\le_h y$ 且 $y \not\le_h x$。事实上，存在一个实数 $x \not\le_h 0$，满足 $\omega_1^x = \omega_1^{CK}$。

证明。令 $A = \{x \mid x \notin \xi_0\}$ 为非空的 $\Sigma^1_1$-集合。根据定理 2.5.3 和推论 2.4.11，集合 $B = \{x \in A \mid \omega_1^x = \omega_1^{CK}\}$ 是非空的 $\Sigma^1_1$-集合。根据引理 2.5.4，$B$ 是不可数的。由于可高算归约到 0 的实数至多有可数个，因此存在实数 $x \in B$ 使得 $x \not\le_h 0$。而且，由于 $\omega_1^x = \omega_1^{CK}$，故 $x \not\le_h 0$。$\square$

应当指出，Spector 对定理 2.5.5 的原始证明与上面给出的证明截然不同。他的证明涉及测度论证法，并且是非构造性的。该思想将在第 14 章（关于更高随机性）中进行探讨。

## 2.5.3 克赖塞尔基定理

**定理 2.5.6** (Kreisel [35])。如果 $x$ 是非高算的，且 $A \subseteq \omega^\omega$ 是非空的 $\Sigma^1_1$-集合，则存在 $y \in A$ 使得 $x \not\le_h y$。

证明。假设 $x$ 是非高算的，且 $A \subseteq \omega^\omega$ 是非空的 $\Sigma^1_1$-集合。根据甘迪基定理 2.5.3，集合 $B = \{z \mid \omega_1^z = \omega_1^{CK} \land z \in A\}$ 是非空的 $\Sigma^1_1$-集合。对于每一对 $(e, n)$（其中 $n \in \omega$），令

$P_{(e,n)} = \{z \mid (\exists i)(\Phi_e^{\tilde{H}_i}(i) \downarrow \lor \Phi_e^{\tilde{H}_i}(i) \downarrow \neq x(i))\}.$

我们声明，对于任何非空的 $\Sigma^1_1$-集合 $C$，都存在非空的 $\Sigma^1_1$-集合 $Q_{(e,n)} \subseteq C \cap P_{(e,n)}$。需考虑三种情况。

- (1) 存在 $z \in C$ 和 $i \in \omega$ 使得 $\Phi_e^{\tilde{H}_i}(i) \uparrow$。则令 $Q_{(e,n)} = \{z \mid (\Phi_e^{\tilde{H}_i}(i) \uparrow \land z \in C)\}$。
- (2) 非情况 (1)，但存在 $z_0, z_1 \in C$ 和 $i \in \omega$ 使得 $\Phi_e^{\tilde{H}_{z_0}}(i) \uparrow \neq \Phi_e^{\tilde{H}_{z_1}}(i)$。则存在 $k \le 1$ 使得 $\Phi_e^{\tilde{H}_k}(i) \neq x(i)$。令 $Q_{(e,n)} = \{z \mid (\Phi_e^{\tilde{H}_z}(i) = \Phi_e^{\tilde{H}_k}(i) \land z \in C)\}$。
- (3) 既非 (1) 也非 (2)。则 $\Sigma^1_1$-集合 $\{u \mid (\exists 2i)(\forall z \in C \land u(i) = \Phi_e^{\tilde{H}_z}(i))\}$ 包含恰好一个实数，该实数必为高算的。令 $Q_{(e,n)} = C$。

根据命题 1.1.12，存在 $y \in B \cap \bigcap_{n < \omega} P_{(e,n)}$。根据 $P_{(e,n)}$ 的定义，$x \neq \Phi_e^{\tilde{H}_y}$。注意 $\omega_1^y = \omega_1^{CK}$。因此，根据定理 2.3.3，我们得出 $x \not\le_h y$。$\square$

定理 2.5.6 表明，高算在某个非高算集合之上的集合锥不包含非空的 $\Sigma^1_1$-子集。特别是，任何非高算集合之上的锥都不是 $\Sigma^1_1$。从模型论角度来看，该定理证明中使用的论证是一类型省略论证。该论证将稍后再次用于构造非标准模型，以通过可构层次 $L$ 刻画高算集合。

## 2.5.4 习题

**习题 2.5.1。** 证明对于任意实数 $z$，集合 $\{(x, 0^x) \mid x \in 2^{\omega}\}$ 不是 $\Sigma_1^1(z)$。

**习题 2.5.2。** 证明存在 $x, y \le_h \mathbf{0}$ 使得 $x \not\le_h y$ 且 $y \not\le_h x$。

**习题 2.5.3。** 证明存在实数序列 $(x_i)_{i < \omega}$ 使得 $x_i <_h x_{i+1} <_h \mathbf{0}$。

**习题 2.5.4** (Slaman [140])。证明不存在 $\Sigma_1^1$-集合 $A \subseteq \omega^\omega$ 使得每个 $\Sigma_1^1$-集合都是 $A$ 的连续单射像。

**习题 2.5.5** (Hjorth [49])。证明每个 $\Sigma_1^1$-集合都是 $\Pi_1^1$-集合 $\{x \in \omega^\omega \mid x \in \omega^\omega\}$ 的连续单射像。

**习题 2.5.6。** 证明任何非空的 $\Sigma_1^1$-集合 $A$ 包含一个元素 $x$，使得 $0^x \le_T \mathbf{0}$。

**习题 2.5.7** (Solovay [152])。给定函数 $f, g: \omega \to \omega$，若对任意 $i < \omega$ 都有 $g(i) \ge f(i)$，则称 $g$ 支配 $f$。证明实数 $x$ 是高算的，当且仅当存在函数 $f \ge_T x$，使得每当 $g$ 支配 $f$ 时都有 $g \ge_T f$。

## 2.6 关于 $\mathbf{O}$ 的更多内容

### 2.6.1 非标准的 $\mathbf{O}$

我们构造一个与 $\mathbf{O}$ 具有许多共同性质的非标准 $\mathbf{O}$。下面的引理表明，存在一个可枚举集合，其域是 $\mathbf{O}$ 的末端扩展。

**引理 2.6.1。** 存在一个可枚举集合 $x$ 和一个定义在 $x$ 上的可枚举偏序关系 $<_x$，使得

- (i) §1.2.1 中的条件 (i)-(iv) 对 $<_x$ 成立；
- (ii) $\mathbf{O} <_x$；
- (iii) $<_0$ 是 $<_x$ 对 $\mathbf{O}$ 的限制；且
- (iv) 若 $m <_x n$ 且 $n \in \mathbf{O}$，则 $m \in \mathbf{O}$。

证明。我们通过有效跨超归纳构造 $<_x$。定义递归函数 $h$ 如下：

```
\(\Phi_{h(e)}((m, n)) = \left\{ \begin{array}{ll} 1 & m = 1 \wedge n = 2, \ 1 & (\exists k)(\Phi_e((m, k)) = 1 \wedge \Phi_e((k, n)) = 1), \ 1 & (\exists k)(\Phi_e((k, m)) = 1 \wedge n = 2^m), \ 1 & m \neq 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)(\exists j)(\Phi_e((j, m)) = 1 \wedge m = \Phi_d(k)), \ \uparrow & \text{Otherwise.} \end{array} \right.\)
```

根据递归定理，存在常数 \(c\) 使得 \(\Phi_{h(c)} = \Phi_c\)。令 \(g = \Phi_c\) 为偏递归函数。因此

```
\(g((m, n)) = \begin{cases} 1 & m = 1 \wedge n = 2, \\ 1 & (\exists k)(g((m, k)) = 1 \wedge g(k, n) = 1), \\ 1 & (\exists k)(g((k, m)) = 1 \wedge n = 2^m), \\ 1 & m \neq 1 \wedge n = 3 \cdot 5^d \wedge (\exists k)(\exists j)(g((j, m)) = 1 \wedge m = \Phi_d(k)), \\ \uparrow & \text{Otherwise.} \end{cases}\)
```

定义 $m <_x n$ 当且仅当 $g(m, n) = 1$。令 $X = \{m \mid (\exists n)(m <_x n)\}$。可以直接验证，$<_x$ 的域满足 (i)-(iv)。

注意，给定 \(n \in \mathbb{N}\) 时，\(<_x\) 对集合 \(\{m \mid m <_x n\}\) 的限制不一定是线性的。我们引入如下修改。定义 \(z \subseteq x\)，使得 \(i \in z\) 当且仅当 \(i \in x\) 且 \(<_x\) 对 \(\{m \mid m <_x i\}\) 的限制是线性的。那么 \(z\) 是一个算术集。显然，\(<_x\) 对 \(z\) 的限制是一个偏序，\(\emptyset \subset z\)，且条件 (i)-(iv) 对 \(<_x\) 对 \(z\) 的限制成立。

现在，对于任意 \(n \in \mathbb{O}\)，令 \(z_n\) 为高算集合，使得 \(i \in z_n\) 当且仅当 \(i \in \mathbb{O}_{2^{n*}}\)，或存在 \(j \in \mathbb{O}_{2^{n*}}\) 满足 \(j <_l i\) 且 \(i \in z\)。换言之，\(z_n\) 是通过将 \(z\) 中不在 \(\mathbb{O}_{2^{n*}}\) 之上的节点“截断”而得到的。因此，\(z_n\) 将 \(\mathbb{O}_{2^{n*}}\) 作为一个“初始段”。注意，\(<_x\) 对 \(z_n\) 的限制也满足条件 (i)-(iv)。

### 定义 2.6.2

令 \(\Theta^* = \bigwedge A\)，其中

```
\(A = \{y \mid y \in x \text{ is hyperarithmetic} \wedge \text{Conditions (i)-(iv) in §1.2.1 hold for } <_x \text{ restricted to } y\}.\)
```

记 \(<_{\Theta^*}\) 为 \(<_x\) 对 \(\Theta^*\) 限制得到的序关系。注意，对所有 \(n \in \mathbb{O}\)，都有 \(z_n \in A\)。此外，根据 \(\emptyset\) 的定义，\(\emptyset \subset \Theta^*\)。由于 §1.2.1 中的条件 (i)-(iv) 是算术陈述，根据推论 2.2.2，可知 \(\Theta^*\) 是 \(\Sigma^1_1\)。

### 2.6.2 穿过 \(\Theta\) 的 \(\Pi^1_1\)-路径

由于 \(\Theta^*\) 是 \(\Sigma^1_1\)，必存在 \(i \in \Theta^* \setminus \mathbb{O}\)。注意，对每个 \(n \in \mathbb{O}\)，都有 \(i \in z_n \setminus \mathbb{O}_n\)。因此，对每个 \(n \in \mathbb{O}\)，存在 \(i_n \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\) 使得 \(i_n <_x i\)，从而 \(i_n <_{\Theta^*} i\)。令 \(\Theta^*_i = \{j \mid j <_{\Theta^*} i \land j \in \mathbb{O}\}\)。则 \(j \in \Theta^*_i\) 当且仅当 \(j \in \Theta \land j <_l i\)。故 \(\Theta^*_i \subseteq \mathbb{O}\) 是一个 \(\Pi^1_1\)-集合。

### 引理 2.6.3

\(<_{\Theta}\) 对 \(\Theta^*_i\) 的限制是一个序类型为 \(\omega^{CK}_1\) 的良序。

证明。显然，\(<_{\Theta}\) 对 \(\Theta^*_i\) 的限制是一个良序。假设 \(<_{\Theta}\) 对 \(\Theta^*_i\) 的限制的序类型小于 \(\omega^{CK}_1\)。则存在 \(n \in \mathbb{O}\) 使得 \(\Theta^*_i \subseteq \mathbb{O}_n\)。于是，对任意 \(k \in \mathbb{O}_{2^{n*}} \setminus \mathbb{O}_{2^n}\)，都有 \(k <_{\Theta^*} j\)。故 \(j \notin z_n\)，产生矛盾。

