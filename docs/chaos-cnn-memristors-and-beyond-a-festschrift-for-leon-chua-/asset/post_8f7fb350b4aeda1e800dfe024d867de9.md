
(ii) On \((t_{i-1}, t_i)\), \(2 \le i \le N\):

To define \(\psi(t)\) on each \((t_{i-1}, t_i)\), we repeat the following process for \(2 \le i \le N\). Let
\[
\psi(t) := (q_i - \tilde{q}_{i-1})(t - t_{i-1})/h, \quad t \in (t_{i-1}, t_i),
\]
then \(\tilde{q}_{i-1} + \psi(t) \in V\), \(t \in (t_{i-1}, t_i)\). Therefore,
\[
\sup_{s \in (t_{i-1}, t_i)} |f(\tilde{q}_{i-1} + \psi(s))| \le C.
\]
Consider (31) with \(t \in (t_{i-1}, t_i)\) and \(y(t_{i-1}) = \tilde{q}_{i-1}\), then we have
\[
y(t) - (\tilde{q}_{i-1} + \psi(t)) = \int_{t_{i-1}}^t \bigl(f(y(s)) - f(\tilde{q}_{i-1} + \psi(s))\bigr)\,ds + \int_{t_{i-1}}^t f(\tilde{q}_{i-1} + \psi(s))\,ds,
\]
which implies
\[
|y(t) - (\tilde{q}_{i-1} + \psi(t))| \le \int_{t_{i-1}}^t |f(y(s)) - f(\tilde{q}_{i-1} + \psi(s))|\,ds + \int_{t_{i-1}}^t |f(\tilde{q}_{i-1} + \psi(s))|\,ds
\]
\[
\le \int_{t_{i-1}}^t L|y(s) - (\tilde{q}_{i-1} + \psi(s))|\,ds + hC.
\]
By Gronwall inequality, we have
\[
|y(t_i) - (\tilde{q}_{i-1} + \psi(t_i))| \le hC e^{Lh} < \epsilon/2,
\]
provided \(h\) is small enough. Denote by \(\tilde{q}_i := y(t_i)\). At the final stage \(i = N\), we have
\[
|y(T) - (\tilde{q}_{i-1} + \psi(T))| = |y(T) - q| < \epsilon/2.
\]
Thus we have \(|S(T, \dot{\psi})x_0 - q| < \epsilon\). The proof is complete.

We will prove that with positive probability the solution \(\phi(t,\omega)p\) of (24) can be approximated by solution \(S(t, \dot{\psi})p\) of (31) in any finite time interval and any initial point \(p\).

**Lemma 4.** Assume (H3)--(H4) hold. Given a piecewise continuous \(\dot{\psi}\), \(T > 0\) and \(\gamma > 0\), the set \(A_\gamma\) defined by
\[
A_\gamma := \left\{ \omega : \sup_{p \in \mathbb{R}^n} \sup_{t \in [0,T]} |S(t, \dot{\psi})p - \phi(t,\omega)p| < \gamma \right\}, \tag{34}
\]
has \(\mathbb{P}(A_\gamma) > 0\).

