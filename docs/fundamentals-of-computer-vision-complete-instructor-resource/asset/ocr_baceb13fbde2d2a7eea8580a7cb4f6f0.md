must therefore deal with arithmetic operations involving numbers ranging over three orders of magnitude. In solving such a system, double precision is likely to be required, and the resulting numbers may still be huge. (Consider computing a determinant of a \(20 \times 20\) matrix of numbers between 0 and 1000. Intermediate results involving numbers on the order of \(1000^{20}\) would not be impossible). The following normalization [12.28] provides significant improvement:

+   - Move the origin of the coordinate system to the center of the image.
+   - Scale the coordinates so that the average distance of a point to the origin is \(\sqrt{2}\).

This technique can be critically important. It is sometimes referred to as *preconditioning* the data.

There are many variations of the 8-point algorithm. In this section, we describe a simple version, so that the student may grasp the basic principles. Of course, this won’t be the absolute best version, but we will also provide pointers to the literature for the student who needs to implement these concepts in robust software.

Start by rewriting Eq. 12.20:

```
\([x_i \ y_i \ 1] \begin{bmatrix} f_{11} & f_{12} & f_{13} \\ f_{21} & f_{22} & f_{23} \\ f_{31} & f_{32} & f_{33} \end{bmatrix} \begin{bmatrix} x_r \\ y_r \\ 1 \end{bmatrix} .\)
```

Multiplying the matrices out, we get

```
\(x_i x_r f_{11} + y_i x_r f_{21} + x_r f_{31} + x_i y_r f_{12} + y_i y_r f_{22} + y_r f_{32} + x_i f_{13} + y_i f_{23} + f_{33} = 0,\)
```

which we can reformulate by defining

```
\(\mathbf{a} = [x_i x_r, y_i x_r, x_r, x_i y_r, y_i y_r, y_r, x_i, y_i, 1]^T\)
```

and

```
\(\mathbf{f} = [f_{11} f_{21} f_{31} f_{12} f_{22} f_{32} f_{13} f_{23} f_{33}]^T\)
```

which converts Eq. 12.24 into

```
\(\mathbf{a}^T \mathbf{f} = 0.\)
```

Equation 12.24, rewritten into Eq. 12.28, only represents a single correspondence. If we have some number of such equations, we can stack them as shown below

```
\(\mathbf{a}_1^T \mathbf{f} = 0\)
\(\mathbf{a}_2^T \mathbf{f} = 0\)
\(\dots\)
\(\mathbf{a}_n^T \mathbf{f} = 0\)
```

and rewrite this system with a single matrix equation:

```
\(A \mathbf{f} = \mathbf{0}.\)
```