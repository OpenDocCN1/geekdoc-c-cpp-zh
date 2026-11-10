
```
End For
Update the trail pheromone intensity for every edge (i, j)

τ_ij(t) = ρτ_ij(t − 1) + Σ_{k=1}^{n} Δτ_ij^k(t) ∀(i, j)

Δτ_ij^k(t) = { Q/L_k(t)  if the edge (i, j) chosen by ant_k
                0          otherwise }

Compare and update the best solution
End For
End While
```

## 15.9 Studies and Applications of Swarm Intelligence

In this section a few illustrations based on scientific and engineering swarm intelligence studies are given.

### 15.9.1 Ant-based Routing

Dorigo et al. and Hewlett-Packard during the mid-1990s applied Swarm Intelligence to the field of Telecommunication Networks and referred to this as Ant-Based Routing. The application involves a probabilistic routing table rewarding or reinforcing the route successfully traversed by each "ant" (a small control packet). Reinforcement of the route in the forward, reverse direction and both simultaneously have been studied and analyzed in their research. A symmetric network is used for backward reinforcement, which couples the network bidirectionally. The forward reinforcement rewards a route before the outcome is known.

### 15.9.2 Clustering Behavior of Ants

The main idea of the clustering algorithm based on swarm intelligence was proposed by Deneubourg. The process of clustering is defined in three stages. In the first stage, the data objects are chosen at random and are projected onto a low dimensional space. During the second phase, simple agents perceive the swarm similarity of the current object with the local region, and compute the probability of pick-up and drop. And finally during the third phase, the cluster centers are formed by the simple agents based on collective behavior.

### 15.9.3 Graph Coloring

Graph coloring was used as a benchmark for solving distributed constraint satisfaction problems is offered. All the agents in the space correspond one-to-one with the nodes of the proposed graph. The agents whose nodes are directly connected are enemies; agents whose nodes are at shortest graph distance are friends. Usually the agents are attracted to friends while moving from one place to the other such as to avoid enemies. The colors for the graph coloring correspond to specific attraction spatial regions and the agents are attracted toward these regions. The graph coloring solution is given by the distribution of the agents over the color attraction regions. If all the agents are placed in one of the color attraction space regions, the system configuration can be interpreted as defining a complete coloration of the graph. If some agents are outside these regions, the system configuration corresponds to a partial solution to the coloration problem.

### 15.9.4 Machine Scheduling

Machine scheduling application is used to assign a set of machines \(M_1, M_2, \ldots, M_n\) to a set of jobs \(J_1, J_2, \ldots, J_m\). Each job consists of a set of operations \(O_{j1}, O_{j2}, \ldots, O_{jm}\) and the machines are assigned jobs based on certain constraints like

- A machine can perform only one operation at a time
- The operations on different jobs do not have any priority
- A running operation cannot be interrupted

Let \(T_i\) represent the time taken for a machine \(M_i\) to complete an operation \(O_{jk}\). Let \(\sum T_i\) denote the time taken by a machine \(M_i\) to complete all the assigned jobs. Thus the objective of a machine scheduling problem is to minimize the maximum completion time defined as \(\max\{\sum T_i\}\) and to minimize the sum of completion times defined as \(\sum_{i=1}^{n}\{\sum T_i\}\).

For machine scheduling problems the parameters of PSO algorithm are initialized as follows:

- Learning vectors \(c_1 = c_2 = 1.49\)
- Inertia weight \(w = 0.9\) initially and gradually decreased to \(0.1\)
- Particle size = 20

The parameters used for machine scheduling problem by applying the ACO algorithm are as follows:

- Number of ants = 5
- Weight of pheromone trail \(\alpha = 1\)
- Weight of heuristic information \(\beta = 5\)
- Pheromone evaporation parameter \(\rho = 0.8\)
- Constant for pheromone updating \(Q = 10\)

### 15.9.5 Quadratic Knapsack Problem

The 0-1 quadratic knapsack problem (QKP) is a hard computational problem, which is a generalization of the knapsack problem (KP). This problem was introduced by Gallo, which was used to choose elements from n items for maximizing a quadratic profit objective function subject to a linear capacity constraint. The problem is defined as follows:

