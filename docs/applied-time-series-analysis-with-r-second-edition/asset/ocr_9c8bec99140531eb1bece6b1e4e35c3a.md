so that $\hat{\phi}_1$ is asymptotically normal with mean $\phi_1$ and variance $\left(1 - \phi_1^2\right)/n$

2. AR(2): The matrix $\mathbf{\Gamma}$, for an AR(2), is given by

$$\mathbf{\Gamma} = \begin{bmatrix} \gamma_0 & \gamma_1 \\ \gamma_1 & \gamma_0 \end{bmatrix}, \tag{7.54}$$

where $\gamma_0$ and $\gamma_1$ are given by 3.113 and 3.114 (with $\theta_1 = 0$) as

$$\gamma_0 = \frac{(1 - \phi_2)\sigma_a^2}{(1 + \phi_2)\left((1 - \phi_2)^2 - \phi_1^2\right)}. \tag{7.55}$$ $$\gamma_1 = \frac{\phi_1\sigma_a^2}{(1 + \phi_2)\left((1 - \phi_2)^2 - \phi_1^2\right)}.$$

After some algebra, it follows that

$$\sigma_a^2 \mathbf{\Gamma}^{-1} = \begin{bmatrix} 1 - \phi_2^2 & -\phi_1(1 + \phi_2) \\ -\phi_1(1 + \phi_2) & 1 - \phi_2^2 \end{bmatrix}. \tag{7.56}$$

From Equation 7.50 and the diagonal elements of Equation 7.56, it can be seen that, asymptotically, $\hat{\phi}_1$ is distributed as a normal random variable with mean $\phi_1$ and variance $\left(1 - \phi_1^2\right)/n$, while $\hat{\phi}_2$ is asymptotically normal with mean $\phi_2$ and the same asymptotic variance as $\hat{\phi}_1$.

# 7.5.1.1 Confidence Intervals: AR Case

A common use for the result in Equation 7.50 is to compute approximate large sample confidence intervals for the parameters. From Equation 7.50, it follows that

$$\left(\hat{\phi} - \phi\right)' \frac{n\hat{\mathbf{\Gamma}}}{\hat{\sigma}_a^2} \left(\hat{\phi} - \phi\right) \Rightarrow \chi^2(p), \tag{7.57}$$