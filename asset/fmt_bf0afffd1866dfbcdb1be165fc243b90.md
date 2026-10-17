
It is readily noticeable that these relations are perfectly equivalent with Formulas 7.3 of the first elimination step and could have been obtained from the latter by simply replacing index "1" with "2." Within the second step, one no longer operates on the first line and first column.

We finalize the forward elimination by dividing the third equation by its pivot element $a_{33}^{(2)}$ (which has to be nonzero for a system with nonsingular matrix) and we get

```
\begin{bmatrix} 1 & a_{12}^{(1)} & a_{13}^{(1)} \\ 0 & 1 & a_{23}^{(2)} \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} b_1^{(1)} \\ b_2^{(2)} \\ b_3^{(3)} \end{bmatrix}, \tag{7.7}
```

with

```
b_3^{(3)} = b_3^{(2)}/a_{33}^{(2)}.
```

The backward substitution implies processing in reversed order the rows of the transformed system with triangular matrix 7.7—resulted from the elimination phase—and calculating the solution components by the recursive procedure:

```
\begin{cases}
x_3 = b_3^{(3)} \\
x_2 = b_2^{(2)} - a_{23}^{(2)} x_3 \\
x_1 = b_1^{(1)} - (a_{12}^{(1)} x_2 + a_{13}^{(1)} x_3).
\end{cases}
(7.8)
```

The determination of the solution components proceeds from high to low indexes, each new component solely depending on the previously determined components.

A beneficial feature of the Gaussian elimination is that it also enables the calculation of the determinant of matrix A on the fly. Indeed, since the final matrix of the transformed system A^{(3)} (7.7) is triangular, its determinant amounts to the product of the diagonal elements

```
\det \mathbf{A}^{(3)} = 1.
```

On the other hand, having in view that the divisions of the rows by the pivot elements finally lead to a coefficient matrix having the determinant equal to the one of the initial matrix divided by the product of the successive pivots, there results

```
\det \mathbf{A}^{(3)} = \frac{\det \mathbf{A}}{a_{11}^{(1)} a_{22}^{(2)} a_{33}^{(2)}} = 1,
```

and hence

```
\det \mathbf{A} = a_{11}^{(1)} a_{22}^{(2)} a_{33}^{(2)}.
(7.9)
```

### Generalization to n × n

Let us now generalize the Gaussian elimination for the case of an n × n linear system (with n equations and n unknowns). Written as a matrix equation, the system reads

```
\mathbf{A} \cdot \mathbf{x} = \mathbf{b}, 
(7.10)
```

and features the coefficient matrix A = [a_{ij}]_{nn}, the column vector b = [b_i]_n of the constant terms, and the column vector x = [x_i]_n of the solution components.

As a result of the first k − 1 steps of the forward elimination, zeros have been created below the main diagonal on the first k − 1 columns of the coefficient matrix, and the system has acquired the equivalent form:

```
\begin{bmatrix}
1 & a_{12}^{(1)} & \dots & a_{1k}^{(1)} & a_{1k+1}^{(1)} & \dots & a_{1n}^{(1)} \\
0 & 1 & \dots & a_{2k}^{(2)} & a_{2k+1}^{(2)} & \dots & a_{2n}^{(2)} \\
\vdots & \vdots & \ddots & \vdots & \vdots & & \vdots \\
0 & 0 & \dots & a_{kk}^{(k-1)} & a_{kk+1}^{(k-1)} & \dots & a_{kn}^{(k-1)} \\
0 & 0 & \dots & a_{k+1k}^{(k-1)} & a_{k+1k+1}^{(k-1)} & \dots & a_{k+1n}^{(k-1)} \\
\vdots & \vdots & & \vdots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & a_{nk}^{(k-1)} & a_{nk+1}^{(k-1)} & \dots & a_{nn}^{(k-1)}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_k \\
x_{k+1} \\
\vdots \\
x_n
\end{bmatrix}
=
\begin{bmatrix}
b_1^{(1)} \\
b_2^{(2)} \\
\vdots \\
b_k^{(k-1)} \\
b_{k+1}^{(k-1)} \\
\vdots \\
b_n^{(k-1)}
\end{bmatrix}.
```

Obviously, equations k, k+1, …, n couple only the solution components x_k, x_{k+1}, …, x_n, the rest having been successively eliminated.

第 $k$ 步 ($k = 1,2,\ldots,n-1$) 的目标是从最后 $n-k$ 个方程中消去未知数 $x_k$ 并将系统化为形式：

```
\begin{bmatrix} 1 & a_{12}^{(1)} & \cdots & a_{1k}^{(1)} & a_{1k+1}^{(1)} & \cdots & a_{1n}^{(1)} \\ 0 & 1 & \cdots & a_{2k}^{(2)} & a_{2k+1}^{(2)} & \cdots & a_{2n}^{(2)} \\ \vdots & \vdots & \ddots & \vdots & \vdots & & \vdots \\ 0 & 0 & \cdots & 1 & a_{kk+1}^{(k)} & \cdots & a_{kn}^{(k)} \\ 0 & 0 & \cdots & 0 & a_{k+1k+1}^{(k)} & \cdots & a_{k+1n}^{(k)} \\ \vdots & \vdots & & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 0 & a_{nk+1}^{(k)} & \cdots & a_{nn}^{(k)} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_k \\ x_{k+1} \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} b_1^{(1)} \\ b_2^{(2)} \\ \vdots \\ b_k^{(k)} \\ b_{k+1}^{(k)} \\ \vdots \\ b_n^{(k)} \end{bmatrix}. \tag{7.11}
```

