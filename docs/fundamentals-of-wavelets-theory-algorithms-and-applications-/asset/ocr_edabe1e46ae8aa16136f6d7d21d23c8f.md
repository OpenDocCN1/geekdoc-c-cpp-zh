(7.12)

$x'(n) = \sum_k y(k)\delta(n-kM).$

The spectrum of the interpolator output is given by

(7.13)

$\hat{X}(e^{j\omega}) = \sum_n \sum_k y(k)\delta(n-kM)e^{-jn\omega}$
$= \sum_k y(k)e^{-jkM\omega}$
$= \hat{Y}(e^{-jM\omega})$

The z-transform of the interpolator output is

(7.14)

$X'(z) = Y(z^M).$

Interpolation raises the sampling rate by filling zeros in between samples. The output sequence has $M$ times more points than the input sequence, and the output spectrum is shrunk by a factor of $M$ on the $\omega$-axis. Unlike the decimator, there is no danger of aliasing for interpolator since the output spectrum has narrower bandwidth than the input spectrum. The spectrum of a twofold interpolator is given in Figure 7.4.

FIGURE 7.4: Spectral characteristic of interpolation by 2.