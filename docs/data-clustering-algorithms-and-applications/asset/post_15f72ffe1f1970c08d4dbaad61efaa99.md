
# TABLE 22.1: Contingency Table Explaining Similarity Measurement of Clustering Solutions

| | $C_1^{(b)}$ | $C_2^{(b)}$ | ... | $C_k^{(b)}$ | sum |
|---|---|---|---|---||
| $C_1^{(a)}$ | $n_{11}$ | $n_{12}$ | ... | $n_{1k}^{(b)}$ | $n_1^{(a)}$ |
| $C_2^{(a)}$ | $n_{21}$ | $n_{22}$ | ... | $n_{2k}^{(b)}$ | $n_2^{(a)}$ |
| ... | ... | ... | ... | ... | ... |
| $C_k^{(a)}$ | $n_{k1}^{(b)}$ | $n_{k2}^{(b)}$ | ... | $n_{kk}^{(b)}$ | $n_k^{(a)}$ |
| sum | $n_1$ | $n_2$ | ... | $n_k^{(b)}$ | $n$ |

The Adjusted Rand Index (ARI) to correct for a zero baseline. ARI, according to the general strategy of correcting for chance, is defined as follows:

```
$$\phi^{(ARI)}(\lambda^{(a)}, \lambda^{(b)}) = \frac{\sum_{h} \frac{n_{hl}}{2} - S_a S_b}{\frac{n}{2} - S_a S_b} = \frac{\sum (S_a + S_b) - S_a S_b}{\frac{n}{2}}$$ (22.5)
```

where $S_a = \sum \frac{n_h^{(a)}}{2}$ and $S_b = \sum \frac{n_h^{(b)}}{2}$. The second term in numerator and denominator adjusts for the expected number of overlaps that occur "by chance". Values of RI between 0 and 1. However, ARI can be negative, which is of no practical interest. ARI is 1 when the two candidate clustering solutions match exactly and is 0 when the index exceeds its expected value.

In [4], the authors mention any as 22 different indices of this class. Subsequent work [66] shows that after correction for chance, some of these indices become equivalent. ARI remains the most popular index of this class. Very recently, a probabilistic version of Rand Index (PRI) [11] has been proposed in which the agreements and disagreements of pairs of data points are weighted according to their chance.

## 2. Information Theoretical-Based Measures: We present information theory-based measures in the literature [50]. We discuss two of them and show how they can be corrected by chance.

### (a) Normalized Mutual Information (NMI)

Strehl and Ghosh [56] propose NMI to measure the similarity between two candidate clusterings. The entropy associated with clustering $\lambda^{(a)}$ is $H(\lambda^{(a)}) = -\sum \frac{n_h^{(a)}}{n} \log(\frac{n_h^{(a)}}{n})$ and with clustering $\lambda^{(b)}$ is $H(\lambda^{(b)}) = -\sum \frac{n_h^{(b)}}{n} \log(\frac{n_h^{(b)}}{n})$. Similarly, the joint entropy of $\lambda^{(a)}$ and $\lambda^{(b)}$ is defined as $H(\lambda^{(a)}, \lambda^{(b)}) = -\sum \frac{n_{ij}}{n} \log(\frac{n_{ij}}{n})$. Now, NMI between $\lambda^{(a)}$ and $\lambda^{(b)}$ is defined as

```
$$\phi^{(NMI)}(\lambda^{(a)}, \lambda^{(b)}) = \frac{I(\lambda^{(a)}, \lambda^{(b)})}{\sqrt{H(\lambda^{(a)})H(\lambda^{(b)})}} $$ (22.6)
```

Here, $I(\lambda^{(a)}, \lambda^{(b)}) = H(\lambda^{(a)}) + H(\lambda^{(b)}) - H(\lambda^{(a)}, \lambda^{(b)})$ is the mutual information between two clusterings $\lambda^{(a)}$ and $\lambda^{(b)}$ [77], which is normalized by the geometric mean of $H(\lambda^{(a)})$ and $H(\lambda^{(b)})$ to compute the NMI. It should be noted that $I(\lambda^{(a)}, \lambda^{(b)})$ is non-negative and has no upper bound. $\Phi^{(NMI)}(\lambda^{(a)}, \lambda^{(b)})$, on the other hand, lies between 0 and 1 and is suitable for easier interpretation and comparisons.

## VI Variation of Information (VI)

VI is another information-theoretic distance measure proposed for cluster validation [44, 45] and is defined as follows:

```
$$\Phi^{(VI)}(\lambda^{(a)}, \lambda^{(b)}) = H(\lambda^{(a)}) + H(\lambda^{(b)}) - 2I(\lambda^{(a)}, \lambda^{(b)})$$
```

