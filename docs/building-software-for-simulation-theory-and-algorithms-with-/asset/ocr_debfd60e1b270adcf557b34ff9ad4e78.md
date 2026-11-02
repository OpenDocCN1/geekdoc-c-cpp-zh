![](bbox=[0.243, 0.11, 0.786, 0.328])

**FIGURE 4.12** Output of the computer in response to a packet that sets a 50% duty ratio for the right motor and 75% for the left motor. The frequency of the computer’s clock is 7.4 kHz.

the discrete-event system

$$S = \{0, 1\}$$

$$X = Y = S \times \mathbb{N}$$

$$\delta_{int}(s) = s$$

$$\delta_{ext}(s, e, \{(b_l, k - 1), (b_r, k + 1)\}) = T(b_l, s, b_r)$$

$$\delta_{con}(s, x^b) = \delta_{ext}(s, 0, x^b)$$

$$\lambda(s) = (s, k)$$

$$ta(s) = 1$$

which models a cell at location $k$. For the moment, assume that each cell begins with its elapsed time equal to 1. If $N$ of these cells are connected to identical neighbors, differing only in $k$, to form a ring, then the output trajectories have nonevents except at $t = (m, 0)$, where $m \in \mathbb{N}$. Likewise, the input trajectories are $\Phi$ except at $t = (m, 0)$, where their values are $\{(b_r, k + 1), (b_l, k - 1)\}$ for $k \in [1, N - 1]$; for the cell at $k = 1$, the input values arrive from $N$ and 2; similarly for the cell at $k = N$. The state trajectories change in the discrete instant following an input, that is, from state $s$ at $t = (m, 0)$ to state $T(b_l, s, b_r)$ at $(m, 1)$.

The discrete-time cell is quite similar in form. It has identical sets of states, inputs, and outputs; an identical output function; and the state transition function is

$$\delta(s, \{(b_l, k - 1), (b_r, k + 1)\}) = T(b_l, s, b_r) \tag{4.21}$$