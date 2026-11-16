
encounter the rich-get-richer phenomenon. Since the number of customers \(N\) is finite, so is the final number of sampled dishes \(M\). Those chosen by many customers relate to features which are common in most of the data samples. These are sometimes referred to as *global features*, while those dishes chosen only by a few customers indicate *local features*, which can be used to distinguish between data samples.

This process of generating the data is independent of the order the customers arrive. A different order of customers means multiplying \(\mathbf{Z}\) by a permutation matrix from the left which changes the row order. We follow this up with a permutation matrix from the right which swaps columns so that the number of leading zeros in each column is increasing from left to right, because each subsequent customer can choose new dishes. Such a permutation is equivalent to relabeling the dishes. The matrix of weights \(\mathbf{W}\) is multiplied by the same permutation matrices from left and right as \(\mathbf{Z}\). These permutations are not performed explicitly, but serve to explain that the choice of order in which samples are generated does not influence the final outcome.

The previous paragraph indicates a preferred order of dishes. More specifically, given an order of customers (rows of \(\mathbf{Z}\)), the columns of \(\mathbf{Z}\) are ordered using their binary nature. Each customer is interpreted as a binary number with the most significant bit in the first row and the least significant one in the last. The columns are ordered in decreasing magnitude of these binary numbers. Two columns might represent exactly the same binary number. This means two dishes were chosen by exactly the same set of customers. In this case, we have freedom of choice in the order of the columns representing the same binary number. This is known as *left-ordering of binary matrices*.

There are \(M!\) possible labelings of the dishes. We need to divide this by the number of possible equivalences. Let \(K\) be the number of distinct columns and let \(m_k\) be the number of occurrences of the distinct column \(k\) for \(k = 1, 2, ..., K\). That is

\(M = \sum_{k=1}^K m_k.\)

The number of possible equivalences in relabeling is

\(\prod_{k=1}^K m_k!.\)

Hence the number of different ways the same data can have been generated is

\(\frac{M!}{\prod_{k=1}^K m_k!}.\)

The above describes a prior distribution \(p(\mathbf{Z})\). Also a prior distribution for \(\mathbf{W}\) needs to be specified. This is done by specifying distributions for the elements of \(\mathbf{W}\). Possible choices are, for example, the normal distribution as seen in Figure 2.2 or the Laplace distribution shown in Figure 2.18. Lastly, prior distributions for each of the columns of D need to be defined.

The learning process updates the parameters of these distributions according to the data, and specific instances are sampled. More specifically, D is kept fixed while the distributions of Z and W are updated. After instances of Z and W are sampled, they are kept fixed and the distributions of D are updated. Several passes through the data are necessary.

The process is similar to the Dirichlet process described in Section 6.7. The exact workings are, however, beyond the scope of this book. An introduction and review can be found in [19]. An example in image processing is provided by [11], where the building blocks making up the image are inferred from the image itself in contrast to engineered blocks as shown in Figure 7.1.

## Appendix A: Matrix Formulae

### A.1 Determinants and Inverses

#### A.1.1 Block Matrix Inversion

For an \( m \times m \) invertible, square matrix \( \mathbf{A} \), an \( n \times n \) invertible square matrix \( \mathbf{D} \), an \( m \times n \) matrix \( \mathbf{B} \) and an \( n \times m \) matrix \( \mathbf{C} \), we have

\(\begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{C} & \mathbf{D} \end{pmatrix}^{-1} = \begin{pmatrix} \mathbf{A}^{-1} + \mathbf{A}^{-1}\mathbf{B}\mathbf{E}^{-1}\mathbf{C}\mathbf{A}^{-1} & -\mathbf{A}^{-1}\mathbf{B}\mathbf{E}^{-1} \\ -\mathbf{E}^{-1}\mathbf{C}\mathbf{A}^{-1} & \mathbf{E}^{-1} \end{pmatrix} = \begin{pmatrix} \mathbf{F}^{-1} & -\mathbf{F}^{-1}\mathbf{B}\mathbf{D}^{-1} \\ -\mathbf{D}^{-1}\mathbf{C}\mathbf{F}^{-1} & \mathbf{D}^{-1} + \mathbf{D}^{-1}\mathbf{C}\mathbf{F}^{-1}\mathbf{B}\mathbf{D}^{-1} \end{pmatrix},\)

