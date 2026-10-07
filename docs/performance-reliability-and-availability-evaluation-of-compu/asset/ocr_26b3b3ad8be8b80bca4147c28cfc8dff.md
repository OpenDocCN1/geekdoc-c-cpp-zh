# Combinatorial Model Analysis

Table 20.9 in which $\Phi(X) = 1$ and summing the probabilities of the lines. An alternative is calculating the system unreliability by multiplying the unreliabilities of each component $\Phi_p(X) = 0$ (Event $E0$) and subtracting from 1. Hence, the system unreliability is $UR(t) 	imes UR(t) 	imes UR(t) = UR^3(t) = (1 - R(t))^3$. Therefore, the system reliability is $1 - (1 - R(t))^3$.

# Table 20.9

# Three Components - Parallel System

| Event | $x_2$ | $x_1$ | $x_0$ | $\Phi_p(X)$ | $UR(t)$ | $UR(t)$ | $UR(t)$ |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $E_0$ | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| $E_1$ | 0 | 1 | 1 | 1 | $UR(t)$ | $UR(t)$ | $R(t)$ |
| $E_2$ | 0 | 1 | 0 | 1 | $UR(t)$ | $R(t)$ | $R(t)$ |
| $E_3$ | 1 | 0 | 0 | 1 | $UR(t)$ | $R(t)$ | $R(t)$ |
| $E_4$ | 1 | 0 | 1 | 1 | $R(t)$ | $UR(t)$ | $UR(t)$ |
| $E_5$ | 1 | 1 | 0 | 1 | $R(t)$ | $UR(t)$ | $UR(t)$ |
| $E_6$ | 1 | 1 | 0 | 1 | $R(t)$ | $R(t)$ | $UR(t)$ |
| $E_7$ | 1 | 1 | 1 | 1 | $R(t)$ | $R(t)$ | $R(t)$ |

The system reliability is computed from the line in which $\Phi_{203}(X) = 1$ (see Table 20.10); thus

> $UR(t) 	imes R(t) + R(t) 	imes UR(t) 	imes R(t) + R(t) 	imes R(t) 	imes UR(t) + R(t) 	imes R(t) 	imes R(t) = 
nR^2(t) 	imes UR(t) + R^2(t) 	imes UR(t) + R^3(t) = 
nR^2(t) 	imes (1 - R(t)) + R^2(t) 	imes (1 - R(t)) + R^3(t) 	imes (1 - R(t)) = 
3R^2(t) 	imes (1 - R(t)) + R^3(t) = 
3R^2(t) - 3R^3(t) + R^3(t) = 
3R^2(t) - 2R^3(t)$.