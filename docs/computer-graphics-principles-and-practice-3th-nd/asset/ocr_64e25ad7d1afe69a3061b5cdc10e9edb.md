$\gamma(t)=\sum_{i=0}^{n} P_i b_3(t-i)$, where

$$b_3(t)=\begin{cases}\frac{1}{6}t^3 & 0\le t\le 1\\[2pt]\frac{1}{6}(-3(t-1)^3+3(t-1)^2+3(t-1)+1) & 1\le t\le 2\\[2pt]\frac{1}{6}(3(t-2)^3-6(t-2)^2+4) & 2\le t\le 3\\[2pt]\frac{1}{6}(-(t-3)^3+3(t-3)^2-3(t-3)+1) & 3\le t\le 4\\[2pt]0 & \text{otherwise.}\end{cases}$$

The domain of the curve $\gamma$ is $0<t<n-2$. Because of the structure of the function $b_3$, it turns out that for $j\le t\le j+1$, the point $\gamma(t)$ lies in the convex hull of the four points $P_j,\ldots,P_{j+3}$. This **convex hull property** is useful in computing the intersection of a ray with a B-spline: If the ray misses the convex hull of four sequential control points, it also must miss the corresponding segment of the B-spline curve. If the ray hits the convex hull, then further computation is needed. The web material for this chapter gives details.

Just like the Bézier and Hermite curves, a segment of a B-spline can be expressed in a matrix form, which can make evaluation more efficient. Recall that the form for the Bézier and Hermite curves was

$$\gamma(t)=\mathbf{G}\mathbf{M}\mathbf{T}(t),$$

where $\mathbf{T}(t)$ is the vector $[1\quad t\quad t^2\quad t^3]^T$ of powers of $t$. Because a B-spline curve is made of many segments, defined for $0\le t\le 1$, $1\le t\le 2$, etc., we’ll end up using $\mathbf{T}(t-j)$ for the $j$th segment, that is, a vector of powers of the fractional part of $t$.

For the $j$th segment, defined for $j\le t\le j+1$, and influenced by control points $P_j,\ldots,P_{j+3}$, we define a geometry matrix

$$\mathbf{G}_B=[P_j;P_{j+1};P_{j+2};P_{j+3}]$$

which is $2\times4$ for curves in the plane, or $3\times4$ for curves in space, and contains the coordinates of the control points as columns of the matrix. We multiply this by the **B-spline basis matrix**, $\mathbf{M}_{Bs}$:

$$\mathbf{M}_{Bs}=\frac{1}{6}\begin{bmatrix}0&0&0&1\\1&3&3&-3\\4&0&-6&3\\1&-3&3&-1\end{bmatrix}.$$

The uniform B-spline curve is then

$$\gamma(t)=\mathbf{G}_B\mathbf{M}_{Bs}\mathbf{T}(t-j),$$

where $j=\lfloor t\rfloor$ so that $t-j$ is the fractional part of $t$.

Although B-splines don’t pass through their control points, their extra degree of continuity makes them attractive in many applications. The tradeoff between controllability (does the curve interpolate its control points?) and continuity (how smooth is it?) is one that must be managed on a case-by-case basis in applications.