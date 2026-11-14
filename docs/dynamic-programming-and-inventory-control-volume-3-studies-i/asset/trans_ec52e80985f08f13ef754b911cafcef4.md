

其中

\(\tilde{v}_j^n(x_1, \cdots, x_j) = v_j(x_j), \forall j \le n\)
\(\tilde{v}_j^n(x_1, \cdots, x_j) = v_0, \forall j \ge n+1.\)

可得

\(u^n(x) = E^{V^n, x} \sum_{j=1}^n \alpha^{j-1} l(y_j, \tilde{v}_j^n) + \alpha^n E^{V^n, x} w_0(y_{n+1}).\)

因此

\(u^n(x) = E^{V^n, x} \sum_{j=1}^\infty \alpha^{j-1} l(y_j, \tilde{v}_j^n)\)

\(u^n(x) = J_x(\tilde{V}^n).\)

由于 \(\tilde{V}^n \in \mathcal{V}^n\)，引理的证明已完成。

为了最终给出最大解的解释，我们引入集合

\(\mathcal{V} = \{V|V = (v_1, \cdots, v_i, \cdots) \text{ where }\)
\(v_i = v_i(x_1, \cdots, x_i)\)
\(\alpha^{j-1} E^{V, x} \bar{u}(y_j) \to 0 \text{ as } j \to +\infty \}.\)

我们可以给出如下定理

### 定理 4.5. 在假设 (4.3.1)、(4.3.2)、(4.3.6) 下，函数方程 (4.3.7) 在 0 和 \(w_0\) 之间的最大解 \(\bar{u}(x)\) 由

\(\bar{u}(x) = \inf_{V \in \mathcal{V}} J_x(V)\)

给出。

### 证明. 考虑控制策略 \(\tilde{V}^n\)。我们将检查对于任意 \(n\)，它是否属于 \(\mathcal{V}\)。我们需要验证

\(\alpha^{k-1} E^{V^n, x} \bar{u}(y_k) \to 0 \text{ as } k \to +\infty.\)

我们可以假设 \(k \ge n+1\)。由于 \(\bar{u}(x) \le w_0(x)\)，只需验证

\(\alpha^{k-1} E^{V^n, x} w_0(y_k) \to 0 \text{ as } k \to +\infty.\)

然而

\(\alpha^{k-1} E^{V^n, x} w_0(y_k) = E^{V^n, x} \sum_{j=k}^\infty \alpha^{j-1} l(y_j, v_0),\)

当 \(k \ge n+1\) 时。

但级数

\(E^{V^n, x} \sum_{j=n+1}^\infty \alpha^{j-1} l(y_j, v_0) \le u^n(x) < \infty,\)

因此是收敛级数。故确实

\(E^{V^n, x} \sum_{j=k}^\infty \alpha^{j-1} l(y_j, v_0) \to 0 \text{ as } k \to \infty.\)

从而得出结果。接下来我们知道

\(u^n(x) = J_x(\tilde{V}^n).\)

因此

\( u^n(x) \ge \inf_{V \in \mathcal{V}} J_x(V) \),

并且

\( \bar{u}(x) \ge \inf_{V \in \mathcal{V}} J_x(V) \).

另一方面，对于任意控制（不一定属于 \(\mathcal{V}\)），我们可以写出

\(\bar{u}(x) \le E^{V,x} \sum_{j=1}^{n} \alpha^{j-1} l(y_j, v_j) + \alpha^n E^{V,x} \bar{u}(y_{n+1})\)

\(\le J_x(V) + \alpha^n E^{V,x} \bar{u}(y_{n+1}).\)

现在如果 \( V \in \mathcal{V} \)，第二项在 \( n \to \infty \) 时趋于 0。因此我们可以断言

\( \bar{u}(x) \le J_x(V) \forall V \in \mathcal{V} \),

这完成了定理的证明。

### 注记. 我们不声称右边 (4.4.7) 的下确界可达。而且最大解是上半连续（u.s.c.）的，而不是下半连续（l.s.c.）的。

### 4.5. 唯一性

我们考虑函数方程 (4.3.7) 在区间 \((0, w_0)\) 上的解的唯一性问题。唯一性的充要条件是最小解和最大解重合。要证明最小解和最大解重合，只需证明最优控制 \(\bar{V} \in \mathcal{V}\)。另一种方法是使用收缩性质（当可用时）。

