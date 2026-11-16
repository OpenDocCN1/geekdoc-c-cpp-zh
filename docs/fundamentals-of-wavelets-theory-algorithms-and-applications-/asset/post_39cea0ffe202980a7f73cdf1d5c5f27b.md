
```matlab
y = 0.0;
end
end
% Higher order
a = zeros(1,500);
if m >= 2 & m < 100
for k = 1:m-1
a(k) = 0.0;
x1 = x - k + 1;
if x1 >= 0.0 & x1 < 1.0
a(k) = x1;
end
if x1 >= 1.0 & x1 < 2.0
a(k) = 2 - x1;
end
end
for p=1:m-2
for q=1:m-1-p
a(q) = ((x-q+1) * a(q) + ((p+2)+q-1-x) * a(q+1)) / (p+1);
end
end
y = a(1);
end
```

## 5.9 REFERENCES

1. Y. Meyer. *Wavelets: Algorithms and Applications*. Philadelphia: SIAM, 1993.

2. S. Mallat. “A Theory of Multiresolution Signal Decomposition: The Wavelet Representation.” *IEEE Trans. Pattern Anal. Machine Intell.* 11 (1989), 674–693.

3. S. Mallat. “Multiresolution Representation and Wavelets.” Ph.D. thesis, University of Pennsylvania, Philadelphia, 1988.

4. C. K. Chui. *An Introduction to Wavelet*. Boston: Academic Press, 1992.

5. I. J. Schoenberg. *Cardinal Spline Interpolation*. CBMS Series 12. Philadelphia: SIAM, 1973.

6. L. L. Schumaker. *Spline Functions: Basic Theory*. New York: Wiley-Interscience, 1981.

7. C. de Boor. *A Practical Guide to Splines*. New York: Springer-Verlag, 1978.

8. C. K. Chui. *Multivariate Splines*. CBMS-NSF Series in Applied Maths 54. Philadelphia: SIAM, 1988.

## CHAPTER SIX

## Construction of Wavelets

In this chapter we are concerned with the construction of orthonormal, semiorthogonal, and biorthogonal wavelets. The construction problem is tantamount to finding suitable two-scale and decomposition sequences as introduced in Chapter 5. It turns out that these coefficients for orthonormal wavelets can be easily derived from those of semiorthogonal wavelets. Therefore, we first discuss the semiorthogonal wavelet followed by orthonormal and biorthogonal wavelets.

Recall that for the semiorthogonal wavelet, both \(\phi(t)\) and \(\tilde{\phi}(t)\) are in \(A_0\), and \(\psi(t)\) and \(\tilde{\psi}(t)\) are in \(W_0\). Consequently, we can write \(\phi(t)\) in terms of \(\tilde{\phi}(t)\); similarly for \(\psi(t)\). These relations as given by (5.21) and (5.22) are reproduced here.

```
\(\hat{\tilde{\phi}}(\omega) = \frac{\hat{\phi}(\omega)}{E_\phi(e^{j\omega})}, \text{ and}\)
(6.1)

\(\hat{\tilde{\psi}}(\omega) = \frac{\hat{\psi}(\omega)}{E_\psi(e^{j\omega})},\)
(6.2)
```

with the Euler-Frobenius-Laurent (E-F-L) polynomial \(E_j(e^{j\omega})\) given by

\( E_f(e^{j\omega}) := \sum_{k=-\infty}^{\infty} \left| \hat{f}(\omega + 2\pi k) \right|^2 = \sum_{k=-\infty}^{\infty} A_f(e^{j\omega k}). \) (6.3)

We will, therefore, concentrate on the construction of \(\phi\) and \(\psi\) only.

As the first step toward constructing wavelets, we express \(\{h_0[k]\}\), \(\{h_1[k]\}\) and \(\{g_1[k]\}\) in terms of \(\{g_0[k]\}\) so that only \(\{g_0[k]\}\) and hence the scaling functions need to be constructed. In semiorthogonal cases, all these sequences have different lengths, in general. Later we will show that for o.n cases, all of these sequences have the same length and that there is a very simple relation among them which can be easily derived as a special case of the relationship for semiorthogonal cases. The construction of a semiorthogonal wavelet is followed by the construction of several popular orthonormal wavelets: the Shannon, Meyer, Battle-Lemarié, and Daubechies wavelets. Finally, we construct a biorthogonal wavelet. Other wavelets such as ridgelets, curvelets, complex wavelets, and lifting wavelets are discussed in Chapter 8.

### 6.1 NECESSARY INGREDIENTS FOR WAVELET CONSTRUCTION

As pointed out before, we need to obtain the coefficient sequences \(\{g_0[k]\}\), \(\{g_1[k]\}\) to be able to construct wavelets. In this section, our goal is to find a relationship among various sequences. This will help us in reducing our task. Here we consider the case of semiorthogonal decomposition of a multiresolution space.

### 6.1.1 Relationship between the Two-Scale Sequences

Recall from Chapter 5 that, as a result of the multiresolution properties, the scaling functions and wavelets at one scale (coarser) are related to the scaling functions at the next higher scale (finer) by the so-called two-scale relations:

```
(6.4)
\(\phi(t) = \sum_k g_0[k] \phi(2t - k),\)
```

```
(6.5)
\(\psi(t) = \sum_k g_1[k] \phi(2t - k).\)
```

By taking the Fourier transform of the above relation, we have

```
(6.6)
\(\hat{\phi}(\omega) = G_0(z) \hat{\phi}\left(\frac{\omega}{2}\right),\)
```

