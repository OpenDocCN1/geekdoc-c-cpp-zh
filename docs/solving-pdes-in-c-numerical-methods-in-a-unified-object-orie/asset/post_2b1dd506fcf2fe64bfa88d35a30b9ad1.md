
As before, these functions vanish (with their gradient and Hessian) at corners different from $\tilde{i}$. At $\tilde{i}$, on the other hand, they have only one nonzero partial derivative. Indeed, by applying $\nabla^t$ to both sides of this equation and using the chain rule (Sections 10.11, 12.5, and 30.10), we obtain the 3 × 3 matrix equation

$$
\nabla^t \begin{pmatrix} R_{|\tilde{i}|+\hat{i}_{0,0,1},t} \\ R_{|\tilde{i}|+\hat{i}_{1,0,0},t} \\ R_{|\tilde{i}|+\hat{i}_{1,0,0},t} \end{pmatrix} = S_t \nabla^t \begin{pmatrix} r_{|\tilde{i}|+\hat{i}_{0,0,1},t} \\ r_{|\tilde{i}|+\hat{i}_{0,1,0},t} \\ r_{|\tilde{i}|+\hat{i}_{1,0,0},t} \end{pmatrix} = S_t \left( \begin{pmatrix} \nabla^t p_{|\tilde{i}|+\hat{i}_{0,0,1}} \\ \nabla^t p_{|\tilde{i}|+\hat{i}_{1,0,0}} \\ \nabla^t p_{|\tilde{i}|+\hat{i}_{1,0,0}} \end{pmatrix} \circ D_t^{-1} \right) S_t^{-1}.
$$

Clearly, at every corner of $t$ that is different from $\tilde{i}$ the middle term in the above triple product is just the 3 × 3 zero matrix, which implies that the gradient vanishes, as required. At $\tilde{i}$, on the other hand, the middle term in the above triple product is the 3 × 3 identity matrix $I$, leading to

$$
\nabla^t \begin{pmatrix} R_{|\tilde{i}|+\hat{i}_{0,0,1},t} \\ R_{|\tilde{i}|+\hat{i}_{0,1,0},t} \\ R_{|\tilde{i}|+\hat{i}_{1,0,0},t} \end{pmatrix} = S_t S_t^{-1} = I,
$$

as required.

Unfortunately, the gradient-related corner functions defined above are not yet basis functions, because their normal derivatives do not necessarily vanish at edge and side midpoints that lie by $\tilde{i}$. Later on, they’ll be modified to be proper basis functions.

## 28.6 Tensors

To define the so-called Hessian-related corner functions, corresponding to the second partial derivatives at a corner $\tilde{i}$ of $t$, we must first introduce the notion of tensors. Let $A$ be a 3 × 3 symmetric matrix. Thanks to the symmetry property, $A$ is well defined in terms of six elements only, and can therefore be represented uniquely as the six-dimensional column vector

$$
A \equiv \begin{pmatrix} a_{1,1} \\ a_{2,1} \\ a_{2,2} \\ a_{3,1} \\ a_{3,2} \\ a_{3,3} \end{pmatrix}.
$$

Let $S$ be some 3 × 3 matrix. Consider the linear mapping

$$
A \to S A S^t,
$$

which maps $A$ to the 3 × 3 symmetric matrix $S A S^t$. More specifically, for every two indices $1 \le l,m \le 3$, we have

$$
(S A S^t)_{l,m} = \sum_{j=1}^{3} \sum_{k=1}^{3} S_{l,j} a_{j,k} (S^t)_{k,m} = \sum_{j,k=1}^{3} S_{l,j} S_{m,k} a_{j,k}.
$$

In this formulation, $A$ can be viewed as a nine-dimensional vector, with the two-dimensional vector index $(j,k)$ rather than the usual scalar index. Furthermore, $S_{l,j} S_{m,k}$ can be viewed as a 9 × 9 matrix, with the two-dimensional vector indices $(l,m)$ (row index) and $(j,k)$ (column index) rather than the usual scalar indices.

A matrix with this kind of indexing is also called a tensor. Here the tensor $S \otimes S$ is defined by

$$
(S \otimes S)_{(l,m),(j,k)} \equiv S_{l,j} S_{m,k}.
$$

Clearly, the transpose tensor is obtained by interchanging the roles of the row index $(l,m)$ and the column index $(j,k)$. Thus, the $(l,m),(j,k)$th element in the transpose tensor is

