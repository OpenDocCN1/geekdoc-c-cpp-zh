at each instance of real time $t$ for which $q$ is constant. When $q$ changes at time $(t,c)$, its subsequent value depends on $q((t,c))$ and $x((t,c))$; the new state at time $(t,c+1)$ is³

$$q((t,c+1)) = \Theta(x((t,c)), q((t,c))) \tag{5.29}$$

The discrete change in the differential function takes effect at time $(t,c+1)$, and $x$ evolves from its value at the transition. Because $x$ does not change discontinuously, the trajectory $x(t)$, which satisfies Equation 5.28 and is a function from $\mathbb{R} \to \mathbb{R}^m$, is equal to $x((t,c))$, a function from $\mathbb{R} \times \mathbb{N} \to \mathbb{R}^m$, for all $c \in \mathbb{N}$, and so the two technically distinct trajectories are interchangeable.

These systems can, of course, be modeled with a trivial hybrid system expressed in terms of differential functions, event surfaces, and discrete transitions. Specifically, it is the input/output-free system with $x$ as written above, $\dot{x}(t,x,q) = (x, \Theta(x,q))$, and $G$ is the time remaining until $\Theta$ changes value.

# ### 5.8.2 Modeling Asynchronous Cellular Automata with Differential Automata

The discrete states of a cellular automaton can be numbered by treating its leftmost cell as the most significant bit in a binary number and its rightmost as the least significant. An automaton with $n$ cells has $2^n$ discrete states. In addition to its binary state, each cell $k$ has a clock $\tau_k$ that induces events in two ways: beginning from zero, $\tau_k$ grows until it reaches the cell’s duration $P_k$; and beginning at $P_k$, $\tau_k$ shrinks until it reaches zero. The direction of the clock is the cell’s third and final state variable.

The pair $(b_k,d_k)$ is the discrete state of cell $k$, where $b_k \in \{0,1\}$ is the binary state and $d_k \in \{1,-1\}$ is the direction of the clock; the set of discrete states is $Q = \{0,1\} \times \{1,-1\}$. The clock $\tau_k$ begins, and remains, in the interval $[0,P_k]$. The differential automaton that models the cell is

$$\dot{\tau}_k = d_k \tag{5.30}$$

$$\Theta_k(\tau_k,(b_k,d_k)) = \begin{cases}(T(b_{k,l},b_{k,r}),-d_k) & \text{if }(\tau_k=0 \land d_k=-1) \\(b_k,-d_k) & \text{if }(\tau_k=P_k \land d_k=1) \\(b_k,d_k) & \text{otherwise}\end{cases} \tag{5.31}$$

where $T$ is as defined by Equation 4.21.

A cellular automaton with $n$ cells is a differential automaton with the set of discrete states $Q^n$ and the continuous state vector $\tau = [\tau_1\ \tau_2\ \cdots\ \tau_n]$. The dynamic equations

³The symbol $\Phi$ commonly denotes the discrete transition function of a differential automata, but this conflicts with our use of it for the nonevent, hence $\Theta$.