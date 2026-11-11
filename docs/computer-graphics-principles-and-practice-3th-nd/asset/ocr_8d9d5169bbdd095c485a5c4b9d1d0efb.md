$$
\begin{aligned}
&\begin{bmatrix}-1&0&0\\0&-1&0\\0&0&1\end{bmatrix}^{-1}
\begin{bmatrix}-1&0&0\\0&-1&0\\0&0&1\end{bmatrix}^{-1}
\begin{bmatrix}0.96&-0.26&0\\0.26&0.96&0\\0&0&1\end{bmatrix}\\
&\cdot\begin{bmatrix}-1&0&0\\0&-1&0\\0&0&1\end{bmatrix}
\begin{bmatrix}1.7&0&0\\0&0.7&0\\0&0&1\end{bmatrix}
\begin{bmatrix}0\\9\\1\end{bmatrix}.
\end{aligned}
\qquad (10.94)$$

We subtract from this the coordinates, (0,9), of the tip of the minute hand (in the minute-hand coordinate system) to get a vector from the tip of the minute hand to the tip of the hour hand.

As a final exercise, suppose we wanted to create an animation of the clock in which someone has grabbed the minute hand and held it so that the rest of the clock spins around the minute hand. How could we do this?

Well, the reason the minute hand moves from its initial 12:00 position on the `Canvas` (i.e., its position *after* it has been rotated 180° the first time) is that a sequence of further transformations has been applied to it. This sequence is rather short: It’s just the varying rotation. If we apply the *inverse* of this varying rotation to each of the clock elements, we’ll get the desired result. Because we apply both the rotation and its inverse to the minute hand, we could delete both, but the structure is more readable if we retain them. We could also apply the inverse rotation as part of the `Canvas`’s render transform.

> **Inline Exercise 10.23:** If we want to implement the second approach—inserting the inverse rotation in the `Canvas`’s render transform—should it appear (in the `WPF` code) before or after the scale-and-translate transforms that are already there? Try it!

# ## 10.12 Transforming Vectors and Covectors

We’ve agreed to say that the point (x, y) ∈ E² corresponds to the 3-space vector [x y 1]ᵀ, and that the vector [u v]ᵀ corresponds to the 3-space vector [u v 0]ᵀ. If we use a 3 × 3 matrix M (with last row [0 0 1]) to transform 3-space via

$$T : \mathbb{R}^3 \to \mathbb{R}^3 : \mathbf{x} \mapsto \mathbf{M}\mathbf{x}, \qquad (10.95)$$

then the restriction of T to the w = 1 plane has its image in E² as well, so we can write

$$(T|_{E^2}) : E^2 \to E^2 : \mathbf{x} \mapsto \mathbf{M}\mathbf{x}. \qquad (10.96)$$

But we also noted above that we could regard T as transforming **vectors**, or displacements of two-dimensional Euclidean space, which are typically written with two coordinates but which we represent in the form [u v 0]ᵀ. Because the last entry of such a “vector” is always 0, the last column of M has no effect on how vectors are transformed. Instead of computing