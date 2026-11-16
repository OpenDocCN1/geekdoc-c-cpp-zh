
TABLE 6.2: Two-Scale Sequence for First-Order Meyer Scaling Function \(\phi_{M;1}\)

| n | g0[n] = g0[-n] | n | g0[n] = g0[-n] | n | g0[n] = g0[-n] |
|---|---|---|---|---|---|
| 0 | 1.063513307325022 | 13 | 0.0018225696961070 | 26 | 0.0000781583234904 |
| 1 | 0.6237929148520031 | 14 | -0.0001225788430400 | 27 | -0.0000281868403039 |
| 2 | -0.0954391217681172 | 15 | -0.0019003177368828 | 28 | -0.0000686017777485 |
| 3 | -0.1762971983704155 | 16 | -0.0000631513505005 | 29 | 0.00003520515347881 |
| 4 | 0.0484777578307502 | 17 | 0.0018514320187282 | 30 | -0.0000059176067635 |
| 5 | 0.0751184831722090 | 18 | 0.0004730929715153 | 31 | -0.0000243116067058 |
| 6 | -0.0099344443938033 | 19 | -0.0010395429751381 | 32 | 0.0000143515571684 |
| 7 | -0.0311015336438103 | 20 | 0.0007208498373768 | 33 | 0.0000150739706291 |
| 8 | 0.0197659340813598 | 21 | 0.0006265174104084 | 34 | -0.0000171599560112 |
| 9 | 0.0110966323385240 | 22 | -0.0005163028169833 | 35 | -0.00000530482980227 |
| 10 | -0.0089152072379117 | 23 | -0.0002172396357580 | 36 | 0.00000628695514764 |
| 11 | -0.0052590831208475 | 24 | 0.0001468858466855 | 37 | 0.00004435267271494 |
| 12 | 0.0025960713118583 | 25 | 0.0001627978141523 | 38 | 0.0000053188445527 |

### 6.4.3 Battle-Lemarié Scaling Function

Battle-Lemarié [5, 6] scaling functions are constructed by orthonormalizing the \(m\)th order cardinal \(B\)-spline \(N_m(t)\) for \(m \ge 2\). As pointed out before, the set of basis functions \(\{N_m(t-k): k \in \mathbb{Z}\}\) is not orthogonal for \(m \ge 2\). The corresponding orthonormal scaling function \(N_m^\perp(t)\) can be obtained as

\(\hat{N}_m^\perp(\omega) = \frac{\hat{N}_m(\omega)}{[E_{N_m}(e^{-j\omega})]^{1/2}}.\)

**(6.53)**

The Battle-Lemarié (B-L) scaling function \(\phi_{BL,m}(t)\) is, then,

\(\phi_{BL,m}(t) = N_m^\perp(t),\)

and the coefficients {g0[k]} can be found from

