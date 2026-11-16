
## CHAPTER TWO

## Mathematical Preliminary

The purpose of this chapter is to familiarize the reader with some of the mathematical notations and tools that are useful in an understanding of wavelet theory. Since wavelets are continuous functions that satisfy certain admissibility conditions, it is prudent to discuss in this chapter some definitions and properties of functional spaces. For a more detailed discussion of functional spaces, the reader is referred to standard texts on real analysis. The wavelet algorithms discussed in later chapters involve digital processing of coefficient sequences. A fundamental understanding of topics in digital signal processing, such as sampling, the z-transform, linear shift-invariant systems, and discrete convolution, are necessary for a good grasp of wavelet theory. In addition, a brief discussion of linear algebra and matrix manipulations is included that is very useful in discrete-time domain analysis of filter banks. Readers already familiar with its contents may skip this chapter.

### 2.1 LINEAR SPACES

In the broadest sense, a functional space is simply a collection of functions that satisfies a certain mathematical structural pattern. For example, the finite energy space \( L^2(-\infty, \infty) \) is a collection of functions that are square integrable; that is,

(2.1) \int_{-\infty}^{\infty} |f(x)|^2 dx < \infty,

Some of the requirements and operational rules on linear spaces are stated as follows:

- 1. The space S must not be empty.
- 2. If x \in S and y \in S, then x + y = y + x.
- 3. If z \in S, then (x + y) + z = x + (y + z).
- 4. There exists in S a unique element 0, such that x + 0 = x.
- 5. There exists in S another unique element -x such that x + (-x) = 0.

Besides these simple yet important rules, we also define scalar multiplication y = cx such that if x \in S, then y \in S, for every scalar c. We have the following additional rules for the space S:

- 1. c(x + y) = cx + cy.
- 2. (c + d)x = cx + dx with scalar c and d.
- 3. (cd)x = c(dx).
- 4. 1 \cdot x = x.

Spaces that satisfy these additional rules are called linear spaces. However, up to now, we have not defined a measure to gauge the size of an element in a linear space. If we assign a number $||x||$, called the norm of x, to each function in S, this space becomes a *normed linear space* (i.e., a space with a measure associated with it). The norm of a space must also satisfy certain mathematical properties:

- 1. $||x|| \ge 0$ and $||x|| = 0 \Leftrightarrow x = 0$.
- 2. $||x + y|| \le ||x|| + ||y||$.
- 3. $||ax|| = |a| ||x||$ where $a$ is scalar.

The norm of a function is simply a measure of the distance of the function to the origin (i.e., 0). In other words, we can use the norm

(2.2) $||x - y||$

to measure the difference (or distance) between two functions x and y.

There are a variety of norms one may choose as a measure for a particular linear space. For example, the finite energy space $L^2(-\infty, \infty)$ uses the norm

(2.3) $||x|| = \left[ \int_{-\infty}^{\infty} |f(x)|^2 dx \right]^{\frac{1}{2}} < \infty$

which we shall call the $L^2$-norm. This norm has also been used to measure the overall difference (or error) between two finite energy functions. This measure is called the root mean square error (RMSE) defined by

RMSE = \left[ \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} |f(x) - f_a(x)|^2 dx \right]^{\frac{1}{2}}
(2.4)

where \(f_a(x)\) is an approximating function to \(f(x)\). The expression in (2.4) is the approximation error in the \(L^2\) sense.

### 2.2 VECTORS AND VECTOR SPACES

Based on the basic concepts of functional spaces discussed in the previous section, we now present some fundamentals of vector spaces. We begin with a brief review of geometric vector analysis.

A vector \(V\) in a three-dimensional Euclidean vector space is defined by three complex numbers \(\{v_1, v_2, v_3\}\) associated with three orthogonal unit vectors \(\{a_1, a_2, a_3\}\).

The ordered set \(\{v_j\}_{j=1}^3\) represents the scalar components of the vector \(V\) where the unit vector set \(\{a_j\}_{j=1}^3\) spans the three-dimensional Euclidean vector space. Any vector \(U\) in this space can be decomposed into three vector components \(\{u_j a_j\}_{j=1}^3\) (Figure 2.1d).

FIGURE 2.1: Orthogonal decomposition of a vector in Euclidean space.

![](img/f73ae67732328dc36596b27ffe8d0152_37_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_37_1.png)

![](img/f73ae67732328dc36596b27ffe8d0152_37_2.png)

![](img/f73ae67732328dc36596b27ffe8d0152_37_3.png)

The addition and scalar multiplication of vectors in this space are defined by:

- 1. \(\boldsymbol{U} + \boldsymbol{V} = \{u_1 + v_1, u_2 + v_2, u_3 + v_3\}\).
- 2. \(k\boldsymbol{V} = \{kv_1, kv_2, kv_3\}\).

