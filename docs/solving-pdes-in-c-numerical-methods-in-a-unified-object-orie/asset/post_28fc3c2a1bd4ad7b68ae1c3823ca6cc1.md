
![](img/1f293b0ceb2de964310ea7f941a1b580_330_0.png)

Figure 9.10. The Newton iteration converges rapidly to the desired root x of the convex function f.

## 9.12 Newton's Iteration for Scalar Functions

The Newton (or Newton–Raphson) iteration is a powerful tool for solving nonlinear equations. Let us introduce it first in the simplest case, the scalar case.

Let $f(x)$ be a scalar function of the scalar variable $x$. Assume that $f$ has at least one root $\tilde{x}$, for which it vanishes:

$$f(\tilde{x}) = 0.$$

The problem is to find a root $\tilde{x}$. To apply the Newton iteration, one must also assume that $f$ has a uniformly nonzero derivative $f'$ in a neighborhood of $\tilde{x}$, that is,

$$|f'(x)| \ge C_1, \quad x \in (\tilde{x} - \zeta, \tilde{x} + \zeta),$$

where $C_1$ and $\zeta$ are some positive constant numbers. To approximate the required root $\tilde{x}$, let us first pick an initial guess $x^{(0)}$. Unfortunately, $x^{(0)}$ may be a rather poor guess. To improve on it, let us define a better approximation to $\tilde{x}$, denoted by $x^{(1)}$. This is done by drawing the tangent to the graph of $f$ at the point $(x^{(0)}, f(x^{(0)}))$ (see Figure 9.10). The slope of this tangent is just the derivative of $f$ at $x^{(0)}$:

$$f'(x^{(0)}) = - \frac{f(x^{(0)})}{x^{(1)} - x^{(0)}}.$$

Because $x^{(1)}$ is not yet defined, one would like to place it in the left-hand side:

