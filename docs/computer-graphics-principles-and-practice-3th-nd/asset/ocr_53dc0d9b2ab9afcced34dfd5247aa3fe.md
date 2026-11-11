# 10.12.1 Transforming Parametric Lines

All the transformations of the $w = 1$ plane we’ve looked at share the property that they send lines into lines. But more than that is true: They send *parametric* lines to *parametric* lines, by which we mean that if $\ell$ is the parametric line $\ell = \{P + tv : t \in \mathbb{R}\}$, and $Q = P + v$ (i.e., $\ell$ starts at $P$ and reaches $Q$ at $t = 1$), and $T$ is the transformation $T(v) = Mv$, then $T(\ell)$ is the line

$$T(\ell) = \{T(P) + t(T(Q) - T(P)) : t \in \mathbb{R}\}, \qquad (10.115)$$

and in fact, the point at parameter $t$ in $\ell$ (namely $P + t(Q - P)$) is sent by $T$ to the point at parameter $t$ in $T(\ell)$ (namely $T(P) + t(T(Q) - T(P))$).

This means that for the transformations we’ve considered so far, transforming the plane commutes with forming affine or linear combinations, so you can either transform and then average a set of points, or average and then transform, for instance.

# 10.13 More General Transformations

Let’s look at one final transform, $T$, which is a prototype for transforms we’ll use when we study projections and cameras in 3D. All the essential ideas occur in 2D, so we’ll look at this transformation carefully. The matrix $M$ for the transformation $T$ is

$$M = \begin{bmatrix}2 & 0 & -1 \\ 0 & 1 & 0 \\ 1 & 0 & 0\end{bmatrix}. \qquad (10.116)$$

It’s easy to see that $T_M$ doesn’t transform the $w = 1$ plane into the $w = 1$ plane.

> **Inline Exercise 10.26.** Compute $T([2\ 0\ 1]^\mathsf{T})$ and verify that the result is not in the $w = 1$ plane.

Figure 10.22 shows the $w = 1$ plane in blue and the transformed $w = 1$ plane in gray. To make the transformation $T$ useful to us in our study of the $w = 1$ plane, we need to take the points of the gray plane and “return” them to the blue plane somehow. To do so, we introduce a new function, $H$, defined by

![](bbox=[0.696, 0.515, 0.916, 0.656])

*Figure 10.22:* The blue $w = 1$ plane transforms into the tilted gray plane under $T_M$.

$$H : \mathbb{R}^3 - \left\{\begin{bmatrix}x\\y\\0\end{bmatrix} : x,y \in \mathbb{R}\right\} \to \mathbb{R}^3, \qquad \begin{bmatrix}x\\y\\w\end{bmatrix} \mapsto [x/w, y/w, 1]. \qquad (10.117)$$

Figure 10.23 shows how the analogous function in two dimensions sends every point except those on the $w = 0$ line to the line $w = 1$: For a typical point $P$, we connect $P$ to the origin $O$ with a line and see where this line meets the $w = 1$ plane. Notice that even a point in the negative-$w$ half-space on the same line gets sent to the same location on the $w = 1$ line. This connect-and-intersect operation isn’t defined, of course, for points on the $x$-axis, because the line connecting them to the origin is the axis itself, which never meets the $w = 1$ line. $H$ is often called *homogenization* in graphics.

![](bbox=[0.707, 0.731, 0.925, 0.87])

*Figure 10.23:* Homogenization $\begin{bmatrix}x\\w\end{bmatrix} \mapsto \begin{bmatrix}x/w\\1\end{bmatrix}$ in two dimensions.