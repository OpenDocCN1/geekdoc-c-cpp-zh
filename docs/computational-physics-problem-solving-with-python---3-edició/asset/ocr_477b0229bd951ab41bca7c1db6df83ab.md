# Table 6.1 The operators of NumPy and their effects.

| Operator | Effect | Operator | Effect |
|---|---|---|---|
| dot(a, b[,out]) | Dot product arrays | vdot(a, b) | Dot product |
| inner(a, b) | Inner product arrays | outer(a, b) | Outer product |
| tensordot(a, b) | Tensor dot product | einsum() | Einstein sum |
| linalg.matrix_power(M, n) | Matrix to power n | kron(a, b) | Kronecker product |
| linalg.cholesky(a) | Cholesky decomp | linalg.qr(a) | QR factorization |
| linalg.svd(a) | Singular val decomp | linalg.eig(a) | Eigenproblem |
| linalg.eigh(a) | Hermitian eigen | linalg.eigvals(a) | General eigen |
| linalg.eigvalsh(a) | Hermitian eigenvals | linalg.norm(x) | Matrix norm |
| linalg.cond(x) | Condition number | linalg.det(a) | Determinant |
| linalg.slogdet(a) | Sign and log(det) | trace(a) | Diag nol sum |
| linalg.solve(a, b) | Solve equation | linalg.tensorsolve(a, b) | Solve ax = b |
| linalg.lstsq(a, b) | Least-squares solve | linalg.inv(a) | Inverse |
| linalg.pinv(a) | Penrose inverse | linalg.tensorinv(a) | Inverse N–D array |

We see here how, after we set up the array I on line 3, we then solve for its eigenvalues and eigenvectors with the single statement Es, evectors = eig(I) on line 8. We then extract the first eigenvector on line 14 and use it, along with the first eigenvalue, to check that (6.34) is in fact satisfied to machine precision.

Well, we think by now you have some idea of the use of NumPy. In Table 6.1 we indicate some more of what is available.

# 6.6

# Exercise: Testing Matrix Programs

Before you direct the computer to go off crunching numbers on a million elements of some matrix, it is a good idea to try out your procedures on a small matrix, especially one for which you know the right answer. In this way, it will take you only a short time to realize how hard it is to get the calling procedure perfect. Here are some exercises.

+   1. Find the numerical inverse of A = ⎛+4  −2  +1⎞
+      ⎜+3  +6  −4⎟
+      ⎝+2  +1  +8⎠.

+   a) As a general check, applicable even if you do not know the analytic answer, check your inverse in both directions; that is, check that AA⁻¹ = A⁻¹A = I, and note the number of decimal places to which this is true. This also gives you some idea of the precision of your calculation.