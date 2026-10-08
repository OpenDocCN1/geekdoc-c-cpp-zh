leads to the following system of equations:

```
$r^* = \lambda_1 B - \lambda_2 A$
$1 = \lambda_1 A - \lambda_2 C$
```

Solving for $\lambda_1$ and $\lambda_2$, gives:

```
$$\lambda_1 = \frac{B - Ar^*}{D}$
$$\lambda_2 = \frac{Cr^* - A}{D}$
```

Substituting $\lambda_1$ and $\lambda_2$ into (6.14):

```
$w^T = \frac{1}{D}(B1^T - AR^T)V^{-1} + \frac{1}{D}(CR^T - A1^T)V^{-1}r^* = g + hr^*$ (6.19)
```

where:

```
$g = \frac{1}{D}(B1^T - AR^T)V^{-1}$
$h = \frac{1}{D}(CR^T - A1^T)V^{-1}$
```

Source 6.4 shows the additional member functions required in the Matrix class to perform the relevant Matrix operations to implement the method of Lagrange multipliers.

# SOURCE 8.4: ADDITIONAL MEMBER FUNCTIONS IN THE Matrix CLASS

```
// ...
// Matrix.h
// ...

Matrix Add(const DBL v); // Add a double
Matrix Subtract(const DBL v); // Subtract a double
Matrix& Divide(const DBL v); // Divide a double

Matrix Minor(const int row, const int col const); // Matrix minor
Matrix Diag(const int n); // Matrix diagonal (overloaded)
Matrix Diag(const Matrix& v); // Matrix diagonal (overloaded)
DBL Det(const Matrix& a); // Matrix determinant
Matrix Inv(const Matrix& a); // Matrix inverse
```