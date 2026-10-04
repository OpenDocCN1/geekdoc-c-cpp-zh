# ARMA Time Series Models

$$\phi(B)(X_t - \mu) = a_t.$

Then, $X_t$ will be called an AR process of order $p$ and denoted AR(p). Again, we will take $\mu=0$ unless indicated to the contrary.

To clarify Definition 3.2, consider the AR(1) model

$$\phi(B)X_t = (1-\alpha B)X_t = a_t,$$

where $|\alpha| < 1$. Noting that $B\alpha^{-t} = \alpha^{-(t-1)}$, then

$$(1-\alpha B)X_t = \alpha'(1-B)\alpha^{-t}X_t,$$

which can be shown by expanding each side to obtain $X_t - \alpha X_{t-1}$. The two operators $1-\alpha B$ and $\alpha'(1-B)\alpha^{-t}$ are equivalent, that is,

$$1-\alpha B = \alpha'(1-B)\alpha^{-t}.$

Therefore,

$$\alpha'(1-B)\alpha^{-t}X_t = a_t.$

So

$$(1-B)\alpha^{-t}X_t = \alpha^{-t}X_t,$$

and

$$\sum_{k=-\infty}^{t}(1-B)\alpha^{-k}X_k = \sum_{k=-\infty}^{t}\alpha^{-k}a_k,$$

which gives

$$\alpha^{-t}X_t - \lim_{j=-\infty}^{t}\alpha^{-j}X_j = \sum_{k=-\infty}^{t}\alpha^{-k}a_k.$

Since $|\alpha| < 1$, it follows that $\alpha^{-t}X_j = 0$ with probability 1. Consequently,

$$X_t = \sum_{k=-\infty}^{t}\alpha^{t-k}a_k,$$

$= \sum_{h=0}^{t}\alpha^h a_{t-h}.$