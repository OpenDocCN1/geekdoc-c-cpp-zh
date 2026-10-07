# Combinatorial Model Analysis

# 20.7.5 DECOMPOSITION

The reliability/availability evaluation of a large system is usually performed by decomposing the system into a subsystem. Each subsystem is decomposed into a smaller subsystem. This process stops when the analyst decides the subsystem is simple enough to be evaluated. Then, the smaller subsystems are evaluated and considered one component (reduction) in the higher-level subsystem. As already presented in Section 20.4, such an approach can be applied to obtain exact results or bounds.

To calculate bounds, after decomposing the system into smaller subsystems, the subsystems can be evaluated using any of those methods already introduced here to calculate bounds, and then reducing each subsystem and representing them as one component with the respective bounds obtained at the higher-level.

Consider a system represented by the RBD depicted in Figure 20.13.a. This model is composed of twenty-one blocks, $\{b_i\}, i \in \{1, 2, \dots, 21\}$. This model was decomposed into three subsystems, $S_1, S_2$ and $S_3$, as shown in Figure 20.13. The subsystem $S_1$ has three minimal path and four minimal cuts. The minimal paths are

```
$MP_1^1 \Rightarrow b_1 \wedge b_2$,
```

```
$MP_2^1 \Rightarrow b_1 \wedge b_3$,
```

and

```
$MP_3^1 \Rightarrow b_4 \wedge b_5$.
```

The minimal cuts are

```
$MC_1^1 \Rightarrow \overline{b_1} \wedge \overline{b_4}$,
```

```
$MC_2^1 \Rightarrow \overline{b_1} \wedge \overline{b_5}$,
```

```
$MC_3^1 \Rightarrow \overline{b_1} \wedge \overline{b_3} \wedge \overline{b_4}$,
```

and

```
$MC_4^1 \Rightarrow \overline{b_1} \wedge \overline{b_3} \wedge \overline{b_5}$.
```

Let us, for instance, apply the Esary-Proschan method introduced in Section 20.7.4, to calculate the probability bounds. Hence, using the minimal paths and the minimal cuts, we get $\rho_1^1 = p_1p_2, \rho_2^1 = p_1p_3, \rho_3^1 = p_4p_5, \gamma_1^1 = (1-p_4)(1-p_5), \gamma_2^1 = (1-p_1)(1-p_5), \gamma_3^1 = (1-p_1)(1-p_3)(1-p_4)$, and $\gamma_4^1 =$