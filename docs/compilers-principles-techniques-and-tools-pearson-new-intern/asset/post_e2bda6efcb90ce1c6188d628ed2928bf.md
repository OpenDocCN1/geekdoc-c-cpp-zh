
- 4. Write access $Y[i, j]$ and itself in statement $s_2$,
- 5. Write access $Y[i, j]$ with read access $Y[i, j]$ in statement $s_2$,
- 6. Write access $Y[i, j]$ in statement $s_2$ with read access $Y[i-1, j]$ in statement $s_1$.

We see that the dependence tests are all simple and highly repetitive. The only dependences present in this code occur in case (3) between instances of accesses $X[i, j]$ and $X[i, j-1]$ and in case (6) between $Y[i, j]$ and $Y[i-1, j]$.

The space-partition constraints imposed by the data dependence between $X[i, j]$ in statement $s_1$ and $X[i, j-1]$ in statement $s_2$ can be expressed in the following terms:

For all $(i, j)$ and $(i', j')$ such that

$$
\begin{aligned}
1 \le i \le 100 &\quad 1 \le j \le 100\\
1 \le i' \le 100 &\quad 1 \le j' \le 100\\
i = i' &\quad j = j' - 1
\end{aligned}
$$

we have

$$
\begin{bmatrix} C_{11} & C_{12} \end{bmatrix}\begin{bmatrix} i \\ j \end{bmatrix} + \begin{bmatrix} c_1 \end{bmatrix} = \begin{bmatrix} C_{21} & C_{22} \end{bmatrix}\begin{bmatrix} i' \\ j' \end{bmatrix} + \begin{bmatrix} c_2 \end{bmatrix}
$$

That is, the first four conditions say that $(i, j)$ and $(i', j')$ lie within the iteration space of the loop nest, and the last two conditions say that the dynamic accesses $X[i, j]$ and $X[i, j-1]$ touch the same array element. We can derive the space-partition constraint for accesses $Y[i-1, j]$ in statement $s_2$ and $Y[i, j]$ in statement $s_1$ in a similar manner. $\square$

### 11.7.4 Solving Space-Partition Constraints

Once the space-partition constraints have been extracted, standard linear algebra techniques can be used to find the affine partitions satisfying the constraints. Let us first show how we find the solution to Example 11.41.

**Example 11.42:** We can find the affine partitions for Example 11.41 with the following steps:

- 1. Create the space-partition constraints shown in Example 11.41. We use the loop bounds in determining the data dependences, but they are not used in the rest of the algorithm otherwise.
- 2. The unknown variables in the equalities are $i, i', j, j', C_{11}, C_{12}, c_1, C_{21}, C_{22}$, and $c_2$. Reduce the number of unknowns by using the equalities due to the access functions: $i = i'$ and $j = j' - 1$. We do so using Gaussian elimination, which reduces the four variables to two: say $t_1 = i = i'$, and $t_2 = j = j' - 1$. The equality for the partition becomes

$$
\begin{bmatrix} C_{11} - C_{21} & C_{12} - C_{22} \end{bmatrix}\begin{bmatrix} t_1 \\ t_2 \end{bmatrix} + \begin{bmatrix} c_1 - c_2 - C_{22} \end{bmatrix} = 0
$$

- 3. The equation above holds for all combinations of $t_1$ and $t_2$. Thus, it must be that

$$
\begin{aligned}
C_{11}-C_{21} &= 0 \\
C_{12}-C_{22} &= 0 \\
c_1-c_2-C_{22} &= 0
\end{aligned}
$$

If we perform the same steps on the constraint between the accesses $Y[i-1,j]$ and $Y[i,j]$, we get

$$
\begin{aligned}
C_{11}-C_{21} &= 0 \\
C_{12}-C_{22} &= 0 \\
c_1-c_2+C_{21} &= 0
\end{aligned}
$$

Simplifying all the constraints together, we obtain the following relationships:

$$
C_{11}=C_{21}=-C_{22}=-C_{12}=c_2-c_1.
$$

- 4. Find all the independent solutions to the equations involving only unknowns in the coefficient matrix, ignoring the unknowns in the constant vectors in this step. There is only one independent choice in the coefficient matrix, so the affine partitions we seek can have at most a rank of one. We keep the partition as simple as possible by setting $C_{11}=1$. We cannot assign 0 to $C_{11}$ because that will create a rank-0 coefficient matrix, which maps all iterations to the same processor. It then follows that $C_{21}=1$, $C_{22}=-1$, $C_{12}=-1$.
- 5. Find the constant terms. We know that the difference between the constant terms, $c_2-c_1$, must be $-1$. We get to pick the actual values, however. To keep the partitions simple, we pick $c_2=0$; thus $c_1=-1$.

Let $p$ be the ID of the processor executing iteration $(i,j)$. In terms of $p$, the affine partition is

$$
s_1:[p]=[\,1\ -1\,]\begin{bmatrix}i\\j\end{bmatrix}+[-1]
$$

$$
s_2:[p]=[\,1\ -1\,]\begin{bmatrix}i\\j\end{bmatrix}+[0]
$$

That is, the $(i,j)$th iteration of $s_1$ is assigned to the processor $p=i-j-1$, and the $(i,j)$th iteration of $s_2$ is assigned to the processor $p=i-j$. $\square$

**Algorithm 11.43:** Finding a highest-ranked synchronization-free affine partition for a program.

**INPUT:** A program with affine array accesses.

**OUTPUT:** A partition.

**METHOD:** Do the following:

