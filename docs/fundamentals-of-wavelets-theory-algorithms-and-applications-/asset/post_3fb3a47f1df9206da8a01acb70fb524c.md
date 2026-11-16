
(6.18)
$$
\left( \sum_k h_0[2k-\ell] e^{-j(2k-\ell)\omega/2} \right) G_0(z) \\
+ \left( \sum_k h_1[2k-\ell] e^{-j(2k-\ell)\omega/2} \right) G_1(z) \stackrel{.}{=} \frac{1}{2}, \forall \ell \in \mathbb{Z}.
$$

Combining the Fourier transforms of the decomposition and two-scale relations we get

(6.19)
$$
[H_0(z) + H_0(-z)]G_0(z) + [H_1(z) + H_1(-z)]G_1(z) = \frac{1}{2} \quad \text{for even } \ell;
$$

(6.20)
$$
[H_0(z) - H_0(-z)]G_0(z) + [H_1(z) - H_1(-z)]G_1(z) = \frac{1}{2} \quad \text{for odd } \ell.
$$

where \(z = e^{-j\omega/2}\) and

$$
H_0(z) := \frac{1}{2} \sum_k h_0[k] z^k,
$$

$$
H_1(z) := \frac{1}{2} \sum_k h_1[k] z^k.
$$

These equations lead to

$$
H_0(z)G_0(z) + H_1(z)G_1(z) = \frac{1}{2}
$$

$$
H_0(-z)G_0(z) + H_1(-z)G_1(z) = 0.
$$

The last equation can also be written as

(6.21) \(H_0(z)G_0(-z) + H_1(z)G_1(-z) = 0.\)

In the matrix form, we have

(6.22)
$$
\begin{bmatrix} G_0(z) & G_1(z) \\ G_0(-z) & G_1(-z) \end{bmatrix} \begin{bmatrix} H_0(z) \\ H_1(z) \end{bmatrix} = \begin{bmatrix} \frac{1}{2} \\ 0 \end{bmatrix},
$$

the solution of which gives

(6.23) \(H_0(z) = \frac{1}{2} \times \frac{G_1(-z)}{\Delta_{G_0 G_1}(z)}\)

(6.24) \(H_1(z) = -\frac{1}{2} \times \frac{G_0(-z)}{\Delta_{G_0 G_1}(z)}\)

with \(\Delta_{G_0 G_1}(z) = G_0(z)G_1(-z) - G_0(-z)G_1(z)\).

It can be shown that

(6.26) \(\Delta_{G_0 G_1}(z) = c z^n E_\phi(z^2),\)

where \(c > 0\) and \(n\) is an integer. Since \(\phi\) generates a Riesz or stable basis, \(E_\phi(z)\) and hence \(\Delta_{G_0 G_1}(z) \neq 0\).

## 6.2 CONSTRUCTION OF SEMIORTHOGONAL SPLINE WAVELETS

The significance of the results obtained in Section 6.1 is that we need to construct only the scaling functions—that is, we need to find only the sequence \(\{g_0[k]\}\). In this section we will obtain these sequences for semiorthogonal spline wavelets introduced by Chui-Wang [1]. Here the cardinal B-splines \(N_m\) are chosen to be the scaling functions. We will show that a finite energy sequence \(\{g_0[m, k]\}\) exists such that the scaling relation

$$
N_m(t) = \sum_k g_0[m, k] N_m(2t - k)
$$

is satisfied and, therefore, \(N_m(t)\) is a scaling function. For \(m = 1\), \(\{N_1(t - k) : k \in \mathbb{Z}\}\) form an orthonormal basis of \(\mathcal{A}_0\). For this case, we have already seen that \(g_0[0] = g_0[1] = 1\) (see Figure 5.3). In this section we will consider the cases for which \(m \ge 2\).

For \(m \ge 2\), the scaling functions \(\{N_m(t - k) : k \in \mathbb{Z}\}\) are no longer orthogonal:

