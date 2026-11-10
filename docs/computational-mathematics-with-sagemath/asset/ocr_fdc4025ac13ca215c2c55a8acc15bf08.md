![](bbox=[0.305, 0.08, 0.693, 0.25])

Figure 4.8 ~ Random walk.

+   - $u_n = [n\ln(n)]\sqrt{2}$ and $N = 10000$, 
+   - $u_n = p_n\sqrt{2}$ and $N = 10000$ (here $p_n$ is the $n$-th prime).

Figure 4.9 is obtained as follows (here for $u_n = n\sqrt{2}$):

```
sage: length = 200; n = var('n')
sage: u = lambda n: n * sqrt(2)
sage: z = lambda n: exp(2 * I * pi * u(n)).n()
sage: vertices = [CC(0, 0)]
sage: for n in range(1, length):
....:     vertices.append(vertices[n - 1] + CC(z(n)))
sage: line(vertices).show(aspect_ratio=1)
```

We see that the curve 4.9a is amazingly regular, which suggests that the uniform distribution of $n\sqrt{2}$ modulo 1 is deterministic. In the case of $u_n = n\ln(n)\sqrt{2}$, the values apparently seem random modulo 1. However, the associated curve 4.9b is remarkably well structured. The curve 4.9c has the same kind of structure as the second one. Finally, the curve 4.9d shows the completely different nature of primes modulo $1/\sqrt{2}$: the spirals have disappeared and the aspect looks very similar to a random walk $u_n$ (Figure 4.8). It thus looks as though “prime numbers make use of all the randomness they are given...”

For a detailed interpretation of these curves, we refer the reader to the book (in French) *Les nombres premiers* of Gérald Tenenbaum and Michel Mendès France [TMF00].

**Exercise 13** (Drawing terms of a recurrent sequence). We consider the sequence $(u_n)_{n\in\mathbb{N}}$ defined by:

$$u_0 = a, \qquad \forall n \in \mathbb{N},\; u_{n+1} = \left|u_n^2 - \frac{1}{4}\right|.$$

Represent graphically the behaviour of the sequence by constructing a list of points $[(u_0, 0), (u_0, u_1), (u_1, u_1), (u_1, u_2), (u_2, u_2), \ldots]$, with $a \in \{-0.4, 1.1, 1.3\}$.

# 4.1.6  Displaying Solutions of Differential Equations

We can combine the above commands to represent solutions of differential equations or systems. To solve symbolically an ordinary differential equation, one calls