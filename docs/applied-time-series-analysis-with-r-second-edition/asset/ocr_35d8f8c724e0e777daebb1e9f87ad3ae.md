∑_{j=0}^{∞} π_j X_{t-j} = a_t

which is a process of infinite AR form.

# Definition 3.4

If an MA(q) process X_t can be expressed as in Equation 3.83 with ∑_{j=0}^{∞} |π_j| < ∞, then X_t is said to be invertible.

The condition ∑_{j=0}^{∞} |π_j| < ∞ assures that ∑_{j=0}^{∞} π_j X_{t-j} is mean square convergent (see Theorem 3.1). The following theorem provides necessary and sufficient conditions for an MA(q) process to be invertible.

# Theorem 3.3

Let X_t be the MA(q) process X_t = θ(B) a_t. Then X_t is invertible if and only if the roots of θ(z) = 0 all lie outside the unit circle.

*Proof:* See Appendix 3B.

In order to determine whether or not a given MA(q) process is invertible, we recommend examining a factor table in which the factors of θ(B) are given.

**Using R:** Factor tables for MA components can be obtained as in the AR case by using the tswge function factor.wge. See Appendix 3B.

# 3.2.13 Two Reasons for Imposing Invertibility

When using an MA(q) model to analyze time series data, we will restrict our attention to invertible models. There are two major reasons for this restriction.

+   1. *Invertibility assures that the present events are associated with the past in a sensible manner:* We rewrite the MA(1) model in Equation 3.9 with μ = 0 in the form a_t = X_t + θ_1 a_{t-1}. Using this form of the model, it follows that a_{t-1} = X_{t-1} + θ_1 a_{t-2}, so that