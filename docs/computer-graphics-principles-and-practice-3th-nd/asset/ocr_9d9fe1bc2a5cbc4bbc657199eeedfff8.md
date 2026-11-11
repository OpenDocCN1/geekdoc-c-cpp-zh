These two concerns, it turns out, are identical! If **d · n** = 0, then the ray is parallel to the plane; that means it’s either contained in the plane (in which case there are infinitely many intersections) or disjoint from the plane, in which case there are none. In the first case, both the numerator and denominator are zero; in the second, only the denominator is.

**Inline Exercise 7.12:** What happens if we solve for *t* and find that it’s negative? That can happen if either the numerator or denominator is negative, and the other is positive. Describe each of these situations geometrically, as in “In the first case, **P** is on the positive side of the plane (i.e., the half-space into which **n** points), and . . .”

Let’s carry out the computation again, in this case with a plane specified by a point **Q** that lies in the plane, and two vectors, **u** and **v**, that lie in the plane and are linearly independent. Now, points in the plane can be written in the form

$$Q + \alpha u + \beta v \tag{7.96}$$

for some real numbers α and β. This version of the problem seems distinctly more difficult, in the sense that a solution will give us *t*, α, and β; that impression is partially correct, as we’ll see.

We want to find a value *t* ≥ 0 with the property that

$$P + td = Q + \alpha u + \beta v \tag{7.97}$$

for some values α and β. The first algebraic steps are similar. Move the points around so that a difference of points appears, and we’ll be working only with vectors:

$$\begin{aligned}
P + td &= Q + \alpha u + \beta v &&\tag{7.98}\\
P - Q + td &= \alpha u + \beta v &&\tag{7.99}\\
P - Q &= \alpha u + \beta v - td. &&\tag{7.100}
\end{aligned}$$

Letting **h** = **P** − **Q**, we can see that now the problem is “Express the vector **h** as a linear combination of **u**, **v**, and **d**.” We could let **M** be the matrix whose columns are these three vectors, and the solution becomes

$$[\alpha\quad\beta\quad -t] = M^{-1}(P - Q). \tag{7.101}$$

To implement this, we’d need to invert a 3 × 3 matrix, which is not difficult, but masks some of the essential features of the problem. First, it’s possible that **M** is not invertible, but even if this happens, there may be a solution to

$$M\,[\alpha\quad\beta\quad -t] = (P - Q). \tag{7.102}$$

(**M** is noninvertible when the ray is parallel to the plane; the solution exists when the ray lies in the plane, and indeed, in this case there are infinitely many solutions.) Second, the inversion must be redone for each new ray we want to intersect with the plane; that makes ray-plane intersection computationally intensive, which is bad.