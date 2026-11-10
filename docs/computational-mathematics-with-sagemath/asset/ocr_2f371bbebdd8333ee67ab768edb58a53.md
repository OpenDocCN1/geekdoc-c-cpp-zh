+   - the method is exact for any polynomial of degree up to $3n + 1$.

We can naively remark that the $3n + 2$ unknowns (the $2n + 1$ weights and the $n + 1$ added points) are a priori determined by requiring that the method is of order at least $3n + 1$ (which indeed yields $3n + 2$ equalities). Beware that the weights associated in the Gauss-Kronrod method to the $n$ Gauss-Legendre points have no reason to coincide with those associated in the original Gauss-Legendre method.

Such an extension method becomes particularly interesting when the main cost of a quadrature rule is the number of evaluations of the function $f$ to integrate (moreover if the integration points and weights are tabulated). The Gauss-Kronrod method being in principle more precise than the Gauss-Legendre method, we can use its result $I_1$ to validate the result $I_0$ of the latter method, and obtain an estimate of the error as $|I_1 - I_0|$, while minimising the number of evaluations of $f$. The reader might compare this strategy, which is particular to the Gauss-Legendre method, with the more general subdivision strategy described on page 308.

# **Double Exponential Methods.**

The double exponential (DE) methods rely on a change of variable which transforms a bounded integration range into $\mathbb{R}$, and on the very good accuracy of the trapezoidal rule on $\mathbb{R}$ for analytic functions. For a function $f$ integrable on $\mathbb{R}$, and an integration step $h$, the trapezoidal rule computes

$$ I_h = h \sum_{i=-\infty}^{+\infty} f(hi) $$

as approximate value for $\int_{-\infty}^{+\infty} f(x) \, dx$. Discovered in 1973 by Takahasi and Mori, the double exponential transform is commonly used by numerical integration software tools. We describe here its main features; an introduction to this transform and its discovery is given in [Mor05]. This article gives in particular an explanation of the surprising good accuracy of the trapezoidal rule, which is optimal in a certain sense, for analytic functions on $\mathbb{R}$.

To compute

$$ I = \int_{-1}^{1} f(x) \, dx, $$

it is possible to use a transform $x = \varphi(t)$ where $\varphi$ is analytic on $\mathbb{R}$ and satisfies

$$ \lim_{t\to -\infty} \varphi(t) = -1, \quad \lim_{t\to +\infty} \varphi(t) = 1, $$

and then

$$ I = \int_{-\infty}^{+\infty} f(\varphi(t))\varphi'(t) \, dt. $$

Applying the trapezoidal rule to this last expression, we compute

$$ I_h^N = h \sum_{k=-N}^{N} f(\varphi(kh))\varphi'(kh) $$