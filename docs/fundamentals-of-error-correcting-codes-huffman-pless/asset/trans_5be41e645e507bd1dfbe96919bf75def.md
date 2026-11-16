

对于某个多项式 \(a(x)\)。将 (5.13) 乘以 \(\sigma(x)\)，将 (5.14) 乘以 \(b_I(x)\)，得到

\(a_I(x)\sigma(x)^{2^l} + b_I(x)\sigma(x)S(x) = r_I(x)\sigma(x)\) and
\(a(x)b_I(x)^{2^l} + \sigma(x)b_I(x)S(x) = \omega(x)b_I(x).\) (5.15) (5.16)

模 \(x^{2^l}\) 下，这些蕴含

\(r_I(x)\sigma(x) \equiv \omega(x)b_I(x) \pmod{x^{2^l}}.\) (5.17)

由于 \(\deg \sigma(x) \le t\)，根据 \(I\) 的选取，\(\deg(r_I(x)\sigma(x)) = \deg r_I(x) + \deg \sigma(x) < t + t = 2t\)。根据引理 5.4.11(iv)、\(I\) 的选取，以及 \(\deg \omega(x) < t\) 这一事实，\(\deg(\omega(x) \times b_I(x)) = \deg \omega(x) + \deg b_I(x) < t + \deg b_I(x) = t + (\deg x^{2^l} - \deg r_{I-1}(x)) \le 3t - t = 2t\)。因此 (5.17) 蕴含 \(r_I(x)\sigma(x) = \omega(x)b_I(x)\)。这，连同 (5.15) 和 (5.16)，表明

\(a_I(x)\sigma(x) = a(x)b_I(x).\) (5.18)

然而，引理 5.4.11(iii) 蕴含 \(a_I(x)\) 和 \(b_I(x)\) 互素，因此由 (5.18) 得 \(a(x) = \lambda(x)a_I(x)\)。将此代入 (5.18) 得到

\(\sigma(x) = \lambda(x)b_I(x).\) (5.19)

将这些代入 (5.14) 得到 \(\lambda(x)a_I(x)x^{2^l} + \lambda(x)b_I(x)S(x) = \omega(x)\)。因此 (5.13) 蕴含

\(\omega(x) = \lambda(x)r_I(x).\) (5.20)

根据引理 5.4.10、(5.19) 和 (5.20)，\(\lambda(x)\) 必须是一个非零常数，从而验证了 Sugiyama 算法的步骤 III。

由于我们只关心 \(\sigma(x)\) 的根，因此只需找出步骤 II 中产生的 \(b_I(x)\) 的根；这将给出所需的错误位置数。

**Example 5.4.12** 使用 Sugiyama 算法和表 5.1，我们从示例 5.4.3 中得到 \(\sigma(x)\) 的一个标量倍数。在该示例中，\(t = 2\)，校验和为 \(S_1 = \alpha^2\)、\(S_2 = \alpha^4\)、\(S_3 = \alpha^{11}\) 和 \(S_4 = \alpha^8\)。下表总结了结果。

| i | r_I(x) | h_I(x) | b_I(x) |
|---|---|---|---|
| -1 | x^4 | | 0 |
| 0 | \alpha^8x^3 + \alpha^{11}x^2 + \alpha^4x + \alpha^2 | | 1 |
| 1 | \alpha x^2 + \alpha^4x + \alpha^{12} | \alpha^7x + \alpha^{10} | \alpha^7x + \alpha^{10} |
| 2 | \alpha^2 | \alpha^7x | \alpha^{14}x^2 + \alpha^2x + 1 |

满足 \(\deg r_I(x) < t = 2\) 的第一个索引 \(I\) 是 \(I = 2\)。因此 \(\sigma(x)\) 是 \(b_2(x) = \alpha^{14}x^2 + \alpha^2x + 1\) 的倍数；事实上，根据示例 5.4.3，\(b_2(x) = \sigma(x)\)。

**Example 5.4.13** 使用 Sugiyama 算法，我们考察示例 5.4.4，其中 \(t = 2\)，\(S_1 = S_2 = S_4 = 0\)，且 \(S_5 = \alpha^{10}\)。下表总结了计算结果。

