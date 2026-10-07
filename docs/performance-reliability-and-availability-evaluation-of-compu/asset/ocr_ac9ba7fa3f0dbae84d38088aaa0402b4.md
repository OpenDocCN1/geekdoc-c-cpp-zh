# Combinatorial Model Analysis 201

Let us first take the minimal cuts, and using the first term of Equation 20.5.2, we have

```
$Q_1 = P(MC_1) + P(MC_2) + P(MC_3) + P(MC_4) = q_1q_4 + q_2q_3q_4 + q_2q_5 + q_1q_3q_5$,
```

where $q_i = 1 - p_i$ is the failure probability of component $i$. If $q_i = 0.1, i \in \{1,2,3,4,5\}$, then

$Q_1 = 0.022, P_1 = 1 - Q_1 = 0.978$. Using the second term of Equation 20.5.2, we obtain

```
$Q_2 = Q_1 + P(MC_1 \cap MC_2) + P(MC_1 \cap MC_3) + P(MC_1 \cap MC_4) + \nP(MC_2 \cap MC_3) + P(MC_2 \cap MC_4) + \nP(MC_3 \cap MC_4) = Q_1 - q_1q_2q_3q_4 - q_1q_2q_5q_4 - q_1q_3q_5q_4 - \nq_1q_2q_3q_4 - q_2q_3q_5q_4 - q_1q_2q_5q_5$.
```

Thus, $Q_2 = 0.02149$ and $P_2 = 1 - Q_2 = 0.97851$.

Now, take into account the third term of Equation 20.5.2, so

```
$Q_3 = Q_2 + P(MC_1 \cap MC_2 \cap MC_3) + P(MC_1 \cap MC_2 \cap MC_3) + P(MC_1 \cap MC_2 \cap MC_3) + \nP(MC_1 \cap MC_2 \cap MC_3) = Q_2 + 4q_1q_2q_3q_4q_5$.
```

Hence, we have $Q_3 = 0.02153$ and $P_3 = 1 - Q_3 = 0.97847$. Now, finally, consider the fourth term of Equation 20.5.2. Hence,

```
$Q_4 = Q_3 + P(MC_1 \cap MC_2 \cap MC_3 \cap MC_4) = Q_3 - q_1q_2q_3q_4q_5$.
```

Thus, we get $Q_4 = 0.02152$ and $P_4 = 0.97848$, where $Q_4$ and $P_4$ are the exact results.

Now consider the minimal paths and take into account the first term of the Equation 20.5.2. Therefore

```
$P_1 = P(MP_1) + P(MP_2) + P(MP_3) + P(MP_4) = p_1p_2 + p_3p_4p_2 + p_1p_3p_5 + p_4p_5$.
```

If $p_i = p = 0.9, i \in \{1,2,3,4,5\}$, then