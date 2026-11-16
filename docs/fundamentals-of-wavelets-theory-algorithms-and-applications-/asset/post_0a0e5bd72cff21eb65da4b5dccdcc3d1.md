
## FIGURE 8.24: A typical magnitude spectrum of a signal.

![](img/f73ae67732328dc36596b27ffe8d0152_399_0.png)

From (8.49) we have

(8.51)
\(2\hat{s}_+(\omega) = \hat{s}(\omega)[1 + \text{sgn}(\omega)] = \hat{s}(\omega) + j[-j \text{sgn}(\omega)\hat{s}(\omega)]\)

where \(\text{sgn}(\omega)\) is the signum function defined as

(8.52)
\(\text{sgn}(\omega) = \begin{cases} 1 & \omega > 0 \\ 0 & \omega = 0 \\ -1 & \omega < 0. \end{cases}\)

In (8.51), \(s_h(t)\) is the Hilbert transform of \(s(t)\), defined as

(8.53)
\(s_h(t) = \mathcal{F}^{-1}\{-j \text{sgn}(\omega)\hat{s}(\omega)\} = \frac{1}{\pi} \int_{-\infty}^{\infty} \frac{s(\tau)}{t - \tau} d\tau\)

where \(\mathcal{F}^{-1}\) represents inverse Fourier transform. It is easy to verify that \(\langle s(t), s_h(t) \rangle = 0 \Rightarrow s_h(t) \perp s(t)\).

There are broadly two approaches to implementing discrete complex wavelets. In the first, \(\psi_c\) forms an orthonormal or biorthogonal basis [15–16]. Such constraints on orthonormality, however, prevent the complex wavelet transform to overcome the shortcomings of DWT, as outlined before. In the other approach, \(\psi_r\) and \(\psi_i\) individually form orthonormal or biorthogonal bases. This latter approach leads to a redundant dual-tree complex wavelets, which is based on two filter bank trees and thus two bases [17–18]. Essentially, dual-tree complex wavelets employ two real DWTs to produce the real and imaginary parts of the transform. Figure 8.25 illustrates decomposition and reconstruction using dual-tree complex wavelets (compare this with Figure 7.19). Since there are two DWT-type processings, we have two pairs of low-pass \(\{g_0, h_0\}\) and band-pass \(\{g_1, h_1\}\) filters along with their duals.

## FIGURE 8.25: Decomposition and reconstruction of a signal using complex wavelets; \(\hat{x}(n)\) should ideally be exactly same as \(x(n)\).

![](img/f73ae67732328dc36596b27ffe8d0152_401_0.png)

It can be shown that a compactly supported wavelet (time-limited function) can only have an approximate Hilbert transform. Hence complex wavelets cannot entirely eliminate the shortcomings of real-valued wavelets mentioned previously; they can only reduce them. The key challenge in dual-tree wavelet design is the joint design of its two filter banks to yield a set of complex wavelet and scaling functions that are as close as possible to be analytic.

The filter sets {h0(n), h1(n)} and {g0(n), g1(n)} individually satisfy the perfect reconstruction (PR) condition. They are the processing filters for the wavelet \(\psi(t)\) and \(\psi_g(t)\), respectively. The filters are jointly designed such that the complex wavelet (8.54) \(\psi_c(t) = \psi_h(t) + j\psi_g(t)\) is approximately analytic—that is, \(\psi_g(t)\) is approximately the Hilbert transform of \(\psi_h(t)\). The dual-tree approach comes very close to mirroring the properties of the Fourier transform.

The filters are all real-valued so that there is no complex processing in the implementation of complex wavelet transform. The complexity is exactly twice that of a 1D real-valued DWT.

It has been shown [17] that the following conditions should be satisfied at least approximately by the filter banks:

- 1. The low-pass filters \(h_0\) and \(g_0\) should be approximately a half-sample shift of each other. That is

  (8.55) \(g_0(n) = h_0(n - 0.5)\)

  which implies that \(\psi_g(t)\) is approximately the Hilbert transform of \(\psi_h(t)\). In the spectral domain, the condition (8.55) is equivalent to the requirement

  (8.56) \(|G_0(z)| = |H_0(z)|; z = e^{j\omega}\)
  \(\angle G_0(z) = \angle H_0(z) - 0.5\omega\)

- 2. PR condition must be satisfied by the filter banks.

- 3. Finite impulse response filters must be of approximately the same length.

- 4. There must be good stop-band behavior.

There are three approaches [17] to designing these filter banks.

### 8.4.1 Linear Phase Biorthogonal Approach

The filter $h_0$ and $g_0$ are symmetric FIR, with odd and even lengths, respectively

