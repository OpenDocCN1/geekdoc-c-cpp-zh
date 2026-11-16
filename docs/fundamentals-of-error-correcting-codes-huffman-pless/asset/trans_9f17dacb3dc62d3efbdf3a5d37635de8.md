

由于 \((0 : 0 : 0)\) 不是射影点，\(\mathcal{F}_m(\mathbb{F}_q)\) 上的奇点仅在 \(\gcd(m, q) \neq 1\) 时才可能存在；在这种情况下，曲线上的每一点都是奇点。因此，如果 \(m\) 和 \(q\) 互素，\(\mathcal{F}_m(\mathbb{F}_q)\) 是非奇异的。

## 练习 773 费马曲线 \(\mathcal{F}_m(\mathbb{F}_q)\) 在示例 13.3.1 中定义。考虑由 \(x^3 + y^3 + z^3 = 0\) 给出的曲线 \(\mathcal{F}_3(\mathbb{F}_q)\)。

- (a) 在 \(\mathcal{F}_3(\mathbb{F}_2)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_2)\) 的三个射影点 \((x : y : z)\)。
- (b) 在 \(\mathcal{F}_3(\mathbb{F}_4)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_4)\) 的九个射影点 \((x : y : z)\)。
- (c) 在 \(\mathcal{F}_3(\mathbb{F}_8)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_8)\) 的九个射影点 \((x : y : z)\)。域 \(\mathbb{F}_8\) 可见示例 3.4.3。

## 示例 13.3.2 设 \(q = r^2\)，其中 \(r\) 是素幂。Hermitian 曲线 \(\mathcal{H}_r(\mathbb{F}_q)\) 是 \(\mathbb{F}_q\) 上的射影平面曲线，由 \(f(x, y, z) = x^{r+1} - y^r z - y z^r = 0\) 定义。

在练习 774 中，你将证明 \(\mathcal{H}_r(\mathbb{F}_q)\) 只有一个无穷远点，即 \((0 : 1 : 0)\)。我们证明在 \(\mathcal{H}_r(\mathbb{F}_q)\) 上有 \(r^3\) 个仿射点 \((x : y : 1)\) 属于 \(\mathbb{P}^2(\mathbb{F}_q)\)。由于 \(z = 1\)，\(x^{r+1} = y^r + y\)。但 \(y^r + y = \text{Tr}_2(y)\)，其中 \(\text{Tr}_2 : \mathbb{F}_{r^2} \to \mathbb{F}_r\) 是从 \(\mathbb{F}_{r^2}\) 到 \(\mathbb{F}_r\) 的迹象映射。由于其像是 1 维空间 \(\mathbb{F}_r\) 的非零子空间，\(\text{Tr}_2\) 是满射。因此其核是 \(\mathbb{F}_{r^2}\) 的 1 维子空间，这意味着有 \(r\) 个元素 \(y \in \mathbb{F}_{r^2}\) 满足 \(\text{Tr}_2(y) = 0\)。当 \(\text{Tr}_2(y) = 0\) 时，\(x^{r+1} = 0\) 有一个解 \(x = 0\)；这在 \(\mathcal{H}_r(\mathbb{F}_q)\) 上导出 \(r\) 个仿射点。如果 \(x \in \mathbb{F}_{r^2}\)，\(x^{r+1} = x^r x = (r + 1)(x - 1) = 0\)，且 \(\mathbb{F}_{r^2}\) 中 \(x_{r+1}\) 的非零元素恰好是满足 \(\beta^{r-1} = 1\) 的那些元素。当 \(y\) 是 \(\mathbb{F}_{r^2}\) 中 \(\text{Tr}_2(y) \neq 0\) 的 \(r^2 - r\) 个元素之一时，有 \(r + 1\) 个解 \(x \in \mathbb{F}_{r^2}\) 满足 \(x^{r+1} = \text{Tr}_2(y)\)。这导出了 \((r^2 - r)(r + 1) = r^3 - r\) 个更多的仿射点。因此，\(\mathcal{H}_r(\mathbb{F}_q)\) 有 \(r^3 - r + r = r^3\) 个仿射点，总共 \(r^3 + 1\) 个射影点。

