# Table 18.6

| Component | MTTF ($h$) | $\lambda (f/h)$ |
|---|---|--|
| MB | 430000 | $2.32555 	imes 10^{-6}$ |
| NC | 220000 | $4.54545 	imes 10^{-6}$ |
| VC | 185000 | $5.40541 	imes 10^{-6}$ |
| DC | 140000 | $7.14286 	imes 10^{-6}$ |
| D | 120000 | $8.33333 	imes 10^{-6}$ |
| S | 50000 | $2.00 	imes 10^{-5}$ |
| OS | 2000 | $5 	imes 10^{-4}$ |
| $A_1$ | 1500 | $6.67 	imes 10^{-4}$ |
| $A_{21}$ | 1800 | $5.56 	imes 10^{-4}$ |
| $A_{22}$ | 1800 | $5.56 	imes 10^{-4}$ |
| $A_3$ | 1600 | $6.25 	imes 10^{-4}$ |

# Table 18.7

Time to Repair - Parameters

| Component | MTTR ($h$) | $\mu (r/h)$ |
|---|---|--|
| $H_w$ | 20 | $5 	imes 10^{-2}$ |
| OS | 4 | $2.5 	imes 10^{-1}$ |
| $A_1$ | 0.5 | 2 |
| $A_{21}$ | 0.5 | 2 |
| $A_{22}$ | 0.5 | 2 |
| $A_3$ | 0.50 | 2 |

# KooN

A system that is operational at least $K$ out of $N$ components is called a $KooN$ structure. A series system is, therefore, a $Noon$ structure, whereas parallel composition is a $1ooN$ structure. NMR redundancies are represented by $KooN$ structures. Structures like $K$ out of $N$, bridges, delta and star arrangements [224] have been represented by RBD; nevertheless such structures can only be represented if the components are replicated in the model [246].

Consider a data center with an ordered set of $N$ similar servers, where $\mathbf{X_N} = (x_1, x_2, x_n)$ denotes the data center state, and $x_i$ represents the state of the server $i$. Servers are observed during period. At the end of the period, each server can be in one of two states, operational ($x_i = 1$) or failed ($x_i = 0$). Assume the data center is considered operational if $K$ out of the $N$ servers are operational. If