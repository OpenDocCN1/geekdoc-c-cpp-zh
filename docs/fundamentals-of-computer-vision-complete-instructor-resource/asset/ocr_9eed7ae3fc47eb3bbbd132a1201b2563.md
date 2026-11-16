![](bbox=[0.15, 0.1, 0.85, 0.29])

Figure 12.4 Two cameras viewing the same object. Neither camera is rotated. Viewed with the positive Y axis into the paper.

vector that describes the origin in the coordinates of the camera, (not the camera in terms of the origin) – e₂, forming a 3 x 4 matrix denoted by M.

$M = R[I | -\mathbf{e}_2]$.

$M$ contains information about the position and orientation of Camera 2. Its elements are called the extrinsic parameters of the camera.

+   2. Finally, the projection matrix is constructed by premultiplying by the matrix of intrinsic parameters.

$P_{3 \times 4} = K_{3 \times 3} M_{3 \times 4}$ (12.11)

where the matrix dimensions are shown for clarity.

Now any point in the view of the camera X projects to a point on the camera focal plane x obeying (writing Eq. 12.5 again):

$\mathbf{x} = P\mathbf{X}$ (12.12)

# Example with no Rotation

In Figure 12.4 two cameras view the same object, both of which have the same focal length, 10, and no other internal distortions. Thus for both cameras, the intrinsic matrix is

$K = \begin{bmatrix} 10 & 0 & 0 \\ 0 & 10 & 0 \\ 0 & 0 & 1 \end{bmatrix}$.

Suppose camera 1 is at the origin ($\mathbf{e}_1 = \mathbf{0}$), and pointed along the Z axis of the global coordinate system. Then its projection matrix is

$P_1 = K \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{bmatrix} = \begin{bmatrix} 10 & 0 & 0 & 0 \\ 0 & 10 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{bmatrix}$.