$$
\int_{-\infty}^{\infty} N_m(t) N_m(t - \ell) \, dt \neq \delta_{0, \ell}
$$

for all \(\ell \in \mathbb{Z}\). An example of nonorthogonality of \(N_2(t)\) is shown in Figure 6.1. The \(\int_{-\infty}^{\infty} N_2(t) N_2(t - \ell) \, dt\) is shown by the shaded area, which is non-zero.

FIGURE 6.1: Nonorthogonality of linear spline shown by the shaded area.

![](img/f73ae67732328dc36596b27ffe8d0152_225_0.png)

### 6.2.1 Expression for \(\{g_0[k]\}\)

Recall, from the definition of \(N_m(t)\) in Chapter 5, that

$$
N_m(t) = (\underbrace{N_1 * \cdots * N_1}_m)(t)
$$

and that

$$
\hat{N}_m(\omega) = \left( \frac{1 - e^{-j\omega}}{j\omega} \right)^m. \tag{6.29}
$$

From the Fourier transform of the two-scale relation, we have

$$
G_0(z) = \frac{1}{2} \sum_k g_0[m, k] z^k = \frac{\hat{N}_m(\omega)}{\hat{N}_m(\omega/2)}
= \left( \frac{1 + e^{-j\omega/2}}{2} \right)^m
= 2^{-m}(1+z)^m, \quad z = e^{-j\omega/2},
$$

$$
= 2^{-m} \sum_{k=0}^m \binom{m}{k} z^k.
$$

By comparing the coefficient of powers of \(z\), we get

$$
g_0[k] := g_0[m, k] = \begin{cases} 2^{-m+1} \binom{m}{k}, & 0 \le k \le m \\ 0 & \text{otherwise.} \end{cases}
$$

Once we have \(\{g_0[k]\}\), the rest of the sequences \(\{g_1[k]\}\), \(\{h_0[k]\}\), and \(\{h_1[k]\}\) can be found by using the relations derived in Section 6.1. The expression of \(\{g_1[k]\}\) is derived next.

For \(N_m(t)\), the E-F-L polynomial \(E_{N_m}(z)\) takes the form of

$$
E_{N_m}(z) = \sum_{k=-\infty}^{\infty} \left| \hat{N}_m \left( \frac{\omega}{2} + 2\pi k \right) \right|^2
= \sum_{k=-\infty}^{\infty} A_{N_m}(k) z^k
= \sum_{k=m+1}^{m-1} N_{2m}(m+k) z^k ,
\tag{6.33}
$$

with \(z := e^{-j\omega/2}\) and the autocorrelation function

$$
A_{N_m}(k) = \int_{-\infty}^{\infty} N_m(x) N_m(k+m) \, dx = N_{2m}(m+k) .
\tag{6.34}
$$

Finally, by using the relation (6.16), we have

$$
g_1[k] := g_1[m,k] = (-1)^k 2^{-m+1} \sum_{\ell=0}^{m} \binom{m}{\ell} N_{2m}(k+1-\ell), \quad 0 \le k \le 3m-2 .
\tag{6.35}
$$

### 6.2.2 Remarks

Recall that, in the expressions for \(H_0(z)\) and \(H_1(z)\) in terms of \(G_0(z)\) and \(G_1(z)\), there is a term \(\Delta_{G_0 G_1}(z) = z^m E_{N_m}(z)\) in the denominator. Consequently, the sequences \(\{h_0[k]\}\) and \(\{h_1[k]\}\) are infinitely long, although their magnitude decays exponentially. These are the sequences that will be used in the development of decomposition and reconstruction algorithms in Chapters 7 and 8. It is clear that while \(G_0\) and \(G_1\) form FIR filters, \(H_0\) and \(H_1\) are always IIR. We will, however, prove in Chapter 7 that we can use \(G_0\) and \(G_1\) for both reconstruction and decomposition purposes. This is a consequence of the duality principle that we briefly mentioned in Chapter 5.

