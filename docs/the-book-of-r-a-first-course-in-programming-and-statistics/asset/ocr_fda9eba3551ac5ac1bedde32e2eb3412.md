# Exercise 18.6

a. For this exercise you’ll need to have written typeII.mean from Exercise 18.5 (b). Using this function, modify power.tester so that a new function, power.mean, calls typeII.mean instead of calling typeII.tester.

+   i. Confirm that the power of the test given by H₀ : μ = 10; Hₐ : μ ≠ 10, with μₐ = 10.5, σ = 0.9, α = 0.01, and n = 50, is roughly 88 percent.

+   ii. Remember the hypothesis test in Section 18.2.1 for the mean net weight of an 80-gram pack of snacks, based on the n = 44 observations provided in the snack vector. The hypotheses were as follows:

H₀ : μ = 80
Hₐ : μ < 80

If the true mean is μₐ = 78.5 g and the true standard deviation of the weights is σ = 3.1 g, use power.mean to determine whether the test is statistically powerful, assuming α = 0.05. Does your answer to this change if α = 0.01?

b. Staying with the snacks hypothesis test, using the sample.sizes vector from the text, determine the minimum sample size required for a statistically powerful test using both α = 0.05 and α = 0.01. Produce a plot showing the two power curves.

# Important Code in This Chapter

| Function/operator | Brief description | First occurrence |
|---|---|---|
| t.test | One- and two-sample t-test | Section 18.2.1, p. 391 |
| prop.test | One- and two-sample Z-test | Section 18.3.1, p. 405 |
| pchisq | χ² cumulative problems | Section 18.4.1, p. 414 |
| chisq.test | χ² test of distribution/independence | Section 18.4.1, p. 414 |
| rowSums | Matrix row totals | Section 18.4.2, p. 417 |
| colSums | Matrix column totals | Section 18.4.2, p. 417 |