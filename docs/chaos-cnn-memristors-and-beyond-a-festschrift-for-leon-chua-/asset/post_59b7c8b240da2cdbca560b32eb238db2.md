
![](img/039e7d3c23390584a66737067db8b75b_253_0.png)

Fig. 1. Some Julia sets for \(z^4+\lambda/z^4\): if \(\lambda=0.04\), \(J(F_\lambda)\) is a Cantor set; if \(\lambda=0.23\), \(J(F_\lambda)\) is a Cantor set of circles; and if \(\lambda=-0.125i\), \(J(F_\lambda)\) is a Sierpiński curve.

interior component. Hence there would be no interior boundary of the Herman ring in the Julia set and the Fatou component would be the entire disk, not an annulus.

So let \(R\) be a Herman ring that surrounds the origin. We have that the Julia set of \(F_\lambda\) is symmetric under rotation by \(2\pi/2n\), i.e., it has \(2n\)-fold symmetry. This follows from the fact that \(F_\lambda(e^{\pi i/n})=-F_\lambda(z)\) and, as we observed above, the orbits of \(\pm z\) are either symmetric under \(z\mapsto -z\) (when \(n\) is odd) or \(F_\lambda(z)=F_\lambda(-z)\) when \(n\) is even.

So assume that we have a Herman ring \(R\) surrounding the origin. Then \(R\) must be symmetric

under the rotation \(z\mapsto e^{\pi i/n}z\). But then, by the above, the map cannot be one-to-one on \(R\), so we have no such Herman ring. This eliminates the first possibility of a non-simply connected component in the Fatou set.

Now suppose that the map has a multiply connected attracting or parabolic basin. Then it is well known [8] that this domain must in fact be infinitely connected. As above, at least one iterate of this domain must surround the origin. To show that this cannot happen when \(\lambda\) is in the connectedness locus, we shall construct Cantor necklaces in the dynamical plane. The boundaries of these necklaces

![](img/039e7d3c23390584a66737067db8b75b_254_0.png)

Fig. 2. The parameter plane when n = 4.

will be closed sets that connect the boundary of B_λ to the boundary of T_λ and lie in the Julia set. This will show that there is no such infinitely connected Fatou component surrounding the origin. For simplicity, we shall concentrate on the case n = 2; the cases where n > 2 are handled in a similar manner; we will discuss the minor modifications for these cases at the end of this section. To define the Cantor necklace, we let Γ denote the Cantor middle-thirds set in the unit interval [0, 1]. We regard this interval as a subset of the real axis in the plane. For each open interval of length 1/3^n removed from the unit interval in the construction of Γ, we replace this interval by an open disk of diameter 1/3^n centered at the midpoint of the removed interval. Thus the boundary of this open disk meets the Cantor set at the two endpoints of the removed interval. We call the resulting set the Cantor middle-thirds necklace. See Fig. 3. Any set homeomorphic to the Cantor middle-thirds necklace is called a Cantor necklace. We do not include the boundary of the open disks in the Cantor necklace for the following technical reason: it is sometimes difficult in practice to verify that these bounding curves are simple closed curves.

![](img/039e7d3c23390584a66737067db8b75b_254_1.png)

Fig. 3. The Cantor middle-thirds necklace.

Now let λ = |λ| e^{iη}. For the rest of this paper, we will consider only the case where 0 < η < 2π. When λ is positive and real, it is known that F_λ is conjugate in the right half plane to a polynomial of the form z^2 + c where c ∈ ℝ^+. See [4]. The boundary of this quadratic like Julia set then lies in the Julia set of F_λ and stretches from B_λ to T_λ and so no Fatou domain can surround the origin in this case. We remark that all of the results below concerning Cantor necklaces also hold when η = 0, but the arguments are slightly different. When |λ| < 1, we have the following estimate of the size of B_λ.

## Lemma. (The Escape Criterion). Suppose |λ| < 1 and |z| ≥ 2. Then z ∈ B_λ, so the Julia set is contained in the open disk |z| < 2.

## Proof. If |z| ≥ 2, then we have |F_λ(z)| ≥ |z|^2 - |λ|/|z|^2 ≥ 2|z| - 1/4 > 3/2 |z|.

Inductively, we find |F_λ^n(z)| ≥ (3/2)^n |z|.

Therefore the orbit of any such z tends to ∞ so all points on or outside the circle of radius 2 lie in B_λ.

As mentioned above, it is known that the Julia set is a Cantor set if |λ| ≥ 1, so we also exclude this case for the remainder of this paper. Therefore we assume throughout that λ = |λ| e^{iη} with 0 < η < 2π and |λ| < 1. Recall that the critical points of F_λ are given by λ^{1/4}. Therefore one of the critical points of F_λ lies on the straight line through the origin given by t exp(iη/4) with t > 0. The image of this line lies along the straight line with argument θ = η/2, and F_λ maps the line t exp(iη/4) with t > 0 in two-to-one fashion over the portion of this image straight line that extends from the critical value 2√λ whose argument is η/2 out to ∞. Note that the image of this line is disjoint from the line itself since we have assumed that 0 < η < 2π. There is a second critical point of F_λ lying on the line with argument θ = η/4 - π/2, and this line is mapped in two-to-one fashion to the opposite line θ = -η/2 exactly as in the above case. Let H_λ be the involution λ^{1/2}/z. Then we have F_λ(H_λ(z)) = F_λ(z) so the Julia set of F_λ is

