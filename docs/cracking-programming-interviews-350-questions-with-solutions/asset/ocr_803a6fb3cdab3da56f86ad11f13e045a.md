# ### 1.1. Approximating the square root of a number

of the loop body. It is assigned a value upon entrance to the loop body, and this value is used throughout the body. It carries no value from iteration to iteration. Moreover, d is used only in two adjacent lines, and its use is obvious from these two lines. A definition of d would belabor the obvious and is therefore omitted.

If the difference $b-a$ is always even, then $d$ can be calculated using

$$d \leftarrow a + \frac{b-a}{2}$$

Therefore, let us attempt to deal with the difference, say $c$, between $b$ and $a$ and to keep this difference even. This will be easiest if $c$ is always a power of 2. Thus we have:

$$b = a + c$$
$$d = a + c/2$$
$$p : 1 \leq p : c = 2^p \quad\Longleftrightarrow\quad c\text{ is even.}$$

Because $b$ and $d$ are defined in terms of $a$ and $c$, we may be able to write the program using only $a$ and $c$. Thus, we try the loop invariant and bound function

$$P : a^2 \leq n < (a+c)^2 \land (p : 1 \leq p : c = 2^p)$$
$$t : c+1$$

The initialization will require a loop to establish $P$, since $c$ must be a power of 2. The rest of the program is derived from the previous program, essentially by deleting the assignments to $b$ and $d$ and transforming the other commands into commands involving $c$:

```
Algorithm 1  Computing Square Root Program

1:  a \leftarrow 0
2:  c \leftarrow 1
3:  while $c^2 \leq n$ do
4:      c \leftarrow 2 \times c
5:  end while                                      ▷ $P$
6:  while $c \neq 1$ do
7:      c \leftarrow c/2
8:      if $(a+c)^2 \leq n$ then
9:          a \leftarrow a+c
10:     else if $(a+c)^2 > n$ then
11:         skip
12:     end if
13: end while                                      ▷ $a^2 \leq n < (a+1)^2$
```