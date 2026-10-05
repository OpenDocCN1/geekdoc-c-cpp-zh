of these is the type of program a good C/C++ programmer without knowing computer architecture. The optimized MKL and FFTW libraries can be 10 times faster, illustrating the value of optimized libraries and programming with a knowledge of computer architecture.^{15}

# 2.4.1 The FFT algorithm in outline

The discrete Fourier transform of $f_0, \dots, f_{N-1}$ is defined as

```
$$\hat{f}_k = \sum_{j=0}^{N-1} \omega^{-jk}f_j, \quad \text{for } k=0, \dots, N-1. \quad (2.1)$
```

$\omega = \exp(2\pi\sqrt{-1}/N)$ is a primitive $N$th root of unity. The $\hat{f}_k$ are linear functions of $f_j$. The discrete Fourier transform from $f=(f_0, \dots, f_{N-1})$ to $\hat{f}=(\hat{f}_0, \dots, \hat{f}_{N-1})$ can be written as $\hat{f}=Mf$, where $M$ is the $N 	imes N$ matrix whose $(j,k)$ entry is $\omega^{-jk}/N$.

The inverse Fourier transform is given by

```
$f_j = \sum_{k=0}^{N-1} \omega^{jk}\hat{f}_k. \quad (2.2)$
```

It can be thought of as a matrix-vector product.
The discrete Fourier transform and its inverse have an intimate connection to Fourier series. Suppose $f(x)$ is a function with period $2\pi$. Its Fourier coefficients are defined by

```
$c_n = \frac{1}{2\pi} \int_{0}^{2\pi} f(x) \exp(-\sqrt{-1}nx) \dx \quad n=0, \pm1, \pm2, \dots$
```

If $f=f(2\pi j/N)$, then $\hat{f}_k \approx c_k$ for $0 \le k < N/2$ and $\hat{f}_k \approx c_{k-N}$ for $N/2 < k \le N-1$. If $N$ is even, $f_{N/2} \approx (c_{N/2}+c_{-N/2})/2$. Here $f(x)$ is assumed to be a function that is integrable and sufficiently smooth.

> ^{15}Our discussion assumes that the FFTW library has been built using --enable-avx (for machines with YMM registers) or --enable-sse (for machines with XMM registers). Without a proper build, FFTW can be too slow by a factor of 2 or 4.