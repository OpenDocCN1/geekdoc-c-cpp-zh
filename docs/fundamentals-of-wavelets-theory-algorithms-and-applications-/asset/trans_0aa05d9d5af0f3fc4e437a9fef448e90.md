

(5.42) \(\hat{N}_1(\omega) = \int_0^1 e^{-j\omega t} dt = \frac{1 - e^{-j\omega}}{j\omega}\)

就我们的目的而言，样条的重要特性在于它们是缩函数。也就是说，存在一个序列 \(\{g_0[m, k]\} \in \mathbb{Z}^2\)，使得

(5.43) \(N_m(t) = \sum_k g_0[m, k] N_m(2t - k)\)

在第6章中，我们将推导 \(g_0[m, k]\) 的表达式。

### 5.5.1 样条的性质

本节讨论了与本书所讨论主题相关的一些重要样条性质，但不给出任何证明。某些性质的证明留作练习。

- 1. 支持集 \(N_m = [0, m]\)，且 \(N_m(0) = N_m(m) = 0\)

- 2. \(N_m(t) \in C^{m-2}\)；\(C^k\) 是 \(k\) 次连续可微函数的空间。

- 3. \(N_m|_{[k-1, k]} \in \pi_{m-1}\)；\(k \in \mathbb{Z}\)，\(\pi_k\) 是次数为 \(k\)（阶为 \(k+1\)）的多项式空间。

- 4. \(\int_{-\infty}^{\infty} N_m(t) dt = 1\)

