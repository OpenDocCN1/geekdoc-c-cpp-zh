# ARMA Time Series Models

it can be that the transformation acts as a band-stop or notch filter discussed in Section 2.4. That is, the transformation removes the effect of the factor $1 - B + 0.8B^2$, from a practical standpoint frees the frequency in the neighborhood of $f_0 = 0.16$.

**Using R:** You can perform an AR transformation $y_t = \phi(B)x_t$, using the tswge function `artrans.wge(x,phi.tr)`. If `phi.tr = c(1, -0.8)` then the function call `y = atrans.wge(x,phi.tr)` will create the new time series $y$ by $y_t = (1-0.8B^2)x_t$. To calculate the difference $y_t = x_t - x_{t-1} = (1-B)x_t$, use `phi.tr = 1`. See Appendix 3B for more details.

# EXAMPLE 3.26: AR TRANSFORMATIONS

Let $X_t$ be given by

$$(1 - 2.5B + 2.34B^2)X_t = (1 + 0.8B)a_t.$$

in which formed form is

$$(1 - 0.9B)(1 - 1.6B + 0.9B^2)X_t = (1 + 0.8B)a_t.$$

If $Y_t = (1 - 0.9B)X_t$, then

$$(1 - 1.6B + 0.9B^2)Y_t = (1 + 0.8B)a_t.$$

and $Y_t$ satisfies an ARMA(2,1) model illustrating Case (1). However, if $X_t$ is given by

$$(1 - 1.3B + 0.8B^2)X_t = (1 + 0.8B)a_t.$$

and $Y_t = (1 - 0.9B)X_t$, then since $1$ is not a factor of $(1 - 1.3B + 0.8B^2)$, it follows that

$$(1 - 1.3B + 0.8B^2)Y_t = (1 + 0.8B)(1 - 0.9B)a_t, 
= (1 - 0.1B - 0.72B)a_t,$$

and consequently, $Y_t$ is an ARMA(2,2) process exemplifying Case (2).

# Appendix 3A: Proofs of Theorems

# 3A.1 Proofs of Theorems

# Proof of Theorem 3.1

AR(1) Case: We obtained the result for the AR(1) in Equation 3.23 and the discussion that preceded it.