+   - Singular value decomposition (SVD) and least-squares solver.
+   - QR decomposition (Householder).
+   - Eigenvalue and eigenvector decompositions.
+   - Sparse matrix storage and related basic linear algebra.

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