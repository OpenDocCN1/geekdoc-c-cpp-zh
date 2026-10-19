![](bbox=[0.02, 0.02, 0.98, 0.58])

A special case of the correlation function c(r) is the autocorrelation function A(r). It measures the correlation of a time signal with itself:

```
A(r) \stackrel{\rm def}{=} \int_{-\infty}^{+\infty} dt \, y^*(t) y(t + r) \equiv \int_{-\infty}^{+\infty} dt \, y(t) y^*(t - r) .
```

This function is computed by taking a signal y(t) that has been measured over some time period and then averaging it over time using y(t + r) as a weighting function. This process is also called folding a function onto itself (as might be done with dough) or a convolution. To see how this folding removes noise from a signal, we go back to the measured signal (12.54), which was the sum of pure signal plus noise s(t) + n(t). As an example, in Figure 12.3a we show a signal that was constructed by adding random noise to a smooth signal. When we compute the autocorrelation function for this signal, we obtain a function (Figure 12.3b) that looks like a broadened, smoothed version of the signal y(t).

We can understand how the noise is removed by taking the Fourier transform of s(t) + n(t) to obtain a simple sum of transforms:

```
Y(\omega) = S(\omega) + N(\omega) ,
```

```
\begin{bmatrix} S(\omega) \\ N(\omega) \end{bmatrix} = \int_{-\infty}^{+\infty} dt \begin{bmatrix} s(t) \\ n(t) \end{bmatrix} \frac{e^{-i\omega t}}{\sqrt{2\pi}} .
```

Because the autocorrelation function (12.58) for y(t) = s(t) + n(t) involves the second power of y, not a linear function, that is, A_y \neq A_s + A_n, but instead

```
A_y(r) = \int_{-\infty}^{+\infty} dt [s(t)s(t + r) + s(t)n(t + r) + n(t)n(t + r)] .
```