# 4.2 Gauss-Newton method

**Least squares problem.** Consider a problem in which we are to minimize a function

$\mathscr{G}(\mathbf{a}) = \sum_{i=1}^{n} g_{i}^{2}(\mathbf{a})$ (4.5)

of $k$ variables $\mathbf{a} = (a_{1}, \ldots, a_{k})$. We assume that $n > k$, and $g_{i}$ have derivatives.

**Newton-Raphson approach to the least squares problem.** As in Newton-Raphson scheme, we start by approximating $\mathscr{G}(\mathbf{a} + \mathbf{h})$ by a quadratic part of Taylor polynomial:

$\mathscr{G}(\mathbf{a} + \mathbf{h}) \approx \mathscr{G}(\mathbf{a}) + \mathbf{D}^{T}\mathbf{h} + \frac{1}{2}\mathbf{h}^{T}\mathbf{H}\mathbf{h}$. (4.6)

where

$\mathbf{D} = \nabla\mathscr{G}(\mathbf{a}) = 2\sum_{i=1}^{n}g_{i}(\mathbf{a})\nabla g_{i}(\mathbf{a})$ (4.7)

is the gradient of $\mathscr{G}$ and

$\mathbf{H} = \nabla^{2}\mathscr{G}(\mathbf{a}) = 2\sum_{i=1}^{n}[\nabla g_{i}(\mathbf{a})][\nabla g_{i}(\mathbf{a})]^{T} + 2\sum_{i=1}^{n}g_{i}(\mathbf{a})\nabla^{2}g_{i}(\mathbf{a})$ (4.8)

is the Hessian matrix of $\mathscr{G}$. The Newton-Raphson method (4.4) uses both **D** and **H**.

**Gauss-Newton for the least squares problem.** The Gauss-Newton method drops the last sum of (4.8), i.e., it replaces **H** with

$\mathbf{H}^{\circ} = 2\sum_{i=1}^{n}[\nabla g_{i}(\mathbf{a})][\nabla g_{i}(\mathbf{a})]^{T}$. (4.9)

To justify this replacement, one usually notes that in typical least squares applications $g_{i}(\mathbf{a})$ are small, hence the second sum in (4.8) is much smaller than the first, so its removal will not change the Hessian matrix **H** much. Also one notes that modifying **H** cannot alter the limit point of the procedure, it can only affect the path that the iterations take to approach that limit$^{1}$.

**Advantages.** Replacing **H** with $\mathbf{H}^{\circ}$ has two immediate advantages:

+   (a) The computation of second order derivatives of $g_{i}$ is no longer necessary;
(b) Unlike **H**, the new matrix $\mathbf{H}^{\circ}$ is always positive semi-definite.

$^{1}$However it can (and does!) slow down the rate of convergence, especially if $g_{i}(\mathbf{a})$ are not so small, see more on that in the end of this section.