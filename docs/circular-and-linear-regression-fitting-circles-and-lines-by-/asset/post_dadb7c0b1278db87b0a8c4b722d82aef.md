
## 4.9 Convergence of iterative algorithms

Scheme:

$$
\begin{aligned}
R_{\text{new}} & = \bar{r} \\
a_{\text{new}} & = -\bar{u} R_{\text{new}} \quad\quad \quad\quad \quad (4.37) \\
b_{\text{new}} & = -\bar{v} R_{\text{new}}
\end{aligned}
$$

where \( \vec{r}, \vec{u}, \vec{v} \) are computed by using the previous iteration. This is a variant of the so-called *fixed point method*, see below.

![](img/86db288e3c266985d1648282179ae4b5_122_0.png)

Figure 4.5 *The Landau algorithm with initial guess at* \((1,1)\) *takes* 700 *iterations* (diamonds) *to converge, while the Levenberg-Marquardt circle fit reaches the goal in* 5 *iterations* (stars); *here* 20 *simulated points are marked by crosses.*

**Fixed point schemes.** A fixed point scheme is one of the simplest ways of solving nonlinear equations. Given an equation \(f(x) = 0\), one first transforms it into \(x = g(x)\) with some function \(g(x)\), and then tries to estimate a root, call it \(x^*\), by iterations \(x_{n+1} = g(x_n)\). If this method converges at all, its limit is necessarily a root of \(x = g(x)\), i.e., \(f(x) = 0\).

