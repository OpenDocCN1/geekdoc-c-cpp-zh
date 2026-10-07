# 234 NUMERICAL LINEAR ALGEBRA

write $A = \{a_{ij}\} = LL^T$ for

```
$L = \begin{pmatrix} l_{11} & 0 & 0 & 0 \ l_{21} & l_{22} & 0 & 0 \ l_{31} & l_{32} & l_{33} & 0 \ \vdots & \vdots & \vdots & \vdots \ l_{n1} & l_{n2} & l_{n3} & l_{nn} \end{pmatrix}$
```

But, if that is the case, the system $A = LL^T$ can be solved directly for the elements $l_{ij}$ of $L$ in terms of the elements of $A$. This approach produces

```
$l_{11} = \sqrt{a_{11}}
lnl_{21} = a_{21}/l_{11}\nl\vdots\nl_{n1} = a_{n1}/l_{11}$
```

which leads to

```
$l_{22} = \sqrt{a_{22}-l_{21}^2}\nl_{32} = (a_{32}-l_{31}l_{21})/l_{22}\nl\vdots\nl_{n2} = (a_{n2}-l_{n1}l_{21})/l_{22}$
```

The general or $j$th step is

```
$l_{jj} = \sqrt{a_{jj}-\sum_{k=1}^{j-1}l_{jk}^2} \quad (7.2)\nl_{ij} = (a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk})/l_{jj}, \quad i=j+1,\dots,n. \quad (7.3)$
```

The Cholesky recursion can be summarized in Algorithm 7.2.

**Algorithm 7.2** Cholesky algorithm
$l_{11} = \sqrt{a_{11}}, a_{i1}/l_{11}, i=2,\dots,n$
for $j=2,\dots,n-1$ **do**
l$l_{jj} = \sqrt{a_{jj}-\sum_{k=1}^{j-1}l_{jk}^2}$
ll_{ij} = (a_{ij}-\sum_{k=1}^{j-1}l_{ik}l_{jk})/l_{jj}, i=j+1,\dots,n$
**end for**
lnl_{nn} = \sqrt{a_{nn}-\sum_{k=1}^{n-1}l_{nk}^2}$

The algorithm uses (7.2)–(7.3) to factorize $A$. Then, given $L$, the system $Ab=c$ is solved as noted in Section 7.2.1 by forward-substitution and back-solving.

Like Gaussian elimination the Cholesky algorithm has complexity on the order of $n^3$. However, one can show that it requires only half the effort of Gaussian elimination (Exercise 7.3).

```
Forward-solve $L=c$ for $h$
Back-solve $L^Tb=h$ for $b$
return $b$
```