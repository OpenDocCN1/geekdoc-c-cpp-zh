process. Cheng (1999) shows that stationary univariate Gaussian processes are always time reversible and that non-Gaussian general linear stationary processes are time reversible if the first two moments exist. Thus, for a given set of data for which the AR(p) model in Equation 7.15 is appropriate, we could just as well consider the “backward” or “reverse” AR(p) model

$$X_t = \phi_1 X_{t+1} + \cdots + \phi_p X_{t+p} + \delta_t,\qquad (7.16)$$

where $\delta_t$ is white noise with zero mean and variance $\sigma_a^2$ and $t = 0, \pm 1, \dots$ The standard AR(p) model specifies the outcome at time $t$ in terms of the $p$ preceding time values plus a random noise component. The autocorrelations between $X_t$ and $X_{t-1}, \dots, X_{t-p}$ are the same autocorrelations that exist between $X_t$ and $X_{t+1}, \dots, X_{t+p}$ in the model of Equation 7.16.

From the model in Equation 7.16, we obtain the $n - p$ “regression” equations

$$\begin{aligned}
X_1 &= \phi_1 X_2 + \cdots + \phi_p X_{p+1} + \delta_1 \\
X_2 &= \phi_1 X_3 + \cdots + \phi_p X_{p+2} + \delta_2 \\
&\vdots \\
X_{n-p} &= \phi_1 X_{n-p+1} + \cdots + \phi_p X_n + \delta_{n-p},
\end{aligned}\qquad (7.17)$$

Instead of minimizing the sum of squares $S_c = \sum_{t=p+1}^n a_t^2$, consider estimating the parameters of the model by minimizing the forward and backward sum of squares (FBSS)

$$\text{FBSS}= \sum_{t=p+1}^n a_t^2 + \sum_{t=1}^{n-p} \delta_t^2.\qquad (7.18)$$

The Durbin–Levinson algorithm can be used to compute the $\hat{\phi}_i$, so that the FBSS is minimized and at the same time guarantees that the resulting model is stationary. This result is due to Burg (1975), and the resulting estimates are referred to as the *maximum entropy* or Burg estimates. Explicitly, the Burg algorithm is as follows, where the input data ($x_j$ in the algorithm) have been mean corrected.

*Initialization:*
Let