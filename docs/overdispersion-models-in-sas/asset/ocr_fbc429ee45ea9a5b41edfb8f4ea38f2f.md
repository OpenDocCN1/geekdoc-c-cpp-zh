# Chapter 10 Generalized Lineardispersion Mixed Models 339

The extension of GLM to GLMM is straightforward and is analogous to the extension of linear models to linear mixed models. A random effect is introduced, corresponding to each subject to capture the deviation of the subject's response from the group average. We consider only the simplified case of subjects treated as random. Real-life examples might be more complex. In instance, a k-dimensional multi-center study where subjects within centers provide repeated measurements over time, it would be reasonable to treat “centers” and “subjects within centers” as random.

We will first present the GLMM in a very general set for multivariate observations from elemental units clusters. Clusters are here used as a generic term, and in practice represent a subject, a center, or investigator. Let $\mathbf{y}_j$ denote the $d$-dimensional response vector from the $j$-th elemental cluster, $j=1,2,\dots,n$, $j=1,2,\dots,m$; suppose mean vectors and variance-covariance matrices of these response vectors are represented as $E(\mathbf{y}_j) = \mu_j$ and $Var(\mathbf{y}_j) = \Phi(\mu_j)$, where the $i$-th component $\mu_{ij}$ of the mean vector $\mu_j$ depends on a $k$-dimensional row of known covariates $\mathbf{x}_{ij}$ and an unknown $k$-dimensional column vector of parameters $oldsymbol{eta}_j$, through a link function $g(\cdot)$ such that $g(\mu_{ij}) = \mathbf{x}_{ij}^	opoldsymbol{eta}_j$. As before, each element of the variance-covariance matrix $V(\mathbf{y}_j)$ is a known function that gives the variance of the observation in terms of the corresponding mean vector. Following the notational conventions of Chapter 7, letting $	heta$ denote the dk-dimensional vector of all the parameters, we can write this model as.

```
$$\mu_{ij} = E(\mathbf{y}_j)\n= g^{-1}(oldsymbol{eta}_j, \mathbf{x}_{ij})$\n= g^{-1}(\mathbf{x}_{ij}^	op\boldsymbol{eta}_j)$ (10.1)$
```

Now, let $\mathbf{y}_j =(\mathbf{y}_{j1}, \mathbf{y}_{j2}, \dots, \mathbf{y}_{jm})$ denote the vector of all responses from the $j$-th cluster. Note that the dimensionality of $\mathbf{y}_j$ is $m,d\times1$. The variance-covariance of the matrix of this response vector

```
$Var(\mathbf{y}_j) \equiv V_j = \Phi(\mu_j)$ (10.2)
```

which will involve the variance-covariance matrices $V(\mathbf{y}_j)$ of elemental level responses $\mathbf{y}_{jl}$ belonging to the $j$-th cluster, $\mu_j ==(\mu_{j1}, \mu_{j2}, \dots, \mu_{jm})$ is the mean vector and $\phi$ an additional scale parameter motivates. Equations (10.1) and (10.2) serve as the framework for quasi-likelihood estimation, which most a scalar adjustment to the standard errors after fitting a model, assuming that the scale parameter is one, as discussed in Chapters 3 and 7. Now let $R(\mathbf{\alpha})$ denote

Morel, and Nagaraj Neeraraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional resources, visit support.sas.com/publishing.