

## Corollary 9.1.

Let \((V, F)\) be a vector space, and let \(S = \{u^1, \cdots, u^n\}\) and \(T = \{v^1, \cdots, v^m\}\) be the basis of \(V\). Then, \(m = n\).

## Proof.

In view of Theorem 9.1, \(m > n\) is impossible. Now since \(T\) is also a basis, \(n > m\) is also impossible. \(\blacksquare\)

Let \((V, F)\) be a vector space, and let \(T = \{v^1, \cdots, v^m\} \subset V\). We say that \(S = \{v^{k_1}, \cdots, v^{k_n}\} \subseteq T\) is a *maximal linearly independent subset* of \(T\) if \(S\) is linearly independent, and if \(v^i \in T \backslash S\), then \(S \cup \{v^i\}\) is linearly dependent.

## Theorem 9.2.

Let \(T = \{v^1, \cdots, v^m\}\) generate the vector space \((V, F)\), and let \(S = \{v^{k_1}, \cdots, v^{k_n}\}\) be a maximal linearly independent subset of \(T\). Then \(S\) is a basis of \(V\).

## Proof.

We need to show that \(S = \{v^{k_1}, \cdots, v^{k_n}\}\) generates \(V\). For this, first we shall prove that each \(v^i \in T \backslash S\) is a linear combination of \(v^{k_1}, \cdots, v^{k_n}\). Since \(S \cup \{v^i\}\) is linearly dependent, there exist scalars \(c_1, \cdots, c_n, x\) not all zero such that

\(c_1 v^{k_1} + \cdots + c_n v^{k_n} + x v^i = 0.\)

Clearly, \(x \neq 0\), otherwise, \(S\) will be linearly dependent. Thus, it follows that

\(v^i = \frac{-c_1}{x} v^{k_1} + \cdots + \frac{-c_n}{x} v^{k_n},\)

which confirms that \(v^i\) is a linear combination of \(v^{k_1}, \cdots, v^{k_n}\). Now let \(u \in V\), then there exist scalars \(\alpha_1, \cdots, \alpha_m\) such that

\(u = \alpha_1 v^1 + \cdots + \alpha_m v^m.\)

In this relation, we replace each \(v^i \in T \backslash S\) by a linear combination of \(v^{k_1}, \cdots, v^{k_n}\). The resulting relation on grouping the terms will lead to a linear combination of \(v^{k_1}, \cdots, v^{k_n}\) for \(u\). Thus \(S\) generates \(V\). \(\blacksquare\)

Let \((V, F)\) be a vector space, and let \(S = \{u^1, \cdots, u^n\} \subset V\) be linearly independent. We say that \(S\) is a *maximal linearly independent set* of \(V\) if and only if \(u \in V \backslash S\), then \(S \cup \{u\}\) is linearly dependent.

## Theorem 9.3.

Let \(S = \{u^1, \cdots, u^n\}\) be a maximal linearly independent set of the vector space \((V, F)\). Then, \(S\) is a basis of \(V\).

## Proof.

The proof is the same as in the first part of Theorem 9.2. \(\blacksquare\)

A vector space \(V\) over the field \(F\) is said to be of *finite dimension* \(n\), or \(n\)-dimensional, written as \(\dim V = n\), if and only if \(V\) has a basis consisting of \(n\) vectors. If \(V = \{0\}\), we say \(V\) has dimension 0. If \(V\) does not have a finite

## Example 9.3.

Since in view of [Problems 6.1 (iii)](Problems 6.1 (iii)),

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_90_0.png)

the vectors $(0,1,1)^t$, $(1,2,2)^t$, $(0,3,6)^t$ are linearly independent and form a basis for $R^3$.

## Example 9.4.

The vectors $(0,1,1)^t$, $(1,2,2)^t$ are linearly independent. To find the third linearly independent vector, we consider the matrix whose columns are $(0,1,1)^t$, $(1,2,2)^t$, $e^1$, $e^2$, $e^3$, and note that

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_90_1.png)

Thus, the required vector is $e^2=(0,1,0)^t$.