## 练习 774 设 \(q = r^2\)，其中 \(r\) 是素幂。Hermitian 曲线 \(\mathcal{H}_r(\mathbb{F}_q)\) 在示例 13.3.2 中定义。

- (a) 证明 \(\mathcal{H}_r(\mathbb{F}_q)\) 是非奇异的。提示：在 \(\mathbb{F}_q\) 中，\(r = 0\)，因为 \(r\) 是 \(\mathbb{F}_q\) 特征的倍数。
- (b) 证明 \((0 : 1 : 0)\) 是 \(\mathcal{H}_r(\mathbb{F}_q)\) 上唯一的无穷远点。
- (c) 在 \(\mathcal{H}_2(\mathbb{F}_4)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_4)\) 的八个仿射点 \((x : y : 0)\)。
- (d) 在 \(\mathcal{H}_4(\mathbb{F}_{16})\) 上找出 \(\mathbb{P}^2(\mathbb{F}_{16})\) 的 64 个仿射点 \((x : y : 1)\)。表 5.1 给出了域 \(\mathbb{F}_{16}\)。

## 练习 775 Klein 四次曲线 \(\mathcal{K}_4(\mathbb{F}_q)\) 是 \(\mathbb{F}_q\) 上由四次齐次多项式方程 \(f(x, y, z) = x^3 y + y^3 z + z^3 x = 0\) 定义的射影曲线。

- (a) 找出 \(f\) 的三个偏导数。
- (b) 证明如果 \(\mathbb{F}_q\) 的特征为 3，则 \(\mathcal{K}_4(\mathbb{F}_q)\) 是非奇异的。
- (c) 如果 \((x : y : z)\) 是 \(\mathcal{K}_4(\mathbb{F}_q)\) 的奇点，利用 \(f(x, y, z) = 0\) 证明 \(x^3 = -3y^3 z\)，并利用 \(f_x(x, y, z) = 0\) 和 \(f_z(x, y, z) = 0\) 证明 \(z^3 x = 9y^3 z\)。
- (d) 如果 \((x : y : z)\) 是 \(\mathcal{K}_4(\mathbb{F}_q)\) 的奇点，利用 \(x^3 y + y^3 z + z^3 x = 0\) 和部分 (c) 证明 \(7y^3 z = 0\)。
- (e) 利用部分 (d)，证明如果 \(\mathbb{F}_q\) 的特征不是 7，则 \(\mathcal{K}_4(\mathbb{F}_q)\) 是非奇异的。
- (f) 在 \(\mathcal{K}_4(\mathbb{F}_2)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_2)\) 中的三个射影点。
- (g) 在 \(\mathcal{K}_4(\mathbb{F}_4)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_4)\) 中的五个射影点。
- (h) 在 \(\mathcal{K}_4(\mathbb{F}_8)\) 上找出 \(\mathbb{P}^2(\mathbb{F}_8)\) 中的 24 个射影点。域 \(\mathbb{F}_8\) 可见示例 3.4.3。

