From Equations (3.25-3.27), we can easily obtain that

```
\frac{\partial^2 f}{\partial s^2}(x_0) = \mathbf{s}^T H \mathbf{s}.
```

This gives the curvature of our surface at some point $x_0$ in any given direction $\mathbf{s}$. This value is identical to the curvature of the curve $\mathcal{C}$ determined by the intersection of the surface with a plane that contains the vectors $\mathbf{n}$ and $\mathbf{s}$ (see Figure (3.28)) and is also known as _normal curvature_. However, to use Equation (3.28), we have to build our local coordinate system every time we want to compute the curvature of some point.

We can simplify this procedure as follows. Consider that our surface $\mathcal{S}$ is given in global coordinates instead of local ones, for example as an implicit function $f(x, y, z) = 0$. We can then, after some mathematical manipulations, express the rate of change of the surface normal at the point $x_0$ as

```
\frac{\partial^2 f}{\partial s^2}(x_0) = \frac{\mathbf{s}^T H \mathbf{s}}{\|\nabla f(x_0)\|}
```

where $H$ is the $3 \times 3$ Hessian matrix of partial derivatives of $f(x, y, z)$ in the _global_ coordinate system:

```
H = \left( \begin{array}{ccc} \frac{\partial^2 f}{\partial x^2} & \frac{\partial^2 f}{\partial x \partial y} & \frac{\partial^2 f}{\partial x \partial z} \\ \frac{\partial^2 f}{\partial y \partial x} & \frac{\partial^2 f}{\partial y^2} & \frac{\partial^2 f}{\partial y \partial z} \\ \frac{\partial^2 f}{\partial z \partial x} & \frac{\partial^2 f}{\partial z \partial y} & \frac{\partial^2 f}{\partial z^2} \end{array} \right).
```

Using Equation (3.30), we can compute the curvature of a surface given in global coordinates, without the need of constructing a local coordinate system. For details of the derivation of Equation 3.29, see [Hartmann 99].

Summarizing, we can compute the curvature of a planar curve using its second derivative $\partial^2 f / \partial x^2$, and the curvature of a 3D surface in a given direction using its Hessian matrix $H$ of partial derivatives. Given this property of the Hessian matrix, it is also called the _curvature tensor_ of the given surface.

Tensors, vectors, and scalars. Besides curvature, tensors can describe other physical quantities that depend on direction, such as water diffusivity or stress and strain in materials. Tensors are characterized by their _rank_. Scalars are tensors of rank 0. Vectors are tensors of rank 1. The Hessian curvature tensor is a rank 2 symmetric tensor, since it is expressed by a symmetric, rank 2 matrix. In general, tensors of rank $k$ are $k$-dimensional real-valued arrays.