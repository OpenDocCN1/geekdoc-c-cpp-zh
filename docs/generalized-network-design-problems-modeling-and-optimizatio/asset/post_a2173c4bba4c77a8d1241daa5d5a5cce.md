
lower bounds as a percentage of the upper bound of the GMSTP (LB/UB), and the computation times (CPU) in seconds for solving the GMSTP with a branch and cut algorithm (see [37]). In the last two columns '-' means that for those instances, [37] did not provide computational results.

It is important to notice that we were able to obtain the optimal solution of the GMSTP, using our simulated annealing combined with a local greedy algorithm, for all instances considered.

From Table 2.2, we observe that, for instances up to 140 nodes, in the case of simulated annealing, computation times were longer, compared with the computation times corresponding to the other methods. However, for larger instances, while the computation times for the rooting procedure increase exponentially, the computation times in the case of simulated annealing are reasonable.

For medium and large instances of the GMSTP (graphs which contain more than 50 clusters and 200 nodes), we compare the results of our SA to Variable Neighborhood Search (VNS) (Hu, Leitner and Raidl [77]), Tabu Search with recency and frequency based memory (TS) (Ghosh [49]), and, in the case of TSPlib instances, also to the Genetic Algorithm (GA) from Golden, Raghavan and Stanojevic [53].

The algorithms have been tested on two kinds of instances. One was introduced by Ghosh [49], who created three types of benchmark instances called grouped Euclidean, random Euclidean, and non-Euclidean random instances, and the other one applies geographical clustering (see Fischetti et al. [43]) on TSPlib instances. In the case of the grouped Euclidean instances, squares with side length span were associated with clusters and were regularly distributed on a grid of size col x row. The nodes of each cluster are randomly distributed, within the corresponding square. For the second type of benchmark instances, the nodes belonging to the same cluster are not necessarily close to each other, since they are randomly generated within a square of size 1000 x 1000 and randomizing the cluster assignment. In these two cases, the cost of the edges is given by the Euclidean distance between the nodes. Finally, in the case of the non-Euclidean random benchmark instances, the cost of the edges was randomly chosen in the integer interval [0, 1000]. All considered graphs have a complete set of edges. The details about these benchmark instances are listed in the Tables 2.3 and 2.4.

In the next two tables, Table 2.5 and 2.6, we present the names of the instance, number of nodes, (average) number of nodes per cluster, and (average) objective values of the final solutions, as obtained by the different algorithms. The best values are printed bold. In case of SA and VNS, we also provide corresponding standard deviations, denoted by $\sigma$, of objective values.

In Table 2.5, we compare our SA to TS, VNS and VNDS on grouped Euclidean instances, random Euclidean instances, and non-Euclidean instances.

Analyzing the results in Tables 2.5 and 2.6, we observe that, among the considered approaches, VNS and TS are overall the most powerful algorithms.

## Table 2.2. Computational results for solving the GMSTP.

