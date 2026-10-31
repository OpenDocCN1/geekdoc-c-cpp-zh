2) An example selected from the R Package MarkovitzR, available from CRAN, is chosen. For this example, the associated R program is run, outputting the concomitant associated numerical and graphical results.

# 3.2.3.1 Markovitz MPT Using R: A Simple Example of a Portfolio Consisting of Two Risky Assets

This example introduces modern portfolio theory in a simple setting of only a single risk-free asset and two risky assets.

# A Portfolio of Two Risky Assets

Consider an investment problem in which there are two nondividend-paying stocks: Stock A and Stock B, and over the next month let

+   - R_A be the monthly simple return on the Stock A, and
+   - R_B be the monthly simple return on the Stock B.

Since these returns will not be realized until the end of each month, their returns may be treated as random variables.

Assume that the returns R_A and R_B are jointly normally distributed, and that the following information are available regarding the means, variances, and covariances of the probability distribution of the two returns:

The means μ_i, standard deviations σ_i, covariance σ_AB, and correlation coefficient ρ_AB are defined as follows:

μ_A = E[R_A]  (3.18a)
σ_A² = var(R_A)  (3.18b)
μ_B = E[R_B]  (3.19a)
σ_B² = var(R_B)  (3.19b)
σ_AB = cov(R_A, R_B)  (3.20)
ρ_AB = cor(R_A, R_B) = σ_AB/(σ_A σ_B)  (3.21)

where E is the expectation and var is the variance.

Generally, these values are estimated from historical return data for the two stocks. On the other hand, they may also be subjective estimates by an analyst!

For this exercise, one may assume that these values are taken as given:

# Remarks:

+   1) For the monthly returns on each of the two stocks, the expected returns μ_A and μ_B are considered to be best estimated expectations. However, since the investment returns are random variables, one must recognize that the actual realized returns may be different from these expectations. The variances σ_A² and σ_B² provide some estimated measures of the uncertainty associated with these monthly returns.