The commonly used cubic spline and the corresponding semiorthogonal wavelet with their duals and magnitude spectra are shown in Figures 6.2 and 6.3. See Chapter 10 for the expressions of commonly used semiorthogonal scaling functions and wavelets. Table 6.1 gives the coefficients \(\{g_1[m, k]\}\) for \(m = 2\) through 6.

TABLE 6.1: Coefficients \(u_{m,k} := 2^{m-1} (2m - 1)! g_1[m, k]\) for Semiorthogonal Wavelet (\(g_1[m, k] = (-1)^m g_1[m, 3m - 2 - k]\))

| k | \(u_{m,k}\) | k | \(u_{m,k}\) | k | \(u_{m,k}\) |
|---|---|---|---|---|---|
| \(m=2\) | | \(m=5\) | | \(m=6\) | |
| 0 | 1 | 0 | 1 | 0 | 1 |
| 1 | -6 | 1 | -507 | 1 | -2,042 |
| 2 | 10 | 2 | 17,128 | 2 | 164,868 |
| 3 | -39 | 3 | -166,304 | 3 | -5,314,970 |
| 4 | -147 | 4 | 748,465 | 4 | 72,108,334 |
| 5 | -303 | 5 | -1,900,113 | 5 | -410,288,436 |
| | | 6 | 2,973,560 | 6 | 296,526,880 |
| \(m=3\) | | | | 7 | -525,228,384 |
| 0 | 1 | | | 8 | 633,375,552 |
| 1 | -29 | | | | |
| 2 | 147 | | | | |
| 3 | -303 | | | | |
| 4 | -1 | | | | |
| 5 | 4 | | | | |
| \(m=4\) | | | | | |
| 0 | 1 | | | | |
| 1 | -124 | | | | |
| 2 | 1,677 | | | | |
| 3 | -7,904 | | | | |
| 4 | 18,482 | | | | |
| 5 | -24,264 | | | | |

FIGURE 6.2: Linear spline, dual linear spline, the corresponding wavelets, and their magnitude spectra.

![](img/f73ae67732328dc36596b27ffe8d0152_229_0.png)

FIGURE 6.3: Cubic spline, dual cubic spline, the corresponding wavelets, and their magnitude spectra.

![](img/f73ae67732328dc36596b27ffe8d0152_230_0.png)

## 6.3 CONSTRUCTION OF ORTHONORMAL WAVELETS

Recall from Chapter 2 that the Riesz bounds for orthonormal bases are 1. Therefore, for orthonormal scaling functions, \(\phi\), and the corresponding wavelets \(\varphi\), we have

$$
E_\phi(e^{i\nu}) = \sum_K |\hat{\phi}(\omega + 2\pi k)|^2 \equiv 1,
$$

$$
E_\psi(e^{j\nu}) = \sum_k |\hat{\psi}(\omega + 2\pi k)|^2 \equiv 1,
$$

for almost all \(\omega\). Consequently,

$$
\tilde{\phi}(t) = \phi(t), \quad \text{and} \quad \tilde{\psi}(t) = \psi(t);
$$

that is, they are self-duals. Remember from our discussion in Chapter 5 that because of the nested nature of MRA subspaces, the scaling functions are not orthogonal with respect to scales. Orthonormal scaling functions imply that these are orthogonal with respect to translation on a given scale. Orthonormal wavelets, on the other hand, are orthonormal with respect to scale as well as the translation. By starting with

$$
\langle \phi(t - \ell), \phi(t) \rangle = \delta_{0,\ell}
\tag{6.36}
$$

and following the derivation of (6.12), we arrive at the following results:

$$
|G_0(z)|^2 + |G_0(-z)|^2 \equiv 1, \quad |z| = 1.
\tag{6.37}
$$

For orthonormal scaling functions and wavelets, the relationships among the various sequences \(\{g_0[k]\}\), \(\{g_1[k]\}\), \(\{h_0[k]\}\), and \(\{h_1[k]\}\) can be obtained from the results of Section 6.1 by setting \(m = 0\). These results are summarized below.
