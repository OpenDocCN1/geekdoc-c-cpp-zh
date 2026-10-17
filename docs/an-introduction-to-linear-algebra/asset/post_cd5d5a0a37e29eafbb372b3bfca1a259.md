
W of R<sup>4</sup> spanned by w<sup>1</sup> = (1, 2, 0, -1) and w<sup>2</sup> = (5, 2, 4, 9). Since W<sup>0</sup> = [Span(W)]<sup>0</sup>, it suffices to find a basis of the set of linear functionals φ such that φ(w<sup>1</sup>) = 0 and φ(w<sup>2</sup>) = 0, where φ(w<sub>1</sub>, w<sub>2</sub>, w<sub>3</sub>, w<sub>4</sub>) = aw<sub>1</sub> + bw<sub>2</sub> + cw<sub>3</sub> + dw<sub>4</sub>. For this, the system

has solutions with c and d as free variables. We fix c = 1 and d = 0, to get a = -1 and b = 1/2. Next, we fix c = 0 and d = 1, to get a = -5/2 and b = 7/4. Hence, the following linear functions

form the basis of W<sup>0</sup>. Similarly, a basis of the annihilator W<sup>0</sup> of the subspace W of R<sup>4</sup> spanned by w<sup>1</sup> = (1, 2, 0, -1), w<sup>2</sup> = (5, 2, 4, 9), and w<sup>3</sup> = (-2, 2, -3, 2) is the linear function φ(w<sup>i</sup>) = -2w<sub>1</sub> + w<sub>2</sub> + 2w<sub>3</sub>, i = 1, 2, 3.

Now we shall prove the following important result.

## Theorem 15.5 (Riesz representation theorem)
Let V be a finite dimensional vector space over the field F (F = R, C) on which (., .) is an inner product. Let f : V → F be a linear functional on V. Then, there exists a vector u ∈ V such that f(v) = (v, u) for all v ∈ V.

### Proof
Using the Gram-Schmidt orthogonalization process we can find an orthonormal basis of V, say, {v<sup>1</sup>, ⋯ , v<sup>n</sup>}. Now for an arbitrary vector v ∈ V, we have v = (v, v<sup>1</sup>)v<sup>1</sup> + ⋯ + (v, v<sup>n</sup>)v<sup>n</sup>. Thus, it follows that f(v) = (v, v<sup>1</sup>)f(v<sup>1</sup>) + ⋯ + (v, v<sup>n</sup>)f(v<sup>n</sup>) = (v, v<sup>1</sup><o>f(v<sup>1</sup>)</o> + ⋯ + v<sup>n</sup><o>f(v<sup>n</sup>)</o>). Denoting by u = v<sup>1</sup><o>f(v<sup>1</sup>)</o> + ⋯ + v<sup>n</sup><o>f(v<sup>n</sup>)</o>, the result follows. ■

### Remark 15.2
The vector u in Theorem 15.5 is unique. Indeed, if there are two vectors u<sup>1</sup>, u<sup>2</sup> such that f(v) = (v, u<sup>1</sup>) = (v, u<sup>2</sup>), then (v, u<sup>1</sup> - u<sup>2</sup>) = 0 for all v ∈ V. But then for v = u<sup>1</sup> - u<sup>2</sup> ∈ V it follows that 0 = (u<sup>1</sup> - u<sup>2</sup>, u<sup>1</sup> - u<sup>2</sup>) = ||u<sup>1</sup> - u<sup>2</sup>||<sup>2</sup> = 0, which implies that u<sup>1</sup> = u<sup>2</sup>.

