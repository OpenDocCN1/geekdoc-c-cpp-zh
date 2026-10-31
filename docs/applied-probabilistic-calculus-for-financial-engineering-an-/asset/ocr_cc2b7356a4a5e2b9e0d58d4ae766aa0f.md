follows from (3.23) that $R_p$ is also normally distributed. Moreover, using the properties of linear combinations of random variables, (3.23) may be used to determine the mean and variance of the distribution of $R_p$, that is, the return of the entire portfolio.

# Probable Expected Return and Variance of the Portfolio

Again, according to (3.23), the mean, variance, and standard deviation of the distribution of the return on the portfolio may be readily derived as follows:

+   - The mean of the portfolio $\mu_p$ is given by
+     $\mu_p = E[R_p]$
+     $= E[x_A R_A + x_B R_B],$ upon direct substitution from (3.23)
+     $= x_A E[R_A] + x_B E[R_B],$ by the linearity property of the expectation operator $E$
+     $= x_A \mu_A + x_B \mu_B$
+     namely,
+     $\mu_p = E[R_p] = x_A \mu_A + x_B \mu_B$  (3.24)
+   
+   - The variance of the portfolio $\sigma_p^2$ is given by
+     $\sigma_p^2 = \text{var}(R_p)$
+     $= E[(R_p - \mu_p)^2],$ by definition of the variance property
+     $= E[((x_A R_A + x_B R_B) - (x_A \mu_A + x_B \mu_B))^2]$
+     upon direct substitutions, respectively, from (3.23) and (3.24):
+     $= E[(x_A R_A + x_B R_B)^2 + (x_A \mu_A + x_B \mu_B)^2 - 2(x_A R_A + x_B R_B)(x_A \mu_A + x_B \mu_B)]$
+     upon squaring the terms
+     $= E[(x_A^2 R_A^2 + x_B^2 R_B^2 + 2x_A x_B R_A R_B) + (x_A^2 \mu_A^2 + x_B^2 \mu_B^2 + 2x_A x_B \mu_A \mu_B) - (2x_A^2 R_A \mu_A + 2x_A x_B R_A \mu_B + 2x_A x_B R_B \mu_A + 2x_B^2 R_B \mu_B)]$
+     upon expanding the multiplication of terms
+     $= E[x_A^2 R_A^2 + x_B^2 R_B^2 + 2x_A x_B R_A R_B + x_A^2 \mu_A^2 + x_B^2 \mu_B^2 + 2x_A x_B \mu_A \mu_B - 2x_A^2 R_A \mu_A - 2x_A x_B R_A \mu_B - 2x_A x_B R_B \mu_A - 2x_B^2 R_B \mu_B]$
+     upon removing all the parentheses
+     $= E[(x_A^2 R_A^2 - 2x_A^2 R_A \mu_A + x_A^2 \mu_A^2) + (x_B^2 R_B^2 - 2x_B^2 R_B \mu_B + x_B^2 \mu_B^2) + (2x_A x_B R_A R_B + 2x_A x_B \mu_A \mu_B - 2x_A x_B R_A \mu_B - 2x_A x_B R_B \mu_A)]$