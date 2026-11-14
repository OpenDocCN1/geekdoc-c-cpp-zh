

因此 \(O_1^s \subseteq O\) 是穿过 \(O\) 的一个 \(\Pi_1^1\)-路径，从而得到以下定理。

### 定理 2.6.4 (Feferman 和 Spector [26])。存在一个 \(\Pi_1^1\)-集合 \(O_1 \subseteq O\)，使得 \(<_O\) 限制在 \(O_1\) 上是序数类型为 \(\omega_1^{CK}\) 的良序。

定理 2.6.4 的证明本质上是模型论的。一个纯递归论的证明可以在 Sacks [123] 中找到。本节的结果也可以一致地相对化。具体来说，存在一个 \(\Sigma_1^1\)-集合 \(\{ (x, O^{x+*}) \mid x \in 2^\omega \}\)，使得对每个 x，\(O^{x+*}\) 是 \(O^x\) 的一个真终端扩展（一个非标准的 \(O^x\)）。

## 2.6.3 穿过 O 的一条正则路径

尽管 O 上的偏序看似复杂，但穿过它的一个 \(\Pi_1^1\)-路径中，每个真初始段都是递归的。这表明在 \(<_O\) 中存在某些隐藏的正则性。

### 定理 2.6.5 (Jockusch [56])。存在一个集合 \(O \subseteq O\)，使得

- \(<_O\)（定义 1.2.1）是在 O 上的序数类型为 \(\omega_1^{CK}\) 的良序；
- O 是 \(<_O\)-下向闭的，且
- 对于任何 \(n \in O\)，\(\{ m \mid m <_O n \}\) 是递归的。

证明。首先，注意，根据经典递归论中的填充引理，我们可以假设

```
\((\forall m \in O)(\forall n \in O)(n +_O m > \max\{m, n\}).\)
```

根据 s-m-n 定理，存在一个递归函数 \(g_0\)，使得对每个 m，

```
\(\varphi_{g_0(e, m, 0)} = \varphi_e(\varphi_m(0)) \land (\forall n)(\varphi_{g_0(e, m)(n+1)} = \varphi_{g_0(e, m)}(n) +_O \varphi_e(\varphi_m(n+1)).\)
```

定义递归函数 \(h_0\) 如下：

```
\(\varphi_{h_0(e)}(n) = \left\{ \begin{array}{ll} 1 & n = 1, \\ 2^{\varphi_e(k)} & n = 2^k, \\ 3 \cdot 5^{\varphi_e(k)} & n = 3 \cdot 5^k, \\ \uparrow & \text{Otherwise.} \end{array} \right.\)
```

根据递归定理，存在一个常数 c 使得 \(\varphi_{h_0(c)} = \varphi_c\)。那么 \(\varphi_c\) 在 O 上是全定的。注意 \(\varphi_c(1) = 1\)，\(\varphi_c(2^n) = 2^{\varphi_c(n)}\)，并且如果 \(n = 3 \cdot 5^k\)，则 \(\varphi_c(n) = 3 \cdot 5^w\)，其中 \(\varphi_w(n) = \varphi_c(\varphi_c(n))\) 且 \(\varphi_w(j+1) = \varphi_w(j) +_O \varphi_c(\varphi_c(j+1))\)。\(\varphi_c\) 遵循 § 1.2.1 中 (i)-(iv) 设定的格式，并具有额外性质：对于 \(n = 3 \cdot 5^k\)，\(\varphi_c(n)\) 给出一个从 \(\varphi_c\) 递归定义的递归函数的索引 w。因此，直观上可以将其视为 \(\varphi_c\) 值域上的 O 的一个版本。令 \(i \in O^* \setminus O\)。我们声称集合

```
\(O = \{ m \mid (\exists n \in O)(m <_O \varphi_c(n) \land n <_{O^*} i) \}\)
```

是所要求的。我们首先将其作为练习留给读者，以验证

