Now every term converges to its true value, in the limit $n \rightarrow \infty$, thus the solutions converge to the true parameter values $\tilde{\alpha}$ and $\tilde{\beta}$. The solutions of (6.50) are called the *adjusted least squares* (ALS) *estimators*.

The adjusted least squares estimators work well in practice, their accuracy is comparable to that of the MLE described in Chapter 1; see [37, 116]. Interestingly, both the estimators (ALS and MLE) have infinite moments, see [37]; paradoxically, this feature appears to be a “certificate of quality.” We note, however, that the ALS (unlike the MLE) assumes that the noise level $\sigma$ is known.

# Adjusted least squares: polynomial case. The above method generalizes to polynomials as follows. Suppose one fits a polynomial of degree $k$,

$$ y = p(x) = \beta_0 + \beta_1 x + \cdots + \beta_k x^k, $$

to observed points by the classical regression, i.e., by minimizing

$$ \mathscr{F}(\beta_0, \ldots, \beta_k) = \frac{1}{n} \sum [y_i - p(x_i)]^2. $$

This reduces to a standard system of linear equations

$$ \beta_0 \overline{x^m} + \beta_1 \overline{x^{m+1}} + \cdots + \beta_k \overline{x^{m+k}} = \overline{x^m y}, \quad \quad m = 0, \ldots, k \quad (6.51) $$

We now compute the limits of the coefficients of these equations, as $n \rightarrow \infty$. According to the central limit theorem, they converge to their mean values, i.e.,

$$ \overline{x^m} = \mathbb{E}(x^m) + \mathscr{O}_P(n^{-1/2}), \quad \quad \overline{x^m y} = \mathbb{E}(x^m y) + \mathscr{O}_P(n^{-1/2}). $$

To ensure the consistency it is enough to make the mean values equal to the corresponding true values, i.e., we need to replace $\overline{x^m}$ and $\overline{x^m y}$ with some other statistics, call them $A_m$ and $B_m$, respectively, so that

$$ \mathbb{E}(A_m) = \overline{x^m}, \quad \quad \mathbb{E}(B_m) = \overline{x^m y}. $$

*Remark.* Superficially, the problem appears to be about adjusting the mean values, i.e., correcting for bias. Some authors mistakenly claim that the adjustment produces unbiased estimates of the unknown parameters. In fact, the resulting estimates are only asymptotically unbiased (in the limit $n \rightarrow \infty$); they are also consistent.

We will show how to choose the desired statistics $A_m$ and $B_m$ for small values of $m$. Obviously, $A_1 = \bar{x}$ and $B_1 = \overline{xy}$. Then direct calculation gives

$$ \begin{aligned} & \mathbb{E}(\overline{x^2}) = \bar{x}^2 + \sigma^2, \\ & \mathbb{E}(\overline{x^3}) = \bar{x}^3 + 3 \bar{x} \sigma^2, \\ & \mathbb{E}(\overline{x^4}) = \bar{x}^4 + 6 \bar{x}^2 \sigma^2 + 3 \sigma^4, \end{aligned} \quad \begin{aligned} & \mathbb{E}(\overline{x^2 y}) = \bar{x}^2 \bar{y} + \bar{x} \sigma^2, \\ & \mathbb{E}(\overline{x^3 y}) = \bar{x}^3 \bar{y} + 3 \bar{x} \sigma^2, \\ & \mathbb{E}(\overline{x^4 y}) = \bar{x}^4 \bar{y} + 6 \bar{x}^2 \sigma^2 + 3 \bar{y} \sigma^4, \end{aligned} $$