枢轴行 $k$ 的更新系数由下式给出

```
\begin{cases} a_{kk}^{(k)} = 1, \\ a_{kj}^{(k)} = a_{kj}^{(k-1)}/a_{kk}^{(k-1)}, \quad j = k+1,\ldots,n, \\ b_k^{(k)} = b_k^{(k-1)}/a_{kk}^{(k-1)}, \end{cases} \tag{7.12}
```

而枢轴线下方非枢轴行的新元素为：

```
\begin{cases} a_{ik}^{(k)} = 0, \\ a_{ij}^{(k)} = a_{ij}^{(k-1)} - a_{ik}^{(k-1)} a_{kj}^{(k)}, \quad j = k+1,\ldots,n,\ i = k+1,\ldots,n, \\ b_i^{(k)} = b_i^{(k-1)} - a_{ik}^{(k-1)} b_k^{(k)}. \end{cases} \tag{7.13}
```

可以注意到，在第 $k$ 步时，实际上只修改系数矩阵右下部分由行和列 $k$ 限定的元素，与前一步相比，其余元素保持不变。

在最后一次消元步骤 $k = n$ 时，只需将最后一个方程除以最后一个枢轴元素 $a_{nn}^{(n-1)}$ 以在对角线上产生 1：

```
\begin{cases} a_{nn}^{(n)} = 1, \\ b_n^{(n)} = b_n^{(n-1)}/a_{nn}^{(n-1)}. \end{cases} \tag{7.14}
```

最后，系统取形式

```
\begin{bmatrix} 1 & a_{12}^{(1)} & \cdots & a_{1k}^{(1)} & a_{1k+1}^{(1)} & \cdots & a_{1n}^{(1)} \\ 0 & 1 & \cdots & a_{2k}^{(2)} & a_{2k+1}^{(2)} & \cdots & a_{2n}^{(2)} \\ \vdots & \vdots & \ddots & \vdots & \vdots & & \vdots \\ 0 & 0 & \cdots & 1 & a_{kk+1}^{(k)} & \cdots & a_{kn}^{(k)} \\ 0 & 0 & \cdots & 0 & 1 & \cdots & a_{k+1n}^{(k+1)} \\ \vdots & \vdots & & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 0 & 0 & \cdots & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_k \\ x_{k+1} \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} b_1^{(1)} \\ b_2^{(2)} \\ \vdots \\ b_k^{(k)} \\ b_{k+1}^{(k+1)} \\ \vdots \\ b_n^{(n)} \end{bmatrix}, \tag{7.15}
```

随后的 *回代* 基于关系式操作：

```
$$\begin{cases}
 x_{nj}=b_{nj}^{(n)}, & j=1,\ldots,m,\\
 x_{kj}=b_{kj}^{(k)}-\displaystyle\sum_{i=k+1}^{n}a_{ki}^{(k)}x_{ij}, & j=1,\ldots,m,\quad k=n-1,\ldots,1.
\end{cases} \tag{7.22}$$
```

并按列（针对 $m$ 个同时系统中的每一个）以逆序给出解矩阵 **X** 的分量。

考虑到最终矩阵 $A^{(n)}$ 的全部相关信息在消元阶段结束时仅包含在主对角线上方上三角中，在消元步骤 $k$ 时，枢轴行的元素 $a_{kj}^{(k)}$ 以及其下非枢轴行的元素 $a_{ij}^{(k)}$ 在列 $j=k$ 上无需显式求值，因为它们按定义等于 1 或 0 并且无论如何都不会被重用。这意味着在矩阵 $A^{(k)}$ 中只需对列 $j=k+1,\ldots,n$ 进行操作。至于回代，在实现关系式 7.22 时，可以使用单个数组同时存储常数项 $b_{kj}$ 和解的分量 $x_{kj}$。

能够求解对应于任意数量同时线性系统的矩阵方程的算法为处理一个具有重要实际意义的问题提供了可能性——方阵的求逆。事实上，将单位矩阵作为常数项矩阵，

```
$$B=E_n=[\delta_{ij}]_{nn},$$
```

系统 **A · X = B** 的解正是系数矩阵的逆，即 $X=A^{-1}$。这显然是任何求解矩阵方程的算法可用于求逆矩阵的非特异性方式。

特别值得关注的，且不只是为了与其他线性矩阵方程求解器进行比较，是高斯消元所需的浮点运算次数。通过分析方程 7.20 至 7.22，可得到以下运算计数：

- 将系数矩阵 A 变换为上三角形式：
  - 求和与减法（方程 7.21）：

```
$$S_A(n)=\sum_{k=1}^{n}\sum_{j=k+1}^{n}\sum_{i=k+1}^{n}1=\frac{1}{3}n^3-\frac{1}{2}n^2+\frac{1}{6}n,$$
```

  - 乘法与除法（方程 7.20 和 7.21）：

```
$$M_A(n)=\sum_{k=1}^{n}\sum_{j=k+1}^{n}1+\sum_{k=1}^{n}\sum_{j=k+1}^{n}\sum_{i=k+1}^{n}1=\frac{1}{3}n^3-\frac{1}{3}n.$$
```
