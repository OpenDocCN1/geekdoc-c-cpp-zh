numerical test problems. The evolution of the bidding strategies by Anthony and Jennings (Anthony & Jennings, 2002) employed a fixed crossover and mutation probability based on the literatures. However, these recommended values may not perform at its best in the genetic algorithm as it has been proven that the parameter values are dependent on the nature of problems to be solved (Engelbrecht, 2002). In this experiment, the crossover and mutation rates are fine tuned with different combination of probabilities in order to discover the best combination of genetic operators’ probabilities. Thus, the main objective of this experiment is to improve the effectiveness of the bidding strategies by “hand tuning” the values of the crossover rate and mutation rate to allow a new combination of static crossover and mutation rates to be discovered. By improving the algorithm, more effective bidding strategies can be found during the exploration of the solution.

The experiment is subdivided into two parts. The first one varies the crossover rate and the second one varies the mutation rate. At the end of this experiment, the combination rate discovered is compared and empirically evaluated with the bidding strategies evolved in Anthony’s work (Anthony, 2003).

# 4.1 Experimental setup

Table 2 and 3 show the evolutionary and parameter setting for the genetic algorithm. The parameters setting in the simulated environment for the empirical evaluations are shown in Table 4. These parameters include the agent’s reservation price; the agent’s bidding time and the number of active auctions. The agent’s reservation price is the maximum amount that the agent is willing to pay for the item while the bidding time is the time allocated for the agent to obtain the user’s required item. The active auctions are the list of auctions that is ongoing before time t_max. Fig. 7 shows the pseudocode of the genetic algorithm.

| Representation | Real Values Number |
|---|---|
| Crossover | Extension Combination Operator |
| Mutation | Creep Operator |
| Selection | Tournament Selection |

Table 2. Genetic algorithm evolutionary setting

| Number of Generations | 50 |
|---|---|
| Number of Individuals | 50 |
| Elitism | 10% |
| Crossover Probability | 0.2, 0.4, 0.6, 0.8 |
| Mutation Probability | 0.2, 0.02, 0.002 |
| Termination Criteria | After 50 Generation |
| Number of Run | 10 |

Table 3. Genetic algorithm parameter setting