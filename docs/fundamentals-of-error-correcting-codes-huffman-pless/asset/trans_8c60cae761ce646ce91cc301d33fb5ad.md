

练习 407 执行以下操作：(a) 为 $\widehat{\mathcal{H}}_3$ 选择一个生成矩阵，并在 $\mathbb{F}_2^6$ 中选择任意方便的权重 2 向量 $\mathbf{v}$。证明非线性码 $\mathcal{C} = \mathbf{v} + \widehat{\mathcal{H}}_3$ 是齐次的。(b) 应用 Prange 定理的第 (i) 部分来求 $C^*$ 的权重分布，并将你的答案与在练习 394 中找到的 $\mathcal{H}_3$ 的权重 1 副类的权重分布进行比较。(c) 证明 $\widehat{\mathcal{H}}_3$ 的权重为 1 的副类不是齐次的。

练习 408 假设 [24, 12, 8] 扩展二进制 Golay 码的一个权重 4 副类是齐次的，使用 Prange 定理和练习 401 的结果，求 [23, 12, 7] 二进制 Golay 码的一个权重 3 副类的权重分布。

## 7.7 其他权重枚举子

码存在其他包含更多关于码字详细信息的权重枚举子。如果 $\mathbf{c} \in \mathbb{F}_q^n$ 且 $\alpha \in \mathbb{F}_q$，令 $s_\alpha(\mathbf{c})$ 为 $\mathbf{c}$ 中等于 $\alpha$ 的分量个数。令 $\mathbb{F}_q = \{\alpha_0, \alpha_1, \dots, \alpha_{q-1}\}$。多项式

$W_C(x_{\alpha_0}, x_{\alpha_1}, \dots, x_{\alpha_{q-1}}) = \sum_{\mathbf{c} \in C} \prod_{\alpha \in \mathbb{F}_q} x_\alpha^{s_\alpha(\mathbf{c})}$

称为 $C$ 的 *完全权重枚举子*。注意，如果 $P$ 是置换矩阵，则 $CP$ 和 $C$ 具有相同的完全权重枚举子；但是，通常如果 $M$ 是单项矩阵，则 $CM$ 和 $C$ 不具有相同的完全权重枚举子。如果 $q=2$，则 $W_C(x_0, x_1)$ 是普通权重枚举子 $W_C(x_1, x_0)$。MacWilliams [213] 还证明了 $C$ 的完全权重枚举子与 $C^\perp$ 的完全权重枚举子之间存在一个恒等式。如果 $q=2$，该恒等式与 $(M_3)$ 相同。如果 $q=3$，且 $\mathbb{F}_3 = \{0, 1, 2\}$，则该恒等式为