### 定理 4.6. 假设 \( l(x, v) \) 有界。那么 (4.3.7) 存在唯一解。

### 证明. 我们可以使用收缩性质。回顾 \( B \) 表示 \( X = R^d \) 上有界函数空间。我们注意到 (4.3.7) 可以写成关于映射

\( T : B \to B, z = Tw, \)

的不动点，其中

\( Tw(x) = \inf_{v \in U} [l(x, v) + \alpha \Phi^v(w)], \)

并且由于 \( l \) 有界，我们可以将 \( T \) 定义为从 \( B \) 到 \( B \) 的映射。当 \( \alpha < 1 \) 时，显然 \( T \) 是收缩映射。因此存在唯一的不动点。

### 注记. 由于 \( w_0 \) 有界，唯一性也直接由条件 (4.4.6) 始终满足这一事实得出。

此结果可以以多种方式推广。

### 定理 4.7. 假设

(4.5.1) \( 0 \le l(x, v) \le h|x| + c|v| + l_0, \)

(4.5.2) \( \Phi^v(|x|) \le \theta|x| + \lambda|v| + \mu, \)

且 \( U \) 为紧集。如果 \( \alpha\theta < 1 \)，则 (4.3.7) 在线性增长函数空间 \( B_1 \) 中的解存在且唯一。

### 证明. 在等式 (4.5.2) 中，我们用 \(|x|\) 表示函数 \(x \to |x|\)。我们为 \( B_1 \) 配备一个等价范数

\( ||u||_1 = \sup_x \frac{|u(x)|}{1 + \sigma|x|}, \)

其中 \(\sigma\) 可以任意选取且将被选得足够小。对于 \( v \in U \)，我们有

\( l(x, v) \le h|x| + l_1 \)

\( \Phi^v(|x|) \le \theta|x| + m \)

再次考虑在定理证明中定义的映射 \( T \)，这次是从 \( B_1 \) 到 \( B_1 \)。注意对于 \( w \in B_1 \) 和 \( v \in U \)，我们有

\( \alpha \Phi^v(w) \le \alpha[|w|](1 + \sigma\Phi^v(|x|)) \)
\( \le \alpha[|w|](1 + \sigma\theta|x| + \sigma m). \)

那么

\( ||Tw_1 - Tw_2|| \le \alpha|w||| \sup_x \frac{1 + \sigma\theta|x| + \sigma m}{1 + \sigma|x|}. \)

得益于假设，我们有

\( \alpha \sup_x \frac{1 + \sigma\theta|x| + \sigma m}{1 + \sigma|x|} \le \alpha(1 + \sigma m), \)

并且通过选择足够小的 \(\sigma\)，右边的数严格小于 1。因此 \( T \) 在 \( B_1 \) 中是收缩映射。存在性和唯一性随之而来。

### 注记. 同样，可以将前面的结果视为最大解和最小解重合这一事实的后果。确实，为了明确起见，取 \(v_0 = 0\)。我们首先注意到，从增长假设中我们有

(4.5.3) \quad w_0(x) \le \frac{h|x|}{1 - \alpha\theta} + \frac{l_0}{1 - \alpha} + \frac{\alpha m}{1 - \alpha\theta}.

取任意控制策略 \(V\)。从 \(V\) 的定义出发，参见 (4.4.6)，利用 \(\bar{u} \le w_0\) 这一事实，只需证明

\( \alpha^{j-1} E^{V,x}[y_j] \to 0 \text{ as } j \to +\infty. \)

然而

\( E^{V,x}[|y_{j+1}| | Y_j] = \Phi^{v_j}[x](y_j) \)
\( \le \theta|y_j| + m. \)

因此

\( E^{V,x}[|y_{j+1}|] \le \theta E^{V,x}[|y_j|] + m, \)

由此可得

\( E^{V,x}[|y_j|] \le \theta^{j-1}|x| + m \sum_{k=0}^{j-2} \theta^k \)
\( \le \theta^{j-1}|x| + m(j-1)\theta^{j-2}, \)

因为不失一般性，\(\theta \ge 1\)。由此可得 \(\alpha^{j-1} E^{V,x}[y_j] \to 0\) 当 \(j \to \infty\)。因此最大解和最小解重合，存在唯一性。

