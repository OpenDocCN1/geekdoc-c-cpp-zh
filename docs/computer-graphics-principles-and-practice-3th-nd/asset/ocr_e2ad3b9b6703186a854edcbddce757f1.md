directly use the 2D barycentric coordinates from the coverage test for shading. That is because the 3D barycentric coordinates of a point on the triangle and the 2D barycentric coordinates of the projection of that point within the projection of the triangle are generally not equal. This can be seen in Figure 15.13. The figure shows a square in 3D with vertices A, B, C, and D, viewed from an oblique perspective so that its 2D projection is a trapezoid. The centroid of the 3D square is point E, which lies at the intersection of the diagonals. Point E is halfway between 3D edges AB and CD, yet in the 2D projection it is clearly much closer to edge CD. In terms of triangles, for triangle ABC, the 3D barycentric coordinates of E must be \(w_A=\frac{1}{2}, w_B=0, w_C=\frac{1}{2}\). The projection of E is clearly not halfway along the 2D line segment between the projections of A and C. (We saw this phenomenon in Chapter 10 as well.)

![](bbox=[0.709, 0.122, 0.928, 0.209])

*Figure 15.13: E is the centroid of square ABCD in 3D, but its projection is not the centroid of the projection of the square. This can be seen from the fact that the three dashed lines are not evenly spaced in 2D.*

Fortunately, there is an efficient analog to 2D linear interpolation for projected 3D linear interpolation. This is interchangeably called **hyperbolic interpolation** [Bli93], **perspective-correct interpolation** [OG97], and **rational linear interpolation** [Hec90].

The perspective-correct interpolation method is simple. We can express it intuitively as, for each scalar vertex attribute \(u\), linearly interpolate both \(u'=u/z\) and \(1/z\) in screen space. At each pixel, recover the 3D linearly interpolated attribute value from these by \(u=u'/(1/z)\). See the following sidebar for a more formal explanation of why this works.

> Let \(u(x,y,z)\) be some scalar attribute (e.g., albedo, a texture coordinate) that varies linearly over the polygon. Two equivalent definitions may be more intuitive: (a) \(u\) is defined at vertices by specific values and varies by barycentric interpolation between them; (b) \(u\) has the form of a 3D plane equation, \(u(x,y,z)=ax+by+cz+d\).
> 
> When the polygon is projected into screen space by the transformation \((x,y,z)\to(-x/z,-y/z,-1)\) for an image plane at \(z=-1\), then the function \(-u(x,y,z)/z\) varies linearly in screen space. Instead of linear interpolation in screen space, we need to perform a kind of “hyperbolic interpolation” to correctly evaluate \(u\) as follows.
> 
> Let \(P\) and \(Q\) be points on the 3D polygon, and let \(u(P)\) and \(u(Q)\) be some function that varies linearly across the plane of the 3D polygon evaluated at those points. Let \(P'=-P/z_P\) be the projection of \(P\) and \(Q'=-Q/z_Q\) be the projection of \(Q\). At point \(M\) on line \(PQ\) that projects to \(M'=\alpha P'+(1-\alpha)Q'\), the value of \(u(M)\) satisfies
> 
> \[
> \frac{u(M)}{-z_M}=\alpha\frac{u(P)}{-z_P}+(1-\alpha)\frac{u(Q)}{-z_Q}, \tag{15.5}
> \]
> 
> while \(-1/z_M\) satisfies
> 
> \[
> \frac{1}{-z_M}=\alpha\frac{1}{-z_P}+(1-\alpha)\frac{1}{-z_Q}. \tag{15.6}
> \]
> 
> Solving for \(u(M)\) yields
> 
> \[
> u(M)=\frac{\alpha\frac{u(P)}{-z_P}+(1-\alpha)\frac{u(Q)}{-z_Q}}{\alpha\frac{1}{-z_P}+(1-\alpha)\frac{1}{-z_Q}}. \tag{15.7}
> \]