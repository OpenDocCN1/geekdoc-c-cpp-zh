

## 9.10 关于 $\mathbb{F}_4$ 上的加法码

我们现在将注意力转向一类因其与量子纠错和量子计算的联系而引人关注的码 [44]。这些 $\mathbb{F}_4$ 上的码可能不是 $\mathbb{F}_4$ 上的线性码，但是是 $\mathbb{F}_2$ 上的线性码。给出适当的内积定义后，量子纠错中使用的码是自正交的。本章中已经介绍的许多思想都可以推广到这一族码中。

长度为 $n$ 的 $\mathbb{F}_4$ 上的加法码 $\mathcal{C}$ 是 $\mathbb{F}_4^n$ 的一个对向量加法封闭的子集。因此，$\mathcal{C}$ 是 $\mathbb{F}_4^n$ 的一个加法子群。因为对于 $\mathbf{x} \in \mathcal{C}$ 有 $\mathbf{x} + \mathbf{x} = \mathbf{0}$，所以 $\mathcal{C}$ 是一个二元向量空间。因此，对于某个满足 $0 \le k \le 2n$ 的 $k$，$\mathcal{C}$ 有 $2^k$ 个码字；如果已知最小权重 $d$，则 $\mathcal{C}$ 将被称为一个 $(n, 2^k)$ 码或一个 $(n, 2^k, d)$ 码。注意，$\mathbb{F}_4$ 上的加法码与 $\mathbb{F}_4$ 上的线性码不同，因为它可能不对标量乘法封闭，因此可能在 $\mathbb{F}_4$ 上是非线性的。一个 $(n, 2^k)$ 加法码 $\mathcal{C}$ 具有由 $k$ 个码字组成的二元基。$\mathcal{C}$ 的生成矩阵是任何 $k \times n$ 矩阵，其行构成 $\mathcal{C}$ 的一个二元基。

### 示例 9.10.1

作为 $\mathbb{F}_4$ 上的线性码，[6, 3, 4] 六码的生成矩阵为

```
[1 0 0 1 \omega \omega; 0 1 0 \omega 1 \omega; 0 0 1 \omega \omega 1]
```

然而，将六码视为一个加法 $(6, 2^6, 4)$ 码，它的生成矩阵为

```
[1 0 0 1 \omega \omega; \omega 0 0 \omega \overline{\omega} \overline{\omega}; 0 1 0 \omega 1 \omega; 0 \omega 0 \overline{\omega} \omega \overline{\omega}; 0 0 1 \omega \omega 1; 0 0 \omega \overline{\omega} \overline{\omega} \omega]
```

后一个矩阵的第二、第四和第六行是通过将前一个矩阵的三行乘以 $\omega$ 得到的。

在量子码与 $\mathbb{F}_4$ 上的加法码之间的联系 [44] 中，加法码出现了一个称为迹内积的自然内积。回顾第 3.8 节，迹 $\text{Tr}_2 : \mathbb{F}_4 \to \mathbb{F}_2$ 定义为 $\text{Tr}_2(\alpha) = \alpha + \alpha^2$。或者，由于 $\mathbb{F}_4$ 中的共轭 $-$ 由 $\overline{\alpha} = \alpha^2$ 给出，$\text{Tr}_2(\alpha) = \alpha + \overline{\alpha}$。因此 $\text{Tr}_2(0) = \text{Tr}_2(1) = 0$ 且 $\text{Tr}_2(\omega) = \text{Tr}_2(\overline{\omega}) = 1$。根据引理 3.8.5，$\text{Tr}_2(\alpha + \beta) = \text{Tr}_2(\alpha) + \text{Tr}_2(\beta)$，这表明 $\text{Tr}_2$ 是 $\mathbb{F}_2$-线性的。$\mathbb{F}_4^n$ 上的迹内积 $\langle \cdot, \cdot \rangle_T$ 定义如下。对于 $\mathbb{F}_4^n$ 中的 $\mathbf{x} = x_1 x_2 \cdots x_n$ 和 $\mathbf{y} = y_1 y_2 \cdots y_n$，令

$$
\langle \mathbf{x}, \mathbf{y} \rangle_T = \text{Tr}_2(\mathbf{x}, \mathbf{y}) = \sum_{i=1}^n (x_i \overline{y_i} + \overline{x_i} y_i),
$$

其中 $\langle \cdot, \cdot \rangle$ 是厄米内积。最右侧的等式由 $\text{Tr}_2$ 的 $\mathbb{F}_2$-线性以及 $\overline{\overline{\alpha}} = \alpha$ 这一事实得出。在处理迹内积时，有用的观察是：如果 $\alpha = 0$ 或 $\beta = 0$，则 $\text{Tr}_2(\alpha\overline{\beta}) = 0$；否则 $\text{Tr}_2(\alpha\overline{\beta}) = 1$。迹内积的以下基本性质的证明留作练习。

