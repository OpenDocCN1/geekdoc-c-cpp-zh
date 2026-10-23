
let alone Taylor expansion. In this case, the boundary-value problem in the above (strong) form may have no solution at all. The correct (well-posed) form should use integration rather than differentiation. This form is called the "weak" formulation, because it requires weaker assumptions than the original "strong" formulation. In particular, it no longer requires u(x, y) to have continuous derivatives but only that the flux vector $(P u_x, Q u_y)$ be continuous. The weak formulation is the basis of the most useful finite-element discretization method.

In the original strong formulation of the diffusion problem as a PDE accompanied by boundary conditions, $P u_x$ and $Q u_y$ must be differentiable. These assumptions may be too strong. For example, when P and Q are discontinuous, $P u_x$ and $Q u_y$ may be continuous but not differentiable. In such cases, the strong formulation may have no mathematical solution at all.

Still, the physical phenomenon does exist and needs to be formulated mathematically. The mathematical model must be well posed in the sense that it has a unique solution, just like the original physical phenomenon. This model is provided by the weak formulation described below.

The weak formulation is based on integration rather than differentiation. Thus, it only requires the flux $(P u_x, Q u_y)$, as well as K and F, be square-integrable over $\Omega$ with respect to the area element $dxdy$. (We say that a function w is square-integrable over $\Omega$ if its square $w^2$ is integrable over $\Omega$: that is, $\int_{\Omega} w^2 \, dxdy < \infty$.) We also assume that $\alpha$ and G are square-integrable over $\Gamma$ with respect to the length element $ds$.

Let us now define the weak formulation in detail. For every function v that is square-integrable over $\Omega$ with respect to the area element $dxdy$ (and also square-integrable over $\Gamma$ with respect to the length element $ds$), define the linear functional $f(v)$ by

$$
f(v) = \int_{\Omega} F v \, dxdy + \int_{\Gamma} G v \, ds.
$$

For every two functions v and w with square-integrable derivatives in $\Omega$, define the symmetric bilinear form $a(v, w)$ by

$$
a(v, w) = \int_{\Omega} (P v_x w_x + Q v_y w_y) \, dxdy + \int_{\Omega} K v w \, dxdy + \int_{\Gamma} \alpha v w \, ds.
$$

The weak formulation is obtained from the strong one by using Green’s divergence formula in the PDE and boundary conditions as follows. Let v be a function in $\Omega$ that vanishes on $\Gamma_0$ and has square-integrable derivatives in $\Omega$. Then, we have, from Green’s formula and the boundary conditions,

$$
\begin{aligned}
\int_{\Gamma} (G v - \alpha u v) \, ds &= \int_{\Gamma} (P u_x v n_1 + Q u_y v n_2) \, ds \\
&= \int_{\partial \Omega} (P u_x v n_1 + Q u_y v n_2) \, ds \\
&= \int_{\Omega} ((P u_x)_x + (Q u_y)_y) v \, dxdy \\
&= \int_{\Omega} ((P u_x)_x v + (Q u_y)_y) v \, dxdy \\
&\quad + \int_{\Omega} (P u_x v_x + Q u_y v_y) \, dxdy.
\end{aligned}
$$

Using the PDE itself, we have

$$
\begin{aligned}
f(v) &= \int_{\Omega} Fv\,dx\,dy + \int_{\Gamma} Gv\,ds \\
&= -\int_{\Omega}\big((Pu_x)_x+(Qu_y)_y\big)v\,dx\,dy \\
&\quad + \int_{\Omega} Kuv\,dx\,dy + \int_{\Gamma} Gv\,ds \\
&= \int_{\Omega}(Pu_xv_x+Qu_yv_y)\,dx\,dy \\
&\quad + \int_{\Omega} Kuv\,dx\,dy + \int_{\Gamma} \alpha uv\,ds \\
&= a(u,v).
\end{aligned}
$$

The problem in its weak formulation is thus as follows: find a function $u$ that agrees with $G$ on $\Gamma_0$ and has square-integrable derivatives in $\Omega$ such that, for every function $v$ that vanishes on $\Gamma_0$ and has square-integrable derivatives in $\Omega$,

$$
a(u,v)=f(v).
$$

From the above discussion, it is clear that a solution to the strong formulation (if it exists) must also be a solution to the weak formulation. In Sections 11.3 to 11.6 below, it is shown that the weak formulation is more suitable than the strong one, because it is well posed in the sense that it has a unique solution, just like the original physical phenomenon. Indeed, a realistic physical phenomenon must have a solution, or it wouldn't exist. Furthermore, the solution must be unique, or the phenomenon would be unstable in the sense that every tiny perturbation in the initial or boundary data may produce enormous changes in the entire physical state, which is highly unlikely in realistic processes.

The mathematical model that approximates the original physical phenomenon must also be stable and well posed. Otherwise, every tiny inaccuracy in the model may result in an enormous error in the solution. In what follows, we show that the weak formulation is indeed well posed and is thus suitable for modeling real physical situations.

## 11.3 The Minimization Problem

In this section, we show that the above weak formulation is equivalent to the following minimization problem: consider the functional

$$
g(v)=\frac{1}{2}a(v,v)-f(v).
$$

From the family of functions that agree with $G$ on $\Gamma_0$ and have square-integrable derivatives in $\Omega$, pick the function $u$ for which $g(u)$ is minimal. This function is referred to as the solution to the minimization problem.

Later on, we will show that this minimization problem has a unique solution; this implies that the weak formulation (which is equivalent to it) is indeed well posed.

