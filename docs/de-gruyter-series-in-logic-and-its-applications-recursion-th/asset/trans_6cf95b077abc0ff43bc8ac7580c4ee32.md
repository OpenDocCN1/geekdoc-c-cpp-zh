

设 \( f : \omega \to \omega^3 \) 为递归双射，使得若 \( f(n) = (n_0, n_1, n_2) \) 且 \( n > 0 \)，则 \( n > n_0 \)。序列的构造如下：

第 0 阶段。令 \(\langle p_0, q_0 \rangle = \langle p_0, q_0 \rangle\) 且 \( v_0 = 0 \)。令 \(\{\gamma_i\}_{i < \omega}\) 为可数集合

\(\{ \alpha < \omega_2 \mid p_0(\alpha) \text{ 已定义 } \lor p_0 \Vdash \text{``}q_0(\alpha) \text{ 已定义''} \}\)。

的枚举。对 \( i, j < \omega \) 令 \(\beta_{0(i,j)} = \gamma_i\)。列表中每个 \(\gamma_i\) 都出现无穷多次，以确保它被对角化无穷多次。

第 \( n + 1 \) 阶段。我们将其分解为 \( 2^n + 1 \) 个子阶段。

在子阶段 \( j \le 2^n \) 时，定义 \(\{v'_\sigma\}_{\sigma \in 2^{n+1}}\) 和 \(\{(p'_\sigma, q'_\sigma)\}_{\sigma \in 2^{n+1}}\)，使得对每个 \( \alpha \notin \beta[n] \) 和 \( \sigma \in 2^n \)，都有 \( p'_{\sigma^\frown 0}(\alpha) = p'_{\sigma^\frown 1}(\alpha) \)。

对于 \( \sigma \in 2^n \) 和 \( i < 2 \)，令 \( v'_{\sigma^\frown i} = v'_\sigma \)。若 \( \beta[n] < \omega_1 \)，则

\( p^0_{\sigma^\frown i}(\alpha) = \begin{cases} p_\sigma(\alpha) & : \alpha \notin \beta[n], \\ \tau \in p_\sigma(\alpha) \mid \tau < t_{p_\sigma(\alpha)}(i) \lor \tau \succeq t_{p_\sigma(\alpha)}(i) & : \text{否则.} \end{cases} \)

令 \( q^0_{\sigma^\frown i} = q_\sigma \)。若 \( \beta[n] \ge \omega_1 \)，则 \( p^0_{\sigma^\frown i} = p_\sigma \) 且 \( q^0_{\sigma^\frown i} \) 是一个名称，使得

\( p_\sigma \Vdash q^0_{\sigma^\frown i}(\alpha) = \begin{cases} \check{q}_\sigma(\alpha) & : \alpha \notin \beta[n], \\ \tau \in p_\sigma \land \tau \in \check{q}_\sigma(\alpha) \land (\tau < t_{q_\sigma(\alpha)}(i) \lor \tau \succeq t_{q_\sigma(\alpha)}(i)) & : \text{否则.} \end{cases} \)

因此 \(\{p^0_\sigma\}_{\sigma \in 2^{n+1}}\) 满足 (2)。现在有两种情况需要考虑。

情况 1。\( \beta[n] \ge \omega_1 \)。由于 (4) 仅包含不小于 \( \omega_1 \) 的序数，令 \(\langle p_{\sigma^\frown i}, \check{q}_{\sigma^\frown i} \rangle = \langle p^0_{\sigma^\frown i}, q^0_{\sigma^\frown i} \rangle\)，\( \beta[n+1, i, j] = \beta[n, i, j] \)，且对每个 \( \sigma \in 2^n \) 和 \( i < 2 \)，\( v_{\sigma^\frown i} = v_\sigma \)，并进入下一阶段。

情况 2。\( \beta[n] < \omega_1 \)。固定 \( 2^n \) 的一个枚举 \(\{\sigma_j\}_{1 \le j \le 2^n}\)。

子阶段 \( j + 1 \)。根据引理 9.1.18，存在一个 \( m > |v'_\sigma| \) 和一个 \(\langle p'', q'' \rangle \le \langle p^j_{\sigma^\frown 0}, q^j_{\sigma^\frown 0} \rangle\)，使得对任何 \(\langle p'', q'' \rangle \le \langle p', q' \rangle\)，都有 \(\langle p'', q'' \rangle \Vdash x(m) = i\)。定义

\( p''(\alpha) = \begin{cases} p'(\alpha) & : \alpha \notin \beta[n], \\ p^j_{\sigma^\frown 1}(\alpha) & : \text{否则.} \end{cases} \)

注意，对任何 \( \alpha \notin \beta[n] \)，都有 \( p^j_{\sigma^\frown 0}(\alpha) = p^j_{\sigma^\frown 1}(\alpha) \)。我们有 \(\langle p'', q''_{\sigma^\frown 1} \rangle \le \langle p^j_{\sigma^\frown 1}, q^j_{\sigma^\frown 1} \rangle\)。令 \(\langle r_1, s_1 \rangle \le \langle p'', q''_{\sigma^\frown 1} \rangle\)，使得对某个 \( v^{j+1}_1 > v^j_1 \) 在 \( 2^{m+1} \) 中，\(\langle r_1, s_1 \rangle \Vdash x(m) = 1\) 且 \(\langle r_1, s_1 \rangle \Vdash x \restriction m + 1 = q^{j+1}_{\sigma^\frown 1}\)。定义

\( r'_0(\alpha) = \begin{cases} r_1(\alpha) & : \alpha \notin \beta[n], \\ p'(\alpha) & : \text{否则.} \end{cases} \)

则 \( r'_0 \le p' \)，所以 \(\langle r'_0, q'' \rangle \Vdash x(n) = i\) 对 \( i < 2 \) 成立。因此存在一个 \(\langle r_0, s_0 \rangle \le \langle r'_0, q' \rangle\)，使得 \(\langle r_0, s_0 \rangle \Vdash x(m) = 0\) 且 \(\langle r_0, s_0 \rangle \Vdash x \restriction m + 1 = v^j_{\sigma^\frown 0}\) 对某个 \( v^j_{\sigma^\frown 0} > v^j_\sigma \) 在 \( 2^{m+1} \) 中成立。令 \(\langle p^{j+1}_{\sigma^\frown 0}, q^{j+1}_{\sigma^\frown 0} \rangle = \langle r_0, \check{s}_0 \rangle\)。定义

\( p^{j+1}_{\sigma^\frown 1}(\alpha) = \begin{cases} r_0(\alpha) & : \alpha \notin \beta[n], \\ r_1(\alpha) & : \text{否则.} \end{cases} \)

则 \((p_{a_{j-1}}^{j+1}, s_1) \le (r_1, s_1)\)。令 \(q_{a_{j-1}}^{j+1} = s_1\)。现在对于 \(j' \neq j\) 和 \(i < 2\)，令 \(v_{a_{j'-1}}^{j+1} = v_{a_{j'-1}}^j\)，且

\(p_{a_{j-1}}^{j+1}(a) = \begin{cases} p_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^j(a) = p_{a_{j-1}}^{j+1}(a), \\ p_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^j(a) = p_{a_{j-1}}^{j+1}(a), \\ p_{a_{j-1}}^{j+1}(a) : \text{否则.} \end{cases}\)

令 \(q_{a_{j-1}}^{j+1}\) 为一个名称，使得

\(q_{a_{j-1}}^{j+1}(a) = \begin{cases} q_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^{j+1} = p_{a_{j-1}}^{j+1} \wedge p_{a_{j-1}}^{j+1} \Vdash q_{a_{j-1}}^j(a) = q_{a_{j-1}}^j(a), \\ q_{a_{j-1}}^{j+1}(a) : p_{a_{j-1}}^{j+1} = p_{a_{j-1}}^{j+1} \wedge p_{a_{j-1}}^{j+1} \Vdash q_{a_{j-1}}^j(a) = q_{a_{j-1}}^j(a), \\ q_{a_{j-1}}^{j+1}(a) : \text{否则.} \end{cases}\)

这完成了子阶段 \(j + 1\) 的构造。

对于 \(\sigma \in 2^n\) 和 \(i < 2\)，令 \((p_{a_\sigma}^{j+1}, q_{a_\sigma}^{j+1}) = (p_{a_\sigma}^{j+1}, q_{a_\sigma}^{j+1})\) 且 \(v_{a_\sigma} = v_{a_\sigma}^{j+1}\)。令 \(\{\gamma_i\}_{i < \omega}\) 为可数集合

\(\{\alpha < \omega \mid (\exists \sigma)(\sigma \in 2^{n+1} \wedge (p_\alpha(a) \text{ 已定义} \vee p_\alpha \Vdash \neg \dot{q}_\alpha(a) \text{ 已定义}'))\}\)。

的枚举。令 \(\beta_{n+1,i,j} = \gamma_i\) 对 \(i, j < \omega\)。这结束了第 \(n + 1\) 阶段的构造。最后，对每个 \(n\)，令 \(a_n = \beta_{(n)}\)。

所定义的序列立即满足条件 (1)-(4)，因此定理 9.1.7 的证明完成。\(\square\)

### 9.1.3 练习

- **练习 9.1.1.** 证明存在一个偏序 \(\langle 2^{<\omega}, \le_P \rangle\)，使得每个大小不超过 \(2^{\aleph_0}\) 的局部可数偏序都可嵌入其中。

- **练习 9.1.2.** 证明定理 9.1.4。

- **练习 9.1.3.** (Sacks [107])。若对任意 \(p \in \mathbf{P}\) 都有 \(|\{q \mid q \le_P p\}| < \aleph_0\)，则称偏序 \(\langle \mathbf{P}, \le_P \rangle\) 为局部有限。证明 \(\langle 2^\omega, \le_P \rangle\) 中的每个局部有限偏序都可嵌入到 \(\langle \mathscr{D}, \le \rangle\) 中。

- **练习 9.1.4.** 证明存在一个大小为 \(2^{\aleph_0}\) 的图灵度独立集 \(X\)。

- **练习 9.1.5.** 证明定理 9.1.6。

## 9.2 将局部有限上半格嵌入到 \(\langle \mathscr{P}, \le \rangle\)

### 9.2.1 嵌入一个上半格

**定义 9.2.1.** 若对任意 \(p, q \in P\)，都存在 \(r \in P\) 使得 \(r\) 是 \(p\) 和 \(q\) 关于 \(\le\) 的最小上界，则称偏序 \(\langle P, \le \rangle\) 为一个 *上半格*。

我们用 \(p \cup q\) 表示 \(p\) 和 \(q\) 的最小上界。显然 \((\mathscr{P}, \le)\) 是一个上半格。在附加假设下，以下内容加强了练习 9.1.3。

**定理 9.2.2** (Sacks [117])。假设 CH。每个局部有限上半格 \(\langle 2^\omega, \subseteq, \cup \rangle\) 都可嵌入到 \((\mathscr{P}, \le)\) 中。

在 [117] 中，Sacks 询问定理 9.2.2 的结论是否是 ZFC 的一个定理。Groszek 和 Slaman 对该问题给出了否定答案。

**定理 9.2.3** (Groszek and Slaman [40])。存在一个模型 \(\mathbb{N} \models \text{ZFC} + 2^{\aleph_0} = \aleph_2\)，其中存在一个局部有限上半格 \(\langle \omega_2, \le, \cup \rangle\)，它不可嵌入到 \((\mathscr{P}, \le, \cup)\) 中。

### 9.2.2 定理 9.2.3 的证明

假设 \(\mathbb{M} \models \text{ZFC} + \text{GCH}\)。令 \(\langle X_\beta \rangle_{\beta < \omega_2}\) 为 \(\mathbb{M}\) 中 \(\mathscr{P}(\omega_1)\) 的一个双切枚举。令 \(\mathbb{U} = \langle \mathbb{U}, \le_{\mathbb{U}}, \cup \rangle\) 为 \(\mathbb{M}\) 中的一个上半格，使得

- (1) \(|\mathbb{U}| = \aleph_2\);
- (2) \(\omega_2 \subseteq \mathbb{U}\)，且
- (3) \((\forall \alpha < \omega_1)(\forall \beta < \omega_2)(\beta < \omega_1 \rightarrow (\alpha \le_\alpha \alpha \cup \beta \leftarrow \alpha \in X_\beta))\)。

令 \(\mathbb{P} = \Pi_{\alpha < \omega_2} \mathbb{P}_\alpha\) 为 Cohen 强迫条件的有限支持 \(\omega_2\)-积。根据定理 6.1.11，我们有：

**引理 9.2.4.** \(\mathbb{P}\) 是 c.c.c. 的，因而保持基数。

假设 \(G\) 是 \(\mathbb{P}\)-泛滤。则 \(G\) 可视为实数的一个 \(\omega_2\)-序列 \(\langle G_\alpha \rangle_{\alpha < \omega_2}\)。根据引理 6.1.6，我们有

**引理 9.2.5.** 对于任何 \(\mathbb{P}\)-泛滤集 \(G\)，\(\mathbb{M}[G] \models 2^{\aleph_0} = \aleph_2\)。

假设存在一个 \(\mathbb{P}\)-泛滤集 \(G\) 使得 \(\mathbb{M}[G] \models \text{``}\exists f \text{ 是 } \mathbb{U} \to (\mathscr{P}, \le) \text{ 的一个嵌入}\text{''}\)。令 \(p_0\) 满足

\(p_0 \Vdash \text{``} f \text{ 是 } \mathbb{U} \text{ 到 } (\dot{\mathscr{P}}, \dot{\le}) \text{ 的一个嵌入}\text{''}\)。

那么对于 \(\alpha \le \omega_1\) 和 \(n < \omega\)，存在 \(G\) 中的一个条件 \(p_{\alpha, n} \le p_0\)，使得

\(p_{\alpha, n} \Vdash f(\alpha)(n) = i\)

对某个 \(i < 2\) 成立。

给定一个条件 \(p\)，令 \(a_p = \min\{a \mid (\forall \beta \ge a)(p(\beta) \text{ 未定义})\}\)。设

\(a_\alpha = \sup\{a_{p_{\gamma, n}} \mid \gamma < \omega_1\}\)。

则 \(a_0 < \omega_2\)。令 \(\mathbb{P}_{< a_0} = \Pi_{\beta < a_0} \mathbb{P}_\beta\) 和 \(\mathbb{P}_{\ge a_0} = \Pi_{\beta \ge a_0} \mathbb{P}_\beta\)。则 \(f(\alpha) \in \mathbb{M}[G_{< a_0}]\)，其中 \(G_{< a_0} = \langle \langle \beta, G_\beta \rangle \mid \beta < a_0 \rangle\) 是一个 \(\mathbb{P}_{< a_0}\)-泛滤集。由于 \(\mathbb{P} = \mathbb{P}_{< a_0} \times \mathbb{P}_{\ge a_0}\)，根据定理 6.1.9，\(G_{\ge a_0} = \langle \langle \beta, G_\beta \rangle \mid \beta \ge a_0 \rangle\) 是在 \(\mathbb{M}[G_{< a_0}]\) 上的一个 \(\mathbb{P}_{\ge a_0}\)-泛滤集。显然 \(\mathbb{P}_{< a_0}\) 和

