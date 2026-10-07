# Combinatorial Model Analysis

# 173

![](bbox=[0.247, 0.103, 0.752, 0.246])

# **Figure 20.1** Enumeration – RBD.

Table 20.1 shows the enumeration of all system states $(X_i, i = \{0,1,...,15\})$ and the respective evaluation of the structure function. The system probability (reliability and availability) computation takes into account the state $X=(x_3,x_2,x1,x0)$ that evaluates structure function to one. Therefore, in this specific example, the states of interest are only $(0,0,0,1), (0,1,1,1), (1,0,1,1), (1,1,0,1),$ and $(1,1,1,1)$.

# **Table 20.1**
State Enumeration – RBD Shown in Figure 20.1

| $E_i$ | $x_3$ | $x_2$ | $x_1$ | $x_0$ | $\Phi(X)$ |
| $E_0$ | 0 | 0 | 0 | 0 | 0 |
| $E_1$ | 0 | 0 | 1 | 0 | 0 |
| $E_2$ | 0 | 1 | 0 | 1 | 0 |
| $E_3$ | 0 | 0 | 1 | 1 | 1 |
| $E_4$ | 0 | 1 | 0 | 0 | 0 |
| $E_5$ | 0 | 1 | 0 | 1 | 0 |
| $E_6$ | 0 | 1 | 1 | 0 | 0 |
| $E_7$ | 0 | 1 | 1 | 1 | 1 |
| $E_8$ | 1 | 0 | 0 | 0 | 0 |
| $E_9$ | 1 | 0 | 0 | 1 | 0 |
| $E_{10}$ | 1 | 0 | 1 | 0 | 0 |
| $E_{11}$ | 1 | 0 | 1 | 1 | 1 |
| $E_{12}$ | 1 | 1 | 0 | 0 | 0 |
| $E_{13}$ | 1 | 1 | 0 | 1 | 1 |
| $E_{14}$ | 1 | 1 | 1 | 0 | 0 |
| $E_{15}$ | 1 | 1 | 1 | 1 | 1 |

> $^1\mathbb{N}^* = \mathbb{N} \cup \{0\}$.