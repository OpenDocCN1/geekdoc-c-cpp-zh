wavelet coefficients in the DWT in the right panel of Figure 12.8 and then reconstructing the signal (i.e., calculating S₀). This basic idea is the foundation of smoothing techniques based on the DWT, see, for example, Donoho (1993) and Donoho and Johnstone (1994, 1995). The basic model in the wavelet domain is

$d_{j,k} = \theta_{j,k} + z_{j,k}, \qquad (12.35)$

where

+   - $d_{j,k}$ is the detail coefficient calculated from the data
+   - $\theta_{j,k}$ is the unknown “true” detail coefficient associated with the underlying signal
+   - $z_{j,k}$ is the zero-mean white noise with variance $\sigma_z^2$

The key idea for extracting “smooth” signals from noisy data such as the upper right frame of Figure 12.8 is that most of the $\theta_{j,k}$ will be zero or approximately zero. Although many of the wavelet coefficients, $d_{j,k}$, of the noisy signal are nonzero, only a relatively few of these nonzero $d_{j,k}$’s are actually attributable to the true bumps signal. The goal is to reconstruct the “signal” based on the estimates $\hat\theta_{j,k}$. This is typically accomplished by selecting a threshold and “zeroing-out” coefficients less than the threshold. Two thresholding techniques suggested by Donoho and Johnstone (1994) based on a positive threshold $\lambda$ are as follows:

# *Hard threshold (“Keep or Kill”)*

$\hat\theta_{j,k} = 0, \quad \text{if } |d_{j,k}| \le \lambda$
$= d_{j,k}, \quad \text{otherwise.}$

# *Soft threshold*

$\hat\theta_{j,k} = 0, \quad \text{if } |d_{j,k}| \le \lambda$
$= d_{j,k} - \lambda, \quad \text{if } d_{j,k} > \lambda$
$= d_{j,k} + \lambda, \quad \text{if } d_{j,k} < -\lambda.$