![](img/039e7d3c23390584a66737067db8b75b_255_0.png)

symmetric under $H_\lambda$. Note that $H_\lambda$ interchanges $B_\lambda$ and $T_\lambda$. By the escape criterion, we know that any point on or outside $r=2$ is mapped closer to $\infty$. Let $\beta_\lambda$ denote the image of this circle, so that $\beta_\lambda\subset B_\lambda$. Using the involution $H_\lambda$, there is a second circle, namely $r=|\lambda|^{1/2}/2$, that is also mapped two-to-one onto $\beta_\lambda$.

Consider the open region $R_\lambda$ bounded by the rays $\theta=\eta/4$ and $\theta=\eta/4-\pi/2$ and the two circular preimages of $\beta_\lambda$. The set $R_\lambda$ is a quarter of an annulus. Let $L_\lambda=-R_\lambda$. We call $R_\lambda$ (resp., $L_\lambda$) the right (resp., left) fundamental sector. These fundamental sectors are a pair of disjoint, open, simply connected regions in $\mathbb C$. Note that, for each $\lambda$, $R_\lambda$ lies in the right half plane $\operatorname{Re}z>0$, while $L_\lambda$ lies in the left half plane. See Fig. 4.

## **Proposition.**

$F_\lambda$ maps each of the fundamental sectors in one-to-one fashion onto the open set $\mathcal O$ bounded by $\beta_\lambda$ minus the portions of the two straight lines $\theta=\pm\eta/2$ extending from the critical values $\pm v_\lambda$ to $\beta_\lambda$. So the image of each of these fundamental sectors contains the closures of both $R_\lambda$ and $L_\lambda$ in its interior.

## **Proof.**

The images of the straight rays bounding $R_\lambda$ and $L_\lambda$ are contained in the rays $\theta=\pm\eta/2$, both of which lie outside these sectors. The image of the outer circular boundary of each fundamental sector is exactly one-half of $\beta_\lambda$, while the inner boundary of each sector is mapped to the opposite half of $\beta_\lambda$. Hence each fundamental sector is mapped onto the open disk bounded by $\beta_\lambda$ minus the two portions of the rays $\theta=\pm\eta/2$ lying beyond the critical values. This set is $\mathcal O$. By fourfold symmetry, this map must be one-to-one on each fundamental sector.

Since $F_\lambda$ maps the union of the fundamental sectors strictly over itself, most points in $R_\lambda\cup L_\lambda$ have orbits that leave this set after iteration. Let $\Gamma_\lambda$ be the set of points whose orbits remain for all iterations in $R_\lambda\cup L_\lambda$. Then we have:

## **Proposition.**

The set $\Gamma_\lambda$ is a Cantor set and $F_\lambda|\Gamma_\lambda$ is conjugate to the one-sided shift on two symbols.

## **Proof.**

By the previous result, each of the fundamental sectors is mapped in one-to-one fashion onto the open region $\mathcal O$ that properly contains $R_\lambda\cup L_\lambda$ in $\mathbb C$. So we have a pair of well-defined inverses $G_0$ (resp., $G_1$) of $F_\lambda$ that map $\mathcal O$ into $R_\lambda$ (resp., $L_\lambda$). Standard arguments then show that these inverses are contractions in the Poincaré metric on $\mathcal O$. Then, for any one-sided sequence $(s_0s_1s_2\ldots)$ of 0’s and 1’s, the set

```
$$\bigcap_{j=0}^{\infty}G_{s_0}\circ\cdots\circ G_{s_j}(\mathcal O)$$
```

is a unique point and the map that takes the sequence $(s_0s_1s_2\ldots)$ to this point defines a homeomorphism between the space of one-sided sequences of 0’s and 1’s endowed with the usual topology and $\Gamma_\lambda$. Hence $\Gamma_\lambda$ is a Cantor set and we have that $F_\lambda|\Gamma_\lambda$ is conjugate to the one-sided shift on two symbols.

Now suppose, in addition, that the critical values do not lie in $B_\lambda$. So $B_\lambda$ is a simply connected open set. Our goal now is to construct a Cantor necklace in the dynamical plane. The Cantor set portion of the necklace will be the set $\Gamma_\lambda$ constructed above, whereas the open disks will be certain of the preimages of the basin of $\infty$ that lie in $R_\lambda$ and $L_\lambda$.

To construct the necklace, we have that $F_\lambda$ is conjugate to $z^2$ in $B_\lambda$. Hence there are a pair of external rays in $B_\lambda$ that correspond to the rays of angles 0 and $\pi$ in the basin of $\infty$ for $z^2$. It is known [10] that the external ray of angle 0 limits on the fixed point $p_\lambda$ that lies in $R_\lambda\cap\partial B_\lambda$, and the external ray of angle $1/2$ limits on its preimage $-p_\lambda$ in $L_\lambda$. Let $\pm q_\lambda$ be the preimages of $-p_\lambda$ in $L_\lambda$ and $R_\lambda$. Then there is a unique curve in $T_\lambda$ passing through 0 and connecting $q_\lambda$ to $-q_\lambda$ that