$$
S_{j,l} S_{k,m} = (S^t)_{l,j} (S^t)_{m,k}.
$$

As a result, the transpose tensor is associated with the transpose mapping

$$
A \to S^t A S.
$$

Thanks to the linearity of the original mapping that maps the symmetric matrix $A$ to the symmetric matrix $S A S^t$, it can also be represented more economically as a mapping of six-dimensional column vectors:

$$
\begin{pmatrix} a_{1,1} \\ a_{2,1} \\ a_{2,2} \\ a_{3,1} \\ a_{3,2} \\ a_{3,3} \end{pmatrix} \to Z \begin{pmatrix} a_{1,1} \\ a_{2,1} \\ a_{2,2} \\ a_{3,1} \\ a_{3,2} \\ a_{3,3} \end{pmatrix}.
$$

where $Z \equiv Z(S)$ is a suitable 6 × 6 matrix. In fact, $Z$ can be defined as follows: the six components in its first column are the same as the six elements in the lower triangular part of

$$
S \begin{pmatrix} 1 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} S^t.
$$

The six components in its second column are the same as the six elements in the lower triangular part of

$$
S \begin{pmatrix} 0 & 1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} S^t.
$$

And so on.

As a matter of fact, the mapping defined by $Z$ can also be viewed as a mapping of six-dimensional row vectors:

$$
(a_{1,1},a_{2,1},a_{2,2},a_{3,1},a_{3,2},a_{3,3}) \to (a_{1,1},a_{2,1},a_{2,2},a_{3,1},a_{3,2},a_{3,3}) Z^t.
$$

## 28.7 Hessian-Related Corner Functions

In the definition of the so-called Hessian-related corner functions, corresponding to the second partial derivatives at the corner $i$ of $T$, the matrix $S$ used in the above tensor is set to be the transpose of the inverse of $S_i$:

$$
S \leftarrow S_i^{-T}.
$$

So the 6 × 6 matrix $Z$ takes the concrete value

$$
Z = Z(S_i^{-T}).
$$

This special case is particularly relevant to the second partial derivatives of a composite function defined in $t$. Indeed, for any function $v(x, y, z)$ with continuous second partial derivatives, $\nabla\nabla^T v$ is a 3 × 3 symmetric matrix. Therefore, $\nabla\nabla^T v$ can also be represented uniquely as the six-dimensional row vector

$$
(v_{xx}, v_{xy}, v_{yy}, v_{xz}, v_{yz}, v_{zz}).
$$

We are thus ready to define the Hessian-related corner functions in $t$, whose partial derivatives vanish at all four corners, except for only one second partial derivative at one corner $\tilde{i} \in t$, which has the value 1. The six functions are defined compactly by

$$
\begin{pmatrix}
R_{|\tilde{i}|+\hat{i}_{0,0,2},t}^i \\
R_{|\tilde{i}|+\hat{i}_{0,1,1},t}^i \\
R_{|\tilde{i}|+\hat{i}_{0,2,0},t}^i \\
R_{|\tilde{i}|+\hat{i}_{1,0,1},t}^i \\
R_{|\tilde{i}|+\hat{i}_{1,1,0},t}^i \\
R_{|\tilde{i}|+\hat{i}_{2,0,0},t}^i
\end{pmatrix} \equiv Z^{-T}
\begin{pmatrix}
r_{|\tilde{i}|+\hat{i}_{0,0,2},t}^i \\
r_{|\tilde{i}|+\hat{i}_{0,1,1},t}^i \\
r_{|\tilde{i}|+\hat{i}_{0,2,0},t}^i \\
r_{|\tilde{i}|+\hat{i}_{1,0,1},t}^i \\
r_{|\tilde{i}|+\hat{i}_{1,1,0},t}^i \\
r_{|\tilde{i}|+\hat{i}_{2,0,0},t}^i
\end{pmatrix}.
$$

Indeed, the Hessian operator can be applied separately to each of these six functions, to map it to the six-dimensional row vector of its second partial derivatives and form the following 6 × 6 matrix:

