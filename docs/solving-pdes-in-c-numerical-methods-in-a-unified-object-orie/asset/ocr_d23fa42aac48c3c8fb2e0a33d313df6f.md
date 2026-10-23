+   6. Define the scalars \(\gamma_0 = \gamma = (r, \tilde{r})\).

+   7. Apply the iterative method to \(\tilde{p}\) with zero right-hand side:
+   
+   \[
+   \tilde{p} \leftarrow \tilde{p} - \mathcal{P}^{-1}A\tilde{p}.
+   \]

+   8. Compute the vector
+   
+   \[
+   \tilde{u} = \tilde{p} - \tilde{r} = \mathcal{P}^{-1}A\tilde{p}.
+   \]

+   9. Compute the vector
+   
+   \[
+   w = A\tilde{p}.
+   \]

+   10. Compute the scalar
+   
+   \[
+   \alpha = \gamma /(\tilde{p}, w).
+   \]

+   11. Update the approximate solution \(\tilde{x}\) by
+   
+   \[
+   \tilde{x} \leftarrow \tilde{x} + \alpha\tilde{p}.
+   \]

+   12. Update the residual by
+   
+   \[
+   r \leftarrow r - \alpha w.
+   \]

+   13. Update the preconditioned residual by
+   
+   \[
+   \tilde{r} \leftarrow \tilde{r} - \alpha\tilde{w}.
+   \]

+   14. Compute the scalar
+   
+   \[
+   \beta = (r, \tilde{r})/\gamma.
+   \]

+   15. Update \(\gamma\) by
+   
+   \[
+   \gamma \leftarrow \beta\gamma.
+   \]

+   16. Update the direction vector \(\tilde{p}\) by
+   
+   \[
+   \tilde{p} \leftarrow \tilde{r} + \beta\tilde{p}.
+   \]

+   17. If \(\gamma/\gamma_0 > 10^{-12}\), then go to step 7.

The above algorithm converges to \(x\) whenever \(A\) and \(\mathcal{P}\) are SPD. The convergence is particularly rapid when the basic iterative method is good (e.g., multigrid), so the preconditioner \(\mathcal{P}\) is a good spectral approximation to \(A\). However, when \(A\) or \(\mathcal{P}\) is not SPD, the PCG method does not necessarily converge to \(x\). Other Krylov-space methods that are not limited to the SPD case are required.

One such acceleration method is the conjugate gradient squared (CGS) method in [74]. When the CGS method is applied to the preconditioned system

\[
\mathcal{P}^{-1}Ax = \mathcal{P}^{-1}f,
\]