$W_{C'}(x_0, x_1, x_2) = \frac{1}{|C|} W_C(x_0 + x_1 + x_2, x_0 + \xi x_1 + \xi^2 x_2, x_0 + \xi^2 x_1 + \xi x_2), \quad (7.12)$

其中 $\xi = e^{2\pi i / 3}$ 是单位的原始复数立方根。如果 $q=4$，且 $\mathbb{F}_4 = \{0, 1, \omega, \overline{\omega}\}$ 如第 1.1 节所示，则存在两个 MacWilliams 恒等式，取决于考虑的是厄米对偶还是普通对偶；参见 [291]。对于普通对偶，有

$W_{C'}(x_0, x_1, x_\omega, x_{\overline{\omega}}) = \frac{1}{|C|} W_C(x_0 + x_1 + x_\omega + x_{\overline{\omega}}, x_0 + x_1 - x_\omega - x_{\overline{\omega}}, x_0 - x_1 - x_\omega + x_{\overline{\omega}}, x_0 - x_1 + x_\omega - x_{\overline{\omega}}). \quad (7.13)$

而对于厄米对偶，MacWilliams 恒等式为

$W_{C', H}(x_0, x_1, x_\omega, x_{\overline{\omega}}) = \frac{1}{|C|} W_C(x_0 + x_1 + x_\omega + x_{\overline{\omega}}, x_0 + x_1 - x_\omega - x_{\overline{\omega}}, x_0 - x_1 - x_\omega + x_{\overline{\omega}}, x_0 - x_1 + x_\omega - x_{\overline{\omega}}). \quad (7.14)$

练习 409 回顾在示例 1.3.3 中引入的 [4, 2] 三元四元码 $\mathcal{H}_{3,2}$，其生成矩阵为

$G = \begin{bmatrix} 1 & 0 & 1 & 1 \\ 0 & 1 & 1 & 2 \end{bmatrix}$。

求 $\mathcal{H}_{3,2}$ 的完全权重枚举子，并证明 MacWilliams 恒等式 (7.12) 成立；使用计算机代数系统将最有帮助。$\diamond$

练习 410 设 $\mathcal{C}$ 为 $\mathbb{F}_4$ 上的 [4, 2, 3] 扩展 Reed-Solomon 码，其生成矩阵为

$G = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & \omega & \overline{\omega} & 0 \end{bmatrix}$。

- (a) 证明 $\mathcal{C}$ 在普通内积下是自对偶的。
- (b) 求 $\mathcal{C}$ 的完全权重枚举子，并证明 MacWilliams 恒等式 (7.13) 成立；使用计算机代数系统将最有帮助。$\diamond$

练习 411 设 $\mathcal{C}$ 为 $\mathbb{F}_4$ 上的 [6, 3, 4] 六元码，其生成矩阵如示例 1.3.4 所示：

$G = \begin{bmatrix} 1 & 0 & 0 & 1 & \omega & \omega \\ 0 & 1 & 0 & \omega & 1 & \omega \\ 0 & 0 & 1 & \omega & \omega & 1 \end{bmatrix}$。

它是厄米自对偶的。求 $\mathcal{C}$ 的完全权重枚举子，并证明 MacWilliams 恒等式 (7.14) 成立；使用计算机代数系统将最有帮助。$\diamond$

练习 412 回顾 $-$ 表示如第 1.3 节所述在 $\mathbb{F}_4$ 中的共轭。执行以下操作：

- (a) 证明 $W_C^2(x_0, x_1, x_\omega, x_{\overline{\omega}}) = W_C^2(x_0, x_1, x_{\overline{\omega}}, x_\omega)$。
- (b) 证明 (7.13) 成立当且仅当 (7.14) 成立。$\diamond$

练习 413 证明对于 $\mathbb{F}_4$ 上的码，$W_C(x, y) = W_C^L(y, x, x, x)$。$\diamond$

李权重枚举子有时用于特征为 $p \neq 2$ 的域上的码。对于这样的域，令 $\mathbb{F}_q = \{a_0 = 0, a_1, \dots, a_{r-1}, -a_1, \dots, -a_r\}$，其中 $r = (q-1)/2$。$\mathcal{C}$ 的李权重枚举子是多项式

$W_C^L(x_0, x_1, \dots, x_{q-1}) = \sum_{c \in C} x_0^{k(c)} \prod_{i=1}^r x_{a_i}^{(c)_i + (-c)_i}$。

李权重枚举子基本上将完全权重枚举子中的变量数量减半。如果 $q > 3$，则 $W_C(x_0, x_0) = W_C^L(x_0, x_1)$。$\mathcal{C}$ 的李权重枚举子与 $C^\perp$ 的李权重枚举子之间也存在一种关系，该关系通过在完全权重枚举子的 MacWilliams 恒等式中令 $x_a$ 等于 $x_{-a}$ 来获得。

[291] 中还为其他码族和其他类型的权重枚举子建立了 MacWilliams 恒等式。

## 7.8 权重约束

在本节中，我们将介绍偶二进制码中码字权重的约束，回顾如果二进制码的所有码字都具有偶权重，则该码称为偶码。下面来自定理 1.4.3 的恒等式对于两个向量 x, y \in F_2^n 将很有用：

wt(x + y) = wt(x) + wt(y) - 2wt(x \cap y), (7.15)

其中 x \cap y 是 F_2^n 中的向量，其在 x 和 y 都为 1 的位置上恰好有 1。当两个向量 x 和 y 之间的普通内积为 0 时，我们说这些向量正交，并用 x \perp y 表示。

以下是 (7.15) 的一个简单推论。

### 引理 7.8.1 设 x 和 y 为 F_2^n 中的两个向量。

- (i) 假设 wt(x) \equiv 0 (mod 4)。则 wt(x + y) \equiv wt(y) (mod 4) 当且仅当 x \perp y，且 wt(x + y) \equiv wt(y) + 2 (mod 4) 当且仅当 x \not\perp y。
- (ii) 假设 wt(x) \equiv 2 (mod 4)。则 wt(x + y) \equiv wt(y) (mod 4) 当且仅当 x \not\perp y，且 wt(x + y) \equiv wt(y) + 2 (mod 4) 当且仅当 x \perp y。

练习 414 证明引理 7.8.1。

我们称一个二进制向量为四重偶向量，如果其权重可被 4 整除。一个二进制向量称为二重偶向量，如果其权重是偶数但不可被 4 整除。回顾定理 1.4.8，如果一个二进制码仅包含四重偶向量，则该码是自正交的。我们将主要关注并非所有码字都是四重偶向量的码。我们将介绍偶二进制码的一种分解，分解为称为码的核、H-平面和 A-平面的部分。H-平面或 A-平面是由 x 和 y 展开的 2 维空间，该空间记为 span{x, y}。核、H-平面和 A-平面定义如下：

- 码 C 的核是子码 H = C \cap C^{\perp}。
- 如果 x 和 y 是四重偶向量但不正交，则我们称 span{x, y} 为 H-平面。注意，如果 span{x, y} 是 H-平面，则根据引理 7.8.1(i)，wt(x + y) \equiv 2 (mod 4)，因此 H-平面包含两个非零四重偶向量和一个二重偶向量。
- 如果 x 和 y 是二重偶向量但不正交，则我们称 span{x, y} 为 A-平面。如果 span{x, y} 是 A-平面，则根据引理 7.8.1(ii)，wt(x + y) \equiv 2 (mod 4) 仍然成立；因此 A-平面包含三个二重偶向量。

练习 415 证明如果 C 是一个 [n, k] 偶二进制码，那么要么 C 是自正交的，要么其核的维数最多为 k - 2。

练习 416 设 C 是一个不是自正交的 2 维偶二进制码。证明以下内容：

- (a) C 的核是 {0}。
- (b) 要么 C 包含三个二重偶向量，在这种情况下它是一个 A-平面，要么 C 包含恰好两个非零四重偶向量，在这种情况下它是一个 H-平面。

