$Y_t = \sum_{j=1}^{m} A_j \cos(2\pi f_j t + \mathcal{U}_j) + N_t,$
$= H_t + N_t,$

for $t = 0, \pm1, ...$, where $H_t$ is referred to as the harmonic component or signal and $N_t$ is a stationary noise process. As in Equation 4.5, the $A_j$ and $f_j$ are constants, and the $\mathcal{U}_j$ s are uncorrelated random variables each distributed as uniform $[0, 2\pi]$. Additionally, $H_t$ and $N_t$ are uncorrelated processes. It follows at once that $Y_t$ in Equation 4.10 is a stationary process, since it is the sum of uncorrelated stationary processes (see Problem 1.10.).

For our purpose here, we consider the case $m = 1$, for which it can be shown (Problem 1.12) that when $N_t$ is discrete white noise, $\gamma_k$ is given by

$\gamma_k = \frac{A_1^2}{2}\cos 2\pi f_1 k, \quad k \neq 0$  $(4.11)$
$= \frac{A_1^2}{2} + \sigma_N^2, \quad k = 0.$

Thus, $\rho_k$ is given by

$\rho_k = \frac{(A_1^2/2)\cos 2\pi f_1 k}{(A_1^2/2)+\sigma_N^2}, \quad k \neq 0$
$= 1, \quad k = 0.$

Since $H_t$ and $N_t$ are uncorrelated, it follows that the spectrum is given by

$P_Y(f) = \frac{A_1^2}{4}\big(\Delta(f - f_1) + \Delta(f + f_1)\big) + \sigma_N^2,$

and the spectral density is
$S_Y(f) = \frac{(A_1^2/4)(\Delta(f - f_1) + \Delta(f + f_1)) + \sigma_N^2}{A_1^2/2 + \sigma_N^2}.$

A realization from the model