
### 3.3 Existence of a minimum

From now on we work with the enlarged space containing all circles, lines, and singletons. On this space we define a topology by the same rule (3.17), in which $\mathbb{S}_i$ and $\mathbb{S}$ may denote either circles or lines or singletons.

**Theorem 5** *Let* $\mathbb{B}$ *be a given bounding box containing all the data points. Then the* ‘enlarged’ *space of circles, lines, and singletons intersecting* $\mathbb{B}$ *is compact.*

*Proof.* Let $\{\mathbb{S}_i\}$ be a sequence of objects (circles, lines, singletons) that intersect $\mathbb{B}$. If there are infinitely many singletons in $\{\mathbb{S}_i\}$, then a subsequence of those converges to a point in $\mathbb{B}$ because the latter is compact. If there are infinitely many nonsingletons, then each of them is represented by a vector $(A_i, B_i, C_i, D_i)$ with $A_i \geq 0$. The sequence $\{A_i\}$ contains a subsequence that either converges to a limit $A < \infty$ or diverges to infinity. In the latter case we have a sequence of circles in $\mathbb{B}$ whose radii converge to zero, then they have a limit point in $\mathbb{B}$ just as singletons do, see above. If $A = 0$, then we have a sequence of arcs whose radii grow to infinity, and it contains a subsequence converging to a line because the space of lines crossing $\mathbb{B}$ is compact (Section 2.2). Lastly, if $0 < A < \infty$, then we have a sequence of circles crossing $\mathbb{B}$ whose radii converge to $R = 1/(2A)$. Then their centers must stay within distance $2R$ from the box $\mathbb{B}$, hence there is a subsequence of these circles whose centers converge to a limit point $(a,b)$. Therefore our subsequence converges to the circle $(a,b,R)$. The theorem is proved. $\square$

We remark that singletons need not really be involved, as they never provide the minimum of the objective function $\mathscr{F}$, unless all the data points collapse, but even in that case any line or circle through that collapsed data point would provide the best fit $\mathscr{F} = 0$ anyway.

Next, again as in Section 2.2 suppose a circle $\mathbb{S}$ (or a line $\mathbb{L}$) does not cross the box $\mathbb{B}$. Then it cannot provide a minimum of $\mathscr{F}$, as one can just move $\mathbb{S}$ (or $\mathbb{L}$) closer to the box and thus reduce all the distances from the data points to $\mathbb{S}$ (or $\mathbb{L}$). So we can restrict our search of the minimum of $\mathscr{F}$ to the space of circles and lines that intersect the bounding box $\mathbb{B}$. Since it is compact we obtain:

**Theorem 6** *The objective function* $\mathscr{F}$ *always attains its minimum, though it may be attained either on a circle or on a line.*

This resolves the existence issue in a satisfactory way.

### 3.4 Multivariate interpretation of circle fit

The conclusions of the previous section can be illustrated by a multidimensional geometric construction similar to the one described in Section 1.5.

**Megaspace**. Given $n$ data points $(x_1, y_1)$, $\dots$, $(x_n, y_n)$, we can represent them by one point (‘megapoint’) $\mathscr{X}$ in the $2n$-dimensional space $\mathbb{R}^{2n}$ with coordinates $x_1, y_1, \dots$, $x_n, y_n$. Recall that the orthogonal line fit corresponds to projecting the point $\mathscr{X}$ onto an $(n+2)$-dimensional quadratic surface (manifold) $\mathbb{P} \subset \mathbb{R}^{2n}$.

We now interpret the orthogonal circle fit in a similar manner. Consider the subset $\mathbb{Q} \subset \mathbb{R}^{2n}$ defined by

$$(x_1, y_1, \dots, x_n, y_n) \in \mathbb{Q} \iff \exists a, b, R: (x_i - a)^2 + (y_i - b)^2 = R^2 \ \forall i,$$

i.e., $\mathbb{Q}$ consists of all $(x_1, y_1, \dots, x_n, y_n) \in \mathbb{R}^{2n}$ such that the $n$ planar points $(x_1, y_1)$, $\dots$, $(x_n, y_n)$ lie on a circle (we call such points “co-circular,” which is perhaps an unconventional term).

**Projection in the megaspace.** Now the best fitting circle minimizes the sum

$$\sum_{i=1}^{n} (x_i - \bar{x}_i)^2 + (y_i - \bar{y}_i)^2.$$

where the points $(\bar{x}_1, \bar{y}_1)$, $\dots$, $(\bar{x}_n, \bar{y}_n)$ are constrained to lie on one circle. Therefore, the true values $\bar{x}_1, \bar{y}_1, \dots$, $\bar{x}_n, \bar{y}_n$ are represented by one megapoint (we denote it by $\overline{\mathscr{X}}$) in $\mathbb{Q}$. The orthogonal circle fitting procedure corresponds to choosing a megapoint $\overline{\mathscr{X}} \in \mathbb{Q}$ closest to the megapoint $\mathscr{X} \in \mathbb{R}^{2n}$ representing the data. In other words, we just need to project the point $\mathscr{X}$ onto $\mathbb{Q}$ orthogonally.

