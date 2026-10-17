
## Remark 14.1.

From (14.6), we have

\(u^i=(c_{i1}v^1+\cdots+c_{i,i-1}v^{i-1})+v^i,i=1,\cdots,n\)

and hence if \(S\) and \(T\) are ordered bases, then for changing the basis from \(T\) to \(S\) the transition matrix is lower triangular and nonsingular as each diagonal element is 1. Then the inverse of this matrix is also lower triangular (see Problem 4.4), i.e., there exist scalars \(d_{ij},i=1,\cdots,n,j=1,\cdots,i\) such that

\(v^i=d_{i1}u^1+\cdots+d_{ii}u^i.\)

## Remark 14.2.

Let \((V,C)\) be an \(n\)-dimensional inner product space, and let \(u^1,\cdots,u^r,r<n\) be orthogonal vectors of \(V\). Then, from Corollary 9.3 and Theorem 14.4 it follows that there are vectors \(u^{r+1},\cdots,u^n\) in \(V\) such that \(S=\{u^1,\cdots,u^n\}\) is an orthogonal basis of \(V\).

## Theorem 14.5.

Let \((V,C)\) be an \(n\)-dimensional inner product space, and let \(U\) be a subspace of \(V\). Then, \(V=U\oplus U^\perp\).

### Proof.

In view of Theorem 14.4, there exists an orthogonal basis \(\{u^1,\cdots,u^r\}\) of \(U\), and by Remark 14.2, we can extend it to an orthogonal basis \(\{u^1,\cdots,u^n\}\) of \(V\). Clearly, \(u^{r+1},\cdots,u^n\in U^\perp\). Now let \(u\in V\), then

\(u=c_1u^1+\cdots+c_ru^r+c_{r+1}u^{r+1}+\cdots+c_nu^n,\)

where \(c_1u^1+\cdots+c_ru^r\in U\) and \(c_{r+1}u^{r+1}+\cdots+c_nu^n\in U^\perp\). Thus, \(V=U\oplus U^\perp\). On the other hand, if \(v\in U\cap U^\perp\), then \((v,v)=0\), and this implies that \(v=0\), and hence \(U\cap U^\perp=\{0\}\). Therefore, from Theorem 9.6, we have \(V=U\oplus U^\perp\).

## Example 14.8.

For a given \(m\times n\) matrix \(A\) if \(\{u^1,\cdots,u^r\}\) is a basis (orthogonal basis) of \(R(A)\) and \(\{u^{r+1},\cdots,u^n\}\) is a basis (orthogonal basis) for \(\mathcal{N}(A)\), then from Theorems 11.4 and 14.5 it immediately follows that \(\{u^1,\cdots,u^n\}\) is a basis (orthogonal basis) for \(R^n\). Thus the set of vectors \(\{(1,2,1,5)^t,(0,0,1,2)^t,(-2,1,0,0)^t,(-3,0,-2,1)^t\}\) obtained in Example 11.1 form a basis of \(R^4\).

## Remark 14.3.

Theorem 14.5 holds for infinite dimensional inner product spaces also.

## Remark 14.4.

In view of Theorem 14.5 every \(v\in V\) can be uniquely written as \(v=u+u'\), where \(u\in U\) and \(u'\in U^\perp\). We say \(u\) is the _orthogonal projection of v along U_, and denote it by \(\text{proj}(v,U)\), or \(\text{proj}_Uv\). In particular, if \(U\) is spanned by an orthogonal set \(S=\{u^1,\cdots,u^r\}\), then \(\text{proj}_Sv=\text{proj}_Uv=c_1u^1+\cdots+c_ru^r\) where \(c_i=(v,u^i)/(u^i,u^i),i=1,\cdots,r\). Thus, \(\text{proj}_Uv=\sum_{i=1}^r\text{proj}_{u^i}v\). In the case where \(S\) is ordered, then \((c_1,\cdots,c_r)^t\) are the coordinates of \(u\) with respect to the set \(S\).

## Problems

**14.1.** For the vectors \(u=(a_1,a_2,a_3)^t,v=(b_1,b_2,b_3)^t \in R^3\) the _cross product_ (valid only in \(R^3\)), denoted as \(u \times v \in R^3\), is defined as

