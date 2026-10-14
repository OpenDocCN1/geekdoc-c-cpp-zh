Therefore, using the same technique as we used before, we can find the rotation matrix \mathcal{R} as

```
P' = \begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} = \begin{pmatrix} cos(\theta) & -sin(\theta) & 0 \\ sin(\theta) & cos(\theta) & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} x \\ y \\ 1 \end{pmatrix} = \mathcal{R}(\theta)P \tag{6.17}
```

Clearly, the inverse transformation of \mathcal{R} is a rotation by -\theta. Therefore,

```
\mathcal{R}(\theta)^{-1} = \mathcal{R}(-\theta) \tag{6.18}
```

Now plug in -\theta in \mathcal{R} and you will see that the matrix is a transpose of \mathcal{R}, i.e.

```
\mathcal{R}(\theta)^{-1} = \mathcal{R}(-\theta) = \mathcal{R}(\theta)^T \tag{6.19}
```

This property of inverse of rotation matrix being its transpose is a very special and useful one and is true for all rotation matrices, even in higher dimensions!

![](bbox=[0.16, 0.58, 0.38, 0.71])

Now, let us extend this concept to 3D. While a rotation about a plane occurs around a point, a 3D rotation occurs about an axis. Figure 6.4 shows a rotation about the z-axis. For a rotation about the z-axis, the z-coordinates of the points remain unchanged. The rotation still affects the x and y coordinates just the same way as it would in a 2D on the xy plane. Therefore the 3D rotation can be represented by the following equations.

Figure 6.4. This shows the 3D rotation of a point (x, y, z) about the z-axis resulting in the point (x', y', z).

```
x' = x cos(\theta) - y sin(\theta) \tag{6.20}
y' = x sin(\theta) + y cos(\theta) \tag{6.21}
z' = z \tag{6.22}
```

In 3D we distinguish the rotations with their axes. Therefore, the 3D rotation about z-axis, \mathcal{R}_z is given by

```
\mathcal{R}_z(\theta) = \begin{pmatrix} cos(\theta) & -sin(\theta) & 0 & 0 \\ sin(\theta) & cos(\theta) & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} \tag{6.23}
```

Also, in this case of 3D rotation,

```
\mathcal{R}_z(\theta)^{-1} = \mathcal{R}_z(-\theta) = \mathcal{R}_z(\theta)^T \tag{6.24}
```