$$
\begin{pmatrix}
\nabla\nabla^T R_{|\tilde{i}|+\hat{i}_{0,0,2},t}^i \\
R_{|\tilde{i}|+\hat{i}_{0,1,1},t}^i \\
R_{|\tilde{i}|+\hat{i}_{0,2,0},t}^i \\
R_{|\tilde{i}|+\hat{i}_{1,0,1},t}^i \\
R_{|\tilde{i}|+\hat{i}_{1,1,0},t}^i \\
R_{|\tilde{i}|+\hat{i}_{2,0,0},t}^i
\end{pmatrix} = Z^{-T}
\begin{pmatrix}
\nabla\nabla^T r_{|\tilde{i}|+\hat{i}_{0,0,2},t}^i \\
\nabla\nabla^T r_{|\tilde{i}|+\hat{i}_{0,1,1},t}^i \\
\nabla\nabla^T r_{|\tilde{i}|+\hat{i}_{0,2,0},t}^i \\
\nabla\nabla^T r_{|\tilde{i}|+\hat{i}_{1,0,1},t}^i \\
\nabla\nabla^T r_{|\tilde{i}|+\hat{i}_{1,1,0},t}^i \\
\nabla\nabla^T r_{|\tilde{i}|+\hat{i}_{2,0,0},t}^i
\end{pmatrix} = Z^{-T}
\begin{pmatrix}
\nabla\nabla^T p_{|\tilde{i}|+\hat{i}_{0,0,2}} \odot D_t^{-1} \\
\nabla\nabla^T p_{|\tilde{i}|+\hat{i}_{0,1,1}} \odot D_t^{-1} \\
\nabla\nabla^T p_{|\tilde{i}|+\hat{i}_{0,2,0}} \odot D_t^{-1} \\
\nabla\nabla^T p_{|\tilde{i}|+\hat{i}_{1,0,1}} \odot D_t^{-1} \\
\nabla\nabla^T p_{|\tilde{i}|+\hat{i}_{1,1,0}} \odot D_t^{-1} \\
\nabla\nabla^T p_{|\tilde{i}|+\hat{i}_{2,0,0}} \odot D_t^{-1}
\end{pmatrix} Z^t.
$$

(The chain rule has been used here twice.) Clearly, at corners different from $\tilde{i}$, the middle term in the above triple product vanishes, as required. At $\tilde{i}$, on the other hand, it is just the 6 × 6 identity matrix $I$, leading to

$$
\nabla\nabla^t \begin{pmatrix} R_{|\tilde{i}|+\hat{i}_{0,0,2},t}^i \\ R_{|\tilde{i}|+\hat{i}_{0,1,1},t}^i \\ R_{|\tilde{i}|+\hat{i}_{0,2,0},t}^i \\ R_{|\tilde{i}|+\hat{i}_{1,0,1},t}^i \\ R_{|\tilde{i}|+\hat{i}_{1,1,0},t}^i \\ R_{|\tilde{i}|+\hat{i}_{2,0,0},t}^i \end{pmatrix} = Z^{-T} I Z^t = I,
$$

as required.

Unfortunately, these functions are not yet basis functions, because their normal derivatives do not necessarily vanish at edge and side midpoints that lie by $\tilde{i}$. They'll be modified later to be proper basis functions.

## 28.8 Edge-Midpoint Functions

Here we define the so-called edge-midpoint functions $R_{i,f}$ ($40 \le i < 52$) in $t$. Consider the two degrees of freedom $40 \le i, i + 1 < 52$ (for some even $i$) corresponding to the normal derivatives at the edge midpoint $w \in e$, where $e$ is some edge in the reference tetrahedron $T$. (The basis functions corresponding to these degrees of freedom, $p_i$ and $p_{i+1}$, are defined in $T$ in Section 28.2.) Let us denote these normal directions by the three-dimensional unit vectors $\vec{n}^{(1)}$ and $\vec{n}^{(2)}$. Let $\vec{n}^{(3)}$ be the unit vector that is tangent to $e$.

Let us show that both $p_i$ and $p_{i+1}$ vanish in the edge $e$ in $T$. Indeed, in this edge, they are just polynomials of degree five in one variable, so they are determined uniquely by six degrees of freedom only. Now, both functions have six vanishing degrees of freedom in $e$: the function and its first and second derivative at the endpoints. Therefore, they must vanish in the entire edge $e$, as asserted.

As a result, their tangential derivative along $e$ (and, in particular, at its midpoint $w$) must vanish as well:

$$
\nabla p_i(w) \vec{n}^{(3)} = \nabla p_{i+1}(w) \vec{n}^{(3)} = 0.
$$

Define the 3 × 3 matrix formed by these three unit column vectors:

$$
\vec{N}_e \equiv ( \vec{n}^{(1)} | \vec{n}^{(2)} | \vec{n}^{(3)} ).
$$
