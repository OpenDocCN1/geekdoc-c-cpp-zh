# Fitting the Quadric

We begin with a version of the quadric equation that has been normalized by dividing by the constant term:

$ax^2 + by^2 + cz^2 + fyz + gzx + hxy + px + qy + rz + 1 = 0.$ (12.98)

For some particular point $(x_i, y_i, z_i)$ define the vectors:

$\mathbf{x}_i = \begin{bmatrix} x_i^2 \\ y_i^2 \\ z_i^2 \\ y_i z_i \\ z x_i \\ x_i y_i \\ x_i \\ y_i \\ z_i \end{bmatrix} \text{ and } \mathbf{a} = \begin{bmatrix} a \\ b \\ c \\ f \\ g \\ h \\ p \\ q \\ r \end{bmatrix} .$

Construct a matrix $X$ from the set of points $\mathbf{x}$ by making each $\mathbf{x}_i$ a column of $X$. Now, $X$ is a matrix of 9 rows and $n$ columns, where $n$ is the number of points we measure. If each point (each column of $X$) actually lies on the surface defined by $\mathbf{a}$, then

$X^T \mathbf{a} + [\mathbf{1}] = [\mathbf{0}]$ (12.99)

where $[\mathbf{1}]$ and $[\mathbf{0}]$ are $n$-vectors of ones and zeros, respectively.

or

$X^T \mathbf{a} = -[\mathbf{1}].$ (12.100)

Now, we may use the pseudoinverse to find the mean-squared estimate of $\mathbf{a}$

$\hat{\mathbf{a}} = (X X^T)^{-1} X^T [-\mathbf{1}]$ (12.101)

Rewriting Eq. 12.101 to show dimensions, we see

$\hat{\mathbf{a}}_{9 \times 1} = (X_{9 \times n} X_{n \times 9}^T)^{-1}_{9 \times 9} X_{9 \times n} [-\mathbf{1}]_{n \times 1}$ (12.102)

which requires only the solution of a $9 \times 9$ inverse to find the coefficients that describe this quadric. Furthermore this method allows use of an overdetermined system of equations and a minimum squared error solution.

# Determining the Geometry

From range or other surface data, the quadric coefficients may be determined by methods such as those in the previous section. Given the coefficients, the type of quadric may be determined by the following method. (Note that here we define the $yz$, $zx$, and $xy$ terms using an additional coefficient of 2. This is just to make the matrix of Eq. 12.104 work out conveniently. Otherwise, the 2's will not be there.$^{11}$)