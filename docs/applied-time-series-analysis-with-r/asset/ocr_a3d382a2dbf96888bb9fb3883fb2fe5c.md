464

for lags k=0, ..., 25. The sample autocorrelations are similar to those in Figure 11.3(d) for a realization from a fractional model with $d=0.4$. We will return to this data set in Equation 11.9 for purposes of estimating the parameters.

NOTE: It should be noted that there is "Nile" data set that is also used to illustrate long-memory behavior. This data set consists measurements of the annual minimal water levels of the River Nile for the years 622-1281, measured at the Roda gauge near Cairo (Tousson, 1925 and see also Beran, 1994, p. 366–385) and is included in tswge under the name nile.min. See Problem 11.6.

# 11.3 Gegenbauer and GARMA Processes

Even though the FARMA models have been widely studied and have shown to be useful long-memory models, it be that the fractional difference $(1-B)^d$ can only model "first-order" long-memory behavior. For example, according to Theorem 11.1(3) the peak in the spectrum associated with $(1-B)^d$ will always be at $f=0$. Also the autocorrelations like $ho(k) \approx k^{2d-1}$ as $k \to \infty$ are noncyclic in nature. The important point is that fractional and FARMA models, as defined in Section 11.2, cannot model cyclic long-memory behavior associated with a spectrum that is unbounded for $f \in (0,0.5)$ or for which the autocorrelation decays like $ho_k \approx k^\alpha \cos(2\pi f)$ as $k \to \infty$ where $0 < \alpha < 1$.

The restriction to long-memory behavior associated with system frequency $f=0$ is analog, in the setting of AR(p) models, to be restricted to first-order AR models with $\phi_1 > 0$. Recall that in Section 3.2 it was shown that cyclic behavior associated with $f=(0,0.5)$ in AR(p) models is associated with irreducible second-order factors of $\phi(z)$. In this section, we discuss a second-order extension of the fractional process in Equation 11.5 which is based on the second-order factor $(1-2uB+B^2)^l$ for $|u| \le 1$. In order to understand properties associated with such factors, we first consider the Gegenbauer polynomials.

# 11.3.1 Gegenbauer Polynomials

Gegenbauer polynomials are the classical orthogonal polynomials of applied mathematics and physics. The Gegenbauer polynomial is defined by

```
$C_n^{(\lambda)}(u) = \sum_{k=0}^{[n/2]} \frac{(-1)^k (\lambda)_{n-k}(2u)^{n-2k}}{k!(n-2k)!} \quad (11.9)$
```