$$x^{(1)} - x^{(0)} = - \frac{f(x^{(0)})}{f'(x^{(0)})}$$

or

$$x^{(1)} = x^{(0)} - \frac{f(x^{(0)})}{f'(x^{(0)})}.$$

From Figure 9.10, it is clear that $x^{(1)}$ is indeed a better approximation to $\tilde{x}$ than $x^{(0)}$. By repeating this process, the Newton iteration can now be defined for every $i = 0,1,2,\ldots$ by

$$x^{(i+1)} = x^{(i)} - \frac{f(x^{(i)})}{f'(x^{(i)})}.$$

Under certain conditions discussed below, the Newton iteration converges rapidly to $\tilde{x}$. Thus, for sufficiently large $i$, the error at the $(i+1)$st iteration, $|x^{(i+1)} - \tilde{x}|$, is sufficiently small, so $x^{(i+1)}$ can be accepted as a sufficiently accurate approximation to $\tilde{x}$.

## 9.13 Superlinear Convergence

To show that the Newton iteration indeed converges rapidly to a root of $f$, let us also assume that all the approximants $x^{(i)}$ lie in $(\tilde{x} - \zeta, \tilde{x} + \zeta)$ and that $f$ also has a second derivative $f''$ that is bounded in magnitude by some constant $C_2$ in $(\tilde{x} - \zeta, \tilde{x} + \zeta)$ (e.g., $f$ is convex in the closed interval $[\tilde{x} - \zeta, \tilde{x} + \zeta]$). Using the Taylor expansion around $x^{(i)}$ (Section 5.11), we can then write $f(\tilde{x})$ in terms of $f$ and $f'$ at $x^{(i)}$ and $f''$ at an intermediate point $\xi$ that lies between $\tilde{x}$ and $x^{(i)}$:

$$0 = f(\tilde{x}) = f(x^{(i)}) + f'(x^{(i)})(\tilde{x} - x^{(i)}) + \frac{1}{2} f''(\xi)(\tilde{x} - x^{(i)})^2$$

or

$$f(x^{(i)}) = -f'(x^{(i)})(\tilde{x} - x^{(i)}) - \frac{1}{2} f''(\xi)(\tilde{x} - x^{(i)})^2.$$

By substituting this formula in the original Newton iteration, we have the error at the $(i+1)$st iteration in terms of the error at the $i$th iteration:

$$x^{(i+1)} - \tilde{x} = x^{(i)} - \frac{f(x^{(i)})}{f'(x^{(i)})} - \tilde{x}$$

$$= x^{(i)} - \tilde{x} + \frac{f'(x^{(i)})(\tilde{x} - x^{(i)}) + \frac{1}{2} f''(\xi)(\tilde{x} - x^{(i)})^2}{f'(x^{(i)})}$$

$$= \frac{f''(\xi)(\tilde{x} - x^{(i)})^2}{2 f'(x^{(i)})}.$$

With this interpretation, the Newton iteration is defined in the same way as in Section 9.12 above, except that the division by $f'(x^{(i)})$ is now interpreted as the multiplication from the left by the inverse of the Jacobian, $(f'(x^{(i)}))^{-1}$:

$$x^{(i+1)} = x^{(i)} - (f'(x^{(i)}))^{-1} f(x^{(i)})$$

Clearly, because the Jacobian of $f$ depends on $x^{(i)}$, it must be recalculated before each iteration. Furthermore, it must have an inverse matrix; in other words, it must be nonsingular (invertible). Fortunately, this inverse matrix doesn’t have to be calculated explicitly. Instead, one only needs to solve a linear system in which the Jacobian serves as the coefficient matrix. This can be done in an inner iteration, using one of the iterative methods from Chapter 17.

Furthermore, with the present interpretation, the error estimate in Section 9.13 is still valid, provided that $f'^{-1}$ and the individual Hessian components in $f''$ are bounded in a neighborhood of $\tilde{x}$. Indeed, the Taylor expansion around $x^{(i)}$ used in Section 9.13 can be adapted to the present vector function to read

$$f(\tilde{x}) = f(x^{(i)}) + f'(x^{(i)})(\tilde{x} - x^{(i)}) + \frac{1}{2} (\tilde{x} - x^{(i)})^t f''(\xi) (\tilde{x} - x^{(i)})$$

where $\xi$ is an $n$-dimensional vector in the neighborhood of $\tilde{x}$, and the triple product in the last term in the above formula is interpreted separately for each Hessian component in $f''(\xi)$. Indeed, the above formula is just a compact form of the $n$ individual Taylor expansions of the scalar functions $f_1, f_2, \dots, f_n$. Thus, the error estimate can proceed just as in Section 9.13 to hold in the vector case as well.

Unfortunately, the Newton iteration converges superlinearly only when $x^{(i)}$ enters a sufficiently small neighborhood of $\tilde{x}$. If the initial guess $x^{(0)}$ is too poor, then the Newton iteration may converge rather slowly. It is thus essential to pick a suitable initial guess. A few ways to do this are discussed in Sections 21.9 and 28.16 below.

## 9.15 The Relaxed Newton Iteration

Furthermore, for some unstable problems (such as saddle-point problems), the Newton iteration may even diverge. Indeed, if $f'(x^{(0)})$ is nearly singular in the sense that it has an eigenvalue that is too small in magnitude, then the iteration may diverge as in Figure 9.11. To avoid this, the Newton iteration can be modified to read

$$x^{(i+1)} = x^{(i)} - \alpha (f'(x^{(i)}))^{-1} f(x^{(i)})$$

where $0 < \alpha < 1$ is a relaxation parameter.

Clearly, with this relaxed iteration, the convergence rate is no longer superlinear but only linear. Indeed, using the Taylor expansion of $f$ around $\tilde{x}$ as in Section 9.13, we have

$$x^{(i+1)} - \tilde{x} = x^{(i)} - \alpha (f'(x^{(i)}))^{-1} f(x^{(i)}) - \tilde{x}$$

$$= x^{(i)} - \tilde{x} - \alpha (f'(x^{(i)}))^{-1} \big( f'(x^{(i)})(x^{(i)} - \tilde{x}) + O(\|x^{(i)} - \tilde{x}\|^2) \big)$$

$$= (1 - \alpha)(x^{(i)} - \tilde{x}) + O(\|x^{(i)} - \tilde{x}\|^2)$$

as $x^{(i)}$ approaches $\tilde{x}$. In other words, the error is multiplied by the constant factor $1 - \alpha < 1$ in each iteration. Thus, to enhance convergence it is advisable to pick $\alpha$ that is not too small. On the other hand, $\alpha$ should also be not too large, so that divergence as in Figure 9.11 never happens.

In most applications in this book there is no need to relax the Newton iteration. The original version in Section 9.14 can be safely used, which is equivalent to picking $\alpha = 1$ here. Only in the most complicated system towards the end of the book, the nonlinear Maxwell system, is there a need to use $\alpha = 0.5$ to guarantee convergence.

## 9.16 Newton’s Iteration for Differential Operators

The Newton iteration is based on the linearization of the original (scalar or vector) function $f$ at $x^{(i)}$. Indeed, for a fixed $x^{(i)}$, the function

$$g(x) \equiv f(x^{(i)}) + f'(x^{(i)})(x - x^{(i)})$$

is the unique linear function that agrees with $f$ on $x^{(i)}$,

$$g(x^{(i)}) = f(x^{(i)}),$$

and also has the same derivative (or Jacobian) as $f$ does at $x^{(i)}$:

$$g'(x^{(i)}) = f'(x^{(i)}).$$

This is why $g$ might be called the linearization of $f$ at $x^{(i)}$ (see Section 5.11).

So far, we’ve assumed that $f$ is either a scalar or a vector function. Assume now that $f$ is an operator that maps a given function $u$ onto the unique function $f(u)$. In this case, both $u$ and $f(u)$ are functions of (at least) one variable.

We are particularly interested in the case in which $f$ is a nonlinear (partial) differential operator. In this case, the operator $f$ uses the (partial) derivatives of $u$. Furthermore, $f$ may contain products of (partial) derivatives of $u$, which produces nonlinearity.

Consider, for example, the case in which $f$ is a quasi-linear (partial) differential operator that contains no products of derivatives of $u$ but only terms of the form

$$C(u)Du,$$

where $C$ is an ordinary mapping (the coefficient) that uses no differentiation at all and $D$ is a linear differential operator. Clearly, this term is linearized at the given function $u^{(i)}$ by the linear differential operator

$$C(u^{(i)})D,$$

which agrees with the original term on $u^{(i)}$. Doing this for all the terms in the original quasi-linear operator $f$ produces the linear (partial) differential operator $f'(u^{(i)})$ that linearizes $f$ at $u^{(i)}$. The Newton iteration to find the unknown root function $\tilde{u}$ that satisfies

$$f(\tilde{u}) \equiv 0$$

can then be defined as in Section 9.14 above:

$$u^{(i+1)} = u^{(i)} - (f'(u^{(i)}))^{-1} f(u^{(i)}).$$
