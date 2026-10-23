With this interpretation, the Newton iteration is defined in the same way as in Section 9.12 above, except that the division by $f'(x^{(i)})$ is now interpreted as the multiplication from the left by the inverse of the Jacobian, $(f'(x^{(i)}))^{-1}$:

```
$x^{(i+1)} = x^{(i)} - (f'(x^{(i)}))^{-1} f(x^{(i)})$
```

Clearly, because the Jacobian of $f$ depends on $x^{(i)}$, it must be recalculated before each iteration. Furthermore, it must have an inverse matrix; in other words, it must be nonsingular (invertible). Fortunately, this inverse matrix doesn’t have to be calculated explicitly. Instead, one only needs to solve a linear system in which the Jacobian serves as the coefficient matrix. This can be done in an inner iteration, using one of the iterative methods from Chapter 17.

Furthermore, with the present interpretation, the error estimate in Section 9.13 is still valid, provided that $f'^{-1}$ and the individual Hessian components in $f''$ are bounded in a neighborhood of $	ilde{x}$. Indeed, the Taylor expansion around $x^{(i)}$ used in Section 9.13 can be adapted to the present vector function to read

```
$f(	ilde{x}) = f(x^{(i)}) + f'(x^{(i)})(	ilde{x} - x^{(i)}) + \frac{1}{2} (	ilde{x} - x^{(i)})^t f''(\xi) (	ilde{x} - x^{(i)})$
```

where $\xi$ is an $n$-dimensional vector in the neighborhood of $	ilde{x}$, and the triple product in the last term in the above formula is interpreted separately for each Hessian component in $f''(\xi)$. Indeed, the above formula is just a compact form of the $n$ individual Taylor expansions of the scalar functions $f_1, f_2, \dots, f_n$. Thus, the error estimate can proceed just as in Section 9.13 to hold in the vector case as well.

Unfortunately, the Newton iteration converges superlinearly only when $x^{(i)}$ enters a sufficiently small neighborhood of $	ilde{x}$. If the initial guess $x^{(0)}$ is too poor, then the Newton iteration may converge rather slowly. It is thus essential to pick a suitable initial guess. A few ways to do this are discussed in Sections 21.9 and 28.16 below.

# 9.15 The Relaxed Newton Iteration

Furthermore, for some unstable problems (such as saddle-point problems), the Newton iteration may even diverge. Indeed, if $f'(x^{(0)})$ is nearly singular in the sense that it has an eigenvalue that is too small in magnitude, then the iteration may diverge as in Figure 9.11. To avoid this, the Newton iteration can be modified to read

```
$x^{(i+1)} = x^{(i)} - \alpha (f'(x^{(i)}))^{-1} f(x^{(i)})$
```

where $0 < \alpha < 1$ is a relaxation parameter.

Clearly, with this relaxed iteration, the convergence rate is no longer superlinear but only linear. Indeed, using the Taylor expansion of $f$ around $	ilde{x}$ as in Section 9.13, we have

```
$x^{(i+1)} - \tilde{x} = x^{(i)} - \alpha (f'(x^{(i)}))^{-1} f(x^{(i)}) - \tilde{x}$
$= x^{(i)} - \tilde{x} - \alpha (f'(x^{(i)}))^{-1} \big( f'(x^{(i)})(x^{(i)} - \tilde{x}) + O(\|x^{(i)} - \tilde{x}\|^2) \big)$
$= (1 - \alpha)(x^{(i)} - \tilde{x}) + O(\|x^{(i)} - \tilde{x}\|^2)$
```