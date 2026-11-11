
![](img/f464cd0043eb5336aa0543fe20a0561b_281_0.png)

*Figure 10.8:* (a) An n × k matrix, with n > k, factors as a product of an n × n matrix with orthonormal columns (indicated by the vertical stripes on the first rectangle), a diagonal k × k matrix, and a k × k matrix with orthonormal rows (indicated by the horizontal stripes), which we write as UDV^T, where U and V have orthonormal columns. (b) An n × k matrix with n < k is written as a similar product; note that the diagonal matrix in both cases is square, and its size is the smaller of n and k.

As a guideline, if the ratio of the largest to the smallest singular values is very large (say, $10^6$), then numerical computations with the matrix are likely to be unstable.

> **Inline Exercise 10.16:** The singular value decomposition is not unique. If we negate the first row of $\mathbf{V}^{\mathsf{T}}$ and the first column of $\mathbf{U}$ in the SVD of a matrix $\mathbf{M}$, show that the result is still an SVD for $\mathbf{M}$.

In the special case where $n = k$ (the one we most often encounter), the matrices $U$ and $V$ are both square and represent change-of-coordinate transformations in the domain and codomain. Thus, we can see the transformation

$$ T(x) = Mx \tag{10.41} $$

as a sequence of three steps: (1) Multiplication by $V^{\mathsf{T}}$ converts $x$ to v-coordinates; (2) multiplication by $D$ amounts to a possibly nonuniform scaling along each axis; and (3) multiplication by $U$ treats the resultant entries as coordinates in the u-coordinate system, which then are transformed back to standard coordinates.

### 10.3.8 Computing the SVD

How do we find $U$, $D$, and $V$? In general it’s relatively difficult, and we rely on numerical linear algebra packages to do it for us. Furthermore, the results are by no means unique: A single matrix may have multiple singular value decompositions. For instance, if $S$ is any $n \times n$ matrix with orthonormal columns, then

$$ I = S I S^{\mathsf{T}} \tag{10.42} $$

is one possible singular value decomposition of the identity matrix. Even though there are many possible SVDs, the singular values are the same for all decompositions.

The **rank** of the matrix **M**, which is defined as the number of linearly independent columns, turns out to be exactly the number of nonzero singular values.

### 10.3.9 The SVD and Pseudoinverses

Again, in the special case where $n = k$ so that $U$ and $V$ are square, it’s easy to compute $\mathbf{M}^{-1}$ if you know the SVD:

$$ \mathbf{M}^{-1} = \mathbf{V}\mathbf{D}^{-1}\mathbf{U}^{\mathsf{T}}. \tag{10.43} $$

where $D^{-1}$ is easy to compute—you simply invert all the elements of the diagonal. If one of these elements is zero, the matrix is singular and no such inverse exists; in this case, the **pseudoinverse** is also often useful. It’s defined as

$$ \mathbf{M}^{\dagger}=\mathbf{V}\mathbf{D}^{\dagger}\mathbf{U}^{\mathsf{T}}, \tag{10.44} $$

where $D^{\dagger}$ is just $D$ with every nonzero entry inverted (i.e., you try to invert the diagonal matrix $D$ by inverting diagonal elements, and every time you encounter a zero on the diagonal, you ignore it and simply write down 0 in the answer). The definition of the pseudoinverse makes sense even when $n\ne k$; the pseudoinverse can be used to solve “least squares” problems, which frequently arise in graphics.

**The Pseudoinverse Theorem:**

- **(a)** If $\mathbf{M}$ is an $n\times k$ matrix with $n>k$, the equation $\mathbf{M}\mathbf{x}=\mathbf{b}$ generally represents an overdetermined system of equations² which may have no solution. The vector $\mathbf{x}_0=\mathbf{M}^{\dagger}\mathbf{b}$ (10.45) represents an optimal “solution” to this system, in the sense that $\mathbf{M}\mathbf{x}_0$ is as close to $\mathbf{b}$ as possible.
- **(b)** If $\mathbf{M}$ is an $n\times k$ matrix with $n<k$, and rank $n$, the equation $\mathbf{M}\mathbf{x}=\mathbf{b}$ represents an underdetermined system of equations.³ The vector $\mathbf{x}_0=\mathbf{M}^{\dagger}\mathbf{b}$ (10.46) represents an optimal solution to this system, in the sense that $\mathbf{x}_0$ is the *shortest* vector satisfying $\mathbf{M}\mathbf{x}=\mathbf{b}$.

² In other words, a situation like “five equations in three unknowns.”

³ That is, a situation like “three equations in five unknowns.”

Here are examples of each of these cases.

**Example 1: An overdetermined system**

The system

$$ \begin{bmatrix}2\\1\end{bmatrix}t=\begin{bmatrix}4\\3\end{bmatrix} \tag{10.47} $$

