+   1. Initialize $\mathbf{a}_0$ and $\lambda_0$, set $k = 0$.
2. At the current point $\mathbf{a}_k$ compute the vector $\mathbf{g}_k$ and its gradient $\mathbf{J}_k$.
3. Compute $\mathbf{h}_k$ by solving equation $(\mathbf{J}_k^T\mathbf{J}_k + \lambda_k\mathbf{I})\mathbf{h}_k = -\mathbf{J}_k^T\mathbf{g}_k$.
4. Compute the vector $\mathbf{g}'$ at the point $\mathbf{a}' = \mathbf{a}_k + \mathbf{h}_k$.
5. If $||\mathbf{g}'||^2 \ge ||\mathbf{g}_k||^2$, reset $\lambda_k := \beta\lambda_k$ and return to Step 3.
6. Update $\lambda_{k+1} = \alpha\lambda_k$ and $\mathbf{a}_{k+1} = \mathbf{a}_k + \mathbf{h}_k$, increment $k$, return to Step 2.

Table 4.1: *Levenberg-Marquardt algorithm.*

if $\mathscr{G}(\mathbf{a}') < \mathscr{G}(\mathbf{a})$, it is accepted and $\lambda$ is decreased by a certain factor $\alpha$ before the next iteration (suppressing the corrective term $\lambda\mathbf{I}$).

Otherwise the new value $\mathbf{a}' = \mathbf{a} + \mathbf{h}$ is rejected, $\lambda$ is increased by a certain factor $\beta$ and the augmented normal equations $\mathbf{N}_\lambda\mathbf{h} = -\mathbf{J}^T\mathbf{g}$ are solved again. These recursive attempts continue until the increment $\mathbf{h}$ leads to a smaller value of $\mathscr{G}$. This is bound to happen, since for large $\lambda$ the method approaches the steepest descent.

Advantages. In other words, when $\lambda$ increases, the recomputed vector $\mathbf{h}$ not only gets smaller but also turns (rotates) and aligns somewhat better with the negative gradient vector $-\nabla\mathscr{G}(\mathbf{a})$. As $\lambda \rightarrow \infty$, the length of $\mathbf{h}$ approaches zero and its direction converges to that of $-\nabla\mathscr{G}(\mathbf{a})$ (Fig. 4.1).

We see that the Levenberg-Marquardt correction combines two classical ideas:

+   (a) The quadratic approximation to the function, which works well in a vicinity of its minimum and yields a fast (nearly quadratic) convergence.

+   (b) The steepest descent scheme that ensures reliability in difficult cases.

As the algorithm is based on a reasonable balance between these two principles, it is sometimes referred to as Marquardt compromise.

Practical issues. In many implementations, the parameter $\lambda$ is initialized to a small value, e.g., $10^{-3}$ or $10^{-4}$. A common choice for $\alpha$ and $\beta$ is $\alpha = 0.1$ and $\beta = 10$.

*Remark. Just like equations (4.12) in the previous section, the new system* $\mathbf{N}_\lambda\mathbf{h} = -\mathbf{J}^T\mathbf{g}$ can be solved numerically in many ways, including Cholesky factorization, QR decomposition, and SVD. The use of QR and SVD requires a trick, though, because the system (4.16) is not in the right form (yet). The trick is to rewrite (4.16) as

```
$\mathbf{J}_\lambda^T\mathbf{J}_\lambda\mathbf{h} = -\mathbf{J}_\lambda^T\mathbf{g}_0,$ (4.17)
```