where \( \mathbf{E} = \mathbf{D} - \mathbf{C}\mathbf{A}^{-1}\mathbf{B} \) and \( \mathbf{F} = \mathbf{A} - \mathbf{B}\mathbf{D}^{-1}\mathbf{C} \) need to be non-singular.

#### A.1.2 Block Matrix Determinant

For matrices as above,

\(\left| \begin{array}{cc} \mathbf{A} & \mathbf{B} \\ \mathbf{C} & \mathbf{D} \end{array} \right| = |\mathbf{A}||\mathbf{D} - \mathbf{C}\mathbf{A}^{-1}\mathbf{B}| = |\mathbf{A} - \mathbf{B}\mathbf{D}^{-1}\mathbf{C}||\mathbf{D}|.\)

#### A.1.3 Woodbury Identity

For an \( m \times m \) invertible, square matrix \( \mathbf{A} \), an \( n \times n \) invertible square matrix \( \mathbf{C} \), an \( m \times n \) matrix \( \mathbf{B} \) and an \( n \times m \) matrix \( \mathbf{D} \), we have

\((\mathbf{A} + \mathbf{B}\mathbf{C}\mathbf{D})^{-1} = \mathbf{A}^{-1} - \mathbf{A}^{-1}\mathbf{B}(\mathbf{C}^{-1} - \mathbf{D}\mathbf{A}^{-1}\mathbf{B})^{-1}\mathbf{D}\mathbf{A}^{-1}.\)

#### A.1.4 Sherman-Morrison Formula

In particular, if \( n = 1 \) in the above Woodbury identity, then \( C = c \) is a scalar and \( \mathbf{B} = \mathbf{b} \) and \( \mathbf{D} = \mathbf{d}^T \) are vectors. The identity becomes

\((\mathbf{A} + c\mathbf{b}\mathbf{d}^T)^{-1} = \mathbf{A}^{-1} - \frac{1}{1/c - \mathbf{d}^T\mathbf{A}^{-1}\mathbf{b}}\mathbf{A}^{-1}\mathbf{b}\mathbf{d}^T\mathbf{A}^{-1},\)

known as the Sherman-Morrison formula. For this to be valid, we need \(1/c - \mathbf{d}^T \mathbf{A}^{-1} \mathbf{b} \neq 0\).

#### A.1.5 Matrix Determinant Lemma

For matrices as in the above Woodbury identity, the determinant can be calculated as

$$|\mathbf{A} + \mathbf{BCD}| = |\mathbf{C}^{-1} - \mathbf{D}\mathbf{A}^{-1}\mathbf{B}||\mathbf{C}||\mathbf{A}|.$$

### A.2 Derivatives

#### A.2.1 Derivative of Squared Norm

Let \(\mathbf{x}\) be a general vector; then the derivative of the squared Euclidean norm is

\(\frac{\partial}{\partial \mathbf{x}} \|\mathbf{x}\|_2^2 = \frac{\partial}{\partial \mathbf{x}} \mathbf{x}^T \mathbf{x} = 2\mathbf{x}\).

#### A.2.2 Derivative of Inner Product

Let \(\mathbf{x}\) be a general vector and \(\mathbf{a}\) a constant vector of the same length; then the derivative of the inner product between them is

\(\frac{\partial}{\partial \mathbf{x}} \mathbf{x}^T \mathbf{a} = \frac{\partial}{\partial \mathbf{a}} \mathbf{x}^T \mathbf{a} = \mathbf{a}\).

#### A.2.3 Derivative of Second Order Vector Product

Let \(\mathbf{x}\) be a general vector of length \(m\) and \(\mathbf{b}\) and \(\mathbf{e}\) constant vectors of length \(n\). Further let \(\mathbf{A}\) and \(\mathbf{D}\) be constant of \(m \times m\) matrices and \(\mathbf{C}\) a constant \(n \times n\) matrix; then