**Proof.** According to Lemma 1 and Lemma 2, \(S(t, \dot{\psi})p\) and \(\phi(t,\omega)p\) are defined for \(t \in [0,T]\). From (24) and (31) we have
\[
d(x - y) = (f(x) - f(y))dt - \sigma \dot{\psi}(t)dt + \sigma dW(t). \tag{35}
\]
We may assume \(\psi(0) = 0\) since it doesn't affect the solution of (31). Let \(\tilde{W}(t) := W(t) - \psi(t)\), \(t \in [0,T]\), then we have
\[
d\tilde{W} = -\dot{\psi}(t)dt + dW. \tag{36}
\]
By Girsanov's Theorem ([19]), \(\tilde{W}\) is a Brownian motion under probability \(\tilde{\mathbb{P}}\), where
\[
\frac{d\tilde{\mathbb{P}}}{d\mathbb{P}} = \exp\left(\int_0^T \dot{\psi}(s) \cdot dW(s) - \frac12 |\dot{\psi}(s)|^2 ds\right) > 0. \tag{37}
\]
Let \(\tilde{\Lambda}_\varepsilon := \{\omega : \sup_{t \in [0,T]} |\tilde{W}(t,\omega)| < \varepsilon\}\) and \(\Lambda_\varepsilon := \{\omega : \sup_{t \in [0,T]} |W(t,\omega)| < \varepsilon\}\), then \(\tilde{\mathbb{P}}(\tilde{\Lambda}_\varepsilon) > 0\), which implies \(\mathbb{P}(\tilde{\Lambda}_\varepsilon) > 0\) by (37). It follows that for \(\omega \in \tilde{\Lambda}_\varepsilon\),
\[
|\phi(t,\omega)p - S(t, \dot{\psi})p| \le \int_0^t |f(\phi(s,\omega)p) - f(S(s, \dot{\psi})p)|\,ds + \sigma |\tilde{W}(t)|
\]
\[
\le \int_0^t L|\phi(s,\omega)p - S(s, \dot{\psi})p|\,ds + \sigma \varepsilon. \tag{38}
\]
By Gronwall inequality, we have
\[
\sup_{p \in \mathbb{R}^n} \sup_{t \in [0,T]} |S(t, \dot{\psi})p - \phi(t,\omega)p| < \sigma \varepsilon e^{LT}, \quad \omega \in \tilde{\Lambda}_\varepsilon.
\]
The assertion follows by choosing \(\varepsilon\) small enough.

**Proof of Theorem 3.** We still denote by \(\phi(t,\omega)\) the flow for (2) with piecewise constant diffusion \(\sigma(t)\) shown in Fig. 1. Let \(q_0\) be an initial point. We may assume \(B(p_i, \epsilon)\) lies in the stable manifold of \(p_i\) for \(i = 1, \dots, N\).