- (1) \(\Phi_e\) 在 \(<_O\) 的意义下是严格递增的；
- (2) 对于每个 \(j_0\) 和 \(m\)，如果 \(\Phi_\omega(j_0) \le_O n <_O \Phi_\omega(j_0 + 1)\)，则存在一个 \(j_1 \in \Theta\) 使得 \(m = \Phi_e(j_0) \vdash_O j_1\)。

由于 \(n <_O m\) 蕴含 \(\Phi_e(n) <_O \Phi_e(m)\)，\(<_O\) 在 O 上是一个良序。注意，对于任何 \(n \in O\)，\(|n| \le |\Phi_e(n)|\)。因此 \(\Phi_e : \{n \in O \mid n <_O \cdot\} \to O\) 是一个嵌入，故 \(<_O\) 在 O 上是序数类型为 \(\omega_1^{CK}\) 的良序。通过在 i 以下的标准序数记号 \(<_O\) 上进行跨越归纳，很容易看出 O 是 \(<_O\)-下向闭的。

根据定理 1.3.4，存在一个递归函数 \(g_1\)，使得对任何 \(n \in O\)，\(W_{g_1(n)} = \{j \mid j <_O n\}\)。我们声称 \(W_{g_1(n)}\) 在限制于 \(n \in O\) 时是递归集合。然后将随之而来，集合 \(\{(j, k) \mid j <_k n <_O n\}\) 也是递归的。

通过有效的跨越归纳与递归定理的应用，我们将定义一个部分递归函数 \(q\)，使得对 \(n \in O\)，\(W_{q(n)} = \omega \setminus W_{g_1(n)}\)。情形 \(n = 2^k\) 且 \(\Phi_e(n) = 2^{\Phi_e(k)}\) 留给读者作为练习（练习 2.6.1）。假设 \(n = 3 \cdot 5^k\) 且 \(\Phi_e(3 \cdot 5^k) = 3 \cdot 5^w\)，其中 w 如前定义，且 e 给定使得对每个 \(j < \omega\)，\(\Phi_e(\Phi_e(j))\) 有定义。首先注意，对 j 的归纳表明 \(\Phi_\omega(j) \ge j\)。如果对于每个 j，\(W_{\Phi_e(\Phi_e(j))} = \omega \setminus W_{g_1(\Phi_e(j))}\)，则我们声称

\(m \in \bigcup_{j < \omega} W_{g_1(\Phi_e(j))} \iff (\exists j_0 \le m)(m \in W_{g_1(\Phi_e(j_0+1))}).\)

该声明从右向左的证明是直接的。对于另一方向，令 \(j_0\) 使得 \(\Phi_\omega(j_0) \le_O m < \Phi_\omega(j_0 + 1)\)。然后根据 (2)，存在一个 \(j_1 \in \Theta\) 使得 \(\Phi_\omega(j_0) \vdash_O j_1 = m\)。这蕴含 \(j_0 \le \Phi_\omega(j_0) \le m\)。由于 \(m \le_O \Phi_\omega(j_0 + 1)\)，我们已证明了该声明。

因此 \(\bigcup_{j < \omega} W_{g_1(\Phi_e(j))} = \omega \setminus \bigcap_{j < \omega} \Phi_\omega(\Phi_e(j))\) 是递归的。现在这个计算是一致的，因此存在一个递归函数 \(g_2\)，使得如果对于每个 j，\(W_{\Phi_e(\Phi_e(j))} = \omega \setminus W_{g_1(\Phi_e(j))}\)，则 \(W_{g_2(e,w)} = \bigcap_{j < \omega} W_{\Phi_e(\Phi_e(j))}\)。令 \(g_3\) 为一个递归函数，使得 \(W_{g_1(e,w)} = W_e \setminus \{w\}\)。回顾，如果 \(\Phi_e(3 \cdot 5^k) = 3 \cdot 5^w \in O\)，则 \(\Phi_\omega(j + 1) = \Phi_\omega(j) \vdash_O \Phi_e(j + 1)\)。令 \(W_{c_1} = \omega\)。