在考察曲线上的点时，我们需要知道它们的次数。点的次数 \(m\) 取决于所考虑的域。设 \(q = p^r\)，其中 \(p\) 是素数，且 \(m \ge 1\) 是整数。映射 \(\sigma_q : \mathbb{F}_{q^m} \to \mathbb{F}_{q^m}\)，由 \(\sigma_q(\alpha) = \alpha^q\) 给出，是 \(\mathbb{F}_{q^m}\) 的一个自同构，它固定 \(\mathbb{F}_q\)；\(\alpha_q\)，其中 \(\sigma_q\) 是第 3.6 节中定义的 Frobenius 映射。如果 \(P = (x, y)\) 或 \(P = (x : y : z)\) 的坐标在 \(\mathbb{F}_{q^m}\) 中，则令 \(\sigma_q(P)\) 分别表示 \((\sigma_q(x), \sigma_q(y))\) 或 \((\sigma_q(x) : \sigma_q(y) : \sigma_q(z))\)。根据练习 776，在射影情况下，对点应用 \(\sigma_q\) 时，射影点的代表元的选择无关紧要。假设 \(f\) 属于 \(\mathbb{F}_q[x, y]\) 或 \(\mathbb{F}_q[x, y, z]\)，在后一种情况下 \(f\) 是齐次的。因此 \(f\) 定义了 \(\mathbb{F}_q\) 或 \(\mathbb{F}_{q^m}\) 上的仿射曲线或射影曲线。练习 776 表明，如果 \(P\) 是 \(\mathcal{X}/(\mathbb{F}_{q^m})\) 上的点，那么 \(\sigma_q(P)\) 也是。因此 \(\{\sigma_q^i(P) \mid i \ge 0\}\) 是 \(\mathcal{X}/(\mathbb{F}_{q^m})\) 上的一组点；然而，由于 \(\sigma_q^m\) 是 \(\mathbb{F}_{q^m}\) 的恒等自同构，该集合中最多有 \(m\) 个不同的点。这使我们能够扩展点的概念。一个 _点_ \(P\) _在_ \(\mathcal{X}/(\mathbb{F}_q)\) _上在_ \(\mathbb{F}_q\) _上的次数为_ \(m\) 是 \(m\) 个不同点的集合 \(P = \{P_0, \dots, P_{m-1}\}\)，其中 \(P_i\) 在 \(\mathcal{X}/(\mathbb{F}_{q^m})\) 上，且 \(P_i = \sigma_q^i(P_0)\)；\(P\) 在 \(\mathbb{F}_q\) 上的 _次数_ 记作 deg(\(P\))。\(\mathcal{X}/(\mathbb{F}_q)\) 上次数为 1 的点称为 _有理点_ 或 \(\mathbb{F}_q\)_-有理点_。\(^2\) 该定义受到实数上多项式的众所周知情况的启发。共轭是固定实数的复数自同构。带有实系数的多项式 \(p(x) = x^2 - 4x + 5\) 没有实根，但有两个复共轭根，\(2 + i\) 和 \(2 - i\)。在我们的新术语中，\(p(x)\) 的根被归为一对 \(\{2 + i, 2 - i\}\)，它是 \(p(x) = 0\) 上在实数上次数为 2 的点（尽管每个单独的根都不是实数）。在 \(\mathbb{F}_q\) 上次数为 \(m\) 的点 \(P = \{P_0, \dots, P_{m-1}\}\) 的定义中，要求 \(P_i\) 互不相同。从 \(\mathbb{A}^2(\mathbb{F}_{q^m})\) 或 \(\mathbb{P}^2(\mathbb{F}_{q^m})\) 中的一点 \(P_0\) 开始，\(P_i = \sigma_q^i(P_0)\) 对于 \(0 \le i \le m - 1\) 可能不互不相同。在这种情况下，不同的 \(P_i\) 构成一个次数较小的点；参见练习 777(c)。

## 练习 776 做如下练习：

- (a) 设 \((x : y : z) = (x' : y' : z') \in \mathbb{P}^2(\mathbb{F}_{q^m})\)。证明 \((\sigma_q(x) : \sigma_q(y) : \sigma_q(z)) = (\sigma_q(x') : \sigma_q(y') : \sigma_q(z'))\)。
- (b) 设 \(f\) 是 \(\mathbb{F}_q[x, y]\) 中的多项式或 \(\mathbb{F}_q[x, y, z]\) 中的齐次多项式。证明如果 \(P\) 分别在 \(\mathbb{A}^2(\mathbb{F}_{q^m})\) 或 \(\mathbb{P}^2(\mathbb{F}_{q^m})\) 中，且 \(f(P) = 0\)，则 \(f(\sigma_q(P)) = 0\)。

## 示例 13.3.3 设 \(f(x, y, z) = x^3 + xz^2 + z^3 + y^2z + yz^2 \in \mathbb{F}_2[x, y, z]\)。由该方程确定的曲线是 _椭圆曲线_ 的一个例子。在 \(\mathcal{X}/(\mathbb{F})\) 上的无穷远点，其中 \(\mathbb{F}\) 是 \(\mathbb{F}_2\) 的任意扩展域，满足 \(z = 0\)；因此 \(x^3 = 0\)，这意味着 \(y\) 可以是任意非零值。因此，\(\mathcal{X}/(\mathbb{F})\) 上只有一个无穷远点，即 \(P_\infty = (0 : 1 : 0)\)。无穷远点在 \(\mathbb{F}_2\) 上的次数为 1（即它是有理的），因为其坐标在 \(\mathbb{F}_2\) 中。

