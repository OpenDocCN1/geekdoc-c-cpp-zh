

- (1) \( T_1^i = \{\sigma \mid (\sigma, i) \in T^0\} \);
- (2) \( (\sigma, \tau) \in T_i \Rightarrow (\exists \tau' \supseteq \tau)(\tau' \in T_1^i \land \Delta_{c_0}^{T^0}(\sigma)[\tau'] = 1) \);
- (3) \( T_0^i = \sigma \mid (\exists \tau > \emptyset)(\langle \sigma, \tau \rangle \in T_i) \);
- (4) \( \psi_i : T_{i+1}^i \to T^0 \) 是 \( \emptyset^{(i+1)} \);
- (5) \( \psi_i \) 是从 \( [T_{i+1}^i] \) 到 \( [T_0^i] \) 的同胚，使得 \( (\forall x \in [T_i])(\psi_i(x^{-1}) \ominus \emptyset^{(i+1)} \equiv_T (x \ominus \emptyset^{(i)})') \) 通过 (c2, c3) 和
- (5a) \( \sigma < \tau \Rightarrow \psi_i(\sigma) \le \psi_i(\tau) \);
- (5b) 如果 \( \sigma \nsubseteq T_0^i \)，那么 \( |\psi_i(\sigma)| \ge |\sigma| \);
- (6) \( T_0^i \cap \emptyset^{<i} = 2^{<i} \)，且
- (7) \( (\forall \sigma \in T_{i+1}^i \cap \emptyset^i)(\sigma \le \psi_i(\sigma)) \).

假设这些序列已被定义。

### 引理 11.2.3.
对于每个 \( x \in [T_0^0] \) 和 \( i < \omega \)，
(i) \( x^0 \equiv x \ominus \emptyset^0 \) 且
(ii) \( x^{(i)} \not\le_T \emptyset^{(i+1)} \).

**证明.** 由 (4)、(5) 关于 \( i \) 的归纳，(i) 立即成立。若 \( x^{(i)} \ge_T \emptyset^{(i+1)} \)，则 \( x^{(i+1)} \equiv_T x \ominus \emptyset^{(i+1)} \le_T x^0 \)，这产生矛盾。故 (ii) 成立。

### 引理 11.2.4.
\( [T_0^0] \) 与 \( 2^\omega \) 同胚.

**证明.** 我们定义 \( [T_0^0] \) 与 \( 2^\omega \) 之间的双射 \( f \) 如下：对于每个 \( x \in [T_0^0] \)，令
\( f(x) = \bigcup_{i < \omega} \psi_1^{i-1} \circ \psi_{i-1}^1 \circ \cdots \circ \psi_0^1(x) \mid i \).

令 \( x \in [T_0^0] \). 对于 \( i < \omega \)，令 \( x_i = \psi_1^{i-1} \circ \psi_{i-1}^1 \circ \cdots \circ \psi_0^1(x) \mid i \). 则 \( \psi_1^{i-1} \circ \cdots \circ \psi_0^1(x) \in [T_{i+1}^i] \cap [\sigma_i] \). 又 \( \psi_{i+1}^1 \circ \cdots \circ \psi_0^1(x) \in [T_{i+2}^i] \). 因为 \( \psi_{i+1}^1 \) 是单射，所以 \( \psi_{i+1} \circ \psi_i^1 \circ \cdots \circ \psi_0^1(x) \in [T_{i+1}^i] \cap [\sigma_i] \). 由 (7)，\( \psi_{i+1}^1 \circ \cdots \circ \psi_0^1(x) \mid (i+1) \ge \psi_{i+1}^1 \circ \cdots \circ \psi_0^1(x) \mid i+1 = \sigma_{i+1} \). 故 \( \sigma_{i+1} \ge \sigma_i \). 由 (5b)，\( f(x) \in 2^\omega \).

令 \( y \in 2^\omega \) 且对 \( n, i < \omega \) 令 \( \tau_{n,i+1} = \psi_n \circ \cdots \circ \psi_{i+1}(y \mid n+t) \). 由 (5a), (6) 和 (7),
\( y \upharpoonright n \le \tau_{n,n} \le \tau_{n,n+1} \le \tau_{n,n+2} \cdots \).

此外，由 (5b)，对每个 \( i \)，\( |\tau_{n,n+i}| \ge n+i \). 令 \( X_n = \bigcup_{i < \omega} \tau_{n,n+i} \). 则 \( X_n \in [T_0^0] \cap [y \mid n] \). 因为 \( \psi_n^{-1} \) 是单射，由 (7) 得 \( \psi_n^{-1} \circ \psi_{n+1}^{-1} \circ \cdots \circ \psi_0^{-1}(x_0) \mid n = X_n \mid n = y \mid n \). 由 \( f \) 的定义，有 \( f(x_0) = y \). 所以 \( f \) 是满射.

现在假设 \( x_0, x_1 \in [T_0^0] \) 满足 \( f(x_0) = f(x_1) \)，且对某个 \( n_0 \) 以及 \( i \neq j \)，有 \( x_0 \mid n_0 = x_1 \mid n_0 \)，且 \( x_0 \supset x_0 \mid n_0 \)，\( x_1 \supset x_1 \mid n_0 \). 由 (5b) 和 (7)，\( \psi_{n_0+1}^1 \circ \psi_{n_0}^1 \circ \cdots \circ \psi_0^1(x_0) \mid n_0 + 1 = \psi_{n_0+1}^1 \circ \psi_{n_0}^1 \circ \cdots \circ \psi_0^1(x_1) \mid n_0 + 1 \). 然后由 (5a) 和 (5b)，\( x_0 \mid n_0 + 1 = x_1 \mid n_0 + 1 \)，这产生矛盾.
显然 \( f \) 和 \( f^{-1} \) 都是连续的。因此 \( [T_0^0] \) 与 \( 2^\omega \) 同胚.

注意 \( T_0^0 = \{\sigma \mid \Phi_{e_0}^0(\sigma) = 1\} \) 是一棵递归树。因此集合 \( A = [T_0^0] \) 是一个具有所需性质的不可数 \( \Pi_1^0 \)-集.

我们现在转向定义满足 (1)-(7) 的树、函数序列以及常数。给定一棵树 \( T \)，若对任意 \( \sigma, \tau \in T \) 当且仅当 \( \Phi_i^t(\sigma) = 1 \)，则记 \( T = \Phi_i^t \).

### **引理 11.2.5.** 存在一个递归函数 \( t : \omega \to \omega \)，使得对于任何 \( x \in 2^\omega \) 和 \( \omega^\omega \) 中的树 \( T = \Phi_{e_i}^x \)，\( \Phi_{i(x)}^0 \) 是 \( \omega^\omega \) 中的一棵树 \( \hat{T} \)，且 \( [\hat{T}] = \{z \oplus h_x \mid z \in [T]\} \)，其中 \( h_x \) 是一个 \( x \)-递归函数，使得 \( h_x(e, n) \) 要么是 0，要么是 \( \min\{s + 1 \mid \Phi_{e(x)}^x(n)[s] \downarrow\} \).

**证明.** 令

\(\hat{T} = \{\sigma \oplus \tau \mid (\forall e, n)((\langle e, n \rangle < |\tau| \land \tau(\langle e, n \rangle) > 0 \to \tau(\langle e, n \rangle) = \min\{s + 1 \le |\tau| \mid \Phi_{e(x)}^{t_k}(n)[s] \downarrow\}) \land (\exists v < 2^{|\tau|}(\forall e \le |v|)(v(e) = 1 \to \Phi_{e(\tau(\langle e, e \rangle))}^{t_k(\langle e, e \rangle)}(e)[\tau(\langle e, e \rangle)] \downarrow) \land \Phi_i^0(\sigma) = 1)\}.\)

则 \( \hat{T} \) 即为所需。由于 \( \hat{T} \) 是一致得到的，存在一个递归函数 \( t : \omega \to \omega \)，使得 \( \hat{T} = \Phi_{i(0)}^t \).

现在对于 \( i, j < \omega \) 且 \( T_{i+1} = \Phi_{i+1}^{\psi(i+1)} \)，我们定义一棵树 \( T_i \)，使得 \( T_i \) 在将 \( \{c_i\}_{i \le j} \) 替换为依赖于 \( T_{i+1} \) 的参数后满足 (1)-(7). 该构造在 \( i \) 和 \( j \) 中是一致的。这意味着存在一个递归函数 \( t \)，使得 \( T_j^0 = \Phi_{i(j)}^{\psi(j)} \). 由递归定理，存在一个 \( c_0 \) 使得 \( T_0^0 = \Phi_{c_0}^0 = \Phi_{i(0)}^{\psi(0)} \). 令 \( T_i = \{(\sigma, \tau) \mid (\exists t' \ge t)(\langle i, t' \rangle \in T^{\omega \omega} \Phi_{c_i}^{t'}(\sigma)[t'] = 1)\} \).

其余参数 \( c_i \)（\( 1 \le i \le 3 \)）以同样的方式得到。因此我们可以假设 \( T_{i+1}^0 \) 具有性质 (1)-(7). \( T_i^0 \) 由 \( T_{i+1}^0 \) 定义.

### **引理 11.2.6.** 给定一棵递归树 \( T_0 \le \omega^\omega \)，存在一棵递归树 \( T_1 \) 和一个 \( A_2^0 \)-同态 \( \psi : T_0 \to T_1 \)，使得对于任何 \( x \in [T_1] \)，\( x' \equiv_T x \oplus 0' \).

**证明.** 证明采用有限损伤论证。给定一棵递归树 \( T_0 \le \omega^\omega \)，我们通过完全逼近构造定义 \( \psi \) 和 \( T_1 \).

### 阶段 0.
令 \( \psi_0(\emptyset) = \emptyset \) 且 \( T_{0,0} = \emptyset \). 我们声明所有节点 \( \sigma \in T_0 \) 都是新鲜的.

### 阶段 \( s + 1 \).
假设 \( \psi_s : T_0 \to T_{1,s} \le 2^{<\omega} \) 是部分定义的。搜索最小的 \( t \le s \)，使得存在一个新鲜的 \( \sigma \in T_0 \)，对于该 \( \sigma \) 存在一个 \( \tau \in T_{1,s} \upharpoonright (\psi_s(\sigma)) \cap 2^{>s} \)，使得 \( \Phi_i^t(t)[\tau] \downarrow \). 对于每个这样的 \( \sigma \)，定义 \( \psi_{s+1}(\sigma) = \tau' > \tau \)，其中 \( |\tau'| = \tau' \cap 0^{t+1} \). 对于所有在 \( T_0 \cap \text{Dom}(\psi_s) \) 中与这样的 \( \sigma \) 不兼容的 \( v \)，令 \( \psi_{s+1}(v) = \psi_s(v) \). 若 \( v \in \text{Dom}(\psi_s) \) 与这些 \( \sigma \) 不兼容且对所有 \( \tau' \in T_0 \upharpoonright \text{Dom}(\psi_s) \)，则定义 \( \psi_{s+1}(\nu') = \psi_s(\nu') \). 声明对于每个这样的 \( \sigma \)，\( \sigma \) 不是新鲜的，且对于扩展这样的 \( \sigma \) 的任何 \( \tau \)，\( \tau \) 是新鲜的. 令 \( T_{1,s+1} = \text{Range}(\psi_{s+1}) \).

这完成了阶段 \( s + 1 \) 的构造。注意对于每个 \( \sigma \)，\( |\{s \mid \psi_s(\sigma) \neq \psi_{s+1}(\sigma)\}| \le |\sigma| \). 因此对于每个 \( \sigma \)，\( \psi(\sigma) = \lim_{s \to \infty} \psi_s(\sigma) \) 存在。于是 \( \psi \) 是 \( A_2^0 \).

令 \( T_1 = \bigcup_{s < \omega} T_{1,s} \). 由构造，\( \psi : [T_0^0] \to [T_1] \) 是一个同态。假设 \( x \in [T_1] \). 给定 \( t \)，为了判定 \( \Phi_i^t(t) \) 是否收敛，我们以 \( \emptyset' \)-递归方式搜索一个

\(\sigma \in T_1 \cap 2^{<\omega}\) 和一个阶段 \( s \ge t \) 使得 \( \psi_s(\sigma) = \psi(\sigma) < x \). 则 \( \Phi_i^t(t) \) 收敛当且仅当 \( \Phi_i^{\psi(\sigma)}(t)[s] \). 因此 \( x' \le_T x \oplus \emptyset' \).

现在如果 \( i < \omega \) 且 \( \sigma \in 2^{<\omega} \)，令 \( \hat{T}_{i+1,l,\alpha} \) 如引理 11.2.5 所述为一个 \( \emptyset^{(i)} \)-递归树，其中将 \( T \) 设为 \( \{\tau \mid \sigma^\frown \tau \in T_{i+1}^0\} \)，将 \( x \) 设为 \( \emptyset^{(i)} \). 通过将 \( T_0 \) 替换为 \( \hat{T}_{i+1,l,\alpha} \) 来对 \( \emptyset^{(i)} \) 实现引理 11.2.6，我们得到一个 \( \emptyset^{(i)} \)-递归同胚 \( \psi_i : \hat{T}_{i+1,l,\alpha} \to T_{l,\alpha} \)，其中 \( T_{l,\alpha} \) 是引理 11.2.6 中的 \( T_1 \). 定义 \( T_i^0 \) 为一个 \( \emptyset^{(i)} \)-递归树，使得 \( \tau \in T_i^0 \) 当且仅当以下之一成立：

- \( |\tau| \le 1 \)，或

- \( \tau = (\tau \upharpoonright \gamma)^\frown \tau' \)，其中 \( \tau' \in T_{1, \upharpoonright \gamma} \).

定义 \( \psi_i \le_T \theta^{(i+1)} : T_{i+1}^0 \to T_i^0 \)，使得

- 若 \( \tau \in 2^{<\omega} \)，则 \( \psi_i(\tau) = \tau \);

- 否则，令 \( \tau = (\tau \upharpoonright \gamma)^\frown \tau' \). 定义 \( \psi_i(\tau) = \tau \upharpoonright \gamma \psi_i(\tau' \oplus (h_{00} \upharpoonright |\tau'|)) \).

因此对于任何路径 \( x \in [T_i^0] \),

\( (x \oplus \theta^{(i)})' \equiv_T x \oplus \theta^{(i+1)} \equiv_T \psi_i^{-1}(x) \oplus \theta^{(i+1)} \).

由于构造是一致的，可以直接验证 (1)-(7) 都满足。这完成了定理 11.2.2 的证明.

## 11.2.2 哈灵顿定理的证明

我们遵循 Hjorth [50] 的表述。由定理 2.6.5，对于任何递归序数 \( \beta \ge \omega \)，存在一个 \( n \in \omega \) 使得 \( [n] = \beta \) 且集合 \( \{m \mid m <_n n\} \) 是递归的。我们选择这样的序数 \( \beta \) 和相应的 \( n \).

对于每个 \( m = 3 \cdot 5^k < \alpha_0 \)，令 \( \{i_{j,m}\}_{j<\omega} \) 为满足以下条件的数字序列：

\( i_{0,m} = \Phi_k(m) \)

和

\( i_{j+1,m} = \Phi_k(m+j+1) \).

由定理 2.6.5 的证明，我们可以假设对所有 \( j \) 都有 \( m \le i_{j,m} < i_{j+1,m} \). 显然集合 \( \{(i_{j,m}, m) \mid (\exists k)(m = 3 \cdot 5^k \land \alpha_0 < n \land j \in \omega)\} \) 是递归的.

### 引理 11.2.7.

- (i) 对于任何 \( m = 3 \cdot 5^k < \alpha_0 \) 和 \( j < \omega \)，\( i_{j,m} < i_{j+1,m} \).

- (ii) 对于任何 \( l < \alpha_0 \)，集合 \( \{m \mid (\exists k)(i_{0,m} < l < m = 3 \cdot 5^k < \alpha_0)\} \) 是有限的;

- (iii) 集合 \( \{(m,l) \mid (\exists k)(i_{0,m} < l < m = 3 \cdot 5^k < \alpha_0)\} \) 是递归的;

- (iv) 若 \( m = 3 \cdot 5^k < \alpha_0 \) 且 \( |m| = \lim_{n \to \infty} \alpha_n \)，其中 \( \{\beta_i\} \) 是一个递增的极限序数序列，那么对于任何 \( i \)，存在一个 \( m' = 3 \cdot 5^{k'} < \alpha_0 \) 且 \( |m'| > \beta_i \)，使得对于任何 \( m'' = 3 \cdot 5^{k''} < \alpha_0 \) 且 \( |m'| > |m''| \)，都有 \( |i_{0,m'}| > |m''| \).

