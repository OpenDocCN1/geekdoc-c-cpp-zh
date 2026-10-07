# Overdispersion Models in SAS

```
$$\hat{\phi} = \max\left(r, \text{trace} \left[ \hat{\Omega} \left[ \sum_{i=1}^m \hat{D}_i^T \hat{\Sigma}_i^{-1} \mathbf{e}_i \hat{D}_i \right] \right] \right), 0 \leq r \leq 1.\$$
```

The factor $c = \frac{m-1}{m-k}\frac{m}{m-1}$ should provide additional reduction to the small bias associated with the empirical covariance estimate, and the default value $\frac{m}{m-k}$ if "subject"

(cluster) contains a single record of data. In this case, the factor $\frac{m}{m-k}$ represents the degrees of freedom correction applied to the residual mean squares for ordinary least squares in which k parameters are estimated.

The formula for $\hat{\delta}_m$ given above is a generalization of the corresponding formula from Morel (1989); it allows the user to bound $\hat{\delta}_m$ from above by $\frac{1}{d}$. The default value is 2, which corresponds to an upper bound of 0.5. The choice $d=1$ implies $\hat{\delta}_m=1$ whenever $m \leq 2k$. In this case the classical sandwich is "inflated additively" by $\hat{\phi}$.

The quantity

```
$$\text{trace} \left[ \hat{\Omega} \left[ \sum_{i=1}^m \hat{D}_i^T \hat{\Sigma}_i^{-1} \mathbf{e}_i \hat{D}_i \right] \right] / k$$
```

is the average of the "Generalized Designs Effects" (see Rao and Scott, 1981). In quasi-likelihood theory this is an estimator of the stable constant needed to inflate or deflate the "naïve" covariance estimate. Note

```
$$\text{trace} \left[ \hat{\Omega} \left[ \sum_{i=1}^m \hat{D}_i^T \hat{\Sigma}_i^{-1} \mathbf{e}_i \hat{D}_i \right] \right] > 0.$$$$
```

User might choose $r$ such that $0 \leq r \leq 1$. Default value is $r=1$, which is a natural lower bound of $\phi$ assuring always inflation of the sandwich. This corresponds to the common case of overdispersion where the design effect is greater than one. In case the user suspects underdispersion, $r$ should be smaller than 1 so that the inflation is less pronounced. By taking $r$ positive, the user enforces a minimum amount of correction. The choice $r=0$ implies that no restriction on the lower bound of $\phi$ has been imposed,

Morel, Jorge, and Nagarajeraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.