### 引理 9.10.2

如果 $\mathbf{x}, \mathbf{y},$ 和 $\mathbf{z}$ 在 $\mathbb{F}_4^n$ 中，则：

- (a) $\langle \mathbf{x}, \mathbf{y} \rangle_T = 0$，
- (b) $\langle \mathbf{x}, \mathbf{y} \rangle_T = \langle \mathbf{y}, \mathbf{x} \rangle_T$，
- (c) $\langle \mathbf{x} + \mathbf{y}, \mathbf{z} \rangle_T = \langle \mathbf{x}, \mathbf{z} \rangle_T + \langle \mathbf{y}, \mathbf{z} \rangle_T$，且
- (d) 如果 $\text{wt}(\mathbf{x})$ 是偶数，则 $\langle \mathbf{x}, \omega \mathbf{x} \rangle_T = 0$；如果 $\text{wt}(\mathbf{x})$ 是奇数，则 $\langle \mathbf{x}, \omega \mathbf{x} \rangle_T = 1$。

### 练习 554

计算 $\langle 1\omega 1\bar{\omega}\bar{\omega}1, 1\bar{\omega}\omega\bar{\omega}\omega 1\omega \rangle_T$。

### 练习 555

证明引理 9.10.2。

像往常一样，定义加法码 $\mathcal{C}$ 的迹对偶 $\mathcal{C}^{L^\perp}$ 为 $\mathcal{C}^{L^\perp} = \{ \mathbf{y} \in \mathbb{F}_4^n \mid \langle \mathbf{u}, \mathbf{y} \rangle_T = 0 \text{ 对所有 } \mathbf{u} \in \mathcal{C} \}$。

练习 556 表明，如果 $\mathcal{C}$ 是一个加法 $(n, 2^k)$ 码，那么 $\mathcal{C}^{L^\perp}$ 是一个加法 $(n, 2^{2n-k})$ 码。如果 $\mathcal{C} \subseteq \mathcal{C}^{L^\perp}$，则加法码 $\mathcal{C}$ 是迹自正交的；如果 $\mathcal{C} = \mathcal{C}^{L^\perp}$，则是迹自双的。因此，一个迹自双加法码是一个 $(n, 2^n)$ 码。Höhn [134] 证明，适用于 $\mathbb{F}_4$ 上线性码的相同 MacWilliams 方程也适用于 $\mathbb{F}_4$ 上的加法码；即（参见 (M$_3$)）

\[
W_{\mathcal{C}^{L^\perp}}(x, y) = \frac{1}{|\mathcal{C}|} W_{\mathcal{C}}(y - x, y + 3x).
\]

### 练习 556

证明如果 $\mathcal{C}$ 是一个加法 $(n, 2^k)$ 码，那么 $\mathcal{C}^{L^\perp}$ 是一个加法 $(n, 2^{2n-k})$ 码。

要从加法码 $\mathcal{C}_1$ 得到一个等价加法码 $\mathcal{C}_2$，与 $\mathbb{F}_4$ 上的线性码一样，我们可以对 $\mathcal{C}_1$ 的坐标进行置换和缩放。对于线性码，随后允许对得到的向量进行共轭；对于加法码，我们实际上可以更一般地进行共轭，如下所示。两个加法码 $\mathcal{C}_1$ 和 $\mathcal{C}_2$ 是等价的，前提是存在一个将 $\mathcal{C}_1$ 的码字映射到 $\mathcal{C}_2$ 的码字的映射，该映射由坐标置换、随后是坐标缩放（$\mathbb{F}_4$ 的元素），随后是对某些坐标进行共轭组成。就生成矩阵而言，如果 $G_1$ 是 $\mathcal{C}_1$ 的生成矩阵，那么可以通过对 $G_1$ 进行列置换、列缩放，然后对某些得到的列进行共轭，得到 $\mathcal{C}_2$ 的一个生成矩阵。按照自然的方式，我们现在定义加法码 $\mathcal{C}$ 的自同构群，记作 $\text{Aut}(\mathcal{C)}$，由所有将 $\mathcal{C}$ 的码字发送到 $\mathcal{C}$ 的码字的坐标置换、坐标缩放和坐标共轭映射组成。根据练习 557，自正交（或迹自双）码不改变迹自正交性（或迹自双性）。然而，练习 558 表明，如果 $\mathcal{C}_1$ 在 $\mathbb{F}_4$ 上是线性的，并且 $\mathcal{C}_2$ 是通过仅对 $\mathcal{C}_1$ 的某些坐标进行共轭得到的，那么 $\mathcal{C}_2$ 可能不是线性的！

### 练习 557

验证如果 $\mathbf{x}'$ 和 $\mathbf{y}'$ 是通过对 $\mathbb{F}_4^n$ 中的向量 $\mathbf{x}$ 和 $\mathbf{y}$ 进行坐标置换、坐标缩放和对某些坐标进行共轭得到的，那么 $\langle \mathbf{x}', \mathbf{y}' \rangle_T = \langle \mathbf{x}, \mathbf{y} \rangle_T$。

