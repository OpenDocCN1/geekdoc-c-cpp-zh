# The Projection Matrix

We spend some time now reviewing the function of the projection matrix and its relationship to the view frustum's clipping planes. We avoid examining any particular form of the projection matrix and require only that it be invertible. This allows our results to be applied to arbitrary projection matrices that may have already been modified from the standard forms.

Recall that in OpenGL camera space (also known as eye space), the camera lies at the origin and points in the -z direction, as shown in Figure 2.6.1. To complete a right-handed coordinate system, the x-axis points to the right, and the y-axis points upward. (In Direct3D, the z-axis is reversed and camera space is left-handed.) Vertices are normally transformed from whatever space in which they are specified into camera space by the model-view matrix. In this gem, we do not worry about the model-view matrix and assume that vertex positions are specified directly in camera space.

![](bbox=[0.25, 0.38, 0.76, 0.68])

FIGURE 2.6.1 OpenGL camera space and the standard view frustum. The near and far planes are perpendicular to the z-axis and lie at the distances n and f from the camera, respectively.

The standard view frustum is the six-sided truncated pyramid that encloses the volume of space visible to the camera. As shown in Figure 2.6.1, it is bounded by four side planes representing the four edges of the viewport, a near plane at z = -n, and a far plane at z = -f. The near and far planes are normally perpendicular to the camera's viewing direction, but our modifications to the projection matrix will move these two planes and change the fundamental shape of the view frustum.

The projection matrix transforms vertices from camera space to homogeneous clip space. In OpenGL's homogeneous clip space, a four-dimensional point (x, y, z, w)