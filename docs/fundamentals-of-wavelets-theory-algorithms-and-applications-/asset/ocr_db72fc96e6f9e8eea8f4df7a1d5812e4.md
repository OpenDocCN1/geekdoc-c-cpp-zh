0 < R_1 \le \sum_k \left| \hat{\phi}(\omega + 2\pi k) \right|^2 \le R_2 < \infty, \n(2.33)

The derivation of (2.33) is left as an exercise. A hat over a function represents its Fourier transform, a topic that will be discussed in the next chapter.

If $R_1 = R_2 = 1$, the basis is orthonormal. The Shannon basis is an example of a Riesz basis that is orthonormal, since the spectrum of the Shannon function is one in the interval \([-\pi, \pi]\). Hence

\sum_k \left| \phi_{SH}(\omega + 2\pi k) \right|^2 \equiv 1. \n(2.34)

If the basis functions \(\{\phi(t - k) : k \in \mathbb{Z}\}\) are not orthonormal, then we can obtain an orthonormal basis set \(\{\phi^\perp(t - k) : k \in \mathbb{Z}\}\) by the relation

\(\widehat{\phi^\perp}(\omega) = \frac{\hat{\phi}(\omega)}{\left\{ \sum_k \left| \hat{\phi}(\omega + 2\pi k) \right|^2 \right\}^{\frac{1}{2}}}.\) \n(2.35)

The Riesz basis is also called a stable basis in the sense that if

g_1(t) = \sum_j a_j^{(1)} \phi_j(t)