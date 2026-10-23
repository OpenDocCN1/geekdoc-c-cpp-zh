# 3.2. Simulation results

The software simulation environment, developed in C++, allows us to interface with the P3-AT robot and its simulation environment (MobileSim). The arena used consists of three rooms with six targets randomly placed.

# 3.2.1. Learning phase

As far as the simulated robot is concerned, the task assigned to the robot consists of aiming for a target and avoiding obstacles along the way. When the target is found it is switched off and another target appears in the arena. The learning phase lasts until one of the two following conditions occurs: either the a_q averaged on the last 1000 patterns drops below 10⁻⁴, or after 5000 targets have been found.

like in the Skinner’s experiments [93] in order to maximize the RF. More details on the whole mathematical model are given in [12].

At the beginning of the learning phase, the robot randomly modulates the basic behaviors, due to the random initialization of the modulation parameters k_i^q (i = a, o, p), which determine the robot heading. During the learning process, the Motor Map-like algorithm corrects the parameters associated with each pattern. Fig. 10(a) shows the evolution of the k_i^{q1} for the pattern, i.e. q1 = 52274. The modulation parameters associated to all the emerged patterns used in the first part, during and at the end of the learning phase (for a total number of 15000 actions divided in three blocks of 5000) is shown in Fig. 10(b)-(d).

This evolution is typical in several other simulations (for other results see [18]), taken into account and gives an idea of the clustering process that occurs during learning, where the basins of attraction of the Turing patterns that are associated to the modulation parameters, change in space and

> Fig. 10. (a) Evolution of the k_i^f q1 for the emerged pattern (q1 = 52274). The evolution of the modulation parameters is shown in (b–d) where the solutions adopted at the beginning of the learning stage (b), between 5000 and 10000 movements (c) and for the last 5000 movements are shown. In the last picture the region associated with the pattern 52274 is also indicated.

![](bbox=[0.1, 0.115, 0.42, 0.315])

![](bbox=[0.5, 0.115, 0.82, 0.315])

![](bbox=[0.1, 0.33, 0.42, 0.53])

![](bbox=[0.5, 0.33, 0.82, 0.53])