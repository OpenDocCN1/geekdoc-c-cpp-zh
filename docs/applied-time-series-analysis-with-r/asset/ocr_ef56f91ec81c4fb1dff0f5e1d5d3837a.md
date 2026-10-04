# ARMA Time Series Models

# 3.2.7.2 Spectral Density of an AR(2)

The spectral density of an AR(2) model is given by Equation 3.54 to be

```
$$S_X(f) = \frac{\sigma_X^2}{|1 - \phi_1 e^{-2\pi if} - \phi_2 e^{-4\pi if}|^2} = \frac{\sigma_X^2}{\{1 + \phi_1^2 + \phi_2^2 - 2\phi_1\cos(2\pi f) - 2\phi_2\cos(4\pi f)\}} $$ (3.64)$
```

In the case of complex roots sufficiently close to the unit circle, the peak in $S_X(f)$ occurs near, not exactly at the system frequency $f_0$ (see Problem 3.20). Also, if the characteristic equation has at least one real root sufficiently close to the unit circle, then $S(f)$ will have a "peak” at $f=0$ if the root is positive, while $S(f)$ will have a peak at $f=0.5$ if the root is negative.

# 3.2.7.3 Stationary/Causal Region of an AR(2)

In order for the AR(2) process to be causal and stationary, it must be that $|\phi_1| < 1$ and $|\phi_2| < 1$. Clearly, this imposes the constraint that $\phi(z) \neq 0$ for $z=1$, that is, $1-\phi_1-\phi_2 \neq 0$. However, this condition is not sufficient to guarantee causality and stationarity. Schur's lemma (see Appendix 3A) gives necessary and sufficient conditions for the roots of a polynomial equation to all lie outside the unit circle. The matrix C described in that lemma the case can be shown to be

```
$$C = \begin{bmatrix} 1-\phi_2^2 & -\phi_1(1+\phi_2) \ -\phi_1(1+\phi_2) & 1-\phi_2^2 \end{bmatrix},$$ (3.65)$
```

(see Problem 3.22(a)). By definition, C is positive if and only if $1-\phi_2^2 > 0$ and $(1-\phi_2)^2[(1-\phi_2)^2-\\phi_1^2] > 0$. Thus, it can be shown (Problem 3.22(b)) that the AR(2) process is stationary if and only if $\phi_1$ and $\phi_2$ satisfy

```
$$$|\phi_2| < 1 \ \phi_1+\phi_2 < 1 \ \phi_2-\\phi_2 < 1. $$
```

# 3.2.7.4 $\psi$-Weights of an AR(2) Model

Factoring the AR(2) model gives

```
$$X_t - \phi_1 X_{t-1} - \phi_2 X_{t-2} = (1-\alpha_1B)(1-\alpha_2B)X_t = a_t,$$ (3.66)$
```