- 5. \(N'_m(t) = N_{m-1}(t) - N_{m-1}(t - 1)\)

- 6. \(N_m(t)\) 关于中心 \(t^* = m/2\) 对称：

\(N_m\left(\frac{m}{2} + t\right) = N_m\left(\frac{m}{2} - t\right) ; \quad t \in \mathbb{R}\)

(5.44)

- 7. \(N_m(t)\) 表现为低通滤波器 [\(\hat{N}_m(0) = 1\)；参见图 5.7]。

- 8. \(N_m(t)\) 具有 \(m\) 阶逼近阶，即 \(\hat{N}_m(\omega)\) 满足 Strang-Fix 条件

(5.45)

\(\begin{cases} \hat{N}_m(0) = 1, \text{ and} \\ D^j \hat{N}_m(2\pi k) = 0, \quad k \in \mathbb{Z} \setminus \{0\} \quad \text{and} \quad j = 1, ..., m-1, \end{cases}\)

其中 \(D^j\) 表示 \(j\) 阶导数。因此，\(N_m(t)\) 局部再现所有 \(m\) 阶多项式 [8, pp. 114–121]。

- 9. \(N_m(t - k) \equiv 1\)；对所有 \(t\) 成立。该性质称为 *一致分割* 性质。

- 10. *全正性*：\(N_m(t) \ge 0\)，对 \(t \in [0, m]\)。得益于 \(B\)-样条的全正性 [6, p. 7] 属性，\(B\)-样条级数的系数遵循数据的形状。例如，若 \(g(t) = \sum_j \alpha_j N_m(t - j)\)，则

\(\alpha_j \ge 0 \quad \forall j \Rightarrow g(t) \ge 0\)

\(\alpha_j \uparrow (\text{increasing}) \Rightarrow g(t) \uparrow, \text{and}\)

\(\alpha_j (\text{convex}) \Rightarrow g(t) \text{ convex.}\)

此外，\(g(t)\) 的符号变化次数不超过系数序列 \(\{\alpha_j\}\) 的符号变化次数。后一属性可用于识别信号的零交叉点。

- 11. 随阶数 \(m\) 增加，\(N_m(t)\) 趋近于高斯函数（\(\Delta N_m / \Delta_n \to 0.5\)）。例如，对于三次样条（\(m=4\)），时频窗乘积的均方根为 0.501。

## 5.6 将函数映射到 MRA 空间

如第 5.2 节所述，在对信号 \(x(t)\) 进行分解之前，必须将其映射到某个适当尺度 \(M\) 的 MRA 子空间 \(A_M\) 中，即，

(5.46) \(x(t) \mapsto x_M(t) = \sum_k a_{k,M} \phi(2^M t - k).\)

一旦我们知道 \(\{a_{k,M}\}\)，就可以使用快速算法计算 \(s < M\) 时的 \(\{a_{k,s}\}\)。快速算法将在后续章节中讨论。这里我们关注系数 \(\{a_{k,M}\}\) 的求解。

如果在每个 \(t\) 处都已知 \(x(t)\)，则可以通过信号的正交投影（\(L^2\) 投影）得到 \(\{a_{k,M}\}\)：

$$a_{k,M} = 2^M \int_{-\infty}^{\infty} x(t) \bar{\phi}(2^M t - k) dt.$$

然而，在实际中，信号 \(x(t)\) 仅在某些离散点处已知。给定的时间步长决定了函数可以被映射到的尺度 \(M\)。对于如 (5.46) 这样的表示，我们希望它满足两个重要条件：（1）插值性和（2）多项式再现性。所谓 *插值表示*，是指级数至少在给定函数的点处应是精确的，即 \(x(k/2^M) = x_M(k/2^M)\)。如前所述，*多项式再现性* 是指，如果基函数 \(\phi(t)\) 具有 \(m\) 阶逼近阶，则该表示对于 \(m\) 阶多项式在每个点处都是精确的。换句话说，对于 \(x(t) \in \pi_{m-1}\)，有 \(x(t) \equiv x_M(t)\)。基数 \(B\)-样条具有 \(m\) 阶逼近阶。此外，由于它们是局部基，表示 (5.46) 也是局部的。所谓 *局部*，是指为了求得某个 \(k\) 的系数 \(a_{kM}\)，我们不需要所有函数值；仅需少数几个值，由样条的支撑集决定即可。当 \(\phi(t) = N_2(t)\) 和 \(\phi(t) = N_4(t)\) 时，系数如下推导。

### 5.6.1 一次样条（m = 2）

假设函数 \(x(t)\) 在 \(t = k 2^{-M}, k \in \mathbb{Z}\) 处已知。为了求得表示

$$x(t) \mapsto x_M(t) = \sum_k a_{k,M} N_2(2^M t - k).$$

的样条系数 \(\{a_{k,M}\}\)，我们应用插值条件，即

(5.49)
\( x \left( \frac{\ell}{2^M} \right) = x_M \left( \frac{\ell}{2^M} \right). \)

使用方程 (5.49)，并结合以下事实

(5.50)
\( N_2(1) = 1, \text{ and } N_2(k) = 0, k \in \mathbb{Z} \setminus \{0\}, \)

可得

(5.51)
\( a_{k,M} = x \left( \frac{k+1}{2^M} \right). \)

表示 (5.48) 保留所有次数不超过 1 的多项式。

### 5.6.2 三次样条（\(m = 4\)）

在此情形下

(5.52)
\( x(t) \mapsto x_M(t) = \sum_k a_{k,M} N_4(2^M t - k) \)

其中 [4, p. 117]

\( a_{k,M} = \sum_{n=k-2}^{k+6} v_{k+2-2n} x \left( \frac{n}{2^{M-1}} \right), \)

和

| \(n\) | \(V_n\) |
|-------|---------|
| 0 | \(\frac{29}{24}\) |
| \(\pm 1\) | \(\frac{7}{12}\) |
| \(\pm 2\) | \(-\frac{1}{8}\) |
| \(\pm 3\) | \(-\frac{1}{12}\) |
| \(\pm 4\) | \(\frac{1}{48}\) |
| 其他 | 0 |

表示 (5.52) 保留所有次数不超过 3 的多项式。

## 5.7 习题

- 1. 对于给定的 \(j \in \mathbb{Z}\)，任何给定函数 \(f(t) \in L^2(-\infty, \infty)\) 到“帽函数空间”

\(V_j = \left\{ \sum_{k=-\infty}^{\infty} c_k N_2(2^j t - k) : \{c_k\}_{k \in Z} \in \ell_2 \right\}\)

的投影 \(P_{2j}f(t)\) 可由插值条件 \(P_{2j}f(k/2^j) = f(k/2^j)\) 对所有 \(k \in Z\) 确定。若 \(P_{2j}f\) 写为

\(P_{2j}f(t) = \sum_{n=-\infty}^{\infty} a_n N_2(2^j t - n).\)

求系数 \(\{a_n\}\) 的公式。

- 2. 对于 Haar 小波

\(\psi_H(t) := \begin{cases} 1 & \text{for } t \in [0, \frac{1}{2}) \\ -1 & \text{for } t \in [\frac{1}{2}, 1) \\ 0 & \text{otherwise.} \end{cases}\)

定义

\(\psi_{H, k, s}(t) = 2^{\frac{s}{2}} \psi_H(2^s t - k), \quad k, s \in \mathbb{Z}\)

证明正交关系

\(\int_{-\infty}^{\infty} \psi_{H, k, s}(t) \psi_{H, m, p}(t) dt = \delta_{m,k} \delta_{s,p} \quad m, k, p, s \in \mathbb{Z}.\)

由于这些关系，我们称集合 \(\{\psi_{H, k, s}\}_{k, s \in Z}\) 在 \(L^2(-\infty, \infty)\) 中构成一组正交归一族。

- 3. 证明高斯函数 \(\phi(t) = e^{-t^2}\) 不能作为多分辨率分析的缩函数。（提示：假设 \(e^{-t^2}\) 可以写成 \(e^{-t^2} = \sum_{k=-\infty}^{\infty} a_k e^{-(2t-k)^2}\) 的形式，其中序列 \(\{a_k\}_{k \in \mathbb{Z}} \in l_2\)，若 \(e^{-t^2} \in V_0 \subset V_1\) 则此假设必须成立。接着，对等式两边进行傅里叶变换并比较结果，证明这会导致矛盾。）

- 4. 证明 \(m\) 阶 \(B\)-样条 \(N_m(t)\) 及其整数平移构成一致分割：

\(\sum_{k=-\infty}^{\infty} N_m(t-k) = 1 \quad \text{for all } t \in \mathbb{R}.\)

（提示：使用泊松求和公式。）

- 5. 证明 \(N_m(t)\) 的以下对称性质：

\(N_m\left(\frac{m}{2} + t\right) = N_m\left(\frac{m}{2} - t\right), \quad t \in \mathbb{R}.\)

- 6. 利用习题 5 证明

\(\int_{-\infty}^{\infty} N_m(t+k) N_m(t) dt = N_{2m}(m+k)\)

对任意 \(k \in \mathbb{Z}\) 成立。

- 7. 证明帽函数

$$N_2(t) = \begin{cases} t & t \in [0, 1] \\ 2-t & t \in [1, 2] \\ 0, & \text{otherwise} \end{cases}$$
(5.53)

与函数 \(N_1(t)\) 通过卷积相关：\(N_2(t) = N_1(t) * N_1(t)\)。求下列函数的定义方程（多项式表达式）：

\(N_3(t) := N_2(t) * N_1(t)\)

\(N_4(t) := N_3(t) * N_1(t)\).

## 5.8 计算机程序

### 5.8.1 B-样条

```
%
% PROGRAM Bspline.m
%
% Computes uniform Bsplines
function y = Bspline(m,x)
y = 0;
% Characteristic function
if m == 1
if x >= 0.0 & x < 1.0
y = 1.0;
else
```

