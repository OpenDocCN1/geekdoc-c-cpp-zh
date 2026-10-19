Although there are more efficient numerical approaches, a direct way to solve

**A x = b**
(6.32)

is to calculate the inverse **A**⁻¹, and then multiply both sides of the equation by the inverse, yielding

**x = A⁻¹ b**
(6.33)

```
>>> from numpy.linalg import inv      # Test inverse
>>> dot(inv(A), A)
array([[ 1.00000000e+00, -1.33226763e-15, -1.77635684e-15],
       [ 8.88178420e-16,  1.00000000e+00,  0.00000000e+00],
       [ -4.44089210e-16,  4.44089210e-16,  1.00000000e+00]])
>>> print ('x =', multiply(inv(A), b))
x = [-1.4057971 -0.1884058 0.92753623]      # Solution
>>> print ('Residual =', dot(A, x) - b)
Residual = [ 4.44089210e-16  0.00000000e+00 -3.55271368e-15]
```

Here we first tested that inv(A) is in fact the inverse of A by seeing if A times inv(A) equals the identity matrix. Then we used the inverse to solve the matrix equation directly, and got the same answer as before (some error at the level of machine precision is just fine).

Our second example occurs in the solution for the principal-axes system of a cube, and requires us to find a coordinate system in which the inertia tensor is diagonal. This entails solving the eigenvalue problem

**I ω = λ ω** ,
(6.34)

where **I** is the inertia matrix (tensor), **ω** is an unknown eigenvector, and λ is an unknown eigenvalue. The program Eigen.py solves for the eigenvalues and vectors, and shows how easy it is to deal with matrices. Here it is in an abbreviated interpretive mode:

```
>>> from numpy import*
>>> from numpy.linalg import eig
>>> I = array([[2./3, -1./4], [-1./4,2./3]])
>>> print('I =\n', I)
I =
[[ 0.66666667 -0.25 ]
 [-0.25  0.66666667 ]]
>>> Es, evectors = eig(A)                 # Solves eigenvalue problem
>>> print('Eigenvalues =', Es, '\n Eigenvector Matrix =\n', evectors)
Eigenvalues = [ 0.91666667  0.41666667 ]
Eigenvector Matrix =
[[ 0.70710678  0.70710678 ]
 [-0.70710678  0.70710678 ]]
>>> Vec = array([ evectors[0, 0], evectors[1, 0] ])
>>> LHS = dot(I, Vec)                     # Matrix x vector
>>> RHS = Es[0]*Vec                       # Scalar mult
>>> print('LHS - RHS =', LHS-RHS)         # Test for zero
LHS - RHS = [ 1.11022302e-16 -1.11022302e-16]
```