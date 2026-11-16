We can find the null space by multiplying $A$ by the unknown vector $\mathbf{x} = [x_1 \ x_2 \ x_3]^T$ and setting the result to zero.

```
$$
\begin{bmatrix} 1 & 5/4 & 3/2 \\ 0 & 1 & 2 \\ 0 & 0 & 0 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}.
$$
```

Setting the product to zero yields the following equations

```
$x_1 + \frac{5}{4}x_2 + \frac{3}{2}x_3 = 0$ (3.8)

$x_2 + 2x_3 = 0.$ (3.9)
```

That simplifies to

```
$x_1 = x_3$ (3.10)

$x_2 = -2x_3.$ (3.11)
```

Let $x_3 = 1$, and the null vector is $[1 \ -2 \ 1]^T$. Since the rank is 2, the null space consists of this one vector and all scalar multiples of it. Division of $[1 \ -2 \ 1]^T$ by its magnitude, $\sqrt{6}$, produces a unit vector; $[0.4082 \ -0.8165 \ 0.4082]^T$.

# Right and Left Null Space

Above, we solved the problem

```
$A\mathbf{x} = \mathbf{0}.$
```

Instead, however, we might have been confronted with the following problem

```
$\mathbf{x}A = \mathbf{0},$
```

which is referred to as finding the left null space. The left null space of a matrix, $A$ is simply the null space of $A^T$.

# 3.2.4 Function Spaces

Think about a function, say $f(x) = x^2$, defined on the integers greater than zero and less than six. You could list the values of $f(x)$ as an ordered set: [1, 4, 9, 16, 25], which looks exactly like a vector. So it is perfectly fine to think of a function as a vector. Of course, there is one slight problem. If we define our function on the real numbers, we end up with a vector with infinite dimensionality. But, except for the fact that we cannot list all the elements, infinite dimensionality is not a problem.

The concept of orthogonality can easily be extended to continuous functions by simply thinking of a function as an infinite-dimensional vector. Just list all the values of $f(x)$ as $x$ varies between, say, $a$ and $b$. If $x$ is continuous, then there are an infinite number of possible values of $x$ between $a$ and $b$. But that should not stop us – we cannot enumerate them, but we can still think of a vector containing all the values of $f(x)$. Now, the concept of summation that we defined for finite-dimensional vectors turns into integration, and an inner product may be written

```
$<f(x), g(x)> = \int_a^b f(x)g(x)dx.$ (3.12)
```