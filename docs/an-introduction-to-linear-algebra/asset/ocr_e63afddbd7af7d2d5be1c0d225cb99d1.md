where $x_i,y_j\in F$. Then, we have

$$0=L(0)=L(x_1u^1+\cdots+x_ru^r+y_1v^1+\cdots+y_sv^s)$$
$$\phantom{0}=x_1L(u^1)+\cdots+x_rL(u^r)+y_1L(v^1)+\cdots+y_sL(v^s).$$

However, since $u^i\in\mathcal N(L)$, $L(u^i)=0$, and $L(v^j)=w^j$, from (12.2) it follows that $y_1w^1+\cdots+y_sw^s=0$. But, since $w^j$ are linearly independent, each $y_j=0$. Thus, (12.1) reduces to $x_1u^1+\cdots+x_ru^r=0$. However, since $u^i$ are linearly independent, each $x_i=0$.

For the linear mappings $L:V\to W$ and $G:V\to W$ the sum mapping $L+G:V\to W$, and the scalar product mapping $cL:V\to W$, $c\in F$ are respectively defined as $(L+G)(u)=L(u)+G(u)$ and $(cL)(u)=cL(u)$. It is clear that the mappings $L+G$ and $cL$ are also linear. The collection of all mappings from $V$ to $W$, denoted as $\operatorname{Hom}(V,W)$ (where Hom stands for homomorphism), with the above operations of addition and scalar multiplication forms a vector space. For this space the zero element is the zero mapping, denoted as $0$ from $V$ to $W$.

# **Theorem 12.5.**

Suppose that $\dim V=n$ and $\dim W=m$. Then, $\dim\operatorname{Hom}(V,W)=nm$.

# **Proof.**

Let $S=\{u^1,\ldots,u^n\}$ and $T=\{w^1,\ldots,w^m\}$ be ordered bases for $V$ and $W$, respectively. For each pair of integers $(i,j)$, $i=1,\ldots,m$, $j=1,\ldots,n$ we define a linear mapping $L^{i,j}$ from $V$ to $W$ as follows:

$$L^{i,j}(u^s)=\begin{cases}0&\text{if }s\ne j\\w^i&\text{if }s=j\end{cases}=\delta_{sj}w^i.$$

In view of **Theorem 12.1** such a unique linear mapping exists. Clearly, the set $\{L^{i,j}\}$ contains exactly $nm$ elements, and hence it suffices to show that it is a basis for $\operatorname{Hom}(V,W)$. For this, let $L\in\operatorname{Hom}(V,W)$ be an arbitrary mapping. Suppose $L(u^k)=v^k$, $k=1,\ldots,n$. Since each $v^k\in W$ is a linear combination of $w^i$, there exist scalars $a_{ik}$ such that

$$v^k=a_{1k}w^1+\cdots+a_{mk}w^m,\qquad k=1,\ldots,n.$$

Consider the linear mapping

$$G=\sum_{i=1}^{m}\sum_{j=1}^{n}a_{ij}L^{i,j}.$$

Clearly, we have

$$G(u^\tau)=\sum_{i=1}^{m}\sum_{j=1}^{n}a_{ij}L^{i,j}(u^\tau)=\sum_{i=1}^{m}a_{i\tau}w^i=v^\tau=L(u^\tau),\qquad \tau=1,\ldots,n.$$