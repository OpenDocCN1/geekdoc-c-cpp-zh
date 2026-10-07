$x \exp \{-exp[\gamma_0 + \gamma_{1j} + \theta_{0k})y_{j+l+k}]^{\theta_0}\} \exp \{-\frac{1}{2}\theta_0^T \Sigma_{\theta_0} \theta_0\}, (4.13)$

where $\Sigma_{\theta_0} = \theta_0^2/K_0$ denotes a $K_0 \times K_0$ covariance matrix of $\theta_0$.

It is easy to show that the full conditional distributions in (4.11) to (4.13) are log-concave in each parameter. Then, we can implement the adaptive rejection algorithm of [15] to sample from the posterior distribution of $[\gamma, \theta, \theta_0]$. PROC MCMC in SAS also provides a Metropolis-Hastings algorithm [16] to sample from the posterior distribution of $[\gamma, \theta, \theta_0]$.