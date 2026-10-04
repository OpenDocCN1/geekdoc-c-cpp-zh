

506 应用 R 进行时间序列分析

## 12.3.1 傅里叶级数背景

为了充分理解小波方法，需要对小波分析的扩展——经典傅里叶方法有一定的熟悉程度。关于傅里叶级数的简要回顾，参见附录 12A。

如第 1.5 节和附录 12A 所讨论，傅里叶分析涉及将函数表示为正弦和余弦的线性组合。12A.1 指出，一个在 $[-\pi,\pi]$ 上表现良好的函数 $g$ 可以表示为正交系统 $S_1=\{\cos kx, \sin kx; k=1, 2, ...\}$ 中的 *基函数* 的线性组合，或等价地表示为 $S_2=\{e^{ikx}, k=0, \pm1, ...\}$ 的线性组合。使用 $S_2$ 的优点是基函数实际上只由一个“基本”函数组成，即 $\phi(x)=e^{ix}$，而各个函数是该函数的“积分扩张”，即 $e^{ikx}=\phi(kx)$。随着 $k$ 的增大，函数 $\phi(kx)=\cos(kx)+i\sin(kx)$ 的频率增加；即整数 $k$ 控制基函数 $\phi(kx)$ 中的频率含量。傅里叶分析基于这样一个事实：当某些条件成立时，函数可以写成单个函数 $e^{ix}$ 的扩张的线性组合，参见附录 12A。在小波分析中，起着与傅里叶分析中 $\phi(x)=e^{ix}$ 类似的根本作用。

## 12.3.2 小波分析介绍

假设 $g$ 在实数线上是平方可积的，即 $\int_{-\infty}^{\infty}g(x)^2dx<\infty$。此类函数的集合记为 $L^2(\mathbb{R})$，其中 $\mathbb{R}=(-\infty,\infty)$。我们希望有一组基函数，它们都是单个函数 $\psi(x)$ 的变体，使得 $L^2(\mathbb{R})$ 中的函数 $g$ 可以用这些元素的有限线性组合任意逼近。需要指出的是，$\sin x, \cos x$ 和 $e^{ix}$ 都不是所需基函数的候选，因为它们不在 $L^2(\mathbb{R})$ 中。事实上，$\int_{-\infty}^{\infty}g(x)^2dx<\lim_{|x|\to\infty}|g(x)|=0$ 的一个必要条件是。也就是说，基函数必须随着 $|x|\to\infty$ 衰减到零，因此直观上需要短波或“小波”。在小波分析中，常用 $\psi(2^{-jx})$，其中 $j$ 是整数，且 $j$ 控制基函数 $\psi(2^{-jx})$ 中的阻尼量，类似于 $k$ 控制基函数 $\phi(kx)$ 中的频率行为。用单个快速衰减函数的扩张来逼近定义在整个实数线上的函数 $g$ 直观上是困难的。因此，在小波分析中，我们考虑基函数的扩张和平移，以便估计局部频率行为。也就是说，给定一个函数 $\psi(x)$，我们使用作为基集合的

$\psi_{j,k}(x)=2^{-j}\psi(2^{-jx}x-k),$$ (12.9)

其中 $j$ 和 $k$ 是整数，分别称为 *扩张指数* 和 *平移指数*。函数 $\psi(x)$ 称为母小波，因为它“诞生”了整个基元素集合。

### EXAMPLE 12.1: HAAR WAVELETS

作为小波的第一个例子，我们考虑由

$$\psi(x)=1, \quad 0 \leq x < 1/2\n=-1, \quad 1/2 \leq x < 1\n=0, \quad \text{elsewhere.} \quad (12.10)$$

定义的 Haar 小波。

Figure 12.5 shows the Haar wavelet along with three dilations and translations. If $f_t$, for example, $j=2$ and $k=0$, then $\psi_{2,0}(x)$ is given by $\psi_{2,0}(x)=2^{-1}\psi(2^{-2}x-0)$, that is,

$$\psi_{2,0}(x)=0.5, \quad 0 \leq x < 2\n=-0.5, \quad 2 \leq x < 4\n=0, \quad \text{elsewhere.} \quad (12.11)$$

![](img/41dcbfb9af56fa48895afde322197b0b_523_0.png)

**FIGURE 12.5**
(a) Haar mother wavelet and various dilations and translations, (b) $j=2, k=0$, (c) $j=-1, k=1$, (d) $j=-2, k=8$.

508 应用 R 进行时间序列分析

which is shown in Figure 12.5b. Figure 12.5c and d shows $\Psi_{-1,1}$ and $\Psi_{-2,8}$
respectively. Note that

$$\int \psi(x)dx=0, \quad (12.12)$$

and consequently for each $j$ and $k$

$$\Psi_{j,k}(x)dx=0. \quad (12.13)$$

Haar 小波具有紧支撑，因为它们在有界区间 $[2k, 2(k+1)]$ 外等于零。具体来说，

$$\Psi_{j,k}(x)=2^{j/2}, \quad 2'k \le x < 2'(k+0.5)\n=-2^{-j/2}, \quad 2'(k+0.5) \le x < 2'(k+1)\n=0. \quad (12.14)$$

