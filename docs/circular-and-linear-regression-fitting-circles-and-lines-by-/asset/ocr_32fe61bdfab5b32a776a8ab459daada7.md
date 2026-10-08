We note that (7.30) actually gives the component of $\Delta_2\mathbf{A}$ orthogonal to $\tilde{\mathbf{A}}$, but it is exactly what we need, because we set $\|\mathbf{A}\| = 1$. We can rewrite (7.31) as

where, according to (7.27),

$$\begin{aligned} \mathbf{R} & = \frac{1}{n}\bigg[\Delta_1\mathbf{X}^T\Delta_1\mathbf{X} + \hat{\mathbf{X}}^T\Delta_2\mathbf{X} + \Delta_2\mathbf{X}^T\hat{\mathbf{X}} \\ & \qquad \qquad - \frac{1}{n}(\hat{\mathbf{X}}^T\Delta_1\mathbf{X} + \Delta_1\mathbf{X}^T\hat{\mathbf{X}})\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}\bigg]. \end{aligned}$$

Thus the formula for the bias becomes

$$\mathbb{E}(\Delta_2\mathbf{A}) = \hat{\mathbf{M}}^{-}\begin{bmatrix} \tilde{\mathbf{A}}^T\mathbb{E}(\mathbf{R}\tilde{\mathbf{A}}) & \tilde{\mathbf{N}}\tilde{\mathbf{A}} - \mathbb{E}(\mathbf{R}\tilde{\mathbf{A}}) \\ \tilde{\mathbf{A}}^T\tilde{\mathbf{N}}\tilde{\mathbf{A}} \end{bmatrix} + \mathcal{O}(\sigma^4).$$

Next we find the mean value of (7.32), term by term. First,

$$\begin{aligned} \frac{1}{n}\mathbb{E}(\Delta_1\mathbf{X}^T\Delta_1\mathbf{X}) & = \frac{1}{n}\mathbb{E}\Big(\sum_i(\Delta_1\mathbf{X}_i)(\Delta_1\mathbf{X}_i)^T\Big) = \frac{\sigma^2}{n}\sum_i\tilde{\mathbf{T}}_i = \boldsymbol{\sigma}^2\tilde{\mathbf{T}}. \end{aligned}$$

Second, since $\mathbb{E}(\Delta_2\mathbf{X}_i) = (2\sigma^2, 0, 0, 0)^T$, we obtain

$$\begin{aligned} \frac{1}{n}\mathbb{E}(\hat{\mathbf{X}}^T\Delta_2\mathbf{X} + \Delta_2\mathbf{X}^T\hat{\mathbf{X}}) & = \frac{2\sigma^2}{n}\sum_i \begin{bmatrix} 2\tilde{z}_i & \tilde{x}_i & \tilde{y}_i & 1 \\ \tilde{x}_i & 0 & 0 & 0 \\ \tilde{y}_i & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 \end{bmatrix} = \boldsymbol{\sigma}^2(\tilde{\mathbf{T}} - \mathbf{P}). \end{aligned}$$

The above two terms combined constitute the essential bias, i.e.,

$$\mathbb{E}(\Delta_2\mathbf{A}) \overset{\mathrm{ess}}{=} \boldsymbol{\sigma}^2\hat{\mathbf{M}}^{-}\begin{bmatrix} \frac{\tilde{\mathbf{A}}^T(2\tilde{\mathbf{T}}-\mathbf{P})\tilde{\mathbf{A}}}{\tilde{\mathbf{A}}^T\tilde{\mathbf{N}}\tilde{\mathbf{A}}} & \tilde{\mathbf{N}}\tilde{\mathbf{A}} - (2\tilde{\mathbf{T}}-\mathbf{P})\tilde{\mathbf{A}} \end{bmatrix}.$$ 

**The entire $\mathcal{O}(\sigma^2)$ bias.** We continue computing the mean value of (7.32):

$$\begin{aligned} \mathbb{E}(\hat{\mathbf{X}}^T\Delta_1\mathbf{X}\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}) & = \sum_i\mathbb{E}(\hat{\mathbf{X}}_i\Delta_1\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}_i\Delta_1\mathbf{X}_i^T) \ & = \sum_i\mathbb{E}(\hat{\mathbf{X}}_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\Delta_1\mathbf{X}_i\Delta_1\mathbf{X}_i^T) \ & = \boldsymbol{\sigma}^2\sum_i\hat{\mathbf{X}}_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\tilde{\mathbf{T}}_i. \end{aligned}$$

Similarly, we have

$$\mathbb{E}(\Delta_1\mathbf{X}^T\hat{\mathbf{X}}\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}) = \boldsymbol{\sigma}^2\sum_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}_i\tilde{\mathbf{T}}_i.$$