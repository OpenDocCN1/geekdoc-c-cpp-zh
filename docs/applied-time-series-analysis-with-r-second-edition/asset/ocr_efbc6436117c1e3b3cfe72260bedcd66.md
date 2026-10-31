+   2. If \(|u|<1\) and \(\lambda>-1/2\) or if \(u=\pm1\) and \(\lambda>-1/4\), then \(X_t\) is invertible.

+   3. The spectrum of a stationary and invertible Gegenbauer process is given by

$$
P(f)=\sigma_{a_l}^{2}\left|1-2u\exp(2\pi if)+\exp(4\pi if)\right|^{-2\lambda}
$$
$$
=\sigma_{a_l}^{2}\left[4(\cos 2\pi f-u)^2\right]^{-\lambda}.
$$
(11.15)

The frequency \(f_G=(\cos^{-1}u)(2\pi)\) is referred to as the *Gegenbauer frequency (G-frequency)*.

+   4. If \(0<\lambda<1/2\) and \(|u|<1\) or if \(|u|=1\) and \(0<\lambda<1/4\), then \(X_t\) is long memory.

+   5. The autocorrelations of a stationary and invertible Gegenbauer process, \(X_t\), are given in the following:

+   a. If \(u=1\) and \(0<\lambda<1/4\), the autocorrelation function of \(X_t\) is

$$\rho_k=\frac{\Gamma(1-2\lambda)\,\Gamma(k+2\lambda)}{\Gamma(2\lambda)\,\Gamma(k-2\lambda+1)}.$$

Thus \(\rho_k\simeq k^{4\lambda-1}\) as \(k\to\infty\). Also,

$$\sigma_X^2=\frac{\Gamma(-4\lambda+1)}{\left(\Gamma(-2\lambda+1)\right)^2}.$$

+   b. If \(u=-1\) and \(0<\lambda<1/4\), the autocorrelation function of \(X_t\) is

$$\rho_k=(-1)^k\frac{\Gamma(1-2\lambda)\,\Gamma(k+2\lambda)}{\Gamma(2\lambda)\,\Gamma(k-2\lambda+1)}.$$

Thus \(\rho_k\simeq(-1)^k k^{4\lambda-1}\) as \(k\to\infty\). Also,

$$\sigma_X^2=\frac{\Gamma(-4\lambda+1)}{\left(\Gamma(-2\lambda+1)\right)^2}.$$

+   c. If \(|u|<1\) and \(0<\lambda<1/2\), then

$$\rho_k\simeq k^{2\lambda-1}\cos(2\pi f_G k),\qquad\text{as }k\to\infty\text{ where }f_G\text{ is the G-frequency}$$
$$\text{defined in (3). Also, }\sigma_X^2=\sum_{j=0}^{\infty}[C_j^{(\lambda)}(u)]^2\sigma_a^2.$$

*Proof:* See Gray et al. (1989, 1994) and Andel (1986). Note that (4) follows from