In addition to these operations, vectors in a three-dimensional Euclidean space also obey the commutative and associative laws:

- 1. \(\boldsymbol{U} + \boldsymbol{V} = \boldsymbol{V} + \boldsymbol{U}\).
- 2. \((\boldsymbol{U} + \boldsymbol{V}) + \boldsymbol{W} = \boldsymbol{U} + (\boldsymbol{V} + \boldsymbol{W})\).

We may represent a vector by a column matrix

$$\mathbf{V} = \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix},$$

since all of the above mathematical rules apply to column matrices. We define the length of a vector similar to the definition of the norm of a function by

$$|\mathbf{V}| = \sqrt{v_1^2 + v_2^2 + v_3^2}.$$

The scalar product (inner product) of two vectors is a very important operation in vector algebra that we should consider here. It is defined by

$$\begin{aligned} \mathbf{U} \cdot \mathbf{V} &:= |\mathbf{U}||\mathbf{V}| \cos \angle \mathbf{U}, \mathbf{V} \\ &= u_1 v_1 + u_2 v_2 + u_3 v_3 \\ &= [u_1 \ u_2 \ u_3] \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} \\ &= \begin{bmatrix} u_1 \\ u_2 \\ u_3 \end{bmatrix}^t \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix}, \end{aligned}$$

where the superscript \(t\) indicates matrix transposition and \(:=\) is the symbol for definition. It is known that the scalar product obeys the commutative law: \(\mathbf{U} \cdot \mathbf{V} = \mathbf{V} \cdot \mathbf{U}\). Two vectors \(\mathbf{U}\) and \(\mathbf{V}\) are *orthogonal* to each other if \(\mathbf{U} \cdot \mathbf{V} = 0\).

We define the *projection* of a vector onto another vector by

\(\frac{\boldsymbol{U} \cdot \boldsymbol{V}}{|\boldsymbol{V}|} = \boldsymbol{U} \cdot \boldsymbol{a}_v\)
\(= \text{projection of } \boldsymbol{U} \text{ in the direction of } \boldsymbol{a}_v\)
\(= \text{a component of } \boldsymbol{U} \text{ in the direction of } \boldsymbol{a}_v.\)
(2.8)

Projection is an important concept that will be used often in later discussions. If one needs to find the component of a vector in a given direction, simply project the vector in that direction by taking the scalar product of the vector with the unit vector of the desired direction.

We may now extend this concept of basis and projection from the three-dimensional Euclidean space to an \(N\)-dimensional vector space. The components of a vector in this space form an \(N \times 1\) column matrix, while the basis vectors \(\{ \boldsymbol{a}_j \}_{j=1}^N\) form an orthogonal set such that

(2.9) \(\boldsymbol{a}_k \cdot \boldsymbol{a}_\ell = \delta_{k,\ell}, \quad \forall k, \ell \in \mathbb{Z}\)

where \(\delta_k\) is the Kronecker delta, defined as

(2.10) \(\delta_{k,\ell} = \begin{cases} 1, & k = \ell \\ 0, & k \neq \ell. \end{cases}\)

and \(\mathbb{Z}\) is the set of all integers, \(\{..., -1, 0, 1, ...\}\).

One can obtain a specific component $v_j$ of a vector $\boldsymbol{V}$ (or the projection of $\boldsymbol{V}$ in the direction of $\boldsymbol{a}_j$) using the inner product

**(2.11)** $$v_j = \boldsymbol{V} \cdot \boldsymbol{a}_j,$$

and the vector $\boldsymbol{V}$ is expressed as a linear combination of its vector components

**(2.12)** $$\boldsymbol{V} = \sum_{k=1}^N v_k \boldsymbol{a}_k.$$

It is well known that a vector can be decomposed into elementary vectors along the direction of the basis vectors by finding its components one at a time. Figure 2.1 illustrates this procedure. The vector $\boldsymbol{V}$ in Figure 2.1a is decomposed into $\boldsymbol{V}_p = \boldsymbol{V} - v_3 \boldsymbol{a}_3$ and its orthogonal complementary vector $v_3 \boldsymbol{a}_3$. The vector $\boldsymbol{V}_p$ is further decomposed into $v_1 \boldsymbol{a}_1$ and $v_2 \boldsymbol{a}_2$. Figure 2.1d represents the reconstruction of the vector $\boldsymbol{V}$ from its components.

The example shown in Figure 2.1, although elementary, is analogous to the wavelet decomposition and reconstruction algorithm. There the orthogonal components are wavelet functions at different resolutions.

### 2.3 BASIS FUNCTIONS, ORTHOGONALITY, AND BIORTHOGONALITY

We extend the concept of Euclidean geometric vector space to normed linear spaces. That is, instead of thinking
