from (13.4) it follows that

$$y_T(L(u))=Ax_S(u)=A(c,b-c,a-b)^t=\left(c-b+\frac{1}{3}a,b-c+\frac{1}{3}a\right)^t.$$

In view of (13.5), we also have

$$L(u)=(a+b-c,a-b+c)^t=\left(c-b+\frac{1}{3}a\right)(1,2)^t+\left(b-c+\frac{1}{3}a\right)(2,1)^t,$$

which confirms (13.6).

Conversely, assume that an $m\times n$ matrix $A$ is given. Then from the relation (13.4) we can compute the coordinates $y_T(L(u))$ for the unknown mapping $L$. But, then (13.2) uniquely determines the mapping $L:V\to W$. It can easily be verified that this mapping is linear. In conclusion, we find that for the two given vector spaces $V$ and $W$ with fixed ordered bases $S$ and $T$, there exists a one-to-one correspondence between the set of all linear mappings $L:V\to W$ and the set of all matrices $M^{m\times n}$.

Now let $S=\{u^1,\ldots,u^n\}$, $\widetilde S=\{\widetilde u^1,\ldots,\widetilde u^n\}$ be ordered bases for $V$, and $T=\{w^1,\ldots,w^m\}$, $\widetilde T=\{\widetilde w^1,\ldots,\widetilde w^m\}$ be ordered bases for $W$, and $L:V\to W$ be a linear mapping. Since $L$ can be characterized by $A=A_{ST}=(a_{ij})$ and $B=A_{\widetilde S\widetilde T}=(b_{ij})$, it is natural to know the relation between these matrices. For this, let

$$L(w^j)=\sum_{i=1}^{m}a_{ij}w^i,\quad j=1,\ldots,n$$

$$L(\widetilde u^j)=\sum_{k=1}^{m}b_{kj}\widetilde w^k,\quad j=1,\ldots,n$$

$$u^j=\sum_{\mu=1}^{n}p_{\mu j}\widetilde u^\mu,\quad j=1,\ldots,n$$

$$w^j=\sum_{\nu=1}^{m}q_{\nu j}\widetilde w^\nu,\quad j=1,\ldots,m.$$

Then, we have

$$L(u^j)=L\left(\sum_{\mu=1}^{n}p_{\mu j}\widetilde u^\mu\right)=\sum_{\mu=1}^{n}p_{\mu j}L(\widetilde u^\mu)=\sum_{\mu=1}^{n}\sum_{k=1}^{m}p_{\mu j}b_{k\mu}\widetilde w^k$$

and

$$L(u^j)=\sum_{i=1}^{m}a_{ij}w^i=\sum_{i=1}^{m}a_{ij}\left(\sum_{\nu=1}^{m}q_{\nu i}\widetilde w^\nu\right)=\sum_{i=1}^{m}\sum_{\nu=1}^{m}a_{ij}q_{\nu i}\widetilde w^\nu.$$