# Overdispersion Models in SAS

$m,d\timesd$ matrix, capturing the within cluster correlation structure referred to the working correlation matrix. For univariate responses, this matrix could be easily visualized for independent, exchangeable autoregressive correlation structures. However, the working correlation matrix will have much more complex blocked structure in the multivariate response case. We will simply assume that this is possible to rewrite

```
$$\mathbf{V}_j = \mathbf{V}_j(\mu_j, \alpha_j) = \phi_j \mathbf{A}_j^T \mathbf{R}(\alpha_j) \mathbf{A}_j$,
```

for $j=1,2,...,n$, where

```
$$\mathbf{A}_j = \text{Diag}\left(\mathbf{V}(y_{j1}),\mathbf{V}(y_{j2}),\dots,\mathbf{V}(y_{jd}),\dots,\mathbf{V}(y_{jn1}),\mathbf{V}(y_{jn2}),\dots,\mathbf{V}(y_{jnd})\right)\right).$$
```

Equations (10.1) and (10.3) provide a GLM in a framework that can accommodate valued responses for each element within clusters, the commonly used distributions from the exponential family, and a variety of link functions. Equations (9.20) of Chapter 9 exemplify the formulation for multinomial responses for generalized log and cumulative log links.

If the link functions are identity, then the framework reduces to the well-known multivariate linear model as given in Rao (1965, Section 85c). The linear model equation for multivariate observations is analogous to the equations stated in Chapter 9 (equation 9.5). It can be written as

```
$$\mathbf{y} = \mathbf{X\beta} + \varepsilon$,$$
```

where $\mathbf{y} = (y_1^T,y_2^T,...,y_n^T)^T$ is the vector of observations from all n clusters, and therefore of

dimension $d\sum_{j=1}^n \times X$ represents the design matrix (or the matrix of known covariates)
covariates from all clusters properly concatenated, and $\beta$ is the unknown vector of parameters. The dimensions of $\mathbf{X}$ and $\beta$ depend on the exact formulation of the model.
If different components of the multivariate response do not share any parameters, $\beta$ is a $dk$-dimensional column vector. For example, if the response is a multinomial, and the link is cumulative log so that all responses share the same set of parameters other than the intercept, then $\beta$ is $dk+1$ dimensional.

The parameters in the model equation (10.4) are fixed effects. The Mixed models are obtaining by augmenting the fixed effects with random effects. Random effects are used to capture the within-cluster correlations. They are also used to represent hierarchical nesting de the structure of the design used in the study. In general, a Linear Mixed Model (LMM) is written as

```
$$\mathbf{y} = \mathbf{X\beta} + \mathbf{Z\gamma} + \varepsilon$,$$
```