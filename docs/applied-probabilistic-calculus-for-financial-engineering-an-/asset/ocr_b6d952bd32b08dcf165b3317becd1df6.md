# Incorporating investor views:

+   1. Analysts tell you that AEP has found a way to store electricity. Based on this breakthrough, they expect AEP to outperform XOM by 1% per month.
+   2. Given the current economic conditions, we think that INTC will outperform AMZN by 1.75% per month.

+   - Relative views are common in reality.
+   - Absolute views, such as AEP having returns of 2% per month, are much less common.

# Views versus Implied Excess Returns:

View 1: AEP outperforms XOM by 1% per month

+   - The difference in implied excess returns is −0.32% per month.
+   - One would expect that incorporating these views will lead to an increase in one's holdings of AEP and a decrease in XOM.

0.0092

View 2: INTC will outperform AMZN by 1.75% per month.

+   - The difference in implied excess returns is 0.18% per month.
+   - We would expect that incorporating our view will increase our holdings of INTC and reduce our holdings of AMZN.

The views expressed above are relative views of assets.

# Incorporating our views:

To link our views to implied excess returns, we need a link matrix, P.
Matrix P is constructed in the following way:
Each row represents a view, each column represents a company:

| | INTC | AEP | AMZN | MRK | XOM |
|---|---|---|---|---|---|
| P = View 1 | 0 | 1 | 0 | 0 | -1 |
| View 2 | 1 | 0 | -1 | 0 | 0 |
| View 3 | 0.5 | 0 | 0.5 | -0.5 | -0.5 |

# The View Vector and Uncertainty

What do Q and Ω look like?

```
Q + ε = [Q1; :; Qk] + [ε1; :; εk] → Q + ε = [0.01; 0.0175] + [ε1; ε2]
View 1 ↓
View 2 ↑
```