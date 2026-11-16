
When considering the affine points, we can assume $z = 1$ and so

$x^3 + x + 1 = y^2 + y$.
(13.9)

What are the affine points of degree 1 over $\mathbb{F}_2$ on the curve? Since $x$ and $y$ are in $\mathbb{F}_2$, we see that $y^2 + y = 0$ but $x + x + 1 = 1$. So the only point of degree 1 (that is, the only rational point) over $\mathbb{F}_2$ is the point at infinity. There are points of degree 2 over $\mathbb{F}_2$. Here $x$ and $y$ are in $\mathbb{F}_4$. If $y = 0$ or $1$, then $y^2 + y = 0$. By (13.9), $x^3 + x + 1 = 0$, which has no solution in $\mathbb{F}_4$. If $y = w$ or $\bar{w}$, then $y^2 + y = 1$ and so $x^3 + x = 0$ by (13.9). Thus the points of degree 2 over $\mathbb{F}_2$ on the curve are $P_1 = \{p_1, p'_1\}$, where $p_1 = (0 : w : 1)$ and $p'_1 = (0 : \bar{w} : 1)$, and $P_2 = \{p_2, p'_2\}$, where $p_2 = (1 : w : 1)$ and $p'_2 = (1 : \bar{w} : 1)$, noting that $\sigma_2$ switches the two projective points in each pair.

**Exercise 777** Let $f(x, y, z) = x^3 + xz^2 + z^3 + y^2z + yz^2 \in \mathbb{F}_2[x, y, z]$ determine an elliptic curve as in Example 13.3.3.
(a) Prove that $X_f(\mathbb{F})$ is nonsingular for any extension field $\mathbb{F}$ of $\mathbb{F}_2$.
(b) Find the four points of degree 3 on the curve over $\mathbb{F}_2$. The field $\mathbb{F}_8$ can be found in Example 3.4.3.
(c) Find the five points of degree 4 on the curve over $\mathbb{F}_2$. The field $\mathbb{F}_{16}$ can be found in Table 5.1. (Along the way you may rediscover the points of degree 2.)

**Exercise 778** This exercise uses the results of Exercise 773. Find the points on the Fermat curve defined by $x^3 + y^3 + z^3 = 0$ of degrees 1, 2, and 3 over $\mathbb{F}_2$.

**Exercise 779** This exercise uses the results of Exercise 774.
(a) There are eight affine points $(x : y : 1)$ of $\mathbb{P}^2(\mathbb{F}_8)$ on the Hermitian curve $\mathcal{H}_2(\mathbb{F}_8)$. Find the two affine points on this curve of degree 1 over $\mathbb{F}_2$ and the three affine points of degree 2 also over $\mathbb{F}_2$.
(b) There are 64 affine points $(x : y : 1)$ of $\mathbb{P}^2(\mathbb{F}_{16})$ on the Hermitian curve $\mathcal{H}_4(\mathbb{F}_{16})$. Find the two affine points on this curve of degree 1 over $\mathbb{F}_2$, the single affine point of degree 2 over $\mathbb{F}_2$, and the 15 affine points of degree 4 over $\mathbb{F}_2$.

**Exercise 780** This exercise uses the results of Exercise 775. Find the points on the Klein quartic defined by $x^3y + y^3z + z^3x = 0$ of degrees 1, 2, and 3 over $\mathbb{F}_2$.

When defining algebraic geometry codes, we will need to be able to compute the points on the intersection of two curves. In addition to the degree of a point of intersection, we need to know the *intersection multiplicity*, which we shorten to *multiplicity*, at the point of intersection. We do not formally define multiplicity because the definition is too technical. As the following example illustrates, we can compute multiplicity similarly to the way multiplicity of zeros is computed for polynomials in one variable.

### Example 13.3.4

In Example 13.3.3 and Exercise 777, we found some of the projective points from $\mathbb{P}^2(\mathbb{F}_q)$, where $q$ is a power of 2, on the elliptic curve determined by $x^3 + xz^2 + z^3 + y^2z + yz^2 = 0$. We now explore how this curve intersects other curves.

- Intersection with $x = 0$. We either have $z = 0$ or can assume that $z = 1$. In the former case we obtain the point at infinity $P_\infty = (0 : 1 : 0)$; in the latter, the equation $y^2 + y + 1 = 0$ must be satisfied leading to the two points $p_1 = (0 : w : 1)$ and $p'_1 = (0 : \bar{w} : 1)$ in $\mathbb{P}^2(\mathbb{F}_4)$.

We can view this in one of two ways. Over \(\mathbb{F}_4\) or extension fields of \(\mathbb{F}_4\), the curves \(x^3 + xz^2 + z^3 + y^2z + yz^2 = 0\) and \(x = 0\) intersect at the three points \(P_\infty\), \(p_1\), and \(p'_1\). Each of these points has degree 1, and the intersection multiplicity at each of these points is 1. Over \(\mathbb{F}_2\) or extension fields of \(\mathbb{F}_2\) not containing \(\mathbb{F}_4\), the points \(p_1\) and \(p'_1\) combine to form a point of degree 2, and so in this case we have two points of intersection: \(P_\infty\) and \(P_1 = \{p_1, p'_1\}\). The point \(P_\infty\) has degree 1 and \(P_1\) has degree 2. Of course, the intersection multiplicity at each of these points is still 1.

- Intersection with \(x^2 = 0\). We can view \(x^2 = 0\) as the union of the line \(x = 0\) with itself. Therefore every point on the elliptic curve and \(x^2 = 0\) occurs twice as frequently as it did on the single line \(x = 0\). Thus over \(\mathbb{F}_4\) or extension fields of \(\mathbb{F}_4\) there are three points of intersection, \(P_\infty\), \(p_1\), and \(p'_1\); each point continues to have degree 1 but now the intersection multiplicity at each point is 2. Similarly, over \(\mathbb{F}_2\) or extension fields not containing \(\mathbb{F}_4\), there are two points of intersection, \(P_\infty\) and \(P_1 = \{p_1, p'_1\}\). They have degree 1 and degree 2, respectively, and the intersection multiplicity at each point is now 2.

- Intersection with \(z = 0\). We saw from Example 13.3.3 that there was only one point \(P_\infty\) on the elliptic curve with \(z = 0\). This point has degree 1 over \(\mathbb{F}_2\) or any extension field of \(\mathbb{F}_2\). Plugging \(z = 0\) into the equation defining our elliptic curve, we obtain \(x^3 = 0\). Hence \(P_\infty\) occurs on the intersection with multiplicity 3.

- Intersection with \(z^2 = 0\). As in the case \(x^2 = 0\), we double the multiplicities obtained in the case \(z = 0\). Thus over any field of characteristic 2, the elliptic curve intersects the union of two lines each given by \(z = 0\) at \(P_\infty\). This point has degree 1 over \(\mathbb{F}_2\) or any extension field of \(\mathbb{F}_2\). The intersection multiplicity at \(P_\infty\) doubles and therefore is 6.

- Intersection with \(y = 0\). Here \(z = 0\) is not possible as then \(x\) would have to be 0. So \(z = 1\) and we must have $x^3 + x + 1 = 0$. The only solutions occur in $\mathbb{F}_8$ and lead to the points $p_3 = (\alpha : 0 : 1)$, $p'_3 = (\alpha^2 : 0 : 1)$, and $p''_3 = (\alpha^4 : 0 : 1)$ in $\mathbb{P}^2(\mathbb{F}_8)$. (Compare this to your answer in Exercise 777(b).) Thus over $\mathbb{F}_8$ or extension fields of $\mathbb{F}_8$ there are three points of intersection, $p_3$, $p'_3$, and $p''_3$; each has degree 1. The intersection multiplicity at each point is 1. Over $\mathbb{F}_2$ or extension fields not containing $\mathbb{F}_8$, the three points combine into a single point of intersection $P_3 = \{p_3, p'_3, p''_3\}$ of degree 3. Its intersection multiplicity remains 1.

## Exercise 781

As in Example 13.3.4, find the intersection of the elliptic curve \(x^3 + xz^2 + z^3 + y^2z + yz^2 = 0\) with the curves given below over \(\mathbb{F}_2\) and its extension fields. In addition give the degree of each point and the intersection multiplicity at each point of intersection.

- (a) \(x + z = 0\).
- (b) \(x^2 + z^2 = 0\). Hint: \(x^2 + z^2 = (x + z)^2\).
- (c) \(y^2 = 0\).
- (d) \(xz = 0\). Hint: This is the union of two lines \(x = 0\) and \(z = 0\).
- (e) \(yz = 0\).
- (f) \(xy = 0\).
- (g) \(z^2 + y^2 + yz = 0\).

Example 13.3.4 illustrates a certain uniformity in the number of points of intersection if counted properly. To count “properly” one must consider both multiplicity and degree; namely, an intersection of multiplicity \(m\) at a point of degree \(d\) counts \(md\) times. The total count of the points of intersection is computed by adding the products of all the multiplicities and degrees. From Example 13.3.4, the elliptic curve intersects $x = 0$ either in three points of degree 1 each with multiplicity 1, giving a total count of $1 \cdot 1 + 1 \cdot 1 + 1 \cdot 1 = 3$ points of intersection, or in one point of degree 1 intersecting with multiplicity 1 and one point of degree 2 intersecting with multiplicity 1, giving a total count of $1 \cdot 1 + 1 \cdot 2 = 3$ points of intersection. We also found that the elliptic curve intersects $x^2 = 0$ either in three points of degree 1 with intersection multiplicity 2, giving a total count of $2 \cdot 1 + 2 \cdot 1 + 2 \cdot 1 = 6$ points of intersection, or in one point of degree 1 with multiplicity 2 and one point of degree 2 also with multiplicity 2, giving a total count of $2 \cdot 1 + 2 \cdot 2 = 6$ points of intersection. Notice that these counts, 3 and 6, equal the product of the degree 3 of the homogeneous polynomial defining the elliptic curve and the degree, 1 or 2, of the homogeneous polynomial defining the curve intersecting the elliptic curve. This illustrates the following theorem due to Bézout.

## Theorem 13.3.5 (Bézout)

Let $f(x, y, z)$ and $g(x, y, z)$ be homogeneous polynomials over $\mathbb{F}$ of degrees $d_f$ and $d_g$, respectively. Suppose that $f$ and $g$ have no common nonconstant polynomial factors. Then $X_f$ and $X_g$ intersect in $d_f d_g$ points when counted with multiplicity and degree.

## Exercise 782

Verify that Bézout's Theorem agrees with the results of Exercise 781. ♦

This discussion naturally leads to the concept of a divisor on a curve. Let $X$ be a curve over the field $\mathbb{F}$. A divisor $D$ on $X$ over $\mathbb{F}$ is a formal sum $D = \sum n_P P$, where $n_P$ is an integer and $P$ is a point of arbitrary degree on $X$, with only a finite number of the $n_P$ being nonzero. The divisor is effective if $n_P \geq 0$ for all $P$. The support $\operatorname{supp}(D)$ of the divisor $D = \sum n_P P$ is $\{P \mid n_P \neq 0\}$. The degree of the divisor $D = \sum n_P P$ is $\deg(D) = \sum n_P \deg(P)$.

### Example 13.3.6

In Example 13.3.3 we found the points of degrees 1 and 2 over $\mathbb{F}_2$ on the elliptic curve $x^3 + xz^2 + z^3 = y^2z + yz^2 = 0$. So one divisor on that curve over $\mathbb{F}_2$ is $D_1 = 7P_\infty + 4P_1 - 9P_2$; this is not effective. The divisor $D_2 = 7P_\infty + 4P_1 + 9P_2$ is an effective divisor. Both $D_1$ and $D_2$ have support $\{P_\infty, P_1, P_2\}$. Also $\deg(D_1) = 7 \cdot 1 + 4 \cdot 2 - 9 \cdot 2 = -3$ and $\deg(D_2) = 7 \cdot 1 + 4 \cdot 2 + 9 \cdot 2 = 33$. Note that $7P_\infty + 4P_1 - 9P_2$ is not a divisor over $\mathbb{F}_2$ because the points in $P_1$ and $P_2$ are not defined over $\mathbb{F}_2$; we are required to list the entire pair $P_1$ and $P_2$ in a divisor over $\mathbb{F}_2$. However, $7P_\infty + 4p_1 - 9p'_2$ is a divisor over $\mathbb{F}_4$ with support $\{P_\infty, p_1, p'_2\}$ and degree $7 \cdot 1 + 4 \cdot 1 - 9 \cdot 1 = 2$. ■

We can use the notation of divisors to describe the intersection of two curves easily. If $X_1$ and $X_2$ are projective curves, then the intersection divisor over $\mathbb{F}$ of $X_1$ and $X_2$, denoted $X_1 \cap X_2$, is $\sum n_P P$, where the summation runs over all points over $\mathbb{F}$ on both $X_1$ and $X_2$ and $n_P$ is the multiplicity of the point on the two curves. If these curves are defined by homogeneous polynomials, with no common nonconstant polynomial factors, of degrees $d_f$ and $d_g$, then the intersection divisor has degree $d_f d_g$ by Bézout's Theorem.