\(\frac{\partial}{\partial \mathbf{x}} (\mathbf{Ax} + \mathbf{b})^T \mathbf{C} (\mathbf{Dx} + \mathbf{e}) = \mathbf{A}^T \mathbf{C} (\mathbf{Dx} + \mathbf{e}) + \mathbf{D}^T \mathbf{C}^T (\mathbf{Ax} + \mathbf{b})\).

#### A.2.4 Derivative of Determinant

Let \(\mathbf{X}\) be a square matrix and let \(|\cdot|\) denote the determinant. Then

\(\frac{\partial}{\partial \mathbf{X}} |\mathbf{X}| = |\mathbf{X}| (\mathbf{X}^{-1})^T\).

Let \(\mathbf{X}\) depend on a variable \(x\), then

\(\frac{\partial}{\partial x} |\mathbf{X}| = |\mathbf{X}| \text{tr} \left( \mathbf{X}^{-1} \frac{\partial \mathbf{X}}{\partial x} \right)\).

where \(\text{tr}(\cdot)\) denotes the trace.

#### A.2.5 Derivative of Matrix Times Vectors

Let \(\mathbf{X}\) be a m x n matrix and \(\mathbf{a}\) and \(\mathbf{b}\) constant vectors of length m and n respectively. Then

$$ \frac{\partial}{\partial X}(\mathbf{a}^T \mathbf{Xb}) = \mathbf{ab}^T. $$

#### A.2.6 Derivative of Transpose Matrix Times Vectors

Let \(\mathbf{X}\) be a m x n matrix and \(\mathbf{a}\) and \(\mathbf{b}\) constant vectors of length n and m respectively. Then

$$ \frac{\partial}{\partial X}(\mathbf{a}^T \mathbf{X}^T \mathbf{b}) = \mathbf{b} \mathbf{a}^T. $$

#### A.2.7 Derivative of Inverse

Let \(\mathbf{X}\) be an invertible matrix, where the entries depend on a variable x. Then

$$ \frac{\partial}{\partial x} \mathbf{X}^{-1} = -\mathbf{X}^{-1} \frac{\partial \mathbf{X}}{\partial x} \mathbf{X}^{-1}. $$

#### A.2.8 Derivative of Inverse Times Vectors

Let \(\mathbf{X}\) be an invertible n x n matrix and \(\mathbf{a}\) and \(\mathbf{b}\) constant vectors of length n, then

$$ \frac{\partial}{\partial X}(\mathbf{a}^T \mathbf{X}^{-1} \mathbf{b}) = -(\mathbf{X}^{-1})^T \mathbf{b} \mathbf{a}^T (\mathbf{X}^{-1})^T. $$

#### A.2.9 Derivative of Trace of Second Order Products

Let \(\mathbf{X}\) be a general m x n matrix, \(\mathbf{A}\), \(\mathbf{B}\) and \(\mathbf{C}\) constant matrices of dimensions k x m, n x n and m x k respectively. Then

$$ \frac{\partial}{\partial X}(\mathbf{A} \mathbf{X} \mathbf{B} \mathbf{X}^T \mathbf{C}) = \mathbf{A}^T \mathbf{C}^T \mathbf{X} \mathbf{B}^T + \mathbf{C} \mathbf{A} \mathbf{X} \mathbf{B}. $$

#### A.2.10 Derivative of Trace of Product with Diagonal Matrix

Let \(\mathbf{A}\) be a constant square matrix and \(\mathbf{X}\) a diagonal matrix of the same dimension. \(\text{tr}(\cdot)\) denotes the trace. Then the derivative of the trace of the product is

$$ \frac{\partial}{\partial X} \text{tr}(\mathbf{AX}) = \text{diag}(\mathbf{A}), $$ 

 where \(\text{diag}(\mathbf{A})\) is a diagonal matrix with the same diagonal as \(\mathbf{A}\).