$h_0(n) = h_0(N-1-n)$,

$g_0(n) = g_0(N-1)$,

where $N$ is an odd number so that the half-delay condition is met. This satisfies the phase condition of (8.56); however, the filters should be designed such that spectral amplitudes are approximately the same.

### 8.4.2 Quarter-Shift Approach

In the quarter-shift (q-shift) method, the filter length $N$ of $h_0(n)$ is chosen as even and $g_0(n)$ is set to be

(8.57) $g_0(n) = h_0(N-1-n)$.

This choice clearly satisfies the magnitude condition of (8.56); however, the filters should be designed such that both have approximately the same phase characteristics.

Figure 8.26 show complex wavelets designed using q-shift approach (N = 14).

## FIGURE 8.26: Complex wavelets using the q-shift approach (N = 14).

(Reprinted with permission from [17], copyright © 2005 by IEEE.)

![](img/f73ae67732328dc36596b27ffe8d0152_404_0.png)

### 8.4.3 Common Factor Approach

By choosing a common factor and introducing it into the low-pass filters

$h_0(n) = F(n) * A(n)$

$g_0(n) = F(n) * A(L - n)$

the amplitude requirement of (8.56) is satisfied. The phase requirement can be approximately satisfied if the phase of A(n) is chosen as a fractional delay allpass filter. Figure 8.27 show complex wavelets designed all using common factor approach.

## FIGURE 8.27: Complex wavelets using the common factor approach.

(Reprinted with permission from [17], copyright © 2005 by IEEE.)

![](img/f73ae67732328dc36596b27ffe8d0152_405_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_405_1.png)

![](img/f73ae67732328dc36596b27ffe8d0152_405_2.png)

![](img/f73ae67732328dc36596b27ffe8d0152_405_3.png)

### 8.5 LIFTING WAVELET TRANSFORM

The lifting scheme [19] is an alternative approach to constructing wavelets and computing wavelet transform. Unlike the classical wavelet construction methods demonstrated in previous chapters that rely heavily on the Fourier transform, the lifting procedure for discrete wavelet transform and for wavelet construction is carried out entirely in the time domain. Instead of using the filter banks for decomposition and reconstruction of a signal, the lifting procedure uses three steps—namely, the split [S], the predict [P] and the update [U] to decompose a signal into approximation and wavelet coefficients $a_{k,S}$ and $w_{k,S}$. It eliminates the need for performing the convolution followed by decimation or interpolation followed by convolution in wavelet analysis of a signal. Instead of using the synthesis filters $g_0[k]$ and $g_1[k]$ to derive the analysis filters $h_0[k]$ and $h_1[k]$, as shown in Chapter 6, the lifting algorithm can be used to construct the wavelet from coefficients resulting from the lifting process.

The advantage of the lifting procedure is that the coefficients can be computed in place to minimize the storage requirement and the reconstruction phase can be carried out by running the decomposition process backward. The procedure eliminates the need for the Fourier transform as in the classical method for signal processing, and new wavelets are constructed out of the lifting process.

In this section, we use the Haar wavelet to illustrate the decomposition of a signal. It proceeds in simple steps, with each step moving toward one-level lower in resolution. It computes the average and difference of adjacent signal values. Let $\{x(k)\}$ be a signal that has $2^n$ points. At some resolution $j + 1$, one decomposition step using Haar wavelet computes the average and difference of the adjacent signal value.

$a_{k, \ell} = \frac{a_{2k, \ell+1} + a_{2k+1, \ell+1}}{2}$,

$w_{k, \ell} = a_{2k+1, \ell+1} - a_{2k, \ell+1}$.

As this step is repeated, it generates the approximation coefficient (the average) and wavelet coefficients (the difference) of the next lower resolution.

It is easy to see that if we wish to reconstruct the signal from level \(\ell\) to \((\ell + 1)\), we simply solve for the values of \(a_{2k, \ell+1}\) and \(a_{2k+1, \ell+1}\), using the above equations to obtain

(8.58) \(a_{2k+1, \ell+1} = a_{k, \ell} + \frac{w_{k, \ell}}{2},\)

(8.59) \(a_{2k, \ell+1} = a_{k, \ell} - \frac{w_{k, \ell}}{2}.\)

Rewriting (8.59),

(8.60) \(a_{k, \ell} = a_{2k, \ell+1} + \frac{w_{k, \ell}}{2},\)

we observe that the approximation coefficient of the lower resolution can be computed from the corresponding approximation coefficients of the higher resolution—namely the even coefficient plus half of the difference between its adjacent coefficients. Instead of computing the average and difference simultaneously, we