在 \( U \) 不是紧集的情况下，可以在以下情形下获得唯一性

(4.5.4)
\( h|x| + c|v| \le l(x, v) \)
\( \Phi^v(\Phi^0)^{j-1}|x| \ge (\Phi^0)^j|x|, \forall j, \forall v \in U \)

### 定理 4.8.

我们采用定理 4.7 的假设，但将 \( U \) 紧集替换为 (4.5.4)。那么我们在 \( B_1 \) 中拥有函数方程 (4.3.7) 解的存在性和唯一性。

### 证明. 证明包括在等式 (4.3.7) 右边找到 \( v \) 的一个先验界。我们将证明只需取 \( v \in U \) 使得

\( |v| \le \frac{l_0}{1-\alpha}, \)

然后我们可以假设 \( U \) 是紧集。确实，从 (4.3.7) 和对 \( l(x, v) \) 的假设出发，我们可以验证解 \( u(x) \) 必须满足

\( u(x) \ge h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x|. \)

因此

\( l(x, v) + \alpha \Phi^v u(x) \ge c|v| + h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x|, \)

因此只需寻找 \( v \) 使得

\( c|v| + h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x| \le w_0(x). \)

但是（回顾 \( v_0 = 0 \)）

\( w_0(x) \le \frac{l_0}{1-\alpha} + h \sum_{j=1}^\infty (\alpha \Phi^0)^{j-1}|x|, \)

因此只需选取 \( |v| \le \frac{l_0}{c(1-\alpha)}. \)

本页故意留空

## 没有设置成本的库存控制

在本章中，我们将第 4 章的一般结果应用于库存控制的情况。我们将考虑不允许缺货（无积压）和允许缺货（积压）的情况。在不允许缺货的情况下，无法满足的需求将丢失，并产生罚金。设置成本的情况将在第 9 章中考虑。

### 5.1. 不允许缺货.

### 5.1.1. 问题的提出.

我们处于第 4 章第 4.2.3 节的情况。如果 \( y_n \) 表示时刻 n 的库存，则有演化

(5.1.1) \( y_{n+1} = (y_n + v_n - D_n)^+ \quad y_1 = x, \)

其中 \( v_n \) 是时刻 n 的控制，\( D_n \) 是需求，它是一组独立随机变量的序列，概率密度为 \( f(x) \)。我们用 \( F(x) \) 表示与 \( f(x) \) 关联的累积分布函数（CDF）。控制策略（称为 \( V \)）由一组可测函数 \( v_n(D_1, \cdots D_{n-1}) \) 定义。对于 \( n=1 \)，\( v_1 \) 只是一个确定数。引入 \(\sigma\)-代数 \( \mathcal{F}^n = \sigma(D_1, \cdots D_{n-1}) \)，\( v_n \) 是 \( \mathcal{F}^n \) 可测的。算子 \( \Phi^v \) 由

(5.1.2) \( \Phi^v \varphi(x) = E\varphi((x+v-D)^+). \)

给出。

转移概率由

(5.1.3) \( \pi(x, v; d\eta) = \bar{F}(x+v)\delta(\eta) + f(x+v-\eta)\mathbb{1}_{\eta \le x+v} d\eta, \)

给出，因此

(5.1.4) \( \Phi^v \phi(x) = \bar{F}(x+v)\phi(0) + \int_0^{x+v} f(x+v-\eta)\phi(\eta)d\eta. \)

集合 \( U = [0, \infty) \) 不是紧集。算子 \( \Phi^v \) 对测试函数 \( \phi(x, v) \) 的像由

(5.1.5) \( \Phi^v \phi_0(x) = \phi(0,v)\bar{F}(x+v) + \int_0^{x+v} \phi(x+v-\eta, v)f(\eta)d\eta, \)

给出，且假设 (4.3.1) 得到满足。

我们定义函数 \( l(x, v) \) 如下

(5.1.6) \( l(x, v) = cv + hx + p \int_{x+v}^{\infty} (\xi - x - v)f(\xi)d\xi. \)

它包含订购成本（纯变动成本）、持有成本和失去销售的罚金。我们注意到不等式

(5.1.7) \( cv + hx \le l(x, v) \le cv + hx + p\bar{D}, \)

