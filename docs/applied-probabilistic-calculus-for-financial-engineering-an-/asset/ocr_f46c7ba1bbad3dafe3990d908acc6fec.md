A general problem in using Bayes' theory is to identify an intuitive and tractable prior distribution. One of the core assumptions of the Black-Litterman model (and Mean-Variance optimization) is that asset returns are normally distributed. For that reason, one confines to the case of normally distributed conditional and prior distributions. Given that the inputs are normal distributions, it follows that the posterior will also be normally distributed. When the prior distribution and the posterior have the same structure, the prior is known as a conjugate prior.

Given interest, there is nothing to keep us from building variants of the Black-Litterman model using different distributions; however, the normal distribution is generally the most straightforward.

Another core assumption of the Black-Litterman model is that the variance of the prior and the conditional distributions about the actual mean are known, but the actual mean is not known. This case, known as "Unknown Mean and Known Variance," is well documented in the Bayesian literature. This matches the model that Theil uses where one has an uncertain estimate of the mean, but know the variance.

Remarks: The significant distributions are defined here below:

+   1) The prior distribution
+   
+   \(P(A) \sim N(x, S/n)\)  (3.131)
+   
+   where \(S\) is the sample variance of the distribution about the mean, with \(n\) samples, then \(S/n\) is the variance of the estimate of \(x\) about the mean.
+   
+   The conditional distribution
+   
+   \(P(B|A) \sim N(\mu, \Omega)\)  (3.132)
+   
+   where \(\Omega\) is the uncertainty in the estimate \(\mu\) of the mean, it is not the variance of the distribution about the mean.
+   
+   2) Then the posterior distribution is specified by
+   
+   \(P(A|B) \sim N\{[\Omega^{-1}\mu + nS^{-1}x][\Omega^{-1} + nS^{-1}]^{-1}, (\Omega^{-1} + nS^{-1})^{-1}\}\)  (3.133)
+   
+   3) The variance term in (3.133) is the variance of the estimated mean about the actual mean. In Bayesian statistics, the inverse of the variance is known as the precision. One may describe the posterior mean as the weighted mean of the prior and conditional means, where the weighting factor is the respective precision.
+   
+   4) Furthermore, the posterior precision is the sum of the prior and conditional precision. Equation (3.133) requires that the precision of the prior and conditional be noninfinite, and that the sum is nonzero. Infinite precision corresponds to a variance of 0, or absolute confidence.