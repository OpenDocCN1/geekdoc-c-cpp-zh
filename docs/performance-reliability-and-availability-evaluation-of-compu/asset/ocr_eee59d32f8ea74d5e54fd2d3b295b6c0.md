# Reliability Block Diagram

Now, applying the transformation rules depicted in Table 18.3, we get

```
$$\Phi(X) = x_1 \times (1 - x_2) \times (1 - x_3).\quad (18.3.5)$
```

The structure function may also be obtained by conditioning the RBD in terms of its components. **Conditioning** is also called **factoring, pivoting, or expansion [54]** (see Chapter 20). The structure function $\Phi(X)$ may be re-written by

```
$$\Phi(X) = x_i \times \Phi(1_i, X) + (1 - x_i) \times \Phi(0, X),\quad (18.3.6)$
```

where $\Phi(1_i, X)$ represents a state in which component $c_i$ is operational and the states of the other components are random variables $\Phi(x_1, x_2, ..., l_i, ..., x_n)$. Unlike, $\Phi(0_i, X)$ denotes a state in which $c_i$ has failed and the states of the other components are random variables $\Phi(x_1, x_2, ..., 0_i, ..., x_n)$. Factoring the structure function is a very useful strategy when modeling complex systems, with its repeated application one can eventually reach a substructure whose function is simpler to deal with.

Now, let us apply such a strategy to the RBD depicted in Figure 18.1. First, let us conditioning on the component $b_1$. Hence, we get

```
$$\Phi(x_1, x_2, x_3) = x_1 \Phi(1, x_2, x_3) + (1 - x_1) \Phi(0, x_2, x_3).$$
```

$\Phi(0, x_2, x_3) = 0$, we have

```
$$\Phi(x_1, x_2, x_3) = x_1 \Phi(1, x_2, x_3).$$
```

Now, conditioning $\Phi(1, x_2, x_3)$ on component $b_2$, we obtain

```
$$\Phi(1, x_2, x_3) = x_2 \Phi(1, 1, x_3) + (1 - x_2) \Phi(1, 0, x_3).$$
```

$\Phi(1, 1, x_3) = 1$, then

```
$$\Phi(1, x_2, x_3) = x_2 + (1 - x_2) \Phi(1, 0, x_3).$$
```

Therefore

```
$$\Phi(x_1, x_2, x_3) = x_1 (x_2 + (1 - x_2) \Phi(1, 0, x_3)).$$
```

Now, let us conditioning $\Phi(1, 0, x_3)$ on component $b_3$. Hence

```
$$\Phi(1, 0, x_3) = x_3 \Phi(1, 0, 1) + (1 - x_3) \Phi(1, 0, 0).$$
```