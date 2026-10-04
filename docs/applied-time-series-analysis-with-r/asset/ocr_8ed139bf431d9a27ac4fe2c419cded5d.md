460

Applied Time Series Analysis with R

![](bbox=[0.118, 0.118, 0.868, 0.458])

Figure 11.2
True autocorrelations for fractional processes with various values of d. (a) d = 0.2. (b) d = 0.35. (c) d = 0.45, (d) d = 0.48.

# Theorem 11.2

$X_t$ be a FARMA$(p,d,q)$ process as defined in Equation 11.6.

+   1. If $d < 0.5$ and all the roots of $\varphi(z) = 0$ are outside the unit circle, $X_t$ is causal and stationary
2. If $d > -0.5$ and all the roots of $	heta(z) = 0$ are outside the unit circle, $X_t$ is invertible
3. If $d \in (-0.5, 0.5)$ and $d 
eq 0$, then the autocorrelation function $ho_k$ satisfies

```
$\rho(k) = k^{2d-1} \quad \text{as } k \to \infty. \quad (11.7)$
```

+   4. If $d \in (-0.5, 0.5)$ and $d 
eq 0$, then $\lim_{f \to 0} f^2 S(f)$ exists and is finite

Proof: See Hosking (1981, Theorem 2) or Blackwell and Davis (1991).

NOTE: Hosking (1981) and others call $X_t$ in Equation 11.6 an ARIMA$(p,d,q)$ process, but we reserve the expression ARIMA$(p,d,q)$ to refer to processes for which $d$ is a positive integer. The model in Equation 11.6 is also referred to as an ARFIMA$(p,d,q)$ model.