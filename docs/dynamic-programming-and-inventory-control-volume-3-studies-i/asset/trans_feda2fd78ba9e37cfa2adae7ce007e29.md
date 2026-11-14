

现在 \(\beta T(u_1)(x) \le T(\beta u_1)(x)\)。假设我们找到 \(\beta\) 使得 \(\gamma < \beta \le 1\) 且 \(\beta M(u_1)(x) \le M(u_2)(x)\)。

那么将由下面的引理 8.1 得出 \(\beta u_1(x) \le u_2(x), \forall x\)，故 \(\beta \le \gamma\)，这将是一个矛盾。验证所需性质意味着

\(K\beta + \inf_{w \ge 0} (\beta c_0(w) + \beta u_1(x+w)) \le K + \inf_{w \ge 0} (c_0(w) + u_2(x+w))\).

利用 \(\gamma u_1 \le u_2\)，只需验证

\(K\beta + \inf_{w \ge 0} (\beta c_0(w) + \beta u_1(x+w)) \le K + \inf_{w \ge 0} (c_0(w) + \gamma u_1(x+w))\).

or

\(K\beta + \inf_{w \ge 0} (c_0(w) + \beta u_1(x+w)) \le K + \inf_{w \ge 0} (c_0(w) + \gamma u_1(x+w))\).

我们希望 \(\beta > \gamma\)。由于 \(u_1 - C_0 \le 0, u_2 - C_0 \le 0\)，我们还有

\(\inf_{w \ge 0} (c_0(w) + \beta u_1(x+w)) \le \inf_{w \ge 0} (c_0(w) + \gamma u_1(x+w)) + (\beta - \gamma)C_0\).

因此，只需选择 \(\beta\) 使得

\((\beta - \gamma)C_0 \le K(1 - \beta)\).

设

\(\rho = \frac{K}{C_0}\).

我们可以取

\(\beta = \frac{\rho + \gamma}{\rho + 1}, \gamma < \beta \le 1\).

我们现在证明存在性。我们从一些初步结果开始。

**引理 8.1.** 设 \(\psi \in C\) 且 \(S(w) = z \in C\) 是

\(z = \min[\psi, T(z)]\).

的解。若 \(\zeta \in C\) 满足

\(\zeta \le \psi, \zeta \le T(\zeta)\),

则 \(\zeta \le z\)。

证明。考虑映射 \(\Sigma : C \to C\)，定义为

\(\Sigma(z) = \min[\psi, T(z)]\).

算子 \(\Sigma\) 是收缩映射且单调递增。由于根据假设

\(z = \Sigma^n(z), \zeta \le \Sigma^n(\zeta)\),

故

\(z - \zeta \ge \Sigma^n(z) - \Sigma^n(\zeta)\).

令 \(n\) 趋于 \(\infty\)，右边趋于 0。因此结果已得到。

**引理 8.2.** 算子 \(S\) 是凹的，即

\(S(\lambda \psi_1 + (1-\lambda)\psi_2) \ge \lambda S(\psi_1) + (1-\lambda)S(\psi_2), \forall \lambda \in [0, 1]\)

**练习 8.1.** 证明 \(T\) 是凹的，并进一步验证 \(S\) 也是凹的，利用引理 8.1。

**引理 8.3.** 算子 \(S\) 是单调递增的

**练习 8.2.** 利用引理 8.1 证明引理 8.3。

接下来定义

\(A(z)(x) = S(M)(z)(x)\)。

**练习 8.3.** 验证 \(A\) 是凹的且单调递增。

令 \(\overline{u}\) 为 \(\overline{u} = T(\overline{u})\) 的唯一解。则 \(0 \le \overline{u} \le C_0\)。我们可以定义 \(\lambda > 0\) 使得 \(\lambda \overline{u}(x) \le K, \forall x\)。

我们给出如下结论

**引理 8.4.** 设 \(z, \zeta \in C\) 为正，且 \(\beta \in [0, 1]\) 使得

\(z(x) - \zeta(x) \le \beta z(x), \forall x,\)

