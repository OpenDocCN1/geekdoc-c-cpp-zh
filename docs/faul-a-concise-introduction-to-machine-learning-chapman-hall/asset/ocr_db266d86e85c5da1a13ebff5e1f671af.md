For infinite $\alpha_i$, we have $q_i = Q_i$ and $s_i = S_i$, since in this case $\mathbf{C} = \mathbf{C}_{-i}$. While for finite $\alpha_i$,

```
$s_i = \mathbf{d}_i^T \mathbf{C}_{-i}^{-1} \mathbf{d}_i = \mathbf{d}_i^T (\mathbf{C} + \mathbf{d}_i(-\alpha_i)^{-1} \mathbf{d}_i^T)^{-1} \mathbf{d}_i$
$= \mathbf{d}_i^T [\mathbf{C}^{-1} - \mathbf{C}^{-1} \mathbf{d}_i (-\alpha_i + \mathbf{d}_i^T \mathbf{C}^{-1} \mathbf{d}_i)^{-1} \mathbf{d}_i^T \mathbf{C}^{-1}] \mathbf{d}_i$
$= S_i + \frac{S_i^2}{\alpha_i - S_i} = \frac{\alpha_i S_i}{\alpha_i - S_i}.$
```

Similarly,

```
$q_i = \frac{\alpha_i Q_i}{\alpha_i - S_i}.$
```

Let's examine $Q_i$ more closely. The matrices $\Sigma$ and $\mathbf{C}$ are related by the Woodbury matrix identity in Appendix A.1.3,

```
$\mathbf{C}^{-1} = (\sigma^2 \mathbf{I} + \mathbf{D} \mathbf{A}^{-1} \mathbf{D}^T)^{-1}$
$= \sigma^{-2} \mathbf{I} - \sigma^{-2} \mathbf{D} (\mathbf{A} + \mathbf{D}^T \sigma^{-2} \mathbf{D})^{-1} \mathbf{D}^T \sigma^{-2}$
$= \sigma^{-2} (\mathbf{I} - \sigma^{-2} \mathbf{D} \Sigma \mathbf{D}^T).$
```

Using this and (8.7),

```
$\mathbf{C}^{-1} \mathbf{t} = \sigma^{-2} (\mathbf{t} - \mathbf{D} \mu).$
```

However, $\mathbf{D}\mu$ is exactly the mean of our predictive probability distribution for $\mathbf{t}$. Thus, $\mathbf{C}^{-1} \mathbf{t}$ gives the difference between the target and the predictive mean for each sample scaled by the noise variance. If this is small, our current model is adequate to explain the data. If not, we consider $\mathbf{C}^{-1} \mathbf{t}$ an error which needs to be removed. Calculating $Q_i = \mathbf{d}_i^T \mathbf{C}^{-1} \mathbf{t}$ checks how well aligned $\mathbf{d}_i$ is with this error. If it is orthogonal, than $\mathbf{d}_i$ will not help in removing this error. If it is well aligned, then the inclusion of $\mathbf{d}_i$ in the model will be beneficial. Therefore $Q_i$ is known as the *quality factor*.

$S_i$ on the other hand is known as the sparsity factor, since, as we will see below, it helps to evaluate how collinear $\mathbf{d}_i$ is to the other basis functions. The quantities $s_i$ is a penalty term associated with the basis functions $d_i$. It quantifies how well $d_i$ could be modeled by the other basis functions. On the other hand, $q_i$ is a quality term, measuring how well $d_i$ would contribute to explaining the data, given the current model. Both $s_i$ and $q_i$ depend on $\mathbf{C}_{-i}$ which in turn depends on $\alpha_{-i}$. Thus the optimal value for $\alpha_i$ changes as the other hyperparameters $\alpha_{-i}$ are adjusted.

The possibility to optimize the hyperparameters individually in turn gives rise to the following algorithm. It initializes the model with a single basis function and its optimal hyperparameter value, and sets the hyper-parameters of the others notably to infinity. At the start of the algorithm when only one basis function is in the model, $\mathbf{D}$ has only one column, and $\Sigma$ is a $1 \times 1$ matrix. $\mathbf{C}$ is $\sigma^2 \mathbf{I}$ plus the outer product of that single basis function evaluated at the sample points with itself. Its inverse is easily calculated using the Sherman-Morrison formula from Appendix A.1.4. Then the basis function $d_i(\mathbf{x})$, where