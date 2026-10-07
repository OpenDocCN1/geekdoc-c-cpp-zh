# Combinatorial Model Analysis

$(p_i)$ and on the system's probabilities conditioned on $x_i = 1$ and $x_i = 0$. If the system probabilities for these two conditions are known, the system reliability is straightforwardly calculated.

Some examples presented in previous chapters covered the pivoting strategy as an auxiliary method for computing reliability and availability. It is worth looking at the solutions presented for bridge structure in Section 18.5 and the Example 19.3.3.

**Example 20.3.1.** Let us study another system in which factoring helps the system probability. Consider the RBD shown in Figure 20.3. This RBD is more complex than simple series-parallel structures. Particular attention is needed to compound $C_2$ and $C_3$. These two components are bidirectional (see the bridge structure in Section 18.5). Let us first define the structure variables of each component $C_i$ by $x_i$, $i \in \{1, 2, 3, 4, 5, 6\}$.

![](bbox=[0.287, 0.368, 0.712, 0.455])

**Figure 20.3** Non-Series-Parallel RBD.

The RBD shown in Figure 20.3 can be factored into two RBDs by, for instance, first conditioning on the states of $C_2$. If $x_2 = 1$, the RBD depicted in Figure 20.3 is transformed into the RBD shown in Figure 20.4.a. On the other hand, if $x_2 = 0$, the RBD presented in Figure 20.3 is represented by the RBD depicted in Figure 20.4.b. The system structure function can; thus, be be represented

```
$$\Phi(X) = x_2 \times \Phi(1_2,X) + (1 - x_2) \times \Phi(0_2,X)$
```

Therefore

```
$$\Phi(X=1) = p_2 \times \Phi(1_2,X) = 1 + (1 - p_2) \times \Phi(0_2,X) = 1$.
```

The RBD shown in Figure 20.4.a is a simple series-parallel structure.

```
$$\Phi(1_2,X) = 1 = (1 - (1 - p_1)(1 - p_5)) \times (1 - (1 - p_4)) \times (1 - ((1 - (1 - p_3)(1 - p_6)))$.
```

The RBD shown in Figure 20.4.b, components $C_5$ and $C_6$ are in series; the probability of these two components is

```
$$\Phi(x_5,x_6) = 1 = p_5 \times p_6$.
```