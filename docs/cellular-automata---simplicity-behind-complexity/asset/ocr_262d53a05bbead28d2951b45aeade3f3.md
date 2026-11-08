instead the original $Z_d$, which means the space of cellular automata dosen't have to be Euclid space. It could be a network or graph structure. Accordingly the $N$ in the cellular automata may follow the graph's neighbourhood definition. Further more, the $N$ dosen't have to be stable. $\sigma: N \to N$ is the neighbourhood transformation function, which can change the neighbourhood in every evolution step of the cellular automata. $P$ stands for the public information. Accordingly the state transition function becomes $\delta: P,S^{s+1}\to S$.

Although we extended the definition from classic cellular automata, we still kept its essential features. The new kinds of cellular automata are still time-space discrete system. Each cell decides its state in next step according to the states of neighbours and itself in current step. The macrodynamics of cellular automata is the emergence of masses of cells' adaptive behaviours. The classic cellular automaton could be regarded as an instance of the new definition. Because the cells could be heterogeneous, a cellular automaton under new definition could also be a multi-agent system.

New definition of cellular automata gives us a foundation to define a cellular automata based artificial financial market. Because there could be many artificial financial markets under different assumptions, we just define the general part of them. In a cellular automata based artificial financial market, each cell represents an investor. $Z$ in the formula (4) is the set of cells. In cellular automata based artificial financial market, the finite states set $S$ is a 6-tuple:

$$S = (C_u, C_f, S_u, S_f, Q, E) \tag{5}$$

$C_u$ and $C_f$ stand for usable and frozen cash respectively. $S_u$ and $S_f$ are usable and frozen stock respectively. $Q$ is the set of orders which have been quoted to exchange house but have not been completed or canceled yet. Each order includes direction (ask or bid), price and amount. $E$, which valued rise, fall, or keeping, is the price prediction of an investor. $C_p$ is the total property of an investor. Given $P$ as current stock price, $C_p$ can be expressed as follows:

$$C_p = C_u + C_f + P(S_u + S_f) \tag{6}$$

Maximization of $C_p$ is the only goal for all investors.
$N$ is the neighborhood in cellular automata. In this ASM, $N$ is a directed graph. When $Cell_i$ is making a prediction, a directed edge <i, j> between $Cell_i$ and $Cell_j$ exists only if the $S_E$ value of $Cell_j$ can affect the $S_E$ value of $Cell_i$. In this condition, $Cell_j$ is defined as a neighbor of $Cell_i$. The neighbour relationship between these two cells is not self reciprocal.

In the cellular automata based artificial financial market, public information includes trading data, public financial policy, such as risk free rate, and company news, such as financial reports and bonus. As the definition of cellular automata, public information is represented by $P$. The state transition function decide a cell's state according to the public information and the states of the cell self and the neighbours. So is defined as.

$$\delta: P, S^{s+1} \to S \tag{7}$$

The neighborhood transition function is:

$$\sigma: N \to N \tag{8}$$

$\sigma$ is the variance of the dependency relationship between cells. Based on different assumptions, methods to rebuild the dependency networks can be different. $\sigma$ would be performed after each trading day.