| Pb. size | | SA algorithm | | Rooting procedure | | Branch and cut | |
|---|---|---|---|---|---|---|---|
| m | n | UB/OPT | CPU | LB/OPT | CPU | LB/UB | CPU |
| 8 | 24 | 100 | 2.6 | 100 | 0.0 | 100 | 0.0 |
| | 32 | 100 | 3.7 | 100 | 0.0 | 100 | 0.2 |
| | 48 | 100 | 5.6 | 100 | 0.3 | 100 | 1.4 |
| | 80 | 100 | 10.2 | 100 | 2.2 | 100 | 4.2 |
| 10 | 30 | 100 | 4.8 | 100 | 0.2 | 100 | 1.0 |
| | 40 | 100 | 6.7 | 100 | 0.3 | 100 | 1.0 |
| | 60 | 100 | 10.8 | 100 | 0.7 | 100 | 3.2 |
| | 100 | 100 | 20.6 | 100 | 1.9 | 100 | 8.8 |
| 12 | 36 | 100 | 8.3 | 100 | 0.7 | 100 | 1.8 |
| | 48 | 100 | 11.6 | 100 | 0.9 | 99.2 | 3.2 |
| | 72 | 100 | 19.1 | 100 | 3.7 | 100 | 6.8 |
| | 120 | 100 | 39.0 | 100 | 9.3 | - | - |
| 15 | 45 | 100 | 16.6 | 100 | 1.3 | 100 | 3.6 |
| | 60 | 100 | 21.6 | 100 | 1.7 | 97.1 | 6.2 |
| | 90 | 100 | 39.7 | 100 | 9.6 | 100 | 21.4 |
| | 150 | 100 | 80.2 | 100 | 34.1 | 98.8 | 42.4 |
| 18 | 54 | 100 | 27.2 | 100 | 2.6 | 99.5 | 7.6 |
| | 108 | 100 | 68.1 | 100 | 13.8 | - | - |
| | 180 | 100 | 143.8 | 100 | 150.4 | - | - |
| 20 | 60 | 100 | 37.5 | 100 | 7.2 | - | - |
| | 120 | 100 | 181.9 | 100 | 33.2 | 96.3 | 39.8 |
| | 200 | 100 | 219.8 | 100 | 203.8 | 94.6 | 191.4 |
| 25 | 75 | 100 | 80.8 | 100 | 17.5 | - | - |
| | 150 | 100 | 221.7 | 100 | 266.4 | 88.3 | 178.8 |
| | 200 | 100 | 331.1 | 100 | 284.5 | 97.8 | 140.6 |
| 30 | 90 | 100 | 150.4 | 100 | 60.2 | - | - |
| | 180 | 100 | 412.0 | 100 | 721.8 | 96.6 | 114.6 |
| | 240 | 100 | 627.4 | 100 | 1948.9 | - | - |
| 40 | 120 | 100 | 382.1 | 100 | 142.6 | 100 | 92.6 |
| | 160 | 100 | 561.0 | 100 | 572.3 | 94.2 | 288.6 |
| | 280 | 100 | 691.2 | 100 | 25672.3 | - | - |

## Table 2.3. Benchmark instances adopted from Ghosh [49]. Each instance has a constant number of nodes per cluster.

| Instance set | |V| | |E| | r | |V|/r | col | row | sep | span |
|---|---|---|---|---|---|---|---|---|---|---|
| Grouped Eucl 125 | 125 | 7750 | 25 | 5 | 5 | 5 | 10 | 10 |
| Grouped Eucl 500 | 500 | 124750 | 100 | 5 | 10 | 10 | 10 | 10 |
| Grouped Eucl 600 | 600 | 179700 | 20 | 30 | 5 | 4 | 10 | 10 |
| Grouped Eucl 1280 | 1280 | 818560 | 64 | 20 | 8 | 8 | 10 | 10 |
| Random Eucl 250 | 250 | 31125 | 50 | 5 | - | - | - | - |
| Random Eucl 400 | 400 | 79800 | 20 | 20 | - | - | - | - |
| Random Eucl 600 | 600 | 179700 | 20 | 30 | - | - | - | - |
| Non-Eucl 200 | 200 | 19900 | 20 | 10 | - | - | - | - |
| Non-Eucl 500 | 500 | 124750 | 100 | 5 | - | - | - | - |
| Non-Eucl 600 | 600 | 179700 | 20 | 30 | - | - | - | - |

## Table 2.4. TSPlib instances with geographical clustering, from Feremans [37]. Numbers of nodes varies for each cluster.

| Name of instance | |V| | |E| | r | |V|/r | d_min | d_max |
|---|---|---|---|---|---|---|---|---|
| gr137 | 137 | 9316 | 28 | 5 | 1 | 12 |
| kroa150 | 150 | 11175 | 30 | 5 | 1 | 10 |
| d198 | 198 | 19503 | 40 | 5 | 1 | 15 |
| kroB200 | 200 | 19900 | 40 | 5 | 1 | 8 |
| gr202 | 202 | 20301 | 41 | 5 | 1 | 16 |
| ts225 | 225 | 25200 | 45 | 5 | 1 | 9 |
| pr226 | 226 | 25425 | 46 | 5 | 1 | 16 |
| gil262 | 262 | 34191 | 53 | 5 | 1 | 13 |
| pr264 | 264 | 34716 | 54 | 5 | 1 | 12 |
| pr299 | 299 | 44551 | 60 | 5 | 1 | 11 |
| lin318 | 318 | 50403 | 64 | 5 | 1 | 14 |
| rd400 | 400 | 79800 | 80 | 5 | 1 | 11 |
| fl417 | 417 | 86736 | 84 | 5 | 1 | 22 |
| gr431 | 431 | 92665 | 87 | 5 | 1 | 62 |
| pr439 | 439 | 96141 | 88 | 5 | 1 | 17 |
| pcb442 | 442 | 97461 | 89 | 5 | 1 | 10 |

