```
$$S_X(f)=\frac{P_X(f)}{\sigma_X^2}=\sum_{k=-\infty}^{\infty}e^{-2\pi i k f}\rho_k$$
```

If

```
$$\sum_{k=-\infty}^{\infty}|\gamma_k|<\infty\tag{1.27}$$
```

then it can be shown that the series in Equations 1.25 and 1.26 converge and

```
$$\gamma_k=\int_{-0.5}^{0.5}e^{2\pi i f k}P_X(f)\,df\tag{1.28}$$
```

that is, the spectrum and the autocovariance function are Fourier transform pairs. Consequently, given the spectrum of a stationary process satisfying Equation 1.27, the autocovariance function can be obtained mathematically from it and vice versa. The results in Equations 1.25 and 1.28 show that the autocovariance and the spectrum contain equivalent information about the process. The autocovariance conveys this information in the time domain while the spectrum expresses the equivalent information in the frequency domain. We will see that for a particular application, one of these may provide more understandable information about the process than does the other. A similar relationship exists between the autocorrelation and the spectral density.

We leave it as an exercise to show that $P_X(f)$ and $S_X(f)$ in Definition 1.12 can be written as

```
$$P_X(f)=\sigma_X^2+2\sum_{k=1}^{\infty}\gamma_k\cos(2\pi f k)\tag{1.29}$$
```

and

```
$$S_X(f)=1+2\sum_{k=1}^{\infty}\rho_k\cos(2\pi f k)\tag{1.30}$$
```