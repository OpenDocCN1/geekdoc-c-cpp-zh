# 23.10 Alternative Right-Hand Side

Alternatively, the right-hand side $f$ could also be defined as follows. For $1 \le i \le N$, let $e^{(i)}$ be the $i$th standard unit vector, or the $i$th column of the identity matrix of order $N$. Furthermore, let $j(i)$ be an integer number between $1$ and $m$ for which $f^{(j(i))}$ is maximal (in modulus) at component (or pixel) $i$:

$|f_i^{(j(i))}| \ge |f_i^{(1)}|$  
$|f_i^{(j(i))}| \ge |f_i^{(2)}|$  
$\vdots$  
$|f_i^{(j(i))}| \ge |f_i^{(m)}|.$

Initially, let $f$ be the zero $N$-dimensional vector. Now, for $i = 1,2,\ldots,N$, update $f$ by the following substitution:

$f \leftarrow f + u_i^{(j(i))} A e^{(i)}$,

where

$u^{(1)} = A^{-1} f^{(1)}$  
$u^{(2)} = A^{-1} f^{(2)}$  
$\vdots$  
$u^{(m)} = A^{-1} f^{(m)}.$

Fortunately, the $u^{(j)}$'s are already available on the original fine level, so no inversion of $A$ is required. Furthermore, on the coarse level, it is assumed that $Q$ is easily invertible.

Moreover, the above loop contains no expensive vector operation. Indeed, $A e^{(i)}$ is already available as the $i$th column in the sparse matrix $A$, or the $i$th row in the symmetric sparse matrix $A$. Thus, each update of $f$ in the above loop requires only a few scalar operations.

In the example in Section 23.14 below, however, it turns out that the original definition of $f$ in Section 23.9 above gives a better result.

# 23.11 Global Features

Unfortunately, the combined right-hand side $f$ calculated above is still not good enough. Indeed, it may contain only local sources and sinks that are well-observed on the fine grid, but not necessarily more global coarse-grid features. To have these features as well, it is not enough to calculate the algebraic solution $x$ associated with $f$. Indeed, the naive algebraic solution

$x = A^{-1} f$

may lack any coarse-grid sharpness. A more sophisticated multigrid fusion algorithm is required not only to solve algebraically the original system with the inaccurate right-hand side $f$ but also to take into account coarse-grid contributions to the true image as well.