It turns out that VI is a metric. Its original definition is not consistent if data sets of different sizes and clusters with different number of clusters are considered. Therefore, several normalized versions of VI have been proposed. The one proposed by [37] takes the following form:

```
$$\Phi^{(NVI)}(\lambda^{(a)}, \lambda^{(b)}) = 1 - \frac{I(\lambda^{(a)}, \lambda^{(b)})}{max(H(\lambda^{(a)}), H(\lambda^{(b)}))}$$
```

which is again metric. However, the one proposed by Wu et al. [68] is not a metric and takes the following form:

```
$$\Phi^{(NVI)}(\lambda^{(a)}, \lambda^{(b)}) = 1 - \frac{2I(\lambda^{(a)}, \lambda^{(b)})}{H(\lambda^{(a)}) + H(\lambda^{(b)})}$$
```

Both of these measures lie between 0 and 1. Note that one could also define a distance measure from NMI using its complement. However, such distance measure is not metric. Vinh et al. [50] empirically showed that RI does not attain any constant baseline. The problem is more severe when the number of clusters is comparable to the number of data points. With increase in the number of clusters, the expected values of the indices either increase (for NMI) or decrease (for VI). Therefore, if one needs to make a decision based on the observed values of the indices, on average, a clustering solution with more (or fewer for VI) clusters will be preferred.

Therefore, following the generalized suggestion for correction given in Equation 22, Vinh et al. [50] proposed to correct these measures with the expected value of mutual information of the solutions and empirically showed the invariance of the measure w.r.t the number of clusters. The expression for the expected value of mutual information under the permutation is given:

```
$$\E[I(S_a, S_b)] = \sum_{h_a=min(n_a, n_b)}^{maxmax(n_a, n_b)} \frac{n_h}{n} \log(\frac{n_h}{n})$$
```

However, if the ratio of the number of data points and the number of clusters is more than 100 for both solutions, empirical studies show that $\E[I(S_a, S_b)]$ is close to zero, hence no adjustment for chance is necessary. Unfortunately, with such adjustment, none of the distances is a metric. Therefore, depending on the applications, one needs to make a choice between the metric property and the zero baseline.

## 2.4.1 Probabilistic Approaches to Cluster Ensembles

The two basic probabilistic models for solving cluster ensembles are described in this subsection.

### 2.4.1.1 A Mixture Model for Cluster Ensembles (MMCE)

In a typical mixture model [10] approach to clustering, fitting the data using a mixture of Gaussians with $k$ mixture components, one each cluster. A component-specific distribution is used to model the distribution of data attributed to a specific component. Such an approach can be applied to form the consensus decision if the number of clusters is specified. This yields the pioneering approach taken in [60]. We give a bit more detail as this work is essential to build an understanding of later works [64, 65].

In the mixture model of cluster ensembles [60], each object $x_i$ is represented by $y_i = L(x_i)$, i.e. the labels provided by the base clusters. We assume that there are $k$ clusters each $\ell$ and for each clustering $q$, we have a multinomial distribution $\beta^{(q)}$ of dimension $k^{(q)}$. Therefore, a sample from this distribution is a cluster label corresponding to the $q^{th}$ cluster base. The underlying generative process is assumed as:

For $i^{th}$ point $x_i$:

- 1. Choose $z_i = \mathbf{I}_{\ell}$ such that $\ell \sim \text{multinomial}(\theta_i)$. Here $\mathbf{I}_{\ell}$ is a probability vector of dimension $k$ with only the $\ell^{th}$ component being 1, and $\theta_i$ is a multinomial distribution of dimension $k$.
- 2. For the $q^{th}$ base clustering of the $i^{th}$ point, choose the base cluster result $y_{iq} = \ell \sim \text{multinomial}(\beta^{(q)})$.

These probabilistic approaches give rise to a simple maximum log-likelihood problem that can be solved using the Expectation Maximization (EM) algorithm. This model also takes care of the missing labels in a natural way.

### 2.4.1.2 Bayesian Cluster Ensembles (BCE)

A Bayesian version of the multinomial model described above was subsequently proposed by Wang et al, [64]. As in the simple mixture model, we assume $k$ clusters with $\beta^{(q)}$ being the multinomial distribution corresponding to each cluster $\ell$ and each base clustering $q$. The complete generative process for this model is as follows:

For $i^{th}$ point $x_i$:

- 1. Choose $\theta_i \sim \text{Dirichlet}(\theta_i)$ where $\theta_i$ is a multinomial distribution of dimension $k$.
- 2. For the $q^{th}$ base clustering
  - (a) Choose $z_{iq} = \mathbf{I}_{\ell}$ such that $\ell \sim \text{multinomial}(\theta_i)$. With only the $\ell^{th}$ component being 1.
  - (b) Choose the base cluster result $y_{iq} = \ell \sim \text{multinomial}(\beta^{(q)}).
