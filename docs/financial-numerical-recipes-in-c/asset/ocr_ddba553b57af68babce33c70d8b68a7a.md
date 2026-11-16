![](bbox=[0.34, 0.02, 0.66, 0.23])

# 6.9 Short-sale constraints

So far the analysis has put no restrictions on the set of weights \(w_p\) that defines the minimum variance frontier. For practical applications, existence of negative weights is problematic, since this involves selling securities short.

This has led to the investigation of restricted mean variance frontiers, where the weights are constrained to be non-negative.

Definition 1 A short sale restricted minimum variance portfolio p solves

```
w_p = \arg \min_w \frac{1}{2} w' V w
subject to
w'e = E[r_p]
w'1 = 1
w' \ge 0
```

Such short sale restricted minimum variance portfolio portfolios are much harder to deal with analytically, since they do not admit a general solution, one rather has to investigate the Kuhn-Tucker conditions for corner solutions etc. To deal with this problem in practice one will use a subroutine for solving constrained optimization problems.

# 6.10 The Sharpe Ratio

The Sharpe ratio of a given portfolio p is defined as

```
S_p = \frac{E[r_p] - r_f}{\sigma(r_p)}
```

The Sharpe ratio \(S_p\) of a portfolio \(p\) is the slope of the line in mean-standard deviations space from the risk free rate through \(p\). Note that in the case with a risk free asset, the tangency portfolio has the maximal Sharpe Ratio on the efficient frontier.