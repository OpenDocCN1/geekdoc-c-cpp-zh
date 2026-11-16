![](bbox=[0.18, 0.1, 0.8, 0.42])

badly to unseen test data, while in Figure 8.6b it is not so clear whether polynomials of degree 1, 2, 3, or 4 are best chosen.

# ## 8.6 Bias and Variance

Both example data sets in the previous section were generated from the same underlying process. They are two different snapshots of the process. The reconstructions are inconclusive regarding which model space should be chosen. Taking many snapshots, the picture becomes clearer. For example, running the experiment generating noisy data and fitting polynomials of various degrees 100 times results in the following average mean squared training and test errors and variances:

| degree of polynomial | mean squared training error | variance of squared training error | mean squared test error | variance of squared test error |
|---|---|---|---|---|
| 0 | 0.82 | 8.6 * 10^-3 | 1.0 | 13 * 10^-3 |
| 1 | 0.076 | 0.14 * 10^-3 | 0.1 | 0.24 * 10^-3 |
| 2 | 0.066 | 0.11 * 10^-3 | 0.15 | 1.3 * 10^-3 |
| 3 | 0.057 | 0.083 * 10^-3 | 0.62 | 0.27 |
| 4 | 0.045 | 0.064 * 10^-3 | 7.5 | 100 |
| 5 | 0.038 | 0.053 * 10^-3 | 24 | 156 * 10^3 |