则

\(A(z)(x) - A(\zeta)(x) \le \beta(1-\lambda)A(z)(x), \forall x.\)

根据假设，\((1-\beta)z(x) \le \zeta(x)\)。利用 \(A\) 的单调性和凹性，我们可以写出

\(A(\zeta)(x) \ge A((1-\beta)z)(x) \ge (1-\beta)A(z)(x) + \beta A(0)(x)\)

然而 \(A(0) = S(M(0)) = S(K)\)。但由 \(\lambda \overline{u}(x) \le K\) 且 \(\lambda \overline{u}(x) = \lambda T(\overline{u})(x)\)，故 \(\lambda \overline{u}(x) \le T(\lambda \overline{u})(x)\)，利用引理 8.1 可得

\(\lambda \overline{u}(x) \le S(K) = A(0).\)

综合以上结果，我们写出

\(A(\zeta)(x) \ge (1-\beta)A(z)(x) + \beta \lambda \overline{u}(x).\)

现在

\(A(z) \le T A(z) \quad \overline{u} = T \overline{u}\)

并且通过与引理 8.1 类似的推理，我们推导出 \(A(z)(x) \le \overline{u}(x)\)。因此

\(A(\zeta)(x) \ge (1-\beta)A(z)(x) + \beta \lambda A(z)(x),\)

这正是性质 (8.3.8)。

我们可以转向定理 8.4 中存在性的直接证明。

证明。存在性：

这等同于证明算子 \(A\) 有一个不动点。我们考虑递减序列

\(u^{n+1} = A(u^n) \quad u^0 = \overline{u}\)

我们有

\(u^0 \ge \dots \ge u^n \ge \dots\)

由于 \(u^0 - u^1 \le u^0\)，由引理 8.4 可得

\(A(u^0) - A(u^1) \le (1-\lambda)A(u^0),\)

即

\(u^1 - u^2 \le (1-\lambda)u^1.\)

迭代可得

\(u^m - u^{m+1} \le (1-\lambda)^m u^m \le (1-\lambda)^m u^0.\)

我们容易推断，对于 \( n \ge m \)

\( u^m - u^n \le \frac{(1-\lambda)^m}{\lambda} u^0. \)

令 \( n \) 趋于 \(\infty\)，我们得到 \( u^n \downarrow u \)，因此也有

\( u^m - u \le \frac{(1-\lambda)^m}{\lambda} u^0 \le \frac{(1-\lambda)^m}{\lambda} C_0, \)

这证明了极限 \( u \in C(X) \)。接下来我们检查

\( M(u^n) \downarrow M(u) \text{ and in } C \)

\( T(u^{n+1}) \downarrow T(u) \text{ and in } C \)

由于

\( u^{n+1} = \min[M(u^n), T(u^{n+1})], \)

极限 \( u \) 是一个解。证明已完成。

## 8.4. 概率解释

在定理 8.2 中，我们已经用随机控制问题的值函数给出了函数方程 (8.18) 解的一种概率解释。该表述中没有停时。以类似于最优停止中所见的方式（参见定理 7.5），我们将得到一种涉及停时作为决策变量的不同表述。事实上，我们将解释第二种表述，即方程 (8.3.3)。同样，为简化技术细节，我们仅限于 (8.3.3)，这意味着成本 \( l(x, v) \) 是有界的。

我们采取一种控制策略 \( V = \{v_1, \cdots, v_n, \cdots \} \)，其中 \( v_n \) 是 \( \mathcal{Y}_n \) 可测的，且属于 \( U \)。控制策略 \( W\) 将以略有不同的方式定义。我们考虑一组 \( \mathcal{Y}^m \) 停时 \( \{\tau_1, \cdots, \tau_n, \cdots \} \)。我们假设没有累积，即 \( \tau_n < \tau_{n+1}, \forall n, \text{a.s.} \)。考虑 \( \tau_n \) 之前事件的 \(\sigma\)-代数 \( \mathcal{Y}^{\tau_n} \) 以及一组 \( \mathcal{Y}^{\tau_n} \) 可测的随机变量 \( \xi_{\tau_n} \)，其值在 \( X = R^d \) 中。\( \xi_{\tau_n} \ge 0, \neq 0 \)。我们关联如下定义的控制 \( W = \{w_1, \cdots, w_n, \cdots \} \)

