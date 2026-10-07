# 110 Performance, Reliability, and Availability Evaluation of Computational Systems

where $\sum_{j \in S} L_i(j)$ is the total number of states that yields the system to operational state $(\Phi(x_1, ..., x_{i-1}, x_{i+1}, ..., x_n) = 1)$ given the component $i$ is operational; $\sum_{j \in S} O_i(j)$ is the total number of states that yields the system to operational state $(\Phi(x_1, ..., x_{i-1}, 0, x_{i+1}, ..., x_n) = 1)$ given the component $i$ failed.

**Example 18.9.** Assume a system with the RBD shown in Figure 18.1. Table 18.8 presents the values of the structure function and of the indicator functions ($L_i$ and $O_i$) for each state, and Table 18.9 presents the structural importance for each component. Component $b_1$ is the most important component, since $L_1^B = 0.75$, and $L_1^2 = L_1^3 = 0.25$. Figure 18.28 also shows the structural importance of each component.

# Table 18.8

# Structure Function

| | $x_3$ | $x_2$ | $x_1$ | $\Phi(x_3,x_2,x_1)$ | $L_1$ | $O_1$ | $O_2$ | $O_3$ |
|---|---|---|---|---|---|---|---||
| | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| 2 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| 3 | 0 | 1 | 1 | 1 | 0 | 1 | 0 | 1 |
| 4 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 5 | 1 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |
| 6 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| 7 | 1 | 1 | 1 | 1 | 0 | 1 | 0 | 0 |

# Table 18.9 - $n = 3$

# Structural Importance - $n=3$

| Metrics | $b_1$ | $b_2$ | $b_3$ |
|---|---|---||}{
| $\Sigma L_i = \sum_{j=0}^n L_i(j)$ | 3 | 2 | 2 |
| $\Sigma O_i = \sum_{j=0}^n O_i(j)$ | 0 | 1 | 1 |
| $\Sigma L_i - \Sigma O_i$ | 3 | 1 | 1 |
| $L_i^B$ | 0.75 | 0.25 | 0.25 |

![](bbox=[0.856, 0.843, 0.879, 0.856])

The **reliability importance**, also called **Birnbaum importance** (B-Importance) of a component $i$ at time $t$ is defined by the partial derivative of the system reliability