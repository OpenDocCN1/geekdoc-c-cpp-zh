$f(t)$. If $t$ represents space, $\hat{f}(\omega)$ is called the *spatial spectrum*.

The Fourier transform is very important in the development of wavelet analysis and will be used often in subsequent chapters. We will use it as an example to present some of the properties of the $\delta$-function.

Let us recall that

(3.23) \(\int_{-\infty}^{\infty} f(t)\delta(t-y)dt = f(y)\).

Consequently, the Fourier transform of $\delta(t)$

(3.24) \(\hat{\delta}(\omega) = \int_{-\infty}^{\infty} \delta(t)e^{-j\omega t}dt = e^{-j\omega 0} = 1\).

From the inverse transform of $\hat{\delta}(\omega)$, the identity

(3.25) \(\delta(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} e^{j\omega t} d\omega\)

is established. The inverse transform in (3.22) can now be shown to be