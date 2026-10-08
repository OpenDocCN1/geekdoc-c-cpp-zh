resulting parameter estimates will be asymptotically efficient if and only if the weights $w_{i}$ are proportional to the gradient weights (6.15), i.e.,

```
$\mathbf{V} = \mathbf{V}_{\min} \quad \Longleftrightarrow \quad w_{i} = \frac{c(\boldsymbol{\Theta})}{\|\nabla_{\mathbf{x}} P(x_{i}, y_{i}; \boldsymbol{\Theta})\|^{2}}$,
```

where $c(\boldsymbol{\Theta})$ is any function that depends on the parameters only.

In addition, Chernov and Lesort [42] derived (6.40) in the context of not only the Cartesian model, but also the radial model. Lastly, they named the inequality (6.40) Kanatani-Cramer-Rao (KCR) lower bound, recognizing the crucial contribution of Kanatani [95, 96].

**Assessing the quality of estimators.** Our analysis dictates the following strategy of assessing the quality of an estimator $\hat{\boldsymbol{\Theta}}$: first of all, its accuracy is characterized by the matrix $\mathbf{V}$, which must be compared to the KCR lower bound $\mathbf{V}_{\min}$. We will see that for all the circle fitting algorithms and for many popular ellipse fitting algorithms the matrix $\mathbf{V}$ actually achieves its lower bound $\mathbf{V}_{\min}$, i.e., we have $\mathbf{V} = \mathbf{V}_{\min}$, hence the corresponding algorithms are optimal to the leading order.

Next, once the factor $\mathbf{V}$ is already at its natural minimum, the accuracy of an estimator should be characterized by the vector $\mathbf{B}_{1}$ representing the essential bias: better estimates should have smaller essential biases. It appears that there is no natural minimum for $\|\mathbf{B}_{1}\|$, in fact there exist estimators which have a minimum variance $\mathbf{V} = \mathbf{V}_{\min}$ and a zero essential bias, i.e., $\mathbf{B}_{1} = \mathbf{0}$. We will construct them in Section 7.5.

# **6.10  Bias and inconsistency in the large sample limit**

Thus far our analysis was restricted to the small noise asymptotic model, in which $\sigma \rightarrow 0$ and $n$ was fixed (or assumed to be a moderately large constant); such a model is perhaps appropriate for most computer vision applications. However, many statisticians investigate curve fitting algorithms in the traditional large sample limit $n \rightarrow \infty$ keeping $\sigma > 0$ fixed. We devote the last few sections to these studies.

**Bias.** In many nonlinear statistical models, unbiased estimation of unknown parameters is virtually impossible, thus all practical estimators are biased. We have seen in Chapters 1 and 2 that even in the linear EIV model $y = a + bx$ all known estimators of $a$ and $b$ are actually biased. In nonlinear EIV regression, the bias is inevitable and much more significant than in the linear case, see e.g., [28, 79]. The biasedness of curve fitting algorithms has been pointed independently by many authors, see [17, 18, 31, 94, 189, 198], just to name a few.

The origin of the bias is geometrically obvious, see our illustration in Fig. 6.5. Under the standard assumption that the noise is centrally-symmetric,