Resulting in:

M = τΣ − τΣP^T(PτΣP^T + Ω)^{-1}PτΣ
= τΣ − τΣP^T(PτΣP^T + P(τΣ)P^T)^{-1}PτΣ
= τΣ − τΣP^T(2PτΣP^T)^{-1}PτΣ
= τΣ − (1/2)τΣ(P^T)^{-1}(P^T)^{-1}(τΣ)^{-1}(P)^{-1}(P)(τΣ)
= τΣ − (1/2)τΣ
(3.113)

namely,

M = (1/2) τ Σ
(3.117)

Note that τ is not eliminated from (3.117). One may also observe that if τ is on the order of 1, and if one were to use the equation

Σ_p = Σ + M
(3.107)

then the uncertainty in the estimate of the mean would be a significant portion of the variance of the returns. With the Alternate Reference Model, no posterior variance computations are preformed and the mixing is weighted by the variance of returns.

In both cases, the choice for Ω has evenly weighted the prior and conditional distributions in the estimation of the posterior distribution. This matches the intuition when one considers one has blended two inputs, for both of which one has the same level of uncertainty. The posterior distribution will be the average of the two distributions. If instead one solves for the more useful general case of

Ω = α P(τ Σ) P^T
(3.118)
where α ≥ 0, substituting into (3.105) and following the same logic as used to derive (3.117) one obtains
Π̄ = Π + 1/(1 + α)[P^{-1} Q − Π]
(3.119)
This parameterization of the uncertainty is specified in Meucci (2005) and it allows us an option between using the same uncertainty for the prior and views, and having to specify a separate and unique uncertainty for each view. Given that one is essentially multiplying the prior covariance matrix by a constant, this parameterization of the uncertainty of the views does not have a negative impact on the stability of the results.
Note that this specification of the uncertainty in the views changes the assumption from the views being uncorrelated to the views having the same correlations as the prior returns.
In summary, if the investor uses the Alternative Reference Model and makes Ω proportional to Σ, then it is necessary only to calibrate the constant of proportionality, α, which indicates their relative confidence in their views versus