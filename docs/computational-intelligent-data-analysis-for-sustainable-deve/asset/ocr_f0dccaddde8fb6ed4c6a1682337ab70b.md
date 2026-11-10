\[ f_{Y|X=x_k}(y|x_k) = \frac{f_{X,Y}(x_k, y)}{\int_{y} f_{X,Y}(x_k, y)dy} \quad (10.1) \]

Step 3: We now can make a point prediction of \(\hat{y}_k\) by finding the value for \(y\) that maximizes the conditional:

\[ \hat{y} = \arg\max_{y \in Y} f(y|\mathbf{X} = \mathbf{x}_k) \quad (10.2) \]

Step 4: All the predictions for \(\hat{y}_{1..k}\) are estimated to a Weibull density function, which gives an estimate of the long-term wind resource at the test site.

The methodology implies two design decisions:

+   1. *Choosing a model*: A key decision is which density function should be used to model the univariate densities \(f_{x_k}(x)\), and the choice of the joint density function. A simple and straightforward choice is univariate and multivariate Gaussians. This is because Gaussian density functions have closed-form analytic equations for estimation of parameters and evaluating conditionals that are readily computed. Unfortunately, in many cases, this choice could lead to inaccuracies. Individual variables may not fit a Gaussian density function without significant error—for example, when they have significant tail properties or bimodal distribution. A joint Gaussian density function only captures the linear correlation between the variables. If we choose non-Gaussian univariate densities for \(x_n\), then we must employ *copulas* to construct a multivariate joint density function.

+   2. *Assumptions regarding variable dependency structure*: Parametric estimation of a joint density function is expensive to compute and requires a large amount of data. Inference from the joint is also expensive. Assuming conditional independency among some variables offers efficiency in all three respects because it allows the density function to be factored. As an example, Figure 10.3 shows two different possible dependency structures for the variables and the