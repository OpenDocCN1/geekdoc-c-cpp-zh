# Remark 14.1.

From (14.6), we have

\(u^i=(c_{i1}v^1+\cdots+c_{i,i-1}v^{i-1})+v^i,i=1,\cdots,n\)

and hence if \(S\) and \(T\) are ordered bases, then for changing the basis from \(T\) to \(S\) the transition matrix is lower triangular and nonsingular as each diagonal element is 1. Then the inverse of this matrix is also lower triangular (see Problem 4.4), i.e., there exist scalars \(d_{ij},i=1,\cdots,n,j=1,\cdots,i\) such that

\(v^i=d_{i1}u^1+\cdots+d_{ii}u^i.\)

# Remark 14.2.

Let \((V,C)\) be an \(n\)-dimensional inner product space, and let \(u^1,\cdots,u^r,r<n\) be orthogonal vectors of \(V\). Then, from Corollary 9.3 and Theorem 14.4 it follows that there are vectors \(u^{r+1},\cdots,u^n\) in \(V\) such that \(S=\{u^1,\cdots,u^n\}\) is a orthogonal basis of \(V\).

# Theorem 14.5.

Let \((V,C)\) be an \(n\)-dimensional inner product space, and let \(U\) be a subspace of \(V\). Then, \(V=U\oplus U^\perp\).

# Proof.

In view of Theorem 14.4, there exists an orthogonal basis \(\{u^1,\cdots,u^r\}\) of \(U\), and by Remark 14.2, we can extend it to an orthogonal basis \(\{u^1,\cdots,u^n\}\) of \(V\). Clearly, \(u^{r+1},\cdots,u^n\in U^\perp\). Now let \(u\in V\), then

\(u=c_1u^1+\cdots+c_ru^r+c_{r+1}u^{r+1}+\cdots+c_nu^n,\)

where \(c_1u^1+\cdots+c_ru^r\in U\) and \(c_{r+1}u^{r+1}+\cdots+c_nu^n\in U^\perp\). Thus, \(V=U\oplus U^\perp\). On the other hand, if \(v\in U\oplus U^\perp\), then \((v,v)=0\), and this implies that \(v=0\), and hence \(U\oplus U^\perp=\{0\}\). Therefore, from Theorem 9.6, we have \(V=U\oplus U^\perp\).

# Example 14.8.

For a given \(m\times n\) matrix \(A\) if \(\{u^1,\cdots,u^r\}\) is a basis (orthogonal basis) of \(R(A)\) and \(\{u^{r+1},\cdots,u^n\}\) is a basis (orthogonal basis) for \(\mathcal{N}(A)\), then from Theorems 11.4 and 14.5 it immediately follows that \(\{u^1,\cdots,u^n\}\) is a basis (orthogonal basis) for \(R^n\). Thus the set of vectors \(\{(1,2,1,5)^t,(0,0,1,2)^t,(-2,1,0,0)^t,(-3,0,-2,1)^t\}\) obtained in Example 11.1 form a basis of \(R^4\).

# Remark 14.3.

Theorem 14.5 holds for infinite dimensional inner product spaces also.

# Remark 14.4.

In view of Theorem 14.5 every \(v\in V\) can be uniquely written as \(v=u+u'\), where \(u\in U\) and \(u'\in U^\perp\). We say \(u\) is the _orthogonal projection of v along U_, and denote it by \(\text{proj}(v,U)\), or \(\text{proj}_Uv\). In particular, if \(U\) is spanned by an orthogonal set \(S=\{u^1,\cdots,u^r\}\), then \(\text{proj}_Sv=\text{proj}_Uv=c_1u^1+\cdots+c_ru^r\) where \(c_i=(v,u^i)/(u^i,u^i),i=1,\cdots,r\). Thus, \(\text{proj}_Uv=\sum_{i=1}^r\text{proj}_{u^i}v\). In the case where \(S\) is ordered, then \((c_1,\cdots,c_r)^t\) are the coordinates of \(u\) with respect to the set \(S\).