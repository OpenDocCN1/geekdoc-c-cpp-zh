![](bbox=[0.19, 0.11, 0.75, 0.27])

Figure 12.5 Top view of two cameras. The camera on the right is rotated by -20 degrees about the positive y axis (which goes into the paper). The point where the ray intersects the focal plane is x = -4.6 on the right camera and x = 10 on the left camera.

In the following, for notational convenience, sin θ and cos θ are replaced by s and c, respectively.

Now we need to concatenate the identity matrix with the vector to the origin, as before, and premultiply by K:

```
P_2 = \begin{bmatrix} 10 & 0 & 0 \\ 0 & 10 & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} c & 0 & -s \\ 0 & 1 & 0 \\ s & 0 & c \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 & -100 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{bmatrix} \quad (12.18)
```

then

```
P_2 = \begin{bmatrix} 10 & 0 & 0 \\ 0 & 10 & 0 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} c & 0 & -s & -100c \\ 0 & 1 & 0 & 0 \\ s & 0 & c & -100s \end{bmatrix} .
```

```
P_2 = \begin{bmatrix} 10c & 0 & -10s & -1000c \\ 0 & 10 & 0 & 0 \\ s & 0 & c & -100s \end{bmatrix}
```

Multiplying this matrix by the point X that we have used before, we find

```
\mathbf{x} = \begin{bmatrix} 10c & 0 & -10s & -1000c \\ 0 & 10 & 0 & 0 \\ s & 0 & c & -100s \end{bmatrix} \begin{bmatrix} 50 \\ 0 \\ 50 \\ 1 \end{bmatrix}
```

```
= \begin{bmatrix} 500c - 500s - 1000c \\ 0 \\ 50s + 50c - 100s \end{bmatrix} = \begin{bmatrix} -500(s + c) \\ 0 \\ 50(c - s) \end{bmatrix} .
```

Now, take a look at Figure 12.5.