| i | r_i(x) | h_i(x) | b_i(x) |
|---|---|---|---|
| -1 | x^4 | | 0 |
| 0 | \alpha^{10} x^2 | | 1 |
| 1 | 0 | \alpha^5 x^2 | \alpha^5 x^2 |

满足 \(\deg r_I(x) < t = 2\) 的第一个索引 \(I\) 是 \(I = 1\)。但在此例中，\(b_1(x) = \alpha^5 x^2\)，其根为 0，表明发生了超过两个错误，这与示例 5.4.4 一致。还要注意，\(r_1(x) = 0\) 由 (5.20) 蕴含 \(\omega(x) = 0\)，这显然是不可能的，因为根据引理 5.4.10，\(\sigma(x)\) 和 \(\omega(x)\) 应该是互素的。

**Example 5.4.14** 使用 Sugiyama 算法，我们从示例 5.4.5 中得到 \(\sigma(x)\) 的一个标量倍数。这里 \(t = 3\)，且 \(S_1 = \alpha^{14}\)、\(S_2 = \alpha^{13}\)、\(S_3 = \alpha^{14}\)、\(S_4 = \alpha^{11}\)、\(S_5 = 1\) 和 \(S_6 = \alpha^{13}\)。下表总结了结果。

| i | r_i(x) | h_i(x) | b_i(x) |
|---|---|---|---|
| -1 | x^5 | | 0 |
| 0 | \alpha^{13} x^5 + x^4 + \alpha^{11} x^3 + \alpha^4 x^2 + \alpha^{13} x + \alpha^4 | | 1 |
| 1 | \alpha^{11} x^4 + \alpha^4 x^3 + \alpha^{14} x^2 + \alpha x + \alpha^3 | \alpha^2 x + \alpha^4 | \alpha^2 x + \alpha^4 |
| 2 | \alpha^{12} | \alpha^2 x + \alpha^2 | \alpha^4 x^2 + \alpha^{12} x + \alpha^{13} |

满足 \(\deg r_I(x) < t = 3\) 的第一个索引 \(I\) 是 \(I = 2\)。因此 \(\sigma(x)\) 是 \(b_2(x) = \alpha^4 x^2 + \alpha^{12} x + \alpha^{13}\) 的倍数。根据示例 5.4.5，\(\sigma(x) = \alpha^2 b_2(x)\)。

- Exercise 305 验证示例 5.4.12、5.4.13 和 5.4.14 中的计算。

- Exercise 306 使用 Sugiyama 算法，找出示例 5.4.6 中错误定位多项式的一个标量倍数。

- Exercise 307 使用 Sugiyama 算法，找出练习 299 中错误定位多项式的标量倍数。

- Exercise 308 使用 Sugiyama 算法，找出练习 300 中错误定位多项式的标量倍数。

- Exercise 309 使用 Sugiyama 算法，找出练习 301 中错误定位多项式的标量倍数。

我们指出，Sugiyama 算法适用于 \(f(x)\) 和 \(s(x)\) 的其他选择，只需对算法在步骤 II 中停止的条件做适当修改。这种修改适用于 Goppa 码的解码；参见 [232]。

值得注意的是，Peterson–Gorenstein–Zierler 算法、Berlekamp–Massey 算法或 Sugiyama 算法可用于解码任何循环码，直至 BCH 界。设 \(C\) 为定义集为 \(T\) 的循环码，并假设 \(T\) 包含 \(\delta\) 个连续元素 \(\{b, b+1, \dots, b+\delta-2\}\)。设 \(B\) 为定义集为 \(C_b \cup C_{b+1} \cup \dots \cup C_{b+\delta-2}\) 的 BCH 码，它是 \(T\) 的子集。根据练习 239，\(C \subseteq B\)。设 \(t = \lfloor (\delta-1)/2 \rfloor\)。假设发送了一个代码字 \(c(x) \in \mathcal{C}\)，接收到 \(y(x)\)，其中发生了 \(t\) 个或更少的错误。那么 \(c(x) \in \mathcal{B}\)，且任何应用于 \(\mathcal{B}\) 的解码算法都将纠正 \(y(x)\) 并产生 \(c(x)\)。因此，这些算法将纠正任何循环码中的接收字，前提是如果发生错误，\(2t + 1\) 不超过该码的 BCH 界。当然，这个错误数可能少于 \(\mathcal{C}\) 实际能够纠正的错误数。

