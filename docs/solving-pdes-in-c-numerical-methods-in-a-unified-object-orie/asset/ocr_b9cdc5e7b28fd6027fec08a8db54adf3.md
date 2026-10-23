# 27.6  The Advantage of the Object-Oriented Framework

The power of OOP is apparent in the implementation of the matrix $A^{(n)}(v)$. Indeed, it can be implemented in a sparse-matrix object, with “T” being a "matrix2" object rather than a mere scalar. For consistency, the elements in the stiffness matrix $A^{(s)}$ are implemented as "matrix2" objects as well, using the equivalence

$$c \sim \begin{pmatrix} \Re c & -\Im c \\ \Im c & \Re c \end{pmatrix}$$

for any complex number $c$. This allows arithmetic operations with such matrices, including multiplication by a complex number (implemented as a "matrix2" object) and addition. Furthermore, vectors are implemented with components that are "point" objects rather than mere scalars, using the equivalence

$$c \sim \begin{pmatrix} \Re c \\ \Im c \end{pmatrix}$$

for any complex number $c$. This allows arithmetic operations with such vectors, including multiplication (from the left) by a complex number (implemented as a "matrix2" object) and addition. Furthermore, it allows the matrix-times-vector multiplication. With these operations, the Newton iteration of Section 9.14 can be easily implemented.

# 27.7  The Newton Iteration

Consider the nonlinear operator $F$ defined on the set of the vector grid functions by

$$F(v)=\left(A^{(s)}+\sqrt{K}\,A^{(b)}+K\,A^{(m)}\right)v+K_1f(v)$$

(where $v$ is any vector grid function, and the nonlinear operator $f$ is as in Section 27.5). Clearly, the Jacobian of the nonlinear operator $F$ at $v$ is the matrix

$$A(v)=A^{(s)}+\sqrt{K}\,A^{(b)}+K\,A^{(m)}+K_1A^{(n)}(v).$$$

This Jacobian will be useful in the Newton iteration below. (See Section 9.14.)

Consider now the following problem: find a vector grid function $u$ for which

$$F(u)=\vec{0}$$

(where $\vec{0}$ is the zero vector grid function). The Newton iteration that converges to the required solution $u$ is defined as follows:

+   1. Let the vector grid function $u^{(0)}$ be a suitable initial guess.
+   
+   2. For $i=0,1,2,\ldots$,
+      (a) Solve the linear system
+      $$A(u^{(i)})x=F(u^{(i)})$$
+      for the unknown vector grid function $x$.
+   
+      (b) Define
+      $$u^{(i+1)}\equiv u^{(i)}-x.$$