**Dimensionality of $\mathbb{Q}$.** It takes a little effort to verify that $\mathbb{Q}$ is specified by $n - 3$ independent relations

$$\det \begin{bmatrix} x_i - x_{i+1} & y_i - y_{i+1} & x_i^2 - x_{i+1}^2 + y_i^2 - y_{i+1}^2 \\ x_i - x_{i+2} & y_i - y_{i+2} & x_i^2 - x_{i+2}^2 + y_i^2 - y_{i+2}^2 \\ x_i - x_{i+3} & y_i - y_{i+3} & x_i^2 - x_{i+3}^2 + y_i^2 - y_{i+3}^2 \end{bmatrix} = 0 \hspace{2cm} (3.18)$$

for $i = 1, \dots, n - 3$, each of which means the co-circularity of the four planar points $(x_i, y_i)$, $(x_{i+1}, y_{i+1})$, $(x_{i+2}, y_{i+2})$, and $(x_{i+3}, y_{i+3})$. The relations (3.18) are polynomials of fourth degree, hence $\mathbb{Q}$ is an $(n+3)$-dimensional algebraic manifold in $\mathbb{R}^{2n}$ defined by *quartic* polynomial equations.

**Relation between $\mathbb{P}$ and $\mathbb{Q}$.** Note that the dimension of $\mathbb{Q}$ is one higher than that of $\mathbb{P}$, i.e., dim $\mathbb{Q} = $ dim $\mathbb{P} + 1$. A closer examination shows that $\mathbb{P}$ plays the role of the boundary of $\mathbb{Q}$, i.e., $\mathbb{Q}$ terminates on $\mathbb{P}$. Indeed, imagine $n$ co-circular points lying on a small arc of a very large circle. Now let us straighten (flatten) that arc as illustrated in Fig. 3.3, and move our $n$ points with the arc. These points are represented by one megapoint $\mathscr{X} \in \mathbb{Q}$, and when our arc is flattening, the point $\mathscr{X}$ is moving (sliding) on the surface $\mathbb{Q}$.

As the arc transforms into a straight line (the dashed line in Fig. 3.3), our moving point $\mathscr{X} \in \mathbb{Q}$ leaves the surface $\mathbb{Q}$ and instantaneously hits the manifold $\mathbb{P}$ representing all sets of $n$ collinear points. Thus $\mathbb{Q}$ borders on $\mathbb{P}$, or $\mathbb{P}$ serves as the boundary (frontier) of $\mathbb{Q}$.

![](img/86db288e3c266985d1648282179ae4b5_90_0.png)

Figure 3.4: A grey disk, $\mathbb{Q}$, is cut in half by a line, $\mathbb{P}$.

Moreover, in the above construction we can approach the limit straight line from each of its two sides. Only a one-sided approach is shown in Fig. 3.3, but we can reflect all of the arcs across the dashed line and get another sequence of arcs converging to the same line from the other side. That shows that there are two parts of the surface $\mathbb{Q}$ that terminate on $\mathbb{P}$; they approach $\mathbb{P}$ from the opposite directions.

A schematic illustration is shown in Fig. 3.4. The grey surface (disk) represents $\mathbb{Q}$: it is cut into two halves by a black line that represents $\mathbb{P}$. This picture shows how the surface $\mathbb{Q}$ borders on the line $\mathbb{P}$ approaching it from two sides.

**Geometric description of $\mathbb{P}$ and $\mathbb{Q}$.** With some degree of informality, one can say that $\mathbb{P}$ cuts right through $\mathbb{Q}$ and ‘divides’ it into two pieces. (This description is purely local, we do not mean to say that $\mathbb{Q}$, as a whole, consists of two pieces; in fact it is a connected manifold, as every circle can be continuously transformed into any other circle).

Actually, if one examines the equations (3.18) closely, it becomes clear that they describe not only all sets of $n$ co-circular points in the plane, but also all sets of $n$ collinear points. In other words, equations (3.18) describe both manifolds, $\mathbb{Q}$ and $\mathbb{P}$ (that is, their union $\mathbb{Q} \cup \mathbb{P}$). This is another way to convince yourself that lines must be naturally treated as particular types of circles (we can call lines, say, ‘degenerate circular arcs’).

Now it is easy to see why the best fitting circle may not exist (if lines are not treated as circles). Given a data point $\mathscr{X} \in \mathbb{R}^{2n}$ we need to project it orthogonally onto $\mathbb{Q}$. The projection is well defined unless the point $\mathscr{X}$ happens to be right above $\mathbb{P}$; then its projection of $\mathscr{X}$ onto $\mathbb{Q}$ falls exactly into the border of $\mathbb{Q}$, i.e., into $\mathbb{P}$.

### 3.5 (Non)uniqueness

After we have seen multiple lines fitted to a data set in Section 2.2 it may not be surprising to find out that there can be multiple fitted circles as well. However examples are much harder to construct; we review the ones from [43].
