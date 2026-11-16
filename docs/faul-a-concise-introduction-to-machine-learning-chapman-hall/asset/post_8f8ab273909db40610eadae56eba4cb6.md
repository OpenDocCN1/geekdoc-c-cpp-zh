
```
function [V,idx,MU,SIGMA] = BayesianMixture(N,K,alpha,mu0,...
    lambda,Psi,nu)
% Input:
% N:   number of data points to be generated,
% K:   number of clusters
% alpha: concentration parameter,
% mu0: location vector,
% lambda: mean fraction,
% Psi:   Inverse scale matrix,
% nu:    degrees of freedom,
% Output:
% V:   data vector,
% idx: index vector which process generated the sample,
% MU:  array of the means of all processes,
% SIGMA: array of the covariance matrices of all processes.
% Generate vector of mixture coefficients from Dirichlet
% distribution given by alpha and K using the Gamma distribution.
a = alpha/K*ones(1,K);
PI = gamrnd(a,1);
PI = PI/sum(PI);
% Generate latent indicator variable for cluster membership.
idx = randsample(K,N,true,PI);
% Generate distribution for each cluster.
SIGMA = zeros(2,2,K);
MU = zeros(2,K);
for k=1:K
    sigma = iwishrnd(Psi,nu);
    SIGMA(:,:,k) = sigma;
    MU(:,k) = mvnrnd(mu0,sigma/lambda);
end
% Generate data.
V = zeros(N,2);
for n=1:N
    v = mvnrnd(MU(:,idx(n)),SIGMA(:,:,idx(n)));
    V(n,:) = v;
end
```

Listing 6.4: Generating data from a distribution of distributions for a fixed number of clusters.

This can be viewed without involving the latent variables z_n. Imagine a distribution G over the set of all possible pairs of (μ, Σ) which can be generated from G_0. Since there is only a finite number of clusters, G is zero everywhere apart from the specific pairs (μ_k, Σ_k) where it has a point probability mass of π_k.

Using this distribution G, the generation of data can be described as:

```
\mathbf{v}_n \sim \mathcal{N}(\mu_k, \Sigma_k)
\pi \sim \text{Dir}(\alpha),
\mu_k, \Sigma_k \sim G.
```

The base distribution G_0 is indirectly part of the distribution G, since the points where G is nonzero are drawn from G_0, while the probability masses at these points are drawn from Dir(α).

Having explored the way the data is generated, we now look at inferring the cluster membership from the data. First, let D = {v_1, ..., v_N} be a set of data samples drawn from a multivariate normal distribution with mean μ and covariance matrix Σ, where μ and Σ are themselves drawn from a normal inverse Wishart distribution. We assume a prior normal inverse Wishart distribution with parameters m, λ, Ψ and ν. The posterior is also a normal inverse Wishart distribution. Let

```
\bar{\mathbf{v}} = \frac{1}{N} \sum_{n=1}^N \mathbf{v}_n
```

be the sample mean and

```
\mathbf{S} = \sum_{n=1}^N (\mathbf{v}_n - \bar{\mathbf{v}})(\mathbf{v}_n - \bar{\mathbf{v}})^T
```

the scaled sample covariance matrix. The posterior then has parameters

```
\mathbf{m}^{\text{post}} = \frac{\lambda \mathbf{m} + N \bar{\mathbf{v}}}{\lambda + N},
\lambda^{\text{post}} = \lambda + N,
\nu^{\text{post}} = \nu + N,
\Psi^{\text{post}} = \Psi + \mathbf{S} + \frac{\lambda N}{\lambda + N}(\bar{\mathbf{v}} - \mathbf{m})(\bar{\mathbf{v}} - \mathbf{m})^T.
```

In particular, if N = 1, we have one single data point v and \bar{v} = v and S = 0. With this,

```
\mathbf{m}^{\text{post}} = \frac{\lambda \mathbf{m} + \mathbf{v}}{\lambda + 1},
\lambda^{\text{post}} = \lambda + 1,
\nu^{\text{post}} = \nu + 1,
\Psi^{\text{post}} = \Psi + \frac{\lambda}{\lambda + 1}(\mathbf{v} - \mathbf{m})(\mathbf{v} - \mathbf{m})^T. \tag{6.11}
```

Thus the data samples can be considered one at a time and the posterior is calculated sequentially.

However, the above does not consider the probabilities of a sample belonging to a particular cluster which are governed by a Dirichlet prior distribution with parameter \(\alpha = (\alpha/K, \dots, \alpha/K)^T\). We start with a random assignment of the indicator variables \(\mathbf{z}_1, \dots, \mathbf{z}_N\). For each individual cluster \(k\), we let \(N_k\) be the number of samples in it with this particular assignment. We then calculate the parameters \(\mathbf{m}_k, \lambda_k, \Psi_k\) and \(\nu_k\) of the posterior, normal, inverse Wishart distribution for each cluster and draw \(\mu_k\) and \(\Sigma_k\) from this distribution.

Gibbs sampling is used to reassign samples to clusters in a random order. To this end, a random sample \(\mathbf{v}_n\) is selected. Let \(l\) be its current cluster assignment. Consider the data set without this sample, \(\mathcal{D} \setminus \{\mathbf{v}_n\}\). It needs to be removed from cluster \(l\) by returning to the prior parameters of the normal, inverse Wishart distribution for the \(l^{th}\) cluster. Using (6.11) backwards, we see that

