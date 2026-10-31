In the same manner that the fractional process has been extended to FARMA process, Definition 11.6 which follows extends the Gegenbauer process by combining it with the ARMA process.

# Definition 11.6

If $X_t$ is a causal, stationary, and invertible process satisfying

$\phi(B)(1 - 2uB + B^2)^{\lambda}(X_t - \mu) = \theta(B)a_t,$  (11.16)

where $\phi(z)$ and $\theta(z)$ share no common factors, then $X_t$ is a Gegenbauer ARMA (GARMA) process which will be denoted GARMA$(p, \lambda, u, q)$.

Theorem 11.5 summarizes the properties of the GARMA process.

# Theorem 11.5

Let $X_t$ be a GARMA process $(\lambda \neq 0)$ and let all roots of $\phi(z)=0$ and $\theta(z)=0$ lie outside the unit circle. Then we have the following:

+   1. $X_t$ is stationary if $\lambda < 1/4$ when $u = \pm 1$ or $\lambda < 1/2$ when $|u| < 1$.
+   2. $X_t$ is invertible if $\lambda > -1/4$ when $u = \pm 1$ or $\lambda > -1/2$ when $|u| < 1$.
+   3. The spectrum is given by
+      $$P(f) = \sigma_a^2 \left| \frac{\theta(e^{-2\pi i f})}{\phi(e^{-2\pi i f})} \right|^2 \left| 1 - 2u\exp(-2\pi i f) + \exp(-4\pi i f) \right|^{-2\lambda}$$
+      $$= \sigma_a^2 \left| \frac{\theta(e^{-2\pi i f})}{\phi(e^{-2\pi i f})} \right|^2 \left[4(\cos 2\pi f - \cos 2\pi f_G)^2\right]^{-\lambda}.$$
+   4. $X_t$ is long memory if $0 < \lambda < 1/4$ when $u = \pm 1$ or $0 < \lambda < 1/2$ when $|u| < 1$.
+   5. As $k \to \infty$, 
+      a. $\rho_k \simeq k^{4\lambda -1}$ when $u = 1$ and $0 < \lambda < 1/4$
+      b. $\rho_k \simeq (-1)^k k^{4\lambda -1}$ when $u = -1$ and $0 < \lambda < 1/4$
+      c. $\rho_k \simeq k^{2\lambda -1} \cos(2\pi f_G k)$ when $|u| < 1$ and $0 < \lambda < 1/4$

*Proof:* See Gray et al. (1989, 1994).