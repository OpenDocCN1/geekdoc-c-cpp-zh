
We can find the null space by multiplying $A$ by the unknown vector $\mathbf{x} = [x_1 \ x_2 \ x_3]^T$ and setting the result to zero.

$$
\begin{bmatrix} 1 & 5/4 & 3/2 \\ 0 & 1 & 2 \\ 0 & 0 & 0 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}.
$$

Setting the product to zero yields the following equations

$x_1 + \frac{5}{4}x_2 + \frac{3}{2}x_3 = 0$ (3.8)

$x_2 + 2x_3 = 0.$ (3.9)

That simplifies to

$x_1 = x_3$ (3.10)

$x_2 = -2x_3.$ (3.11)

Let $x_3 = 1$, and the null vector is $[1 \ -2 \ 1]^T$. Since the rank is 2, the null space consists of this one vector and all scalar multiples of it. Division of $[1 \ -2 \ 1]^T$ by its magnitude, $\sqrt{6}$, produces a unit vector; $[0.4082 \ -0.8165 \ 0.4082]^T$.

### Right and Left Null Space

Above, we solved the problem

$A\mathbf{x} = \mathbf{0}.$

Instead, however, we might have been confronted with the following problem

$\mathbf{x}A = \mathbf{0},$

which is referred to as finding the left null space. The left null space of a matrix, $A$ is simply the null space of $A^T$.

### 3.2.4 Function Spaces

Think about a function, say $f(x) = x^2$, defined on the integers greater than zero and less than six. You could list the values of $f(x)$ as an ordered set: [1, 4, 9, 16, 25], which looks exactly like a vector. So it is perfectly fine to think of a function as a vector. Of course, there is one slight problem. If we define our function on the real numbers, we end up with a vector with infinite dimensionality. But, except for the fact that we cannot list all the elements, infinite dimensionality is not a problem.

The concept of orthogonality can easily be extended to continuous functions by simply thinking of a function as an infinite-dimensional vector. Just list all the values of $f(x)$ as $x$ varies between, say, $a$ and $b$. If $x$ is continuous, then there are an infinite number of possible values of $x$ between $a$ and $b$. But that should not stop us – we cannot enumerate them, but we can still think of a vector containing all the values of $f(x)$. Now, the concept of summation that we defined for finite-dimensional vectors turns into integration, and an inner product may be written

$<f(x), g(x)> = \int_a^b f(x)g(x)dx.$ (3.12)

![](img/5f95dd954ac63cc68119f6f48ca99e18_37_0.png)

Figure 3.2 The mental image that appears in the mind of someone who confuses orthogonal and perpendicular in misunderstanding the statement “The cosine is orthogonal to the sine.”

The concepts of orthogonality and orthonormality hold for this definition of the inner product as well. If the integral is equal to zero, we say the two functions are orthogonal. So the transition from orthogonal vectors to orthogonal functions is not that difficult. With an infinite number of dimensions, it is impossible to visualize orthogonal as “perpendicular,” of course, so you need to give up on thinking about things being perpendicular. Just recall the definition and use it.

However, in case you like silly misunderstandings, Figure 3.2 illustrates an incorrect interpretation of the statement “The sine and the cosine are orthogonal.”²

### 3.2.5 Linear Transformations

A linear transformation, A, is simply a matrix. Suppose A is m × d. If applied to a vector x ∈ ℜ^d, y = Ax then y ∈ ℜ^m. So A took a vector from one vector space, ℜ^d, and produced a vector in ℜ^m. If that vector y could have been produced by applying A to one and only one vector in ℜ^d, then A is said to be one-to-one. Now suppose that there are no vectors in ℜ^m that cannot be produced by applying A to some vector in ℜ^d; in that case, A is said to be onto. If A is one-to-one and onto, then $A^{-1}$ exists. Two matrices A and B are conformable if the matrix multiplication C = AB makes sense.

Some important (and often forgotten) properties: If \(A\) and \(B\) are conformable, then

\((AB)^T = B^T A^T\) (3.13)

and

\((AB)^{-1} = B^{-1} A^{-1}\) (3.14)

if \(A\) and \(B\) are invertible at all.

A couple of other useful properties related to determinant (det) and trace (tr) are

\(\det(AB) = \det(BA) \quad \text{and} \quad \text{tr}(AB) = \text{tr}(BA)\)

which is only true, of course, if \(A\) and \(B\) are square.

### Orthonormal Transformation

If a matrix \(A\) satisfies

\(AA^T = A^T A = I\) (3.15)

