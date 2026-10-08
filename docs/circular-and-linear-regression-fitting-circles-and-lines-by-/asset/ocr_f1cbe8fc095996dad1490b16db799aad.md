For example, if one deals with a linear relation $y = a + bx$, then the least squares estimates $\hat{a}$ and $\hat{b}$ minimize the function

$$\mathcal{F}(a, b) = \sum_{i=1}^{n} (y_i - a - bx_i)^2 .$$

Solving equations $\partial \mathcal{F} / \partial a = 0$ and $\partial \mathcal{F} / \partial b = 0$ gives

$$\hat{a} = \bar{y} - \hat{b} \bar{x} \quad \text{and} \quad \hat{b} = s_{xy}/s_{xx}, \tag{1.3}$$

where $\bar{x}$ and $\bar{y}$ are the “sample means”

$$\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i \quad \text{and} \quad \bar{y} = \frac{1}{n}\sum_{i=1}^{n} y_i \tag{1.4}$$

and

$$\begin{aligned} s_{xx} &= \sum_{i=1}^{n} (x_i - \bar{x})^2 \\ s_{yy} &= \sum_{i=1}^{n} (y_i - \bar{y})^2 \\ s_{xy} &= \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y}). \end{aligned}$$

are the components of the so called “scatter matrix”

$$\mathbf{S} = \left[ \begin{array}{cc} s_{xx} & s_{xy} \\ s_{xy} & s_{yy} \end{array} \right], \tag{1.5}$$

which characterizes the “spread” of the data set about its centroid $(\bar{x}, \bar{y})$.

> *Remark.* To estimate $a$ and $b$, one does not need to know the variance $\sigma^2$. It can be estimated separately by maximizing the log-likelihood function (1.1) with respect to $\sigma^2$, which gives

$$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{a} - \hat{b}x_i)^2. \tag{1.6}$$

This estimate is slightly biased, as $\mathbb{E}(\hat{\sigma}^2) = \frac{n-2}{n}\sigma^2$. It is customary to replace $n$ in the denominator with $n - 2$, which gives an unbiased estimate of $\sigma^2$. Both versions of $\hat{\sigma}^2$ are strongly consistent, i.e., they converge to $\sigma^2$ with probability one.

The regression model has excellent statistical properties. The estimates $\hat{a}$ and $\hat{b}$ are strongly consistent, i.e., $\hat{a} \to a$ and $\hat{b} \to b$ as $n \to \infty$ (with probability