However, the convergence depends on the function \(g\). The method converges to \(x^*\) if \(|g'(x^*)| < 1\) and diverges if \(|g'(x^*)| > 1\) (similar conditions exist for multidimensional variables \(x \in \mathbb{R}^n\), see [112]). Since such conditions are in practice hard to verify, the method is generally not very reliable. In other words, one has to carefully find a representation \(x = g(x)\) of the given equation \(f(x) = 0\) for which \(|g'| < 1\) at and near the desired root.

Besides, the speed of convergence of a fixed point method is linear (unless \(g'(x^*) = 0\), which rarely happens), while the convergence of the Gauss-Newton method and its Levenberg-Marquardt modification is nearly quadratic. The linear convergence means that if $\hat{\boldsymbol{\theta}}_k$ is the parameter approximation at the $k$'s iteration and $\boldsymbol{\theta}^{*} = \lim_{k \rightarrow \infty} \boldsymbol{\theta}_k$, then

$$ \|\boldsymbol{\theta}_{k+1} - \hat{\boldsymbol{\theta}}^{*}\| \leq c\|\boldsymbol{\theta}_k - \hat{\boldsymbol{\theta}}^{*}\| $$

with some constant $c < 1$.

**Speed of convergence.** Landau [119] has estimated the convergence constant $c$ for his method and showed that $0.5 \leq c < 1$. In fact, $c \approx 0.5$ when the data are sampled along the entire circle, $c \approx 0.9$ when data are sampled along half a circle, and $c$ quickly approaches one as the data are sampled along smaller arcs. In practice, the performance of the Landau algorithms (as is typical for fixed point schemes) is very sluggish – it happens to be even slower than the Späth method.

A typical example is shown in Fig. 4.5, where 20 points are randomly generated along a $130^{\circ}$ arc of the unit circle $x^{2} + y^{2} = 1$ with a Gaussian noise at level $\sigma = 0.05$. The Levenberg-Marquardt fit starts at $a = b = 1$ and converges to the (unique) minimum of $\mathscr{F}$ at $\hat{a} = 0.014$ and $\hat{b} = -0.020$ in 5 iterations (marked by stars). The Landau algorithm, on the contrary, took almost 700 iterations (marked by diamonds) to converge.

The Späth and Landau methods sometimes take quite different routes to converge to the minimum, see another example in Fig. 4.6, where 20 points are randomly generated along a $130^{\circ}$ arc of the unit circle $x^{2} + y^{2} = 1$ with a Gaussian noise at level $\sigma = 0.05$, and the initial guess is again $a = b = 1$. The Levenberg-Marquardt circle goes straight to the limit point and converges in 5 iterations. The Späth method (diamonds) approaches the limit point from the right in about 100 iterations, and the Landau method (circular markers) comes from the left (taking about 400 steps).

![](img/86db288e3c266985d1648282179ae4b5_123_0.png)

Figure 4.6: Three algorithms converge along different routes.

**Last remarks.** We only described the most popular algorithms for geometric circle fitting. Some authors use “heavy artillery,” such as the Nelder-Mead simplex method [68]. Others use various heuristics, such as Fisher scoring [33]. We do not include them here.

> ²For example, the equation \(x^3 - 10 = 0\) can be transformed into \(x = x^3 + x - 10\) or \(x = 10/x^2\). There are infinitely many ways to write it as \(x = g(x)\) with different g's.

## 4.10 Divergence and how to avoid it

The previous sections reviewed the most popular geometric circle fitting algorithms. They perform well when the initial guess is chosen close enough to the minimum of the objective function \( \mathscr{F} \). They can also cope with the initial guesses picked far from the minimum (although sometimes iterations move slowly). But there is one condition under which all of them fail.

**Divergence in the escape valley.** The failure occurs if the initial guess (or one of the iterations) falls into the escape valley described in Section 3.7. Then all the iterative algorithms are driven away from the minimum of \( \mathscr{F} \) and diverge.

An example is shown in Fig. 4.7, where 20 points are randomly generated along a 130\(^{\circ}\) arc of the unit circle \( x^{2} + y^{2} = 1 \) with a Gaussian noise at level \( \sigma = 0.05 \). The Levenberg-Marquardt fit and the Späth and Landau methods start at \( a = 1.1 \) and \( b = 0.1 \). All of them move in the wrong direction (to the right) and diverge (the figure shows only the initial stage of divergence). The reason for their failure is that the initial guess happens to be in the escape valley that descends to the right, all the way to the horizon. (The divergence of the Landau algorithm may have no clear cause, as it is purely heuristic and does not use the derivatives of the objective function \( \mathscr{F} \), but it follows suit anyway.)

We cannot blame iterative algorithms for their divergence here; they do what they are supposed to: detect the shape of the function at the current locality and move in the direction where the function seems to decrease. They have no way of knowing that they are in the escape valley stretching to the horizon, while the true minimum is left behind, “over the ridge.”

We have established in Section 3.7 that the escape valley exists for practically every data set. However, if the data points are sampled along the full circle or a large arc, then the escape valley lies far from the true circle, and the iterative algorithms can operate safely. On the other hand, if the data points are clustered along a small arc, then the escape valley is right next to the data.

For example, the set shown in Fig. 3.1 is sampled along an arc (solid line) whose center lies above the \( x \) axis. Choosing the initial center below the \( x \) axis places the iterative procedure into the escape valley and sends it away to infinity.

One way to guard the iterative procedures against the escape valley is to use the rules for handling the singular cases described in Section 3.9. Alternatively, the iterative scheme can be initialized by any algebraic circle fit presented in the next section (which is the most common strategy in practice). Then the initial guess is almost automatically placed on the “right” side of the data set and the procedure avoids the escape valley (however, there are some exotic exceptions; see the W-example in Section 5.13).

![](img/86db288e3c266985d1648282179ae4b5_125_0.png)

On the other hand, if one has to use bad (arbitrarily chosen) initial guesses (for example, we had to do this in our experiment determining the typical number of local minima, cf. Section 3.6), then one is basically at the mercy of the initial choice.

**Chernov-Lesort algorithm.** In an attempt to bypass the divergence problem Chernov and Lesort [43] developed a rather unusual circle fitting algorithm, which converges to a minimum of the objective function from any (!) starting point. The trick is to adopt a different parametrization scheme in which escape valleys simply do not exist! Recall that the algebraic equation

$$A(x^2 + y^2) + Bx + Cy + D = 0$$

with four parameters $A, B, C, D$ satisfying the constraint

$$B^2 + C^2 - 4AD = 1 \tag{4.38}$$

describes all circles on the $xy$ plane and, in addition, all straight lines. Circles correspond to $A \neq 0$ and lines to $A = 0$.

We have proved in Section 3.2 that if the data set lies within a bounding box $\mathfrak{B}$, then the minimum of the objective function $\mathscr{F}$ is restricted to a bounded region in the parameter space

$$|A| < A_{\max}, |B| < B_{\max}, |C| < C_{\max}, |D| < D_{\max} \tag{4.39}$$