```
\begin{aligned}
\mathbf{m}_l^{\text{prior}} &= \frac{\lambda_l \mathbf{m}_l - \mathbf{v}_n}{\lambda_l - 1}, \\
\lambda_l^{\text{prior}} &= \lambda_l - 1, \\
\nu_l^{\text{prior}} &= \nu_l - 1, \\
\Psi_l^{\text{prior}} &= \Psi_l - \frac{\lambda_l}{\lambda_l - 1}(\mathbf{v}_n - \mathbf{m}_l)(\mathbf{v}_n - \mathbf{m}_l)^T.
\end{aligned}
```

Note that this is independent of the order, in which samples were assigned clusters. A new mean \(\mu_l\) and covariance matrix \(\Sigma_l\) are drawn from this distribution, and \(N_l\) is replaced by \(N_l - 1\).

We calculate for \(k = 1, \dots, K\) the probabilities that \(\mathbf{v}_n\) belongs to cluster \(k\) given all the other data samples and their assignments,

```
\begin{aligned}
p(z_{n,k} = 1 | \mathbf{v}_n, \mathcal{D} \setminus \{\mathbf{v}_n\}, \alpha, \mathbf{m}, \lambda, \Psi, \nu) = \\
p(z_{n,k} = 1 | \mathcal{D} \setminus \{\mathbf{v}_n\}, \alpha) p(\mathbf{v}_n | \mathcal{D} \setminus \{\mathbf{v}_n\}, z_{n,k} = 1, \mathbf{m}, \lambda, \Psi, \nu)
\end{aligned}
```

following the product rule. Here \(\mathcal{D} \setminus \{\mathbf{v}_n\}\) means the set of samples as well as their assignments.

The first factor is the probability of \(\mathbf{v}_n\) belonging to cluster \(k\) which is governed by the posterior Dirichlet distribution, given the prior Dirichlet distribution and all other cluster assignments. From the discussion about conjugate distributions leading to equation (6.23), this is

```
\(\frac{N_k + \alpha/K}{N - 1 + \alpha}.\)
```

The second factor in (6.12) is the likelihood of seeing sample \(\mathbf{v}_n\) given \(\mathcal{D} \setminus \{\mathbf{v}_n\}, z_{n,k} = 1\), and the parameters of the posterior, normal, inverse Wishart distribution for this cluster. This is approximated by the normal distribution with mean \(\mu_k\) and covariance matrix \(\Sigma_k\). Hence, \(p(\mathbf{v}_n | \mathcal{D} \setminus \{\mathbf{v}_n\}, z_{n,k} = 1, \mathbf{m}, \lambda, \Psi, \nu)\) is approximately

```
\(\frac{1}{\sqrt{|2\pi \Sigma_k|}} \exp \left( -\frac{1}{2} (\mathbf{v}_n - \mu_k)^T \Sigma_k^{-1} (\mathbf{v}_n - \mu_k) \right)\)
```

```
function [idx,MU, SIGMA] = InferBayesianMixture(V, K, alpha, m,...
lambda, Psi, nu, iter)
% Input:
% V: data
% K: number of clusters
% alpha: prior concentration parameter,
% m: prior location vector,
% lambda: prior mean fraction,
% Psi: prior inverse scale matrix,
% nu: prior degrees of freedom,
% iter: number of iterations
% Output:
% idx: index vector of cluster assignments,
% MU: array of the means sampled from the posterior normal
% Wishart distributions for each cluster,
% SIGMA: array of the inverse Wishart distributions sampled from the posterior
% normal inverse Wishart distributions for each cluster.
%
N = size(V,1);
% Start with random cluster assignments.
idx = randi([1,K],N);
% For each cluster store its size, posterior location vector,
% posterior mean fraction, posterior inverse scale matrix,
% degrees of freedom.
nk = zeros(1,K);
M = zeros(2,K);
LAMBDA = zeros(1,K);
PSI = zeros(2,2,K);
NU = zeros(1,K);
% For each cluster store a draw from the posterior normal,
% inverse Wishart distribution.
SIGMA = zeros(2,2,K);
MU = zeros(2,K);
% For each cluster initialize these for the initial random cluster
% assignments and draw MU and SIGMA from that posterior normal,
% inverse Wishart distribution.
for k=1:K
    v = V(idx == k,:);
    nk(k) = size(v,1);
    sampleM = mean(v);
    sampleS = (nk(k)-1) * cov(v);
    M(:,k) = (lambda*m(:,1) + nk(k)*sampleM(:))/(lambda + nk(k));
    LAMBDA(k) = lambda + nk(k);
    PSI(:,:,k) = sampleS + ...
    lambda*nk(k)*(sampleM - m(:,1))'*(sampleM - m(:,1)) ...
    % Store Cholesky factorization to maintain positive definiteness.
    PSI(:,:,k) = chol(PSI);
    NU(k) = nu + nk(k);
    SIGMA(:,:,k) = iwishrnd(PSI(:,:,k) * PSI(:,:,k), NU(k));
    MU(:,k) = mvnrnd(M(:,k),SIGMA(:,:,k)/LAMBDA(k));
end
```

6.5a: Bayes' rule and Gibbs sampling determining the mixture model for a fixed number of clusters - initialization.