定义递归函数 \(h_1\) 如下：

\(\Phi_{h_1(e)}(n) = \begin{cases} c_1 & n=1, \\ g_3(\Phi_e(m), m) & n=2^m, \\ g_2(e, w) & n=3 \cdot 5^w, \\ \uparrow & \text{Otherwise.} \end{cases}\)

根据递归定理，存在一个 d 使得 \(\Phi_{h_1(d)} = \Phi_d\)。令 \(q = \Phi_d\)。那么 q 即为所需。

## 2.6.4 练习

### 练习 2.6.1. 完成定理 2.6.5 中情形 \(n = 2^k\) 且 \(\Phi_e(n) = 2^{\Phi_e(k)}\) 的归纳论证。

### 练习 2.6.2. 证明对于任何 \(i \in O^* \setminus O\)，\(<_O\) 在集合 \(\{j \mid j \in O^* \land j <_O i\}\) 上不是良序。

### 练习 2.6.3. 证明定理 2.6.5 中的 (1) 和 (2)。

### 练习 2.6.4. 证明穿过 O 的路径有 \(2^{\aleph_0}\) 条。

### 练习 2.6.5. 证明不存在部分递归函数 \(p : \omega^2 \to \omega\) 满足练习 14.1 中的性质 (1)-(3)，其中将 x 替换为 \(O_1\)。

## 2.7 集合的编码

在 § 2.2.3 中，介绍了一种 \(\Delta^1_1\)-集合的编码方法。然而，该方法没有提供跟踪 \(\Delta^1_1\)-集合构造的有效方式。在这里，我们讨论超算术编码方法，它作为对实数的 \(\Delta^1_1\) 集合进行归纳分析的有用工具。

### 2.7.1 Borel 编码

*在本节中，固定 \(\omega^{<\omega}\) 的一个有效枚举* \(\{\sigma_i\}_{i < \omega}\) *。*

对于每个 \(x \in 2^\omega\)，定义 \((x)_n = \{m \mid 2^n \cdot 3^m \in x\}\)。定义实数集的一个序列 \(\{\Sigma_\beta\}_{\beta < \omega_1}\) 如下：

- \(\beta = 0\)：令 \(\Sigma_0 = \{x \in 2^\omega \mid 0\}\)。

- \(\beta > 0\)：令 \(\Sigma_\beta = \{x \in 2^\omega \mid (\forall n)(\exists \gamma < \beta)((x)_n \in \Sigma_\gamma)\}\)。

令 BC = \(\bigcup_{\beta < \omega_1} \Sigma_\beta\) 为 Borel 编码的集合。对于每个 \(x \in\) BC，定义 \(A_x\) 为：

\(x \in \Sigma_0\)：\(A_x = \bigcup_{i \in x} \{ \sigma_i \}\)。

\(\beta > 0\) 且 \(x \in \Sigma_\beta\)：\(A_x = \bigcup_n (2^\omega \setminus A_{(x)_n})\)。

如果 \(\sigma\) 是空字符串，令 \((y)_\sigma = y\)。对于每个 \(\sigma \in \omega^{<\omega}\)，定义

\((y)_\sigma = (\dots ((y)_{\sigma(1)})_{\sigma(2)}) \dots )_{\sigma(|\sigma|)}\)。

给定一个实数 y，我们定义 \(\omega^{<\omega}\) 上的一棵树 \(T' \le_T y\) 如下：

\(\emptyset \in T'\)；

对于任何 \(\sigma \in T'\)，如果 \((y)_\sigma \in \Sigma_0\)，则 \(\sigma\) 在 \(T'\) 中没有扩展。否则，对于每个 n，\(\sigma^\frown n \in T'\)。

