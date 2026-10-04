The condition $\sum_{j=0} |\pi_j| < \infty$ assures that $\sum_{j=0} \pi_j X_{t-j}$ is mean square convergent (see Theorem 3.1). The following theorem provides necessary and sufficient conditions for an MA($q$) process to be invertible.

# Theorem 3.3

Let $X_t$ be the MA($q$) process $X_t = 	heta(B)a_t$. Then $X_t$ is invertible if and only if the roots of $	heta(z) = 0$ all lie outside the unit circle.

Proof: See Appendix 3B.

In order to determine whether or not a MA($q$) process is invertible, we recommend examining a factor table in which the factors of $	heta(B)$ are given.

**Using R:** Factor tables for MA components can be obtained as in the AR case by using the tswge function factor.wge. See Appendix 3B.

# 3.2.13 Two Reasons for Imposing Invertibility

When using an MA($q$) model to analyze time series data, we restrict our attention to invertible models. There are two main reasons for this restriction.

+   1. Invertibility assures that the present events are associated with the past in a sensible manner: We rewrite the MA(1) model in Equation 3.9 with $\mu=0$ in the form $a_t = X_t + 	heta_{t-1}$. Using this form of the model, it follows that $a_{t-1} = X_{t-1} + 	heta_{t-1}a_{t-2}$ so that

```
$a_t = X_t + 	heta_{t-1}(X_{t-1} + 	heta_{t-1}a_{t-2})$
$= X_t + 	heta_{t-1}X_{t-1} + 	heta_{t-1}^2a_{t-2}$
$= X_t + 	heta_{t-1}X_{t-1} + 	heta_{t-1}^2X_{t-2} + 	heta_{t-1}^3a_{t-3}$.
```

Continuing, we obtain $a_t = X_t + 	heta_{t-1}X_{t-1} + 	heta_{t-1}^2X_{t-2} + \cdots + 	heta_{t-1}^kX_{t-k}$

```
$X_t = -	heta_{t-1}X_{t-1} - 	heta_{t-1}^2X_{t-2} - \cdots - 	heta_{t-1}^kX_{t-k} + 	heta_{t-1}^ka_{t-k} - 	heta_{t-1}^{k+1}a_{t-k-1}. \quad (3.84)
```

If $|	heta_1| > 1$ the process is not invertible and Equation 3.84 shows that in this case, $X_t$ is increasingly dependent on the past. For most problems, this is not a practically acceptable model.

+   2. Imposing invertibility removes model multiplicity: We again consider the MA(1) model in Equation 3.9. From Equation 3.11, the autocorrelation