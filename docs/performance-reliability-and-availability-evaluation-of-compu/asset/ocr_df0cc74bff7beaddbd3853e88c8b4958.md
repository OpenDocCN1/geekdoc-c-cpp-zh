# Reliability Block Diagram

$R_a(t) 	imes R_b(t)-2 	imes (R_a(t) + R_b(t)) + 4-2 	imes R_a(t) 	imes R_b(t) + \frac{2 	imes R_a(t) 	imes R_b(t)}{2-R_a(t) 	imes R_b(t)}$

$2-R_a(t) 	imes R_b(t)-2 	imes (R_a(t) + R_b(t)) + \frac{2 	imes R_a(t) 	imes R_b(t)}{2-R_a(t) 	imes R_b(t)} =$

$2-R_a(t) 	imes R_b(t) + \frac{2 	imes R_a(t) 	imes R_b(t)-2 	imes (R_a(t) + R_b(t))}{2-R_a(t) 	imes R_b(t)} =$

which finally leads to

$1+2 	imes \frac{1-(R_a(t) + R_b(t)) + R_a(t) 	imes R_a(t)}{2-R_b(t) 	imes R_b(t)}$.

As $R_a(t) \in [0, 1]$ and $R_b(t) \in [0, 1], \frac{R_{52}(t)} \ge 1$.

Therefore, component redundancy (Figure 18.25.c) is more reliable than system redundancy (Figure 18.25.b) [381].

**Example 18.6.1.** Assume the times to failure of the components of the systems shown in Figure 18.25 are exponentially distributed with rate $\lambda_1 = \lambda_2 = 10^{-4} f/h$, respectively. The reliability of system $S$ and the respective redundant systems $S_1$ (system redundancy) and $S_2$ (component redundancy) are depicted in Figure 18.26. It is worth noting the higher reliability of the component redundant system $R_{52}(t)$.

![](bbox=[0.213, 0.591, 0.786, 0.846])

**Figure 18.26** System Redundancy and Component Redundancy Reliabilities.