
![](img/a0e0259119deb8c7b41dfd4f664e541d_614_0.png)

## FIGURE 12.3

Time–frequency representations for the data in Figure 12.1. (a) Gabor spectrum for Figure 12.1a, (b) Gabor spectrum for Figure 12.1b, (c) Wigner–Ville spectrum for Figure 12.1a, and (d) Wigner–Ville spectrum for Figure 12.1b.

![](img/a0e0259119deb8c7b41dfd4f664e541d_614_1.png)

## FIGURE 12.4

Time–frequency representations for the data in Figure 12.2a: (a) Gabor spectrum and (b) Wigner–Ville spectrum.

It is clear that the time–frequency plot in Figure 12.4a does a much better job of describing the frequency behavior in Figure 12.2a than does the usual spectral plot in Figure 12.2b. For more discussion on the Gabor transform see Chui (1992), Kumar and Foufoula-Georgiou (1994), Ogden (1997), and Carmona et al. (1998).

## 12.2.2 Wigner–Ville Spectrum

Recall that the spectrum for a stationary discrete time series defined on t = 0, ± 1, ± 2, ... is defined in Equation 1.25 to be

$P(f) = \sum_{k=-\infty}^{\infty} \gamma(k) e^{-2\pi i f k}$
(12.7)

for −0.5 < f < 0.5. However, for time series whose autocorrelation changes with time, Condition 3 in (12.1) does not hold. Letting γ(t₁, t₂) denote the autocovariance between Xₜ₁ and Xₜ₂ the discrete Wigner–Ville spectrum can be defined by

$W(t, f) = \sum_{k=-\infty}^{\infty} \gamma(t + k/2,\ t - k/2) e^{-2\pi i f k}$
(12.8)

If Xₜ is approximately stationary in a neighborhood of t, then γ(t + k/2, t − k/2) can be approximated by use of a (time domain) window centered at t, see Martin and Flandrin (1985) and Boashash (2003). Figure 12.3c and d shows the Wigner–Ville time–frequency representation associated with the data in Figure 12.2a and b, respectively. It is seen that the information concerning time–frequency relationships are consistent with those shown using the Gabor spectrum shown in Figure 12.3a and b. Similarly, the Wigner–Ville plot in Figure 12.4b for the chirp data shows the same linearly increasing time–frequency relationship shown in Figure 12.4a.

**Using R:** The Gabor transform can be obtained using function cgt in the package Rwave which is available on CRAN, and the Wigner–Ville plot can be obtained using the tswge function wv.wge. See Appendix 12B for more details.

## 12.3 Wavelet Analysis

In this section we give an overview of wavelet analysis and its application to statistical time series analysis of nonstationary data. Wavelets provide an alternative to the window methods for investigating frequency behavior that changes across time. Wavelet analysis is a relatively recent methodology developed primarily in the mathematical sciences and engineering, and it has proved to be a powerful tool for the analysis of localized behavior of data whose characteristics change with time. These methods can be viewed as variations of classical Fourier analysis in which short waves (or “wavelets”) are used in place of the classical sines and cosines.

### 12.3.1 Fourier Series Background