## 5.4.4 Sudan–Guruswami 解码算法

在 1997 年的一篇论文中，Madhu Sudan [323] 开发了一种用于解码 \([n, k, d]\) Reed–Solomon 码的过程，该过程能够纠正某些 \(e\) 个错误，其中 \(e > (d - 1)/2\)。Guruswami 和 Sudan [113] 扩展了该方法，以消除原始 Sudan 算法中的某些限制。为了能够纠正 \(e\) 个错误（其中 \(e > (d - 1)/2\)），该算法生成一个所有可能代码字的列表，这些代码字与任何接收向量的 Hamming 距离在 \(e\) 以内；这样的算法称为 *list-decoding algorithm*。Sudan–Guruswami 算法适用于广义 Reed–Solomon 码以及某些 BCH 码和代数几何码。在本节中，我们针对广义 Reed–Solomon 码介绍该算法，并将感兴趣的读者引向 [113] 以了解其他码。Sudan–Guruswami 算法本身已由 Kötter 和 Vardy [179] 推广，以应用于软判决解码。

为准备该算法，我们需要一些涉及两个变量多项式的初步记号。假设 \(x\) 和 \(y\) 是独立不定式，且 \(p(x, y) = \sum \sum p_{i,j} x^i y^j\) 是 \(\mathbb{F}_q[x, y]\) 中的一个多项式，即两个变量 \(x\) 和 \(y\) 的所有多项式组成的环。设 \(w_x\) 和 \(w_y\) 为非负实数。\(p(x, y)\) 的 \((w_x, w_y)\)-加权次数定义为

\(\max\{w_x i + w_y j \mid p_{i,j} \neq 0\}.\)

注意，\(p(x, y)\) 的 \((1, 1)\)-加权次数仅仅是 \(p(x, y)\) 的次数。对于正整数 \(s\) 和 \(\delta\)，设 \(N_s(\delta)\) 表示 \((1, s)\)-加权次数小于或等于 \(s\) 的单项式 \(x^i y^j\) 的数量。我们说点 \((\alpha, \beta) \in \mathbb{F}_q^2\) *位于* 或 *是* \(p(x, y)\) 的一个根，前提是 \(p(\alpha, \beta) = 0\)。我们将需要这个根的重数。为了说明重数的定义，回顾一下，如果 \(f(x) \in \mathbb{F}_q[x]\) 且 \(\alpha\) 是 \(f(x)\) 的一个根，那么它作为 \(f(x)\) 根的重数是数 \(m\)，其中 \(f(x) = (x - \alpha)^m g(x)\) 对于某些 \(g(x) \in \mathbb{F}_q[x]\) 且 \(g(\alpha) \neq 0\)。在处理两个变量时，我们不能直接推广此记号。然而，请注意 \(f(x + \alpha) = x^m h(x)\)，其中 \(h(x) = g(x + \alpha)\)；此外 \(h(0) \neq 0\)。特别是，\(f(x + \alpha)\) 包含一个次数为 \(m\) 的单项式，但不包含更小次数的单项式。这个概念可以推广。多项式 \(p(x, y)\) 的根 \((\alpha, \beta)\) 具有重数 \(m\)，前提是移位多项式 \(p(x + \alpha, y + \beta)\) 包含一个次数为 \(m\) 的单项式，但不包含较低次数的单项式。

**Exercise 310** 设 \(p(x, y) = 1 + x + y - x^2 - y^2 - 2x^2y + xy^2 - y^3 + x^4 - 2x^3y - x^2y^2 + 2xy^3 \in \mathbb{F}_5[x]\)。证明 \((1, 2) \in \mathbb{F}_5^2\) 是 \(p(x, y)\) 的一个重数为 3 的根。