由方程 12.14 可知，$\Psi_{jb}$ 的支撑长度为 2(k+1)-2k=2。这 translates and of a wavelet are designed to
describes localized frequency behavior. Then, the wavelet $\Psi_{jb}$ describes
localized behavior related to pseud or decay of duration
(or "period") about 2 for $x$ in the neighborhood of $2(k+0.5)$. Haar 小波 $\Psi_{jk}$ 的支撑也称为小波的 *尺度*。一般来说，小波的尺度是其宽度的度量。

*关于频率的说明：* 需要注意的是，由于我们没有使用正弦和余弦作为基元素，频率的严格解释不再有效。由于尺度是小波“周期”的度量，我们使用“1/尺度”作为“频率”的度量。。

有许多类型的小波，Haar 是 true for simple-
properties. In Equations 12.12 and 12.13 are true for all wavelets. While the
Haar wavelet has compact support, this is not a requirement. When
wavelets have the property that $|Psi_j(x)| \to 0$ as $|x| \to \infty$. Figure 12.6 shows
several wavelets. The Daubert(4), Daubert(8), and Daubert(12) mother wavelets
in 12.6a, c, and e are from the Dafamily of wavelets suggested by
Daubechies (1988). The Daubert(2) wavelet, that is, the second-order Daubert,
b broader. The higher the order, the smoother the wavelet, and the Daubert(4) wavelet is sometimes called the shark-
fin for obvious reasons. Figure 12.6g shows the Symlet(8) wavelet.
This wavelet is widely used and is a member of the Symlet (sometimes least asymmetric) family of wavelets also proposed by Daubechies (1988). The
Symlet and Dafamily are both orthogonal families. That is, for exam-
ple, the Symlet(8) wavelet and its collection of dilates and translates given in

Wavelets 509

![](img/41dcbfb9af56fa48895afde322197b0b_525_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_525_1.png)

![](img/41dcbfb9af56fa48895afde322197b0b_525_2.png)

![](img/41dcbfb9af56fa48895afde322197b0b_525_3.png)

**Figure 12.6**nFour mother wavelets and their corresponding father wavelets. (a) D4 mother wavelet. (b) D4 father wavelet. (c) D8 mother wavelet. (d) D8 father wavelet. (e) D12 mother wavelet. (f) D12 father wavelet. (g) S8 mother wavelet. (h) S8 father wavelet.

Equation 12.9 is an orthogonal collection of functions that form a base for $g \in L^2(\mathbb{R})$ in the sense of Theorem 12.1 that follows. Comparing Figure 12.6a, c, and e we see that as k increases, the support of the Daubelet(k) wavelet (interval on which the wavelet takes on nonzero values) gets longer and the wavelet becomes smoother.

**Using R:** The wavelet plots as those in Figure 12.6 can be obtained using the draw function in the wavethresh CRAN package. See Appendix 12B.

NOTE: The discretized versions of Daubelet(2k) and Symlet(2k) wavelets on 2k values and some authors refer to these as Daubelet(2k) (and Symlet(2k)) wavelets, as we have here. The wavslim package we often use in the following nomenclature. However, others refer to them as Daubelet(k) and Symlet(k) wavelets. That is, the Daubelet(4) (shark-fin) wavelet in Figure 12.6a is sometimes referred to as a Daubelet(2) wavelet. Check the definition and be careful!

## 12.3.3 Fundamental Wavelet Approximation Result

与傅里叶级数逼近类似的基本小波逼近结果在下面的定理 12.1 中给出。

## Theorem 12.1

Let $\{\psi_{j,k}\}$ be an orthogonal wavelet basis, and let $g \in L^2(\mathbb{R})$. Then,

$g(x) = \sum_{j=-\infty}^{\infty} \sum_{k=-\infty}^{\infty} d_{j,k}\psi_{j,k}(x), \quad 12.15$

where the equality is in the mean-square sense and the wavelet transform coefficients, $d_{j,k}$, are given by

$d_{j,k} = \frac{1}{\|\psi||^2} \int g(t)\psi_{j,k}(t)dt, \quad 12.16$

where $|\psi||^2$ denotes $\int_{-\infty}^{\infty}|\psi(x)|^2dx$.

Proof: See Daubechies (1992) and Ogden (1997). Appendix 12A gives a formal derivation to show that if Equation 12.15 holds, then $d_{j,k}$ is given by Equation 12.16.

Equation 12.15 is analogous to the Fourier series representation in Equation 12A.3. Also, the coefficients, $d_{j,k}$ in Equation 12.1 correspond to the Fourier series coefficients, $\alpha_k$ in Equation 12A.4. In Fourier analysis large values of $\alpha_k^2$ are associated with data (in our time series) that have periodic content in the neighborhood of the frequency $f=k$. Similarly large values of $|d_{j,k}|$ in Equation 12.15 are associated with detail behavior of about $2^j$, that is, the "frequency" or "1/scale" is about $2^{-j}$. In Fourier analysis, $\alpha_k$ as defined in Equation 12A.4 are Fourier transforms of $g(x)$, and similarly the coefficients, $d_{j,k}$ defined in Equation 12.16 are referred to as (continuous) wavelet expressions.

The expression in Equation 12.15 is sometimes expressed as

$g(x) = \sum_{j=-\infty}^{\infty} \sum_{k=-\infty}^{\infty} d_{j,k}\psi_{j,k}(x) + \sum_{j=-\infty}^{\infty} \sum_{k=-\infty}^{\infty} d_{j,k}\psi_{j,k}(x),$

which is often written as

