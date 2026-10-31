+   1. The processes are stationary AR(3) models, since the roots are outside the unit circle (i.e., the absolute reciprocals of the roots are all less than 1)
+   2. In each model, the three roots are all equidistant from the unit circle (i.e., $|r_j^{-1}| = 0.95$)
+   3. The system frequencies associated with the two factors

This type of presentation will be used throughout this book. We note that for higher-order models, the factorization must be done numerically.

# TABLE 3.1

Factor Table for the AR(3) Model in Example 3.8

| AR Factors | Roots ($r_j$) | $|r_j^{-1}|$ | $f_{0j}$ |
|---|---|---|---|
| $1 - 1.6B + 0.9B^2$ | $0.89 \pm 0.57i$ | 0.95 | 0.09 |
| $1 - 0.95B$ | 1.053 | 0.95 | 0 |

# TABLE 3.2

Factor Table for the AR(3) Model in Example 3.9

| AR Factors | Roots ($r_j$) | $|r_j^{-1}|$ | $f_{0j}$ |
|---|---|---|---|
| $1 - 1.6B + 0.9B^2$ | $0.89 \pm 0.57i$ | 0.95 | 0.09 |
| $1 + 0.95B$ | $-1.053$ | 0.95 | 0.5 |

Using R: For a given AR(p) model, you can obtain a factor table using the tswge function factor.wge. This function will factor an mth order polynomial into its first order and irreducible second order factors. Again, be careful with the signs. See Appendix 3B for more details.

# EXAMPLE 3.12: An AR(4) Model

Consider the AR(4) process given by

$X_t -1.15X_{t-1} +0.19X_{t-2} +0.64X_{t-3} -0.61X_{t-4} = a_t. \quad (3.81)$

Although inspecting the coefficients in Equation 3.81 tells us nothing about the nature of the model, much can be learned about the model characteristics by examining the factors. The characteristic polynomial can be factored as