Let \(q_i \in \mathbb{R}^n\). For each \(1 \le i \le N\), by Lemma 3, there exists a piecewise continuous \(\dot{\psi}_i(t)\), \(t \in [S_i, T_i]\), such that the solution of
\[
dy^{(i)} = f(y^{(i)})dt + \sigma(t)\dot{\psi}_i dt, \quad y^{(i)}(S_i) = q_{i-1}, \tag{39}
\]
satisfying
\[
y^{(i)}(T_i) \in B(p_i, \epsilon/2).
\]
Since \(\sigma(t) = 0\) and \(y^{(i)}(T_i)\) lies in the stable manifold of \(p_i\), it follows that
\[
y^{(i)}(t) \in B(p_i, \epsilon/2), \quad t \in [T_i, S_{i+1}],
\]
Selecting \(q_i = y^{(i-1)}(S_{i-1})\), \(2 \le i \le N\), and let \(\dot{\psi}(t)\) be the piecewise continuous function defined by
\[
\dot{\psi}(t) = \begin{cases} \dot{\psi}_i(t), & t \in [S_i,T_i], \ 1 \le i \le N, \\ 0, & \text{otherwise.} \end{cases} \tag{40}
\]
Then we have
\[
S(t,\dot{\psi})q_0 \in B(p_i,\epsilon/2), \quad t \in [T_i,S_{i+1}], \quad 1 \le i \le N,
\]
By Lemma 4, the set
\[
\left\{\omega : \sup_{t\in[0,T]} |S(t,\dot{\psi})q_0 - \phi(t,\omega)q_0| < \epsilon/2 \right\}, \tag{41}
\]
has positive probability, which implies the set
\[
\Omega' := \{\omega : \phi(t,\omega)q_0 \in B(p_i,\epsilon_i), \ t \in [T_i,S_{i+1}], \ 1 \le i \le N\}, \tag{42}
\]
has \(\mathbb{P}(\Omega') > 0\). The proof is complete.

## 4. Numerical Examples

In this section, we demonstrate the ID method on four standard test examples for global optimization methods. They are designed to have many local minima which are similar to the global minima, and the local minima can easily trap the solutions. In all the experiments, we set the parameters \(\alpha = 10\), \(\gamma = 10\) and \(N = 10\).

### Problem 1. Penalized Shubert Function

Let
\[
g_1(x) = \sum_{i=1}^{5} i \cos((i+1)x + 1) \tag{43}
\]
be the standard Shubert function. Then the penalized Shubert function is defined by
\[
g(x) := g_1(x) + u(x,10,100,2) \tag{44}
\]
where \(u(x,a,k,m)\) is called the penalization function defined by
\[
u(x,a,k,m) := \begin{cases} k(x-a)^m, & x > a, \\ 0, & -a \le x \le a, \\ k(-x-a)^m, & x < -a. \end{cases} \tag{45}
\]
As shown in Fig. 2, the function \(g\) has 19 local minima in the region \(\{x : |x| < 10\}\) and three of them are global minima. One realization of the ID method gives the circled points, which are the convergent points of the gradient flow after the diffusion is turned off. It finds the global minimum in the middle.

![](img/039e7d3c23390584a66737067db8b75b_487_0.png)

*Fig. 2. Numerical experiment for Problem 3. The blue circles mark the convergent points at the non-diffusion step.*

### Problem 2. Two-Dimensional Penalized Shubert Function

It is defined by
\[
g(x,y) = \left\{\sum_{i=1}^{5} i \cos((i+1)x + 1)\right\} \times \left\{\sum_{i=1}^{5} i \cos((i+1)y + 1)\right\} + u(x,10,100,2) + u(y,10,100,2). \tag{46}
\]
It has 760 local minima in the region \(\{(x,y) : |x| < 10, |y| < 10\}\), and 18 of them are global minima as shown in Fig. 3. It also shows that an arbitrary realization of ID algorithm gives the circled points. Among them, it finds three global minima.

![](img/039e7d3c23390584a66737067db8b75b_488_0.png)

*Fig. 3. Numerical experiment for Problem 4. The black circles mark the convergent points at the non-diffusion step.*

### Problem 3. Two-Dimensional Penalized Shubert Function with Parameter \(\beta\)

It is defined by
\[
g(x,y) = \left\{\sum_{i=1}^{5} i \cos((i+1)x + 1)\right\} \times \left\{\sum_{i=1}^{5} i \cos((i+1)y + 1)\right\} + u(x,10,100,2) + u(y,10,100,2) + \beta[(x - 6.0835)^2 + (y + 5.8581)^2], \tag{47}
\]
where \(\beta > 0\) is a constant. The point \((x,y) = (6.0835, -5.8581)\) is a global minimizer of \(g\) with \(\beta = 0\). The function behaves roughly the same with the function considered in Problem 2, but has only one unique global minimizer at \((x,y) = (6.0853, -5.8581)\) as shown in Fig. 4. We show the results of convergent points (circled points) of an arbitrary ID realization. Similar to the previous problems, the ID method is able to find the global minima.

![](img/039e7d3c23390584a66737067db8b75b_488_1.png)

*Fig. 4. Numerical experiment for Problem 5. The black circles mark the convergent points at the non-diffusion step.*

### Problem 4. A Multi-Dimensional Function

Let
\[
g(x) = (\pi/n) \left\{ k \sin^2(\pi y_1) + \sum_{i=1}^{n-1} (y_i - A)^2[1 + k \sin^2(\pi y_{i+1})] + (y_n - A)^2 \right\}, \tag{48}
\]
where
\[
x = (x_1, \dots, x_n) \in \mathbb{R}^n, \quad y_i = 1 + (x_i - 1)/4, \quad i = 1, \dots, n, \quad k = 10, \quad A = 1.
\]
The function has roughly \(5^n\) local minima in the region \(\{(x_1,\dots,x_n) : |x_i| < 10, \ i = 1,\dots,n\}\) and a unique global minimum located at
\[
x_i = 1, \quad i = 1, \dots, n.
\]
For \(n = 3\), Fig. 5 is the projection plot of the graph of \(y = g(x_1,x_2,x_3)\) on the space \(x_3 = 1\), which illustrates the global minimizer is surrounded by many local minimizers. The 10 convergent points visited in a sequential order by an arbitrary ID realization for \(n = 3\) and \(n = 4\) are given in Table 1, respectively.

![](img/039e7d3c23390584a66737067db8b75b_488_2.png)

*Fig. 5. The projection plot of the graph of \(y = g(x_1,x_2,x_3)\) on the space \(x_3 = 1\) for Problem 6.*

The ID method finds the global minima for both cases. And the frequencies of visiting the global minimum are obviously higher than that of any other local minima.
