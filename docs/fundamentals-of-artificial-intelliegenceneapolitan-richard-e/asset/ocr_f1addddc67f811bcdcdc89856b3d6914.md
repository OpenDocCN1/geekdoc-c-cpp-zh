# Table 11.1 Miles and Dollars for 25 American Express Card Holders

| Passenger | Miles (X) | Dollars (Y) |
|---|---|---|
| 1 | 1211 | 1802 |
| 2 | 1345 | 2405 |
| 3 | 1422 | 2005 |
| 4 | 1687 | 2511 |
| 5 | 1849 | 2332 |
| 6 | 2026 | 2305 |
| 7 | 2133 | 3016 |
| 8 | 2253 | 3385 |
| 9 | 2400 | 3090 |
| 10 | 2468 | 3694 |
| 11 | 2699 | 3371 |
| 12 | 2806 | 3998 |
| 13 | 3082 | 3555 |
| 14 | 3209 | 4692 |
| 15 | 3466 | 4244 |
| 16 | 3643 | 5298 |
| 17 | 3852 | 4801 |
| 18 | 4033 | 5147 |
| 19 | 4267 | 5738 |
| 20 | 4498 | 6420 |
| 21 | 4533 | 6059 |
| 22 | 4804 | 6426 |
| 23 | 5090 | 6321 |
| 24 | 5233 | 7026 |
| 25 | 5439 | 6964 |

+   2. For every value x of X, \(\epsilon_x\) has the same standard deviation \(\sigma\)

+   3. The random variables \(\epsilon_x\) for all x are mutually independent

Note that these assumptions entail that the expected value of Y given a value x of X is given by

```
E(Y|X = x) = \beta_0 + \beta_1 x.
```

The idea is that the expected value of Y is a deterministic linear function of x. However, the actual value y of Y is not uniquely determined by the value of X because of a random error term \(\epsilon_x\).

Once we make these assumptions about two random variables, we use simple linear regression to try to discover the linear relationship shown in Equality 11.1 from a random sample of values of X and Y. To estimate the values of \(\beta_0\) and \(\beta_1\), we find the values of b_0 and b_1 that minimize the Mean Square Error (MSE), which is

```
\frac{\sum_{i=1}^n[y_i - (b_0 + b_1 x_i)]^2}{n},
```