or

w = Π(δΣ)^{-1}  (3.86c)

As a first test of the algorithm, one verifies that when the investor has no views that the weights are correct, substituting (3.109) into (3.86b)

Σ_p = (1 + τ)Σ  (3.109)

one obtains

w_nv = Π[δ(1 + τ)Σ]^{-1}
= Π(δΣ)^{-1} / (1 + τ)

or

w_nv = w/(1 + τ)  (3.121)

Hence, it is clear that the output weights with no views will be impacted by the choice of τ when the Black-Litterman reference model is used. He and Litterman (1999) indicate that if the investor is a Bayesian, then one shall not be certain of the prior distribution and thus would not be fully invested in the risky portfolio in the beginning. This is consistent with (3.121).

# Matching the Results of He and Litterman

First one shall consider the results shown in He and Litterman (1999). These results are easy to reproduce as they clearly implement the Canonical Reference Model and they provide all the data required to reproduce their results in the paper.

He and Litterman (1999) set

Ω = diag[P^T (τΣ)P]  (3.122)

This makes the uncertainty of the views equivalent to the uncertainty of the Equilibrium estimates. A small value for τ, 0.05, was selected, and the Canonical Reference Model was used. The updated posterior variance of returns is calculated in (3.113) and (3.107).

The results of Table 3.5 correspond to Table 7 in (He and Litterman, 1999). Figures 3.30 and 3.31 show the pdf for the prior, view, and posterior for each view defined in the problem. The y-axis uses the same scale in each graph. Note how in Figure 3.27 the conditional distribution of the estimated mean is much more diffuse because the variance of the estimate is larger (viz., precision of the estimate is smaller). Note how the precision of the prior and views impacts the precision (width of the peak) on the pdf. In Figure 3.27 with the less precise view, the posterior is also less precise.

# Matching the Results of Idzorek

This section reproduces the results of Idzorek (2005). In trying to match Idzorek’s results, it is found that Idzorek used the