# 528 Multidimensional Arrays

```
$L = \begin{bmatrix} x_1 & x_2 \ y_1 & y_2 \ 1 & 1 \end{bmatrix}$
```

Multiply the translation matrix and the coordinate matrix.

```
$L' = R(\theta) * L$
```

```
$$\begin{bmatrix} x'_1 & x'_2 \ y'_1 & y'_2 \ 1 & 1 \end{bmatrix} = \begin{bmatrix} \cos\theta & -sin\theta & 0 \ \sin\theta & \cos\theta & 0 \ 0 & 0 & 1 \end{bmatrix} * \begin{bmatrix} x_1 & x_2 \ y_1 & y_2 \end{bmatrix}$
```

Data

Transformation matrix:

```
$R(\theta) = \begin{bmatrix} \cos\theta & -sin\theta & 0 \ \sin\theta & \cos\theta & 0 \ 0 & 0 & 1 \end{bmatrix}$
```

Coordinate matrix:

```
$L = \begin{bmatrix} x_1 & x_2 \ y_1 & y_2 \ 1 & 1 \end{bmatrix}$
```

Pseudocode

```
main:
  funcrotate
  funcinput
  funcmultiply
  funcoutput
stop
```

funcrotate:

  input the rotation angle and set up the rotation matrix

end