## Table 2.5. Results on instance sets from Ghosh [49].

| Set | |V| | r | |V|/r | TS C(T) | VNDS C(T) | SA C(T) | σ | VNS C(T) | σ |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Grouped Eucl 125 | 125 | 25 | 5 | 141.1 | 141.1 | 152.3 | 0.52 | 141.1 | 0.00 |
| | 125 | 25 | 5 | 133.8 | 133.8 | 150.9 | 0.74 | 133.8 | 0.00 |
| | 125 | 25 | 5 | 143.9 | 145.4 | 156.8 | 0.00 | 141.4 | 0.00 |
| Grouped Eucl 500 | 500 | 100 | 5 | 566.7 | 577.6 | 642.3 | 0.00 | 567.4 | 0.57 |
| | 500 | 100 | 5 | 578.7 | 584.3 | 663.3 | 1.39 | 585.0 | 1.32 |
| | 500 | 100 | 5 | 581.6 | 588.3 | 666.7 | 1.81 | 583.7 | 1.82 |
| Grouped Eucl 600 | 600 | 20 | 30 | 85.2 | 87.5 | 93.9 | 0.00 | 84.6 | 0.11 |
| | 600 | 20 | 30 | 87.9 | 90.3 | 99.5 | 0.28 | 87.9 | 0.00 |
| | 600 | 20 | 30 | 88.6 | 89.4 | 99.2 | 0.17 | 88.5 | 0.00 |
| Grouped Eucl 1280 | 1280 | 64 | 20 | 327.2 | 329.2 | 365.1 | 0.46 | 315.9 | 1.91 |
| | 1280 | 64 | 20 | 322.2 | 322.5 | 364.4 | 0.00 | 318.3 | 1.78 |
| | 1280 | 64 | 20 | 332.1 | 335.5 | 372.0 | 0.00 | 329.4 | 1.29 |
| Random Eucl 250 | 250 | 50 | 5 | 2285.1 | 2304.9 | 2584.3 | 23.82 | 2300.9 | 40.27 |
| | 250 | 50 | 5 | 2183.4 | 2343.3 | 2486.7 | 0.00 | 2201.8 | 23.30 |
| | 250 | 50 | 5 | 2048.4 | 2263.7 | 2305.0 | 16.64 | 2057.6 | 31.58 |
| Random Eucl 400 | 400 | 20 | 20 | 557.4 | 725.9 | 665.1 | 3.94 | 615.3 | 10.8 |
| | 400 | 20 | 20 | 724.3 | 839.0 | 662.1 | 7.85 | 595.3 | 0.00 |
| | 400 | 20 | 20 | 604.5 | 762.4 | 643.7 | 14.54 | 587.3 | 0.00 |
| Random Eucl 600 | 600 | 20 | 30 | 541.6 | 656.1 | 491.8 | 7.83 | 443.5 | 0.00 |
| | 600 | 20 | 30 | 540.3 | 634.0 | 542.8 | 25.75 | 573.0 | 10.2 |
| | 600 | 20 | 30 | 627.4 | 636.5 | 469.5 | 2.75 | 469.0 | 11.9 |
| Non-Eucl 200 | 200 | 20 | 10 | 71.6 | 94.7 | 76.9 | 0.21 | 71.6 | 0.00 |
| | 200 | 20 | 10 | 41.0 | 76.6 | 41.1 | 0.02 | 41.0 | 0.00 |
| | 200 | 20 | 10 | 52.8 | 75.3 | 86.9 | 5.38 | 52.8 | 0.00 |
| Non-Eucl 500 | 500 | 100 | 5 | 143.7 | 203.2 | 200.3 | 4.44 | 152.5 | 3.69 |
| | 500 | 100 | 5 | 132.7 | 187.3 | 194.3 | 1.20 | 148.6 | 4.27 |
| | 200 | 20 | 10 | 162.3 | 197.4 | 205.6 | 0.00 | 166.1 | 2.89 |
| Non-Eucl 600 | 600 | 20 | 30 | 14.5 | 59.4 | 22.7 | 1.49 | 15.6 | 1.62 |
| | | 20 | 30 | 5 | 17.7 | 23.7 | 22.0 | 0.82 | 16.1 | 1.24 |
| | | 600 | 20 | 30 | 15.1 | 29.5 | 22.1 | 0.44 | 16.0 | 1.66 |
