

$$\Delta_{\psi}^+ := \left\{ \frac{\int_0^\infty \left(\omega - \omega_\psi^*\right)^2 \left|\hat{\psi}(\omega)\right|^2 d\omega}{\int_0^\infty \left|\hat{\psi}(\omega)\right|^2 d\omega} \right\}^{\frac{1}{2}}.$$

**(4.39)**

The definitions for \(t^*\) and \(\Delta_\psi\) remain the same as those in Section 4.1, with \(\phi(t)\) replaced by \(\psi(t)\). For wavelets the uncertainty principle gives

$$\Delta_\psi \Delta_\psi^+ > \frac{1}{2}.$$

**(4.40)**

If \(t^*\) is the center and \(\Delta_\psi\) is the radius of \(\psi(t)\), then \(W_\psi f(b, a)\) contains the information of \(f(t)\) in the time window

$$[at^* + b - a\Delta_\psi, at^* + b + a\Delta_\psi].$$

**(4.41)**

Let us apply Parseval's identity to (4.32) to get an idea of the frequency window:

$$W_\psi f(b, a) = \frac{1}{\sqrt{a}} \int_{-\infty}^\infty f(t) \overline{\psi\left(\frac{t-b}{a}\right)} dt$$

**(4.42)**

$$= \frac{\sqrt{a}}{2\pi} \int_{-\infty}^\infty \hat{f}(\omega) \overline{\hat{\psi}(a\omega)} e^{ib\omega} d\omega.$$

**(4.43)**

From (4.43) it is clear that the frequency window is

$$\left[ \frac{1}{a}(\omega^* - \Delta_\psi^-), \frac{1}{a}(\omega^* + \Delta_\psi^+) \right].$$

**(4.44)**

The time-frequency window product \( = 2a\Delta_\psi \times (2/a)\Delta_\psi^- = 4\Delta_\psi \Delta_\psi^+ = \text{constant.} \)

Figure 4.7 represents the notion of the time-frequency window for the wavelet transform. Compare Figure 4.7 with the corresponding Figure 4.3 for STFT and observe the flexible nature of the window in the wavelet transform.

For the higher frequency \( (1/a_2) \), the time window is small, whereas for the lower frequency \( (1/a_0) \), the time window is large. For the fixed frequency level, \( (1/a_0) \), for example, both the time and frequency windows are fixed. Recall that in STFT the time-frequency window is fixed regardless of the frequency level.

**FIGURE 4.7:** Time-frequency window for continuous wavelet transform.

![](img/f73ae67732328dc36596b27ffe8d0152_151_0.png)

Example:

We perform a continuous wavelet transform on the same function used for computing the STFT. We choose the complex Morlet wavelet given by

$$\psi(t) = e^{\frac{-t^2}{2}} e^{j5.336t}$$

**(4.45)**

to compute the CWT

$$W_\psi f(b,a) = \int_{-\infty}^{\infty} f(t) \overline{\psi\left(\frac{t-b}{a}\right)} dt.$$

The results are shown in Figure 4.8. The figure indicates good resolution of the events in both the time and the frequency axes. If we choose an appropriate range for \(a\), the transform needs be computed only once to capture most, if not all, of the events occurring in the time and frequency domains.

**FIGURE 4.8:** Continuous wavelet transform of the signal shown in Figure 4.4 with Morlet's wavelet.

![](img/f73ae67732328dc36596b27ffe8d0152_152_0.png)

## 4.6 DISCRETE WAVELET TRANSFORM

Similar to the discrete Fourier transform and discrete short-time Fourier transform, we have the discrete wavelet transform (DWT). However, unlike the discretized time and frequency axes shown earlier in Fourier analysis, here we take the discrete values of the scale parameter \(a\) and the translation parameter \(b\) in a different way. The interest here is to introduce the DWT and show the relationship between DWT and IWT. A detailed discussion of the DWT will be presented in Chapter 7. Here we just mention that we will take \(a\) to be of the form \(2^{-s}\) and \(b\) to be of the form \(k2^{-s}\), where \(k, s \in \mathbb{Z}\). With these values of \(a\) and \(b\), the integral of (4.32) becomes

$$W_\psi f(k2^{-s}, 2^{-s}) = 2^{\frac{s}{2}} \int_{-\infty}^{\infty} f(t) \psi(2^s t - k) dt.$$

**(4.46)**

Let us now discretize the function \(f(t)\). For simplicity, assume the sampling rate to be 1. In that case, the integral of (4.46) can be written as

$$W_\psi f(k2^{-s}, 2^{-s}) = 2^{\frac{s}{2}} \sum_n f(n) \psi(2^s n - k).$$

