# # Appendix A

# ## Mathematical Background

# ### A.1 Notation and Math Background

This section reviews basic notation and concepts from calculus and real analysis.

# #### A.1.1 Generalities

+   * $\mathbf{1}_A$: Indicator function of a set $A$. This means that $\mathbf{1}_A(x) = 1$ when $x \in A$ and 0 otherwise.
* $J(-)$: The "dot" is used to stress that $J$ is a function of some variable.
* $\mathbf{u}$: Boldface is compact notation used to designate a sequence. Alternative notation: $\mathbf{u}=\{u_0, u_1, \dots\} = u_{0,\infty}$.
* For a function $J: \mathbb{R}^n 	o \mathbb{R}$, do not forget the gradient $
abla J$ is *not the same* as the derivative $\partial J$. The gradient is a column vector, and the derivative a row vector (the linear approximation of the scalar valued function $J$).

Concerning sets and sequences in $\mathbb{R}^n$.

# ### A.1.2 Topology

+   * Neighborhood of $x \in \mathbb{R}^n$: a set containing $x$ that is open.
* A set $S \subset \mathbb{R}^n$ is compact if it is closed and bounded.
* A collection of sets $\{O_
u : 
u \in \mathcal{N}\}$ (where the index $\mathcal{N}$ may be uncountable infinite) is called a covering of a set $S \subset \mathbb{R}^n$ if $S \subset O_
u$ for each $
u \in \mathcal{N}$, and $S \subset igcup O_
u$. Many books in the theory make implicit use one of the following characterization: A set $S$ is compact if and only if every cover admits a finite subcovering (there is a finite collection of indices $\{
u_i : 1 \le i \le n\}$ satisfying $S \subset igcup_{i=1}^n O_{
u_i}$).
* For a function $g: Z 	o \mathbb{R}$, the span is defined by

```
$||g\|_{ap} = \max_{\hat{z}} |g(z) - r| = \frac{1}{2}[\max_{\hat{z}} g(z) - \min_{\hat{z}} g(z)]$
```

Equation (10.34) shows an example of a variation of this.

The following notation refers to a collection of vectors or scalars scaled by a variable $t \in \mathbb{T}$ interpreted as time, or the number of iterations in an algorithm. Examples: $\mathbb{Z}_+ = \{0, 1, 2, \dots\}$ and $\mathbb{R}_+$.