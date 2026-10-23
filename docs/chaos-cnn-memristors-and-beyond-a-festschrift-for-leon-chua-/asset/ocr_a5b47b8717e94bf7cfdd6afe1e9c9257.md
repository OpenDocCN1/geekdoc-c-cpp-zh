subregions

```
$$P_0=\{(p,q):pq<1\},$$

$$P_{IT}=\bigcup_{m>2}P_m,$$

$$P_m=\left\{(p,q):\sum_{i=0}^{m-2}p^{-i}<q<p^{-m+1}\right\},$$

$$P_{ST}=P\setminus(\overline{P_0}\cup\overline{P_{IT}}),$$
```

each is open in $P$. The boundary between the sub-regions is advisable to represent in the form

```
$$G=\bigcup_{m\ge2}G_m^-\cup\bigcup_{m\ge3}G_m^+,$$

$$G_2^- =\{(p,q):pq=1\},$$

$$G_m^- =\{(p,q):q=p^{-m+1}\}\cap\overline{P_m},$$

$$G_m^+ =\left\{(p,q):\sum_{i=0}^{m-2}p^{-i}=q\right\}\cap\overline{P_m},\qquad m=3,4,\ldots$$
```

+   - Where $(p,q)\in P_0$, the map $g$ has an attracting cycle of period 2, that attracts all the points from $[0,1]$ except the (repelling) fixed point $z=q/(1+q)$.
+   - Where $(p,q)\in P_m^+$, $m>2$, the map $g$ has an attracting cycle of period $m$; this cycle attracts all the points from $[0,1]$ except the set $D(g)$ formed by the unstable points of $g$ (and including the repelling cycles and their preimages) and is a cantor set of positive Hausdorff dimension $(0<d_H D(g)<1)$. The basin of the attracting cycle consists of a countable number of open intervals (which are the preimages of the $m$ “main” intervals that contain this cycle).
+   - Where $(p,q)\in P_{ST}$, the map $g$ has no attracting cycles but it has a cycle of intervals $J_1,\ldots,J_s$, $s=s(p,q)$, that “takes up” almost all the points from $[0,1]$. In this case, $g$ is transitive on the set $J=\bigcup_{i=1}^sJ_i$ (i.e. almost each trajectories is dense on $J$) and has a smooth invariant measure concentrated on $J$ (in addition, $g^s$ is probabilistically intermixing on $J_k$, $k=1,\ldots,s$). When $(p,q)$ is in the vicinity of $G_m^-$, then $s=2m$. When $(p,q)$ is in the vicinity of $G_m^+$, then $s=1$ and, moreover, $J=[0,1]$; hence, the support of the smooth invariant measure consists of the unique interval $[0,1]$.

The boundary $G$ is the site of bifurcations of two types.

+   - At the boundary $G_m^-$, $m\ge2$, we observe a ‘soft’ doubling period bifurcation. The attracting cycle of period $m$, that exists when $(p,q)\in P_m$, transforms, when $(p,q)$ gets on $G_m^-$, into a “taking up” cycle of intervals $J_1,\ldots,J_m$ of exclusive structure: $g^m(z)|_{J_i}=-z$, $i=1,\ldots,m$; therewith the end-points of the intervals $J_1,\ldots,J_m$ are the preimages of the break-point $z=a$. Consequently, every interval $J_i$ is the union of two adjacent intervals which transform one into another under $g^m$. When $(p,q)$ moves away from $G_m^-$ and passes in $P_{ST}$, the adjacent intervals “move apart” and produce a cycle of intervals with period $2m$. It is just the way in which the ‘soft’ doubling period bifurcations happen for piecewise linear maps.
+   - At the boundary $G_m^+$, $m\ge3$, we deal with a ‘hard’ cycle birth bifurcation. Locally this cycle birth corresponds to a tangential bifurcation for smooth maps: the (repelling or semi-repelling) cycle of period $m$, produced during the transition of $(p,q)$ from $P_{ST}$ at $G_m^+$, splits into two cycles of period $m$, attracting and repelling, when $(p,q)$ moves away from $G_m^+$ and passes in $P_m$.

However, the case $(p,q)\in G_m^+$, $m\ge3$, is the first to give rise a cycle of period $m$, that has the so-called maximal type [2]: if $\gamma_1<\gamma_2<\cdots<\gamma_m$ are the points of the cycle, then $g(\gamma_i)=\gamma_{i+1}$, $i=1,2,\ldots,m-1$, and $g(\gamma_m)=\gamma_1$, which means

![](bbox=[0.529, 0.645, 0.903, 0.944])