\( w_{\tau_n} = \xi_{\tau_n}, \)

\( w_j = 0 \text{ if } j \neq \tau_1, \cdots, \tau_n, \cdots \)

我们可以验证 \( w_j \) 是 \( \mathcal{Y}^j \) 可测的，\( \forall j \)。然后我们可以考虑 \( J_x(V, W) \) 并将其写为

\( J_x(V, W) = E^{V, W}_x \sum_{n=1}^\infty \alpha^{\tau_n - 1} \left[ K + c_0(\xi_{\tau_n}) + l(y_{\tau_n} + \xi_{\tau_n}, v_{\tau_n}) + \sum_{j=\tau_n+1}^{\tau_{n+1}-1} \alpha^{j-\tau_n} l(y_j, v_j) \right]. \)

对于最优反馈 \( \hat{v}(x), \hat{w}(x) \)，我们关联如下定义的控制策略 \( \hat{V}, \hat{W} \)

\( \hat{v}_n = \hat{v}(y_n) \)

\( \hat{w}_n = \hat{w}(y_n) \)

接下来定义

\(\hat{\tau}_1 = \inf\{n \ge 1 | \hat{w}_n \neq 0\}\)

\(\hat{\tau}_2 = \inf\{n \ge \hat{\tau}_1 + 1 | \hat{w}_n \neq 0\}\)

\(\dots\)

和

\(\hat{\xi}_{\hat{\tau}_j} = \hat{w}_{\hat{\tau}_j}\)。

使用与定理 7.2 类似的论证，我们可以得到

\(u(x) = J_*(V, \hat{W}) = \inf J_*(V, W)\)

本页故意留空

## 带设置成本的库存控制

冲动控制技术将现在应用于研究库存控制中的设置成本情况。第 5 章中引入的基准库存策略将被 H. Scarf [35] 引入并由许多作者研究的 s, S 策略概念所取代。我们将首先考虑一种无积压的确定性情况，但不同于第 5 章第 5.3 节的情况。

### 9.1. 确定性模型

### 9.1.1. 模型描述。

我们假设库存按以下方式演变

\[
(9.1.1) \quad y_{n+1} = y_n + v_n - D \quad y_1 = x,
\]

并受约束

\[
(9.1.2) \quad v_n \ge 0, y_n \ge 0.
\]

新之处在于状态约束。没有未满足的需求。由于需求 \( D \) 是确定性的，这转化为对控制的约束，该约束取决于状态

\[
(9.1.3) \quad v_n \ge D - y_n.
\]

定义 \( V = \{v_1, \cdots, v_n, \cdots\} \)，我们考虑目标函数

\[
(9.1.4) \quad J_x(V) = \sum_{n=1}^{\infty} \alpha^{n-1} [K \mathbb{I}_{v_n > 0} + c v_n + h y_n],
\]

并且我们想要研究值函数

\[
(9.1.5) \quad u(x) = \inf_V J_x(V).
\]

新增项是固定成本 \( K \mathbb{I}_{v_n > 0} \)，仅在订单 \( v_n \) 不为 0 时支付。这不是一个连续函数。如果我们记

\[
(9.1.6) \quad l(x, v) = K \mathbb{I}_{v > 0} + cv + hx,
\]

则函数 \( l(x, v) \) 在 \( v \) 中不连续。然而它是下半连续的。

### 9.1.2. 贝尔曼方程。

贝尔曼方程写为

\[
(9.1.7) \quad u(x) = hx + \inf_{v \ge (D-x)^+} [K \mathbb{I}_{v > 0} + cv + \alpha u(x + v - D)].
\]

这个函数方程属于第 4 章研究的一般类别。我们将关注具体方面。

第一个重要事实如下