### 练习 558

找出一个在 $\mathbb{F}_4$ 上是线性的码 $\mathcal{C}$ 的示例，使得当仅对第一个坐标进行共轭时，得到的码不再在 $\mathbb{F}_4$ 上是线性的。

我们现在专注于迹自双加法码。对于 $\mathbb{F}_4$ 上的线性码，厄米自双码和迹自双码之间没有区别。

### 定理 9.10.3

设 $\mathcal{C}$ 为 $\mathbb{F}_4$ 上的线性码。那么 $\mathcal{C}$ 是厄米自双码当且仅当 $\mathcal{C}$ 是迹自双码。

**证明：** 首先假设 $\mathcal{C}$ 是一个 $[n, n/2]$ 厄米自双码。那么对于 $\mathcal{C}$ 中的所有 $\mathbf{x}$ 和 $\mathbf{y}$，有 $\langle \mathbf{x}, \mathbf{y} \rangle = 0$。因此 $\langle \mathbf{x}, \mathbf{y} \rangle_T = \text{Tr}_2(\langle \mathbf{x}, \mathbf{y} \rangle) = 0$，这意味着 $\mathcal{C} \subseteq \mathcal{C}^{L_T}$。作为一个加法码，$\mathcal{C}$ 是一个 $(n, 2^n)$ 码，因此根据练习 556，$\mathcal{C}^{L_T}$ 也是一个 $(n, 2^n)$ 码。因此 $\mathcal{C} = \mathcal{C}^{L_T}$，$\mathcal{C}$ 是迹自双码。

现在假设 $\mathcal{C}$ 是一个 $(n, 2^n)$ 迹自双码。因为 $\mathcal{C}$ 是 $\mathbb{F}_4$ 上的线性码，如果 $\mathbf{x} \in \mathcal{C}$，那么 $\alpha \mathbf{x} \in \mathcal{C}$，因此 $\langle \mathbf{x}, \alpha \mathbf{x} \rangle_T = 0$。根据引理 9.10.2(d)，对于所有 $\mathbf{x} \in \mathcal{C}$，$\text{wt}(\alpha \mathbf{x})$ 是偶数。根据定理 1.4.10，$\mathcal{C} \subseteq \mathcal{C}^{L_H}$。因为 $\mathcal{C}$ 作为 $\mathbb{F}_4$ 上的线性码的维数为 $n/2$，所以 $\mathcal{C}^{L_H}$ 的维数也是 $n/2$，这意味着 $\mathcal{C}$ 是厄米自双码。

与仅包含偶权重码字的厄米自双码不同，迹自双加法码可能包含奇权重码字；根据定理 9.10.3，这样的码不能在 $\mathbb{F}_4$ 上是线性的。这导致了以下定义：如果加法码 $\mathcal{C}$ 是迹自双的且所有码字都有偶权重，则 $\mathcal{C}$ 是 Type II 码。练习 383 适用于 $\mathbb{F}_4$ 上的加法码，因为 MacWilliams 方程 (M$_a$) 成立。特别是，如果 $\mathcal{C}$ 是长度为 $n$ 的 Type II 码，那么 $\mathcal{C}^{L_T} = \mathcal{C}$ 包含一个权重为 $n$ 的码字，这意味着 $n$ 是偶数。根据推论 9.2.2，$\mathbb{F}_4$-线性厄米自双码存在当且仅当 $n$ 是偶数。因此，Type II 加法码存在当且仅当 $n$ 是偶数。如果 $\mathcal{C}$ 是迹自双的但某个码字有奇权重（在这种情况下，码不能是 $\mathbb{F}_4$-线性的），则该码是 Type I 码。$n \times n$ 单位矩阵生成一个 $(n, 2^n)$ Type I 加法码，这意味着 Type I 码对于所有 $n$ 都存在。

Type II 加法码有一个类似于 Gleason 定理的类比，它与厄米自双线性码的 Gleason 定理相同；参见 [291, 第 7.7 节]。

### 定理 9.10.4

如果 $\mathcal{C}$ 是一个 Type II 加法码，那么

$$
W_{\mathcal{C}}(x, y) = \sum_{i=0}^{\lfloor \frac{n}{2} \rfloor} a_i g_6(x, y)^{2i} g_7(x, y)^{n-3i} g_1(x, y)^i.
$$

其中 $g_6(x, y) = y^2 + 3x^2$ 且 $g_7(x, y) = y^6 + 45x^4y^2 + 18x^6$。所有 $a_i$ 都是有理数且 $\sum a_i = 1$。

迹自双加法码的最小距离也有一个界 [291, 定理 33]。如果 $d_{\text{I}}$ 和 $d_{\text{II}}$ 分别是 Type I 和 Type II 加法码的最小距离，