(6.54)
\(\frac{1}{2} \sum_k g_0[k] z^k = G_0(e^{-j\omega/2}) = \frac{\hat{N}'_m(\omega)}{\hat{N}_m(\omega/2)}\)

where \(z = e^{-j\omega/2}\). By combining (6.53) and (6.54), we have

(6.55)
\(G_0(z) = \left( \frac{1+z}{2} \right)^m \left[ \frac{\sum_{k=-m+1}^{m-1} N_{2m}(m+k) z^k}{\sum_{k=-m+1}^{m-1} N_{2m}(m+k) z^{2k}} \right]^{\frac{1}{2}}\)

As an example consider the linear B-L scaling function for which \(m = 2\). For this case we have

(6.56)
\(\frac{1}{2} \sum_k g_0[k] z^k = G_0(z) = \frac{(1+z)^2}{4} \times \frac{z^2 + 4z + 1}{z^4 + 4z^2 + 1}\)

The coefficients {g0[k]} can be found by expanding the expression on the right-hand side as a polynomial in z and then comparing the coefficients of the like powers of z. These coefficients can also be found by computing the Fourier coefficients of the right-hand side expression. Observe that G0(1) = 1 is satisfied, thus giving the sum of all {g0[k]} to be 2. In Tables (6.3) and (6.4) we provide the coefficients of the linear and cubic B-L scaling functions. The linear and cubic Battle-Lemarié scaling functions and corresponding wavelets are shown in Figure 6.8.

TABLE 6.3: Two-scale Sequence for Linear Battle-Lemarié Scaling Function \(\phi_{BL;2}\)

| n | \(g_l[n] = g_l[2-n]\) | n | \(g_l[n] = g_l[2-n]\) | n | \(g_l[n] = g_l[2-n]\) |
|---|---|---|---|---|---|
| 1 | 1.1536266304457929 | 14 | -0.0000024422257478 | 27 | -0.0000000053986543 |
| 2 | 0.5618629285876487 | 15 | -0.0000195427343909 | 28 | -0.0000000028565276 |
| 3 | -0.0977235484799832 | 16 | -0.0000105279065482 | 29 | 0.0000000013958989 |
| 4 | -0.0734618133554703 | 17 | 0.0000049211790530 | 30 | 0.0000000007374693 |
| 5 | 0.0240068439163234 | 18 | 0.0000026387010627 | 31 | -0.0000000003617852 |
| 6 | 0.0144189917255644 | 19 | -0.0000124777019294 | 32 | -0.0000000001904191 |
| 7 | -0.0041976153812384 | 20 | -0.0000004709572222 | 33 | 0.0000000000939609 |
| 8 | -0.0031140290154640 | 21 | 0.0000031807558564 | 34 | 0.0000000000495170 |
| 9 | 0.0013058436261069 | 22 | 0.0000001693792269 | 35 | -0.0000000000244478 |
| 10 | 0.0007255625100098 | 23 | -0.0000008145195990 | 36 | -0.0000000000128703 |
| 11 | -0.0003172028555467 | 24 | -0.0000000432545262 | 37 | 0.0000000000063579 |
| 12 | -0.0001725806359701 | 25 | 0.0000004286363757 | 38 | 0.0000000000033584 |
| 13 | 0.0000782586448683 | 26 | 0.0000000110972572 | 39 | -0.0000000000016567 |

TABLE 6.4: Two-Scale Sequence for Cubic Battle-Lemarié Scaling Function \(\phi_{BL;4}\)

| n | \(g_l[n] = g_l[4-n]\) | n | \(g_l[n] = g_l[4-n]\) | n | \(g_l[n] = g_l[4-n]\) |
|---|---|---|---|---|---|
| 2 | 1.084275125686560 | 15 | 0.0026617387556783 | 28 | -0.0000025171646500 |
| 3 | 0.6136592734426418 | 16 | -0.0015669238233188 | 29 | -0.0000022283943141 |
| 4 | -0.070995959848591 | 17 | -0.0013112570210398 | 30 | 0.00001460735867894 |
| 5 | -0.1556158437675466 | 18 | 0.0007918699951128 | 31 | 0.0000114467590896 |
| 6 | 0.0453692402954247 | 19 | 0.0006535296221413 | 32 | -0.0000075774407788 |
| 7 | 0.0594936331541212 | 20 | -0.0004039935254263 | 33 | -0.0000059109049366 |
| 8 | -0.0242907783203567 | 21 | -0.0003258860945923 | 34 | 0.0000039378865616 |
| 9 | -0.0295036005200569 | 22 | 0.0001966348024232 | 35 | 0.0000030357806066 |
| 10 | 0.0122825617178522 | 23 | 0.0001663505502899 | 36 | -0.0000020497919302 |
| 11 | 0.0115986402962103 | 24 | -0.0001066037892378 | 37 | -0.0000015870262674 |
| 12 | -0.0061572588095633 | 25 | -0.0000846821755363 | 38 | 0.0000010685382577 |
| 13 | -0.0054905784658009 | 26 | 0.0000546341264354 | 39 | 0.0000008247217560 |
| 14 | 0.003024782908629 | 27 | 0.0000434039957782 | 40 | -0.0000005577533664 |

FIGURE 6.8: Battle-Lemarié scaling function, the corresponding wavelet, and their magnitude spectra.

![](img/f73ae67732328dc36596b27ffe8d0152_244_0.png)

### 6.4.4 Daubechies Scaling Function

Battle-Lemarié obtained orthonormal scaling functions by orthonormalizing mth-order cardinal B-splines $N_m(t)$ for $m \ge 2$. However, because of the presence of $\hat{E}_{N_m}(z)$ in the denominator for the orthonormalization process, the sequence $\{g_0[k]\}$ becomes infinitely long.

To obtain orthonormality but preserve the finite degree of the (Laurent) polynomial, Daubechies [7, 8] considered the two-scale symbol for the scaling function $\phi_{D,m}$:

$G_0(z) = \left(\frac{1+z}{2}\right)^m S(z),$ (6.57)

where $S(z) \in \pi_{m-1}$. So our objective is to find $S(z)$. First, observe that since $G_0(1) = 1$, we must have $S(1) = 1$. Furthermore, we also want $S(-1) \neq 0$ because if $S(-1) = 0$, then $z+1$ is a factor of $S(z)$ and hence can be taken out. Now $G_0(z)$ is given by (6.57) must satisfy the orthogonality condition, namely

$|G_0(z)|^2 + |G_0(-z)|^2 = 1, \quad z = e^{-j\omega/2}$ (6.58)
$$\Rightarrow \cos^{2m}(\frac{\omega}{4})|S(z)|^2 + \sin^{2m}(\frac{\omega}{4})|S(-z)|^2 = 1.$$ (6.59)

By defining

$x := \sin^2\left(\frac{\omega}{4}\right), \text{ and }$

$f(x) := |S(z)|^2,$

Equation (6.59) can be rewritten as

$$(1-x)^m f(x) + x^m f(1-x) = 1$$
$$\Rightarrow f(x) = (1-x)^m \{1 - x^m f(1-x)\}$$
$$= \sum_{k=0}^{m-1} \binom{m+k-1}{k} x^k + R_m(x),$$ (6.60)

where the remainder \( R_m(x) \) is

(6.61)
\( R_m(x) := \sum_{k=m}^{\infty} \binom{m+k-1}{k} x^k + (-x)^m f(1-x) \sum_{k=0}^{\infty} \binom{m+k-1}{k} x^k. \)

Since \( f(x) \) is a polynomial of order \( m \), \( R_m(x) \equiv 0 \). Therefore, we have

(6.62)
\( |S(z)|^2 = \sum_{k=0}^{m-1} \binom{m+k-1}{k} \sin^{2k}\left(\frac{\omega}{4}\right), \quad z = e^{-j\omega/2}. \)

The above polynomial can be converted to

(6.63)
\( |S(z)|^2 = \frac{a_0}{2} + \sum_{k=1}^{m-1} a_k \cos\left(\frac{k\omega}{2}\right), \)

where [9]

(6.64)
\( a_k = (-1)^k \sum_{n=0}^{m-k-1} \frac{1}{2^{2(k+n)-1}} \binom{2(k+n)}{n} \binom{m+k+n-1}{k+n}. \)

Our next task is to retrieve \( S(z) \) from \( |S(z)|^2 \). According to Riesz lemma [10], corresponding to a cosine series

(6.65)
\(\hat{f}(\omega) = \frac{a_0}{2} + \sum_{k=1}^N a_k \cos(k\omega)\)

with \(a_0, \cdots, a_N \in \mathbb{R}\) and \(a_N \neq 0\), there exists a polynomial

(6.66)
\(g(z) = \sum_{k=0}^N b_k z^k\)

with \(b_0, \cdots, b_N \in \mathbb{R}\), such that

(6.67)
\(|g(z)|^2 = \hat{f}(\omega), \quad z = e^{-j\omega}.\)

By applying Riesz lemma to (6.63) it easy to verify [9] that \(S(z)\) has the following form

(6.68)
\(S(z) = C \prod_{k=1}^K (z-r_k) \prod_{l=1}^L (z-z_\ell)(z-\overline{z_\ell}), \quad K+2L=m-1,\)

where \(\{r_k\}\) are the nonzero real roots and \(\{z\}\) are the complex roots of \(z^{m-1}|S(z)|^2\) inside a unit circle and \(C\) is a constant such that \(S(1) = 1\). Once we have \(S(z)\), we can substitute this into (6.57) and compare the coefficients of powers of \(z\) to get the sequence \(\{g_k\}\). We will show the steps to get these sequences with an example. Consider \(m = 2\). For this, we have \(a_0 = 4\) and \(a_1 = -1\), which gives