In order to fully appreciate wavelet methods, it is necessary to have some familiarity with the classical Fourier methods of which wavelet analysis is an extension. For a brief review of Fourier series methods, see [Appendix 12A](#).

As discussed in [Section 1.5](#) and [Appendix 12A](#), Fourier analysis involves expressing functions as linear combination of sines and cosines. Theorem 12A.1 states that a well-behaved function, $g$, defined on $[-\pi,\pi]$ can be expressed as a linear combination of the *basis functions* in the orthogonal systems $S_1=\{1,\cos kx,\sin kx;\ k=1,2,\ldots\}$ or equivalently of $S_2=\{e^{ikx},\ k=0,\pm1,\pm2,\ldots\}$. The advantage of using $S_2$ is that the basis functions actually consist of one “fundamental” function, namely, $\varphi(x)=e^{ix}$, and the individual basis functions are “integral dilations” of this function, that is, $e^{ikx}=\varphi(kx)$. Note that as $k$ increases, the function $\varphi(kx)=\cos(kx)+i\sin(kx)$ becomes increasingly higher frequency, that is, the integer $k$ controls the frequency content in the basis function $\varphi(kx)$. Fourier analysis is based on the fact that when certain conditions hold, functions can be written as a linear combination of dilations of the single function $e^{ix}$, see [Appendix 12A](#). In wavelet analysis, functions, $\psi(x)$, will be defined that play a fundamental role such as that played by $\varphi(x)=e^{ikx}$ in Fourier analysis.

### 12.3.2 Wavelet Analysis Introduction

Suppose that $g$ is square integrable over the real line, that is, that $\int_{-\infty}^{\infty}|g(x)|^2dx<\infty$. The class of such functions is denoted $L^2(\mathbb{R})$ where $\mathbb{R}=(-\infty,\infty)$. We desire a collection of basis functions (which are all variations of a single fundamental function, $\psi(x)$ such that functions $g \in L^2(\mathbb{R})$ can be approximated arbitrarily closely using a finite linear combination of these basis elements. It should be noted that $\sin x$, $\cos x$, and $e^{ix}$ are not candidates for the desired basis functions since they are not in $L^2(\mathbb{R})$ themselves. In fact, a necessary condition for
$$
\int_{-\infty}^{\infty} |g(x)|^2\,dx < \infty
$$
is
$$
\lim_{|t|\to\infty}|g(t)|=0.
$$
That is, the basis functions must decay to zero as $|t|\to\infty$, so intuitively short waves or “wavelets” are needed. In the wavelet setting, it is common to use $\psi(2^{-j}x)$, where $j$ is an integer, as dilations of $\psi(x)$. That is, the integer $j$ controls the amount of damping in the basis function $\psi(e^{-kx})$ similar to the way $k$ controls the frequency behavior in the basis function $\varphi(kx)$. Approximating functions $g$ that are defined over the entire real line would intuitively be difficult to accomplish simply using dilations of a single, quickly damping function. Thus, in wavelet analysis, we consider dilations and translations of the basis function for purposes of estimating localized frequency behavior. That is, given a function $\psi(x)$, we use as our basis collection the functions

$$\psi_{j,k}(x)=2^{-j/2}\psi(2^{-j}x-k), \tag{12.9}$$

where $j$ and $k$ are integers that are referred to as the *dilation index* and *translation index*, respectively. The function $\psi(x)$ is called the *mother wavelet* since it “gives birth” to the entire collection of basis elements.

## EXAMPLE 12.1: HAAR WAVELETS

As a first example of a wavelet we consider the Haar wavelet defined by

$$
\psi(x)=
\begin{cases}
1, & 0\le x<1/2,\\
-1, & 1/2\le x<1,\\
0, & \text{elsewhere.}
\end{cases}
\tag{12.10}
$$

**Figure 12.5** shows the Haar mother wavelet along with three dilations and translations. If, for example, $j=2$ and $k=0$, then $\psi_{2,0}(x)$ is given by $\psi_{2,0}(x)=2^{-1}\psi(2^{-2}x-0)$, that is,

The Haar wavelets have compact support because they are equal to zero outside the closed bounded interval [2^j k, 2^j(k+1)]. Specifically,

ψ_{j,k}(x) = 2^{-j/2},      2^j k ≤ x < 2^j(k+0.5)      (12.14)
= -2^{-j/2},  2^j(k+0.5) ≤ x < 2^j(k+1)
= 0,          otherwise.

From Equation 12.14 it follows that the support of ψ_{j,k} is of length 2^j(k+1) − 2^j k = 2^j. Dilates and translates of a wavelet are designed to describe localized frequency behavior. Thus, the wavelet ψ_{j,k} describes localized behavior related to pseudocyclic or detail behavior of duration (or “period”) about 2^j for x in the neighborhood of 2^j(k+0.5). The support of the Haar wavelet ψ_{j,k} is also called the scale of the wavelet. In general the scale of a wavelet is a measure of its width.

*A note about frequencies:* It is important to note that since we are not using sines and cosines as the basis elements, the strict interpretation of frequency is no longer valid. Since scale is a measure of the “period” of a wavelet we use “1/scale” as a measure of “frequency.”

There are many types of wavelets, and the Haar is shown here for simplicity. Properties in Equations 12.12 and 12.13 are true for all wavelets. While the Haar wavelet has compact support, this is not a requirement. However, all wavelets have the property that | ψ_{j,k}(x) | → 0 as | x | → ∞. Figure 12.6 shows several wavelets. The Daublet(4), Daublet(8), and Daublet(12) mother wavelets in Figure 12.6a, c, and e are from the Daublet family of wavelets suggested by Daubechies (1988). The Daublet(2) wavelet, that is, the second-order Daublet, is the Haar wavelet. The higher the order, the smoother the wavelet, and the broader the support. The Daublet(4) wavelet is sometimes called the shark-fin wavelet for obvious reasons. Figure 12.6g shows the Symlet(8) wavelet. This wavelet is widely used and is a member of the Symlet (sometimes called least asymmetric) family of wavelets also proposed by Daubechies (1988). The Symlet and Daublet families are both orthogonal families. That is, for example, the Symlet(8) wavelet and its collection of dilates and translates given in
