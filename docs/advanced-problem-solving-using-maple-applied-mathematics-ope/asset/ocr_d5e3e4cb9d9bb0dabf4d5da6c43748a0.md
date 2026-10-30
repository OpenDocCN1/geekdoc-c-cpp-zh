To calculate the efficiency of $DMU_3$, use the linear program

```
$$\begin{aligned}
\text{Maximize } DMU_3 &= 4t_1+9t_2+13t_3\\
\text{subject to}\quad
-9t_1-4t_2-16t_3+5w_1+14w_2 &\ge 0,\\
-5t_1-7t_2-10t_3+8w_1+15w_2 &\ge 0,\\
-4t_1-9t_2-13t_3+7w_1+12w_2 &\ge 0,\\
7w_1+12w_2 &=1,\\
t_i,w_j&\ge 0\quad\text{for all }i,j.
\end{aligned}$$
```

Use Maple to solve the three linear programs.

```
> with(Optimization):
```

Define the input and output data matrices. Using the *Matrix Palette* makes entry easier and less error prone. Set the size, then click *Insert Matrix*.

```
> Inputs := \begin{bmatrix}5&14\\8&15\\7&12\end{bmatrix}: \\
  Outputs := \begin{bmatrix}9&4&16\\5&7&10\\4&9&13\end{bmatrix}:
```

Define the decision variables and weights.

```
> T := {t_i$i = 1..3}: \\
> W := {w_i$i = 1..2}:
```

Compute the LP’s objective functions.

```
> DMUObj := Outputs . T; \\
\begin{bmatrix}9t_1+4t_2+16t_3\\5t_1+7t_2+10t_3\\4t_1+9t_2+13t_3\end{bmatrix}
```

Set up the constraints.

```
> Inputs . W - Outputs . T >=~ 0;  # ‘>=~ 0’ applies ‘>= 0’ element-wise.\\
  MainConstraints := convert(%, set):\\
  \left\{\begin{aligned}
  0 &\le 5w_1+14w_2-9t_1-4t_2-16t_3\\
  0 &\le 8w_1+15w_2-5t_1-7t_2-10t_3\\
  0 &\le 7w_1+12w_2-4t_1-9t_2-13t_3
  \end{aligned}\right.
```