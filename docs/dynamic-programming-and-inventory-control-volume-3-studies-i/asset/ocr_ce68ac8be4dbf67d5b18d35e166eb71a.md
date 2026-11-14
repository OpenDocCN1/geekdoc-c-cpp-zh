Introduce the vector in $R^L, X = (x, x_1, \cdots, x_{L-1})$. We can define the objective functional

(13.2.4) 
$$J_X(V) = \sum_{n=1}^\infty \alpha^{n-1} EC(v_n) + \sum_{j=1}^{L-1} \alpha^{j-1} El(y_j) + \sum_{n=1}^\infty \alpha^{n-2+L} El(y_{n+L-1}).$$

If $L=1$ the intermediary sum disappears and we recover the standard cost objective. This intermediary sum is a given function of $X$, not depending on the control. The rest depends on $X$ through $y_L$, so in fact depends on $X$ only through the number

(13.2.5) 
$$z = x + x_1 + \cdots + x_{L-1}.$$

Therefore we can write

$$J_X(V) = \sum_{j=1}^{L-1} \alpha^{j-1} El(y_j) + \bar{J}_z(V),$$

where

(13.2.6) 
$$ar{J}_z(V) = \sum_{n=1}^\infty \alpha^{n-1} EC(v_n) + \sum_{n=1}^\infty \alpha^{n-2+L} El(y_{n+L-1}).$$

Note that $z$ represents the initial inventory augmented by the sum of the pending deliveries. It is called the *inventory position*. Similarly, we use for $L \ge 2$

$$y_{n+L-1} = y_n + v_{n-1} + \cdots + v_{n-L+1} - (D_n + \cdots + D_{n+L-2}),$$

with the notation

$$v_0 = x_{L-1}; v_{-1} = x_{L-2} \cdots; v_{2-L} = x_1,$$

to define

$$\begin{aligned} z_n &= y_{n+L-1} + D_n + \cdots + D_{n+L-2} \\ &= y_n + v_{n-1} + \cdots + v_{n-L+1}, \end{aligned}$$

which is the inventory position at time $n$. We have $z_1 = z$. We then have the evolution

(13.2.7) 
$$z_{n+1} = z_n + v_n - D_n.$$

This proves that the process $z_n$ is adapted to the filtration $\mathcal{F}^{n-1}$. Next

$$l(y_{n+L-1}) = l(z_n - (D_n + \cdots + D_{n+L-2})).$$

But $D_n, \cdots, D_{n+L-2}$ are independent from $z_n$. Therefore

$$\alpha^{L-1} El(y_{n+L-1}) = E\bar{l}(z_n),$$

where

(13.2.8) 
$$\bar{l}(x) = \alpha^{L-1} El\left(x - \sum_{j=1}^{L-1} D_j\right).$$

We can then write

(13.2.9) 
$$\bar{J}_z(V) = \sum_{n=1}^\infty \alpha^{n-1} EC(v_n) + \sum_{n=1}^\infty \alpha^{n-1} E\bar{l}(z_n).$$

The problem has been reduced to a standard one, replacing the inventory with the inventory position, and the function $l(x)$ with $\bar{l}(x)$.