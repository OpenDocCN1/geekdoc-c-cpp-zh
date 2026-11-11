
![](img/f464cd0043eb5336aa0543fe20a0561b_354_0.png)

*Figure 13.6: The uvw frame for a camera, the look and up vectors, and the points P, A, B, and C.*

In writing the equations, we’ll use **vup** and **look** to indicate the up vector and look direction, respectively; these shorter names make the equations more comprehensible. The point *P* is just a shorter name for the camera’s Position.

We’ll build the orthonormal basis, **u**, **v**, **w**, in reverse order. First, **w** is a unit vector pointing opposite the look direction, so

$$\mathbf{w}=-\frac{\text{look}}{\|\text{look}\|}=S(\text{look}). \tag{13.2}$$

To construct **v**, we first project **vup** onto the plane perpendicular to **w**, and hence perpendicular to the **look** direction as well, and then adjust its length:

$$\hat{\mathbf{v}}=\mathbf{vup}-(\mathbf{vup}\cdot\mathbf{w})\mathbf{w} \tag{13.3}$$
$$\mathbf{v}=\frac{\hat{\mathbf{v}}}{\|\hat{\mathbf{v}}\|}=S(\hat{\mathbf{v}}). \tag{13.4}$$

Finally, to create a right-handed coordinate system, we let

$$\mathbf{u}=\mathbf{v}\times\mathbf{w}. \tag{13.5}$$

- **Inline Exercise 13.1:** Some camera software (like Direct3D, but not OpenGL) starts by letting $\mathbf{w}=S(\text{look})$, without negation.
  - (a) Show that this makes no difference in the computation of **v**.
  - (b) Show that in this case, if we want **u**, **v** to retain the same orientation on the view plane (i.e., **u** pointing right, **v** pointing up), then the computation of **u** becomes $\mathbf{u}=\mathbf{w}\times\mathbf{v}$.
  - (c) Is the resultant *uvw*-coordinate system right- or left-handed?

Now we’ll compute the four points *P*, *A*, *B*, and *C*. The only subtlety concerns determining the length of edges *AB* and *AC*. The edge *AB* subtends half the horizontal field of view at *P*, and is at distance *f* from *P*, so

$$\tan\left(\frac{\theta_h}{2}\right)=\frac{AB}{f}, \quad\text{so} \tag{13.6}$$
$$AB=f\tan\left(\frac{\theta_h}{2}\right), \tag{13.7}$$

where $\theta_h$ denotes the horizontal field of view angle, converted to radians,

$$\theta_h=\text{FieldOfView}\frac{\pi}{180}. \tag{13.8}$$

and similar expressions determine θ_v, the vertical field of view, and the length of AC:

$$P = \text{Position} \tag{13.9}$$
$$A = P - f\mathbf{w} \tag{13.10}$$
$$B = A + f\tan\left(\frac{\theta_h}{2}\right)\mathbf{u} = P + f\tan\left(\frac{\theta_h}{2}\right)\mathbf{u} - f\mathbf{w} \tag{13.11}$$
$$C = A + f\tan\left(\frac{\theta_v}{2}\right)\mathbf{v} = P + f\tan\left(\frac{\theta_v}{2}\right)\mathbf{v} - f\mathbf{w}. \tag{13.12}$$

Notice that the near-plane distance n has not entered into our computations yet.

We now use the four points P, A, B, and C to transform the view frustum to the standard view frustum shown in Figure 13.7, and known as the standard perspective view volume.

All we need to do is say where the four points should be sent. We want to send P to the origin, A to the midpoint of the back face, which is (0, 0, −1), B to the mid-right edge of the back face, which is (1, 0, −1), and C to the mid-top edge, which is (0, 1, −1). The matrix that performs this transformation is denoted M_per (for “perspective”), so we’ll call the associated transformation T_PER. The code that creates our transformation is

```cpp
Transform3 Tper =
  Transform3.PointsToPoints(
    P, A, B, C,
    Point3(0, 0, 0), Point3(0, 0, -1), Point3(1, 0, -1), Point3(0, 1, -1));
```

Under this transformation, points of the far plane are transformed to the z = −1 plane. Since distances along the ray from P to A must transform linearly, points of the near plane are transformed to the plane z = −n/f. We’re nearly done at this point: We’ve transformed the view volume to a standard view volume, and from this point onward, almost everything we’ll do is independent of the camera parameters, the exception being that the ratio −n/f will enter into some of our computations.

![](img/f464cd0043eb5336aa0543fe20a0561b_355_0.png)

*Figure 13.7: The standard perspective view volume is the pyramid that ranges from −1 to 1 in x and y, and from 0 to −1 in z. The scale in z is exaggerated.*

This may appear too simple to you. Indeed, in an earlier edition of this book, the development of the transformation took several pages. But it’s an example of the power of proving one good theorem and writing the associated code.

The transformation can also be realized step-by-step. We can take the camera’s view volume and apply a sequence of transformations to it: translate it so that $P$ moves to the origin; rotate it several times around various coordinate axes so that the $uvw$-axes align with the $xyz$-axes; scale in $z$ so that the far plane ends up at $z=-1$ instead of $z=-f$; and scale in $x$ and $y$ to make the view frustum have a width and height of 2. Letting $P_x$, $P_y$, and $P_z$ denote the world coordinates of $P$, and similarly for $u$, $v$, and $w$, the matrix for the transformation is then