\(u \times v = (a_2b_3 - a_3b_2, a_3b_1 - a_1b_3, a_1b_2 - a_2b_1)^t.\)

Show that for all vectors \(u,v,w \in R^3\)

- (i) \(u \times v = -(v \times u)\)
- (ii) \(u \times u = 0\)
- (iii) the vector \(u \times v\) is orthogonal to both \(u\) and \(v\)
- (iv) \(u \times (v + w) = (u \times v) + (u \times w)\)
- (v) \((u \times v) \times w = (u,w)v - (v,w)u\)
- (vi) \((u \times v)^2 = ((u \times v),(u \times v)) = (u,u)(v,v) - (u,v)^2\)
- (vii) the absolute value of the _triple product_ \((u,(v \times w))\) represents the volume of the parallelepiped formed by the vectors \(u,v,w\).

**14.2.** Let \(u=(a_1,\cdots,a_m)^t \in R^m\), \(v=(b_1,\cdots,b_n)^t \in R^n\). The _outer product_ of \(u\) and \(v\) is defined as \(uv^t\), which is an \(m \times n\) matrix. For \(m=n\) show that \(u^tv = \text{tr}(uv^t) = \text{tr}(vu^t)\).

**14.3.** Let \((V,R)\) be an \(n\)-dimensional vector space, and let \(S = \{u^1,\cdots,u^n\}\) be an ordered basis for \(V\). If \(u,v \in V\) are such that \(u = a_1u^1 + \cdots + a_nu^n\) and \(v = b_1u^1 + \cdots + b_nu^n\), then show that \((u,v) = (y_S(u),y_S(v)) = \sum_{i=1}^n a_ib_i\) is an inner product on \(V\).

**14.4.** Let \((V,R)\) be an \(n\)-dimensional inner product space, and let \(S = \{u^1,\cdots,u^n\}\) be an ordered basis for \(V\). Show that

- (i) the _matrix of the inner product_ \(C = (c_{ij})\), where \(c_{ij} = (u^i,u^j)\) is symmetric
- (ii) if \(a = (a_1,\cdots,a_n)^t\) and \(b = (b_1,\cdots,b_n)^t\) are the coordinates of the vectors \(u,v \in V\), then \((u,v) = a^tCb\), i.e., the matrix \(C\) determines \((u,v)\) for every \(u\) and \(v\) in \(V\).

**14.5.** Let \(V\) and \(W\) be finite dimensional inner product spaces with inner products \((\cdot,\cdot)_V\) and \((\cdot,\cdot)_W\), and let \(T: V \rightarrow W\) be a linear mapping. The mapping (if it exists) \(T^*: W \rightarrow V\) is called the _adjoint mapping_ of \(T\) if for all \(u \in V\) and \(w \in W\), \((T(u),w)_W = (u,T^*(w))_V\). Show that

- (i) if \(T = A \in R^{m \times n}\), then \(T^* = A^t\)
- (ii) if \(T = A \in C^{m \times n}\), then \(T^* = A^H\)
- (iii) \((T^*)^* = T\).

**14.6.** Find a nonzero vector \(v\) that is orthogonal to the given vectors

- (i) \((1,3,5)^t\), \((3,5,1)^t\), \(v \in R^3\)
- (ii) \((1,1,2,2)^t, (1,3,3,1)^t, (5,5,1,1)^t, v \in R^4\).

**14.7.** Find a basis for the subspace \(u^\perp\) of \(R^3\), where

- (i) \(u = (1,3,5)^t\)
- (ii) \(u = (-1,0,1)^t\).

**14.8.** Let \(U, W\) be subsets of an inner product space \(V\). Show that

- (i) \(U \subseteq U^{\perp\perp}\)
- (ii) if \(U \subseteq W\), then \(W^\perp \subseteq U^\perp\)
- (iii) \(U^\perp = \text{span}(U)^\perp\).

**14.9.** Let \(U, W\) be subspaces of a finite dimensional inner product space \(V\). Show that

- (i) \(U = U^{\perp\perp}\)
- (ii) \((U + W)^\perp = U^\perp \cap W^\perp\)
- (iii) \((U \cap W)^\perp = U^\perp + W^\perp\).

