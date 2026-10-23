The final four equations are obtained from evaluating the normal derivative at the side midpoints. The next equation is obtained from the normal derivative (the z-partial derivative) at the side midpoint (1/3,1/3,0):

```
B_{52,\hat{j},i,j,k} \equiv \begin{cases} 3^{j-k} & \text{if } i=1, \\ 0 & \text{otherwise.} \end{cases}
```

Similarly, the next equation is obtained from the normal derivative (the y-partial derivative) at the side midpoint (1/3,0,1/3):

```
B_{53,\hat{j},i,j,k} \equiv \begin{cases} 3^{i-k} & \text{if } j=1, \\ 0 & \text{otherwise.} \end{cases}
```

Similarly, the next equation is obtained from the normal derivative (the x-partial derivative) at the side midpoint (0,1/3,1/3):

```
B_{54,\hat{j},i,j,k} \equiv \begin{cases} 3^{i-j} & \text{if } k=1, \\ 0 & \text{otherwise.} \end{cases}
```

The final equation is obtained from the normal derivative (the sum of the x-, y-, and z-partial derivatives, divided by √3) at the side midpoint (1/3,1/3,1/3):

```
B_{55,\hat{j},i,j,k} \equiv (i + j + k) 3^{-i-j-k+1} / \sqrt{3}.
```

This completes the definition of the matrix B.

In order to solve the above linear system for the unknown vector \tilde{x}, one can use three possible approaches. The direct approach is to calculate the inverse matrix B^{-1} explicitly (as in Section 3.20) to obtain \tilde{x} as the qth column in B^{-1}. A more indirect approach is to solve the original linear system iteratively by a Krylov-subspace method, such as GMRES [62]. Finally, one may also multiply the original linear system by the transpose matrix B^t to obtain the so-called normal equations

```
B^t B \tilde{x} = B^t I^{(q)} ,
```

which can be solved by preconditioned conjugate gradients [56].

# 28.3 Functions in the Mesh

Consider now a tetrahedron t in the three-dimensional mesh M, with vertices (or corners) denoted by \vec{k}, \vec{l}, \vec{m}, and \vec{n} in the three-dimensional Cartesian space. In this case, we write

```
t = (\vec{k}, \vec{l}, \vec{m}, \vec{n}),
```

where the order of vertices in this notation is determined arbitrarily in advance.

A function in t has 56 degrees of freedom: its value and the values of its first and second partial derivatives at the four corners, its two normal derivatives at the six edge midpoints, and its normal derivatives at the four side midpoints. The values of these degrees of freedom determine the function uniquely. In a basis function in t, for example, only one of these degrees of freedom has a nonzero value: the value 1.