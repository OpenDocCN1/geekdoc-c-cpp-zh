Recall that the distance $d_{i}$ is given by

```
$$
\begin{aligned} d_{i} & = \sqrt{\left(x_{i}-a\right)^{2}+\left(y_{i}-b\right)^{2}-R} \\ & = \sqrt{\left[\left(\bar{x}_{i}-\bar{a}\right)+\left(\delta_{i}-\Delta a\right)\right]^{2}+\left[\left(\bar{y}_{i}-\bar{b}\right)+\left(\varepsilon_{i}-\Delta b\right)\right]^{2}-\bar{R}-\Delta R,}\end{aligned}\tag{7.1}
$$
```

cf. (3.3). Here $\bar{a}, \bar{b}, \bar{R}$ are the parameters of the true circle. For brevity we denote

```
$$
\tilde{u}_{i}=\left(\bar{x}_{i}-\bar{a}\right) / \bar{R} \quad \text { and } \quad \tilde{v}_{i}=\left(\bar{y}_{i}-\bar{b}\right) / \bar{R},
$$
```

in fact these are the "true" values of $u_{i}$ and $v_{i}$ introduced earlier in (4.20)-(4.21). Note that $\tilde{u}_{i}^{2}+\tilde{v}_{i}^{2}=1$ for every $i$.

Now, to the first order, we have

```
$$
\begin{aligned} d_{i} & = \sqrt{\bar{R}^{2}+2 \bar{R} \tilde{u}_{i}\left(\delta_{i}-\Delta a\right)+2 \bar{R} \tilde{v}_{i}\left(\varepsilon_{i}-\Delta b\right)+\mathcal{O}_{P}\left(\sigma^{2}\right)-\bar{R}-\Delta R} \\ & =\tilde{u}_{i}\left(\delta_{i}-\Delta a\right)+\tilde{v}_{i}\left(\varepsilon_{i}-\Delta b\right)-\Delta R+\mathcal{O}_{P}\left(\sigma^{2}\right) .\end{aligned}\tag{7.2}
$$
```

Minimizing $\sum d_{i}^{2}$ to the first order is equivalent to minimizing

```
$$
\sum_{i=1}^{n}\left(\tilde{u}_{i} \Delta a+\tilde{v}_{i} \Delta b+\Delta R-\tilde{u}_{i} \delta_{i}-\tilde{v}_{i} \varepsilon_{i}\right)^{2} .
$$
```

This is a classical least squares problem that can be written as

```
$$
\mathbf{W} \Delta \Theta \approx \tilde{\mathbf{U}} \delta+\tilde{\mathbf{V}} \varepsilon,\tag{7.3}
$$
```

where

```
$$
\mathbf{W}=\left[\begin{array}{ccc} \tilde{u}_{1} & \tilde{v}_{1} & 1 \\ \vdots & \vdots & \vdots \\ \tilde{u}_{n} & \tilde{v}_{n} & 1 \end{array}\right],\tag{7.4}
$$
```

$\Theta=(a, b, R)^{T}$, and

```
$$
\delta=\left(\delta_{1}, \ldots, \delta_{n}\right)^{T} \quad \text { and } \quad \varepsilon=\left(\varepsilon_{1}, \ldots, \varepsilon_{n}\right)^{T}
$$
```

and

```
$$
\tilde{\mathbf{U}}=\operatorname{diag}\left(\tilde{u}_{1}, \ldots, \tilde{u}_{n}\right) \quad \text { and } \quad \tilde{\mathbf{V}}=\operatorname{diag}\left(\tilde{v}_{1}, \ldots, \tilde{v}_{n}\right) .
$$
```

The solution of the least squares problem (7.3) is

```
$$
\Delta \hat{\Theta}=\left(\mathbf{W}^{T} \mathbf{W}\right)^{-1} \mathbf{W}^{T}\left(\tilde{\mathbf{U}} \delta+\tilde{\mathbf{V}} \varepsilon\right),\tag{7.5}
$$
```

of course this does not include the $\mathcal{O}_{P}\left(\sigma^{2}\right)$ terms.

Thus the variance of our estimator, to the leading order, is

```
$$
\mathbb{E}\left[\left(\Delta \hat{\Theta}\right)\left(\Delta \hat{\Theta}\right)^{T}\right]=\left(\mathbf{W}^{T} \mathbf{W}\right)^{-1} \mathbf{W}^{T} \mathbb{E}\left[\left(\tilde{\mathbf{U}} \delta+\tilde{\mathbf{V}} \varepsilon\right)\left(\delta^{T} \tilde{\mathbf{U}}+\varepsilon^{T} \tilde{\mathbf{V}}\right)\right] \mathbf{W}\left(\mathbf{W}^{T} \mathbf{W}\right)^{-1} .
$$
```