$$M_{per}=\text{scaling matrix}\;\text{rotation matrix}\;\text{translation matrix} \tag{13.13}$$

The rightmost matrix effects the translation; the middle one transforms $u$ to $e_1$, $v$ to $e_2$, and $w$ to $e_3$; the leftmost scales each axis appropriately. We present these merely for your interest and strongly advocate using the `PointsToPoints` method instead, as it’s far less prone to errors in order of matrix multiplication, in copying of coordinates, etc.

At this point, it’s easy to project points in the standard perspective view volume onto the back plane, for instance, using the nonlinear transformation $(x,y,z) \mapsto (x/z,y/z,1)$. This is more or less the process we followed when we rendered the cube in Chapter 3: Our $uvw$ basis was already aligned with the $xyz$-axes, and our center of projection was chosen to be the center of our coordinate system, so all we had to do was the projection step.

**Inline Exercise 13.2.** Review the rendering code in Chapter 3 to verify that it matches this description.

Rather than take that approach, however, we’re going to apply two transformations—the first to “open up” our pyramidal viewing volume into a rectangular angular parallelepiped, and the second to project along the $z$-axis. There are two reasons for this.

- When we discuss “parallel” cameras and projections rather than the perspective cameras we’ve seen so far, the parallelepipedal volume will be a more natural target than the pyramidal one.
- When we project along the $z$-axis, it’s especially easy to determine which objects obscure which other objects, that is, visibility testing becomes trivial. This property is essential in the design of the so-called $z$-buffer algorithm at the heart of most graphics hardware.

![](img/f464cd0043eb5336aa0543fe20a0561b_357_0.png)

*Figure 13.8: The standard parallel view volume.*

![](img/f464cd0043eb5336aa0543fe20a0561b_357_1.png)

*Figure 13.9: The unhinging transformation.*

Our **standard parallel view volume** (see Figure 13.8) is a parallelepiped that ranges from −1 to 1 in *x* and *y*, and from 0 to −1 in *z*. Its near clipping plane is *z* = 0; its far clipping plane is *z* = −1. (This differs from the parallel view volume used in either Direct3D or OpenGL, but only slightly.)

Now we’ll transform the portion of the standard perspective view volume between the transformed near and far planes (i.e., the portion between *z* = −*n*/*f* and *z* = −1) to the standard parallel view volume. The transformation we use will be a *projective* transformation in which all the rays passing from the view volume toward the origin are transformed into rays passing from the view volume toward the *xy*-plane in the positive-*z* direction (see Figure 13.9). This is sometimes called an **unhinging transformation**, because the planes defining opposite sides of the view frustum meet along a “*hinge line*,” which this transformation “*sends to infinity*.”

![](img/f464cd0043eb5336aa0543fe20a0561b_358_0.png)

*Figure 13.10: The standard perspective view at left (with a near clipping plane at \(z=-1/4\)) contains a small square, which is transformed into a parallelogram in the parallel view volume at right.*

Applying this transformation has no impact on the final results of our rendering because the perspective projection (i.e., \((x,y,z)\mapsto (x/z,y/z,1)\)) of a shape in the pre-transformed volume is the same as the parallel projection, \((x,y,z)\mapsto (x,y,1)\) of the transformed shape in the post-transformed volume. This is easy to see if we look at a two-dimensional slice of the situation, just the \(yz\)-plane. Consider, for instance, the small square shown in Figure 13.10 that occupies the middle half of a perspective view of the scene. **Occlusion** (which points are obscured by others) is determined by the ordering of points along rays from the viewpoint into the scene so that the point \(B\) is obscured by the near edge of the square. After transformation, that ray from the viewpoint into the scene becomes a ray in the \(-z\) direction; once again, the point \(B'\) is obscured by the front edge of the square. And once again, the transformed square ends up filling the middle half of the parallel view of the scene. The essential underlying fact is that light (the underlying agent of vision) travels in straight lines, and the transformation we’ll build converts straight lines to straight lines (and in particular, the projection rays from the perspective view to projection rays for the parallel view).

Recall from Section 11.1.1 that a *projective transformation* on \(\mathbb{R}^3\) can be written as a *linear transformation* on \(\mathbb{R}^4\) (the homogeneous-coordinate representation of points in 3-space), followed by the homogenizing transformation

\[H(x,y,z,w)=\left(\frac{x}{w},\frac{y}{w},\frac{z}{w},1\right).\tag{13.14}\]

Letting \(c=-\frac{n}{f}\) denote the \(z\)-coordinate of the front clipping plane after transformation to the standard perspective view volume (here at last the parameter \(n\) is being used!), we’ll simply write down the linear transformation from perspective to parallel, which we call \(M_{\mathrm{pp}}\):

\[M_{\mathrm{pp}}=\begin{bmatrix}1&0&0&0\\0&1&0&0\\0&0&\frac{1}{1+c}&-\frac{c}{1+c}\\0&0&-1&0\end{bmatrix}=\begin{bmatrix}1&0&0&0\\0&1&0&0\\0&0&\frac{f}{f-n}&\frac{n}{f-n}\\0&0&-1&0\end{bmatrix}.\tag{13.15}\]
