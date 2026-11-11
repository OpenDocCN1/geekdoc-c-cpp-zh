Because we’ll be homogenizing in a moment, we can multiply through by \(f-n\) and instead use the matrix

\[\mathbf{M}_{pp}=\begin{bmatrix} f-n&0&0&0\\0&f-n&0&0\\0&0&f&n\\0&0&-(f-n)&0\end{bmatrix}. \tag{13.16}\]

The derivation of this matrix is slightly messy and not particularly informative; we cover it in this chapter’s web materials. For now, all we need to do is verify that it does in fact transform the frustum between the near and far planes (\(z=c\) and \(z=-1\), respectively) in the standard perspective view volume to the standard parallel view volume. We’ll do so by looking at corners.

![](bbox=[0.705, 0.208, 0.936, 0.424])

The only interesting part of the unhinging matrix of Equation 13.15 is in the \(zw\)-plane, so it’s worth looking at that more closely, remembering that after this transformation, all points will be homogenized (i.e., projected radially from the origin onto the \(w=1\) line in the diagram). Figure 13.11 shows the slice of the view volume before transformation. The thick blue segment at the right on the \(w=1\) line represents the \(zw\)-slice of the view frustum between the near and far clipping planes. The thick red segment at the left is the part of the view cone between the near plane and the eye. The red point on the \(y\)-axis is the eye. The transformation tilts and stretches the \(w=1\) line (see Figure 13.12). Points at \(z=-1\) (the far clipping plane) remain fixed. The near clipping plane is transformed to lie on the \(z=0\) line. The eye is transformed onto the \(w=0\) line. After homogenization (see Figure 13.13), the front clipping plane remains at \(z=0\), while the eye is sent to “infinity on the \(z\)-axis,” causing the lines that used to meet at the eye to become parallel lines that “meet at infinity on the \(z\)-axis” (i.e., parallel lines that are parallel to the \(z\)-axis). These three constraints on the transformation are enough to uniquely determine the matrix (see Exercise 13.9).

![](bbox=[0.706, 0.455, 0.935, 0.616])

Consider the upper-right front corner of the frustum. It’s at the location \((-c,-c,c)\). (Recall that \(c=-n/f\) is negative, so \(-c\) is positive.) Under the transformation \(\mathbf{M}_{pp}\) it becomes

\[\begin{bmatrix} f-n&0&0&0\\0&f-n&0&0\\0&0&f&n\\0&0&-(f-n)&0\end{bmatrix}\begin{bmatrix}-c\\-c\\c\\1\end{bmatrix}=\begin{bmatrix}-c(f-n)\\-c(f-n)\\cf+n\\-(f-n)c\end{bmatrix}. \tag{13.17}\]

![](bbox=[0.706, 0.648, 0.933, 0.833])

Homogenizing, we get

\[\left[1\quad 1\quad\frac{cf+n}{-(f-n)c}\quad 1\right]^T=[1\quad 1\quad 0\quad 1]^T, \tag{13.18}\]

the upper-right front corner of the standard perspective view volume, as promised, where the last step depends on \(cf+n=-\frac{n}{f}f+n=0\).