
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

- a) Generate an uncorrelated $N(0,1)$ vector $Z$.
- b) Calculate the Cholesky lower-triangular matrix $C$ of the matrix $\Sigma$.
- c) Compute the new correlated random vector $X=CZ+m$ where $m$ is the mean of $X$.

See also Exercise 8.

## 26.10.1 Appendix: Overview of the *Eigen* Matrix Library

*Eigen* is a high-level C++ library of template headers for linear algebra, matrix and vector operations, geometrical transformations, numerical solvers and related algorithms. *Eigen* is an open-source library and it is implemented using the *expression templates metaprogramming* techniques; it builds expression trees at compile-time and generates custom code to evaluate them. Using expression templates and a cost model of floating-point operations, the library performs its own *loop unrolling and vectorisation*.

A summary of the main features in *Eigen* is:

- Matrix and array classes and basic linear algebra; array manipulation.
- LU decomposition.
- LLT and LDLT Cholesky decomposition.
- Singular value decomposition (SVD) and least-squares solver.
- QR decomposition (Householder).
- Eigenvalue and eigenvector decompositions.
- Sparse matrix storage and related basic linear algebra.

One way to learn Eigen and apply it to applications in computational finance is to copy exemplar code and then modify it to suit your current application. If you know numerical linear algebra and possibly another C++ matrix library then learning Eigen should be easy.

As a final example, we discuss how to solve an overdetermined linear system: given an m × n matrix A where m ≥ n and an m × 1 vector b, find a vector x such that Ax is the 'best' approximation to b.

The system Ax = b is overdetermined so it cannot be solved exactly. But it does have a least-squares solution:

```
Aᵀ (b − Ax) = 0 or (AᵀA) x = Aᵀb  (26.28)
```

satisfying:

```
‖b − Ax‖ ≤ ‖k − Ay‖ ∀y ∈ ℝⁿ.
```

System (26.28) is called the normal equations (Dahlquist and Björck, 1974, p. 197).

The code is as follows:

```
// Create overdetermined system
// From Dahlquist's bookpage 199: answer is (5/4, 7/4, 3)
int M = 6; int N = 3;
Eigen::MatrixXd A(M, N);
A(0, 0) = 1.0; A(0, 1) = 0.0; A(0, 2) = 0.0;
A(1, 0) = 0.0; A(1, 1) = 1.0; A(1, 2) = 0.0;
A(2, 0) = 0.0; A(2, 1) = 0.0; A(2, 2) = 1.0;
A(3, 0) = -1.0; A(3, 1) = 1.0; A(3, 2) = 0.0;
A(4, 0) = 0.0; A(4, 1) = -1.0; A(4, 2) = 1.0;
A(5, 0) = -1.0; A(5, 1) = 0.0; A(5, 2) = 1.0;

Eigen::VectorXd b(M);
b[0] = 1.0; b[1] = 2.0; b[2] = 3.0; b[3] = 1.0; b[4] = 2.0; b[5] = 1.0;

// Set up and solve overdetermined system
auto AT = A.transpose();
auto ATb = AT*b;
auto ATA = AT*A;
Eigen::VectorXd x = ATA.ldlt().solve(ATb);
std::cout << "Solution(5/4, 7/4, 3): " <<x[0]<<","<<x[1]<< "," << x[2];

// Compute the residual
auto r = AT*A*x - AT*b;
std::cout << "Residual size: " << r.norm() << std::endl;
```

Finally, we apply the Cholesky method to the example in Kienitz and Wetterau (2012, p. 138; we get the same output):

```
unsigned D = 4;
Eigen::MatrixXd corr(D, D);

corr(0, 0) = corr(1, 1) = corr(2, 2) = corr(3, 3) = 1.0;

corr(0, 1) = corr(1, 0) = 0.748733508;
corr(0, 2) = corr(2, 0) = 0.888524896;
corr(0, 3) = corr(3, 0) = 0.821526502;

corr(1, 2) = corr(2, 1) = 0.726662801;
corr(1, 3) = corr(3, 1) = 0.683150423;

corr(3, 2) = corr(2, 3) = 0.878266274;
std::cout << "\nThe correlated matrix is" << std::endl << corr;

// Compute the Cholesky decomposition of matrix corr
Eigen::LLT<Eigen::MatrixXd> lltOfA(corr);
// Retrieve factor L in the decomposition
Eigen::MatrixXd L = lltOfA.matrixL();
// Previous two lines can also be written as "L = A.llt().matrixL()"

std::cout << "\nThe Cholesky factor L is" << std::endl << L;
std::cout << "\nTo check this, let us compute L * L.transpose()" ;
std::cout << L * L.transpose() << std::endl;
std::cout << "\nThis should equal the matrix corr matrix" << std::endl;

// Sanity check
auto Diff = corr - L * L.transpose();
std::cout << "\nThis should equal zero? " << Diff << std::endl;
```