then obviously, the transpose of the matrix is the inverse as well, and \(A\) is said to be an orthonormal transformation (OT), which will correspond geometrically to a rotation. If \(A\) is a \(d \times d\) orthonormal transformation, then the columns of \(A\) are orthonormal, linearly independent, and form a basis spanning the space of \(\Re^d\). For \(\Re^3\), three convenient OTs are the rotations about the Cartesian axes (assuming the right-handed coordinate system*) with \(\theta\) being the rotation angle defined in the counterclockwise direction.

\(R_x = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos \theta & -\sin \theta \\ 0 & \sin \theta & \cos \theta \end{bmatrix}, R_y = \begin{bmatrix} \cos \theta & 0 & \sin \theta \\ 0 & 1 & 0 \\ -\sin \theta & 0 & \cos \theta \end{bmatrix}, R_z = \begin{bmatrix} \cos \theta & -\sin \theta & 0 \\ \sin \theta & \cos \theta & 0 \\ 0 & 0 & 1 \end{bmatrix}\) (3.16)

Suppose \(R\) is an OT, and \(\mathbf{y} = R\mathbf{x}\), then both \(\mathbf{x}\) and \(\mathbf{y}\) have the same magnitude:

\(|\mathbf{y}| = |\mathbf{x}|\) (3.17)

Although the three rotation matrices in Eq. 3.16 share some common characteristics, i.e., there are always a column of zeros and a single 1 as well as a row of zeros and a single 1, these characteristics are not the necessary condition to make a rotation matrix. In fact, rotation matrices share two interesting properties:

- the product of two rotation matrices (i.e., OT) is a rotation matrix, and
- any OT can be considered a rotation matrix, where the rotation is about some axis.

In the following, we show an example that well demonstrates the above two properties.

3 We assume you know the meanings of transpose, inverse, determinant, and trace. If you do not, you should not be taking this course.

4 Right-handed coordinate system indicates that the axis about which the rotation (indicated by circling the fingers) occurs points toward the observer.

Suppose two rotations are performed in sequence with the first one rotating about x by 20 degrees, followed by a second one rotating about z by 45 degrees, both in the counter-clockwise direction, then the composite transformation matrix, \( R_{xz} \), can be calculated by \( R_{xz} = R_z R_x \), where

\( R_x = \begin{bmatrix} 1.0000 & 0 & 0 \\ 0 & 0.9397 & 0.3420 \\ 0 & -0.3420 & 0.9397 \end{bmatrix}, R_z = \begin{bmatrix} 0.7071 & -0.7071 & 0 \\ 0.7071 & 0.7071 & 0 \\ 0 & 0 & 1.0000 \end{bmatrix} \).

and

\( R_{xz} = R_z R_x = \begin{bmatrix} 0.7071 & -0.7071 & 0 \\ 0.6645 & 0.6645 & 0.3420 \\ -0.2418 & -0.2418 & 0.9397 \end{bmatrix} \).

As we can see, in the composite matrix \( R_{xz} \), the columns are orthogonal, yet we do not see the column of zeros and a single 1 that characterizes the three rotation matrices around x, y, and z in Eq. 3.16.

### Positive Definite

A matrix \( A \) is positive definite if

\( y = x^T A x > 0, \forall x \in \Re^d, x \neq 0 \).

A matrix \( A \) is positive semidefinite if

\( y = x^T A x \ge 0, \forall x \in \Re^d, x \neq 0 \).

\( x^T A x \) is called a quadratic form. Since the quadratic form always returns a scalar, a positive definite or a positive semidefinite matrix is always square.

### 3.2.6 Derivatives and Derivative Operators

The derivative of a quadratic form is particularly useful:

\( \frac{d}{dx}(x^T A x) = (A + A^T)x \).

Since we mentioned derivatives, we will mention a couple of other vector calculus things:

Suppose \( f(\mathbf{x}) \) is a scalar function of \( \mathbf{x}, \mathbf{x} \in \Re^d \), then

\( \frac{df}{d\mathbf{x}} = \left[ \frac{\partial f}{\partial x_1} \frac{\partial f}{\partial x_2} \dots \frac{\partial f}{\partial x_d} \right]^T, \quad (3.18) \).

and is called the gradient. This will be often used when we talk about edges in images, and \( f(\mathbf{x}) \) will be the brightness as a function of the two spatial directions. If \( f(\mathbf{x}) \) is vector-valued, then the derivative is a matrix

\( \frac{d\mathbf{f}}{d\mathbf{x}} = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \dots & \frac{\partial f_1}{\partial x_d} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial f_d}{\partial x_1} & \frac{\partial f_d}{\partial x_2} & \dots & \frac{\partial f_d}{\partial x_d} \end{bmatrix}, \quad (3.19) \).

and is called the Jacobian.
