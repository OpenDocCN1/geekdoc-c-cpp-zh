In the two-dimensional case the covariance matrix is:

$$\Sigma=\begin{pmatrix}\sigma_1^2 & \sigma_1\sigma_2\rho\\ \sigma_1\sigma_2\rho & \sigma_2^2\end{pmatrix}$$

where:

$\sigma_1,\sigma_2>0$ and $-1\leq\rho\leq1$.

In this case the Cholesky decomposition becomes:

$$\Sigma=LL^{\mathrm T}$$

where:

$$L=\begin{pmatrix}\sigma_1 & 0\\ \rho\sigma_2 & \sqrt{1-\rho^2}\sigma_2\end{pmatrix}.$$

Thus, in order to sample from a *bivariate normal distribution* $N(\mu,\Sigma)$ with $(\mu=\mu_1,\mu_2)^{\mathrm T}$ we use the formula:

$$X_1=\mu_1+\sigma_1Z_1$$
$$X_2=\mu_2+\sigma_2Z_1+\sigma_2\sqrt{1-\rho^2}Z_2.$$

Finally, the algorithm to generate arrays of correlated random numbers is:

+   a) Generate an uncorrelated $N(0,1)$ vector $Z$.
+   b) Calculate the Cholesky lower-triangular matrix $C$ of the matrix $\Sigma$.
+   c) Compute the new correlated random vector $X=CZ+m$ where $m$ is the mean of $X$.

See also Exercise 8.

# 26.10.1 Appendix: Overview of the *Eigen* Matrix Library

*Eigen* is a high-level C++ library of template headers for linear algebra, matrix and vector operations, geometrical transformations, numerical solvers and related algorithms. *Eigen* is an open-source library and it is implemented using the *expression templates metaprogramming* techniques; it builds expression trees at compile-time and generates custom code to evaluate them. Using expression templates and a cost model of floating-point operations, the library performs its own *loop unrolling and vectorisation*.

A summary of the main features in *Eigen* is:

+   - Matrix and array classes and basic linear algebra; array manipulation.
+   - LU decomposition.
+   - LLT and LDLT Cholesky decomposition.