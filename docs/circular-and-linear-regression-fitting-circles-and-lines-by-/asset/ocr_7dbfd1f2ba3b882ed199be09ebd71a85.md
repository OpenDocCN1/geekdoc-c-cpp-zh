# **6.9 Kanatani-Cramer-Rao lower bound**

**KCR lower bound.** The matrix **V**, representing the leading terms of the variance, has a natural lower bound (an analogue of the Cramer-Rao bound): there is a symmetric positive semi-definite matrix $\mathbf{V}_{\min }$ such that for every geometrically consistent estimator

$$
\mathbf{V} \geq \mathbf{V}_{\min } \text{,}
$$

in the sense that $\mathbf{V}-\mathbf{V}_{\min }$ is a positive semi-definite matrix.

In fact, the matrix $\mathbf{V}_{\min }$ coincides with $\mathbf{V}_{\mathrm{MLE}}$, cf. (6.37) obtained by Fuller for the variance of the Maximum Likelihood Estimator, i.e.

$$
\mathbf{V}_{\min }=\mathbf{V}_{\mathrm{MLE}}=\left(\sum_{i=1}^{n} \frac{\mathbf{P}_{\Theta i} \mathbf{P}_{\Theta i}^{T}}{\left\|\mathbf{P}_{\mathbf{X} i}\right\|^{2}}\right)^{-1} \text{,}
$$

see the notation of (6.37).

We say that an estimator $\hat{\Theta}$ is $asymptotically\ efficient$, as $\boldsymbol{\sigma} \rightarrow \mathbf{0}$, if its covariance matrix $\mathbf{V}$ satisfies $\mathbf{V}=\mathbf{V}_{\min }$. Obviously, the MLE (the geometric fit) is asymptotically efficient.

**History of the KCR.** The inequality (6.40) with the formula (6.41) have an interesting history. First, an analogue of (6.40) was proved in the mid-1990s by Kanatani [95, 96] who showed that for any $unbiased$ estimator $\hat{\Theta}$

$$
\operatorname{Var}(\hat{\Theta}) \geq \sigma^{2} \mathbf{V}_{\min } \text{.}
$$

He also derived an explicit formula (6.41) for the matrix $\mathbf{V}_{\min }$.

It is important to note that the inequality (6.42) is, in a sense, stronger than (6.40), because it gives a lower bound on the $actual$ covariance matrix, rather than its leading term. On the other hand, Kanatani assumed unbiasedness, hence his bound (6.42), strictly speaking, could not be applied to many practical estimators, including $\hat{\Theta}_{\mathrm{MLE}}$, as they are biased in most cases. (Very likely it cannot be applied to $any$ existing estimator of nonlinear curve parameters, as virtually all of them are biased.)

In the early 2000s Chernov and Lesort [42] realized that Kanatani's argument [95] essentially works for biased estimators, provided those are geometrically consistent. As a result, they derived a more general bound (6.40) for all geometrically consistent estimates (including the MLE). Incidentally, this proves that the MLE is asymptotically efficient (optimal to the leading order) in the much larger class of all geometrically consistent estimators.

Furthermore, Chernov and Lesort proved [42] that the gradient-weighted algebraic fit (GRAF), introduced in Section 6.5, is always asymptotically efficient, i.e., its covariance matrix $\mathbf{V}$ attains the lower bound $\mathbf{V}_{\min }$. In fact, they showed in [42] that if one uses a general weighted algebraic fit (6.13), then the