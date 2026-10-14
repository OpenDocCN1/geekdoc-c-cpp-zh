# TABLE 24.3

Numerical Results for Example 3

| x | Exact Solution $f_{ex}(x)$ | Approximate Solution $f(x)$ | Error $|f_{ex}(x)-f(x)|$ |
|---|---|---|---|
| 0 | 0.0 | 0.0 | 3.46944695e-18 |
| 0.1 | 0.01 | 0.01 | 0.0 |
| 0.2 | 0.04 | 0.04 | 0.0 |
| 0.3 | 0.09 | 0.09 | 0.0 |
| 0.4 | 0.16 | 0.16 | 0.0 |
| 0.5 | 0.25 | 0.25 | 0.0 |
| 0.6 | 0.36 | 0.36 | 0.0 |
| 0.7 | 0.49 | 0.49 | 0.0 |
| 0.8 | 0.64 | 0.64 | 0.0 |
| 0.9 | 0.81 | 0.81 | 0.0 |

# TABLE 24.4

Numerical Results for Example 4

| x | Exact Solution $f_{ex}(x)$ | Approximate Solution $f(x)$ | Error $|f_{ex}(x)-f(x)|$ |
|---|---|---|---|
| 0 | 0 | 0.00078125 | 7.81250000e-04 |
| 0.1 | 0.001 | 0.00078125 | 2.18749991e-04 |
| 0.2 | 0.008 | 0.00828125 | 2.81250018e-04 |
| 0.3 | 0.027 | 0.02671875 | 2.81249968e-04 |
| 0.4 | 0.064 | 0.06421875 | 2.18750042e-04 |
| 0.5 | 0.125 | 0.12578125 | 7.81250052e-04 |
| 0.6 | 0.216 | 0.21578125 | 2.18749938e-04 |
| 0.7 | 0.343 | 0.34328125 | 2.81250074e-04 |
| 0.8 | 0.512 | 0.51171875 | 2.81249910e-04 |
| 0.9 | 0.729 | 0.72921875 | 2.18750103e-04 |

# Example 5.5 Solve the following integral equation:

$$\int_{0}^{x} \exp(x-t) f(t) dt = x \quad 0 \le x < 1,$$

with the exact solution $f(x)=1-x$.

The minimum value of RMS is achieved for $r=10^{-6}$ and its value is 3.16342271e-12. The MAE obtained in [13] using Haar wavelet with 16 collocation points is 4.5e-04 whereas in our method the MAE obtained is 6.89326373e-12 using 12 collocation points. The accuracy achieved by the present method is much higher than the method presented in [13]. The numerical results are presented in Table 24.5.

# Example 5.6 Solve the following integral equation:

$$\int_{0}^{x} e^{(x-t)} \ln(f(t)) dt = e^{x} - x - 1, \quad 0 \le x < 1.$$