has no solution: There’s simply no number $t$ with $2t=4$ and $1t=3$ (see Figure 10.9). But among all the multiples of $\mathbf{M}=\begin{bmatrix}2\\1\end{bmatrix}$, there is one that’s closest to the vector $\mathbf{b}=\begin{bmatrix}4\\3\end{bmatrix}$, namely $2.2\begin{bmatrix}2\\1\end{bmatrix}=\begin{bmatrix}4.4\\2.2\end{bmatrix}$, as you can discover with elementary geometry. The theorem tells us we can compute this directly, however, using the pseudoinverse. The SVD and pseudoinverse of $\mathbf{M}$ are

![](img/f464cd0043eb5336aa0543fe20a0561b_282_0.png)

$$ \mathbf{M}=\mathbf{U}\mathbf{D}\mathbf{V}^{\mathsf{T}}=\left(\frac{1}{\sqrt{5}}\begin{bmatrix}2\\1\end{bmatrix}\right)[\sqrt{5}][1] \tag{10.48} $$

$$ \mathbf{M}^{\dagger}=\mathbf{V}\mathbf{D}^{\dagger}\mathbf{U}^{\mathsf{T}}=[1][1/\sqrt{5}]\left(\frac{1}{\sqrt{5}}\begin{bmatrix}2&1\end{bmatrix}\right) \tag{10.49} $$

$$ =[0.4\quad 0.2]. \tag{10.50} $$

And the solution guaranteed by the theorem is

$$ t = \mathbf{M}^{\dagger}\mathbf{b} = [0.4\quad 0.2]\begin{bmatrix}4\\3\end{bmatrix} = 2.2. \tag{10.51} $$

**Example 2: An underdetermined system**

The system

$$ \begin{bmatrix}1 & 3\end{bmatrix}\begin{bmatrix}x\\y\end{bmatrix}=4. \tag{10.52} $$

has a great many solutions; any point $(x, y)$ on the line $x + 3y = 4$ is a solution (see Figure 10.10). The solution that’s *closest to the origin* is the point on the line $x + 3y = 4$ that’s as near to $(0, 0)$ as possible, which turns out to be $x = 0.4; y = 1.2$. In this case, the matrix $\mathbf{M}$ is $[1\quad 3]$; its SVD and pseudoinverse are simply

![](img/f464cd0043eb5336aa0543fe20a0561b_283_0.png)

**Figure 10.10:** Any point of the blue line is a solution; the red point is closest to the origin.

$$ \mathbf{M} = \mathbf{U}\mathbf{D}\mathbf{V}^{\mathsf{T}} = [1]\,[\sqrt{10}]\,[1/\sqrt{10}\quad 3/\sqrt{10}] \quad \text{and} \tag{10.53} $$

$$ \mathbf{M}^{\dagger} = \mathbf{V}\mathbf{D}^{-1}\mathbf{U}^{\mathsf{T}} = \begin{bmatrix}1/\sqrt{10}\\3/\sqrt{10}\end{bmatrix}[1/\sqrt{10}]\begin{bmatrix}1\end{bmatrix} = \begin{bmatrix}1/10\\3/10\end{bmatrix}. \tag{10.54} $$

And the solution guaranteed by the theorem is

$$ \mathbf{M}^{\dagger}\mathbf{b} = \begin{bmatrix}1/10\\3/10\end{bmatrix}\begin{bmatrix}4\end{bmatrix} = \begin{bmatrix}0.4\\1.2\end{bmatrix}. \tag{10.55} $$

Of course, this kind of computation is much more interesting in the case where the matrices are much larger, but all the essential characteristics are present even in these simple examples.

A particularly interesting example arises when we have, for instance, two polyhedral models (consisting of perhaps hundreds of vertices joined by triangular faces) that might be “essentially identical.” One might be just a translated, rotated, and scaled version of the other. In *Section 10.4*, we’ll see how to represent *translation* along with rotation and scaling in terms of matrix multiplication. We can determine whether the two models are in fact essentially identical by listing the coordinates of the first in the columns of a matrix **V** and the coordinates of the second in a matrix **W**, and then seeking a matrix **A** with

$$ \mathbf{A}\mathbf{V} = \mathbf{W}. \tag{10.56} $$

This amounts to solving the “overconstrained system” problem; we find that $\mathbf{A} = \mathbf{V}^{\mathsf{T}}\mathbf{W}$ is the best possible solution. If, having computed $\mathbf{A}$, we find that

$$ \mathbf{A}\mathbf{V} = \mathbf{W}, \tag{10.57} $$

then the models are essentially identical; if the left and right sides differ, then the models are not essentially identical. (This entire approach depends, of course, on corresponding vertices of the two models being listed in the corresponding order; the more general problem is a lot more difficult.)

## 10.4 Translation

We now describe a way to apply linear transformations to generate *translations*, and at the same time give a nice model for the *points-versus-vectors* ideas we’ve espoused so far.
