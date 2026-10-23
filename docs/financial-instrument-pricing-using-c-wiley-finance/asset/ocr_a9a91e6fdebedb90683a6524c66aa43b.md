**Definition 19.6** Let $f:[a,b]\to\mathbb{R}$ be a real-valued function and suppose we can find two constants $M$ and $\alpha$ such that $|f(x)-f(y)|\le M|x-y|^\alpha$, $\forall x,y\in[a,b]$ and $\alpha>0$. Then we say that $f$ satisfies a Lipschitz condition of order $\alpha$ and we write $f\in Lip(\alpha)$.

We take an example. Let $f(x)=x^2$ on the interval $[a,b]$. Then:

$$|f(x)-f(y)|=|x^2-y^2|=|(x+y)(x-y)|\le |x+y|\,|x-y|$$
$$\le (|x|+|y|)|x-y|$$
$$\le M|x-y|,\quad\text{where }M=2\max(|a|,|b|).$$

Hence, $f\in Lip(1)$. A concept related to Lipschitz continuity is contraction.

**Definition 19.7** Let $(X,d_1)$ and $(Y,d_2)$ be metric spaces where $d_1$ and $d_2$ are metrics. A transformation $T$ from $X$ into $Y$ is called a *contraction* if there exists a number $\lambda\in(0,1)$ such that:

$$d_2(T(x),T(y))<\lambda d_1(x,y)\quad\forall x,y\in X.$$

In general, a contraction maps a pair of points into another pair of points that are closer together. A contraction is always continuous.

The ability to discover and apply contraction mappings has considerable theoretical and numerical value. For example, it is possible to prove that SDEs have unique solutions by the application of fixed-point theorems (Bharucha-Reid, 1972; Tsokos and Padgett, 1974). Some specific examples are:

+   - Brouwer’s fixed-point theorem.
+   - Kakutani’s fixed-point theorem.
+   - Banach’s fixed-point theorem.
+   - Schauder’s fixed-point theorem.

Our interest here lies in the following fixed-point theorem.

**Theorem 19.1** *(Banach Fixed-Point Theorem)* Let $T$ be a contraction of a complete metric space $X$ into itself:

$$d(T(x),T(y))\le\lambda d(x,y),\quad \lambda\in(0,1).$$

Then $T$ has a unique fixed point $x$. Moreover, if $x_0$ is any point in $X$ and the sequence $\{x_n\}$ is defined recursively by the formula $x_n=T(x_{n-1})$, $n=1,2,\ldots$ then $\lim x_n=\bar{x}$ and:

$$d(\bar{x},x_n)\le\frac{\lambda}{1-\lambda}d(x_{n-1},x_n)\le\frac{\lambda}{1-\lambda}d(x_0,x_1).\tag{19.25}$$

In general, we assume that $X$ is a Banach space and that $T$ is a linear or nonlinear mapping of $X$ into itself. We then say that $x$ is a fixed point of $T$ if $Tx=x$.