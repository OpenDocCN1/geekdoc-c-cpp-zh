if $\mathbb{E}(\mathbf{M}) = \tilde{\mathbf{M}}$, where $\tilde{\mathbf{M}}$ is the "true" value of $\mathbf{M}$, i.e., the one obtained by the substitution of the true points $(\tilde{x}_i, \tilde{y}_i)$ for the observed data points $(x_i, y_i)$; one may call it the noise-free ($\sigma=0$) version of $\mathbf{M}$. In the same way we construct $\tilde{\mathbf{N}}$, if the matrix $\mathbf{N}$ is also data-dependent. Then we have an analogue of Huber's theorem:

> **Theorem 13** Suppose an estimator $\hat{\mathbf{A}}$ is a solution of a matrix equation $(7.63)$, in which $\mathbf{M}$ and $\mathbf{N}$ are unbiased, i.e., $\mathbb{E}(\mathbf{M}) = \tilde{\mathbf{M}}$ and $\mathbb{E}(\mathbf{N}) = \tilde{\mathbf{N}}$. Then $n^{1/2}(\hat{\mathbf{A}} - \tilde{\mathbf{A}})$ converges to a normal law with mean zero; in particular, $\hat{\mathbf{A}}$ is asymptotically unbiased and consistent, in the limit $n \to \infty$.

Thus in order to obtain an asymptotically unbiased and consistent estimator, one needs to modify the matrices $\mathbf{M}$ and $\mathbf{N}$ so that they become unbiased.

Interestingly, there is another benefit of making such a modification: it eliminates the essential bias of the estimator. Indeed, we have seen in $(7.33)$ that the essential bias is proportional to $\mathbb{E}(\Delta_2\mathbf{M})$, thus if the matrix $\mathbf{M}$ is unbiased, i.e., $\mathbb{E}(\Delta_2\mathbf{M}) = \mathbf{0}$, then the estimator $\hat{\mathbf{A}}$ becomes essentially unbiased (its essential bias is zero). The unbiasedness of $\mathbf{N}$ does not affect the essential bias of $\hat{\mathbf{A}}$.

# **7.9** Asymptotically unbiased and consistent circle fits

Our construction of the unbiased versions of $\mathbf{M}$ and $\mathbf{N}$ for the algebraic circle fits is similar to that developed for more general quadratic models by Kanatani $[93, 94, 95]$ and by Kukush, Markovsky, and van Huffel $[114, 115, 130, 167]$.

First recall the structure of the matrix $\mathbf{M}$:

```
$\mathbf{M} = \begin{bmatrix} \bar{zz} & \bar{xz} & \bar{yz} & \bar{z} \\ \bar{zx} & \bar{xx} & \bar{xy} & \bar{x} \\ \bar{zy} & \bar{xy} & \bar{yy} & \bar{y} \\ \bar{z} & \bar{x} & \bar{y} & 1 \end{bmatrix}$ .
```

A straightforward calculation shows that the mean values of its components are

```
$\mathbb{E}(\bar{x}) = \tilde{x}$,   \qquad$ $\mathbb{E}(\bar{y}) = \tilde{y}$,   \qquad$ $\mathbb{E}(\bar{xy}) = \tilde{x}\tilde{y}$,
$\mathbb{E}(\bar{xx}) = \tilde{x}\tilde{x} + V$,   \qquad$ $\mathbb{E}(\bar{yy}) = \tilde{y}\tilde{y} + V$,   \qquad$ $\mathbb{E}(\bar{z}) = \tilde{z} + 2V$,
$\mathbb{E}(\bar{xz}) = \tilde{x}\tilde{z} + 4\tilde{x}V$,   \qquad$ $\mathbb{E}(\bar{yz}) = \tilde{y}\tilde{z} + 4\tilde{y}V$,   \qquad$ $\mathbb{E}(\bar{zz}) = \tilde{z}\tilde{z} + 8\tilde{z}V + 8V^2$,
```

where we denote, for convenience, $V = \sigma^2$, and our "sample mean" notation is applied to the true points, i.e., $\bar{x} = \frac{1}{n} \sum \tilde{x}_i$, etc.

Now it follows immediately that

```
$\mathbb{E}(\bar{xx} - V) = \tilde{x}\tilde{x}$,   \qquad$ $\mathbb{E}(\bar{yy} - V) = \tilde{y}\tilde{y}$,   \qquad$ $\mathbb{E}(\bar{z} - 2V) = \tilde{z}$,
$\mathbb{E}(\bar{xz} - 4\tilde{x}V) = \tilde{x}\tilde{z}$,   \qquad$ $\mathbb{E}(\bar{yz} - 4\tilde{y}V) = \tilde{y}\tilde{z}$,   \qquad$ $\mathbb{E}(\bar{zz} - 8\tilde{z}V + 8V^2) = \tilde{z}\tilde{z}$.
```