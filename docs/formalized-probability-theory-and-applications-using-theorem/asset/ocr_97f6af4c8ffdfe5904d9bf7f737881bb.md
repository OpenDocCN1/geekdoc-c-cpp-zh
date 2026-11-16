function (PMF) as Pr (D_t = i) = a_j, where i = 1, 2, ..., n refers to the position of the least recently used page in the stack at time t, and \sum_{j=1}^n a_j = 1. This way the distribution function becomes Pr (D_t \le i) = \sum_{j=1}^i a_j. Now, if a tagged page occupies the i^{th} position in the stack at time t, which is expressed as s_t in Figure 1, then the position of this page in the stack s_{t+1} depends on the next reference x_{s_t} and the position of this page in the stack s_t.

Based on the described updating procedure in the LRU stack, the evaluation of the page-fault rate of the LRU paging algorithm becomes quite simple. If the evaluated program has been allocated i page frames of main memory, then a page fault will occur at time t when D_t > i. Hence, the page fault probability is

F (LRU) = Pr (D_t > i) = 1 - \sum_{j=1}^i a_j \quad (7.2)

The movement of the tagged page through the LRU state is then a random process \{ E_t \}_{t \ge 0}. If the page occupies the i^{th} position in the stack s_t, then E_t = i, for all 1 \le i \le n. Now, we have the following transition probabilities:

p_{ii} = Pr (E_{t+1} = i | E_t = i) = Pr (D_{t+1} = i) = a_i, 1 \le i \le n
p_{ii} = Pr (E_{t+1} = i | E_t = i) = Pr (D_{t+1} < i) = \sum_{j=1}^{i-1} a_{i-j}, 2 \le i \le n
p_{i, i+1} = Pr (E_{t+1} = i+1 | E_t = i) = Pr (D_{t+1} > i) = 1 - \sum_{j=1}^i a_{i-j}, 1 \le i \le n-1
p_{ij} = 0, otherwise.

The LRU stack is then described as an aperiodic and irreducible DTMC by assuming a_i > 0 for all i \in [1, n].

The state diagram of this aperiodic and irreducible DTMC is shown in Figure 2, where the transition probabilities can be expressed as the following higher-order logic function: