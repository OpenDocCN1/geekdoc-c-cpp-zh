
2) An example selected from the R Package MarkowitzR, available from CRAN, is chosen. For this example, the associated R program is run, outputting the concomitant associated numerical and graphical results.

## 3.2.3.1 Markowitz MPT Using R: A Simple Example of a Portfolio Consisting of Two Risky Assets

This example introduces modern portfolio theory in a simple setting of only a single risk-free asset and two risky assets.

### A Portfolio of Two Risky Assets

Consider an investment problem in which there are two nondividend-paying stocks: Stock A and Stock B, and over the next month let

- R_A be the monthly simple return on the Stock A, and
- R_B be the monthly simple return on the Stock B.

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

### Remarks:

- 1) For the monthly returns on each of the two stocks, the expected returns μ_A and μ_B are considered to be best estimated expectations. However, since the investment returns are random variables, one must recognize that the actual realized returns may be different from these expectations. The variances σ_A² and σ_B² provide some estimated measures of the uncertainty associated with these monthly returns.

### Table 3.2 Example data for a two-asset portfolio.

| μ_A | σ_A² | μ_B | σ_B² | σ_A | σ_B | σ_AB | ρ_AB |
|---|---|---|---|---|---|---|---|
| 0.2 | 0.05 | 0.04 | 0.01 | 0.2236 | 0.1000 | -0.0038 | -0.17 |

And the characteristics of the two-asset portfolio data may be expanded, to be given by Table 3.2, as follows:

Given the available investment data as expressed in Table 3.2, the asset allocation problem may be stated as follows:

### Assets Allocation

For a given amount of initial liquid asset, totaling T₀, the task at hand is that one will fully invest *all* this amount in the two stocks A and B. The investment problem is the asset allocation decision: how much to allocate in asset A and how much in asset B?

*Let x_A be the fraction of T₀ to be invested in stock A and x_B be the fraction of T₀ to be invested in stock B.*

The values of x_A and x_B may be positive, zero, or negative:

- Positive values imply *long* positions, in the *purchase*, of the asset.
- Negative values imply *short* positions, in the *sales*, of the asset.
- Zero values imply *no* positions in the asset.

As all the wealth is invested in these two assets, it follows that

x_A + x_B = 1

(3.22)

Thus, if asset A is "shorted," then the proceeds of the short sale will be used to buy more of asset B and vice versa. (To "short" an asset, one borrows the asset, usually from a broker, and then sells it: and the proceeds from the short sale are usually kept on account with a broker—often there may be some restrictions that prevent the use of these funds for the purchase of other assets. The short position is closed out when the asset is repurchased, and then returned to original owner. Should the asset drops in value, then a gain is made on the short sale; and if the asset increases in value, then a loss occurred!) Hence, the investment problem is *to ascertain the values of x_A and x_B in such a way that the overall profit of the investment will always be maximized!*

The present investment in the two stocks forms a portfolio, and the shares of A and B are the portfolio shares or weights.

In this example, the return on the portfolio, R_p, over the following month is a random variable, given by

R_p = x_A R_A + x_B R_B

(3.23)

that is, a weighted average or linear combination of the random variables R_A and R_B. Moreover, as both R_A and R_B are assumed to be normally distributed, it follows from (3.23) that $R_p$ is also normally distributed. Moreover, using the properties of linear combinations of random variables, (3.23) may be used to determine the mean and variance of the distribution of $R_p$, that is, the return of the entire portfolio.

### Probable Expected Return and Variance of the Portfolio

Again, according to (3.23), the mean, variance, and standard deviation of the distribution of the return on the portfolio may be readily derived as follows:

- The mean of the portfolio $\mu_p$ is given by
  $\mu_p = E[R_p]$
  $= E[x_A R_A + x_B R_B],$ upon direct substitution from (3.23)
  $= x_A E[R_A] + x_B E[R_B],$ by the linearity property of the expectation operator $E$
  $= x_A \mu_A + x_B \mu_B$
  namely,
  $\mu_p = E[R_p] = x_A \mu_A + x_B \mu_B$  (3.24)

- The variance of the portfolio $\sigma_p^2$ is given by
  $\sigma_p^2 = \text{var}(R_p)$
  $= E[(R_p - \mu_p)^2],$ by definition of the variance property
  $= E[((x_A R_A + x_B R_B) - (x_A \mu_A + x_B \mu_B))^2]$
  upon direct substitutions, respectively, from (3.23) and (3.24):
  $= E[(x_A R_A + x_B R_B)^2 + (x_A \mu_A + x_B \mu_B)^2 - 2(x_A R_A + x_B R_B)(x_A \mu_A + x_B \mu_B)]$
  upon squaring the terms
  $= E[(x_A^2 R_A^2 + x_B^2 R_B^2 + 2x_A x_B R_A R_B) + (x_A^2 \mu_A^2 + x_B^2 \mu_B^2 + 2x_A x_B \mu_A \mu_B) - (2x_A^2 R_A \mu_A + 2x_A x_B R_A \mu_B + 2x_A x_B R_B \mu_A + 2x_B^2 R_B \mu_B)]$
  upon expanding the multiplication of terms
  $= E[x_A^2 R_A^2 + x_B^2 R_B^2 + 2x_A x_B R_A R_B + x_A^2 \mu_A^2 + x_B^2 \mu_B^2 + 2x_A x_B \mu_A \mu_B - 2x_A^2 R_A \mu_A - 2x_A x_B R_A \mu_B - 2x_A x_B R_B \mu_A - 2x_B^2 R_B \mu_B]$
  upon removing all the parentheses
  $= E[(x_A^2 R_A^2 - 2x_A^2 R_A \mu_A + x_A^2 \mu_A^2) + (x_B^2 R_B^2 - 2x_B^2 R_B \mu_B + x_B^2 \mu_B^2) + (2x_A x_B R_A R_B + 2x_A x_B \mu_A \mu_B - 2x_A x_B R_A \mu_B - 2x_A x_B R_B \mu_A)]$

- 3) Hence, assets with negatively correlated returns may be beneficial when building up a portfolio since the concomitant risk, as indicated by portfolio standard deviation, is reduced.
- 4) Forming portfolios with positively correlated assets may reduce risk as long as the correlation is small.

## Example 3.2 Some Preliminary Model Portfolios

Using the asset information in Table 3.2, one may create some preliminary portfolios:

**Portfolio 1:** An equally weighted portfolio with $x_A = 0.500 = x_B$.

Given:
Here one may use Equations (3.23–3.26):

$R_p = x_A R_A + x_B R_B$  (3.23)
$\mu_p = E[R_p] = x_A \mu_A + x_B \mu_B$  (3.24)
$\sigma_p^2 = \text{var}(R_p) = x_A^2 \sigma_A^2 + x_B^2 \sigma_B^2 + 2 x_A x_B \sigma_{AB}$  (3.25)
$\sigma_p = \text{SD}(R_p) = \sqrt{\text{var}(R_p)} = \sqrt{x_A^2 \sigma_A^2 + x_B^2 \sigma_B^2 + 2 x_A x_B \sigma_{AB}}$  (3.26)

to obtain

$\mu_p = E[R_p] = x_A \mu_A + x_B \mu_B$, using (3.24)
$= (0.500)(0.2) + (0.500)(0.04)$, using Table 3.2
$= 0.100 + 0.020$
$= 0.120$

$\sigma_p^2 = \text{var}(R_p) = x_A^2 \sigma_A^2 + x_B^2 \sigma_B^2 + 2 x_A x_B \sigma_{AB}$, using (3.25) and Table 3.2
$= (0.500)^2 (-0.2236)^2 + (0.500)^2 (-0.1000)^2$
$+ 2(0.500)(0.500)(-0.0038)(-0.1000)$
$= 0.0125 + 0.0025 + 0.00019$
$= 0.01519$

$\sigma_p = \sqrt{\sigma_p^2} = \text{SD}(R_p) = \sqrt{\text{var}(R_p)}$, using (3.26)
$= \sqrt{(0.01519)}$
$= 0.12325$

$\mu_p = E[R_p] = x_A \mu_A + x_B \mu_B$

**Remark:**
The following R-code* segment may be used for this computations:

```
mu <- A'muA + B'muB
σ_p^2 <- var(R_p) <- x_A^2 σ_A^2 + x_B^2 σ_B^2 + 2 x_A x_B σ_AB
var <- A'A sigA*sigA + B'B sigB*sigB + 2' A'B' sigAB)
```