**(4.47)**

To compute the wavelet transform of a function at some point in the time-scale plane, we do not need to know the function values for the entire time axis. All we need is the function at those values of time at which the wavelet is nonzero. Consequently, the evaluation of the wavelet transform can be done almost in real time. We will discuss algorithms to compute the wavelet transform in later chapters.

One of the important observations about (4.47) is its time-variant nature. The DWT of a function shifted in time is quite different from the DWT of the original function. To explain it further, let

$$f_m(t) = f(t - t_m).$$

**(4.48)**

This gives

$$W_\psi f_m(k 2^{-s}, 2^{-s}) = 2^{\frac{s}{2}} \int_{-\infty}^{\infty} f_m(t) \psi(2^s t - k) dt = 2^{\frac{s}{2}} \sum_n f(n-m) \psi(2^s n - k) = 2^{\frac{s}{2}} \sum_n f(n) \psi(2^s n - (k - m 2^s)) = W_\psi f((k - m 2^s) 2^{-s}, 2^{-s}).$$

Therefore, we see that for DWT, a shift in time of a function manifests itself in a rather complicated way. Recall that a shift in time of a function appears as a shift in time location by an exact amount in the case of STFT, with an additional phase shift. Also in Fourier transform, the shift appears only as a phase change in the frequency domain.

## 4.7 WAVELET SERIES

Analogous to the Fourier series, we have the wavelet series. Recall that the Fourier series exists for periodic functions only. Here for any function \(f(t) \in L^2\), we have its wavelet series representation given as

$$f(t) = \sum_s \sum_k w_{k,s} \psi_{k,s}(t),$$

where

$$\psi_{k,s}(t) = 2^{\frac{s}{2}} \psi(2^s t - k).$$

The double summation in (4.50) is due to the fact that wavelets have two parameters: the translation and scale parameters. For a periodic function \( p(t) \), its Fourier series is given by

$$p(t) = \sum_k c_k e^{jkt} .$$

**(4.52)**

Since \( \{e^{jkt} : k \in \mathbb{Z} \} \) is an orthogonal basis of \( L^2(0, 2\pi) \), we can obtain \( c_k \) as

$$c_k = \frac{1}{2\pi} \langle p(t), e^{jkt} \rangle .$$

**(4.53)**

On a similar line, if \( \{\psi_{k,s}(t) : k, s \in \mathbb{Z} \} \) forms an orthonormal basis of \( L^2(\mathbb{R}) \), then we can get

$$w_{k,s} = \langle f(t), \psi_{k,s}(t) \rangle$$

**(4.54)**

$$= W_\psi f \left( \frac{k}{2^s}, \frac{1}{2^s} \right) .$$

**(4.55)**

Therefore, the coefficients \( \{w_{k,s}\} \) in the wavelet series expansion of a function are nothing but the integral wavelet transform of the function evaluated at certain dyadic points \( (k/2^s, 1/2^s) \). No such relationship exists between Fourier series and Fourier transform, which are applicable to different classes of functions; Fourier series applies to functions that are square integrable in \( [0, 2\pi] \), whereas Fourier transform is for functions that are in \( L^2(\mathbb{R}) \). Both wavelet series and wavelet transform, on the other hand, are applicable to functions in \( L^2(\mathbb{R}) \).

If \(\{\psi_{k,s}(t)\}\) is not an orthonormal basis, then we can obtain \(w_{k,s}\) using the dual wavelet \(\{\tilde{\psi}_{k,s}(t)\}\) as \(w_{k,s} = \langle f(t), \tilde{\psi}_{k,s}(t) \rangle\). The concept of dual wavelets will appear in subsequent chapters.

## 4.8 INTERPRETATIONS OF THE TIME-FREQUENCY PLOT

Let us briefly discuss the significance of a surface over the time-frequency plane. Usually the height of a point on the surface represents the magnitude of the STFT or the IWT. Suppose the given function is such that its frequency does not change with time; then we should expect a horizontal line parallel to the time-axis in the time-frequency plot corresponding to the frequency of the function. However, because of the finite support of the window function and the truncation of the sinusoid, instead of getting a line we will see a band (widened line) near the frequency. To understand it more clearly, let us consider a truncated sinusoid of frequency \(\omega_0\). We assume, for the purpose of explaining the time-frequency plot here, that even though the sinusoid is truncated, its Fourier transform is represented as \(\hat{\delta}(\omega - \omega_0)\).

By replacing \(\hat{f}(\omega) = \hat{\delta}(\omega - \omega_0)\) in (4.7) and (4.32), respectively, we obtain

