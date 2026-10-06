# Research on Scene 3D Reconstruction ■ 269

Clearly this equation is unaffected by multiplication by a nonzero-scale factor and the homogeneous representation of the plane is the four-vector $\mathfrak{p} = (\mathfrak{p}_1, \mathfrak{p}_2, \mathfrak{p}_3, \mathfrak{p}_4)^	op$

Also we may have $\mathfrak{p}^	op X=0$, which expresses that the point $X$ is on the plane $p$. It is easy to find that the first three components of the plane cor respond to the normal plane of Euclidean geometry. This formula also be written as

```
$(\mathfrak{p}_1, \mathfrak{p}_2, \mathfrak{p}_3)^	op(x_1, x_2, x_3)^	op+d=0 \quad (11.3)$
```

where:
d=\pi_4$

# 11.2.3.2 Camera Model

A camera is a mapping between the 3D world (object space) and the 3D image. The principal plane of interest here is central projection.

11.2.3.2.1 The Basic Pinhole Model We consider the central projection of points onto a plane. The center of projection is the origin of a Euclidean coordinate system, and consider the plane $Z=f$, which is called the image plane or focal plane. In this model, a point $X=(X, Y, Z)^	op$ is mapped to the point on the image plane where a line joining the point $X$ to the center of projection meets the image plane. Ignoring the final image coordinate, we use that $(X, Y, Z)^	op (fX/z, fY/z, fZ/z)^	op$. This is a mapping from Euclidean three-space to two-space. The mapping can be represented by homogeneous vectors as

$$\begin{array}{ccccccc} \mathfrak{E} & & & & & \mathfrak{E} & \ \mathfrak{A}_x & \mathfrak{E}x & \mathfrak{E}f & & & & \ \mathfrak{A}_y & \mathfrak{E}y & & f & & & (11.4) \ & \mathfrak{A}_z & & \mathfrak{I} & & & \ & & \mathfrak{A}_z & & & & & \ & & \mathfrak{A}_1 & & 1 & & & \end{array}$}$

Or more briefly, $m=K\mathbf{0}X$, where $m=(x,y)^	op$ and $K=\text{diag}(f,f)$.\Because in Reference 1, the author believes that all the principal points are in the center of image plane, there is no need to find the principal point.

# 11.2.3.2.2 Camera Rotation and Translation

In general, points will be expressed in terms of a different Euclidean coordinate frame, known as