Objective: To maximize
\[
f(x) = \sum_{i=1}^{n} p_i x_i + \sum_{i=1}^{n-1} \sum_{j=i+1}^{n} p_{ij} x_i x_j
\]

Subject to the constraint:
\[
g(x) = \sum_{i=1}^{n} w_i x_i - C \le 0
\]

where \(p_i\) and \(p_{ij}\) are profit coefficients, \(w_i\) is weight coefficient and \(C\) denotes the capacity of the knapsack. All these coefficients are non-negative integers. \(x_i\) denotes the item that is to be selected.

The best choice of parameters used by PSO algorithm for solving the QKP problem can be initialized as follows:

- Learning vectors \(c_1 = c_2 = 1.49445\)
- Inertia weight \(w = 0.729\) initially and gradually decreased to \(0.1\)
- Particle size = 20
- Range and dimension of particles = \(2.8 \times 10^9\)

The best choice of parameters used by ACO algorithm for solving the QKP problem can be initialized as follows:

- Number of ants = 30
- Weight of pheromone trail \(\alpha = 1\)
- Weight of heuristic information \(\beta = 5\)
- Pheromone evaporation parameter \(\rho = 0.01\)
- Constant for pheromone updating \(Q = 10\)

### 15.9.6 Traveling Salesman Problem

The objective of the traveling salesman problem is defined to visit a number of cities, plan the trip such that every city is visited at least once and that the whole trip is as short as possible. The Traveling Salesman Problem (TSP) is a simple combinatorial problem in computational mathematics. The salesman starts from a city and travels through n number of cities cyclically. Once he has visited all the cities he finishes up where he started. The constraint is to minimize the distance traveled and such as to find a proper order of the cities to be traveled. More formally, the TSP can be represented by a complete weighted graph \(G = (N,A)\) where \(N\) denotes the set of nodes, representing the cities, and \(A\) the set of arcs fully connecting the nodes \(N\). Each arc is assigned a value \(d_{ij}\), which is the length of arc \((i, j) \in A\), that is, the distance between cities i and j, with \(i, j \in N\).

The best choice of parameters used by PSO algorithm for solving the TSP problem can be initialized as follows:

- Learning vectors \(c_1 = c_2 = 1\)
- Inertia weight \(w =\) initially and gradually decreased to \(0.1\)
- Particle size = 20

The best choice of parameters used by ACO algorithm for solving the TSP problem can be initialized as follows:

- Number of ants = 25
- Weight of pheromone trail \(\alpha = 1\)
- Weight of heuristic information \(\beta = 2\)
- Pheromone evaporation parameter \(\rho = 0.2\)
- Constant for pheromone updating \(Q = 20\)

## 15.10 MATLAB Examples of Swarm Intelligence

A few applications of Particle Swarm Optimization and Ant Colony Optimization such as Traveling Salesman Problem (TSP), Quadratic Assignment Problem (QAP), behavior and simulation of swarms in MATLAB are explained in this section.

### 15.10.1 Illustration 1: Simulation of the Movement of Swarm to Minimize the Objective Function

```matlab
%% Particle Swarm Optimization Simulation
% Simulates the movements of a swarm to minimize
% the objective function
% (x - 15)^2 + (y - 20)^2

% The swarm matrix is
%
% swarm(index, [location, velocity, best position, best
% value], [x, y components or the value component])
%
%
% Initialization
% Parameters
clear
clc
iterations = 30;
inertia = 1.0;
correction.factor = 2.0;
swarm.size = 49;
% - - - - initial swarm position - - - -
index = 1;
for i = 1 : 7
    for j = 1 : 7
    swarm(index, 1, 1) = i;
    swarm(index, 1, 2) = j;
    index = index + 1;
    end
end

swarm(:, 4, 1) = 1000; % best value so far
swarm(:, 2, :) = 0;     % initial velocity
% Iterations
for iter = 1 : iterations

    %- - evaluating position & quality - - -
    for i = 1 : swarm.size
    swarm(i, 1, 1) = swarm(i, 1, 1) + swarm(i, 2, 1)/1.3;
    % update x position
```