Now let $U$ and $W$ be subspaces of a vector space $V$. Recall that in [Problem 1.4](Problem 1.4) we have defined the sum of $U$ and $W$ as $U+W=\{z:z=u+w\text{ where }u\in U,\ w\in W\}$. For this sum we shall prove the following result.

## Theorem 9.5.

Let $U$ and $W$ be subspaces of a vector space $V$. Then,

$$\dim(U+W)=\dim U+\dim W-\dim(U\cap W).$$

## Proof.

In view of [Problem 1.3](Problem 1.3), $U\cap W$ is a subspace of both $U$ and $W$. Let $\dim U=m$, $\dim W=n$, and $\dim U\cap W=r$. Let $S_1=\{v^1,\ldots,v^r\}$ be a basis for $U\cap W$. By [Corollary 9.3](Corollary 9.3) we can extend $S_1$ to a basis of $U$, say $S_2=\{v^1,\ldots,v^r,u^1,\ldots,u^{m-r}\}$ and to a basis of $W$, say, $S_3=\{v^1,\ldots,v^r,w^1,\ldots,w^{n-r}\}$. Now let $S=S_1\cup S_2\cup S_3=\{v^1,\ldots,v^r,u^1,\ldots,u^{m-r},w^1,\ldots,w^{n-r}\}$. Clearly, $S$ has exactly $m+n-r$ vectors. Thus it suffices to show that $S$ is a basis of $U+W$. For this, we note that $S_2$ spans $U$, and $S_3$ spans $W$, and hence $S_2\cup S_3=S$ spans $U+W$. To show the linear independence of $S$, suppose that

$$a_1v^1+\cdots+a_rv^r+b_1u^1+\cdots+b_{m-r}u^{m-r}+c_1w^1+\cdots+c_{n-r}w^{n-r}=0, \tag{9.1}$$

where $a_i,b_j,c_k$ are scalars. Let

$$u=a_1v^1+\cdots+a_rv^r+b_1u^1+\cdots+b_{m-r}u^{m-r}. \tag{9.2}$$

Then from $(9.1)$, we have

$$u=-c_1w^1-\cdots-c_{n-r}w^{n-r}. \tag{9.3}$$

From $(9.2)$ and $(9.3)$, respectively, it follows that $u\in U$ and $u\in W$. Thus,

u ∈ U ∩ W, and hence can be written as u = d₁v¹ + ⋯ + dᵣvʳ, where dᵢ are scalars. Thus, from (9.3) it follows that

$$d_1v^1+\cdots+d_rv^r+c_1w^1+\cdots+c_{n-r}w^{n-r}=0.$$

But since S₃ is a basis of W, the above relation implies that c₁ = ⋯ = cₙ₋ᵣ = 0. Substituting this in (9.1), we get

$$a_1v^1+\cdots+a_rv^r+b_1u^1+\cdots+b_{m-r}u^{m-r}=0.$$

Finally, since S₂ is a basis of U, the above relation implies that a₁ = ⋯ = aᵣ = b₁ = ⋯ = bₘ₋ᵣ = 0.

The vector space V is said to be a direct sum of its subspaces U and W, denoted as U ⊕ W, if for every v ∈ V there exist unique vectors u ∈ U and w ∈ W such that v = u + w.

## Example 9.5.

Consider V = ℝ³, U = {(a₁, a₂, 0)ᵗ : a₁, a₂ ∈ ℝ}, W = {(0, a₂, a₃)ᵗ : a₂, a₃ ∈ ℝ}. Then, ℝ³ = U + W but ℝ³ ≠ U ⊕ W, since sums are not necessarily unique, e.g., (1, 3, 1)ᵗ = (1, 1, 0)ᵗ + (0, 2, 1)ᵗ = (1, 2, 0)ᵗ + (0, 1, 1)ᵗ. However, if we let U = {(a₁, a₂, 0)ᵗ : a₁, a₂ ∈ ℝ}, W = {(0, 0, a₃)ᵗ : a₃ ∈ ℝ}, then ℝ³ = U ⊕ W.

## Theorem 9.6.

The vector space V is the direct sum of its subspaces U and W, i.e., V = U ⊕ W, if and only if V = U + W, and U ∩ W = {0}.

## Proof.

