# Chapter 13

# Matrix Representation

In this chapter we shall establish the connection between linear mappings and matrices. Our discussion, in particular, generalizes Theorems 10.1 and 10.2. We shall also introduce the concept of similar matrices, which plays an important role in later chapters.

As in Chapter 12, unless specified, here we shall also consider the finite dimensional vector spaces V and W over the same field F. Let $S=\{u^1,\ldots,u^n\}$ and $T=\{w^1,\ldots,w^m\}$ be ordered bases for V and W, respectively, and $L:V\to W$ be a linear mapping. Then, for each $j=1,\ldots,n$ there exist unique scalars $a_{ij}$, $i=1,\ldots,m$ such that

$$L(u^j)=a_{1j}w^1+\cdots+a_{mj}w^m=\sum_{i=1}^{m}a_{ij}w^i. \tag{13.1}$$

Clearly, $(a_{1j},\ldots,a_{mj})^t\in F^m$ are the coordinates of $L(u^j)$ in the ordered basis $T$. Thus, (13.1) implies that the linear mapping $L$ is completely determined by the scalars $a_{ij}$. This unique $m\times n$ matrix $A=(a_{ij})$ is called the transition matrix of $L$ relative to the bases $S$ and $T$. Now let $u=x_1u^1+\cdots+x_nu^n$ be a vector in $V$. Then from (13.1) it follows that

$$L(u)=L\left(\sum_{j=1}^{n}x_ju^j\right)=\sum_{j=1}^{n}x_jL(u^j)$$
$$\phantom{L(u)}=\sum_{j=1}^{n}x_j\left(\sum_{i=1}^{m}a_{ij}w^i\right)=\sum_{i=1}^{m}\left(\sum_{j=1}^{n}a_{ij}x_j\right)w^i.$$

Thus, if
$$w=L(u)=y_1w^1+\cdots+y_mw^m, \tag{13.2}$$
then we have
$$y_i=\sum_{j=1}^{n}a_{ij}x_j. \tag{13.3}$$

Hence, if $(x_1,\ldots,x_n)^t_S$ are the coordinates of $u\in V$ and $(y_1,\ldots,y_m)^t_T$ are the coordinates of $w=L(u)\in W$, then
$$y=Ax\quad\text{or}\quad y_T(L(u))=Ax_S(u). \tag{13.4}$$