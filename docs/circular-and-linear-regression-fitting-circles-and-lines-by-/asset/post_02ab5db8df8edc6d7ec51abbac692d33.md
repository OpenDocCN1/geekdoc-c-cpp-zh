
### Notation

$\sigma_i^- = \begin{cases} 1/\sigma_i & \text{if } \sigma_i > 0 \\ 0 & \text{if } \sigma_i = 0 \end{cases}$

For probability, we use the following notation:

- $Prob(A)$ denotes the probability of an event $A$.
- $\mathbb{E}(X)$ denotes the mean value of a random variable $X$.
- $Var(X)$ denotes the variance of a random variable $X$.
- $Cov(X, Y)$ denotes the covariance of random variables $X$ and $Y$.
- $N(\mu, \sigma^2)$ denotes a normal random variable with mean $\mu$ and variance $\sigma^2$.
- $X_n \overset{L}{\to} X$ denotes the weak convergence of random variables, i.e., the convergence of the distribution functions of $X_n$ to the distribution function of $X$ at every point where the latter is continuous.
- $\mathcal{O}_p(\sigma^k)$ denotes a random variable, $X$, that may depend on $\sigma$ and such that $\sigma^{-k}X$ is bounded in probability; i.e., such that for any $\varepsilon > 0$ there exists $A_{\varepsilon} > 0$ such that $Prob\{\sigma^{-k}X > A_{\varepsilon}\} < \varepsilon$ for all $\sigma > 0$.

For statistics, we use the following notation:

- Given a sample $x_1, \ldots, x_n$ we denote its sample mean by $\bar{x} = \frac{1}{n} \sum_{i=1}^n x_i$.
- We conveniently extend the above sample mean notation as follows:
$$\bar{\bar{x}} = \frac{1}{n} \sum x_i^2, \quad \bar{\bar{xy}} = \frac{1}{n} \sum x_i y_i, \quad \text{etc.}$$
- $\Theta$ usually denotes the vector of unknown parameters, and $\theta_1, \theta_2, \ldots$ its components. For example, $a$ and $b$ are the parameters of an unknown line $y = a + bx$.
- We use tildas for the true values of the unknown parameters, i.e., we write $\tilde{\Theta} = (\tilde{\theta}_1, \tilde{\theta}_2, \ldots)$. For example, $\tilde{a}$ and $\tilde{b}$ are the true values of the parameters $a$ and $b$.
- We use 'hats' for estimates of the unknown parameters, i.e., we write $\hat{\Theta} = (\hat{\theta}_1, \hat{\theta}_2, \ldots)$. For example, $\hat{a}$ and $\hat{b}$ denote estimates of the parameters $a$ and $b$.
- MLE is an abbreviation for Maximum Likelihood Estimate. For example, we write $\hat{a}_{MLE}$ for the MLE of the parameter $a$.
- $bias(\hat{a}) = \mathbb{E}(\hat{a}) - \tilde{a}$ denotes the bias of an estimate $\hat{a}$. An estimate is unbiased if its bias is zero.
- MSE is the Mean Squared Error (of an estimate). For example,

$$MSE(\hat{a}) = \mathbb{E}[(\hat{a} - \tilde{a})^2] = Var(\hat{a}) + [bias(\hat{a})]^2$$

- For a parameter vector $\Theta$, the MSE is a matrix
\[
\begin{gathered}
\operatorname{MSE}(\hat{\Theta}) = \mathbb{E}\left[\left(\hat{\Theta} - \Theta\right)\left(\hat{\Theta} - \Theta\right)^T\right] \\
= \operatorname{Cov}(\hat{\Theta}) + \left[\operatorname{bias}(\hat{\Theta})\right]\left[\operatorname{bias}(\hat{\Theta})\right]^T
\end{gathered}
\]
where $\operatorname{Cov}(\hat{\Theta})$ stands for the covariance matrix of the estimate $\hat{\Theta}$.

## List of Figures