## 26.11 SUMMARY AND CONCLUSIONS

We have given an overview of random number generation and statistical distributions in C++. We first gave a short introduction to the mathematical foundations of random number generation and some of the associated use cases, such as generating uniform random variates and variates from a given univariate distribution. There are several basic engines, engine adapters and adapters with predefined parameters and furthermore 20 distributions classified into five major categories.

It will be interesting to see the uptake of this library in the future. One advantage is that we no longer need to rely on proprietary libraries. On the other hand, the functionality in standard C++ may not be suitable for all applications in computational finance and in these cases we may need to resort to more specialised libraries.

Chapters 31 and 32 apply the results of this chapter to computational finance.

## 26.12 EXERCISES AND PROJECTS

- 1. **(Legacy Code Migration)**

Some legacy systems may still use the *polar Marsaglia* (equation (26.2)) or *Box–Muller* (equation (26.3)) methods based on `std::rand()`, for example. The objective of this exercise is to write functions for these methods using the engines in C++11. The return type is a tuple of values, each field being a standard normal random variate. Test your code. Examine the possible performance issues associated with the creation and unpacking of tuples, especially if performed in a loop. Consider the interface that returns a single value.

- 2. **(Random Variates)**

Generate a random variable with pdf:

$$
f_X(x)=
\begin{cases}
2x, & 0 \le x \le 1\\
0, & \text{otherwise.}
\end{cases}
$$

Show that the cdf is given by:

$$
F_X(x)=
\begin{cases}
0, & x<0\\
x^2, & 0\le x\le 1\\
1, & x>1
\end{cases}
$$

and that:

$$X=F_X^{-1}(U)=\sqrt{U},\quad 0\le U\le 1.$$

In other words, in order to generate a variate from this distribution we generate a uniform variate $U$ on $(0,1)$ (for example, using a C++ engine) and then take the square root of $U$.

- 3. **(Distributions Not Supported in C++11)**

In some cases we may wish to generate random variates from distributions that are not supported in C++11. What do we do in such cases? There are basically two choices; first, an exact formula may be known or failing that, we resort to numerical methods. In the first case we take the example of the *Rayleigh distribution* which has many applications, for example when we condition a standard Brownian motion starting at the origin to have the value $b$ at time 1 (Glasserman, 2004, p. 56). Then the maximum over the closed interval $[0,1]$ is given by:

$$F(x)=1-e^{2x(x-b)},\quad x\ge b.$$

If we solve the equation $F(X)=U$ with $U\in(0,1)$ we get the roots:

$$X=\frac{b}{2}\pm\frac{\sqrt{b^2-2\log(1-U)}}{2}.$$

We take the larger of the roots since the maximum of the Brownian path must be at least $b$. Since $U$ and $1-U$ have the same distribution, we arrive at the value:

$$X = \frac{b}{2} + \frac{\sqrt{b^2 - 2 \log(U)}}{2}.$$

Implement this formula as a C/C++ function using one of the engines in C++11. Finally, implement the same functionality using an iterative solver using the inverse transform method (26.6) in combination with the Boost C++ Math Toolkit (see also Chapter 19) that contains a class for the Rayleigh distribution.

- 4. **(Acceptance–Rejection Method)**

The efficiency of the algorithm in Section 26.3.2 can be improved because the majorising function $g$ is not very accurate. We propose a better function to reduce the rejection rate. To this end, let us consider the majorising function:

$$g(x) = 2x, \quad 0 \le x \le 1.$$

We can check that the cdf is given by $F(x) = x^2$ and hence the inverse transform equation (26.6) tells us that $X = F_X^{-1}(U) = \sqrt{U}$. Show that the test for acceptance becomes $U_2 \le \frac{3}{2}\sqrt{U_1}$ and we then accept $U_1$ as the random variable from $f$.

Test the efficiency of this procedure compared with the solution given in Section 26.3.2.

- 5. **(Weibull Distribution)**

Consider the Weibull distribution with shape parameter $k > 0$ and scale parameter $\lambda > 0$. Show that the cdf is given by:

$$F(x) = \begin{cases} 1 - e^{-\left(\frac{x}{\lambda}\right)^k} & x \ge 0 \\ 0, & x < 0. \end{cases}$$

Show that a random variate of this distribution is given by:

$$X = (\lambda - \log U)^{1/k}$$

where $U$ is a uniform variate on the interval $(0, 1)$. We note that C++ supports the Weibull distribution.

- 6. **(Multinormal Distribution)**

A random vector $X = (X_1, \dots, X_n)$ has a multinormal distribution if its pdf is given by:

$$f_X(x) = \frac{1}{(2\pi)^{n/2} |\Sigma|^{1/2}} \exp\left[-\frac{1}{2} (x - \mu)^\top \Sigma^{-1} (x - \mu)\right]$$
