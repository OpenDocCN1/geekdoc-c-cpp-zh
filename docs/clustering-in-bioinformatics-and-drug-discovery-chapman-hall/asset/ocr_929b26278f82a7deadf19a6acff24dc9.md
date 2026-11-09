# # Chapter 12

# ## Appendices

The following appendices are meant in large part as a review of mathematical topics that the reader should have at least a passing understanding if not a deep grounding in. They are also slanted to the usage of those topics in cluster analysis. Some of the most basic elements are assumed.

# ### 12.1 Primer on Matrix Algebra

A great deal of the mathematics of statistics is in the form of linear algebra, where the manipulation of matrices and vectors is commonplace. Statistical learning theory and in particular regression theory contain many formulas and derivations in the form of vectors and matrices. Cluster analysis is often concerned with pattern and (dis)similarity matrices, their properties, relationships, and transformations. An additional important concern is the how vector and matrix data are represented in a computer and how machine operations on these data impacts results, given finite precision. This latter concern is the domain of numerical analysis, which is replete with numerical algorithms for operating on vectors and matrices and arrive at results of a given precision and error.

By convention an $n$-dimensional vector is displayed vertically:

$$\mathbf{x}=\begin{pmatrix}x_1\\x_2\\\vdots\\x_n\end{pmatrix}$$

Its transpose is laid out horizontally:

$$\mathbf{x}^{T}=(x_1,x_2,\ldots,x_n) \qquad (12.1)$$

This convention follows vector-vector and vector-matrix operation conventions. The inner product or dot product of two vectors of equal length, the sum of the corresponding pair-wise entries of each vector, thereby equals a scalar