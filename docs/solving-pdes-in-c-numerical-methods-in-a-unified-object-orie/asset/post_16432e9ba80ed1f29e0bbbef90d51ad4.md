
Fortunately, R is used in Section 30.11 only to calculate the quadruple product ((RA')A')f. For this purpose, one only needs to solve linear systems of the form

\(\left(A^{[k,l]}\right)^{[m,n]} x = f^{(k,m)}\)

where 1 ≤ m < k ≤ N, 1 ≤ n < l ≤ N, f^{(k,m)} is the (N − 2)-dimensional vector obtained from f by dropping the k th and m th components, and x is the (N − 2)-dimensional vector of unknowns. The numerical solution x is then converted back to an N-dimensional vector by the transpose operator: introducing zero components to serve as the new l th and n th components, while shifting the original components ahead.

The total number of linear systems is

\(\binom{N}{2}^2 = \frac{N^2(N-1)^2}{4} = O(N^4).\)

Fortunately, these linear systems are completely independent of each other, so they can be solved concurrently in parallel. Furthermore, each linear system can be solved by some suitable iterative method, accelerated by GMRES or some other suitable acceleration technique. This way, the sparsity of the coefficient matrix and preconditioner can be used in the efficient implementation of the numerical solution process.

In practice, many of the above linear systems don't have to be solved. Indeed, since A is sparse, A' is sparse as well. Thus, the numerical solution x contributes nothing to the required quadruple product ((RA')A')f if

\(a'_{k,l}=0 \text{ or } a'_{m,n}=0\)

and

\(a'_{k,n}=0 \text{ or } a'_{m,l}=0.\)

Thus, the total number of linear systems that need to be solved decreases to O(N^2) only.

## 30.14 The Newton–Gauss–Seidel Iteration

Let us now consider the more general case, in which A depends not only on e but rather on the K unknowns e1, e2, …, eK:

\(A \equiv A(e_1,e_2,\dots,e_K).\)

Clearly, in this case A' and A'' depend on these K unknowns as well. As a result, the error-energy function b depends on these K unknowns as well. For this reason, the derivative b' used above should be replaced by the gradient of b, so the optimal e1, e2, …, eK are the solution of the system

\(\nabla b \equiv \nabla_{e_1,e_2,\dots,e_K} b(e_1,e_2,\dots,e_K)=0.\)

In fact, this is a natural extension of the scalar case K = 1 discussed above in detail.

The Newton iteration to solve this system requires (Section 9.14) the Hessian of b

\(\left(b_{e_i e_j}\right)_{1\le i,j\le K} \equiv \left(\frac{\partial^2 b}{\partial e_i \partial e_j}\right)_{1\le i,j\le K}.\)

## 30.15 A More Practical Iteration

Each particular partial derivative of the form b_{e_i e_j} can be calculated in the same way as the derivative b'' has been calculated above. The only thing one needs to do is replace the first derivative by ∂/∂e_j and the second derivative by ∂/∂e_i (1 ≤ i, j ≤ K).

Unfortunately, the Newton iteration in Section 9.14 requires the expensive calculation (and implicit inversion) of the entire Hessian in each iteration. Fortunately, one may use the Newton–Gauss–Seidel iteration, which requires only the main-diagonal part of this Hessian. As a matter of fact, the Newton–Gauss–Seidel iteration may be considered as a natural extension to nonlinear systems of the original Gauss–Seidel relaxation in Section 17.3 above.

Here is how a single Newton–Gauss–Seidel iteration is defined. For i = 1,2,...,K, update (or improve) e_i by applying one scalar Newton iteration as in Section 9.12 to the i-th equation

b_{e_i} = 0.

while keeping e_1,...,e_{i-1} and e_{i+1},...,e_K fixed. This loop (or sweep) updates all the e_i's one by one, and completes one Newton–Gauss–Seidel iteration. This iteration is then repeated to update the e_i's again and again, until they are nearly optimal.

Clearly, the Newton–Gauss–Seidel iteration lacks the superlinear-convergence property of the original vector Newton iteration (Sections 9.13 and 9.14). Still, it has the advantage of avoiding the calculation of the mixed partial derivatives in the off-diagonal part of the Hessian. Furthermore, the Newton–Gauss–Seidel iteration can also be used as a relaxation method within the multigrid V-cycle in Section 23.4 above. Below we present a yet more efficient iterative method that avoids the calculation of any partial derivative of b at all.

As we've seen above, the calculation of any (partial) derivatives of the error-energy function b can be rather expensive. Even in the Newton–Gauss–Seidel iteration introduced above, one still needs to calculate partial derivatives of the form b_{e_i e_i} in each iteration, which can be rather time consuming, unless a very powerful parallel computer is available. To avoid this, one might approximate the (partial) derivatives of b by divided differences as follows:

[b(e_i + Δ_n) - b(e_i - Δ_n)] / [2Δ_n] → b_{e_i}
[b(e_i + Δ_n) - 2b(e_i) + b(e_i - Δ_n)] / Δ_n² → b_{e_i e_i},

where Δ_n → 0 is a monotonically decreasing sequence of positive parameters. Furthermore, the convergence can be accelerated further by Richardson's extrapolation or any other acceleration technique. The approximate (partial) derivatives of b can then be used in Newton or Newton–Gauss–Seidel iteration, even when the mapping A^{-1}(f) is nonlinear. Alternatively, one might prefer to update e_i by the golden-ratio algorithm as in Sections 30.4 and 30.5 above rather than by the scalar Newton method. More precisely, the improved e_i can be defined by calculating b at e_i ± δ (for some small parameter δ) and then choosing from the set {e_i - δ, e_i, e_i + δ} the element that minimizes b. In other words, one sweep or one iteration is defined as follows. For $i = 1, 2, \ldots, K$, update $e_i$ by

$$e_i \leftarrow \arg\min_{q\in\{e_i-\delta,e_i,e_i+\delta\}} b(e_1,\ldots,e_{i-1},q,e_{i+1},\ldots,e_K).$$

Thus, in one sweep or iteration, all the $e_i$'s are updated one by one in this way. The iteration is then repeated until the $e_i$'s produce a sufficiently small value of $b$.

The present iteration has yet another advantage. Because no differentiation of $b$ is required, it is no longer necessary to assume that $A$ is differentiable or even continuous with respect to any of the $e_i$'s. The present iteration is therefore relevant even for rather nonstandard kinds of applications, in which the order of $A$ may change as the $e_i$'s change.

## 30.16 Exercises

- 1. Assume that $u^{(n)}(z_0)$ is available by some experimental observation at the boundary point $z_0=(1,0)$ that lies on the right edge in the domain in Figure 22.4. Use the code in Section 1.20 in conjunction with the Helmholtz solver in this nearly rectangular domain to obtain a (locally) optimal depth of slit, for which the error

   $$
   |u^{(n)}(z_0)-u^{(o)}(z_0)|
   $$

   is minimized.

- 2. Assume that $u^{(o)}(z_0)$ is available by some experimental observation at the boundary point $z_0=(1,0)$ that lies on the circular part of the boundary of the domain in Figure 22.5. Use the code in Section 1.20 in conjunction with the Helmholtz solver in this nearly circular domain to obtain a (locally) optimal depth of slit, for which the error

   $$
   |u^{(n)}(z_0)-u^{(o)}(z_0)|
   $$

   is minimized.

- 3. Show that, if $A'$ in Section 30.8 is sparse and contains $O(N)$ nonzero elements only, then the total number of linear systems that need to be solved in Section 30.13 decreases to $O(N^2)$.

- 4. Implement the tensor object with four indices (Section 30.9). Implement also the tensor-matrix product.

- 5. Implement the tensor object with six indices (Section 30.9). Implement also the tensor-matrix product.

- 6. Use your code in the above exercises to implement Newton’s iteration in Section 30.11 to minimize the error-energy function $b=b(e)$.

- 7. Use your code in the above exercises to implement Newton’s iteration to minimize the error-energy function $b\equiv b(e_1,e_2,\ldots,e_K)$ in the vector case $K>1$ (Section 30.14).

- 8. Implement also the Newton–Gauss–Seidel iteration in Section 30.14.

- 9. Implement also the straightforward iteration in Section 30.15 above in the vector case $K>1$.