- 0.1 The Brogar Ring on Orkney Islands [15, 178]. The stones are marked by pluses; the fitted circle is the dotted line. xii
- 0.2 Reflection coefficients in microwave engineering [15]. The observed values are marked by stars; the fitted circle is the dashed line. xiii
- 0.3 A typical arc drawn by pencil with a profile gauge from a circular wheelmade antefix. xiv
- 0.4 A fragment of the arc shown in Fig. 0.3. xiv
- 0.5 The structure of the book. xvii
- 1.1 Ordinary regression minimizes the sum of squares of vertical distances: a cubic polynomial fitted to 10 data points. 2
- 1.2 50 data points (marked by dots) are fitted by two methods: the regression of $y$ on $x$ is the lower line and the regression of $x$ on $y$ is the upper line. Their slopes are 0.494 and 0.508, respectively. 5
- 1.3 Orthogonal regression minimizes the sum of squares of orthogonal distances. 7
- 1.4 The regression of $y$ on $x$ minimizes the sum of squares of vertical distances (top); the regression of $x$ on $y$ does the same with horizontal distances (middle); the orthogonal regression minimizes the sum of squares of orthogonal distances (bottom). 11
- 1.5 The EIV fit minimizes the sum of squares of "skewed" distances from the data points to the line. Here $\kappa = 2$. 12
- 1.6 Projection of the point $\mathscr{X}$ onto the quadratic manifold $\mathbb{P}$. 14
- 1.7 The true points location and the noise level in our experiment. 17
- 1.8 The average estimate $\hat{\beta}_M$ over $k$ randomly generated samples (solid line), as $k$ runs from 1 to $10^6$. The true slope $\hat{\beta} = 1$ is marked by the dashed line. The average estimate $\hat{\beta}_L$ is the dotted line, it remains stable at level 0.52, systematically underestimating $\beta$. 18
- 1.9 Two algorithms minimizing a function $F(x)$. One makes shorter steps and converges to a local minimum. The other makes longer steps and converges to the global minimum. 21
- 1.10 Two algorithms minimizing a function $F(x)$ with a unique minimum. One approaches it fast (from the left) and arrives in a vicinity of the minimum in 5–10 steps. The other moves very slowly (from the right); it may take 100 or 1000 iterations to get near the minimum. 22
- 1.11 The graph of an explicit nonlinear function $y = g(x)$ (left). After rotation, the same curve (right) does not represent any explicit function. 23
- 2.1 Parameters $\phi$ and $C$ of a straight line. 27
- 2.2 A line $\mathbb{L}$ not crossing the bounding box $\mathbb{B}$. 29
- 2.3 A horizontal solid line fitted to four points (pluses) and a vertical dashed line fitted to four other points (crosses). 30
- 2.4 The ratios $r_1$ (dashed line) and $r_2$ (solid line), as functions of $\sigma/L$. Here $n = 10$ (top) and $n = 100$ (bottom). 38
- 3.1 Data points (diamonds) are sampled along a very small arc of a big circle. The correct fit (the solid line) and the wrong fit (the dashed line) have centers on the opposite sides of the data set. 49
- 3.2 Karimäki’s parameters $d$ and $\phi$. 50
- 3.3 Straightening a circular arc and shrinking a circle to a singleton. 54
- 3.4 A grey disk, $\mathbb{Q}$, is cut in half by a line, $\mathbb{P}$. 57
- 3.5 A data set for which the objective function has four minima. 58
- 3.6 The objective function with four minima. 59
- 3.7 A simulated data set of 50 points. 61
- 3.8 The objective function $\mathscr{F}$ for the data set shown in Fig. 3.7 (large view). 62
- 3.9 The objective function $\mathscr{F}$ for the data set shown in Fig. 3.7 (a vicinity of the minimum). 62
- 3.10 A grey-scale contour map of the objective function $\mathscr{F}$. Darker colors correspond to smaller values of $\mathscr{F}$. The minimum is marked by a cross. 63
- 3.11 Functions $f_0(\phi)$ (dashed line) and $f_1(\phi)$ (solid line) for a randomly generated data set. 66
- 3.12 Best circle beats the best line despite $\overline{\mathbf{xy}} = 0$. 68
- 4.1 The level curves of $\mathcal{L} (\mathbf{a} + \mathbf{h})$ are concentric ellipses (solid ovals), the boundaries of trust regions are dashed circles around $\mathbf{a}$. 77
- 4.2 Two versions of the Levenberg-Marquardt circle fit with initial guess at $(1, 1)$: the full version (the solid line with star markers) and the reduced one (the dashed line with diamond markers) converge to the same limit in 7 steps; here 20 simulated points are marked by crosses. 81
- 4.3 Alternative minimization with respect to $x$ and $y$, separately. 87
- 4.4 The Späth algorithm with initial guess at $(1, 1)$ takes 200 iterations (diamonds) to converge, while the Levenberg-Marquardt circle fit makes only 7 iterations (stars); here 20 simulated points are marked by crosses. 88
- 4.5 The Landau algorithm with initial guess at $(1, 1)$ takes 700 iterations (diamonds) to converge, while the Levenberg-Marquardt circle fit reaches the goal in 5 iterations (stars); here 20 simulated points are marked by crosses. 89
- 4.6 Three algorithms converge along different routes. 90
- 4.7 Three algorithms move to the right, away from the true circle (along the escape valley) and diverge. The Levenberg-Marquardt circle fit dashes fast, in three steps (marked by stars) it jumps beyond the picture's boundaries. The Späth method makes 50 steps (diamonds) before escaping, and the Landau scheme crawls in 1000 steps (circular markers that quickly merge into a solid strip) before reaching the top edge; here 20 simulated points are marked by crosses. 92
- 4.8 Three different itineraries of the Chernov-Lesort procedure. 94
- 5.1 The distance $d_i$ from $(x_i, y_i)$ to the nearest point and $D_i$ to the farthest point on the circle. 102
- 5.2 Perpendicular bisector $L_{ij}$ of the chord $P_i P_j$ passes through the center $(a, b)$. 103
- 5.3 Four samples, each of 20 points (marked by crosses), along different arcs of the unit circle $x^2 + y^2 = 1$. The Kåsa fit is the solid circle; the geometric fit is the dotted circle. 105
- 5.4 13 data points (crosses) form a symmetric pattern stretching along a horizontal line (the $x$ axis). The best fit is obviously the $x$ axis itself; the Kåsa method returns a circle that is far from the best fit. 105
- 5.5 The true arc (solid lines) and the arc after its radius is halved (dashed lines). 106