**14.10.** Let \(\{\tilde{u}^1, \cdots, \tilde{u}^n\}\) and \(\{\tilde{v}^1, \cdots, \tilde{v}^n\}\) be orthonormal ordered bases of an \(n\)-dimensional real inner product space \(V\). Show that the transition matrix \(A\) defined in (10.4) is orthogonal.

**14.11.** Let \(A\) be a real (complex) square matrix. Show that the following are equivalent

- (i) \(A\) is orthogonal (unitary)
- (ii) the rows of \(A\) form an orthonormal set
- (iii) the columns of \(A\) form an orthonormal set.

**14.12.** For the matrices given in Problem 11.1 use the method of Example 14.8 to find bases of \(R^5\) and \(R^6\).

**14.13.** For the given basis for \(R^3\) use the Gram–Schmidt orthogonalization process to find an orthonormal basis for \(R^3\)

- (i) \(\{(1,1,1)^t, (-1,1,0)^t, (-1,0,1)^t\}\)
- (ii) \(\{(1,0,1)^t, (0,-1,1)^t, (0,-1,-1)^t\}\).

**14.14.** Enlarge the following sets of linearly independent vectors to orthonormal bases of \(R^3\) and \(R^4\)

- (i) \(\{(1,1,1)^t, (1,1,2)^t\}\)
- (ii) \(\{(1,1,1,3)^t, (1,2,3,4)^t, (2,3,4,9)^t\}\).

## Inner Products and Orthogonality

**14.15.** Show that the set

\(\left\{\sqrt{\frac{2}{\pi}} \sin nx, \ n = 1, 2, \cdots \right\}\)

is orthonormal on \(0 < x < \pi\). This set generates the Fourier sine series.

**14.16.** Show that the set

\(\left\{\frac{1}{\sqrt{\pi}}, \sqrt{\frac{2}{\pi}} \cos nx, \ n = 1, 2, \cdots \right\}\)

is orthonormal on \(0 < x < \pi\). This set generates the Fourier cosine series.

**14.17.** Show that the set

\(\left\{\frac{1}{\sqrt{2\pi}}, \frac{1}{\sqrt{\pi}} \cos nx, \frac{1}{\sqrt{\pi}} \sin nx, \ n = 1, 2, \cdots \right\}\)

is orthonormal on \(-\pi < x < \pi\). This set generates the Fourier trigonometric series.

**14.18.** _Legendre polynomials_, denoted as \(P_n(x)\), \(n = 0, 1, 2, \cdots\) can be defined by _Rodrigues’ formula_

\(P_n(x) = \frac{1}{2^n n!} \frac{d^n}{dx^n}(x^2 - 1)^n, \quad n = 0, 1, 2, \cdots\)  (14.7)

In fact, from (14.7) we easily obtain

\(P_0(x) = 1, \quad P_1(x) = x, \quad P_2(x) = \frac{1}{2}(3x^2 - 1), \quad P_3(x) = \frac{1}{2}(5x^3 - 3x),\)

\(P_4(x) = \frac{1}{8}(35x^4 - 30x^2 + 3), \quad P_5(x) = \frac{1}{8}(63x^5 - 70x^3 + 15x), \cdots\)

Show that the set \(\{P_0(x), P_1(x), P_2(x), \cdots \}\) is orthogonal in the interval \([-1, 1]\).

**14.19.** Consider the space \(V\) of all real infinite sequences \(u = (a_1, a_2, \cdots)\) satisfying \(\sum_{i=1}^\infty a_i^2 < \infty\). Addition and scalar multiplication for all \(u = (a_1, a_2, \cdots), v = (b_1, b_2, \cdots) \in V\), \(c \in R\) is defined as \((u + v) = (a_1 + b_1, a_2 + b_2, \cdots)\), \(cu = (ca_1, ca_2, \cdots)\). Show that

- (i) \(V\) is a vector space
- (ii) the inner product \((u, v) = a_1b_1 + a_2b_2 + \cdots\) is well defined, i.e., \(\sum_{i=1}^\infty a_ib_i\) converges absolutely.

This inner product space is called \(\ell_2\)-_space_ and is an example of a _Hilbert space_.