Let us assume that the functions P, Q, K, and $\alpha$ are bounded and nonnegative, so $a(u, v) \ge 0$ for every function v. In order to show the equivalence between the weak formulation and the minimization problem, we have to show that every solution to the one also solves the other. Assume first that u solves the minimization problem, and let us show that it also solves the weak formulation. Indeed, if u were not a solution to the weak formulation, then there would exist a function v that vanishes on $\Gamma_0$ and has square-integrable derivatives in $\Omega$, and yet $a(u, v) \ne f(v)$.

$a(u, v) \ne f(v)$.

Without loss of generality, we can assume that $a(u, v) < f(v)$. (Otherwise, just replace v by $-v$.) Let $\epsilon$ be a positive parameter. For sufficiently small $\epsilon$, we have

$$
\begin{aligned}
g(u + \epsilon v) &= \frac{1}{2} a(u + \epsilon v, u + \epsilon v) - f(u + \epsilon v) \\
&= \frac{1}{2} a(u, u) + \epsilon a(u, v) + \frac{1}{2} \epsilon^2 a(v, v) - f(u) - \epsilon f(v) \\
&= g(u) + \epsilon (a(u, v) - f(v)) + \frac{1}{2} \epsilon^2 a(v, v) < g(u),
\end{aligned}
$$

which contradicts the assumption that u minimizes g. Thus, u must also solve the weak formulation.

Conversely, assume now that u solves the weak formulation, and let us show that it must also solve the minimization problem. Indeed, let w be some function that agrees with G on $\Gamma_0$ and has square-integrable derivatives in $\Omega$, and define $v = w - u$. Since v vanishes on $\Gamma_0$, we have

$$
\begin{aligned}
g(w) &= \frac{1}{2} a(w, w) - f(w) \\
&= \frac{1}{2} a(u + v, u + v) - f(u + v) \\
&= \frac{1}{2} a(u, u) + a(u, v) + \frac{1}{2} a(v, v) - f(u) - f(v) \\
&= g(u) + \frac{1}{2} a(v, v) \ge g(u),
\end{aligned}
$$

which implies that u also solves the minimization problem. This completes the proof that the weak formulation and the minimization problem are indeed equivalent to each other.

## 11.4 The Coercivity Property

In this section, we discuss the coercivity property of the quadratic form $a(w, w)$. This property is most useful for proving the existence and uniqueness of the solution to the minimization problem defined above.

For this purpose, however, we need some more assumptions:

1. The domain $\Omega$ is connected (every two points in it can be connected to each other by a curve that lies in it).
2. There is a constant $\eta > 0$ such that $P \ge \eta$ and $Q \ge \eta$ in $\Omega$.
3. Either $\Gamma_0$ is nonempty, or $\int_{\Gamma} \alpha \, ds > 0$, or $\int_{\Omega} K \, dx \, dy > 0$.

These assumptions, in conjunction with the assumptions made in Section 11.3, guarantee that the quadratic form $a(w, w)$ is coercive in the sense that if w is a function with square-integrable derivatives in $\Omega$ such that $a(w, w) = 0$ and $w(r) = 0$ at some reference point $r \in \Omega$, then w must be the zero function $w \equiv 0$. Indeed, for every point $q \in \Omega$, $w(q)$ takes the form

$$
w(q) = w(r) + \int_{r}^{q} (w_x s_1 + w_y s_2) \, ds,
$$

where the integral is taken along some curve connecting r to q in $\Omega$, and $(s_1, s_2)$ is the unit vector tangent to this curve. But, from the assumptions, it is clear that both $w_x$ and $w_y$ must vanish on the curve, so the integral along it vanishes as well, which implies that $w(q) = 0$ as well.

So far, we have assumed the existence of the reference point r for which $w(r) = 0$. In some cases, however, this assumption can be relaxed. For example, consider the case in which $\Gamma_0$ is empty. According to the assumptions at the beginning of this section, we must then have $\int_{\Gamma} \alpha \, ds > 0$ or $\int_{\Omega} K \, dx \, dy > 0$. In either case, the required reference point r must exist: in the first case it lies in the support of $\alpha$ in $\Gamma$, whereas in the second case it lies in the support of K in $\Omega$. (The support of a function is the set of points where the function is nonzero.)

When $\Gamma_0$ is nonempty, we must explicitly assume the existence of the reference point r. However, as we’ll see below, we are mostly interested in functions w that vanish on $\Gamma_0$. For such functions, r could be any point in $\Gamma_0$.

## 11.5 Existence Theorem

Here, we show that the minimization problem indeed has a solution. In the next section, we’ll show that this solution is also unique. Together, these sections show that the minimization problem (and, hence, also the weak formulation) is indeed well posed.

In order to show the existence of a solution to the minimization problem, let us reformulate it in a slightly different way. By the same reasoning as in the previous section, one can also show that $\int_{\Omega} (u^2 + u_x^2 + u_y^2) \, dx \, dy$ cannot be too large (where u is some solution to the minimization problem, if it exists). Indeed, if it is large, then $a(u, u)$ will be large as well. As a result, g(u) will also be large, because $a(w, w)$ grows quadratically with w, whereas $f(w)$ grows only linearly. This contradicts the fact that u minimizes g. Therefore, there must exist a sufficiently large constant $L_0$ for which

$$
\int_{\Omega} (u^2 + u_x^2 + u_y^2) \, dx \, dy \le L_0
$$

for any solution u to the minimization problem, if it exists.
