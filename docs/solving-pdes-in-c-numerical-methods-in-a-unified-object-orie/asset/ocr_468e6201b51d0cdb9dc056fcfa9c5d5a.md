9. Show that B above is SPD.

10. Define the energy inner product by

$(u, v)_B \equiv (u, Bv) = u^T B v$

(where $u$ and $v$ are any two vectors).
A matrix $M$ is symmetric with respect to the energy inner product if

$(Mu, v)_B = (u, Mv)_B$

for every two vectors $u$ and $v$. Show that $B^{-1} A$ and $B^{-1} K$ are symmetric with respect to the energy inner product.

11. Define the energy norm of a matrix $M$ by

$\|M\|_B \equiv \max_{v \neq 0} \left( \frac{(M^T v, M^T v)_B}{(v, v)_B} \right)^{1/2}$.

It is well known that, if $M^T$ is symmetric with respect to the energy inner product, then the above quantity is also equal to the modulus of the largest eigenvalue of $M^T$. In other words,

$\|M\|_B = \max_{v \neq 0} \left| \frac{(v, M^T v)_B}{(v, v)_B} \right|.$

12. Use the SPD property of $A$ and $K$ to show that, for every nonzero vector $v$, 

$\frac{(v, (\Delta t)^{-1} K v)}{(v, ((\Delta t)^{-1} K + A) v)}$ and $\frac{(v, ((\Delta t)^{-1} K - A/2) v)}{(v, ((\Delta t)^{-1} K + A/2) v)}$

are smaller than 1 in magnitude, and, for sufficiently small $\Delta t$, 

$\frac{(v, ((\Delta t)^{-1} K - A) v)}{(v, (\Delta t)^{-1} K v)}$

is also smaller than 1 in magnitude.

13. Use the above results to show that the block submatrices $Q_i B_i^{-1}$ in Chapter 8, Section 3, are smaller than 1 in terms of the energy norm induced by $B_i$. Furthermore, use this result to show stability and accuracy in the time marching.

14. Compare your proof with the proof in Chapter 18 in [68].

15. Assume that the function $\alpha$ in the above mixed boundary conditions is constant in each particular boundary edge, e.g., an edge leading from node $i$ to node $j$ that both lie on the boundary segment where the mixed boundary conditions are imposed. Show that the contribution to $A_{i,i}$ from this edge is positive and twice as large as the contribution to $A_{i,j}$.