**TABLE 6.1: Linearity Likelihood for Math, Science, and Engineering Data; Devore**

| Correlation ρ | Relationship |
|---|---|
| 0.8 < |ρ| ≤ 1.0 | Strong linear relationship |
| 0.5 < |ρ| ≤ 0.8 | Moderate linear relationship |
| 0.0 ≤ |ρ| ≤ 0.5 | Weak linear relationship |

**TABLE 6.2: Linearity Likelihood for Non-Math, Non-Science, and Non-Engineering Data; Johnson**

| Correlation ρ | Relationship |
|---|---|
| 0.5 < |ρ| ≤ 1.0 | Strong linear relationship |
| 0.3 < |ρ| ≤ 0.5 | Moderate linear relationship |
| 0.1 ≤ |ρ| ≤ 0.3 | Weak linear relationship |
| 0.0 ≤ |ρ| ≤ 0.1 | No linear relationship |

In our modeling efforts, we emphasize the interpretation of ρ ≈ 0. A very small correlation coefficient can be interpreted as indicating either no linear relationship or the existence of a nonlinear relationship. Many neophyte analysts fail to pick up on the importance of potential nonlinear relationships in their interpretation.

Let’s look at an example where we attempt to fit a linear model to data that may not be linear.

# Example 6.1. Exponential Decay.

Build a mathematical model to predict the degree of recovery after discharge for orthopedic surgical patients. There are two variables: time t in days in the hospital, and a medical prognosis index for every v with larger values indicating a better prognosis. The data in Table 6.3 comes from Neter et al. [NKNW1996, p. 469].

**TABLE 6.3: Hospital Stay vs. Recovery Index Data**

| t | 2 | 5 | 7 | 10 | 14 | 19 | 26 | 31 | 34 | 38 | 45 | 52 | 53 | 60 | 65 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| y | 54 | 50 | 45 | 37 | 35 | 25 | 20 | 16 | 18 | 13 | 8 | 11 | 8 | 4 | 6 |