Suppose V = U ⊕ W. Then any v ∈ V can be uniquely written in the form v = u + w, where u ∈ U and w ∈ W. This in particular implies that V = U + W. Now let v ∈ U ∩ W, then v = v + 0 where v ∈ U, 0 ∈ W; also, v = 0 + v where 0 ∈ U, v ∈ W. But this in view of the uniqueness implies that v = 0 + 0 = 0 and U ∩ W = {0}.

Conversely, suppose that V = U + W and U ∩ W = {0}. If v ∈ V, then there exist u ∈ U and w ∈ W such that v = u + w. We need to show that this sum is unique. For this, let v = u′ + w′ where u′ ∈ U and w′ ∈ W is also such a sum. Then, u + w = u′ + w′, and hence u − u′ = w − w′. But u − u′ ∈ U and w − w′ ∈ W; therefore in view of U ∩ W = {0} it follows that u − u′ = 0 and w − w′ = 0, i.e., u = u′ and w = w′.

## Corollary 9.4.

Let U and W be subspaces of a vector space V. Then, dim U ⊕ W = dim U + dim W.

## Problems

+   1. **9.1.** Find the dimension of the following spaces spanned by all
+      (i) m × n matrices, and give a basis for this space

+   (ii) $n \times n$ diagonal matrices
+   
+   (iii) $n \times n$ upper triangular matrices
+   
+   (iv) $n \times n$ symmetric matrices
+   
+   (v) polynomials of degree $n-1$, and give a basis for this space.
+   
+   (vi) $n$ dimensional real vectors $u=(u_1,\cdots,u_n)$ such that $u_1+\cdots+u_n=0$
+   
+   (vii) $n \times n$ real matrices $A=(a_{ij})$ such that $\operatorname{tr}(A)=0$.

**9.2.** Suppose that $\{u^1,\cdots,u^n\}$ is a basis for $R^n$, and $A$ is an $n\times n$ nonsingular matrix. Show that $\{Au^1,\cdots,Au^n\}$ is also a basis for $R^n$.

**9.3.** Let $(V,F)$ be an $n$-dimensional vector space, and let $W\ne\{0\}$ be a subspace. Show that $(W,F)$ has a basis, and its dimension is $\le n$.

**9.4.** Let $U$ and $W$ be subspaces of a vector space $V$, and let $S=\{u^1,\cdots,u^\ell\}$ span $U$ and $T=\{w^1,\cdots,w^k\}$ span $W$. Show that $S\cup T$ spans $U+W$.

**9.5.** Let $U$ and $W$ be subspaces of a vector space $V$, and let $V=U\oplus W$. If $S=\{u^1,\cdots,u^\ell\}$ and $T=\{w^1,\cdots,w^k\}$ are linearly independent subsets of $U$ and $W$ respectively, show that

(i) $S\cup T$ is linearly independent in $V$

(ii) if $S$ and $T$ are bases for $U$ and $W$, then $S\cup T$ is a basis of $V$.

**9.6.** Show that the space $R$ over the field of rational numbers $Q$ with the usual operations is infinite dimensional.

**9.7.** Find $\lambda\in R$ so that the vectors $u^1=(1,\lambda,1)^t$, $u^2=(1,1,\lambda)^t$, $u^3=(1,-1,1)^t$ form a basis of $R^3$.

**9.8.** Let $V=\{u\in R^5:u_1+2u_2-u_3+u_4=0,\ u_1+u_2+u_3+u_5=0\}$. Find the dimension of $V$ and find $W$ such that $V\oplus W=R^5$.

## Answers or Hints

+   **9.1.**
+   
+   (i) $mn$, $\{E_{ij}\}$ where the $m\times n$ matrix $E_{ij}$ has elements $e_{k\ell}=1$ if $k=i,\ell=j$ and $e_{k\ell}=0$ if $k\ne i,\ell\ne j$.
+   
+   (ii) $n$.
+   
+   (iii) $n(n+1)/2$.
+   
+   (iv) $n(n+1)/2$.
+   
+   (v) $n$, $\{1,x,\cdots,x^{n-1}\}$. This basis is known as natural, or standard basis for $(P_n,R)$.
+   
+   (vi) $n-1$.
+   
+   (vii) $n^2-1$.

