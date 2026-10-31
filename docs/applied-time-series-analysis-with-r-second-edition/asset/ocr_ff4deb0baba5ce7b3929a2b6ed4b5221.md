better estimated with \hat{γ}_k than \tilde{γ}_k. Ergodic results for \hat{γ}_k (and for \tilde{γ}_k because of their asymptotic equivalence) can also be obtained, but they are in general not of the straightforward nature of Theorem 1.2. Most of the results for \hat{γ}_k are proved for the case in which μ is assumed to be known and, without loss of generality, equal to zero. For a discussion of ergodic theorems for \hat{γ}_k and for some results concerning Var(\hat{γ}_k) and Cov(\hat{γ}_k, \hat{γ}_j), see Priestley (1981). In the remainder of this book, we assume that the necessary conditions hold for the sample autocovariances to be ergodic for γ_k.

![](bbox=[0.18, 0.35, 0.65, 0.6])

# FIGURE 1.8

Theoretical and sample autocovariances based on the realization in Figure 1.5.

# 1.4.3 Estimation of ρ_k

The natural estimator of ρ_k = γ_k / γ_0 is \hat{ρ}_k = \hat{γ}_k / \hat{γ}_0, which we will henceforth refer to as the sample autocorrelation function. The estimator \hat{ρ}_k has the desirable property that |\hat{ρ}_k| ≤ 1, a property that \tilde{ρ}_k = \tilde{γ}_k / \tilde{γ}_0 does not possess. This property can be shown by relating \hat{ρ}_k to the Pearson product-moment correlation coefficient between the two sets of n + k observations

0, 0, ... 0, X_1 - \bar{X}, X_2 - \bar{X}, ... X_n - \bar{X}
X_1 - \bar{X}, X_2 - \bar{X}, ... X_n - \bar{X}, 0, 0, ... 0,

where, in each case, there are k zeros. For notational convenience, we will