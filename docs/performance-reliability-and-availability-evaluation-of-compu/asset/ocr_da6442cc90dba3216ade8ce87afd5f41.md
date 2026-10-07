# Lifetime Data Analysis

# 571

![](bbox=[0.218, 0.096, 0.781, 0.296])

**Figure 25.22** ln(t_i) × ln(1/(1-F(t_i)))- Parameter Estimation.

# **Table 25.16**

**Test Result - Fifty Devices: Success: 1 Failure:0

| x_i | x_i | x_i | x_i | x_i | x_i | 31 | 1 | x_i |
|---|---|---|---|---|---|---|---||}{
| 1 | 0 | 11 | 17 | 21 | 1 | 41 | 1 | 1 |
| 2 | 1 | 12 | 22 | 31 | 32 | 42 | 1 | 1 |
| 3 | 0 | 13 | 23 | 33 | 43 | 1 | 1 |
| 4 | 0 | 14 | 24 | 34 | 44 | 1 | 1 |
| 5 | 0 | 15 | 25 | 35 | 45 | 1 | 1 |
| 6 | 1 | 16 | 26 | 36 | 46 | 1 | 1 |
| 7 | 1 | 17 | 27 | 37 | 47 | 1 | 1 |
| 8 | 1 | 18 | 28 | 38 | 48 | 0 | |
| 9 | 1 | 19 | 29 | 39 | 49 | 1 | |
| 10 | 1 | 20 | 30 | 40 | 50 | 1 | |

# Normal Distribution

Assume T is a random normally distributed random variable with parameters $\mu$ and $\sigma$ that specify the time to failure of a class of computers. Assume a time failure sample of size n was collected from a population distributed according to T. As the normal distribution has two parameters, the expressions of the first two moments about the origin should first be obtained. These moments could be derived from the normal moment generating function:

$M_T(t) = e^{\frac{\sigma^2}{2}+\mu t}. \quad (25.3.9)$

Taking the first derivative of $M_T(t)$ in relation to t, we obtain

$\frac{dM_T(t)}{dt} = e^{\frac{\sigma^2}{2}+\mu t}(\mu+\sigma^2);$