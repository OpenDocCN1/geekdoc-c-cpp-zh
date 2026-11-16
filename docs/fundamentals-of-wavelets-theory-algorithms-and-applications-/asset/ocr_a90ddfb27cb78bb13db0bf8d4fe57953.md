less than $\pi/\Omega$. The function $f(t)$ is recovered by using the formula

```
$f(t) = h \sum_{k \in \mathbb{Z}} f(kh) \frac{\sin[\Omega(t-kh)]}{[\pi(t-kh)]}, \quad k \in \mathbb{Z}.$

(3.77)
```

If $h = \pi/\Omega$, the sampling frequency $f_s = 1/h = \Omega/\pi$ is called the Nyquist rate. Theoretically, $f(t)$ can always be recovered perfectly from samples if $h < \pi/\Omega$. In practice, however, we cannot recover $f(t)$ without error due to the infinite nature of the sinc function.

Let $\hat{f}(\omega)$ be the Fourier transform of $f(t)$

```
$\hat{f}(\omega) = \int_{-\infty}^{\infty} f(t) e^{-i\omega t} \, dt.$
```

The integral can be approximated using Simpson's rule as

```
$\hat{f}(\omega) \doteq \hat{F}(\omega) = h \sum_{k \in \mathbb{Z}} f(kh) e^{-j\omega kh}.$

(3.78)
```

Using Poisson's sum formula in (3.64), we can rewrite $\hat{F}(\omega)$