```
(6.7)
\(\hat{\psi}(\omega) = G_1(z) \hat{\phi}\left(\frac{\omega}{2}\right),\)
```

where \(z = e^{-j\omega/2}\) and

```
(6.8)
\(G_0(z) := \frac{1}{2} \sum_k g_0[k] z^k,\)
```

(6.9) $$G_1(z) := \frac{1}{2} \sum_k g_1[k] z^k.$$

Observe that \(\phi(t) \in A_0, \phi(2t) \in A_1\), and \(\psi(t) \in W_0\). From the nested property of MRA, we know that \(A_0 \subset A_1\) and \(A_0 \perp W_0\) such that \(A_0 \oplus W_0 = A_1\). The orthogonality of the subspaces \(A_0\) and \(W_0\) implies that for any \(\ell \in \mathbb{Z}\),

(6.10) $$\langle \phi(t - \ell), \psi(t) \rangle = 0.$$

Equation (6.10) can be rewritten by using the Parseval's identity as

$$\begin{aligned} 0 &= \frac{1}{2\pi} \int_{-\infty}^{\infty} \hat{\phi}(\omega) e^{-j\ell\omega} \overline{\hat{\psi}(\omega)} d\omega \\ &= \frac{1}{2\pi} \int_{-\infty}^{\infty} G_0(z) \overline{G_1(z)} \left| \hat{\phi} \left( \frac{\omega}{2} \right) \right|^2 e^{-j\ell\omega} d\omega \\ &= \frac{1}{2\pi} \sum_k \int_{4\pi k}^{4\pi(k+1)} G_0(z) \overline{G_1(z)} \left| \hat{\phi} \left( \frac{\omega}{2} \right) \right|^2 e^{-j\ell\omega} d\omega \\ &= \frac{1}{2\pi} \sum_k \int_{0}^{4\pi} G_0(z) \overline{G_1(z)} \left| \hat{\phi} \left( \frac{\omega}{2} + 2\pi k \right) \right|^2 e^{-j\ell\omega} d\omega \\ &= \frac{1}{2\pi} \int_{0}^{4\pi} G_0(z) \overline{G_1(z)} E_\phi(z) e^{-j\omega} d\omega \end{aligned}$$ (6.11)

where \(z = e^{-j\omega/2}\). By partitioning the integration limit \([0, 4\pi]\) into \([0, 2\pi]\) and \([2\pi, 4\pi]\), and with a simple change of variable, it is easy to verify that equation (6.11) is the same as

(6.12)
\(\frac{1}{2\pi} \int_0^{2\pi} [G_0(z)\overline{G_1(z)} E_\phi(z) + G_0(-z)\overline{G_1(-z)} E_\phi(-z)] e^{-j\ell\omega} d\omega = 0.\)

The expression (6.12) holds for all \(\ell \in \mathbb{Z}\). What does it mean? To understand this let us recall that an integrable \(2\pi\)-periodic function \(f(t)\) has the Fourier series representation

(6.13)
\(f(\omega) = \sum_\ell c_\ell e^{j\ell\omega}, \text{ where}\)

(6.14)
\(c_\ell = \frac{1}{2\pi} \int_0^{2\pi} f(\omega) e^{-j\ell\omega} d\omega.\)

From the above it is clear that the quantity on the left of (6.12) represents the \(\ell\)-th Fourier coefficient of a periodic function \(G_0(z)\overline{G_1(z)} E_\phi(z) + G_0(-z)\overline{G_1(-z)} E_\phi(-z)\). Since all these coefficients are zero, it implies that

(6.15)
\(G_0(z)\overline{G_1(z)} E_\phi(z) + G_0(-z)\overline{G_1(-z)} E_\phi(-z) \equiv 0\)

for \(|z| = 1\). The solution of (6.15) gives the relationship between \(G_1(z)\) and \(G_0(z)\). By direct substitution, we can verify that

(6.16)
\(G_1(z) = -c z^{2m+1} \overline{G_0(-z)} E_\phi(-z)\)

for any integer \(m\), and a constant \(c > 0\) is a solution (6.15). Without any loss of generality we can set \(c = 1\). The effect of \(m\) is to shift the index of the sequence \(\{g_1[k]\}\). Usually \(m\) is chosen such that the index begins with 0.

### 6.1.2 Relationship between Reconstruction and Decomposition Sequences

Recall from Chapter 5 that the scaling function at a certain scale (finer) can be obtained from the scaling functions and wavelets at the next lower (coarse) scale. In mathematical terms, it means that there exist finite energy sequences \(\{h_0[k]\}, \{h_1[k]\}\) such that

```
(6.17)
\(\phi(2t - \ell) = \sum_k \{h_0[2k - \ell]\phi(t - k) + h_1[2k - \ell]\psi(t - k)\};\)
```

where, as discussed in Chapter 5, \(\{h_0[k]\}, \{h_1[k]\}\) are the decomposition sequences. By taking the Fourier transform of the decomposition relation, we get

```
\(\frac{1}{2} \hat{\phi}\left(\frac{\omega}{2}\right) e^{-j\omega \ell/2} = \sum_k h_0[2k - \ell] e^{-jk\omega} \hat{\phi}(\omega) + \sum_k h_1[2k - \ell] e^{-jk\omega} \hat{\psi}(\omega)\)
\(= \left( G_0(z) \sum_k h_0[2k - \ell] e^{-jk\omega} + G_1(z) \sum_k h_1[2k - \ell] e^{-jk\omega} \right) \hat{\phi}\left(\frac{\omega}{2}\right).\)
```

This equation reduces to