Let V and W be two vector spaces on which inner products are defined. Let f : V → W be a linear mapping. For each vector w ∈ W, we define a map f<sub>w</sub> : V → R as f<sub>w</sub>(v) = (f(v), w). It follows that this map is a linear functional. Indeed, we have f<sub>w</sub>(v<sup>1</sup> + v<sup>2</sup>) = (f(v<sup>1</sup> + v<sup>2</sup>), w) = (f(v<sup>1</sup>) + f(v<sup>2</sup>), w) = (f(v<sup>1</sup>), w) + (f(v<sup>2</sup>), w) = f<sub>w</sub>(v<sup>1</sup>) + f<sub>w</sub>(v<sup>2</sup>), also f<sub>w</sub>(αv) = (f(αv), w) = (αf(v), w) = αf<sub>w</sub>(v).

### Example 15.7
Let f : R<sup>2</sup> → R<sup>3</sup> given by f(v<sub>1</sub>, v<sub>2</sub>) = (v<sub>1</sub> - 2v<sub>2</sub>, -7v<sub>1</sub>, 4v<sub>1</sub> - 9v<sub>2</sub>). Let w = (-3, 1, 2) ∈ R<sup>3</sup>. Then, we have f<sub>w</sub>(v) = -3(v<sub>1</sub> - 2v<sub>2</sub>) + 1(-7v<sub>1</sub>) + 2(4v<sub>1</sub> - 9v<sub>2</sub>) = -2v<sub>1</sub> - 12v<sub>2</sub>.

In view of above notations and Riesz’s Theorem for the linear functional

φ(w<sup>1</sup>) = φ(1, 2, 0, -1) = a + 2b + 0c - d = 0 φ(w<sup>2</sup>) = φ(5, 2, 4, 9) = 5a + 2b + 4c + 9d = 0

φ<sub>1</sub>(w<sup>1</sup>) = -w<sub>1</sub> + 1/2w<sub>2</sub> + w<sub>3</sub> and φ<sub>2</sub>(w<sup>2</sup>) = -5/2w<sub>1</sub> + 7/4w<sub>2</sub> + w<sub>4</sub>

Thus, it follows that $(f(v),w)=(v,f^*(w))$ for all $v\in V$ and $w\in W$.

From Remark 15.2, the map $f^*:W\to V$ is well defined and is called the adjoint of the linear mapping $f$.

## Theorem 15.6
If $f:V\to W$ is a linear mapping, then the adjoint map $f^*:W\to V$ is also a linear mapping.

### Proof
For all $v\in V$, we have $(v,f^*(w^1+w^2))=(f(v),w^1+w^2)=(f(v),w^1)+(f(v),w^2)=(v,f^*(w^1))+(v,f^*(w^2))=(v,f^*(w^1)+f^*(w^2))$. But then from Remark 15.2 it follows that $f^*(w^1+w^2)=f^*(w^1)+f^*(w^2)$. Now for $\alpha\in R$ and all $v\in V$, we have $(v,f^*(\alpha w))=(f(v),\alpha w)=\alpha(f(v),w)=\alpha(v,f^*(w))=(v,\alpha f^*(w))$, which implies that $f^*(\alpha w)=\alpha f^*(w)$.

### Example 15.8
We consider the same linear mapping as in Example 15.7, and let $(a,b,c)\in R^3$. Then, from $(f(v_1,v_2),(a,b,c))=((v_1-2v_2,-7v_1,4v_1-9v_2),(a,b,c))=a(v_1-2v_2)+b(-7v_1)+c(4v_1-9v_2)=v_1(a-7b+4c)+v_2(-2a-9c)=((v_1,v_2),(a-7b+4c,-2a-9c))$, we have $f^*(a,b,c)=(a-7b+4c,-2a-9c)$.

## Problems

- 15.1. For the given basis $S=\{(11,19,21),(3,6,7),(4,5,8)\}$ of $R^3$, find its dual basis.

- 15.2. For the given basis $S=\{(1,2,1,5),(0,0,1,2),(-2,1,0,0),(-3,0,-2,1)\}$ of $R^4$, find its dual basis.