- 1. Find all data-dependent pairs of accesses in a program. For each pair of data-dependent accesses, $\mathcal{F}_1 = (\mathbf{F}_1, \mathbf{f}_1, \mathbf{B}_1, \mathbf{b}_1)$ in statement $s_1$ nested in $d_1$ loops and $\mathcal{F}_2 = (\mathbf{F}_2, \mathbf{f}_2, \mathbf{B}_2, \mathbf{b}_2)$ in statement $s_2$ nested in $d_2$ loops. Let $(\mathbf{C}_1, \mathbf{c}_1)$ and $(\mathbf{C}_2, \mathbf{c}_2)$ represent the (currently unknown) partitions of statements $s_1$ and $s_2$, respectively. The space-partition constraints state that if

$$
\mathbf{F}_1 \mathbf{i}_1 + \mathbf{f}_1 = \mathbf{F}_2 \mathbf{i}_2 + \mathbf{f}_2
$$

then

$$
\mathbf{C}_1 \mathbf{i}_1 + \mathbf{c}_1 = \mathbf{C}_2 \mathbf{i}_2 + \mathbf{c}_2
$$

for all $\mathbf{i}_1$ and $\mathbf{i}_2$, within their respective loop bounds. We shall generalize the domain of iterations to include all $\mathbf{i}_1$ in $Z^{d_1}$ and $\mathbf{i}_2$ in $Z^{d_2}$; that is, the bounds are all assumed to be minus infinity to infinity. This assumption makes sense, since an affine partition cannot make use of the fact that an index variable can take on only a limited set of integer values.

- 2. For each pair of dependent accesses, we reduce the number of unknowns in the index vectors.

  - (a) Note that $\mathbf{F}\mathbf{i} + \mathbf{f}$ is the same vector as

$$
\left[ \begin{array}{cc} \mathbf{F} & \mathbf{f} \end{array} \right] \left[ \begin{array}{c} \mathbf{i} \\ 1 \end{array} \right]
$$

That is, by adding an extra component 1 at the bottom of column-vector $\mathbf{i}$, we can make the column-vector $\mathbf{f}$ be an additional, last column of the matrix $\mathbf{F}$. We may thus rewrite the equality of the access functions $\mathbf{F}_1 \mathbf{i}_1 + \mathbf{f}_1 = \mathbf{F}_2 \mathbf{i}_2 + \mathbf{f}_2$ as

$$
\left[ \begin{array}{ccc} \mathbf{F}_1 & -\mathbf{F}_2 & (\mathbf{f}_1 - \mathbf{f}_2) \end{array} \right] \left[ \begin{array}{c} \mathbf{i}_1 \\ \mathbf{i}_2 \\ 1 \end{array} \right] = 0
$$

  - (b) The above equations will in general have more than one solution. However, we may still use Gaussian elimination to solve the equations for the components of $\mathbf{i}_1$ and $\mathbf{i}_2$ as best we can. That is, eliminate as many variables as possible until we are left with only variables that cannot be eliminated. The resulting solution for $\mathbf{i}_1$ and $\mathbf{i}_2$ will have the form

$$
\left[ \begin{array}{c} \mathbf{i}_1 \\ \mathbf{i}_2 \\ 1 \end{array} \right] = \mathbf{U} \left[ \begin{array}{c} \mathbf{t} \\ 1 \end{array} \right]
$$

where $\mathbf{U}$ is an upper-triangular matrix and $\mathbf{t}$ is a vector of free variables ranging over all integers.

  - (c) We may use the same trick as in Step (2a) to rewrite the equality of the partitions. Substituting the vectors $(\mathbf{i}_1, \mathbf{i}_2, 1)$ with the result from Step (2b), we can write the constraints on the partitions as

$$
[\ \mathbf{C}_1\quad -\mathbf{C}_2\quad (\mathbf{c}_1-\mathbf{c}_2)\ ]\,\mathbf{U}\begin{bmatrix}\mathbf{t}\\1\end{bmatrix}=0
$$

- 3. Drop the nonpartition variables. The equations above hold for all combinations of $\mathbf{t}$ if

$$
[\ \mathbf{C}_1\quad -\mathbf{C}_2\quad (\mathbf{c}_1-\mathbf{c}_2)\ ]\,\mathbf{U}=0.
$$

Rewrite these equations in the form $Ax=0$, where $x$ is a vector of all the unknown coefficients of the affine partitions.

- 4. Find the rank of the affine partition and solve for the coefficient matrices. Since the rank of an affine partition is independent of the value of the constant terms in the partition, we eliminate all the unknowns that come from the constant vectors like $c_1$ or $c_2$, thus replacing $Ax=0$ by simplified constraints $A'x'=0$. Find the solutions to $A'x'=0$, expressing them as $B$, a set of vectors spanning the null space of $A'$.
- 5. Find the constant terms. Derive one row of the desired affine partition from each basis vector in $B$, and derive the constant terms using $Ax=0$.

Note that Step 3 ignores the constraints imposed by the loop bounds on variables $\mathbf{t}$. The constraints are only stricter as a result, and the algorithm must therefore be safe. That is, we place constraints on the $\mathbf{C}$'s and $\mathbf{c}$'s assuming $\mathbf{t}$ is arbitrary. Conceivably, there would be other solutions for the $\mathbf{C}$'s and $\mathbf{c}$'s that are valid only because some values of $\mathbf{t}$ are impossible. Not searching for these other solutions may cause us to miss an optimization, but cannot cause the program to be changed to a program that does something different from what the original program does.

### 11.7.5 A Simple Code-Generation Algorithm

Algorithm 11.43 generates affine partitions that split computations into independent partitions. Partitions can be assigned arbitrarily to different processors, since they are independent of one another. A processor may be assigned more than one partition and can interleave the execution of its partitions, as long as operations within each partition, which normally have data dependences, are executed sequentially.
