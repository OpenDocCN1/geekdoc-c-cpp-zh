the interpolation mesh points:

```
A_i = (\tilde{D}_{i+1} - \tilde{D}_i)/(6 h_i)
B_i = (\tilde{D}_i x_{i+1} - \tilde{D}_{i+1} x_i)/(2 h_i)
C_i = (\tilde{D}_{i+1} x_i^2 - \tilde{D}_i x_{i+1}^2)/(2 h_i) + (y_{i+1} - y_i)/h_i - A_i h_i^2
D_i = (\tilde{D}_i x_{i+1}^3 - \tilde{D}_{i+1} x_i^3)/(6 h_i) + (y_i x_{i+1} - y_{i+1} x_i)/h_i - (B_i h_i^2)/3.
```

For the complete definition of the splines, one still needs to determine the values \tilde{D}_i of the second derivatives and this can be done by imposing the continuity of the first derivative at the interpolation nodes:

```
S'_{i-1}(x_i) = S'_i(x_i), \quad i = 2,3,...,n-1. \tag{9.35}
```

Using the Expression 9.30 of the first derivative and the form (9.32) of the coefficients C'_i, the above continuity conditions result in

```
(h_{i-1}/6)\tilde{D}_{i-1} + ((h_{i-1}+h_i)/3)\tilde{D}_i + (h_i/6)\tilde{D}_{i+1} = (y_{i+1}-y_i)/h_i - (y_i - y_{i-1})/h_{i-1}, \quad i = 2,3,...,n-1. \tag{9.36}
```

The System 9.36 comprises only (n - 2) equations for the n second derivatives \tilde{D}_i and, consequently, for their unequivocal determination, two additional equations need to be supplied. These supplementary equations can be explicitly derived for two important types of boundaries associated with the spline interpolants: free or natural boundaries and clamped boundaries.

The clamped boundaries require the first derivatives at the end points, y'_1 and y'_n, to be specified and, correspondingly, the two additional relations are

```
S'_1(x_1) = y'_1, \quad S'_{n-1}(x_n) = y'_n,
```

or, explicitly,

```
(h_1/3)\tilde{D}_1 + (h_1/6)\tilde{D}_2 = (y_2 - y_1)/h_1 - y'_1
(h_{n-1}/6)\tilde{D}_{n-1} + (h_{n-1}/3)\tilde{D}_n = y'_n - (y_n - y_{n-1})/h_{n-1}.
```

Therewith, the following tridiagonal system results, having as solution the second derivatives \tilde{D}_i of the splines at the interpolation nodes:

```
b_1 \tilde{D}_1 + c_1 \tilde{D}_2 = d_1
a_i \tilde{D}_{i-1} + b_i \tilde{D}_i + c_i \tilde{D}_{i+1} = d_i, \quad i = 2,3,...,n-1
a_n \tilde{D}_{n-1} + b_n \tilde{D}_n = d_n. \tag{9.37}
```