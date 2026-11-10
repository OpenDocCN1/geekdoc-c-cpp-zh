of the form $B = U^{-1}AU$. The matrix $B$ represents the linear operator in the new basis and the two matrices $A$ and $B$ are then similar. The properties of the linear operator, which are independent of the basis of representation, are thus revealed by the study of the similarity invariants of the matrix, namely its properties that remain invariant under similarity.

Among these invariants, the most elementary are the rank and the determinant. Indeed, since the matrices $U$ and $U^{-1}$ are invertible, the rank of $U^{-1}AU$ is the rank of $A$. Moreover, $\det(U^{-1}AU) = \det(U^{-1})\det(A)\det(U) = \det(U^{-1}U)\det(A) = \det(A)$. Similarly, the characteristic polynomial of the matrix $A$, defined as $\chi_A(x) = \det(xId - A)$ is also invariant under similarity transformation:

$$\det(xId - U^{-1}AU) = \det(U^{-1}(xId - A)U) = \det(xId - A).$$

Consequently, the characteristic values of a matrix, defined as the roots of its characteristic polynomial in its splitting field, are thus also similarity invariants.

By definition, a scalar $\lambda$ is an eigenvalue of a matrix $A$ if there exists a non-zero vector $u$ such that $Au = \lambda u$. The eigenspace associated with an eigenvalue $\lambda$ is the set of all vectors $u$ verifying $Au = \lambda u$. It is a linear subspace defined by $E_\lambda = \operatorname{Ker}(\lambda Id - A)$.

Eigenvalues coincide with characteristic values:

$$\det(\lambda Id - A) = 0 \iff \dim(\operatorname{Ker}(\lambda Id - A)) \ge 1 \iff \exists u \ne 0, \lambda u - Au = 0.$$

These two points of view respectively correspond to the algebraic and the geometric approach to eigenvalues. The geometric viewpoint considers the action of the linear operator $A$ on vectors in the ambient space with more precision than in the algebraic viewpoint. In particular, they differ in the notion of multiplicity of an eigenvalue: the algebraic multiplicity is the multiplicity of the root in the characteristic polynomial while the geometric multiplicity is the dimension of the eigenspace associated to the eigenvalue. When the matrix is diagonalisable, these notions are equivalent, but otherwise the geometric multiplicity is less than or equal to the algebraic multiplicity.

The geometric point of view gives finer details on the structure of the matrix. It also helps designing efficient algorithms to compute eigenvalues, eigenvectors and the characteristic and minimal polynomials.

# **Cyclic Invariant Subspace and Frobenius Normal Form.**

Let $A$ be an $n \times n$ matrix over a field $K$ and $u \in K^n$ a vector. The vectors $u, Au, A^2u, \ldots, A^n u$, called the Krylov sequence, are linearly dependent (as it is a set of $n+1$ vectors of dimension $n$). Let $d$ be the first index such that $A^d u$ is linearly dependent with its predecessors $u, Au, \ldots, A^{d-1}u$. We can write this linear dependence relation as

$$A^d u = \sum_{i=0}^{d-1} \alpha_i A^i u.$$

The polynomial $\varphi_{A,u}(x) = x^d - \sum_{i=0}^{d-1} \alpha_i x^i$, satisfying the relation $\varphi_{A,u}(A)u = 0$ is therefore a monic polynomial annihilating the Krylov sequence, of minimal