- 15.3. For $f\in(P_3,R)$ let the linear functionals $\phi_{-1},\phi_0,\phi_1$ be defined by $\phi_{-1}(f(x))=f(-1)$, $\phi_0(f(x))=f(0)$, $\phi_1(f(x))=f(1)$. Show that $S^*=\{\phi_{-1},\phi_0,\phi_1\}$ is linearly independent, and find the basis $S$ of $(P_3,R)$ so that $S^*$ is its dual.

- 15.4. Repeat Problem 15.3 with $\phi_{-1}(f(x))=\int_{-1}^{0}f(x)dx$, $\phi_0(f(x))=f(0)$, $\phi_1(f(x))=\int_{0}^{1}f(x)dx$.

- 15.5. Let $V$, $S$ and $S^*$ be as in Theorem 15.1. Then, show that for any $u\in V$, $u=\sum_{i=1}^{n}\phi_i(u)u^i$, and for any $\phi\in V^*$, $\phi=\sum_{i=1}^{n}\phi(u^i)\phi_i$.

- 15.6. Let $(V,R)$ be a real inner product space. For each $u\in V$ we define the linear functional as $L_u(v)=(u,v)$ for all $v\in V$. Show that
  - (i) the set of all linear functionals $L_u$, denoted as $\widetilde V$, is a linear space
  - (ii) $L_u=0$ if and only if $u=0$

## Chapter 16

## Eigenvalues and Eigenvectors

Eigenvalues and eigenvectors of a matrix are of great importance in the qualitative as well as quantitative study of many physical problems. For example, stability of an aircraft is determined by the location of the eigenvalues of a certain matrix in the complex plane. Basic solutions of ordinary differential and difference equations with constant coefficients are expressed in terms of eigenvalues and eigenvectors of the coefficient matrices. In this chapter we shall mainly summarize properties of the eigenvalues and eigenvectors of matrices, which are of immense value.

The number \(\lambda\), real or complex, is called an _eigenvalue_ (_characteristic root_, _latent root_, _proper value_) of an \(n \times n\) matrix _A_ if there exists a nonzero real or complex vector _u_ such that \(Au = \lambda u\), i.e., _Au_ is parallel to _u_. The vector _u_ is called an _eigenvector_, corresponding to the eigenvalue \(\lambda\). From Corollary 5.1, \(\lambda\) is an eigenvalue of _A_ if and only if it is a solution of the _characteristic equation_

\(p(\lambda) = \det(A - \lambda I) = 0,\) (16.1)

which in the expanded form, known as _characteristic polynomial_ of _A_, can be written as

\(p(\lambda) = (-1)^n \lambda^n + a_1 \lambda^{n-1} + \cdots + a_{n-1} \lambda + a_n = 0.\) (16.2)

Thus from the _fundamental theorem of algebra_ it follows that _A_ has exactly _n_ eigenvalues counting with their multiplicities, i.e., (16.2) can be rewritten as

\(p(\lambda) = (-1)^n (\lambda - \lambda_1)^{r_1} (\lambda - \lambda_2)^{r_2} \cdots (\lambda - \lambda_m)^{r_m} = 0,\) (16.3)

where \(\lambda_i \neq \lambda_j\), \(r_i \geq 1\), \(r_1 + \cdots + r_m = n\). The positive number _r<sub>i</sub>_ is called the _algebraic multiplicity_ of the eigenvalue \(\lambda_i\).

Knowing the distinct eigenvalues \(\lambda_i\), \(i = 1, \cdots, m\) (\(\leq n\)) from (16.3), the corresponding eigenvectors can be obtained by computing nontrivial solutions of the homogenous systems \((A - \lambda_i I)u^i = 0\), \(i = 1, \cdots, m\).

### Example 16.1
The characteristic polynomial for the matrix

\(A = \begin{pmatrix} 2 & 1 & 0 \\ 1 & 3 & 1 \\ 0 & 1 & 2 \end{pmatrix}\) (16.4)
